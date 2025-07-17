FROM rocker/verse:4.4.0

ENV LANG=C.UTF-8 LC_ALL=C.UTF-8
ARG DEBIAN_FRONTEND=noninteractive
RUN apt-get update \
    && apt-get install -y --no-install-recommends build-essential \
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
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

CMD ["bash"]
