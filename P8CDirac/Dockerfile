FROM project8/p8compute:v0.4.0

# The purpose of this container is to bake in the symlinks created when running setup.sh
RUN source $P8COMPUTE_BUILD_PREFIX/setup.sh &&\
    env | grep -e PATH= -e PREFIX= -e TAG= -e ROOTSYS= | sed 's/^/export /' > /etc/profile.d/p8_env_setup.sh &&\
    /bin/true
