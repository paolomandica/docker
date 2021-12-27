FROM pytorch/pytorch:1.8.1-cuda11.1-cudnn8-devel

# Set permission
ARG USER_ID
ARG GROUP_ID

ENV USER=francolu

RUN addgroup --gid $GROUP_ID $USER
RUN adduser --home /home/$USER --disabled-password --gecos '' --uid $USER_ID --gid $GROUP_ID $USER

# Set the working directory and user
WORKDIR /home/$USER

# Set timezone
ENV TZ=Europe/Rome
RUN ln -sf /usr/share/zoneinfo/Europe/Rome /etc/localtime

# Clone the repo
RUN apt-get update && \
    apt-get install -y \
    build-essential \
    git \
    nano \
    tree \
    screen \
    tmux \
    wget \
    ffmpeg \
    htop \
    unzip

RUN python -m pip install --upgrade pip
RUN python -m pip install --upgrade pillow

# Clone and install evaluation repo
RUN git clone https://github.com/davisvideochallenge/davis2017-evaluation.git
RUN cd davis2017-evaluation && python setup.py install

# Install python packages
RUN pip install pillow imageio matplotlib scikit-image scikit-learn \
    wandb visdom opencv-contrib-python av pillow scipy joblib \
    plotly moviepy kornia
RUN pip install decord==0.4.2
RUN pip install mmcv-full -f https://download.openmmlab.com/mmcv/dist/cu111/torch1.8.0/index.html

USER $USER