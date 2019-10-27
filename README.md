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

http://127.0.0.1:10080

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

### Setup Laravel Elixir on 5.2

```
$ docker-compose exec php apt-get install -y npm
```
Add Gulp
```
$ docker-compose exec php npm install --global gulp-cli
```
Install Elixir
```
$ docker-compose exec php npm install
```
If sass is required
```
$ docker-compose exec php npm install node-sass gulp-sass --save-dev
```
If notify is required
```
$ docker-compose exec php apt-get install libnotify-bin
```

## As necessary

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

### Clear database volume

```
$ docker-compose down --volumes --rmi all
$ docker-compose up -d --build
$ docker-compose exec app php artisan migrate
```

### Clone of exists code

```
$ git clone git@github.com:ucan-lab/docker-laravel.git
$ cd docker-laravel
$ docker-compose up -d --build

$ git clone <source code url>
$ docker-compose exec app composer install
$ docker-compose exec app ash -l
$ cp .env.example .env
$ php artisan key:generate
$ php artisan migrate:fresh
```
