# P8Compute

## Container

`project8/p8compute-dirac` -- This container includes the Project 8 analysis and simulation software stack with modified `setup.sh` scripts: because of the way singularity is setup on our main computing resource, the creation of the `current` symlinks is skipped.

Please note that the way this container is setup is a terrible hack that has allowed us to get the container running without rebuilding all of the containers.  The `setup.sh` scripts should be fixed properly to optionally create the symlinks.

In the sections below referring to tags for the containers, you can find the tag names on the Docker Hub page for [p8compute](https://hub.docker.com/r/project8/p8compute-dirac/tags).

## Accessing the `p8compute-dirac` Container

To access the container:
```
host> docker run --rm -it project8/p8compute-dirac:[tag] /bin/bash
```

To access the container and mount a directory on the host into the container:
```
host> docker run --rm -v /host/path/to/data:/p8compute/path/to/data -it project8/p8compute-dirac:[tag] /bin/bash
```

Once in the container, setup the environment by:
```
container> source $P8COMPUTE_BUILD_PREFIX/setup.sh
```
You may test it by running the commands `Katydid`, `LocustSim`, `python`, etc.
