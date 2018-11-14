# P8Compute

## Accessing the Container & Running the Jupyter Notebook Server

The `project8/p8compute-jupyter` container includes root, python, Katydid and Locust packages. The `project8/p8compute-jupyter` container will run a Jupyter notebook that has access to Project 8 python resources. Choose accordingly to your needs.

To access the container:
```
host> docker run --rm -it project8/p8compute:[tag] /bin/bash
```
or to run the jupyter server:
```
host> docker run --rm -p 8888:8888 project8/p8compute-jupyter:[tag]
```
To access the container and mount a directory on the host into the container:
```
host> docker run --rm -v /host/path/to/data:/p8compute/path/to/data -it project8/p8compute:[tag] /bin/bash
```
To run the server and mount a directory on the host into the container:
```
host> docker run -p 8888:8888 -v /host/path/to/data:/p8compute/path/to/data project8/p8compute-jupyter:[tag]
```
The tags may be found on the project8/p8compute dockerhub page: https://hub.docker.com/r/project8/p8compute/.



Once in the container, setup the environment by:
```
container> source $P8COMPUTE_BUILD_PREFIX/setup.sh
```
You may test it by running the commands `Katydid`, `LocustSim`, `python`, etc.

To open the notebook:

1. Once the Jupyter server starts, it should present you with a URL to paste into your browser.  Copy that URL.
1. Paste it into your browser and press enter.  It should look something like this:

    ```
    http://localhost:8888/?token=[hash string]
    ```
