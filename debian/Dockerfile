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
#    docker run -t -i ocarina/build bash
#
###############################################################################

###############################################################################
# Baseline: debian/testing
#
# Note: as of October 2016, we have to baseline on debian testing to
# have GCC/GNAT 6

FROM debian:testing
MAINTAINER Jerome Hugues <hugues.jerome@gmail.com>

RUN apt-get update && apt-get install -y autoconf automake gnat-6 \
    build-essential git python python-dev

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
