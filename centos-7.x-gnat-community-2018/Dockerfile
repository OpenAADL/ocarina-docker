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
    python python-devel fontconfig libX11 which java-1.8.0-openjdk-devel

###############################################################################
# Install default "ocarina" user

RUN useradd -m -c "ocarina" -s /bin/bash ocarina
VOLUME /work

# Set up account and fetch fresh copy of ocarina-build repository

USER ocarina
ENV PATH /home/ocarina/gnat-community-2018-install/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
ENV LANG en_US
ENV LC_ALL en_US.UTF-8

# Install GNAT Community 2018

RUN cd $HOME && \
    wget http://mirrors.cdn.adacore.com/art/5b0d7bffa3f5d709751e3e04 -O gnat-community-2018 && \
    git clone https://github.com/AdaCore/gnat_community_install_script && \
    sh ./gnat_community_install_script/install_package.sh ./gnat-community-2018 $HOME/gnat-community-2018-install

RUN cd $HOME && git clone https://github.com/OpenAADL/ocarina-build.git
WORKDIR /home/ocarina

# Default command: run the fresh-install scenario to build Ocarina in
# the container

CMD cd $HOME/ocarina-build && \
    ./build_ocarina.sh --self-update && \
    ./build_ocarina.sh --scenario=fresh-install --prefix=$HOME/local
