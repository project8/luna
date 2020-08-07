FROM project8/p8compute:v0.10.0

# The purpose of this container is to comment out the symlink creation in the setup.sh scripts
# For now these versions are hard-coded here, but we really should find a better way to do it.
RUN sed -i -e 's/ln -s/#ln -s/' /usr/local/p8/common/v0.9.0/setup.sh &&\
    sed -i -e 's/ln -s/#ln -s/' /usr/local/p8/katydid/v2.17.2/setup.sh &&\
    sed -i -e 's/ln -s/#ln -s/' /usr/local/p8/locust/v2.0.0/setup.sh &&\
    sed -i -e 's/ln -s/#ln -s/' /usr/local/p8/mermithid/v1.2.2/setup.sh &&\
    sed -i -e 's/ln -s/#ln -s/' /usr/local/p8/psyllid/v1.12.2/setup.sh &&\
    sed -i -e 's/ln -s/#ln -s/' /usr/local/p8/compute/v0.10.0/setup.sh &&\
    sed -i -e 's/ln -s/#ln -s/' /usr/local/p8/common/v0.4.0/setup.sh &&\
    sed -i -e 's/ln -s/#ln -s/' /usr/local/p8/katydid/v2.15.3/setup.sh &&\
    sed -i -e 's/ln -s/#ln -s/' /usr/local/p8/locust/v1.11.0/setup.sh &&\
    sed -i -e 's/ln -s/#ln -s/' /usr/local/p8/mermithid/v1.1.8/setup.sh &&\
    sed -i -e 's/ln -s/#ln -s/' /usr/local/p8/compute/v0.5.0/setup.sh &&\
    /bin/true
