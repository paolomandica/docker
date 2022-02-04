# Docker Guidelines

## Build the image

From inside the directory containing the `Dockerfile` run the following command to build the image:

```sh
docker build -t sts-gcn \
--build-arg USER_ID=$(id -u) \
--build-arg GROUP_ID=$(id -g) .
```

## Run the container

Use the following command to run the container. Replace with the correct VOLUME PATH, PORT, GPUS, IMAGE.

```sh
docker run -it --shm-size 8G \
--name NAME -v VOLUME_PATH:/data_volume --gpus '"device=ID,"' sts-gcn
```

**Volume paths**

```sh
# DGX
/raid/data/francolu

# WKS
/home/ares/luca/panasonic
```