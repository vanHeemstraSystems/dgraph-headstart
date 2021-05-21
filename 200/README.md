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
      - 8080:8080 # REST API
      - 9080:9080 # GraphQL API
    volumes:
      - ~/dgraph:/dgraph
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

### 100 - Ratel

Build and run the ratel container:

```
$ docker run --rm -it --name ratel -p 8000:8000 -d dgraph/ratel
```

Check if the container is running:

```
$ docker ps
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS                    NAMES
5fe22d3227b4        dgraph/ratel        "/usr/local/bin/dgra…"   5 seconds ago       Up 4 seconds        0.0.0.0:8000->8000/tcp   ratel
```

Now you should be able to see the ratel web interface at http://localhost:8000

![image](https://user-images.githubusercontent.com/12828104/118998575-d92a0580-b989-11eb-832f-548e0468942e.png)

Choose ***Local Bundle*** - Launch Offline

![image](https://user-images.githubusercontent.com/12828104/119002626-54d98180-b98d-11eb-9669-859ab567a883.png)

First start the DGraph container (see next section), then enter this URL in Dgraph server URL: ```http://[hostname]:8080``` (this is the port of the DGraph container)

More ...

***Note***: You can also use ratel online at https://play.dgraph.io/

### 200 - DGraph (requires Ratel)

Build and run the dgraph container:

```
$ docker run --rm -it --name dgraph -p 8080:8080 -p 9080:9080 -v ~/dgraph:/dgraph -d dgraph/standalone:latest
```

- The ```--rm``` causes Docker to automatically remove the container when it exits.
- The ```-it``` runs Docker interactively (so you get a pseudo-TTY with STDIN).

You will be prompted like below:

```
Warning: This standalone version is meant for quickstart purposes only.
         It is NOT RECOMMENDED for production environments.
...
Dgraph version   : v21.03.0
Dgraph codename  : rocket
Dgraph SHA-256   : b4e4c77011e2938e9da197395dbce91d0c6ebb83d383b190f5b70201836a773f
Commit SHA-1     : a77bbe8ae
Commit timestamp : 2021-04-07 21:36:38 +0530
Branch           : HEAD
Go version       : go1.16.2
jemalloc enabled : true

For Dgraph official documentation, visit https://dgraph.io/docs.
For discussions about Dgraph     , visit https://discuss.dgraph.io.
For fully-managed Dgraph Cloud   , visit https://dgraph.io/cloud.

Licensed variously under the Apache Public License 2.0 and Dgraph Community License.
Copyright 2015-2021 Dgraph Labs, Inc.
...
I0520 13:10:14.433914      25 run.go:568] Bringing up GraphQL HTTP API at 0.0.0.0:8080/graphql
I0520 13:10:14.433931      25 run.go:569] Bringing up GraphQL HTTP admin API at 0.0.0.0:8080/admin
...
I0520 13:10:14.433959      25 run.go:597] HTTP server started.  Listening on port 8080
...
I0520 13:10:19.435206      25 admin.go:824] Error reading GraphQL schema: Please retry again, server is not ready to accept requests.
I0520 13:10:19.439752      25 pool.go:162] CONNECTING to localhost:7080
I0520 13:10:19.540762      25 groups.go:902] Leader idx=0x1 of group=1 is connecting to Zero for txn updates
I0520 13:10:19.540788      25 groups.go:914] Got Zero leader: localhost:5080
I0520 13:10:19.543202      25 groups.go:491] Serving tablet for: 0-dgraph.type
I0520 13:10:19.544741      25 groups.go:491] Serving tablet for: 0-dgraph.drop.op
I0520 13:10:19.546588      25 groups.go:491] Serving tablet for: 0-dgraph.graphql.schema
I0520 13:10:19.548072      25 groups.go:491] Serving tablet for: 0-dgraph.graphql.xid
I0520 13:10:19.549293      25 groups.go:491] Serving tablet for: 0-dgraph.graphql.p_query
I0520 13:10:19.549509      25 groups.go:166] Server is ready
I0520 13:10:19.549546      25 access_ee.go:408] ResetAcl closed
I0520 13:10:19.549555      25 access_ee.go:318] RefreshAcls closed
I0520 13:10:20.236574      23 raft.go:540] CID set for cluster: 0e6bd371-c5f6-40fe-bc48-0904ad9fc136
...
I0520 13:10:24.437692      25 admin.go:835] No GraphQL schema in Dgraph; serving empty GraphQL API
...

```

Check the running container:

```
$ docker ps
CONTAINER ID        IMAGE                      COMMAND                  CREATED             STATUS              PORTS                                                      NAMES
0ef3696a642a        dgraph/standalone:latest   "/run.sh"                55 seconds ago      Up 50 seconds       0.0.0.0:8080->8080/tcp, 8000/tcp, 0.0.0.0:9080->9080/tcp   dgraph
```
Success!

Now when we revisit ratel at http://[hostname]:8000 you will see that the DGraph server is successfully connected to (green icon):

![image](https://user-images.githubusercontent.com/12828104/119003136-c9acbb80-b98d-11eb-992d-44cbdcecb0aa.png)

After clicking "***Continue****" button the Console window shows:

![image](https://user-images.githubusercontent.com/12828104/119003760-463f9a00-b98e-11eb-8fb7-f03f39f63664.png)
more ...
