FROM rocker/verse:4.4.0

ENV LANG=C.UTF-8 LC_ALL=C.UTF-8

ARG DEBIAN_FRONTEND=noninteractive

RUN apt-get update && \
    apt-get install -y --no-install-recommends build-essential && \
    libxml2-dev \
    libssl-dev \
    libgsl-dev \
    libpng-dev \
    libssh2-1 \
    libcairo2-dev \
    libcurl4-openssl-dev \
    libcurl4-doc \
    libidn11-dev \
    libldap2-dev \
    libssh2-1-dev \
    libhdf5-dev \
    unzip \
    wget \
    gwama && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

RUN wget https://s3.amazonaws.com/plink1-assets/plink_linux_x86_64_20250819.zip -O /tmp/plink1.9.zip && \
    unzip /tmp/plink1.9.zip -d /tmp/plink1.9 && \
    mv /tmp/plink1.9/plink /usr/bin/plink && \
    chmod +x /usr/bin/plink && \
    rm -rf /tmp/plink1.9 /tmp/plink1.9.zip && \
    wget https://s3.amazonaws.com/plink2-assets/alpha6/plink2_linux_x86_64_20241222.zip -O /tmp/plink2.zip && \
    unzip /tmp/plink2.zip -d /tmp/plink2 && \
    mv /tmp/plink2/plink2 /usr/bin/plink2 && \
    chmod +x /usr/bin/plink2 && \
    rm -rf /tmp/plink2 /tmp/plink2.zip

CMD ["bash"]
