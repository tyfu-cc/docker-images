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
    libglpk-dev \
    && rm -rf /var/lib/apt/lists/*

# Install BiocManager, MungeSumstats, and genome annotation packages
RUN Rscript -e "\
    options(timeout = 3600); \
    install.packages(\"argparse\", repos = \"https://cloud.r-project.org\"); \
    install.packages(\"data.table\", repos = \"https://cloud.r-project.org\"); \
    install.packages(\"pbapply\", repos = \"https://cloud.r-project.org\"); \
    install.packages(\"remotes\", repos = \"https://cloud.r-project.org\"); \
    remotes::install_github(\"BS1125/CMAverse\"); \
    install.packages(\"BiocManager\", repos = \"https://cloud.r-project.org\"); \
    BiocManager::install(version = \"3.22\", ask = FALSE, update = FALSE); \
    BiocManager::install(\"SummarizedExperiment\", ask = FALSE, update = FALSE); \
"

CMD ["/bin/bash"]
