
FROM rocker/tidyverse:4.4.3

USER root

# Install system dependencies for Python and HDF5
RUN apt-get update && \
    apt-get install -y --no-install-recommends build-essential \
    libxml2-dev \
    libssl-dev \
    libpng-dev \
    libssh2-1 \
    libcairo2-dev \
    libcurl4-openssl-dev \
    libcurl4-doc \
    libidn11-dev \
    libldap2-dev \
    libssh2-1-dev \
    libhdf5-dev \
    libhdf5-dev \
    libxml2-dev \
    libz-dev \
    libbz2-dev \
    liblzma-dev \
    libpcre2-dev \
    python3 \
    python3-pip \
    python3-dev \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

# Install Python libraries
RUN pip3 install --no-cache-dir \
    protobuf \
    h5py \
    tensorflow

# Install R packages
RUN R -q -e "install.packages('BiocManager', repos='https://cloud.r-project.org'); \
             BiocManager::install(c('Biostrings','rtracklayer','BSgenome.Hsapiens.UCSC.hg19')); \
             devtools::install_github('morphos30/DeepG4')"

CMD ["bash"]

