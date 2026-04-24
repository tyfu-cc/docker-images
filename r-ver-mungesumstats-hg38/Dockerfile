FROM rocker/r-ver:4.5.3

# Install system dependencies
RUN apt-get update && \
    apt-get install -y \
    libcurl4-openssl-dev \
    libssl-dev \
    libxml2-dev \
    libfontconfig1-dev \
    libharfbuzz-dev \
    libfribidi-dev \
    libfreetype6-dev \
    libpng-dev \
    libtiff5-dev \
    libjpeg-dev \
    && rm -rf /var/lib/apt/lists/*

# Install BiocManager, MungeSumstats, and genome annotation packages
RUN Rscript -e "\
    install.packages(\"data.table\", repos = \"https://cloud.r-project.org\"); \
    install.packages(\"BiocManager\", repos = \"https://cloud.r-project.org\"); \
    BiocManager::install(version = \"3.22\", ask = FALSE, update = FALSE); \
    BiocManager::install(\"rtracklayer\", ask = FALSE, update = FALSE); \
    BiocManager::install(\"GenomicRanges\", ask = FALSE, update = FALSE) \
    BiocManager::install(\"MungeSumstats\", ask = FALSE, update = FALSE); \
    BiocManager::install(\"SNPlocs.Hsapiens.dbSNP155.GRCh38\", ask = FALSE, update = FALSE); \
    BiocManager::install(\"BSgenome.Hsapiens.NCBI.GRCh38\", ask = FALSE, update = FALSE) \
"

CMD ["/bin/bash"]
