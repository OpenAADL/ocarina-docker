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
| debian-9.0               | Debian 9 stable | debian GCC    |
| debian-testing           | Debian teting   | debian GCC    |
| fedora-26                | Fedora 26       | Fedora GCC    |
| fedora-Rawhide           | Fedora Rawhide       | Fedora GCC    |

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
