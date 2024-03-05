# Docker Guidelines

## Build the image

From inside the directory containing the `Dockerfile` run the following command to build the image:

```sh
docker build -t ubuntu-22.04-deep-learning \
--build-arg HOST_UID=$(id -u) \
--build-arg HOST_GID=$(id -g) .
```

## Run the container with docker-compose

Use the following command to build the image and run the container directly.

```sh
export HOST_UID=$(id -u)
export HOST_GID=$(id -g)
export DATA_VOLUME="..."
export CODE_VOLUME="..."
export SHM_SIZE="12G"

docker-compose up -d
```
