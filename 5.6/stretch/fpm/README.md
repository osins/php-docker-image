# Docker wangsying images

the image is a php-fpm by 5.6.40

## the image suppprt:

```console
redis
memcached
iconv
mcrypt
gd
curl
mysqli
pdo
pdo_mysql
mbstring
json
```

## How to use this image
### Create a `Dockerfile` in your PHP project

```dockerfile
FROM wangsying/php5
COPY . /var/www/code
WORKDIR /var/www/code
CMD [ "php", "./your-script.php" ]
```

Then, run the commands to build and run the Docker image:

```console
$ docker build -t my-php-app .
$ docker run -it --rm --name my-running-app my-php-app
```

### Run a single PHP script

For many simple, single file projects, you may find it inconvenient to write a complete `Dockerfile`. In such cases, you can run a PHP script by using the PHP Docker image directly:

```console
$ docker run -it --rm --name my-running-script -v "$PWD":/var/www/code -w /var/www/code wangsying/php5 php your-script.php
```
### Nginx + PHP fpm 

#### Nginx server config
```nginx config

server {
    ...

    location ~ \.php {
        root /var/www/code;

        fastcgi_pass php5-fpm:9000;
        fastcgi_index index.php;
        fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;
        include fastcgi_params;
    }

    ...
}
```

#### docker compose config docker-compose.yaml :

```compose config

version: '3.3'
services:        
  nginx:
    image: nginx
    container_name: nginx
    hostname: nginx
    privileged: true
    restart: always
    depends_on:
        - "php5-fpm"
    ports:
        - '8080:80'
    networks:        
        - "webapp-network"
    volumes:
        - $PWD/default.conf:/etc/nginx/conf.d/default.conf
        - $PWD/log/nginx:/var/log
        - $PWD/code:/var/www/code

php5-fpm:
  image: wangsying/php5
  container_name: php5-fpm
  hostname: php5-fpm
  privileged: true
  restart: always
  networks:        
  - "webapp-network"
  volumes:
    - $PWD/log/nginx:/var/log
    - $PWD/code:/var/www/code

networks:
  webapp-network:
    driver: bridge
  default:
    external:
      name: webapp-network

```

docker-compose start:
```docker-compose run

docker-compose up -d

```
docker-compose down:
```

docker-compose down -v

```