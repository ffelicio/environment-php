Exemplo de um ambiente php utilizando o projeto `ambientum`

```yml
version: '2'

volumes:
  mysql-data:
    driver: local
  redis-data:
    driver: local

services:
 bd:
    image: ambientum/mysql:5.7
    container_name: bd
    volumes:
      - mysql-data:/var/lib/mysql
    ports:
      - "3306:3306"
    environment:
      - MYSQL_ROOT_PASSWORD=sandbox
      - MYSQL_DATABASE=sandbox
      - MYSQL_USER=sandbox
      - MYSQL_PASSWORD=sandbox
  cache:
    image: ambientum/redis:3.2
    container_name: cache
    command: --appendonly yes
    volumes:
      - redis-data:/data
    ports:
      - "6379:6379"
  app:
    image: ambientum/php-alpine:7.0-nginx
    container_name: app
    volumes:
      - .:/var/www/app
    ports:
      - "80:8080"
    links:
      - mysql
```