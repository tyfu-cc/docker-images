FROM debian:bookworm-slim

# Install dependencies
RUN apt-get update && apt-get install -y \
    wget \
    unzip \
    libgomp1 \
    && rm -rf /var/lib/apt/lists/*

# Install PLINK 1.9
RUN wget https://s3.amazonaws.com/plink1-assets/plink_linux_x86_64_20250819.zip \
    && unzip plink_linux_x86_64_20250819.zip -d /usr/bin/ \
    && rm plink_linux_x86_64_20250819.zip

# Install PLINK 2.0
RUN wget https://s3.amazonaws.com/plink2-assets/plink2_linux_x86_64_20260110.zip \
    && unzip plink2_linux_x86_64_20260110.zip -d /usr/bin/ \
    && rm plink2_linux_x86_64_20260110.zip

CMD ["/bin/bash"]
