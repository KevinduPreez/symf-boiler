# symf-boiler

## THIS IS FOR LOCAL DEVELOPMENT ONLY - DO NOT USE IN PRODUCTION

## Project Start - include into composer.json if not already

        "server-start": "symfony server:start ",
        "server-stop": "symfony server:stop",

        "database-start": "docker-compose up -d",
        "database-stop": "docker-compose down",

        "start": [
            "@database-start",
            "@server-start"
        ],
        "stop": [
            "@database-stop",
            "@server-stop"
        ],
        "restart": [
            "@stop",
            "@start"
        ],
        "migrate": "symfony console doctrine:migrations:migrate",
        "migrate-diff": "symfony console doctrine:migrations:migrate"
        
## For local dev MYSQL in Docker include
```
version: '3.7'
services:
  database:
    container_name: mysql
    image: 'mysql:8.0'
    environment:
      MYSQL_ROOT_PASSWORD: password
      MYSQL_DATABASE: main
    ports:
      # To allow the host machine to access the ports below, modify the lines below.
      # For example, to allow the host to connect to port 3306 on the container, you would change
      # "3306" to "3306:3306". Where the first port is exposed to the host and the second is the container port.
      # See https://docs.docker.com/compose/compose-file/#ports for more information.
      - '3306'
  phpmyadmin:
    image: phpmyadmin/phpmyadmin
    container_name: pma
    depends_on:
      - database
    links:
      - database
    environment:
      PMA_HOST: database
      MYSQL_USER: root
      MYSQL_PASSWORD: password
      DB_DATABASE: main
      PMA_PORT: 3306
      PMA_ARBITRARY: 1
    restart: always
    ports:
      - 8081:80
```
## Local Dev phpMyAdmin Setup

server: database

user: MYSQL_USER

password: MYSQL_PASSWORD
