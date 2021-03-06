# LAPP stack built with Docker Compose

This is a basic LAPP stack environment built using Docker Compose. It consists following:

* PHP 7.4
* Apache 2.4
* PostgreSQL 9.5
* Redis

## Installation

Clone this repository on your local computer and switch to branch `master`. Run the `docker-compose up -d`.

```shell
git clone https://github.com/jbohme/docker-compose-lapp.git
cd docker-compose-lapp/
git fetch --all
cp sample.env .env
docker-compose up -d
```

Your LAPP stack is now ready!! You can access it via `http://localhost`.

## Configuration

This package comes with default configuration options. You can modify them by creating `.env` file in your root directory.

To make it easy, just copy the content from `sample.env` file and update the environment variable values as per your need.

### Configuration Variables

There are following configuration variables available and you can customize them by overwritting in your own `.env` file.

_**DOCUMENT_ROOT**_

It is a document root for Apache server. The default value for this is `./www`. All your sites will go here and will be synced automatically.

_**POSTGRESQL_DATA_DIR**_

This is POSTGRESQL data directory. The default value for this is `./data/postgresql`. All your PostgreSQL data files will be stored here.

_**VHOSTS_DIR**_

This is for virtual hosts. The default value for this is `./config/vhosts`. You can place your virtual hosts conf files here.

> Make sure you add an entry to your system's `hosts` file for each virtual host.

_**APACHE_LOG_DIR**_

This will be used to store Apache logs. The default value for this is `./logs/apache2`.

_**POSTGRESQL_LOG_DIR**_

This will be used to store Apache logs. The default value for this is `./logs/postgresql`.

## Web Server

Apache is configured to run on port 80. So, you can access it via `http://localhost`.

#### Apache Modules

By default following modules are enabled.

* rewrite
* headers

> If you want to enable more modules, just update `./bin/webserver/Dockerfile`. You can also generate a PR and we will merge if seems good for general purpose.
> You have to rebuild the docker image by running `docker-compose build` and restart the docker containers.

#### Connect via SSH

You can connect to web server using `docker-compose exec` command to perform various operation on it. Use below command to login to container via ssh.

```shell
docker-compose exec webserver bash
```

## Database

There are following configuration variables available and you can customize them by overwritting in your own .env file.

_**DATABASE**_

Switch the database vendor from postgresql. You can also easily add additonal database versions. 

## PHP

The installed version of PHP is 7.4

#### Extensions

By default following extensions are installed.

* pgsql
* pdo_sqlite
* pdo_pgsql
* mbstring
* zip
* intl
* mcrypt
* curl
* json
* iconv
* xml
* xmlrpc
* gd

> If you want to install more extension, just update `./bin/webserver/Dockerfile`. You can also generate a PR and we will merge if seems good for general purpose.
> You have to rebuild the docker image by running `docker-compose build` and restart the docker containers.

## Redis

It comes with Redis. It runs on default port `6379`.