
ARG BASE_IMAGE=quay.io/jupyter/pytorch-notebook:cuda12-python-3.11
FROM $BASE_IMAGE

# Name the environment and choose the Python version
ARG env_name=adninn
ARG py_version=3.11

# Add additional libraries
RUN mamba create --yes -p "${CONDA_DIR}/envs/${env_name}" \
    python=${py_ver} \
    ipykernel \
    jupyterlab \
    tqdm \
    numpy \
    pandas \
    matplotlib \
    scikit-learn \
    pip && \
    mamba clean --all -f -y

# Create python kernel and link it to jupyter
RUN "${CONDA_DIR}/envs/${env_name}/bin/python" -m ipykernel install --user --name="${env_name}" && \
    fix-permissions "${CONDA_DIR}" && \
    fix-permissions "/home/${NB_USER}"

# Install pytorch and others
RUN "${CONDA_DIR}/envs/${env_name}/bin/pip" install --no-cache-dir \
    torch torchvision torchaudio --index-url https://download.pytorch.org/whl/cu124 \
    scikit-survival nibabel tensorboard

# This changes the custom Python kernel so that the custom environment will
# be activated for the respective Jupyter Notebook and Jupyter Console
# hadolint ignore=DL3059
RUN /opt/setup-scripts/activate_notebook_custom_env.py "${env_name}"

# Comment the line above and uncomment the section below instead to activate the custom environment by default
# Note: uncommenting this section makes "${env_name}" default both for Jupyter Notebook and Terminals
# More information here: https://github.com/jupyter/docker-stacks/pull/2047
# USER root
# RUN \
#     # This changes a startup hook, which will activate the custom environment for the process
#     echo conda activate "${env_name}" >> /usr/local/bin/before-notebook.d/10activate-conda-env.sh && \
#     # This makes the custom environment default in Jupyter Terminals for all users which might be created later
#     echo conda activate "${env_name}" >> /etc/skel/.bashrc && \
#     # This makes the custom environment default in Jupyter Terminals for already existing NB_USER
#     echo conda activate "${env_name}" >> "/home/${NB_USER}/.bashrc"

USER ${NB_UID}

CMD ["bash"]
