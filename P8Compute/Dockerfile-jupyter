FROM project8/p8compute:v0.4.0

RUN source $P8COMPUTE_BUILD_PREFIX/setup.sh &&\
    pip3 install --upgrade pip &&\
    pip3 install \
    	'scipy' \
    	'matplotlib' \
    	'jupyter' &&\
    /bin/true

EXPOSE 8888

CMD source $P8COMPUTE_BUILD_PREFIX/setup.sh &&\
    jupyter notebook --no-browser --allow-root --ip=0.0.0.0
