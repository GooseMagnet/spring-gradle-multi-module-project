# Setup

The following is used to set up Zookeeper and Kafka on docker

## Docker Network
```shell
docker network create app-tier --driver bridge
```

## Zookeeper
```shell
docker run -d -h zookeeper --name zookeeper-server \
    --network app-tier \
    -e ALLOW_ANONYMOUS_LOGIN=yes \
    bitnami/zookeeper:latest
```

## Kafka
```shell
docker run -d -h kafka --name kafka-server \
    --network app-tier \
    -e ALLOW_PLAINTEXT_LISTENER=yes \
    -e KAFKA_CFG_ZOOKEEPER_CONNECT=zookeeper-server:2181 \
    bitnami/kafka:latest
```

## Hosts
- Get the Kafka container ip
- Add the container's ip to `/etc/hosts`
  - Example:
    `172.18.0.3 kafka`