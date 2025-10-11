# Snyk PHP 8.4 Docker Image

## Build and test locally

```shell
cd snyk-php-8.4
docker build -t snyk-php-8.4 .
docker run -d snyk-php-8.4:latest sh -c "composer --version && npm --version && php --version && snyk --version"
cd ..
```

## Push to hub.docker.com

```shell
cd snyk-php-8.4
docker login registry-1.docker.io
docker build -t snyk-php-8.4 .
docker tag snyk-php-8.4 jpruiz114/snyk-php-8.4:latest
docker push jpruiz114/snyk-php-8.4:latest
cd ..
```

## Pull from hub.docker.com

```shell
docker pull jpruiz114/snyk-php-8.4:latest
```

## Clean up after building

```shell
echo y | docker system prune -a
```