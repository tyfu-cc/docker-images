FROM r-base:4.5.3

# Install system dependencies
RUN apt-get update && apt-get install -y \
    wget \
    unzip \
    libcurl4-openssl-dev \
    libssl-dev \
    libxml2-dev \
    && rm -rf /var/lib/apt/lists/*

# Install PLINK 2.0
RUN wget https://s3.amazonaws.com/plink2-assets/plink2_linux_x86_64_20260110.zip \
    && unzip plink2_linux_x86_64_20260110.zip -d /usr/bin/ \
    && rm plink2_linux_x86_64_20260110.zip

# Install data.table, susieR, and coloc
RUN Rscript -e "\
    install.packages(c(\"data.table\", \"remotes\"), repos = \"https://cloud.r-project.org\"); \
    remotes::install_github(\"stephenslab/susieR@v0.14.2\"); \
    remotes::install_github(\"chr1swallace/coloc@main\") \
"

CMD ["/bin/bash"]
