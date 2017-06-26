###############################################################################
# Ocarina docker image, based on a CentOS image
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
# Baseline: CentOS 7.x
#

FROM centos:7
MAINTAINER Jerome Hugues <hugues.jerome@gmail.com>

RUN yum install -y autoconf automake git make python wget glibc-devel \
    python python-devel

###############################################################################
# Install default "ocarina" user

RUN useradd -m -c "ocarina" -s /bin/bash ocarina
VOLUME /work

# Set up account and fetch fresh copy of ocarina-build repository

USER ocarina
ENV PATH /home/ocarina/gnat-gpl-2017-x86_64-linux-bin/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
ENV LANG en_US
ENV LC_ALL en_US.UTF-8

# Install GNAT GPL 2017

RUN cd $HOME && \
    wget -nv http://mirrors.cdn.adacore.com/art/591c6d80c7a447af2deed1d7 && \
    mv  591c6d80c7a447af2deed1d7 gnat-gpl-2017-x86_64-linux-bin.tar.gz && \
    tar zxf gnat-gpl-2017-x86_64-linux-bin.tar.gz

# Install GNATcoll 2017

RUN cd $HOME && git clone -b gpl-2017  https://github.com/AdaCore/gnatcoll.git

RUN cd $HOME/gnatcoll && ./configure --with-python --enable-shared --without-gtk --without-postgresql --without-sqlite --without-iconv --disable-projects --prefix=/home/ocarina/gnat-gpl-2017-x86_64-linux-bin && make && make install

RUN cd $HOME && git clone https://github.com/OpenAADL/ocarina-build.git
WORKDIR /home/ocarina

# Default command: run the fresh-install scenario to build Ocarina in
# the container

#CMD cd $HOME/ocarina-build && \
#    ./build_ocarina.sh --self-update && \
#    ./build_ocarina.sh --scenario=fresh-install --prefix=$HOME/local
