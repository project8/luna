FROM project8/p8compute_bare as gcc-base

# get gcc from package manager
RUN yum -y install centos-release-scl-rh &&\
    yum -y install \
        devtoolset-7-gcc-c++ \
        rh-python36-python-devel \
        zlib-devel \
        perl-devel \
        gettext-devel \
        libX11-devel \
        libXpm-devel \
        libXft-devel \
        libXext-devel \
        wget

ENV COMMON_TAG=v0.9.0
ENV COMMON_BUILD_PREFIX=/usr/local/p8/common/$COMMON_TAG

# Create the setup.sh script
# Includes a one-time-use-only guard to avoid repeatedly adding to these environment variables.
RUN mkdir -p $COMMON_BUILD_PREFIX &&\
    chmod -R 777 $COMMON_BUILD_PREFIX/.. &&\
    cd $COMMON_BUILD_PREFIX &&\
    echo "# This file is automatically generated by luna/Dependencies/Dockerfile." > setup.sh &&\
    echo '[ -n "$P8COMPUTE_COMMON_SETUP" ] && return || readonly P8COMPUTE_COMMON_SETUP=1' >> setup.sh &&\
    echo "source scl_source enable devtoolset-7" >> setup.sh &&\
    echo "source scl_source enable rh-python36" >> setup.sh &&\
    echo "unset PYTHONPATH" >> setup.sh &&\
    echo "export COMMON_TAG=$COMMON_TAG" >> setup.sh &&\
    echo "export COMMON_BUILD_PREFIX=$COMMON_BUILD_PREFIX" >> setup.sh &&\
    echo 'ln -sfT $COMMON_BUILD_PREFIX $COMMON_BUILD_PREFIX/../current' >> setup.sh &&\
    echo 'export PATH=$COMMON_BUILD_PREFIX/bin:$PATH' >> setup.sh &&\
    echo 'export LD_LIBRARY_PATH=$COMMON_BUILD_PREFIX/lib:$LD_LIBRARY_PATH' >> setup.sh &&\
    /bin/true

RUN source scl_source enable devtoolset-7 &&\
    source scl_source enable rh-python36 &&\
    unset PYTHONPATH &&\
    pip3 install --upgrade pip==18.1 &&\
    pip3 -v install \
        'PyYAML==3.13' \
        'pyparsing==2.1.5' \
        'dnspython==1.12.0' \
        'cycler==0.10.0' \
        'python-dateutil==2.7.2' \
        'pystan==2.17.1.0' \
        'numpy>=1.14' \
        'uproot==2.8.16' \
        'lz4' \
        'pbr==0.10.8' \
        'six' \
        'colorlog' \
        'h5py' \
        'matplotlib' \
        'scipy==1.3.0' \
        &&\
    /bin/true

##########################
FROM gcc-base as common

RUN mkdir -p /tmp_install

##########################
FROM common as cmake_done

## cmake (install manually because the version in yum is too old, v2.8.12)
RUN source $COMMON_BUILD_PREFIX/setup.sh &&\
    cd /tmp_install &&\
    wget https://github.com/Kitware/CMake/releases/download/v3.15.0/cmake-3.15.0.tar.gz &&\
    tar -xvzf cmake-3.15.0.tar.gz &&\
    cd cmake-3.15.0 &&\
    ./configure --prefix=$COMMON_BUILD_PREFIX &&\
    make -j3 install &&\
    /bin/true

##########################
FROM common as git_done

RUN yum install -y libcurl-devel

## git (install manually because the version in yum is too old)
RUN source $COMMON_BUILD_PREFIX/setup.sh &&\
    cd /tmp_install &&\
    wget https://github.com/git/git/archive/v2.22.0.tar.gz &&\
    tar -xvzf v2.22.0.tar.gz &&\
    cd git-2.22.0 &&\
    make configure &&\
    ./configure --prefix=$COMMON_BUILD_PREFIX &&\
    make -j3 install &&\
    /bin/true

##########################
FROM common as hdf5_done

## hdf5
RUN source $COMMON_BUILD_PREFIX/setup.sh &&\
    cd /tmp_install &&\
    wget https://support.hdfgroup.org/ftp/HDF5/releases/hdf5-1.10/hdf5-1.10.5/src/hdf5-1.10.5.tar.gz &&\
    tar -xvzf hdf5-1.10.5.tar.gz &&\
    cd hdf5-1.10.5 &&\
    ./configure --prefix=$COMMON_BUILD_PREFIX --enable-cxx --enable-shared --enable-unsupported --enable-threadsafe &&\
    make -j3 install &&\
    /bin/true

##########################
FROM common as fftw3_done

## fftw3
RUN source $COMMON_BUILD_PREFIX/setup.sh &&\
    cd /tmp_install &&\
    wget http://www.fftw.org/fftw-3.3.8.tar.gz &&\
    tar -xvzf fftw-3.3.8.tar.gz &&\
    cd fftw-3.3.8 &&\
    ./configure --prefix=$COMMON_BUILD_PREFIX --enable-shared --enable-threads --with-pic &&\
    make -j3 install &&\
    /bin/true

