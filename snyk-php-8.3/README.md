# Snyk PHP 8.3 Docker Image

## Build and test locally

```shell
cd snyk-php-8.3
docker build -t snyk-php-8.3 .
docker run -d snyk-php-8.3:latest sh -c "composer --version && npm --version && php --version && snyk --version"
cd ..
```

## Push to hub.docker.com

```shell
cd snyk-php-8.3
docker login registry-1.docker.io
docker build -t snyk-php-8.3 .
docker tag snyk-php-8.3 jpruiz114/snyk-php-8.3:latest
docker push jpruiz114/snyk-php-8.3:latest
cd ..
```

## Pull from hub.docker.com

```shell
docker pull jpruiz114/snyk-php-8.3:latest
```

## Clean up after building

```shell
echo y | docker system prune -a
```
