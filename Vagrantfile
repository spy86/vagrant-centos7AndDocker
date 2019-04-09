# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure("2") do |config|


  config.vm.box = "geerlingguy/centos7" #CentOS 7
 
  config.vm.network :forwarded_port, guest: 22, host: 2222
  config.vm.network :forwarded_port, guest: 80, host: 2280
  config.vm.network :forwarded_port, guest: 8080, host: 2281

  config.vm.network "private_network", ip: "192.168.123.123"

  config.vm.provision "shell", inline: <<-SHELL
  sudo sed -i 's/enforcing/disabled/g' /etc/selinux/config /etc/selinux/config
  sudo sestatus
  yum install java-1.8.0-openjdk-devel wget unzip nano httpd epel-release python2-pip -y
  yum update -y
  yum install -y yum-utils device-mapper-persistent-data lvm2 
  yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo 
  yum install docker-ce -y
  usermod -aG docker $(whoami)  
  systemctl enable docker.service 
  systemctl start docker.service 
  pip install docker-compose
  yum upgrade python* -y
  docker-compose version
  SHELL
end