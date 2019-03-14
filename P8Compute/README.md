# P8Compute

## Container

`project8/p8compute` -- This container includes Project 8 analysis and simulation resources (Katydid and Locust), Python3, and ROOT6.  It can be used to run any of that software, and is the container used to run official analysis and simulation jobs on Project 8 computing resources.

In the sections below referring to tags for the containers, you can find the tag names on the Docker Hub page for [p8compute](https://hub.docker.com/r/project8/p8compute/tags).

## Accessing the `p8compute` Container

To access the container:
```
host> docker run --rm -it project8/p8compute:[tag] /bin/bash
```

To access the container and mount a directory on the host into the container:
```
host> docker run --rm -v /host/path/to/data:/p8compute/path/to/data -it project8/p8compute:[tag] /bin/bash
```

Once in the container, setup the environment by:
```
container> source $P8COMPUTE_BUILD_PREFIX/setup.sh
```
You may test it by running the commands `Katydid`, `LocustSim`, `python`, etc.
