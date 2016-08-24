# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|
  config.vm.box = "centos/7"
  config.vm.provision "shell", path: "bootstrap.sh"
  config.vm.network "private_network", ip: "192.168.23.10"
  config.vm.network "forwarded_port", guest: 80, host: 80
  config.vm.network "forwarded_port", guest: 6060, host: 6060
  config.vm.network "forwarded_port", guest: 8080, host: 8080
  config.vm.network "forwarded_port", guest: 8081, host: 8081
  config.vm.provider "virtualbox" do |vb|
  	vb.memory = "4096"
  	vb.cpus = "2"
  end
end
