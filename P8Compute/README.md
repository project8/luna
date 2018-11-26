# P8Compute

## Containers

* `project8/p8compute` -- This container includes Project 8 analysis and simulation resources (Katydid and Locust), Python3, and ROOT6.  It can be used to run any of that software, and is the container used to run official analysis and simulation jobs on Project 8 computing resources.

* `project8/p8compute-jupyter` -- This container will run a Jupyter notebook. It is built on top of `p8compute`, so it contains all of the same python and Project 8 resources, in addition to Scipy and Matplotlib.

In the sections below referring to tags for the containers, you can find the tag names on the Docker Hub pages for [p8compute](https://hub.docker.com/r/project8/p8compute/tags) and [p8compute-jupyter](https://hub.docker.com/r/project8/p8compute-jupyter/tags).

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

##  Running the Jupyter Notebook Server

To run the server:
```
host> docker run --rm -p 8888:8888 project8/p8compute-jupyter:[tag]
```

To run the server and mount a directory on the host into the container:
```
host> docker run -p 8888:8888 -v /host/path/to/data:/p8compute/path/to/data project8/p8compute-jupyter:[tag]
```

To open the notebook:

1. Once the Jupyter server starts, it should present you with a URL to paste into your browser.  Copy that URL.
1. Paste it into your browser and press enter.  It should look something like this:

    ```
    http://localhost:8888/?token=[hash string]
    ```
