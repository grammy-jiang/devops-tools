# devops-tools

Tools about devops of my own.

## Docker

Running containers by docker-compose.

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

#### Services

### Sentry

#### Images

#### Services

