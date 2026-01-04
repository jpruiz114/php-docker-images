# Composer + PHP 8.5 FPM + Nginx + Node + Dependencies

## Build and test locally

```shell
cd composer-php-8.5-fpm-nginx-node-plus-dependencies

# Build the Docker image
docker build -t composer-php-8.5-fpm-nginx-node-plus-dependencies .

# Test the tools installed
docker run -d composer-php-8.5-fpm-nginx-node-plus-dependencies:latest sh -c "php --version && nginx -v && composer --version && node --version && npm --version && gifsicle --version && jpegoptim --version && optipng --version"

# Run web server on port 8181
docker run -d --name composer-php-8.5-plus-test -p 8181:80 composer-php-8.5-fpm-nginx-node-plus-dependencies:latest

# Check supervisor status (should show nginx and php-fpm running)
docker exec composer-php-8.5-plus-test supervisorctl status

# Test nginx configuration
docker exec composer-php-8.5-plus-test nginx -t

# Stop and remove test container
docker stop composer-php-8.5-plus-test && docker rm composer-php-8.5-plus-test

cd ..
```

## Push to hub.docker.com

```shell
cd composer-php-8.5-fpm-nginx-node-plus-dependencies
docker login registry-1.docker.io
docker build -t composer-php-8.5-fpm-nginx-node-plus-dependencies .
docker tag composer-php-8.5-fpm-nginx-node-plus-dependencies jpruiz114/composer-php-8.5-fpm-nginx-node-plus-dependencies:latest
docker push jpruiz114/composer-php-8.5-fpm-nginx-node-plus-dependencies:latest
cd ..
```

## Pull from hub.docker.com

```shell
docker pull jpruiz114/composer-php-8.5-fpm-nginx-node-plus-dependencies:latest
```

## Clean up after building

```shell
echo y | docker system prune -a
```
