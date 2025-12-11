
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
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

# Install micromamba
RUN curl -L https://micro.mamba.pm/api/micromamba/linux-64/latest | \
    tar -xvj -C /usr/local/bin --strip-components=1 bin/micromamba

# Create conda env for DeepG4
RUN micromamba create -y -p /opt/conda/envs/deepg4 \
    python=3.7 \
    tensorflow=2.1.0 \
    h5py=2.10.0 \
    protobuf=3.20 \
    pip

# Make environment available system-wide
ENV PATH=/opt/conda/envs/deepg4/bin:$PATH
ENV RETICULATE_PYTHON=/opt/conda/envs/deepg4/bin/python

# Install R packages
RUN R -q -e "install.packages('BiocManager', repos='https://cloud.r-project.org'); \
             BiocManager::install(c('Biostrings','rtracklayer','BSgenome.Hsapiens.UCSC.hg19')); \
             devtools::install_github('morphos30/DeepG4')"

CMD ["bash"]

