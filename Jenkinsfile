cat > Jenkinsfile << 'EOF'
pipeline {
  agent any
  tools { jdk 'jdk17'; nodejs 'node16' }
  environment {
    DOCKER_HUB    = credentials('dockerhub-credentials')
    DOCKER_IMAGE  = "${DOCKER_HUB_USR}/youtube-clone"
    IMAGE_TAG     = "${BUILD_NUMBER}"
    SCANNER_HOME  = tool 'sonar-scanner'
  }
  stages {
    stage('Clean')    { steps { cleanWs() } }
    stage('Checkout') { steps { git branch: env.BRANCH_NAME,
                          url: 'https://github.com/YOUR_USERNAME/youtube-devops.git' } }
    stage('Install')  { steps { sh 'npm ci' } }
    stage('SonarQube') {
      steps { withSonarQubeEnv('sonar-server') {
        sh "$SCANNER_HOME/bin/sonar-scanner -Dsonar.projectKey=youtube"
      } }
    }
    stage('Trivy FS') {
      steps { sh 'trivy fs --severity HIGH,CRITICAL --format table -o trivy-fs.txt .' }
    }
    stage('Docker Build') {
      steps { sh "docker build -t ${DOCKER_IMAGE}:${IMAGE_TAG} -t ${DOCKER_IMAGE}:latest ." }
    }
    stage('Push') {
      when { branch 'staging' }
      steps { withDockerRegistry(credentialsId: 'dockerhub-credentials') {
        sh "docker push ${DOCKER_IMAGE}:${IMAGE_TAG}"
        sh "docker push ${DOCKER_IMAGE}:latest"
      } }
    }
    stage('Deploy Staging') {
      when { branch 'staging' }
      steps { sh "docker rm -f youtube-clone || true; \
                  docker run -d --name youtube-clone -p 3000:80 ${DOCKER_IMAGE}:${IMAGE_TAG}" }
    }
  }
}
EOF