FROM ubuntu:18.04

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

# Get Conda-ified Python.
RUN echo 'export PATH=/opt/conda/bin:$PATH' > /etc/profile.d/conda.sh && \
    wget --quiet https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh -O ~/miniconda.sh && \
    sh ~/miniconda.sh -b -p /opt/conda && \
    rm ~/miniconda.sh

ENV PATH /opt/conda/bin:$PATH

# Set CUDA_ROOT
RUN export CUDA_HOME="/usr/local/cuda"

WORKDIR /home/$USER
USER $USER