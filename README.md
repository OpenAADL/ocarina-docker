# ocarina-docker

## About

Ocarina docker images, based on various Linux images: CentOS, debian,
Fedora and Ubuntu.

These docker files fetch all dependencies to compile Ocarina, along
with the `build_ocarina.sh` build script.

The following images are provided, with the following variant

| Name                           | Distribution     | GNAT                |
| ------------------------------ |:----------------:| -------------------:|
| alpine                         | Alpine           | default GCC         |
| centos-7.x-gnat-gpl-2016       | CentOS 7         | GNAT GPL 2016       |
| centos-7.x-gnat-gpl-2017       | CentOS 7         | GNAT GPL 2017       |
| centos-7.x-gnat-community-2018 | CentOS 7         | GNAT Community 2018 |
| debian-9.0                     | Debian 9 stable  | default GCC         |
| debian-10.0                    | Debian 10 stable | default GCC         |
| debian-testing                 | Debian teting    | default GCC         |
| fedora-32                      | Fedora 32        | default GCC         |
| fedora-Rawhide                 | Fedora Rawhide   | default GCC         |
| Ubuntu-Xenial                  | Ubuntu Xenial    | PPA/GCC6            |
| Ubuntu-Artful                  | Ubuntu Artful    | default GCC         |
| ubuntu-20.04                   | Ubuntu 20.04 LTS | default GCC         |

Note: CentOS builds rely on GNAT GPL or Community releases,
Ubuntu-Xenial uses PPA/GCC to use a more recent GCC version. All other
builds rely on the default GCC provided by the Linux distribution.

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

## Running Ocarina from a docker container

The `debian-10.0` dockerfile has been adapted so that you can run
ocarina from the docker container.

Let us suppose you have some AADL files in the common directory, you
can then run

```
docker run -ti  -v `pwd`:/work  ocarina/ocarina ocarina [ocarina arguments]
```
