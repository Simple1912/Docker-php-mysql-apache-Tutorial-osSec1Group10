# PHP

![image](https://user-images.githubusercontent.com/106058477/172595227-d1a174f3-b4e8-4af0-8f1d-5187a61a1fb7.jpg)

PHP is a powerful server-side scripting language for creating dynamic and interactive sites.

PHP is free and widely used. Meanwhile, for competitors like Microsoft ASP, PHP is certainly another efficient option.

# What is PHP?
PHP (full name: PHP: Hypertext Preprocessor, "PHP: Hypertext Preprocessor") is a general-purpose open-source scripting language.  
PHP scripts are executed on the server.  
PHP is free to download and use.  

# What can PHP do?
PHP can generate dynamic page content  
PHP can create, open, read, write, and close files on the server  
PHP can collect form data  
PHP can send and receive cookies  
PHP can add, delete, modify data in your database  
PHP can restrict user access to some pages on your website  
PHP can encrypt data  
With PHP, you are no longer limited to outputting HTML. You can output images, PDF files, and even Flash movies. You can also output arbitrary text, such as XHTML and XML.  

Docker needs to use several services to deploy web projects: php, nginx, etc.  
The first is to pull the mirror.  
```
docker pull php:5.6-fpm
docker pull nginx
```
Create a docker network before starting, and use docker to connect multiple containers.  
```
docker network create -d bridge php-net
```
Start the PHP container  
```
docker run --name php-web -d -p 8000:8000 --network php-net -v  The storage path of php resources in your virtual machine: /data(The path to store the resource in the container)
php:5.6-fpm (mirror)
```
Then create the nginx configuration file conf.d in the virtual machine and fill in the content  
```
server{
    listen 80;
    server localhost;
    location / {
        root /data;  #The corresponding virtual machine is mounted to the /data code directory in the nginx container
        index index.php index.html index.htm;
    }
    location ~\.php(.*)$ {
        root /data;     #The corresponding host hangs in the /data code directory in the PHP container
        fastcgi_pass phpInternal network of containers ip:8000;   #This address is the internal IP address of the PHP container
        fastcgi_index index.php;
        fastcgi_param SCRIPT_FILENAME /data$fastcgi_script_name;  
        fastcgi_param PATH_INFO $1;   #The trip to configure pathinfo，tp The framework must use pathinfo
        include fastcgi_params;
    }
}
```
Start the nginx container  
```
docker run --name php-nginx --network php-net -d -p 80:80 -v 
x/conf.d nginx（mirror）
```
Enter the php-web container to install the extensions required by php  
```
docker exec -it php-web bash
cd /usr/local/bin  
./docker-php-ext-install pdo_mysql  
./docker-php-ext-install mysql
docker-php-ext-install bcmath
docker-php-ext-install mbstring
apt-get update && apt-get install -y libfreetype6-dev libjpeg62-turbo-dev libpng-dev
docker-php-ext-install -j$(nproc) iconv
docker-php-ext-configure gd --with-freetype-dir=/usr/include/ --with-jpeg-dir=/usr/include/
docker-php-ext-install -j$(nproc) gd
pecl install redis-4.0.1 && pecl install xdebug-2.6.0 && docker-php-ext-enable redis xdebug
```
Extensions such as mysql, bcmath, gd, mbstring, redis are installed.  
Restart the php-web container  
```
docker restart php-web
```
