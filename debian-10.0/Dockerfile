###############################################################################
# Ocarina docker image, based on a debian image
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
# Baseline: debian/buster (debian 10.x release)
#

FROM debian:buster
MAINTAINER Jerome Hugues <hugues.jerome@gmail.com>

RUN apt-get update && \
    apt-get install -y --no-install-recommends \
            git wget ca-certificates \
            autoconf automake gnat gprbuild build-essential \
            python python-dev \
            sudo procps

# Note on installed packages
# * git + wget + ca-certificates             : fetch source from repositories
# * autoconf automake gnat-6 build-essential : compilation chain
# * python python-dev                        : testsuite
# * sudo
# * procps                                   : ps, kill, etc.

###############################################################################
# Install default "ocarina" user
# Add Ocarina user to sudoers for building .deb

RUN useradd -m -c "ocarina" -s /bin/bash ocarina && echo "ocarina:ocarina" | chpasswd
RUN adduser ocarina sudo

VOLUME /work

ENV TERM xterm
ENV PATH /usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
ENV LANG C.UTF-8

# Install ocarina-build

RUN cd $HOME && git clone https://github.com/OpenAADL/ocarina-build.git
WORKDIR /work

# Install Ocarina in default directory

RUN cd $HOME/ocarina-build && \
    ./build_ocarina.sh --self-update && \
    ./build_ocarina.sh --scenario=fresh-install --prefix=/usr/

USER ocarina
