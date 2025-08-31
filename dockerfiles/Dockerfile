FROM ghcr.io/taffish-org/blast:2.16.0

LABEL maintainer="taffish@163.com"

ENV DEBIAN_FRONTEND=noninteractive

RUN apt-get update && \
    apt-get install -y curl git gcc g++ make python3 python3-dev build-essential \
                       zlib1g zlib1g-dev bzip2 swig ruby-dev libperl-dev \ 
                       autoconf automake libtool yaggo fig2dev gnuplot xfig \
                       r-base pkg-config libssl-dev && \
    cd / && \
    curl -LO https://github.com/lh3/minimap2/releases/download/v2.29/minimap2-2.29.tar.bz2 && \
    bzip2 -d /minimap2-2.29.tar.bz2 && \
    tar -xvf /minimap2-2.29.tar && rm /minimap2-2.29.tar && \
    cd /minimap2-2.29/ && \
    if [ "$(uname -m)" = "aarch64" ]; then make arm_neon=1 aarch64=1; else make; fi && \
    PATH=/minimap2-2.29:{$PATH} && \
    cd / && \
    git clone https://github.com/lh3/unimap && \
    cd /unimap/ && make && \
    PATH=/unimap:{$PATH} && \
    cd / && \
    curl -LO https://github.com/mummer4/mummer/releases/download/v4.0.1/mummer-4.0.1.tar.gz && \
    tar -zxvf /mummer-4.0.1.tar.gz && rm /mummer-4.0.1.tar.gz && cd /mummer-4.0.1/ && \
    ./configure && make && make check && make install && \
    cd / && \
    curl -LO https://github.com/Benson-Genomics-Lab/TRF/archive/refs/tags/v4.09.1.tar.gz && \
    tar -zxvf /v4.09.1.tar.gz && rm /v4.09.1.tar.gz && \
    cd /TRF-4.09.1/ && \
    mkdir /TRF-4.09.1/build && cd /TRF-4.09.1/build && /TRF-4.09.1/configure && \
    make && make install && \
    cd / && \
    curl -LO https://github.com/weizhongli/cdhit/releases/download/V4.8.1/cd-hit-v4.8.1-2019-0228.tar.gz && \
    tar xvf /cd-hit-v4.8.1-2019-0228.tar.gz && rm /cd-hit-v4.8.1-2019-0228.tar.gz && \
    mv /cd-hit-v4.8.1-2019-0228 /cd-hit && \
    cd /cd-hit/ && make && \
    cd /cd-hit/cd-hit-auxtools/ && make && \
    PATH=/cd-hit:/cd-hit/cd-hit-auxtools:/cd-hit/psi-cd-hit:{$PATH} && \
    curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh -s -- -y && \
    . "$HOME/.cargo/env" && \
    cd / && \
    curl -LO https://github.com/tolkit/telomeric-identifier/releases/download/v0.2.65/source.tar.gz && \
    tar -zxvf /source.tar.gz && rm /source.tar.gz && cd /tidk-0.2.65/ && \
    cargo install --path=. && \
    Rscript -e "install.packages(c('RIdeogram','ggplot2'), repos='https://cloud.r-project.org/')" && \
    cd / && \
    curl -LO https://github.com/aaranyue/quarTeT/archive/refs/tags/v1.2.5.tar.gz && \
    tar -zxvf /v1.2.5.tar.gz && rm /v1.2.5.tar.gz && cd /quarTeT-1.2.5/ && \
    chmod +x ./*.py && \
    PATH=/quarTeT-1.2.5:${PATH}

ENV PATH=/minimap2-2.29:{$PATH}
ENV PATH=/unimap:{$PATH}
ENV PATH=/cd-hit:/cd-hit/cd-hit-auxtools:/cd-hit/psi-cd-hit:{$PATH}
ENV PATH=/root/.cargo/bin:${PATH}
ENV PATH=/quarTeT-1.2.5:${PATH}

ENV TAFFISH_ENV=TAFFISH
ENV TAFFISH_NAME=quartet
