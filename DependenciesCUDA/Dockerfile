FROM project8/p8compute_dependencies:v0.9.0

# CUDA Dockerfile contents from https://gitlab.com/nvidia/container-images/cuda/-/tree/master/dist/11.1/centos7-x86_64
# As of 10/23/2020, version 11.1 is the latest distribution

#
# base
#

RUN NVIDIA_GPGKEY_SUM=d1be581509378368edeec8c1eb2958702feedf3bc3d17011adbf24efacce4ab5 && \
    curl -fsSL https://developer.download.nvidia.com/compute/cuda/repos/rhel7/x86_64/7fa2af80.pub | sed '/^Version/d' > /etc/pki/rpm-gpg/RPM-GPG-KEY-NVIDIA && \
    echo "$NVIDIA_GPGKEY_SUM  /etc/pki/rpm-gpg/RPM-GPG-KEY-NVIDIA" | sha256sum -c --strict  -

COPY cuda.repo /etc/yum.repos.d/cuda.repo
COPY nvidia-ml.repo /etc/yum.repos.d/nvidia-ml.repo

ENV CUDA_VERSION 11.1.0
ENV NCCL_VERSION 2.7.8

# For libraries in the cuda-compat-* package: https://docs.nvidia.com/cuda/eula/index.html#attachment-a
RUN yum upgrade -y && yum install -y \
    cuda-compat-11-1 \
    cuda-nvtx-11-1-11.1.74-1 \
    libnpp-11-1-11.1.1.269-1 \
    libnccl-2.7.8-1+cuda11.1 \
    cuda-nvml-devel-11-1-11.1.74-1 \
    cuda-command-line-tools-11-1-11.1.0-1 \
    libcublas-devel-11-1-11.2.1.74-1 \
    cuda-cudart-devel-11-1-11.1.74-1 \
    cuda-libraries-devel-11-1-11.1.0-1 \
    cuda-minimal-build-11-1-11.1.0-1 \
    cuda-nvprof-11-1-11.1.69-1 \
    libnpp-devel-11-1-11.1.1.269-1 \
    libnccl-devel-2.7.8-1+cuda11.1 \
    && ln -s cuda-11.1 /usr/local/cuda \
    && yum clean all \
    && rm -rf /var/cache/yum/*

# nvidia-docker 1.0
RUN echo "/usr/local/nvidia/lib" >> /etc/ld.so.conf.d/nvidia.conf && \
    echo "/usr/local/nvidia/lib64" >> /etc/ld.so.conf.d/nvidia.conf

ENV PATH /usr/local/nvidia/bin:/usr/local/cuda/bin:${PATH}
ENV LD_LIBRARY_PATH /usr/local/nvidia/lib:/usr/local/nvidia/lib64

# nvidia-container-runtime
ENV NVIDIA_VISIBLE_DEVICES all
ENV NVIDIA_DRIVER_CAPABILITIES compute,utility
ENV NVIDIA_REQUIRE_CUDA "cuda>=11.1 brand=tesla,driver>=418,driver<419 brand=tesla,driver>=440,driver<441 brand=tesla,driver>=450,driver<451"

ENV LIBRARY_PATH /usr/local/cuda/lib64/stubs

#
# runtime
#

#ENV NCCL_VERSION 2.7.8

#RUN yum install -y \
#    cuda-libraries-11-1-11.1.0-1 \
#    cuda-nvtx-11-1-11.1.74-1 \
#    libnpp-11-1-11.1.1.269-1 \
#    libcublas-11-1-11.2.1.74-1 \
#    libnccl-2.7.8-1+cuda11.1 \
#    && yum clean all \
#    && rm -rf /var/cache/yum/*


#
# devel
#

#ENV NCCL_VERSION 2.7.8

#RUN yum install -y \
#    make \
#    cuda-nvml-devel-11-1-11.1.74-1 \
#    cuda-command-line-tools-11-1-11.1.0-1 \
#    libcublas-devel-11-1-11.2.1.74-1 \
#    cuda-cudart-devel-11-1-11.1.74-1 \
#    cuda-libraries-devel-11-1-11.1.0-1 \
#    cuda-minimal-build-11-1-11.1.0-1 \
#    cuda-nvprof-11-1-11.1.69-1 \
#    libnpp-devel-11-1-11.1.1.269-1 \
#    libnccl-devel-2.7.8-1+cuda11.1 \
#    && yum clean all \
#    && rm -rf /var/cache/yum/*

#ENV LIBRARY_PATH /usr/local/cuda/lib64/stubs
