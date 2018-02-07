# ocarina-docker

## About

Ocarina docker images, based on various linux images: debian and fedora

These docker files fetch all dependencies to compile Ocarina, along
with the `build_ocarina.sh` build script.

The following images are provided, with the following variant

| Name                     | Distribution    | GNAT          |
| ------------------------ |:---------------:| -------------:|
| centos-7.x-gnat-gpl-2016 | CentOS 7        | GNAT GPL 2016 |
| centos-7.x-gnat-gpl-2017 | CentOS 7        | GNAT GPL 2017 |
| debian-9.0               | Debian 9 stable | default GCC   |
| debian-testing           | Debian teting   | default GCC   |
| fedora-26                | Fedora 26       | default GCC   |
| fedora-27                | Fedora 27       | default GCC   |
| fedora-rawhide           | Fedora Rawhide  | default GCC   |
| ubuntu-16.04             | Ubuntu Xenial   | PPA/GCC6      |
| ubuntu-17.10             | Ubuntu Artful   | default GCC   |

Note: CentOS builds rely on GNAT GPL releases, Ubuntu-Xenial uses
PPA/GCC to use a more recent GCC version. All other builds rely on the
default GCC provided by the Linux distribution.

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
