REQUIREMENTS
1. nginx (docker)
2. tutorial.basic.conf consist of basic nginx syntax with comment to understand it

WHAT IS NGINX
1. nginx is reverse proxy server

ADVANTAGES OF NGINX
1. faster than apache
2. lightweight

TERMINOLOGY
1. directive, it is like variable in programming language
2. context, it is like function
3. variable, user defined, nginx defined ($host, $uri, $arg): nginx defined variable available in nginx.org variable section

NOTES
1. nginx has 2 type, nginx bundle modules and 3rd party module
2. 3rd party module is nginx that is maintained by 3rd party
3. bundle modules that comes from nginx originally
4. nginx init script : https://www.nginx.com/resources/wiki/start/topics/examples/initscripts/
5. create file in directory /lib/systemd/system/nginx.service, copy and paste what happen in init script "systemd" section
6. change PIDfile path to match configuration in installation step 10
7. change sbin path to match configuration in installation step 10
8. several important context is 
    a. http, http related
    b. server, define our host
    c. location, to intercept and redirect certain url call
9. there is example in default.conf file about prefix, exact, and regex match use in location
10. order of match is
    a. exact
    b. preferential prefix
    c. regex sensitive, insensitive case
    d. prefix
11. there is concept of redirect and rewrite
12. redirect is about changing url when certain url is called, it is happening in location block
13. rewrite is about renaming url that is comes to nginx, it can happen before location block
14. when redirecting to a file you need to return 307 in nginx (it is the standar) and 301 for redirecting
15. rewrite change url, without user knowing, it change before the call
16. redirect change url and can be known by user, it change after the call
17. try_files concept, for more comprehensive explanation see "tutorial.basic.conf" in TRY_FILES section
18. nginx worker concept. it is a process that handle our request in nginx
19. adding nginx worker doesn't directly mean it enhance the performance, hardware limitation plays a role in this one
20. Usually, nginx worker never exceed cpu core of our machine.. SEE tutorial.basic.conf section WORKER
21. action directive like "return 200 'Hello'" doesn't affected by rate limiting or authentication
22. to maintain nginx, run apt-get update and apt-get upgrade periodically in your server
23. several header to secure your nginx, use in server context
    a. add_header X-Frame-Options "SAMEORIGIN" --> prevent usage from other party
    b. add_header X-XSS-Protection "1; mode=block"; --> prevent cross site scripting
24. attacker somehow can do attack based on our nginx version. so remove nginx version from caller can a little bit secure our nginx



HTTPS
1. you need to get your certificate, check usefull command no. 9 to get your certificate, and certificate key
2. listen to 443 with ssl and provide certificate and key to nginx
3. for more detail implementation see tutorial.basic.conf HTTPS section
4. 1st step to securing http call is to redirect all http request to https request
5. you can use SSL (secure socket layer) to crete https, however, there is more current technology called TLS (transport layer security), set SSL to use TLS protocol
6. to secure https, it is better to implement rate limiting request
7. you need siege package to test rate limiting (apt-get install siege)
8. siege is package to simulate rate request

AUTHENTICATION URL
1. install apahce utils (usefull_commands 12)

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
4. nginx -s reload : reload nginx
5. nginx : start nginx
6. nproc : see cpu core
7. lscpu : detail cpu for a machine
8. nginx -V : see detail nginx installation with its module
9. openssl req -x509 -days 10 -nodes -newkey rsa:2048 -keyout /etc/nginx/ssl/self.key -out /etc/nginx/ssl/self.crt : get ssl key
10. openssl dhparam -out /etc/nginx/ssl/dhparam.pem 2048: create dhparam for TLS
11. apt-get install siege : install siege
12. apt-get install apache2-utils : for basic auth in nginx
13. htpasswd -c /etc/nginx/.htpasswd "username" : create htpasswd
14. nginx -c /aboslute/path/to/conf/file : start nginx with user define config file
