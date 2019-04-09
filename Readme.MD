# How to deploy multinode RabbitMQ Cluster using Vagrant and Docker

** Technologies used; **

- Virtualbox
- Vagrant
- Docker
- Docker Compose
- RabbitMQ
- Ubuntu/Xenial64

** File included; **

- Vagrantfile 
- docker-compose.yml
- rabbitmq.config

## Vagrantfile 

STEP 1: Provision base box - Ubuntu/Xenial64
STEP 2: Provision Docker within the base box
STEP 3: Copy files required by Docker Compose to the box
STEP 4: Install Docker Compose using $script and run docker-compose to deploy the cluster

## docker-compose.yml

Docker-compose.yml will deploy 3 containers <node1, node2, node3> using the rabbitmq:3.7.14-management Docker image

All nodes communicate using the cluster-network

All nodes depend on Node1 as it acts as the master node

A volume is shared across all nodes to ensure all containers are deployed using the same configuration file (rabbitmq.config)

3 environment variables are deployed as part of the containers; RABBITMQ_ERLANG_COOKIE, RABBITMQ_NODENAME, RABBITMQ_CONFIG_FILE

RABBITMQ_ERLANG_COOKIE is shared across all nodes to allow communications between the nodes
RABBITMQ_NODENAME identifies the node
RABBITMQ_CONFIG_FILE is required to override the location of main RabbitMQ config file location 

## rabbitmq.config

The cluster uses classic config format (rabbitmq.confiq) which contains configuration settings such as default username and password (plain text), cluster_nodes for auto clustering, http port listener for RabbitMQ management plugin


