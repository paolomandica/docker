FROM nvidia/cuda:11.1-cudnn8-runtime-ubuntu18.04

ENV TORCH_CUDA_ARCH_LIST="6.0 6.1 7.0+PTX"
ENV TORCH_NVCC_FLAGS="-Xfatbin -compress-all"
ENV CMAKE_PREFIX_PATH="$(dirname $(which conda))/../"

ARG USER_ID
ARG GROUP_ID

ENV USER=pinlab
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
    s3cmd \
    && ln -s /usr/lib/x86_64-linux-gnu/libGL.so.1 /usr/lib/x86_64-linux-gnu/libGL.so \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

# Get Conda-ified Python.
RUN echo 'export PATH=/opt/conda/bin:$PATH' > /etc/profile.d/conda.sh && \
    wget --quiet https://repo.anaconda.com/miniconda/Miniconda3-py38_4.10.3-Linux-x86_64.sh -O ~/miniconda.sh && \
    sh ~/miniconda.sh -b -p /opt/conda && \
    rm ~/miniconda.sh

ENV PATH /opt/conda/bin:$PATH

# Set CUDA_ROOT
RUN export CUDA_HOME="/usr/local/cuda"

# Install pytorch and mmcv
RUN conda install -c anaconda pip cython && \
    pip install torch==1.9.0+cu111 torchvision==0.10.0+cu111 torchaudio==0.9.0 -f https://download.pytorch.org/whl/torch_stable.html && \
    pip install mmcv-full -f https://download.openmmlab.com/mmcv/dist/cu111/torch1.9.0/index.html

# Install other python packages
RUN conda install -c conda-forge psutil tensorboard wandb opencv simplejson moviepy av && \
    pip install geoopt autopep8 && \
    conda clean --all

# Install DAVIS
RUN git clone https://github.com/xvjiarui/davis2017-evaluation.git
RUN cd davis2017-evaluation && python setup.py develop

ENV FORCE_CUDA="1"
WORKDIR /home/$USER
USER $USER