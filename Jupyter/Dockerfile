ARG img_repo=ghcr.io/project8/luna
ARG img_tag=v1.0.0

FROM ${img_repo}:${img_tag}

RUN source $P8COMPUTE_BUILD_PREFIX/setup.sh &&\
    pip3 install --upgrade pip &&\
    pip3 install \
    	'jupyter' &&\
    /bin/true

EXPOSE 8888

CMD source $P8COMPUTE_BUILD_PREFIX/setup.sh &&\
    jupyter notebook --no-browser --allow-root --ip=0.0.0.0
