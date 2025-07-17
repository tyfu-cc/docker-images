FROM ubuntu:22.04 AS build

ARG DEBIAN_FRONTEND=noninteractive

WORKDIR /build

RUN apt-get update && \
    apt-get install -y --no-install-recommends \
    bc \
    bzip2 \
    ca-certificates \
    curl \
    g++ \
    gcc \
    gfortran \
    git \
    less \
    make \
    parallel \
    texlive-latex-base texlive-latex-extra \
    unzip \
    xorg-dev \
    zlib1g-dev \
    vim \
    wget \
    libbz2-dev && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*
