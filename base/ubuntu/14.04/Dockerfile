FROM ubuntu:14.04.3

MAINTAINER Florian Dehn <flo@katzefudder.de>

LABEL Description="Ubuntu 14.04 Trusty Tahr" Vendor="katzefudder.de"

# # # # # # # # # # # # # # # # # # #  set timezone to Europe/Berlin
RUN ln -sf /usr/share/zoneinfo/Europe/Berlin /etc/localtime

# # # # # # # # # # # # # # # # # # # unattended installation of packages
RUN export DEBIAN_FRONTEND=noninteractive

# # # # # # # # # # # # # # # # # # # Customize sources for apt-get
RUN  echo "deb http://archive.ubuntu.com/ubuntu trusty main universe\n" > /etc/apt/sources.list \
  && echo "deb http://archive.ubuntu.com/ubuntu trusty-updates main universe\n" >> /etc/apt/sources.list

# # # # # # # # # # # # # # # # # # # Install basic packages
RUN apt-get update && apt-get -y install apt-utils ca-certificates unzip tmux build-essential \
lynx-cur supervisor git vim inetutils-ping sudo telnet curl wget sudo

# # # # # # # # # # # # # # # # # # # Add user with passwordless sudo
RUN sudo useradd flo --shell /bin/bash --create-home \
  && sudo usermod -a -G sudo flo \
  && echo 'ALL ALL = (ALL) NOPASSWD: ALL' >> /etc/sudoers \
  && echo 'flo:a12sdf' | chpasswd

# # # # # # # # # # # # # # # # # # # Root password set to a12sdf
RUN echo 'root:a12sdf' | chpasswd

# # # # # # # # # # # # # # # # # # # do not verify SSL
RUN git config --global http.sslVerify false

# # # # # # # # # # # # # # # # # # # set the environment for later reference
RUN echo "ENVIRONMENT=docker" >> /etc/environment

# # # # # # # # # # # # # # # # # # # create directory for supervisor log dir
RUN mkdir -p /var/log/supervisor/