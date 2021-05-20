# 200 - Running Dgraph

Running the [dgraph/standalone](https://hub.docker.com/r/dgraph/standalone) docker image is the quickest way to get started with Dgraph. This standalone image is meant for quickstart purposes only. It is not recommended for production environments.

Ensure that Docker is installed and running on your machine.

Now, it’s just a matter of running the following command, and you have Dgraph up and running.

## 100 - Using docker-compose (recommended)

Have the Dockerfile as follows:

```
FROM dgraph/standalone

```
containers/dgraph/Dockerfile

Have the sample.docker-compose.yml file as follows:

```
version: '3.7'

services:
  dgraph:
    build: .
    container_name: 'dgraph'
    privileged: true
    ports:
      - 8000:8000 # Web UI
      - 8080:8080 # REST API
      - 9080:9080 # GraphQL API
```
containers/dgraph/sample.docker-compose.yml

Copy the sample file to your own configurable file:

```
$ cd containers/dgraph
$ cp sample.docker-compose.yml docker-compose.yml
```

Build and run the dgraph container:

```
$ cd containers/dgraph
$ docker-compose up -d
```

more ...

## 200 - Using Docker run

Build and run the dgraph container:

```
$ docker run --rm -it -p 8000:8000 -p 8080:8080 -p 9080:9080 dgraph/standalone:latest
```

- The ```--rm``` causes Docker to automatically remove the container when it exits.
- The ```-it``` runs Docker interactively (so you get a pseudo-TTY with STDIN).

Check the running container:

```
$ docker ps
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS                                                                    NAMES
073752b2fa54        dgraph/standalone   "/run.sh"           About an hour ago   Up About an hour    0.0.0.0:8000->8000/tcp, 0.0.0.0:8080->8080/tcp, 0.0.0.0:9080->9080/tcp   unruffled_allen
```
Success!

more ...
