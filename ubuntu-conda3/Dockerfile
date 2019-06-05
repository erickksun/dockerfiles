FROM ubuntu

ENV CONDA_DIR="/opt/conda"
ENV PATH="${CONDA_DIR}/bin:${PATH}"

# Install conda
RUN \ 
    # change source to aliyun
    sed -i 's/archive.ubuntu.com/mirrors.aliyun.com/g' /etc/apt/sources.list && \
    sed -i 's/security.ubuntu.com/mirrors.aliyun.com/g' /etc/apt/sources.list && \
    apt-get --fix-missing update  && \
    apt-get -y upgrade && \
    apt-get --fix-broken install && \
    apt-get -y autoremove && \
    apt-get clean && \
    CONDA_VERSION="4.5.12" && \
    CONDA_MD5_CHECKSUM="866ae9dff53ad0874e1d1a60b1ad1ef8" && \
    #--no-install-recommends ca-certificates apt-transport-https gnupg-curl
    apt-get install wget ca-certificates -y --no-install-recommends && \
    #
    mkdir -p ${CONDA_DIR} && \
    wget "https://repo.continuum.io/miniconda/Miniconda3-${CONDA_VERSION}-Linux-x86_64.sh" -O miniconda.sh && \
    echo "$CONDA_MD5_CHECKSUM  miniconda.sh" | md5sum -c && \
    bash miniconda.sh -f -b -p "$CONDA_DIR" && \
    echo "export PATH=$CONDA_DIR/bin:\$PATH" > /etc/profile && \
    export PATH=$CONDA_DIR/bin:$PATH && \
    rm miniconda.sh && \
    #
    conda config --set auto_update_conda False && \
    rm -rf ${CONDA_DIR}/pkgs/ && \
    #
    apt-get remove wget ca-certificates -y && \
    apt-get -y autoremove && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*
