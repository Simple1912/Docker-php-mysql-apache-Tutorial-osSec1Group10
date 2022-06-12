# PHPMYADMIN

![image](https://github.com/Simple1912/Docker-php-mysql-apache-Tutorial-osSec1Group10/blob/main/GitHubimg/%E4%B8%8B%E8%BD%BD.png)

PHPMyAdmin is a popular administrative interface for MySQL and MariaDB databases. It allows you to interact with your schemas, tables and data using a web browser. phpMyAdmin can provide an intuitive and convenient web management interface for your MySQL, which is very easy to use.  

The project has an official Docker image that simplifies deployment in containerized environments. Here's how to quickly run a new PHPMyAdmin instance with an image.  

# Docker install phpmyadmin  
Use Docker to publish phpmyadmin and connect to an existing MySQL container  
First download the docker image of phpmyadmin  
```
# Query the mirrors in the mirror vault

docker search phpmyadmin
# Pull the most mirrors of star or pull the mirrors you want to use

docker pull docker.io/phpmyadmin/phpmyadmin
```
Start the image and connect to the existing MySQL container  
```
# start up

docker run --name myadmin -p 80:80 -d --link mysql-db:db docker.io/phpmyadmin/phpmyadmin

# Modify the container configuration file , Copy the configuration file to the host

docker cp myadmin:/etc/phpmyadmin/config.inc.php .

## Modify configuration file information (db is the alias specified at startup --link)

$cfg['Servers'][$i]['host'] = 'localhost' ——> $cfg['Servers'][$i]['host'] = 'db'

## Copy the modified configuration file back to the container

docker cp ./config.inc.php myadmin:/etc/phpmyadmin/

# Restart the phpmyadmin container
```

Write the docker-compose.yml file
```
version: "2"

services:

  mysql:

    image: hub.c.163.com/library/mysql

    container_name: test-mysql

    restart: always

    ports:

      - "3306:3306"

    environment:

      MYSQL_USER: "root"

      MYSQL_PASSWORD: "root"

      MYSQL_ROOT_PASSWORD: "root"

    networks:

      - net-mysql

 

  phpmyadmin:

    image: docker.io/phpmyadmin/phpmyadmin

    container_name: test-myadmin

    ports:

      - "80:80"

    environment:

      MYSQL_USER: "root"

      MYSQL_PASSWORD: "root"

      MYSQL_ROOT_PASSWORD: "root"

    networks:

      - net-mysql

 

networks:

  net-mysql:
```
publish container
```
# Publish containers using commands

docker-compose up -d
```
Reference site：  
https://hub.docker.com/_/phpmyadmin
