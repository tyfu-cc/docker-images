FROM r-base:4.5.3

# Install system dependencies
RUN apt-get update && apt-get install -y \
    libcurl4-openssl-dev \
    libssl-dev \
    libxml2-dev \
    && rm -rf /var/lib/apt/lists/*

# Install data.table, susieR, and coloc
RUN Rscript -e "\
    install.packages(c(\"data.table\", \"remotes\"), repos = \"https://cloud.r-project.org\"); \
    remotes::install_github(\"stephenslab/susieR@v0.14.2\"); \
    remotes::install_github(\"chr1swallace/coloc@main\", build_vignettes = TRUE) \
"

CMD ["/bin/bash"]
