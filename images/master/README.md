# Docker Salt-Master

A Docker image which allows you to run a containerised Salt-Master server.

## Building the container

    docker build -t salt .

## Running the Container

You can easily run the container like so:

    docker run --rm -it salt

## Environment Variables

The following environment variables can be set:

* `LOG_LEVEL`: The level to log at, defaults to `error`

## Volumes

There are several volumes which can be mounted to Docker data container as
described here: https://docs.docker.com/userguide/dockervolumes/. The following
volumes can be mounted:

 * `/etc/salt/pki` - This holds the Salt Minion authentication keys
 * `/var/cache/salt` - Job and Minion data cache
 * `/var/logs/salt` - Salts log directory
 * `/etc/salt/master.d` - Master configuration include directory
 * `/srv/salt` - Holds your states, pillars etc

## Ports

The following ports are exposed:

 * `4505`
 * `4506`

These ports allow minions to communicate with the Salt Master.

## Running Salt Commands

Once installed run:

    $ CONTAINER_ID=$(docker run -d soon/salt-master)
    $ docker exec -it $CONTAINER_ID salt '*' test.ping
