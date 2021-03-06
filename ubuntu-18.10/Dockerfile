###############################################################################
# Ocarina docker image, based on an Ubuntu image
#
# This docker file fetches all dependencies to compile Ocarina, along
# with the build_ocarina.sh build script
#
# To build the image:
#    docker build -t ocarina/build .
#
# To run the image:
#    docker run -t -i -v $PWD/data/:/work ocarina/build bash
#
###############################################################################

###############################################################################
# Baseline: Ubuntu/Cosmic 18.10

FROM ubuntu:cosmic
MAINTAINER Jerome Hugues <hugues.jerome@gmail.com>

RUN apt-get update && \
    apt-get install -y --no-install-recommends \
            git wget ca-certificates \
            autoconf automake gnat build-essential \
            python python-dev \
            checkinstall sudo procps emacs

# Note on installed packages
# * git + wget + ca-certificates             : fetch source from repositories
# * autoconf automake gnat-6 build-essential : compilation chain
# * python python-dev                        : testsuite
# * checkinstall sudo                        : automatically build .deb
# * procps                                   : ps, kill, etc.

###############################################################################
# Install default "ocarina" user
# Add Ocarina user to sudoers for building .deb

RUN useradd -m -c "ocarina" -s /bin/bash ocarina && echo "ocarina:ocarina" | chpasswd
RUN adduser ocarina sudo

VOLUME /work

# Set up account and fetch fresh copy of ocarina-build repository

USER ocarina
ENV PATH /usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
ENV LANG en_US
ENV LC_ALL en_US.UTF-8

# Install

RUN cd $HOME && git clone https://github.com/OpenAADL/ocarina-build.git
WORKDIR /home/ocarina

# Default command: run the fresh-install scenario to build Ocarina in
# the container

CMD cd $HOME/ocarina-build && \
    ./build_ocarina.sh --self-update && \
    ./build_ocarina.sh --scenario=fresh-install --prefix=$HOME/local
