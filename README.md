# Parcial 1 - Jimena Vadillo Gutiérrez
## docker-compose.yml
It is a yml extension file where we can define the container _version_, _services_, _volumes_, among others. The top level props that compose the file in this project are the following:  
- version: Indicates the format version of the docker compose file. In terms of compability, we can use an specific format version but its recommended to use the lastest version.
- services: Indicates the resources of the container, we can specify what services our container will use. in this top level props we can find: 
  - image: Defines the docker image that wil manage the container, we can specify the version of the image if there is more than one.
  - restart: Defines the behavior of the container when it stops.
  - environment: Define the values of the environment variables. Each docker image cn have different variables.
  - ports: Defines in which port the container will run.
  - volumes: Defines the folder management implemented by the host.

Why every level have line breaks with each other?. This is because of the best indent practices.

## DB Folder
This folder contains a database managed by MariaBB container. Exists three folders within that synchronize with the container (defined in docker-compose.yml, volumes line 15 to 18).
- conf: Contains the database configuration. 
- files: Contains the database files.
- logs: Contains the database logs
### DB docker-compose file
- version: 3.1: We use the docker 3.1 format version
- services: In this top level props we define the services that our container will use.
- mydatabase: We specify the name of the container.
- image: We use MariaDB docker image.
- restart: Always restart when container suddenly stops.
- environment: We define the container environment variables.
  - MYSQL_ROOT_PASSWORD: We define the password of the database root
  - MYSQL_DATABASE: We define the name of the database
  - MYSQL_USER: We define the name of the user of the database. If this variable and `MYSQL_PASSWORD` are below `MYSQL_DATABASE`, the user will have complete access of the database.
  - MYSQL_PASSWORD: We define the password of the declared user. If this variable and `MYSQL_USER` are below `MYSQL_DATABASE`, the user will have complete access of the database.
- ports: We will be running this container in port 3306.
- volumes: We define what it will contain the folders we created (conf, files, logs).
## Web Folder
This folder contains a web application container created in PHP. Exists a folder `app` that contains the source code of the project, also we can found the docker compose file within the root folder.

### Web docker-compose file
- version: 3.1: We use the docker 3.1 format version
- services: In this top level props we define the services that our container will use.
- measurementapp: We specify the name of the container.
  - image: We use the version 7.4 of the docker image webdevops/php-nginx.
  - restart: Always restart when container suddenly stops.
  - environment: We define the container environment variables.
    - PHP_DISPLAY_ERRORS: We want to see the errors that the application returns.
  - ports: We will be running this container in port 80.
  - volumes: We define that our app folder will contain the source code of the project.