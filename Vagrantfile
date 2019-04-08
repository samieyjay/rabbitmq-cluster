# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|

  config.vm.box = "ubuntu/xenial64"

  # Create a forwarded port mapping which allows access to a specific port
  config.vm.network "forwarded_port", guest: 15672, host: 15672

  config.vm.provision "docker"
  config.vm.provision "shell", path: "docker-compose.sh"
  config.vm.provision "shell", inline: "docker-compose up -d"

  config.vm.provider "virtualbox" do |vb|
    vb.memory = "1024"
    vb.cpus = "2"
  end

end
