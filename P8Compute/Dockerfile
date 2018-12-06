FROM project8/p8compute_dependencies:v0.3.0_dev

ENV P8COMPUTE_TAG=v0.3.0_dev
ENV P8COMPUTE_BUILD_PREFIX=/usr/local/p8/compute/$P8COMPUTE_TAG

# Locust
ARG locust_tag=v1.8.3_dev
COPY --from=project8/locust_mc:v1.8.3_dev /usr/local/p8/locust/$locust_tag /usr/local/p8/locust/$locust_tag

# Katydid
ARG katydid_tag=v2.15.1_dev
COPY --from=project8/katydid:v2.15.1_dev /usr/local/p8/katydid/$katydid_tag /usr/local/p8/katydid/$katydid_tag

# Mermithid
ARG mermithid_tag=v1.1.4_dev
COPY --from=project8/mermithid:v1.1.4_dev /usr/local/p8/mermithid/$mermithid_tag /usr/local/p8/mermithid/$mermithid_tag

# P8Compute directory and setup script
# Fake CVMFS directory to match previous directory structure
ENV CVMFS_PATH=/cvmfs/hep.pnnl.gov/project8
RUN mkdir -p $P8COMPUTE_BUILD_PREFIX &&\
    cd $P8COMPUTE_BUILD_PREFIX &&\
    echo 'ln -sf $P8COMPUTE_BUILD_PREFIX $P8COMPUTE_BUILD_PREFIX/../current || /bin/true' > setup.sh &&\
    echo "source /usr/local/p8/locust/${locust_tag}/setup.sh" >> setup.sh &&\ 
    echo "source /usr/local/p8/katydid/${katydid_tag}/setup.sh" >> setup.sh &&\ 
    echo "source /usr/local/p8/mermithid/${mermithid_tag}/setup.sh" >> setup.sh &&\
    echo "source /usr/local/p8/mermithid/${mermithid_tag}/bin/this_cicada.sh" >> setup.sh &&\
    echo "source /usr/local/p8/mermithid/${mermithid_tag}/bin/this_phylloxera.sh" >> setup.sh &&\
    mkdir -p /cvmfs/hep.pnnl.gov &&\
    ln -sf /usr/local/p8 $CVMFS_PATH &&\
    /bin/true
