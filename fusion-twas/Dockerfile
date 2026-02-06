FROM rocker/r-ver:4.4.3

WORKDIR /root

COPY fusion_twas/. .
COPY plink2R-master ./plink2R-master
COPY LDREF ./LDREF

RUN R -q -e "install.packages(c('Rcpp', 'RcppEigen', 'optparse', 'RColorBrewer')); \
             install.packages('plink2R-master/plink2R/', repos = NULL)"

CMD ["bash"]

