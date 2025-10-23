
ARG BASE_IMAGE=quay.io/jupyter/pytorch-notebook:cuda12-python-3.12.11
FROM $BASE_IMAGE

USER root

# Add additional libraries
RUN mamba install -y -c conda-forge \
    tqdm \
    scikit-survival \
    torchsurv \
    nibabel \
    tensorboard \
    jupyter-server-proxy \
    pip && \
    mamba clean --all -f -y && \
    fix-permissions "${CONDA_DIR}" && \
    fix-permissions "/home/${NB_USER}"

USER ${NB_UID}

CMD ["bash"]
