FROM nvidia/cuda:11.1-cudnn8-runtime-ubuntu18.04

SHELL ["/bin/bash", "--login", "-c"]

ARG USER_ID
ARG GROUP_ID

ENV USER=francolu
RUN addgroup --gid $GROUP_ID $USER
RUN adduser --home /home/$USER --disabled-password --gecos '' --uid $USER_ID --gid $GROUP_ID $USER

# Set timezone
ENV TZ=Europe/Rome
RUN ln -sf /usr/share/zoneinfo/Europe/Rome /etc/localtime

RUN apt-get update && apt-get install -y \
    build-essential \
    cmake \
    curl \
    g++ \
    wget \
    bzip2 \
    git \
    nano \
    tmux \
    screen \
    tree \
    htop \
    git \
    zip \
    unzip \
    ca-certificates \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

# Get Conda-ified Python for non-root user. old is /opt/conda
USER $USER

ENV CONDA_DIR $HOME/miniconda3
RUN wget --quiet https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh -O ~/miniconda.sh && \
    chmod +x ~/miniconda.sh && \
    ~/miniconda.sh -b -p $CONDA_DIR && \
    rm ~/miniconda.sh && \
    echo ". $CONDA_DIR/etc/profile.d/conda.sh" >> /home/$USER/.bashrc && \
    echo "conda activate base" >> /home/$USER/.bashrc

ENV PATH $CONDA_DIR/bin:$PATH
RUN conda init bash

# Set CUDA_ROOT
RUN export CUDA_HOME="/usr/local/cuda"

WORKDIR /home/$USER