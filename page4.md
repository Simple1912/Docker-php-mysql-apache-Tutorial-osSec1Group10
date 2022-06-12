# MYSQL

![image](https://user-images.githubusercontent.com/106058477/172595962-3eaf87c7-130e-4e3c-a4b7-e08dc35fa41b.jpg)

MySQL is a relational database management system developed by the Swedish MySQL AB company and is a product of Oracle. MySQL is one of the most popular relational database management systems. In terms of WEB applications, MySQL is one of the best RDBMS (Relational Database Management System, relational database management system) application software.  
MySQL is a relational database management system, relational databases keep data in different tables instead of keeping all the data in one big warehouse, which increases speed and improves flexibility.  
The SQL language used by MySQL is the most commonly used standardized language for accessing databases. MySQL software adopts a dual-licensing policy, which is divided into community version and commercial version. Due to its small size, fast speed, low total cost of ownership, and especially the open source feature, MySQL is generally chosen as the website for the development of small and medium-sized websites and large-scale websites. database.  

# Docker run mysql
Download mysql image, use latest by default  
```
shell> docker pull mysql/mysql-server:tag
```
Run, --name specifies a custom name, -d is running in the background  
```
shell> docker run --name=mysql -d -p 3306:3306 mysql/mysql-server:tag
```
View run
```
shell> docker ps
CONTAINER ID   IMAGE                COMMAND                  CREATED             STATUS                              PORTS                NAMES
a24888f0d6f4   mysql/mysql-server   "/entrypoint.sh my..."   14 seconds ago      Up 13 seconds (health: starting)    3306/tcp, 33060/tcp  mysql
```
View logs  
```
shell> docker logs mysql
```
Get initial password  
```
shell> docker logs mysql 2>&1 | grep GENERATED
GENERATED ROOT PASSWORD: Axegh3kAJyDLaRuBemecis&EShOs
```
Log in to msyql and enter the initial password obtained above  
```
shell> docker exec -it mysql mysql -uroot -p
```
Add root user, can't do anything before this  
```
mysql> ALTER USER 'root'@'localhost' IDENTIFIED BY 'password';
```
After exiting, log in as root again, ok, but this can only log in inside the container, and you need to add a mysql accessible from the external network  
```
CREATE USER 'root'@'%' IDENTIFIED BY '123456';
#set permission
grant all privileges on *.* to root@"%" WITH GRANT OPTION;
```
It is now accessible outside the container  

Reference documentation:  
https://hub.docker.com/r/mysql/mysql-server
