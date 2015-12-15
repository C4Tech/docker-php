# PHP-FPM containers

A few basic PHP 5.6 FPM container to serve PHP application privately. It is
configured to connect on port 9000 and should be linked to an Nginx container.


## Configuration

Application location should match that of the Nginx container.
If you're using our `c4tech/nginx:php` image, your app root should include
`/app/public` as a mounted volume. We use the `c4tech/generic-data` container
to provide `/app` as a linked volume.

We use the official `mariadb` and `redis` images for DB and cache services.


## Docker Compose example

```
fpm:
  image: c4tech/php-fpm:laravel
  volumes_from:
    - data
  working_dir: /app
```
