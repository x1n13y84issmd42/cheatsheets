# Build & startup order

```yaml
services:

  A:
    ...
  B:
    depends_on:
      - A
  C:
    depends_on:
      - A
```

# Explicit IP for host & containers

```
docker network create -d bridge --subnet 192.168.0.0/24 --gateway 192.168.0.1 dockernet
```

Now each container can connect to the host under the fixed IP 192.168.0.1.

You just need to make sure, that you connect all your containers to that “dockernet” network you just created. You can do that with the `--net=dockernet` option for `docker run`. Or from a `docker-compose.yml`:

```yaml
version: '2'
services:
    db:
        image: some/image
        networks:
            - dockernet
networks:
    dockernet:
        external: true
```

## Alternative

```yaml
version: '2'

services:
  mysql:
    container_name: mysql
    image: mysql:latest
    restart: always
    environment:
      - MYSQL_ROOT_PASSWORD=root
    ports:
     - "3306:3306"
    networks:
      vpcbr:
        ipv4_address: 10.5.0.5

  apigw-tomcat:
    container_name: apigw-tomcat
    build: tomcat/.
    ports:
     - "8080:8080"
     - "8009:8009"
    networks:
      vpcbr:
        ipv4_address: 10.5.0.6
    depends_on:
     - mysql

networks:
  vpcbr:
    driver: bridge
    ipam:
     config:
       - subnet: 10.5.0.0/16
         gateway: 10.5.0.1
```