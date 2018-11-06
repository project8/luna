FROM project8/p8compute_dependencies:v0.2.0

ENV P8COMPUTE_TAG=v0.2.0
ENV P8COMPUTE_BUILD_PREFIX=/usr/local/p8/compute/$P8COMPUTE_TAG

# Locust
ARG locust_tag=v1.8.0
COPY --from=project8/locust_mc:v1.8.0_test /usr/local/p8/locust/$locust_tag /usr/local/p8/locust/$locust_tag

# Katydid
ARG katydid_tag=v2.14.0
COPY --from=project8/katydid:v2.14.0 /usr/local/p8/katydid/$katydid_tag /usr/local/p8/katydid/$katydid_tag

RUN mkdir -p $P8COMPUTE_BUILD_PREFIX &&\
    cd $P8COMPUTE_BUILD_PREFIX &&\
    echo 'ln -sf $P8COMPUTE_BUILD_PREFIX $P8COMPUTE_BUILD_PREFIX/../current' > setup.sh &&\
    echo "source /usr/local/p8/locust/${locust_tag}/setup.sh" >> setup.sh &&\ 
    echo "source /usr/local/p8/katydid/${katydid_tag}/setup.sh" >> setup.sh &&\ 
    /bin/true
