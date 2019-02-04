# ambielecki/docker-skeleton

This is WIP of a simple starting point for connecting multiple web containers 
behind an nginx-proxy. I am currently using it for PHP based projects, but there is no reason 
this should not work with Node, Python, etc or with other DB providers.

* Clone this project in the root folder where your web projects are based
* Copy docker-compose.yml.example to docker-compose.yml
* Change path mappings and host names to match your setup
* Create a live-builds folder under the repos root and a folder to hold the builds for each 
web service.
* Register hosts (eg. example.test) in your machines hosts file
* This should work with xdebug as well, replace docker.for.win.localhost in the xdebug.ini if 
you are on a mac (make sure you use a separate listen port for each apache or php-fpm container)
* HTTPS is a work in progress, you'll need to create a certs folder and generate a self signed
cert for each site.  use the ssl_command_example.txt and replace the divelog.test domain with 
your own.  You'll need to set the certificate as trusted through the mac keychain or Microsoft 
Management Control (google is your friend here), you can also create self signed certs see 
[self-signed certs](https://deliciousbrains.com/ssl-certificate-authority-for-local-https-development/)
* You will need to ssh into the db container or connect through port 33060 with a desktop client
to create schemas and users (for mysql may I suggest creating the users with mysql_native_password 
like `CREATE USER 'example_user'@'%' IDENTIFIED WITH mysql_native_password BY 'example_pwd'` 
for better Laravel compatibility, or just use mysql 5.7)

Note the example .conf files are setup for Laravel projects