#
# Floreant POS Dockerfile
#
# https://github.com/genome21/Floreantpos-1
#

# Pull base image.
FROM ubuntu:14.04

# Install.
RUN \
  sed -i 's/# \(.*multiverse$\)/\1/g' /etc/apt/sources.list && \
  apt-get update && \
  apt-get -y upgrade && \
  apt-get install -y build-essential && \
  apt-get install -y software-properties-common && \
  apt-get install -y byobu curl git htop man unzip vim wget && \
  rm -rf /var/lib/apt/lists/*

# Add files.
ADD root/.bashrc /root/.bashrc
ADD root/.gitconfig /root/.gitconfig
ADD root/.scripts /root/.scripts

# Set environment variables.
ENV HOME /root

# Define working directory.
WORKDIR /usr/Downloads

# Clone the git repo to the docker container
RUN git clone git@github.com:genome21/floreantpos-1.git

# Run Floreant POS
RUN ./start-server.sh
RUN ./floreantpos.bat