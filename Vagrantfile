# -*- mode: ruby -*-
# vi: set ft=ruby :

Vagrant.configure("2") do |config|

  # install docker-compose 
  # launch rabbitmq cluster with docker compose
  $script = <<-SCRIPT
  curl -L "https://github.com/docker/compose/releases/download/1.24.0/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
  chmod +x /usr/local/bin/docker-compose
  ln -s /usr/local/bin/docker-compose /usr/bin/docker-compose
  docker-compose up -d
  SCRIPT

  config.vm.box = "ubuntu/xenial64"

  # Create a forwarded port mapping which allows access to a port 15672 on the host machine
  config.vm.network "forwarded_port", guest: 15672, host: 15672

  config.vm.provision "docker"
  config.vm.provision "file", source: "docker-compose.yml", destination: "$HOME/docker-compose.yml"
  config.vm.provision "file", source: "rabbitmq.config", destination: "$HOME/rabbitmq.config"
  config.vm.provision "shell", inline: $script

end
