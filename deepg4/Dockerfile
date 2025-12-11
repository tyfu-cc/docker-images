
FROM rocker/tidyverse:4.4.3

USER root

# Install system dependencies for Python and HDF5
RUN apt-get update && \
    apt-get install -y --no-install-recommends build-essential \
    libxml2-dev \
    libssl-dev \
    libssh2-1 \
    libcurl4-openssl-dev \
    libidn11-dev \
    libldap2-dev \
    libssh2-1-dev \
    libhdf5-dev \
    libz-dev \
    libbz2-dev \
    liblzma-dev \
    libpcre2-dev \
    curl \
    bzip2 \
    ca-certificates \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

# Install micromamba
RUN curl -L https://micro.mamba.pm/api/micromamba/linux-64/latest | \
    tar -xvj -C /usr/local/bin --strip-components=1 bin/micromamba

# Create conda env for DeepG4
RUN micromamba create -y -p /opt/conda/envs/deepg4 \
    python=3.7 \
    pip && \
    micromamba clean -a -y && \
    /opt/conda/envs/deepg4/bin/pip install --no-cache-dir \
    tensorflow==2.1.0 \
    h5py==2.10.0 \
    protobuf==3.20.* \
    numpy==1.19.*

# Make environment available system-wide
ENV PATH=/opt/conda/envs/deepg4/bin:$PATH

# Install R packages
RUN R -q -e "install.packages(c('BiocManager', 'yardstick'), repos='https://cloud.r-project.org'); \
             BiocManager::install(c('Biostrings','rtracklayer','BSgenome.Hsapiens.UCSC.hg19')); \
             devtools::install_github('morphos30/DeepG4')"

# Ensure reticulate uses micromamba and recognize python
RUN echo 'RETICULATE_PYTHON=/opt/conda/envs/deepg4/bin/python' >> /etc/R/Renviron.site && \
    echo 'RETICULATE_CONDA=/usr/local/bin/micromamba' >> /etc/R/Renviron.site && \
    echo 'Sys.setenv(RETICULATE_PYTHON="/opt/conda/envs/deepg4/bin/python")' >> /etc/R/Rprofile.site && \
    echo 'Sys.setenv(RETICULATE_CONDA="/usr/local/bin/micromamba")' >> /etc/R/Rprofile.site

CMD ["bash"]

