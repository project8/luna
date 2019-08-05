FROM project8/p8compute:v0.7.0

# The purpose of this container is to comment out the symlink creation in the setup.sh scripts
# For now these versions are hard-coded here, but we really should find a better way to do it.
RUN sed -i -e 's/ln -s/#ln -s/' /usr/local/p8/common/v0.7.0/setup.sh &&\
    sed -i -e 's/ln -s/#ln -s/' /usr/local/p8/katydid/v2.17.0/setup.sh &&\
    sed -i -e 's/ln -s/#ln -s/' /usr/local/p8/locust/v1.13.3/setup.sh &&\
    sed -i -e 's/ln -s/#ln -s/' /usr/local/p8/mermithid/v1.1.10/setup.sh &&\
    sed -i -e 's/ln -s/#ln -s/' /usr/local/p8/psyllid/v1.12.1/setup.sh &&\
    sed -i -e 's/ln -s/#ln -s/' /usr/local/p8/compute/v0.8.0/setup.sh &&\
    sed -i -e 's/ln -s/#ln -s/' /usr/local/p8/common/v0.4.0/setup.sh &&\
    sed -i -e 's/ln -s/#ln -s/' /usr/local/p8/katydid/v2.15.3/setup.sh &&\
    sed -i -e 's/ln -s/#ln -s/' /usr/local/p8/locust/v1.11.0/setup.sh &&\
    sed -i -e 's/ln -s/#ln -s/' /usr/local/p8/mermithid/v1.1.8/setup.sh &&\
    sed -i -e 's/ln -s/#ln -s/' /usr/local/p8/compute/v0.5.0/setup.sh &&\
    /bin/true
