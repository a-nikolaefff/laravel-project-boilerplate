# Laravel Project Boilerplate

### [Russian version of the readme](./README-ru.md)

## Description
A build for quickly deploying a local environment for PHP development.
The build  is designed for the WSL (Windows Subsystem for Linux) environment, and
was tested on Ubuntu 22.04.2 LTS built into Windows 10.

## Composition
* Laravel 10 (latest)
* PHP 8.2
* Xdebug
* Composer
* Node.js
* PostgreSQL 15.1
* MySQL 5.7

## Initializing a new Laravel project
* Clone the repository to a new directory using the command:
```
git clone https://github.com/A-Nikolaefff/laravel-project-boilerplate.git YOUR_PROJECT_NAME
```
* Delete the **.geetkeep** file from the **src** directory.
  At the time of creating a new project, this directory must be empty.
* In the project directory run the command: 
```
make up
```
* Wait for docker containers to build and run and 
in the project directory run the command:
```
make init
```
* Check that the project is available at http://localhost:8080/ .
  The first launch of the application may take a long time.

## Command list

* ```make build``` - build containers
* ```make up``` - start containers
* ```make down``` - stop containers
* ```make init``` - initialize a new Laravel project
* ```make list``` - list of running containers
* ```make enter name=SERVICE``` - go to a running container (open command line 
terminal). Replace ```SERVICE``` with the service name according to
**docker-compose.yml**, for example ```php```, ```pgsql``` or ```nginx``` 
and so on
* ```make php``` - go to php container
* ```make npm``` - go to npm container
* ```make vite``` - run Vite's built-in dev server to track changes to css and js files
* ```make vite-build``` - build css and js files for production

## Setting up Xdebug in PHPStorm
* Default server name: **docker**
* Host: **localhost**
* Port: **8080**
* Use path mapping between **src** directory and **/var/www/html** path

## Possible problems

* The default Vite configuration is not intended to be used in a docker container 
and therefore will not work correctly out of the box. To work correctly, edit 
the configuration file **vite.config.js** by adding the following code between 
the lines ```export default defineConfig({``` and ```plugins: [```:
```
  server: {
  host: '0.0.0.0',
  hmr: {
  host: 'localhost'
  },
  port: 3009,
  watch: {
  usePolling: true
  }
  },
```

* In order for PostgreSQL docker container volumes to work correctly, the UID/GID
  of the user inside the container must match the value of the local Linux user.  
  By default, this container starts with UID/GID 1000/1000. If the UID/GID of the
  local user is different you must run the ```export LOCAL_UID=$(id -u)```
  and ```export LOCAL_GID=$(id -g)``` commands before starting the PostgreSQL
  container for the first time.


