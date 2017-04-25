### Introdução
Nesse projeto vou só exemplificar alguns modelos de `docker-compose.yml` utilizando o ambiente de desenvolvimento da galera do `codecasts` [https://github.com/codecasts/ambientum](https://github.com/codecasts/ambientum).

#### Primeiro modelo
* Nesse primeiro exemplo, vou criar um modelo com 3 serviços `(Mysql, Redis e PHP)`
* Crie um arquivo `docker-compose.yml` com o conteúdo abaixo. 

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
      - MYSQL_ROOT_PASSWORD=SEU_USUARIO_ROOT
      - MYSQL_DATABASE=SEU_BANCO_DE_DADOS
      - MYSQL_USER=SEU_USUARIO
      - MYSQL_PASSWORD=SUA_SENHA
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

#### Segundo Modelo
```
Em construção
```

* Depois de escolher seu modelo e criar seu `docker-compose`, crie um diretório  `public` na raiz do seu projeto junto com um arquivo `index.php`, e adicione o seguinte conteudo:
```php
<?php phpinfo()
```

* Agora execute o seguinte comando `docker-compose up --build` para construtir sua stack.
* Agora acesse seu `http:\\localhost`