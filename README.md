 Ocarina docker image, based on various linux images: debian and fedora

 These docker files fetch all dependencies to compile Ocarina, along
 with the `build_ocarina.sh` build script

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
