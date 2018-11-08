# P8Compute

## Running the Jupyter Notebook Server

The `project8/p8compute-jupyter` container will run a Jupyter notebook that has access to Project 8 python resources.

To run the server:

```
host> docker run -p 8888:8888 project8/p8compute-jupyter:[tag]
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
    