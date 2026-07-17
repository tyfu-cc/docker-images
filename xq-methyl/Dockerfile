FROM rocker/verse:4.4.3

ENV LANG=C.UTF-8 LC_ALL=C.UTF-8
ARG DEBIAN_FRONTEND=noninteractive

RUN R -q -e 'devtools::install_github("jcbeer/longCombat")'

CMD ["bash"]
