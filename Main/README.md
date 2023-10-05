# Luna/Main

## Container

`project8/luna` -- This container includes Project 8 analysis and simulation resources (Katydid, Mermithid, and Locust), Python3, and ROOT6.  It can be used to run any of that software, and is the container used to run official analysis and simulation jobs on Project 8 computing resources.

In the sections below referring to tags for the containers, you can find the tag names on the GitHub Container Registry page for [Luna](https://github.com/project8/luna/pkgs/container/luna).

## Accessing the `luna` Container

To access the container:
```
host> docker run --rm -it ghcr.io/project8/luna:[tag] /bin/bash
```

To access the container and mount a directory on the host into the container:
```
host> docker run --rm -v /host/path/to/data:/data -it ghcr.io/project8/luna:[tag] /bin/bash
```

Once in the container, setup the environment by:
```
container> source $P8COMPUTE_BUILD_PREFIX/setup.sh
```
You may test it by running the commands `Katydid`, `LocustSim`, `python3`, etc.
