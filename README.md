# Docker-Compose multi-stage build base

## Overview
- [Description](#description)
- [Project Structure](#project-structure)
- [Requirements](#requirements)
- [Usage](#usage)
- [Note](#note)

## Description
A docker-compose base project with multi-stage build for web full-stack application.</br>
This project is using custom Dockerfiles that are extending official docker images and will deploy 5 containers, 2 volumes and 1 network with a development or production build based on the value of <strong>PROJECT_MODE</strong> in the <strong>.env</strong> file.</br>
Cluster and Containers names are based on the value of <strong>COMPOSE_PROJECT_NAME</strong> in the <strong>.env</strong> file.</br>
You can have a look at the <strong>.env.example</strong> file to check default values used and put you're own in a <strong>.env</strong> file.</br>
By default this project will deploy on <strong>localhost</strong> with the development build on port <strong>443</strong>, I'm using a <strong>self-signed SSL certificate</strong> that I create in the Nginx Dockerfile.</br>
If you want to customize this stack for you're own needs, feel free to do it, you can refer to the [Project Structure Section](#project-structure) for more information.

How to test this project ? Check the [Usage section](#usage)

### Want some more info about ?
- Dockerfiles ==> [click here](https://docs.docker.com/engine/reference/builder/)
- Docker-Compose ==> [click here](https://docs.docker.com/compose/)
- Nginx official image ==> [click here](https://hub.docker.com/_/nginx)
- Php official image ==> [click here](https://hub.docker.com/_/php)
- Node official image ==> [click here](https://hub.docker.com/_/node)
- Mysql official image ==> [click here](https://hub.docker.com/_/mysql)
- Postgresql official image ==> [click here](https://hub.docker.com/_/postgres)

## Project Structure
```
├── DockerFiles (Folder with all different Dockerfile used)
|         |
|         ├── Mysql
|         |       |
|         |       ├── conf-default (default files to configure Mysql)
|         |       |
|         |       ├── Dockerfile (Dockerfile used for Mysql container)
|         |       |
|         |       └── mysql.env.example (Mysql ENV file used in docker-compose)
|         |
|         ├── Nginx
|         |       |
|         |       ├── conf (custom files to configure Nginx) currently using a template to allow ENV substitution
|         |       |
|         |       ├── conf-default (default files to configure Nginx)
|         |       |
|         |       └── Dockerfile (Dockerfile used for Nginx container)
|         |
|         ├── Node
|         |      |
|         |      └── Dockerfile (Dockerfile used for Node container)
|         |
|         ├── Php
|         |     |
|         |     ├── conf (custom files to configure Php)
|         |     |
|         |     ├── conf-default (default files to configure Php)
|         |     |
|         |     └── Dockerfile (Dockerfile used for Php container)
|         |
|         └── Postgresql
|                      |
|                      ├── conf-default (default files to configure Postgresql)
|                      |
|                      ├── Dockerfile (Dockerfile used for Postgresql container)
|                      |
|                      └── postgres.env.example (Postgresql ENV file used in docker-compose)
|
├── node-src (this folder is used as a volume bind mount)
|         |
|         └── Nextjs base src folder (only added a basepath configuration to access over '/node' url path)
|
├── php-src (sub-folders are used as volume bind mount)
|         |
|         ├── adminer (lightweight files to allow debugging and check if mysql and postgres database are good to go)
|         |
|         └── debug (a simple index.php file with a phpinfo() instruction to check Php version etc...)
|
├── .env.example (default ENV values example)
|
├── .gitignore (anything that should not appear on the repo, for example: '.env' files with secrets password / tokens etc...)
|
└── docker-compose.yml (docker-compose file used to instantiate everything)
```

## Requirements
- docker-compose version >= 3.5 (needed for the target instruction)
- .env file at the root of the project
- mysql.env file in Mysql folder
- postgres.env file in Postgresql folder

## Usage
### First time using this repo ?
- ```git clone https://github.com/ConiDev/docker-compose-multi-stage-build-base.git``` (download project)
- ```cd docker-compose-multi-stage-build-base``` (move to project folder)
- ```cp .env.example .env``` (create .env file at root of folder)
- ```cp DockerFiles/Mysql/mysql.env.example DockerFiles/Mysql/mysql.env``` (create mysql.env in Mysql folder)
- ```cp DockerFiles/Postgresql/postgres.env.example DockerFiles/Postgresql/postgres.env``` (create postgres.env in Postgresql folder)

### Start project:
- ```docker-compose up -d --build```

### Stop project:
- ```docker-compose down```

### Endpoints:
- ```https://localhost```   (You should see the Nginx welcome index)
- ```https://localhost/debug``` (You should see the Php info)
- ```https://localhost/adminer``` (You should see the adminer login page)
- ```https://localhost/node``` (You should see the Nextjs welcome index)

## Note
This Repo is an example project and should not be used directly for production deployment.

## License
This Project is under the [MIT License](/LICENSE)
