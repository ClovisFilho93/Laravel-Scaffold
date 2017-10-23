## Laravel & Docker scaffold

Bootstrap your Laravel project in Docker with PHP7, MySQL, Nginx and Redis

#### How to setup the basic docker container
> Remember to always have the latest docker and docker-compose binaries.
* Copy the .env.example file: ```cp .env.example .env```
* Edit ```docker-compose.yml``` and replace the ```scaffold``` word with your directory name. Do the same for the files into ```./docker```
* Start docker: ```docker-compose up -d```
* Go to http://localhost:8080

#### How to connect to dependent containers (MySQL, Redis,...)
To avoid conflicts with existent containers in your development environment, it's better
to let docker decide which ports to expose to the host machine. If you need to know which
port your container is exposing you can use the `docker-compose ps` command

```shell
 $ docker-compose ps
        Name                       Command               State               Ports
----------------------------------------------------------------------------------------------
kindercoolweb_fpm_1     docker-php-entrypoint php-fpm    Up      9000/tcp
kindercoolweb_mysql_1   docker-entrypoint.sh mysqld      Up      0.0.0.0:32781->3306/tcp
kindercoolweb_nginx_1   nginx -g daemon off;             Up      443/tcp, 0.0.0.0:8080->80/tcp
kindercoolweb_redis_1   docker-entrypoint.sh redis ...   Up      0.0.0.0:32780->6379/tcp
```

In the `Ports` column, the first address is the exposed address, the second is the internal one.

In the example above, mysql is exposing port `32781` and redis is exposing `32780`.

Thanks [@alvaro](https://github.com/aguimaraes).