# Docker Guidelines

## Build the image

From inside the directory containing the `Dockerfile` run the following command to build the image:

```sh
docker build -t ubuntu-18.04-conda \
--build-arg USER_ID=$(id -u) \
--build-arg GROUP_ID=$(id -g) .
```

## Run the container

Use the following command to run the container. Replace with the correct VOLUME PATH, PORT, GPUS, IMAGE.

```sh
docker run -it --shm-size 12G \
--name NAME -v VOLUME_PATH:/data_volume \
--gpus '"device=ID,"' ubuntu-18.04-conda
```

**For specific servers**

```sh
# DGX
docker run -it --shm-size 12G \
-v /raid/data/francolu:/data_volume \
--name NAME --gpus all ubuntu-18.04-conda
```

```sh
# Ares WKS
docker run -it --shm-size 12G \
-v /home/ares/luca/panasonic:/code_volume -v /storage:/data_volume \
--name NAME --gpus '"device=ID,"' ubuntu-18.04-conda
```

Once the container is up, you should run:

```sh
conda init bash && exec bash
export PATH="$HOME/.local/bin:$PATH"

```
