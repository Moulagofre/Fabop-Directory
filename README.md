[![License](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](https://opensource.org/licenses/Apache-2.0)
[![AppVeyor](https://img.shields.io/appveyor/ci/moulagofre/fabop-directory.svg)]()
[![pipeline status](https://gitlab.com/moulagofre/fabop-directory/badges/master/pipeline.svg)](https://gitlab.com/moulagofre/fabop-directory/commits/master)
[![coverage report](https://gitlab.com/moulagofre/fabop-directory/badges/master/coverage.svg)](https://gitlab.com/moulagofre/fabop-directory/commits/master)

# FABOP directory

Directory management application of the organization [La Fabrique Opéra Val de Loire](http://www.lafabriqueopera-valdeloire.com/) under Apache 2.0 license.

## Technicals details

The project is maintained under Symfony Frameworks and is using Php as back-end main language.

Front-end is maintained with npm modules as gulp-sass, bootstrap and jquery. Html templates are using Twig.

## Docker stack

The project handle a Docker configuration made for a 4 containers stack :

    - web : Nginx container
        port : 80
        image : debian:stretch

        Handle Http requests through Nginx web reverse proxy

    - php : Php-fpm container
        port : 9000
        image : php:7.2-fpm-alpine

        Handle php backend scripts execution. Serve Nginx on port 9000.

    - mysqldb : MariaDB MySQL Database
        port : 3306
        image : mariadb

        Handle relational type data through Doctrine component.

    - mongodb : MongoDB NoSQL Database
        port : 27017
        image : mongo:latest

        Handle collection/document type data through custom Data management system.

## Getting Started

These instructions will get you a copy of the project up and running on your local machine for development and testing purposes. See deployment for notes on how to deploy the project on a live system.

### Prerequisites

1. Make sure you have php7.2, composer installed.

    **Install PHP 7.2**
    
    `apt-get update`
    
    `apt-get install php-cli`
    
    `apt-get install php-curl php-gd php-intl php-json php-mbstring php-xml php-zip php-mysql php-mongodb`
    
    **Install composer**
    
    `apt install composer`

2. Install git for being able to clone the project, make commits and push, etc...

    `apt-get install git`
    
3. Install nodejs and yarn.

    `apt-get install nodejs npm`
    
    `curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | sudo apt-key add -`
    
    `echo "deb https://dl.yarnpkg.com/debian/ stable main" | sudo tee /etc/apt/sources.list.d/yarn.list`
    
    `apt-get update && apt-get install yarn`

4. Docker dependencies

    Ubuntu : https://docs.docker.com/install/linux/docker-ce/ubuntu/

    Debian : https://docs.docker.com/install/linux/docker-ce/debian/

    Fedora : https://docs.docker.com/install/linux/docker-ce/fedora/
    
    CentOS : https://docs.docker.com/install/linux/docker-ce/centos/


    Windows : https://docs.docker.com/docker-for-windows/install/

### Setting up Docker dev environment

1. First, you need to clone the project and install dependencies with following command lines :

    `git clone https://gitlab.com/moulagofre/fabop-directory`
    
    `cd fabop-directory/app`
    
    `yarn install`
    
    `composer install`

2. Then, when cloning is complete, you can run migrations and gulp routines to make front-end and back-end working.

    `yarn run gulp styles`
    
    `yarn run gulp js`
    
    `yarn run gulp fa`
    
    `yarn run gulp animations`
    
    `yarn run gulp images`
    
    `yarn run gulp fonts`

3. Edit app/.env and set `APP_ENV` to `dev`

4. Set DB passwords in `docker-compose.yml` and copy them into `app/.env` by replacing `<SET PASSWORD HERE>` placeholders. Set also mongodb password in `build/mongodb/mongo-init.js`.

5. Now, build docker images and start it :

    `docker-compose build` (may take few minutes)
    
    `docker-compose up`

    Use `docker-compose start/stop` to manage containers (or any GUI Docker containers manager)

6. Make db migrations by using following commands :

    `docker-compose exec php bin/console --no-interaction doctrine:migrations:diff`

    `docker-compose exec php bin/console --no-interaction doctrine:migrations:migrate`

7. If you need to enter containers terminal :

    `docker exec -it <mycontainer> bash`

### Running the tests

1. Test mongodb manager (custom data retriever) :

    You can run tests with :
    
    `php ./bin/phpunit tests/MongoManagerTest.php --testdox`
    
    OR
    
    `php ./bin/phpunit tests/MongoManagerTest.php` if you want to check details and errors.
    
    **Those tests may not pass if some database's data are not precisely set.**

## Deployment / production server installation

*Will come later*

## Built With

* Php 7.2.16
* JavaScript
* Twig

* Symfony 4.1.7 - The web framework used (PHP)
* npm/yarn - Dependency Management
* Bootstrap 4 - CSS framework
* jquery - JS framework
* fontawesome - Icons font
* Docker - Containers

* MariaDB - MySQL Database
* MongoDB - NoSQL Database