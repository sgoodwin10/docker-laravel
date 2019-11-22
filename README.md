# docker-laravel

## Description

Build Laravel's development environment using docker.
Uses a persistant database store
PHP/MariaDB/nginx/composer/redis/node

## Usage

### Git clone

```
$ git clone git@github.com:sgoodwin10/docker-laravel.git
$ cd docker-laravel
```

### Docker compose build & up

```
$ docker-compose up -d --build
```

### Install Laravel using Composer

```
$ docker-compose exec app composer create-project --prefer-dist "laravel/laravel=6.0.*" .
$ docker-compose exec app composer require predis/predis
```

http://localhost:8080

### Running Migrations

```
$ docker-compose exec app php artisan migrate
```

### Running Testings

```
$ docker-compose exec app ash -l
$ cp .env.example .env.testing
$ php artisan key:generate --env testing
$ sed -i -e 's/<php>/<php>\n        <env name="DB_HOST" value="db-testing" force="true"\/>/' phpunit.xml
$ ./vendor/bin/phpunit
```

### Setup Laravel Elixir on 5.2 on Node container

```
$ docker-compose exec node apt-get install -y npm
```
Add Gulp
```
$ docker-compose exec node npm install --global gulp-cli
```
Install Elixir
```
$ docker-compose exec node npm install
```
If sass is required
```
$ docker-compose exec node npm install node-sass gulp-sass --save-dev
```
If notify is required
```
$ docker-compose exec node apt-get install libnotify-bin
```
Run gulp

## As necessary

Access the bash
```
docker-compose exec php bash
```

### Composer dump autoload

```
$ docker-compose exec app composer dump-autoload
```

### MySQL connection

```
$ docker-compose exec db bash -c 'mysql -uroot -p${MYSQL_PASSWORD} ${MYSQL_DATABASE}'
```

### Redis for Laravel

```
$ docker-compose exec app php artisan tinker
Redis::set('name', 'hoge');
Redis::get('name');
```

### Redis cli

```
$ docker-compose exec redis redis-cli
```


### Clone of exists code

```
$ git clone git@github.com:sgoodwin10/docker-laravel.git
$ cd docker-laravel
$ docker-compose up -d --build

$ git clone <source code url>
$ docker-compose exec app composer install
$ docker-compose exec app ash -l
$ cp .env.example .env
$ php artisan key:generate
$ php artisan migrate:fresh
```
