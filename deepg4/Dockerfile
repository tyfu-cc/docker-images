
FROM quay.io/jupyter/datascience-notebook:python-3.11 

USER root

RUN apt-get update && apt-get install -y \
    git \
    libxml2-dev \
    libcurl4-openssl-dev \
    libssl-dev \
    libz-dev \
    libbz2-dev \
    liblzma-dev \
    libpcre2-dev \
    libfreetype6-dev \
    libpng-dev \
    libjpeg-dev \
    libtiff-dev \
    libwebp-dev \
    pkg-config \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

RUN mamba install -y -c conda-forge \
    jupyter-server-proxy \
    tqdm \
    tensorflow \
    h5py \
    protobuf \
    tensorboard \
    pip \
    r-ragg \
    r-devtools \
    r-biocmanager \
    bioconductor-biostrings \
    bioconductor-rtracklayer \
    bioconductor-bsgenome.hsapiens.ucsc.hg19 && \
    mamba clean --all -f -y && \
    fix-permissions "${CONDA_DIR}" && \
    fix-permissions "/home/${NB_USER}"

USER ${NB_UID}

# Make R use binary packages and not compile anything
ENV R_COMPILE_AND_INSTALL_PACKAGES=never
RUN echo 'options(pkgType="binary")' >> /etc/R/Rprofile.site

# Ensure R finds conda-installed packages
ENV R_LIBS_SITE=/opt/conda/lib/R/library
ENV R_LIBS_USER=/opt/conda/lib/R/library

RUN R -e "devtools::install_github('morphos30/DeepG4')"

CMD ["bash"]

