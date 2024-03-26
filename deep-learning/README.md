# Docker Guidelines

## Build the image

From inside the directory containing the `Dockerfile` run the following command to build the image:

```sh
docker build -t paolomandica/ubuntu-22.04-deep-learning \
--build-arg UID=$(id -u) \
--build-arg GID=$(id -g) .
```

## Run the container with docker-compose

Use the following command to build the image and run the container directly.

```sh
export UID=$(id -u)
export GID=$(id -g)
export DATA_VOLUME="/home/pmandica/"
export CODE_VOLUME="/mnt/homes/paolo/"

docker-compose up -d
```
