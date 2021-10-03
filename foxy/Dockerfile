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
#RUN sudo useradd --create-home --home-dir $GITPOD_HOME --shell /bin/bash --user-group --groups adm $GITPOD_USER && \
#    sudo echo $GITPOD_USER:$GITPOD_USER | chpasswd && \
#    sudo echo "$GITPOD_USER ALL=(ALL) NOPASSWD:ALL" >> /etc/sudoers
COPY ros-foxy-desktop.sh /ros-foxy-desktop.sh
RUN sudo mkdir -p /tmp/ros_setup_scripts_ubuntu && sudo mv /ros-foxy-desktop.sh /tmp/ros_setup_scripts_ubuntu/
#RUN sudo gosu $GITPOD_USER /tmp/ros_setup_scripts_ubuntu/ros-foxy-desktop.sh

RUN set -eu

# This install script is based on https://github.com/Tiryoh/ros2_setup_scripts_ubuntu, released under the Apache-2.0.

# REF: https://index.ros.org/doc/ros2/Installation/Linux-Install-Debians/
# by Open Robotics, licensed under CC-BY-4.0
# source: https://github.com/ros2/ros2_documentation

ENV CHOOSE_ROS_DISTRO=foxy
ENV INSTALL_PACKAGE=desktop

RUN sudo apt-get update
RUN sudo apt-get install -y curl gnupg2 lsb-release
RUN sudo curl -sSL https://raw.githubusercontent.com/ros/rosdistro/master/ros.key -o /usr/share/keyrings/ros-archive-keyring.gpg
RUN echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/ros-archive-keyring.gpg] http://packages.ros.org/ros2/ubuntu $(lsb_release -cs) main" | sudo tee /etc/apt/sources.list.d/ros2.list > /dev/null
RUN sudo apt-get update
RUN sudo apt-get install -y ros-${CHOOSE_ROS_DISTRO}-${INSTALL_PACKAGE}
RUN sudo apt-get install -y python3-argcomplete
RUN sudo apt-get install -y python3-colcon-common-extensions
RUN sudo apt-get install -y python3-rosdep python3-vcstool # https://index.ros.org/doc/ros2/Installation/Linux-Development-Setup/
RUN sudo rosdep init
RUN rosdep update
RUN sudo apt-get install -y ros-${CHOOSE_ROS_DISTRO}-gazebo-ros-pkgs
RUN grep -F "source /opt/ros/${CHOOSE_ROS_DISTRO}/setup.bash" ~/.bashrc ||
RUN echo "source /opt/ros/${CHOOSE_ROS_DISTRO}/setup.bash" >> ~/.bashrc

RUN set +u

RUN source /opt/ros/${CHOOSE_ROS_DISTRO}/setup.bash

RUN echo "success installing ROS2 ${CHOOSE_ROS_DISTRO}"
RUN echo "Run 'source /opt/ros/${CHOOSE_ROS_DISTRO}/setup.bash'"
RUN sudo rm -rf /var/lib/apt/lists/*
#RUN mv $GITPOD_HOME /home/gitpod_moved
ENV USER $GITPOD_USER
