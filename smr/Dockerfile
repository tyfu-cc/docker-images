FROM debian:bookworm-slim

RUN apt-get update && \
    apt-get install -y wget unzip libgomp1 && \
    rm -rf /var/lib/apt/lists/*

RUN wget -q https://yanglab.westlake.edu.cn/software/smr/download/smr-1.4.0-linux-x86_64.zip && \
    unzip smr-1.4.0-linux-x86_64.zip && \
    mv smr-1.4.0-linux-x86_64/smr /usr/bin/smr && \
    chmod +x /usr/bin/smr && \
    rm -rf smr-1.4.1-linux-x86_64*

CMD ["/bin/bash"]
