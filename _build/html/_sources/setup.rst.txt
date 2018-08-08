Setup your development environment
==================================

Prerequisites
-------------
We assume you are using Linux or MacOS.
To get started, make sure you have all dependencies installed::

  git
  go
  docker

Setup Go
--------
Setup your Go environment by determining a directory for your go path in ``$GOPATH``.
All your Go files project files will be stored there.
For the remainder of this documnet, we assume that your ``$GOPATH`` is set to ``~/go/``.

Start running your local instance
---------------------------------
For developing, you might want to start a local instance of the DIA ecosystem.
Just clone our repository::

  mkdir $GOPATH/src/github.com/diadata-org/
  cd $GOPATH/src/github.com/diadata-org/
  git clone git@github.com/diadata-org/api-golang

and build everything.
We use a docker swarm to host a reliable and redundant database.
Connected to the database are all data collectors, with some of them part of our default stack.
To install and run that default stack, start a local docker swarm by typing::

  docker swarm init

Then it is time to build the first containers. This might take some while, as the images have to be downloaded and compiled::

  docker-compose build

Tag your local machine node in your swarm with labels for kafka and the zookeeper::

  docker node update $(docker node ls | tail -n 1 | cut -d " " -f 1) --label-add kafka=1
  docker node update $(docker node ls | tail -n 1 | cut -d " " -f 1) --label-add zoo=1

After that you can deploy the stack on your swarm::

  docker stack deploy -c docker-compose.kafka.yml kafka

Use ``docker ps`` to see which containers are running.

Your initial setup is now complete and you can start developing your own data scraper.
