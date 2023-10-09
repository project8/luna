ARG img_repo=ghcr.io/project8/luna_base
ARG img_tag=v1.3.3

ARG katydid_repo=ghcr.io/project8/katydid
ARG katydid_tag=v2.20.0
ARG locust_repo=ghcr.io/project8/locust_mc
ARG locust_tag=v2.5.3
ARG kassiopeia_tag=v4.0.0
#ARG mermithid_repo=docker.io/project8/mermithid
#ARG mermithid_tag=v1.2.2

# Katydid
FROM ${katydid_repo}:${katydid_tag} AS katydid

# Locust
FROM ${locust_repo}:${locust_tag} AS locust

# Mermithid
#FROM ${mermithid_repo}:${mermithid_tag} AS mermithid

FROM ${img_repo}:${img_tag}

# We repeat the version ARGs here so that we get their values from the pre-FROM ARGs
ARG katydid_tag
ARG locust_tag
ARG kassiopeia_tag
#ARG mermithid_tag

ARG p8compute_tag=beta
ENV P8COMPUTE_TAG=${p8compute_tag}
ENV P8COMPUTE_BUILD_PREFIX=/usr/local/p8/compute/$P8COMPUTE_TAG

COPY --from=katydid /usr/local/p8/katydid/$katydid_tag /usr/local/p8/katydid/$katydid_tag
COPY --from=locust /usr/local/p8/locust/$locust_tag /usr/local/p8/locust/$locust_tag
COPY --from=locust /usr/local/p8/kassiopeia/$kassiopeia_tag /usr/local/p8/kassiopeia/$kassiopeia_tag
#COPY --from=mermithid /usr/local/p8/mermithid/$mermithid_tag /usr/local/p8/mermithid/$mermithid_tag

# P8Compute directory and setup script
RUN mkdir -p $P8COMPUTE_BUILD_PREFIX &&\
    chmod -R 777 $P8COMPUTE_BUILD_PREFIX/.. &&\
    cd $P8COMPUTE_BUILD_PREFIX &&\
    echo 'ln -sfT $P8COMPUTE_BUILD_PREFIX $P8COMPUTE_BUILD_PREFIX/../current' > setup.sh &&\
    echo "source /usr/local/p8/katydid/${katydid_tag}/setup.sh" >> setup.sh &&\ 
    echo "source /usr/local/p8/locust/${locust_tag}/setup.sh" >> setup.sh &&\ 
    echo "source /usr/local/p8/kassiopeia/${kassiopeia_tag}/setup.sh" >> setup.sh &&\ 
#    echo "source /usr/local/p8/mermithid/${mermithid_tag}/setup.sh" >> setup.sh &&\
#    echo "source /usr/local/p8/mermithid/${mermithid_tag}/bin/this_cicada.sh" >> setup.sh &&\
#    echo "source /usr/local/p8/mermithid/${mermithid_tag}/bin/this_phylloxera.sh" >> setup.sh &&\
    chmod 777 /usr/local/p8/katydid \
              /usr/local/p8/locust \
              /usr/local/p8/kassiopeia \
#              /usr/local/p8/mermithid \
              /usr/local/p8/katydid/$katydid_tag \ 
              /usr/local/p8/locust/$locust_tag \
              /usr/local/p8/kassiopeia/$kassiopeia_tag \
#              /usr/local/p8/mermithid/$mermithid_tag &&\
    /bin/true
