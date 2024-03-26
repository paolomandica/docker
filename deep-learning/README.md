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
export DATA_VOLUME="/mnt/homes/paolo/"
export CODE_VOLUME="/home/pmandica/"

docker compose up -d
```

## Commit the container to an image

After you have made changes to the container and you want to save them, you can commit the container to an image.

```sh
docker commit <container_id> paolomandica/<image_name>:<tag>
```
