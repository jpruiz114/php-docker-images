# Composer + PHP 8.3 FPM + Nginx + Node

## Build and test locally

```shell
cd composer-php-8.3-fpm-nginx-node

# Build the Docker image
docker build -t composer-php-8.3-fpm-nginx-node .

# Test the tools installed
docker run -d composer-php-8.3-fpm-nginx-node:latest sh -c "php --version && nginx -v && nginx -t && node --version && npm --version && ps aux | grep supervisor && composer diagnose"

# Run web server on port 8181
docker run -d --name composer-php-8.3-test -p 8181:80 composer-php-8.3-fpm-nginx-node:latest

# Check supervisor status (should show nginx and php-fpm running)
docker exec composer-php-8.3-test supervisorctl status

# Test nginx configuration
docker exec composer-php-8.3-test nginx -t

# Stop and remove test container
docker stop composer-php-8.3-test && docker rm composer-php-8.3-test

cd ..
```

## Push to hub.docker.com

```shell
cd composer-php-8.3-fpm-nginx-node
docker login registry-1.docker.io
docker build -t composer-php-8.3-fpm-nginx-node .
docker tag composer-php-8.3-fpm-nginx-node jpruiz114/composer-php-8.3-fpm-nginx-node:latest
docker push jpruiz114/composer-php-8.3-fpm-nginx-node:latest
cd ..
```

## Pull from hub.docker.com

```shell
docker pull jpruiz114/composer-php-8.3-fpm-nginx-node:latest
```

## Clean up after building

```shell
echo y | docker system prune -a
```