BitcoinHD server for Docker
===========================

[![Docker Stars](https://img.shields.io/docker/stars/btchd/btchdd.svg)](https://hub.docker.com/r/btchd/btchdd/)
[![Docker Pulls](https://img.shields.io/docker/pulls/btchd/btchdd.svg)](https://hub.docker.com/r/btchd/btchdd/)
[![Build Status](https://travis-ci.org/btchd/docker-btchdd.svg?branch=master)](https://travis-ci.org/btchd/docker-btchdd/)
[![ImageLayers](https://images.microbadger.com/badges/image/btchd/btchdd.svg)](https://microbadger.com/#/images/btchd/btchdd)

The BitcoinHD Core docker image.


Requirements
------------

* Physical machine, cloud instance, or VPS that supports Docker (i.e. [Vultr](http://bit.ly/1HngXg0), [Digital Ocean](http://bit.ly/18AykdD), KVM or XEN based VMs) running Ubuntu 14.04 or later (*not OpenVZ containers!*)
* At least 10 GB to store the block chain files (and always growing!)
* At least 1 GB RAM + 2 GB swap file


Really Fast Quick Start
-----------------------

One liner for Ubuntu 14.04 LTS machines with JSON-RPC enabled on localhost and adds upstart init script:

    curl https://raw.githubusercontent.com/btchd/docker-btchdd/master/bootstrap-host.sh | sh -s trusty


Quick Start
-----------

1. Create a `btchdd-data` volume to persist the btchdd blockchain data, should exit immediately.  The `btchdd-data` container will store the blockchain when the node container is recreated (software upgrade, reboot, etc):

        docker volume create --name=btchdd-data
        docker run -v btchdd-data:/btchd --name=btchdd-node -d \
            -p 8733:8733 \
            -p 127.0.0.1:8732:8732 \
            btchd/btchdd

2. Verify that the container is running and btchdd node is downloading the blockchain

        $ docker ps
        CONTAINER ID        IMAGE                         COMMAND             CREATED             STATUS              PORTS                                              NAMES
        d0e1076b2dca        btchd/btchdd:latest           "btchd_oneshot"     2 seconds ago       Up 1 seconds        127.0.0.1:8732->8732/tcp, 0.0.0.0:8733->8733/tcp   btchdd-node

3. You can then access the daemon's output thanks to the [docker logs command]( https://docs.docker.com/reference/commandline/cli/#logs)

        docker logs -f btchdd-node

4. Install optional init scripts for upstart and systemd are in the `init` directory.


Documentation
-------------

* Additional documentation in the [docs folder](docs).
