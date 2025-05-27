FROM python:3.10-slim AS builder

# Always set a working directory
WORKDIR /build

# Sets utf-8 encoding
ENV LANG=C.UTF-8
# Turns off writing .pyc files
ENV PYTHONDONTWRITEBYTECODE=1
# Seems to speed things up
ENV PYTHONUNBUFFERED=1
# Ensures that the python and pip executables used will be those from the virtualenv
ENV PATH="/venv/bin:$PATH"

# Install build tools
RUN apt-get update && \
    apt-get install -y --no-install-recommends \
    build-essential \
    wget \
    git \
    zlib1g-dev && \
    rm -rf /var/lib/apt/lists/*

# Download kallisto
RUN wget -O kallisto.tar.gz https://github.com/pachterlab/kallisto/releases/download/v0.44.0/kallisto_linux-v0.44.0.tar.gz && \
    tar -xzf kallisto.tar.gz && \
    chmod +x kallisto_linux-v0.44.0/kallisto

# Setup the virtualenv
RUN python -m venv /venv

# Install python packages
RUN git clone https://github.com/signalbash/how_are_we_stranded_here.git
RUN pip install --no-cache-dir ./how_are_we_stranded_here


# ---- Second stage ----
FROM python:3.10-slim

# Extra python env
ENV PYTHONDONTWRITEBYTECODE=1
ENV PYTHONUNBUFFERED=1
ENV PIP_DISABLE_PIP_VERSION_CHECK=1
ENV PATH="/venv/bin:$PATH"

WORKDIR /app

# Copy in python packages and kallisto
COPY --from=builder /venv /venv
COPY --from=builder /build/kallisto_linux-v0.44.0/kallisto /usr/local/bin/kallisto

# The WashU RIS seems to overwrites the PATH variable inside the Docker container
RUN find /venv/bin -type f -executable -exec ln -s {} /usr/local/bin/ \;

# Compliant with LSF — no ENTRYPOINT
CMD ["/bin/sh"]

