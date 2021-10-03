FROM dorowu/ubuntu-desktop-lxde-vnc:focal
LABEL maintainer="Tiryoh<tiryoh@gmail.com>"

ENV USELESS_ENV_TO_TRIGGER_FULL_REBUILD true
ENV DEBIAN_FRONTEND noninteractive
RUN echo "Set disable_coredump false" >> /etc/sudo.conf
RUN apt-get update -q && \
    apt-get upgrade -yq && \
    apt-get install -yq wget curl git build-essential vim sudo lsb-release locales bash-completion tzdata gosu && \
    rm -rf /var/lib/apt/lists/*
RUN useradd --create-home --home-dir /home/gitpod --shell /bin/bash --user-group --groups adm,sudo ubuntu && \
    echo gitpod:gitpod | chpasswd && \
    echo "gitpod ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers
COPY foxy/ros-foxy-desktop.sh /ros-foxy-desktop.sh
RUN mkdir -p /tmp/ros_setup_scripts_ubuntu && mv /ros-foxy-desktop.sh /tmp/ros_setup_scripts_ubuntu/ && \
    gosu ubuntu /tmp/ros_setup_scripts_ubuntu/ros-foxy-desktop.sh && \
    rm -rf /var/lib/apt/lists/*
ENV USER gitpod
