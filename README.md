# Luna

This repo includes the Dockerfiles for the containerization of the Project 8 analysis & simulations software stack. Specifically, it includes:
* The `p8compute` container, which brings together the entire stack and is used for official analysis and simulations jobs
* The `p8compute-jupyter` container, which runs a jupyter server for end-user analysis
* The `p8compute-dirac` container, which is optimized for use as a Singularity container

Dockerfiles for individual software packages can be found in their respective repositories.  In principle those individual containers can be used independent of the `p8compute` container.

## P8Compute

Packages currently included:
* Katydid
* Locust_mc
* Mermithid
* Psyllid

## P8Compute Jupyter

## P8Compute DIRAC

