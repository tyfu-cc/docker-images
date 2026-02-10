FROM nextflow/nextflow:25.10.3

USER root

RUN apt-get update && \
    apt-get install -y --no-install-recommends libnsl1 && \
    rm -rf /var/lib/apt/lists/*

ENTRYPOINT ["/usr/local/bin/entry.sh"]

