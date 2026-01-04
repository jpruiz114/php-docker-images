# Composer + PHP 8.5 + Xdebug

## Build and test locally

```shell
cd composer-php-8.5-xdebug
docker build -t composer-php-8.5-xdebug .
docker run -d composer-php-8.5-xdebug:latest sh -c "composer --version && php --version"
cd ..
```

## Push to hub.docker.com

```shell
cd composer-php-8.5-xdebug
docker login registry-1.docker.io
docker build -t composer-php-8.5-xdebug .
docker tag composer-php-8.5-xdebug jpruiz114/composer-php-8.5-xdebug:latest
docker push jpruiz114/composer-php-8.5-xdebug:latest
cd ..
```

## Pull from hub.docker.com

```shell
docker pull jpruiz114/composer-php-8.5-xdebug:latest
```

## Clean up after building

```shell
echo y | docker system prune -a
```
