# PHP-FPM container

A basic PHP 5.6 FPM container to serve a PHP application privately. It is
configured to connect on port 9000 and should be linked to an Nginx container.


## Configuration

Application location should match that of the Nginx container.
If you're using our `c4tech/laravel-nginx` image, your app root should include
`/app/public`as a mounted volume. We use the `c4tech/generic-data` container
to provide `app` as a linked volume.

We use the official `mariadb` and `redis` images for DB and cache services.


## Docker Compose example

```
fpm:
  image: c4tech/laravel-fpm
  volumes_from:
    - data
  working_dir: /app
```
