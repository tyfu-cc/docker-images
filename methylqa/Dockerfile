FROM ubuntu:22.04 AS build

ARG DEBIAN_FRONTEND=noninteractive

WORKDIR /build

RUN apt-get update && \
    apt-get install -y --no-install-recommends \
    build-essential \
    ca-certificates \
    git \
    make \
    zlib1g-dev \
    libpng-dev \
    r-base \
    texlive-latex-base texlive-latex-extra && \
    rm -rf /var/lib/apt/lists/*

RUN git clone https://github.com/lidaof/methylQA.git && \
    cd methylQA/ && \
    sed -i 's/-Werror //' makefile && \
    make && \
    cd ..

# ----------

FROM debian:bookworm-slim

ENV PATH="/usr/local/bin:$PATH"
 
RUN apt-get update && \
    apt-get install -y --no-install-recommends procps && \
    rm -rf /var/lib/apt/lists/*

# # Copy in python packages and kallisto
COPY --from=build /build/methylQA/methylQA /usr/local/bin
# 
CMD ["/bin/sh"]

