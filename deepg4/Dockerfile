
FROM quay.io/jupyter/datascience-notebook:python-3.11

USER root

RUN mamba install -y -c conda-forge \
    jupyter-server-proxy \
    tqdm \
    tensorflow==2.1.0 \
    h5py \
    protobuf \
    tensorboard \
    pip && \
    mamba clean --all -f -y && \
    fix-permissions "${CONDA_DIR}" && \
    fix-permissions "/home/${NB_USER}"

USER ${NB_UID}

RUN R -e "install.packages('devtools', repos='https://cloud.r-project.org'); \
          devtools::install_github('morphos30/DeepG4')"

CMD ["bash"]
