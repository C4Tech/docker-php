# PHP containers

A few basic PHP containers. The FPM images serve PHP privately on port 9000
and should be linked to an Nginx container. The composer container wraps the
official image and uses HHVM to speed up the process. There's also a CLI container for a Laravel application, configured to point to `artisan`.


## Configuration

Application location for FPM containers should match that of the Nginx
container. If you're using our `c4tech/nginx:php` image, your app root for the
FPM container should include `/app/public` as a mounted volume for processing
`index.php`. We use the `c4tech/generic-data` container to provide `/app` as a
linked volume.

We use the official `mariadb` and `redis` images for DB and cache services.


## Docker Compose example

```
appdata:
  image: c4tech/generic-data
  volumes:
    - ./:/app

artisan:
  image: c4tech/php:artisan
  command: env
  volumes_from:
    - appdata

composer:
  image: c4tech/php:composer
  command: install --no-dev --prefer-dist
  volumes_from:
    - appdata

fpm:
  image: c4tech/php:fpm
  volumes_from:
    - appdata
```
