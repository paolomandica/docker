FROM nvidia/cuda:10.1-cudnn7-runtime-ubuntu18.04

# Set permission
ARG USER_ID
ARG GROUP_ID

ENV USER=dev

RUN addgroup --gid $GROUP_ID $USER
RUN adduser --home /home/$USER --disabled-password --gecos '' --uid $USER_ID --gid $GROUP_ID $USER

WORKDIR /home/$USER

ARG DEBIAN_FRONTEND=noninteractive
ENV TZ=Europe/Rome

RUN apt-get update && apt-get install -y \
    build-essential \
    cmake \
    curl \
    g++ \
    wget \
    bzip2 \
    git \
    vim \
    tmux \
    htop \
    git \
    zip \
    unzip \
    ca-certificates \
    libosmesa6-dev \
    libgl1-mesa-glx \
    libglfw3 \
    patchelf \
    libglu1-mesa \
    libxext6 \
    libxtst6 \
    libxrender1 \
    libxi6 \
    libjpeg-dev \
    libpng-dev \
    libopenblas-dev \
    libopencv-dev \
    libyaml-dev \
    libavformat-dev \
    libavcodec-dev \
    libswscale-dev \
    libavutil-dev \
    libavfilter-dev \
    libavdevice-dev \
    libswresample-dev \
    less \
    groff \
    memcached \
    s3cmd && \
    ln -s /usr/lib/x86_64-linux-gnu/libGL.so.1 /usr/lib/x86_64-linux-gnu/libGL.so

RUN apt-get clean && rm -rf /var/lib/apt/lists/*

RUN curl https://rclone.org/install.sh | bash

# Set timezone
RUN ln -sf /usr/share/zoneinfo/Europe/Rome /etc/localtime

# Get Conda-ified Python.
RUN echo 'export PATH=/opt/conda/bin:$PATH' > /etc/profile.d/conda.sh && \
    wget --quiet https://repo.anaconda.com/miniconda/Miniconda3-py38_4.10.3-Linux-x86_64.sh -O ~/miniconda.sh && \
    sh ~/miniconda.sh -b -p /opt/conda && \
    rm ~/miniconda.sh

ENV PATH /opt/conda/bin:$PATH

# Set CUDA_ROOT
RUN export CUDA_HOME="/usr/local/cuda"

# Install pytorch
RUN conda install pytorch=1.6.0 torchvision cudatoolkit=10.1 -c pytorch
RUN pip install simplejson psutil opencv-python tensorboard
RUN conda install av -c conda-forge
RUN conda install -c conda-forge moviepy

# Install decord
#RUN git clone --recursive https://github.com/dmlc/decord
#RUN cd decord && mkdir build && cd build && cmake .. -DUSE_CUDA=0 && make && cd ../python && python setup.py install
RUN pip install decord==0.4.2

# Install MMCV
RUN pip install mmcv-full -f https://download.openmmlab.com/mmcv/dist/cu101/torch1.6.0/index.html
# Install Kornia
#RUN pip install kornia
# RUN pip install git+https://github.com/kornia/kornia

# Install DAVIS
RUN git clone https://github.com/xvjiarui/davis2017-evaluation.git
RUN cd davis2017-evaluation && python setup.py develop

# Install zsh
# RUN sh -c "$(wget -O- https://github.com/deluan/zsh-in-docker/releases/download/v1.1.1/zsh-in-docker.sh)" -t robbyrussell -p git

USER $USER