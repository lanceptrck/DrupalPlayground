# DevOps3 Docker4Drupal Tutorial

This project runs down through installing Drupal via Docker in your local machine through the help of ([Wodby.](https://wodby.com/docs/1.0/stacks/drupal/local/#usage))

## Usage

1. First you need to clone this repository:
```
$ git clone https://github.com/lanceptrck/DrupalPlayground.git devops3_drupal
```
2. Next we need to change to the devops3_drupal directory and unzip the docker compose files:
```
$ cd devops3_drupal
$ unzip docker4drupal.zip
```
3. After unzipping the docker compose files, we then run docker compose
```console
$ docker-compose up -d
```
4. If it builds and runs successfully you should see:
```
Starting devops3_docker_project_traefik ... done
Starting devops3_docker_project_php     ... done
Starting devops3_docker_project_crond   ... done
Starting devops3_docker_project_mailhog ... done
Starting devops3_docker_project_mariadb ... done
Starting devops3_docker_project_nginx   ... done
```
5.  Now we should setup our Drupal enviroment for development, on your CLI: this installs all the dependencies for setting up our environment. This might take a while.
```
$ docker exec -it $(docker ps -aq -f name=php) /bin/sh
root@os:~ $ composer require drupal/devel
```
6. After all of the dependencies are installed, navigate through `var\www\html\web` and open `settings.php`. We will update the local database for this copying the block below. This ensures database access settings in your `settings.php` corresponds to values in `.env` file:
```
$databases['default']['default'] = array (
  'database' => 'devops3', // same as $DB_NAME
  'username' => 'devops3', // same as $DB_USER
  'password' => 'devops3', // same as $DB_PASSWORD
  'host' => 'mariadb', // same as $DB_HOST
  'driver' => 'mysql',  // same as $DB_DRIVER
  'port' => '3306', // different for PostgreSQL
  'namespace' => 'Drupal\\Core\\Database\\Driver\\mysql', // different for PostgreSQL
  'prefix' => '',
);
```
8.  Your drupal website should be up and running at  [http://devops3.docker.localhost:8077](http://devops3.docker.localhost:8077)