FROM python:3.12-slim

ARG HTSLIB_VERSION="1.23"
ARG BCFTOOLS_VERSION="1.23"

# System libraries needed to build htslib and bcftools
RUN apt-get update && apt-get install -y --no-install-recommends \
    build-essential \
    wget \
    bzip2 \
    ca-certificates \
    zlib1g-dev \
    libbz2-dev \
    liblzma-dev \
    libcurl4-openssl-dev \
    libssl-dev \
    libdeflate-dev \
    libncurses-dev \
    && rm -rf /var/lib/apt/lists/*

WORKDIR /tmp

# htslib
RUN wget -q "https://github.com/samtools/htslib/releases/download/${HTSLIB_VERSION}/htslib-${HTSLIB_VERSION}.tar.bz2" \
    && tar -xjf "htslib-${HTSLIB_VERSION}.tar.bz2" \
    && cd "htslib-${HTSLIB_VERSION}" \
    && ./configure --prefix="/usr/local" \
    && make -j"$(nproc)" \
    && make install \
    && cd /tmp && rm -rf "htslib-${HTSLIB_VERSION}"*

# bcftools
RUN wget -q "https://github.com/samtools/bcftools/releases/download/${BCFTOOLS_VERSION}/bcftools-${BCFTOOLS_VERSION}.tar.bz2" \
    && tar -xjf "bcftools-${BCFTOOLS_VERSION}.tar.bz2" \
    && cd "bcftools-${BCFTOOLS_VERSION}" \
    && ./configure --prefix="/usr/local" --with-htslib="system" \
    && make -j"$(nproc)" \
    && make install \
    && cd /tmp && rm -rf "bcftools-${BCFTOOLS_VERSION}"* \
    && ldconfig

# GWASLab
RUN pip install --no-cache-dir --upgrade pip \
    && pip install --no-cache-dir "gwaslab==4.2.2"

CMD ["/bin/bash"]

