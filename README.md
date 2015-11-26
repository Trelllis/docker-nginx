# Trellis • NGINX

Run the NGINX server configured to serve backend and frontend.

Requires that the code is distributed in the following form:

```
./code # document root
  /trellis_backend
  /trellis_frontend
```

Here's an example *docker-compose* file of mounting code and running a PHP app:

> Given that we're at the root and there are two folders **trellis_backend** and **trellis_frontend**.

```yaml
code:
    image: centos:7
    container_name: code
    volumes:
        - ./:/code
    command: /bin/sh -c "while true; do echo hello world > /dev/null; sleep 1; done"
web:
    image: trelllis/nginx
    container_name: web
    volumes_from:
        - code
    ports:
        - "8000:80"
    links:
        - php
php:
    image: vinelab/php-fpm
    container_name: php
    volumes_from:
        - code
    expose:
        - "9000"

```
