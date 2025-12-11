
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
    libtiff-dev \
    libfreetype6-dev \
    libfontconfig1-dev \
    libharfbuzz-dev \
    libfribidi-dev \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

RUN mamba install -y -c conda-forge \
    jupyter-server-proxy \
    tqdm \
    tensorflow \
    h5py \
    protobuf \
    tensorboard \
    pip && \
    mamba clean --all -f -y && \
    fix-permissions "${CONDA_DIR}" && \
    fix-permissions "/home/${NB_USER}"

USER ${NB_UID}

RUN R -e "install.packages('devtools', 'BiocManager', repos='https://cloud.r-project.org'); \
          BiocManager::install(version='3.18') \
          BiocManager::install(c('Biostrings', 'rtracklayer')); \
          devtools::install_github('morphos30/DeepG4')"

CMD ["bash"]

