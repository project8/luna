FROM project8/p8compute:v0.4.0

# The purpose of this container is to comment out the symlink creation in the setup.sh scripts
# For now these versions are hard-coded here, but we really should find a better way to do it.
RUN sed -i -e 's/ln -s/#ln -s/' /usr/local/p8/common/v0.4.0/setup.sh &&\
    sed -i -e 's/ln -s/#ln -s/' /usr/local/p8/locust/v1.10.3/setup.sh &&\
    sed -i -e 's/ln -s/#ln -s/' /usr/local/p8/katydid/v2.15.2/setup.sh &&\
    sed -i -e 's/ln -s/#ln -s/' /usr/local/p8/mermithid/v1.1.5/setup.sh &&\
    sed -i -e 's/ln -s/#ln -s/' /usr/local/p8/compute/v0.4.0/setup.sh &&\
    sed -i -e 's/ln -s/#ln -s/' /usr/local/p8/locust/v1.8.0/setup.sh &&\
    sed -i -e 's/ln -s/#ln -s/' /usr/local/p8/katydid/v2.14.0/setup.sh &&\
    sed -i -e 's/ln -s/#ln -s/' /usr/local/p8/compute/v0.1.9/setup.sh &&\
    /bin/true

# More hacking: in Katydid 2.14 there's no this_katydid.sh script.  So I'm hard-coding one here.
RUN cd /usr/local/p8/katydid/v2.14.0/bin &&\
    echo 'export PYTHONPATH=/usr/local/p8/katydid/v2.14.0/lib/CicadaPy:$PYTHONPATH' > this_katydid.sh &&\
    echo 'export ROOT_INCLUDE_PATH=/usr/local/p8/katydid/v2.14.0/include/Katydid/Cicada:/usr/local/p8/katydid/v2.14.0/include/Katydid/Nymph/Scarab:$ROOT_INCLUDE_PATH' >> this_katydid.sh &&\
    echo 'export ROOT_INCLUDE_PATH=/usr/local/p8/katydid/v2.14.0/include/Katydid:/usr/local/p8/katydid/v2.14.0/include/Katydid/Cicada:/usr/local/p8/katydid/v2.14.0/include/Katydid/Nymph/Scarab:$ROOT_INCLUDE_PATH' >> this_katydid.sh &&\
	/bin/true
