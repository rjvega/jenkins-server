# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = "bento/centos-7.1"

  config.vm.network "public_network"

  config.vm.provider "virtualbox" do |vb|
    vb.name = "jenkins-server"
    vb.gui = false
    vb.memory = "1024"
  end

  config.vm.provision "shell", inline: <<-SHELL
    #
    # EPEL
    #
    yum install -y epel-release
    yum install -y deltarpm
    yum update -y

    # 
    # vim
    #
    command -v vim || yum install -y vim
    
    #
    # Java virtual machine
    #
    command -v javac && java -version || yum install -y java-1.8.0-openjdk.x86_64

    sudo cp /etc/profile /etc/profile_backup
    echo 'export JAVA_HOME=/usr/lib/jvm/jre-1.8.0-openjdk' | sudo tee -a /etc/profile
    echo 'export JRE_HOME=/usr/lib/jvm/jre' | sudo tee -a /etc/profile
    source /etc/profile

    #
    # Git
    #
    command -v git && git --version || yum install -y git

    #
    # Nodejs
    #
    command -v node && node -v || yum install -y nodejs

    #
    # Jenkins
    #
    cd ~
    wget -O /etc/yum.repos.d/jenkins.repo http://pkg.jenkins-ci.org/redhat-stable/jenkins.repo
    rpm --import http://pkg.jenkins-ci.org/redhat-stable/jenkins-ci.org.key
    yum install -y jenkins

    sudo systemctl start jenkins.service
    sudo systemctl enable jenkins.service

    sudo firewall-cmd --zone=public --permanent --add-port=8080/tcp
    sudo firewall-cmd --reload
    
    echo $( hostname -I | awk '{ print $2 }' ) | tee /vagrant/myipaddr.txt
  SHELL
end
