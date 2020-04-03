# OpenCTI

OpenCTI could be deployed using the docker-compose command.

## Clone the repository

```bash
$ mkdir /path/to/your/app && cd /path/to/your/app
$ git clone https://github.com/Crypt-0n/OpenCTI.git
$ cd OpenCTI
```

## Configure the environment

Before running the `docker-compose` command, don't forget to change the admin token (this token must be a [valid UUID](https://www.uuidgenerator.net/)) and the password in the file `.env`.

As OpenCTI has a dependency to ElasticSearch and Grakn, you have to set the `vm.max_map_count` before running the containers, as mentioned in the [ElasticSearch documentation](https://www.elastic.co/guide/en/elasticsearch/reference/current/docker.html#docker-cli-run-prod-mode).

```bash
$ sysctl -w vm.max_map_count=1048575
```

To make this parameter persistent, please update your file `/etc/sysctl.conf` and add the line:
```bash
$ vm.max_map_count=1048575
```

## Run

### Starting grakn, redis, elasticsearch, minio and rabbitmq

Execute (root user) :
```bash
docker-compose -f 1.yml up -d
```

### Starting OpenCTI and worker

Waiting 1 minute and execute (root user) :
```bash
docker-compose -f 3.yml up -d
```

### Starting connectors

Waiting 1 minute and execute (root user) :
```bash
docker-compose -f 3.yml up -d
```

## Stop

```bash
docker-compose -f 1.yml down
docker-compose -f 2.yml down
docker-compose -f 3.yml down
```

## Open OpenCTI

URL : http://localhost:8080
