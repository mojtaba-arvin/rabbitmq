# Simple RabbitMQ Service
![rabbitmq up](https://user-images.githubusercontent.com/6056661/111041550-edafc600-844d-11eb-8123-4d3a9a3473c1.png)
### Setup environment

`RabbitMQ` environment ,must be at `.docker-compose/` directory as `.env` file. you can copy the sample:
```
cp .docker-compose/.env.local .docker-compose/.env
```

### RabbitMQ management UI Access

The RabbitMQ management plugin provides an HTTP-based API for management and monitoring


#### production
To use management UI in production, there is a sample compose file ( `docker-compose.join.nginx.yml` ) , to join `Nginx` reverse proxy network.
you can use docker-compose `-f` option, to join nginx network

```
docker-compose -f docker-compose.yml -f docker-compose.join.nginx.yml up -d
```

#### development
To use management UI in local environment, there is a sample compose file ( `docker-compose.local.yml` ), to map ports.

```
docker-compose -f docker-compose.yml -f docker-compose.local.yml up -d
```

then,the management UI can be accessed using a Web browser at `http://localhost:15672/`.

### Clients

Clients on the same machine, can join this service by define an external network,
for example when the client network name is `sample-network` it should define as:

```
networks:
    sample-network:
        external:
            name: rabbitmq_broker-network
```

The `external` network name, has two part, which are separated by an underline, `rabbitmq` is name of the repository, and `broker-network` is the network name of this repository