##########################
FROM common as matio_done

COPY --from=hdf5_done $COMMON_BUILD_PREFIX $COMMON_BUILD_PREFIX

## matio
RUN source $COMMON_BUILD_PREFIX/setup.sh &&\
    cd /tmp_install &&\
    wget https://github.com/tbeu/matio/releases/download/v1.5.17/matio-1.5.17.tar.gz &&\
    tar -xvzf matio-1.5.17.tar.gz &&\
    cd matio-1.5.17 &&\
    ./configure --prefix=$COMMON_BUILD_PREFIX --with-hdf5=$COMMON_BUILD_PREFIX --with-default-api-version=v110 &&\
    make -j3 install &&\
    /bin/true

##########################
FROM common as boost_done

## boost
RUN source $COMMON_BUILD_PREFIX/setup.sh &&\
    cd /tmp_install &&\
    wget https://dl.bintray.com/boostorg/release/1.70.0/source/boost_1_70_0.tar.gz &&\
    tar -xvzf boost_1_70_0.tar.gz &&\
    cd boost_1_70_0 &&\
    ./bootstrap.sh --prefix=$COMMON_BUILD_PREFIX --with-libraries=date_time,filesystem,program_options,system,thread,chrono &&\
    ./b2 &&\
    ./b2 install &&\
    /bin/true

##########################
FROM common as gsl_done

## gsl
RUN source $COMMON_BUILD_PREFIX/setup.sh &&\
    cd /tmp_install &&\
    wget http://mirrors.ibiblio.org/gnu/ftp/gnu/gsl/gsl-2.5.tar.gz &&\
    tar -xvzf gsl-2.5.tar.gz &&\
    cd gsl-2.5 &&\
    ./configure --prefix=$COMMON_BUILD_PREFIX &&\
    make -j3 all &&\ 
    make install &&\
    /bin/true

##########################
FROM common as root_done

COPY --from=cmake_done $COMMON_BUILD_PREFIX $COMMON_BUILD_PREFIX
COPY --from=hdf5_done $COMMON_BUILD_PREFIX $COMMON_BUILD_PREFIX
COPY --from=fftw3_done $COMMON_BUILD_PREFIX $COMMON_BUILD_PREFIX
COPY --from=gsl_done $COMMON_BUILD_PREFIX $COMMON_BUILD_PREFIX

## root
RUN source $COMMON_BUILD_PREFIX/setup.sh &&\
    cd /tmp_install &&\
    wget https://root.cern/download/root_v6.18.00.source.tar.gz &&\
    tar -xvzf root_v6.18.00.source.tar.gz &&\
    cd root-6.18.00 &&\
    mkdir my_build &&\
    cd my_build &&\
    cmake -D CMAKE_INSTALL_PREFIX:PATH=$COMMON_BUILD_PREFIX \
            -D gnuinstall=ON -D roofit=ON .. &&\
    make -j3 install &&\
    /bin/true

##########################
FROM common as rabbitmq_done

COPY --from=cmake_done $COMMON_BUILD_PREFIX $COMMON_BUILD_PREFIX

## rabbitmq-c
RUN source $COMMON_BUILD_PREFIX/setup.sh &&\
    cd /tmp_install &&\
    wget https://github.com/alanxz/rabbitmq-c/archive/v0.9.0.tar.gz &&\
    tar -xvzf v0.9.0.tar.gz &&\
    mkdir rabbitmq-c-0.9.0/build &&\
    cd rabbitmq-c-0.9.0/build &&\
    cmake \
        -D CMAKE_INSTALL_PREFIX=$COMMON_BUILD_PREFIX \
        -D CMAKE_INSTALL_LIBDIR:PATH=lib \
        -D ENABLE_SSL_SUPPORT:BOOL=FALSE \
        .. &&\
    make -j3 install &&\
    /bin/true

########################
FROM gcc-base

COPY --from=common $COMMON_BUILD_PREFIX $COMMON_BUILD_PREFIX
COPY --from=cmake_done $COMMON_BUILD_PREFIX $COMMON_BUILD_PREFIX
COPY --from=git_done $COMMON_BUILD_PREFIX $COMMON_BUILD_PREFIX
COPY --from=hdf5_done $COMMON_BUILD_PREFIX $COMMON_BUILD_PREFIX
COPY --from=fftw3_done $COMMON_BUILD_PREFIX $COMMON_BUILD_PREFIX
COPY --from=matio_done $COMMON_BUILD_PREFIX $COMMON_BUILD_PREFIX
COPY --from=boost_done $COMMON_BUILD_PREFIX $COMMON_BUILD_PREFIX
COPY --from=root_done $COMMON_BUILD_PREFIX $COMMON_BUILD_PREFIX
COPY --from=gsl_done $COMMON_BUILD_PREFIX $COMMON_BUILD_PREFIX
COPY --from=rabbitmq_done $COMMON_BUILD_PREFIX $COMMON_BUILD_PREFIX

RUN cd $COMMON_BUILD_PREFIX &&\
    echo "source $COMMON_BUILD_PREFIX/bin/thisroot.sh" >> setup.sh &&\
    /bin/true
