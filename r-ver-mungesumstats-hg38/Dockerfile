FROM rocker/r-ver:4.5.3

# Install system dependencies
RUN apt-get update && apt-get install -y \
    libcurl4-openssl-dev \
    libssl-dev \
    libxml2-dev \
    wget \
    bzip2 \
    zlib1g-dev \
    libbz2-dev \
    liblzma-dev \
    libncurses5-dev && \
    rm -rf /var/lib/apt/lists/*

ARG HTS_VERSION="1.23"

RUN cd /tmp && \
    wget "https://github.com/samtools/htslib/releases/download/${HTS_VERSION}/htslib-${HTS_VERSION}.tar.bz2" && \
    tar -xjf "htslib-${HTS_VERSION}.tar.bz2" && \
    cd "htslib-${HTS_VERSION}" && ./configure --prefix=/usr/local && make -j"$(nproc)" && make install && \
    cd /tmp && \
    wget "https://github.com/samtools/bcftools/releases/download/${HTS_VERSION}/bcftools-${HTS_VERSION}.tar.bz2" && \
    tar -xjf "bcftools-${HTS_VERSION}.tar.bz2" && \
    cd "bcftools-${HTS_VERSION}" && ./configure --prefix=/usr/local && make -j"$(nproc)" && make install && \
    cd / && rm -rf /tmp/* && ldconfig

# Install BiocManager, MungeSumstats, and genome annotation packages
RUN Rscript -e "\
    options(timeout = 3600); \
    install.packages(\"data.table\", repos = \"https://cloud.r-project.org\"); \
    install.packages(\"BiocManager\", repos = \"https://cloud.r-project.org\"); \
    BiocManager::install(version = \"3.22\", ask = FALSE, update = FALSE); \
    BiocManager::install(\"rtracklayer\", ask = FALSE, update = FALSE); \
    BiocManager::install(\"GenomicRanges\", ask = FALSE, update = FALSE); \
    BiocManager::install(\"MungeSumstats\", ask = FALSE, update = FALSE); \
    BiocManager::install(\"BSgenome.Hsapiens.NCBI.GRCh38\", ask = FALSE, update = FALSE) \
"

CMD ["/bin/bash"]
