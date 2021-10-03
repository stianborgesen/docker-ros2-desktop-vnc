FROM gitpod/workspace-full-vnc




#FROM dorowu/ubuntu-desktop-lxde-vnc:focal
#LABEL maintainer="Tiryoh<tiryoh@gmail.com>"
ENV GITPOD_HOME=/home/gitpod
ENV GITPOD_USER=gitpod
ENV USER=gitpod

ENV DEBIAN_FRONTEND noninteractive
#RUN echo "Set disable_coredump false" >> /etc/sudo.conf
RUN sudo apt-get update -q
RUN sudo apt-get upgrade -yq 
RUN sudo apt-get install -yq wget curl git build-essential vim sudo lsb-release locales bash-completion tzdata gosu
RUN sudo rm -rf /var/lib/apt/lists/*
RUN sudo useradd --create-home --home-dir $GITPOD_HOME --shell /bin/bash --user-group --groups adm $GITPOD_USER && \
    sudo echo $GITPOD_USER:$GITPOD_USER | chpasswd && \
    sudo echo "$GITPOD_USER ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers
COPY sudo ros-foxy-desktop.sh /ros-foxy-desktop.sh
RUN sudo mkdir -p /tmp/ros_setup_scripts_ubuntu && sudo mv /ros-foxy-desktop.sh sudo /tmp/ros_setup_scripts_ubuntu/ && \
    sudo gosu $GITPOD_USER /tmp/ros_setup_scripts_ubuntu/ros-foxy-desktop.sh && \
    sudo rm -rf /var/lib/apt/lists/*
#RUN mv $GITPOD_HOME /home/gitpod_moved
ENV USER $GITPOD_USER
