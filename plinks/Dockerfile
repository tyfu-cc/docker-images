FROM debian:bookworm-slim

# Install dependencies
RUN apt-get update && apt-get install -y \
    wget \
    unzip \
    libgomp1 \
    && rm -rf /var/lib/apt/lists/*

WORKDIR /opt/bin

# Install PLINK 1.9
RUN wget https://s3.amazonaws.com/plink1-assets/plink_linux_x86_64_20231211.zip \
    && unzip plink_linux_x86_64_20231211.zip -d /usr/local/bin/ \
    && rm plink_linux_x86_64_20231211.zip

# Install PLINK 2.0
RUN wget https://s3.amazonaws.com/plink2-assets/alpha6/plink2_linux_x86_64_20241021.zip \
    && unzip plink2_linux_x86_64_20241021.zip -d /usr/local/bin/ \
    && rm plink2_linux_x86_64_20241021.zip

ENV PATH="/usr/local/bin:${PATH}"

CMD ["/bin/bash"]
