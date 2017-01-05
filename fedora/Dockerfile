###############################################################################
# Ocarina docker image, based on a fedora image
#
# This docker file fetches all dependencies to compile Ocarina, along
# with the build_ocarina.sh build script
#
# To build the image:
#    docker build -t ocarina/build .
#
# To run the image:
#    docker run -t -i ocarina/build bash
#
###############################################################################

###############################################################################
# Baseline: fedora/rawhide
#
# Note: we cannot use Fedora 25 as default GCC (GCC 6.2) causes an ICE
# when building Ocarina

FROM fedora:rawhide
MAINTAINER Jerome Hugues <hugues.jerome@gmail.com>

RUN dnf -y update && \
    dnf clean all && \
    dnf -y install autoconf automake gcc-gnat git make findutils

###############################################################################
# Install default "ocarina" user

RUN useradd -m -c "ocarina" -s /bin/bash ocarina
VOLUME /work

# Set up account and fetch fresh copy of ocarina-build repository

USER ocarina
ENV PATH /usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
ENV LANG en_US
ENV LC_ALL en_US.UTF-8

RUN cd $HOME && git clone https://github.com/OpenAADL/ocarina-build.git
WORKDIR /home/ocarina

# Default command: run the fresh-install scenario to build Ocarina in
# the container

CMD cd $HOME/ocarina-build && \
    ./build_ocarina.sh --self-update && \
    ./build_ocarina.sh --scenario=fresh-install --prefix=$HOME/local
