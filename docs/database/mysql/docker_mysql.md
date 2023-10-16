---
layout: default
title: mysql docker
parent: Database
permalink: /docs/database/mysql
---

## Install mysql in docker

### 1. Pull the Mysql docker image

```bash
    docker pull mysql/mysql-server:latest

    docker images
```


### 2. Start mysql database

    docker run --name mysqldb -d mysql/mysql-server:latest

    docker ps

### 3. Find root password

```bash
   docker log | grep GENERATED
```

### 4. Login to mysql

```bash
   docker exec -it [container_name] mysql -uroot -p
```

### 5. Change password

```sql
    ALTER USER 'root'@'localhost' IDENTIFIED BY 'password';
```

