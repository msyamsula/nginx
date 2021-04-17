REQUIREMENTS
1. nginx (docker)

WHAT IS NGINX
1. nginx is reverse proxy server

ADVANTAGES OF NGINX
1. faster than apache
2. lightweight

TERMINOLOGY
1. directive, it is like variable in programming language
2. context, it is like function
3. variable

NOTES
1. nginx has 2 type, nginx bundle modules and 3rd party module
2. 3rd party module is nginx that is maintained by 3rd party
3. bundle modules that comes from nginx originally
4. nginx init script : https://www.nginx.com/resources/wiki/start/topics/examples/initscripts/
5. create file in directory /lib/systemd/system/nginx.service, copy and paste what happen in init script "systemd" section
6. change PIDfile path to match configuration in installation step 10
7. change sbin path to match configuration in installation step 10
8. serveral important context is 
    a. http, http related
    b. server, define our host
    c. location, to intercept and redirect certain url call
9. there is example in default.conf file about prefix, exact, and regex match use in location
10. order of match is
    a. exact
    b. preferential prefix
    c. regex sensitive, insensitive case
    d. prefix

INSTALLATION
with package manager
1. apt-get update
2. apt-get install nginx
3. nginx
with source and adding extra modules
4. wget http://nginx.org/download/nginx-1.19.10.tar.gz (download nginx tar), the link comes from http://nginx.org download section
5. tar -zvxf nginx-1.19.10.tar.gz (unzip it)
6. cd to nginx-1.19.10
7. apt-get install build-essential (get compiler)
8. apt-get install libpcre3 libpcre3-dev zlib1g zlib1g-dev libssl-dev (more linux nonsense)
9. run ./configure
10. run ./configure --sbin-path=/usr/bin/nginx --conf-path=/etc/nginx/nginx.conf --error-log-path=/var/log/nginx/error.log --http-log-path=/var/log/nginx/access.log --with-pcre --pid-path=/var/run/nginx.pid --with-http_ssl_module --> it tells nginx about sbin,conf, error log, http log, pcre, and pid path, along with option with http ssl module
11. run make
12. run make install

DOCUMENTATION
1. http://nginx.org (main documentation, primitive)
2. http://nginx.com (product site of nginx)

USEFULL COMMANDS
cli
1. nginx -h : help
2. nginx -s : send signal to background nginx
3. nginx -s stop : send stop signal to nginx background
nginx
server context:
    listen "port": to listen to port number
    server_name "name": ip_address/domain of our host
    root: where our resource located
    location context: where to intercept and channel to certain url
http context:
    include mime.types: include mime.types file in /etc/nginx for type handling