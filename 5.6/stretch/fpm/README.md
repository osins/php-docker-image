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