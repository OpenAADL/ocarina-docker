 Ocarina docker image, based on various linux images: debian and fedora

 These docker files fetch all dependencies to compile Ocarina, along
 with the `build_ocarina.sh` build script

* To build the image:
```
    docker build -t ocarina/build .
```

* To run the image:
```
   docker run -t -i ocarina/build bash
```

