# ocarina-docker

## About

Ocarina docker images, based on various linux images: debian and fedora

These docker files fetch all dependencies to compile Ocarina, along
with the `build_ocarina.sh` build script

The following images are provided, with the following variant

- debian: currently uses testing to have access to GCC 6.x

- fedora: use rawhide, but both F25 and rawhide GCC 6.x cause an ICE
  when compiling Ocarina

- centos: even with CentOS 7, uses GNAT GPL 2016

## Usage

* To build the image, from one of the directory:
```
    docker build -t ocarina/build .
```

* To run the image:
```
   docker run -t -i ocarina/build bash
```

or

```
   docker run -t ocarina/build
```

to run the default scenario: perform a fresh install of Ocarina
