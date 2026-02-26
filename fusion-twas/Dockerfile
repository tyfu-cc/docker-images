FROM rocker/r-ver:4.4.3

WORKDIR /opt/fusion

COPY fusion_twas/. .

RUN R -q -e "install.packages(c('optparse', 'devtools', 'data.table')); \
             devtools::install_github('chrchang/plink-ng', subdir = '2.0/pgenlibr')"

CMD ["/bin/bash"]

