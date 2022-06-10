# NGINX

![image](https://github.com/Simple1912/Docker-php-mysql-apache-Tutorial-osSec1Group10/blob/main/GitHubimg/nginx.jpg)

Deploying NGINX tutorial

Nginx is rich in functions and can be used as an HTTP server, reverse proxy server, and mail server. Support FastCGI, SSL, Virtual Host, URL Rewrite, Gzip and other functions. And supports many third-party module extensions.


Nginx's stability, feature set, sample configuration files, and low consumption of system resources made him come from behind, with a usage rate of 12.18% of active websites around the world, or about 22.2 million websites.


Nginx common functions


1. Http proxy, reverse proxy: As one of the most commonly used functions of web servers, especially reverse proxy.
2. Load balancing.  There are two types of load balancing strategies provided by Nginx: built-in strategies and extended strategies.
3. web cache, Nginx can cache different files differently, with flexible configuration, and supports FastCGI_Cache, which is mainly used to cache FastCGI dynamic programs. In conjunction with the third-party ngx_cache_purge, the content of the URL cache can be added or deleted.


Nginx configuration file structure:

```
$dir/wwwroot/                           - The root directory of the website, using the domain name as the folder name
    ./xuexb.com/
    ./static.xuexb.com/

$dir/src/                               - The installation source package

$dir/local/nginx/                       - nginx Related root
    ./conf/                             - configuration files
        ./nginx.conf                    - Configuring the main Entrance
        ./inc                           - GENERAL CONFIGURATION
        ./vhost/                        - Configuration of each site，use `domain name.conf` name
            ./xuexb.com.conf
            ./static.xuexb.com.conf

    ./1.11.1/                           - Versions of nginx
    ./1.11.2/

$dir/logs/                              - Log Related Directory，Within `domain name.type.log` name
        ./last/                         - Latest log
            ./xuexb.com.error.log
            ./xuexb.com.access.log
        ./back/                         - Day - level backup logs
            ./20170908/
```
