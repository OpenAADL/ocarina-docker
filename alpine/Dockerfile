###############################################################################
# Ocarina docker image, based on an Alpine image
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
# Baseline: alpine latest
#

FROM alpine:edge
MAINTAINER Jerome Hugues <hugues.jerome@gmail.com>

RUN echo 'http://dl-cdn.alpinelinux.org/alpine/edge/testing' >> /etc/apk/repositories; \
    echo 'http://dl-cdn.alpinelinux.org/alpine/edge/community' >> /etc/apk/repositories; \
    echo 'http://dl-cdn.alpinelinux.org/alpine/edge/main' >> /etc/apk/repositories;

RUN apk -U upgrade && \
    apk add --no-cache gcc musl-dev gcc-gnat git autoconf automake sudo procps bash ncurses python2 gprbuild make

# Note on installed packages
# * git + wget + ca-certificates             : fetch source from repositories
# * autoconf automake gnat-6 build-essential : compilation chain
# * python python-dev                        : testsuite
# * sudo
# * procps                                   : ps, kill, etc.

###############################################################################
# Install default "ocarina" user

VOLUME /work

ENV TERM xterm
ENV PATH /usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
ENV LANG C.UTF-8

# Install ocarina-build

RUN cd /root && git clone https://github.com/OpenAADL/ocarina-build.git

# Install Ocarina in default directory

RUN cd /root/ocarina-build/ && ls && \
    ./build_ocarina.sh --self-update && \
    ./build_ocarina.sh --scenario=fresh-install --prefix=/usr/

WORKDIR /work