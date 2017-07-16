# devops-tools

Tools about devops of my own.

## Docker

Running containers by docker-compose.

**If bind is deployed, all of the services worked in containers should be named a domain to easily connect with each other.**

### Bind

#### Images

* [sameersbn/bind - Docker Store](https://store.docker.com/community/images/sameersbn/bind)

#### Services

* bind: `10.0.10.0:53`
* webmin: `https://10.0.10.0:10000`

#### References

* [BIND Open Source DNS Server | Internet Systems Consortium](https://www.isc.org/downloads/bind/)

### Gitlab

#### Images

* [Gitlab Community Edition - Docker Store](https://store.docker.com/images/gitlab-community-edition)

#### Services

* gitlab: `http://10.0.20.0`

### MariaDB

#### Images

#### Services

### MongoDB

MongoDB with mongoclient, mongo-express.

#### Images

* [mongo - Docker Store](https://store.docker.com/images/mongo)
* [mongoclient/mongoclient - Docker Store](https://store.docker.com/community/images/mongoclient/mongoclient)
* [mongo-express - Docker Store](https://store.docker.com/images/mongo-express)

#### Services

* mongodb: `mongodb://10.0.30.250:27017`
* mongoclient: `http://10.0.30.251:3000`
* mongo-express: `http://10.0.30.252:8081`

### MySQL

#### Images

* [mysql - Docker Store](https://store.docker.com/images/mysql)
* [phpmyadmin/phpmyadmin - Docker Store](https://store.docker.com/community/images/phpmyadmin/phpmyadmin)

#### Services

* mysql: `mysql://10.0.30.0:3306`
* phpmyadmin: `http://10.0.30.1`

### OpenLDAP

#### Images

* [osixia/openldap](https://github.com/osixia/docker-openldap)
* [osixia/phpldapadmin](https://github.com/osixia/docker-phpLDAPadmin)

#### Services

* openldap: 
    - `10.0.10.1:389`
    - `10.0.10.1:636`
* phpldapadmmin: `https://10.0.10.2`

### Neo4j

#### Images

* [neo4j - Docker Store](https://store.docker.com/images/neo4j)

#### Services

* neo4j: `http://10.0.30.200:7474`

### PostgreSQL

#### Images

* [postgres - Docker Store](https://store.docker.com/images/postgres)
* [sosedoff/pgweb - Docker Store](https://store.docker.com/community/images/sosedoff/pgweb)

#### Services

* postgresql: `10.0.3.210:5432`
* pgweb: `http://10.0.3.211:8081`

### Readthedocs

#### Images

Build image based on ubuntu 16.04.

For accumlating this process:
* add apt source in mainland China
* add git proxy
* add douban pip source

#### Services

* readthedocs: `http://10.0.40.0`

### Redis

#### Images

* [redis - Docker Store](https://store.docker.com/images/redis)
* [tenstartups/redis-commander - Docker Store](https://store.docker.com/community/images/tenstartups/redis-commander)
* [sasanrose/phpredmin - Docker Store](https://store.docker.com/community/images/sasanrose/phpredmin)

#### Services

* redis: `redis://10.0.30.100:6379`
* redis-commander: `http://10.0.30.101:8081`
* phpredmin: `http://10.0.30.102`

### Sentry

Put Sentry into Docker is a little tricky.

There are two databases used in sentry:
* redis
* postgres

# Right Way to run Sentry in docker compose

There are six steps on the offical website to help to run this sentry container, but it's not the way how to do it in docker-compose, here it is:

First of all, create all fundamental services:

```shell
grammy-jiang@ubuntu:~$ docker run \
> -d \
> --name sentry-redis \
> -v /home/grammy-jiang/PycharmProjects/docker/docker-sentry/redis-data:/data
> redis
```

```shell
grammy-jiang@ubuntu:~$ docker run \
> -d \
> --name sentry-postgres \
> -e POSTGRES_PASSWORD=secret \
> -e POSTGRES_USER=sentry \
> -v /home/grammy-jiang/PycharmProjects/docker/docker-sentry/postgres-data:/var/lib/postgresql/data
> postgres
```

Then generate the secret key:

```shell
grammy-jiang@ubuntu:~$ docker run \
> --rm \
> sentry \
> config generate-secret-key
b2k(q_2-^g*hi!6c*q%@ujf2=o#=adu*3t73th39k0s!(jfw+k
```

This secret key will be used in all services in docker compose, write it down!

Then 

```shell
grammy-jiang@ubuntu:~$ docker run \
> -it \
> --rm \
> -e SENTRY_SECRET_KEY='b2k(q_2-^g*hi!6c*q%@ujf2=o#=adu*3t73th39k0s!(jfw+k' \
> --link sentry-postgres:postgres \
> --link sentry-redis:redis \
> -v /home/grammy-jiang/PycharmProjects/docker/docker-sentry/sentry-files:/var/lib/sentry/files \
> -v /home/grammy-jiang/PycharmProjects/docker/docker-sentry/sentry-sentry:/etc/sentry \
> sentry \
> upgrade
```

After these, stop and remove all containers, up docker-compose.yml, done!

#### Images

* [Sentry - Docker Store](https://store.docker.com/images/sentry)

#### Services

* sentry: `http://10.0.20.20:9000`

#### References

* [Track errors with modern exception logging for JavaScript, Python, Ruby, Java, and Node.js](https://sentry.io/welcome/)