# Snyk PHP 8.5 Docker Image

## Build and test locally

```shell
cd snyk-php-8.5
docker build -t snyk-php-8.5 .
docker run -d snyk-php-8.5:latest sh -c "composer --version && npm --version && php --version && snyk --version"
cd ..
```

## Push to hub.docker.com

```shell
cd snyk-php-8.5
docker login registry-1.docker.io
docker build -t snyk-php-8.5 .
docker tag snyk-php-8.5 jpruiz114/snyk-php-8.5:latest
docker push jpruiz114/snyk-php-8.5:latest
cd ..
```

## Pull from hub.docker.com

```shell
docker pull jpruiz114/snyk-php-8.5:latest
```

## Clean up after building

```shell
echo y | docker system prune -a
```
