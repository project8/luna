# Luna

This repo includes the Dockerfiles for the containerization of the Project 8 analysis & simulations software stack. Specifically, it includes:
* The `luna` container, which brings together the entire stack and is used for official analysis and simulations jobs
* The `luna-jupyter` container, which runs a jupyter server for end-user analysis
* ~~The `p8compute-dirac` container, which is optimized for use as a Singularity container~~ The singularity container has not been updated since the conversion from p8compute to luna.

Dockerfiles for individual software packages can be found in their respective repositories.  In principle those individual containers can be used independent of the `luna` container.

## Main Luna Container

Packages currently included:
* Katydid
* Locust_mc
* Mermithid

The container can be built to include multiple versions of the packages if, for example, a previous version of one package is still needed for analysis compatibility.

## Jupyter Container



