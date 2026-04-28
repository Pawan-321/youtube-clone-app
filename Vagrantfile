# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.boot_timeout = 600
  # ── K8s Master (192.168.56.11) ───────────────────────────────────
  config.vm.define "k8s-master" do |k8s|
    k8s.vm.box = "ubuntu/focal64"
    k8s.vm.hostname = "k8s-master"
    k8s.vm.network "private_network", ip: "192.168.56.11"
    k8s.vm.provider "virtualbox" do |vb|
      vb.memory = 6144
      vb.cpus   = 4
      vb.name   = "k8s-master"
    end
  end

  # ── K8s Worker 1 (192.168.56.12) ────────────────────────────────
  config.vm.define "k8s-worker1" do |w1|
    w1.vm.box = "ubuntu/focal64"
    w1.vm.hostname = "k8s-worker1"
    w1.vm.network "private_network", ip: "192.168.56.12"
    w1.vm.provider "virtualbox" do |vb|
      vb.memory = 2048
      vb.cpus   = 2
      vb.name   = "k8s-worker1"
    end
  end

  # ── K8s Worker 2 (192.168.56.13) ────────────────────────────────
  config.vm.define "k8s-worker2" do |w2|
    w2.vm.box = "ubuntu/focal64"
    w2.vm.hostname = "k8s-worker2"
    w2.vm.network "private_network", ip: "192.168.56.13"
    w2.vm.provider "virtualbox" do |vb|
      vb.memory = 2048
      vb.cpus   = 2
      vb.name   = "k8s-worker2"
    end
  end

  # ── Jenkins Master (192.168.56.10) ──────────────────────────────
  config.vm.define "jenkins-master" do |jenkins|
    jenkins.vm.box = "ubuntu/focal64"
    jenkins.vm.hostname = "jenkins-master"
    jenkins.vm.network "private_network", ip: "192.168.56.10"
    jenkins.vm.provider "virtualbox" do |vb|
      vb.memory = 3072
      vb.cpus   = 2
      vb.name   = "jenkins-master"
    end
  end

  # ── Monitoring (192.168.56.14) ───────────────────────────────────
  config.vm.define "monitoring" do |mon|
    mon.vm.box = "ubuntu/focal64"
    mon.vm.hostname = "monitoring"
    mon.vm.network "private_network", ip: "192.168.56.14"
    mon.vm.provider "virtualbox" do |vb|
      vb.memory = 2048
      vb.cpus   = 2
      vb.name   = "monitoring"
    end
  end

end