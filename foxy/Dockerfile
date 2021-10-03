FROM gitpod/workspace-full-vnc




#FROM dorowu/ubuntu-desktop-lxde-vnc:focal
#LABEL maintainer="Tiryoh<tiryoh@gmail.com>"
ENV HOME=/home/gitpod
ENV GITPOD_USER=gitpod

ENV DEBIAN_FRONTEND noninteractive
RUN echo "Set disable_coredump false" >> /etc/sudo.conf
RUN apt-get update -q && \
    apt-get upgrade -yq && \
    apt-get install -yq wget curl git build-essential vim sudo lsb-release locales bash-completion tzdata gosu && \
    rm -rf /var/lib/apt/lists/*
RUN useradd --create-home --home-dir $HOME --shell /bin/bash --user-group --groups adm $GITPOD_USER && \
    echo $GITPOD_USER:$GITPOD_USER | chpasswd && \
    echo "$GITPOD_USER ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers
COPY ros-foxy-desktop.sh /ros-foxy-desktop.sh
RUN mkdir -p /tmp/ros_setup_scripts_ubuntu && mv /ros-foxy-desktop.sh /tmp/ros_setup_scripts_ubuntu/ && \
    gosu $GITPOD_USER /tmp/ros_setup_scripts_ubuntu/ros-foxy-desktop.sh && \
    rm -rf /var/lib/apt/lists/*
RUN mv $HOME /home/gitpod_moved
ENV USER $GITPOD_USER
