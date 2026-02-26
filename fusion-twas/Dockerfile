FROM rocker/r-ver:4.4.3

RUN apt-get update \
  && apt-get install -y --no-install-recommends \
     build-essential \
     zlib1g-dev \
  && rm -rf /var/lib/apt/lists/*

WORKDIR /opt/fusion

COPY fusion_twas/. .

RUN R -q -e "install.packages(c('optparse', 'devtools', 'data.table')); \
             devtools::install_github('chrchang/plink-ng', subdir = '2.0/pgenlibr')"

CMD ["/bin/bash"]

