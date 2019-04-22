FROM project8/p8compute_dependencies:v0.5.0

ENV P8COMPUTE_TAG=v0.5.0
ENV P8COMPUTE_BUILD_PREFIX=/usr/local/p8/compute/$P8COMPUTE_TAG

# Locust
ARG locust_tag=v1.11.0
COPY --from=project8/locust_mc:v1.11.0 /usr/local/p8/locust/$locust_tag /usr/local/p8/locust/$locust_tag

# Katydid
ARG katydid_tag=v2.15.3
COPY --from=project8/katydid:v2.15.3 /usr/local/p8/katydid/$katydid_tag /usr/local/p8/katydid/$katydid_tag

# Mermithid
ARG mermithid_tag=v1.1.8
COPY --from=project8/mermithid:v1.1.8 /usr/local/p8/mermithid/$mermithid_tag /usr/local/p8/mermithid/$mermithid_tag

# P8Compute directory and setup script
# Fake CVMFS directory to match previous directory structure
ENV CVMFS_PATH=/cvmfs/hep.pnnl.gov/project8
RUN mkdir -p $P8COMPUTE_BUILD_PREFIX &&\
    chmod -R 777 $P8COMPUTE_BUILD_PREFIX/.. &&\
    cd $P8COMPUTE_BUILD_PREFIX &&\
    echo 'ln -sfT $P8COMPUTE_BUILD_PREFIX $P8COMPUTE_BUILD_PREFIX/../current' > setup.sh &&\
    echo "source /usr/local/p8/locust/${locust_tag}/setup.sh" >> setup.sh &&\ 
    echo "source /usr/local/p8/katydid/${katydid_tag}/setup.sh" >> setup.sh &&\ 
    echo "source /usr/local/p8/mermithid/${mermithid_tag}/setup.sh" >> setup.sh &&\
    echo "source /usr/local/p8/mermithid/${mermithid_tag}/bin/this_cicada.sh" >> setup.sh &&\
    echo "source /usr/local/p8/mermithid/${mermithid_tag}/bin/this_phylloxera.sh" >> setup.sh &&\
    mkdir -p /cvmfs/hep.pnnl.gov &&\
    ln -sf /usr/local/p8 $CVMFS_PATH &&\
    chmod 777 /usr/local/p8/locust /usr/local/p8/katydid /usr/local/p8/mermithid \
              /usr/local/p8/locust/$locust_tag /usr/local/p8/katydid/$katydid_tag /usr/local/p8/mermithid/$mermithid_tag &&\
    /bin/true


##############
# Old Versions
##############

# P8Compute v0.1.9 provides Katydid v2.14.0 and Locust v1.8.0
COPY --from=project8/p8compute:v0.1.9 /usr/local/p8/locust/v1.8.0 /usr/local/p8/locust/v1.8.0
COPY --from=project8/p8compute:v0.1.9 /usr/local/p8/katydid/v2.14.0 /usr/local/p8/katydid/v2.14.0
COPY --from=project8/p8compute:v0.1.9 /usr/local/p8/compute/v0.1.9 /usr/local/p8/compute/v0.1.9
# p8compute_dependencies:v0.2.0 (used in p8compute:v0.1.9) is essentially the same as v0.4.0, so use a symlink
RUN ln -s /usr/local/p8/common/v0.4.0 /usr/local/p8/common/v0.2.0 &&\
    chmod 777 /usr/local/p8/locust/v1.8.0 /usr/local/p8/katydid/v2.14.0 /usr/local/p8/compute/v0.1.9 &&\
    /bin/true
