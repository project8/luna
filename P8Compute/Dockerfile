ARG img_repo=project8/luna_base
ARG img_tag=v1.0.0

ARG katydid_repo=ghcr.io/project8/katydid
ARG katydid_tag=v2.18.0
ARG locust_repo=ghcr.io/project8/locust_mc
ARG locust_tag=v2.2.0
ARG mermithid_repo=ghcr.io/project8/mermithid
ARG mermithid_tag=v1.2.2
ARG psyllid_tag=ghcr.io/project8/psyllid
ARG psyllid_tag=v1.12.2

# Katydid
FROM ${katydid_repo}:${katydid_tag} AS katydid

# Locust
FROM ${locust_repo}:${locust_tag} AS locust

# Mermithid
FROM ${mermithid_repo}:${mermithid_tag} AS mermithid

# Psyllid
FROM ${psyllid_repo}:${psyllid_tag} AS psyllid

FROM ${img_repo}:${img_tag}

ARG p8compute_tag=beta
ENV P8COMPUTE_TAG=${p8compute_tag}
ENV P8COMPUTE_BUILD_PREFIX=/usr/local/p8/compute/$P8COMPUTE_TAG

COPY --from=katydid /usr/local/p8/katydid/$katydid_tag /usr/local/p8/katydid/$katydid_tag
COPY --from=locust /usr/local/p8/locust/$locust_tag /usr/local/p8/locust/$locust_tag
COPY --from=mermithid /usr/local/p8/mermithid/$mermithid_tag /usr/local/p8/mermithid/$mermithid_tag
COPY --from=psyllid /usr/local/p8/psyllid/$psyllid_tag /usr/local/p8/psyllid/$psyllid_tag

# P8Compute directory and setup script
# Fake CVMFS directory to match previous directory structure
ENV CVMFS_PATH=/cvmfs/hep.pnnl.gov/project8
RUN mkdir -p $P8COMPUTE_BUILD_PREFIX &&\
    chmod -R 777 $P8COMPUTE_BUILD_PREFIX/.. &&\
    cd $P8COMPUTE_BUILD_PREFIX &&\
    echo 'ln -sfT $P8COMPUTE_BUILD_PREFIX $P8COMPUTE_BUILD_PREFIX/../current' > setup.sh &&\
    echo "source /usr/local/p8/katydid/${katydid_tag}/setup.sh" >> setup.sh &&\ 
    echo "source /usr/local/p8/locust/${locust_tag}/setup.sh" >> setup.sh &&\ 
    echo "source /usr/local/p8/mermithid/${mermithid_tag}/setup.sh" >> setup.sh &&\
    echo "source /usr/local/p8/mermithid/${mermithid_tag}/bin/this_cicada.sh" >> setup.sh &&\
    echo "source /usr/local/p8/mermithid/${mermithid_tag}/bin/this_phylloxera.sh" >> setup.sh &&\
    echo "source /usr/local/p8/psyllid/${psyllid_tag}/setup.sh" >> setup.sh &&\
    mkdir -p /cvmfs/hep.pnnl.gov &&\
    ln -sf /usr/local/p8 $CVMFS_PATH &&\
    chmod 777 /usr/local/p8/katydid \
              /usr/local/p8/locust \
              /usr/local/p8/mermithid \
              /usr/local/p8/psyllid \
              /usr/local/p8/katydid/$katydid_tag \ 
              /usr/local/p8/locust/$locust_tag \
              /usr/local/p8/mermithid/$mermithid_tag \
              /usr/local/p8/psyllid/$psyllid_tag &&\
    /bin/true


##############
# Old Versions
##############

# We're keeping P8Compute v0.5.0 and not v0.6.0, because v0.6.0 was not really in use for very long
# P8Compute v0.5.0 provides Katydid v2.15.3, Locust v1.11.0, and Mermithid v1.1.8
# It also uses Commmon v0.4.0
COPY --from=project8/p8compute:v0.5.0 /usr/local/p8/common/v0.4.0 /usr/local/p8/common/v0.4.0
COPY --from=project8/p8compute:v0.5.0 /usr/local/p8/locust/v1.11.0 /usr/local/p8/locust/v1.11.0
COPY --from=project8/p8compute:v0.5.0 /usr/local/p8/katydid/v2.15.3 /usr/local/p8/katydid/v2.15.3
COPY --from=project8/p8compute:v0.5.0 /usr/local/p8/mermithid/v1.1.8 /usr/local/p8/mermithid/v1.1.8
COPY --from=project8/p8compute:v0.5.0 /usr/local/p8/compute/v0.5.0 /usr/local/p8/compute/v0.5.0
RUN chmod 777 /usr/local/p8/common/v0.4.0 \
              /usr/local/p8/locust/v1.11.0 \
              /usr/local/p8/katydid/v2.15.3 \
              /usr/local/p8/mermithid/v1.1.8 \
              /usr/local/p8/compute/v0.5.0 &&\
    /bin/true
