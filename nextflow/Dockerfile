FROM nextflow/nextflow:25.10.3

USER root

RUN dnf -y install libnsl && \
    dnf clean all && \
    rm -rf /var/cache/dnf

ENTRYPOINT ["/usr/local/bin/entry.sh"]

