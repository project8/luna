FROM project8/p8compute_dependencies:v0.1.0

ENV P8COMPUTE_BUILD_PREFIX=/usr/local/p8/compute-0.1.0

# Locust
ARG locust_dir=locust-v1.8.0
COPY --from=project8/locust_mc:v1.8.0_test /usr/local/p8/$locust_dir /usr/local/p8/$locust_dir

# Katydid
ARG katydid_dir=katydid-v2.14.0
COPY --from=project8/katydid:v2.14.0 /usr/local/p8/$katydid_dir /usr/local/p8/$katydid_dir

RUN mkdir -p $P8COMPUTE_BUILD_PREFIX &&\
    cd $P8COMPUTE_BUILD_PREFIX &&\
    echo 'ln -sf $P8COMPUTE_BUILD_PREFIX $P8COMPUTE_BUILD_PREFIX/../compute' > setup.sh &&\
    echo "source /usr/local/p8/${locust_dir}/setup.sh" >> setup.sh &&\ 
    echo "source /usr/local/p8/${katydid_dir}/setup.sh" >> setup.sh &&\ 
    /bin/true
