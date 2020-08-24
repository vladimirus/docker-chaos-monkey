# docker-chaos-monkey

A Chaos Monkey system for Docker Swarm.

![Original ChaosMonkey Logo](images/cm-logo.png)

Implemented for the book [12 Factor Applications with Docker and Go](https://leanpub.com/12fa-docker-golang).

## Creating a disposable service

Creating a disposable service is as simple as adding a label `role=disposable`.

For example:

~~~
docker service create -l role=disposable --name gotwitter titpetric/gotwitter
~~~

## Running chaos.sh

When running `chaos.sh` you can set two environment variables:

* `DOCKER_LABEL` - "key=value" label that services must have to be killed off
* `SKIP_WARNING=1` - skip initial warning

## Rules

* If the service has only 1 replica (1/1), a container will not be killed.
* If the service has incomplete replicas (4/5), a container will not be killed.
* If no containers are running on the current host, no containers will be killed.
* Only one container per service is killed if the above conditions are met.

## Screenshot

![Screenshot](images/chaos-monkey.png)