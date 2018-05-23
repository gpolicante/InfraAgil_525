# -*- mode: ruby -*-
# vi: set ft=ruby :

# All Vagrant configuration is done below. The "2" in Vagrant.configure
# configures the configuration version (we support older styles for
# backwards compatibility). Please don't change it unless you know what
# you're doing.
Vagrant.configure("2") do |config|
# isto daqui é uma configuração global, posso criar varias maquinas da mesma configuracao atraves daqui
  config.vm.box = "ubuntu/xenial64"

  config.vm.box_check_update = false
  # config.vm.network "forwarded_port", guest: 80, host: 8080
  # config.vm.network "forwarded_port", guest: 80, host: 8080, host_ip: "127.0.0.1"
  # config.vm.network "private_network", ip: "192.168.33.10"
  config.vm.network "public_network"

  # config.vm.synced_folder "../data", "/vagrant_data"

  config.vm.provider "virtualbox" do |vb|
    vb.memory = "2048"
  end
  # aqui acaba a configuracao global 
  (1..2).each do |i|
    config.vm.define "ubuntu#{i}" do |node|
  node.vm.provider "virtualbox" do |vb|
    vb.memory = "2500"
  end
      node.vm.hostname = "ubuntu#{i}"
      node.vm.provision "shell", inline: <<-SHELL
        apt clean all
        apt update
        apt install python -y     
      SHELL
    end
  end

  (1..2).each do |i|
    config.vm.define "dev#{i}" do |node|
      node.vm.box = "centos/7"
      node.vm.hostname = "dev#{i}"
      node.vm.provision "shell", inline: <<-SHELL
        #yum update -y
      SHELL
    end
  end
 # este ultimo serve para as 4 maquinas  
  config.vm.provision "shell", inline: <<-SHELL
    sudo mkdir -p /root/.ssh/
    sudo touch /root/.ssh/authorized_keys
    sudo cat /vagrant/chave.pub >> /root/.ssh/authorized_keys
  SHELL
end











