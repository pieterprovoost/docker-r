FROM ubuntu:latest

LABEL org.opencontainers.image.source="https://github.com/pieterprovoost/docker-r`" \
    org.opencontainers.image.authors="Pieter Provoost <pieterprovoost@gmail.com>"

ENV DEBIAN_FRONTEND=noninteractive

RUN set -e \
    && apt-get update \
    && apt-get upgrade -y \
    && apt-get -y install --no-install-recommends --no-install-suggests \
    apt-transport-https apt-utils ca-certificates cmake curl g++ gcc \
    gfortran git make libblas-dev libcurl4-gnutls-dev libfontconfig1-dev \
    libfreetype6-dev libfribidi-dev libgit2-dev libharfbuzz-dev \
    libiodbc2-dev libjpeg-dev liblapack-dev libmariadb-dev libpng-dev \
    libpq-dev libsqlite3-dev libssh-dev libssl-dev libtiff5-dev \
    libjq-dev libxml2-dev locales pandoc pkg-config r-base \
    && apt-get -y autoremove \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

RUN set -e \
    && Rscript -e 'install.packages(c("remotes", "terra", "arrow", "sf", "ggplot2", "worrms", "leaflet", "DBI", "RPostgres", "seqinr", "BiocManager", "robis"), dependencies = TRUE, repos = "https://cloud.r-project.org")'
RUN set -e \
    && R -e 'remotes::install_github("ropensci/finch", dependencies = TRUE, force = TRUE)'
RUN set -e \
    && R -e 'BiocManager::install(c("phyloseq", "Biostrings"))'

CMD ["R"]
