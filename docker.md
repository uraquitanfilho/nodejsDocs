# Docker (optional)

> If you want to test using local database, you can use docker images

## Postgres Docker Image

```shell
docker run --name YOUR_IMAGE_ALIAS -e POSTGRES_PASSWORD=YOUR_PASSWORD -p 5432:5432 -v YOUR_LOCAL_PATH/data -d postgres
```

## Mongo Docker Image

```shell
sudo docker run --name YOUR_IMAGE_ALIAS -p 27017:27017 -v YOUR_LOCAL_PATH/data -d -t mongo
```

## to start

```shell
sudo docker start YOUR_IMAGE_ALIAS
```
