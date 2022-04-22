FROM nvidia/cuda:11.1-cudnn8-runtime-ubuntu18.04

ARG USER_ID=1013
ARG GROUP_ID=1010

ENV USER=pmandica
ENV HOME=/home/$USER
ENV DEBIAN_FRONTEND noninteractive

WORKDIR $HOME

RUN addgroup --gid $GROUP_ID $USER
RUN adduser --home $HOME --disabled-password --gecos '' \
    --shell /bin/bash --uid $USER_ID --gid $GROUP_ID $USER

# Set timezone
ENV TZ=Europe/Rome
RUN ln -sf /usr/share/zoneinfo/Europe/Rome /etc/localtime

RUN apt-get update && apt-get install -y dialog apt-utils && \
    apt-get install -y \
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
    apt-utils \
    ca-certificates \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

# Get Conda-ified Python for non-root user. old is /opt/conda
ENV CONDA_DIR /opt/conda
ENV PATH $CONDA_DIR/bin:$PATH

RUN wget --quiet https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh -O ~/miniconda.sh && \
    /bin/bash ~/miniconda.sh -b -p $CONDA_DIR && \
    rm ~/miniconda.sh && \
    ln -s $CONDA_DIR/etc/profile.d/conda.sh /etc/profile.d/conda.sh && \
    echo ". $CONDA_DIR/etc/profile.d/conda.sh" >> $HOME/.bashrc && \
    echo "conda activate base" >> $HOME/.bashrc && \
    $CONDA_DIR/bin/conda clean -afy

# Set CUDA_ROOT
RUN export CUDA_HOME="/usr/local/cuda"

RUN chown -R $USER:$USER /opt/conda
RUN chown -R $USER:$USER $HOME

USER $USER
