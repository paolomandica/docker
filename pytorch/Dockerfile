FROM nvcr.io/nvidia/pytorch:22.11-py3

# Set timezone
ENV TZ=Europe/Rome
RUN ln -sf /usr/share/zoneinfo/Europe/Rome /etc/localtime

RUN apt-get update && apt-get install -y tmux tree htop

USER $USER
