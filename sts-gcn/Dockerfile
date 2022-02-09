ARG PYTORCH="1.6.0"
ARG CUDA="10.1"
ARG CUDNN="7"

FROM pytorch/pytorch:${PYTORCH}-cuda${CUDA}-cudnn${CUDNN}-devel

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

RUN apt-get update && apt-get install -y git ninja-build \
    libglib2.0-0 libsm6 libxrender-dev libxext6 ffmpeg \
    build-essential cmake curl g++ ca-certificates \
    wget git nano tmux tree htop zip unzip \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

ENV PATH /opt/conda/bin:$PATH

# Install mmcv-full
RUN conda update -n base -c defaults conda && \
    conda install -c anaconda pip cython && \
    conda install -c conda-forge psutil tensorboard wandb && \
    pip install mmcv-full -f https://download.openmmlab.com/mmcv/dist/cu101/torch1.6.0/index.html && \
    conda clean --all

ENV FORCE_CUDA="1"
WORKDIR /home/$USER
USER $USER
ENV PATH $HOME/.local/bin:$PATH