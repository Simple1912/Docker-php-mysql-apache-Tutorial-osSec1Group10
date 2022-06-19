# PHPMYADMIN

![image](https://github.com/Simple1912/Docker-php-mysql-apache-Tutorial-osSec1Group10/blob/main/GitHubimg/%E4%B8%8B%E8%BD%BD.png)

PHPMyAdmin is a popular administrative interface for MySQL and MariaDB databases. It allows you to interact with your schemas, tables and data using a web browser. phpMyAdmin can provide an intuitive and convenient web management interface for your MySQL, which is very easy to use.  

The project has an official Docker image that simplifies deployment in containerized environments. Here's how to quickly run a new PHPMyAdmin instance with an image.  

# Docker install phpmyadmin  
Use Docker to publish phpmyadmin and connect to an existing MySQL container  

1. First, install the docker image of phpmyadmin. To install the docker image, you may execute the command below on your Windows Terminal:
```
docker pull phpmyadmin/phpmyadmin:latest
```
The ```pull``` command will pull (download and install) the image of phpMyAdmin into the docker. After the pulling process completed, you should see the statement as shown in the picture below from your Windows Terminal:

![image](https://github.com/Simple1912/Docker-php-mysql-apache-Tutorial-osSec1Group10/blob/main/GitHubimg/WhatsApp%20Image%202022-06-19%20at%207.06.06%20PM.jpeg)

2. The next thing you need to is to run build and run the container of the phpMyAdmin image that we have downloaded earlier. To do so, execute the command below:
```
 docker run --name dev-phpmyadmin -d --link dev-mysql:db -p 7098:80 phpmyadmin/phpmyadmin
```
* The ```--name``` command is used to assign name to our phpMyAdmin container. In this tutorial, we named our container as dev-phpmyadmin.
* The ```-d``` command is used to startup the container and run the container in background of the terminal. It does not receive input or display output.
* The ```--link``` command is used to link between containers. In this case, we are trying to link our phpmyadmin container with our mysql container with the name dev-mysql:db.
* The ```-p``` command is used to assign port to our container. In this case, our phpmyadmin container will be mapped to ```7098:80``` port.

After executing the command, your Windows Terminal should display the output as in the image below:

![image](https://github.com/Simple1912/Docker-php-mysql-apache-Tutorial-osSec1Group10/blob/main/GitHubimg/WhatsApp%20Image%202022-06-19%20at%207.07.41%20PM.jpeg)

```20a1330e884852ee3785d104a580d8c478cca4eaf52234f725229649175e7eb3``` is the container ID. This means, the container is successfully built and is now running. You can verify it by searching it in the Docker as in the picture below:

![image](https://github.com/Simple1912/Docker-php-mysql-apache-Tutorial-osSec1Group10/blob/main/GitHubimg/WhatsApp%20Image%202022-06-19%20at%2010.19.46%20PM.jpeg)

3. Next, we can try to access our phpMyAdmin that has been hosted locally through our browser. Just insert this URL address http://localhost:7098/ and you should see the interface as shown in the picture below:

![image](https://github.com/Simple1912/Docker-php-mysql-apache-Tutorial-osSec1Group10/blob/main/GitHubimg/WhatsApp%20Image%202022-06-19%20at%2010.27.29%20PM.jpeg)

4. The next step is to enter the username and password that we have set up in our mySQL container which are ```root``` for the username and ```pass123``` for the password.

![image](https://github.com/Simple1912/Docker-php-mysql-apache-Tutorial-osSec1Group10/blob/main/GitHubimg/WhatsApp%20Image%202022-06-19%20at%2010.30.28%20PM.jpeg)

5. After logging in, you should see the interface as in the picture below. There will be some default databases available in it.

![image](https://github.com/Simple1912/Docker-php-mysql-apache-Tutorial-osSec1Group10/blob/main/GitHubimg/WhatsApp%20Image%202022-06-19%20at%2010.33.15%20PM.jpeg)

**Now, let's create a table and insert some data into it.**

1. After logging in to phpMyAdmin, head on to "Database" tab.

![image](https://github.com/Simple1912/Docker-php-mysql-apache-Tutorial-osSec1Group10/blob/main/GitHubimg/WhatsApp%20Image%202022-06-19%20at%2011.06.45%20PM.jpeg)

2. Create a new database name "Staff" and hit the "Create" button

![image](https://github.com/Simple1912/Docker-php-mysql-apache-Tutorial-osSec1Group10/blob/main/GitHubimg/WhatsApp%20Image%202022-06-19%20at%2011.08.36%20PM.jpeg)

3. Then, head on to "SQL" tab. You will see a blank SQL workspace like in the picture below:

![image](https://github.com/Simple1912/Docker-php-mysql-apache-Tutorial-osSec1Group10/blob/main/GitHubimg/WhatsApp%20Image%202022-06-19%20at%2011.11.46%20PM.jpeg)

3. Right now we will write some SQL command to create table and insert data into it. Below is the example command:

```
CREATE TABLE STAFF
 (STAFF_ID                                            INT(4),
 FIRST_NAME                                           VARCHAR(20),
 LAST_NAME                                            VARCHAR(20),
 EMAIL                                                VARCHAR(50),
 PHONE_NUMBER                                         INT(10),
	CONSTRAINT STAFF_STAFF_ID_PK PRIMARY KEY (STAFF_ID));
  
INSERT INTO STAFF VALUES(432, 'Aidil', 'Haslam', 'aidilHaslam@gmail.com', '0122884567');
INSERT INTO STAFF VALUES(509, 'Mariam', 'Ibrahim', 'mariamIbrahim@gmail.com', '0135114501');
INSERT INTO STAFF VALUES(389, 'Faisal', 'Tahir', 'faisalTahir@yahoo.com', '0104325798');
INSERT INTO STAFF VALUES(504, 'Salman', 'Musliman', 'salmanMusliman@gmail.com', '0144136781');
INSERT INTO STAFF VALUES(235, 'Arif', 'Aiman', 'arifAiman@gmail.com', '0174178523');
INSERT INTO STAFF VALUES(356, 'Zulkhairil', 'Hafiz', 'zulHafiz@gmail.com', '0193456789');
INSERT INTO STAFF VALUES(558, 'Nur', 'Aisyah', 'nurAisyah@yahoo.com', '0164897561');
INSERT INTO STAFF VALUES(876, 'Siti', 'Sarah', 'sitiSarah@yahoo.com', '0155134189');
INSERT INTO STAFF VALUES(889, 'Lizzy', 'Mcguire', 'lizzyMc@hotmail.com', '0188554789');
INSERT INTO STAFF VALUES(239, 'Fatima', 'Zahra', 'fatimaZahra@yahoo.com', '0177415178');
```

![image](https://github.com/Simple1912/Docker-php-mysql-apache-Tutorial-osSec1Group10/blob/main/GitHubimg/WhatsApp%20Image%202022-06-19%20at%2011.14.22%20PM.jpeg)

4. After you finished writing the commands, click the "Go" button and you may see a screen as shown in the picture below:

![image](https://github.com/Simple1912/Docker-php-mysql-apache-Tutorial-osSec1Group10/blob/main/GitHubimg/WhatsApp%20Image%202022-06-19%20at%2011.16.42%20PM.jpeg)

Congratulations! You now have successfully create a database and inserting data into it via phpMyAdmin that you have configured using docker. You may see the created database by clicking on "STAFF" at the left side of your screen. 

![image](https://github.com/Simple1912/Docker-php-mysql-apache-Tutorial-osSec1Group10/blob/main/GitHubimg/WhatsApp%20Image%202022-06-19%20at%2011.19.59%20PM.jpeg)

That's all from us, thank you!
