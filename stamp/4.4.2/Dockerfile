#################################################################
# Dockerfile
#
# Software:     STAMP
# Version:      4.4.2
# Description:  STAMP - Structural Alignment of Multiple Proteins
# Website:      http://www.compbio.dundee.ac.uk/downloads/stamp/
# Provides:     stamp collection tools
# Base Image:   ubuntu:16.04
# Build Cmd:    docker build -t biomadeira/stamp:4.4.2 .
# Push Cmd:     docker push biomadeira/stamp:4.4.2
# Pull Cmd:     docker pull biomadeira/stamp:4.4.2
# Run Cmd:      docker run --rm -it --entrypoint /bin/bash biomadeira/stamp:4.4.2
# Exit Cmd:     exit
#################################################################

# Base Image
FROM ubuntu:16.04
MAINTAINER Fábio Madeira "fabiomadeira@me.com"

################## BEGIN INSTALLATION ######################

# Install required packages
RUN apt-get update; apt-get -y install wget && \
    apt-get -y install make && \
    apt-get -y install csh && \
    apt-get -y install g++

# Cleaning...
RUN apt-get clean && apt-get purge && \
    rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/* /usr/share/doc/*

# Download and untar the Stamp archive
ENV VERSION "4.4.2"
ENV ARCH http://www.compbio.dundee.ac.uk/downloads/stamp/stamp.$VERSION.tar.gz
RUN mkdir -p ./stamp.$VERSION
RUN wget $ARCH -O ./stamp.$VERSION.tar.gz
RUN tar xvf ./stamp.$VERSION.tar.gz -C ./

# Install Stamp
WORKDIR ./stamp.$VERSION
RUN chmod +x ./BUILD
RUN ./BUILD linux

# Add Stamp to PATH ENV
ENV PATH /stamp.$VERSION/bin/linux:$PATH
WORKDIR /root

# Default command to execute at startup of the container
CMD []
