FROM nvidia/cuda:10.0-base

ENV CONDA_DIR="/opt/conda"
ENV PATH="${CONDA_DIR}/bin:${PATH}"

RUN \ 
    # change source to aliyun
    sed -i 's/archive.ubuntu.com/mirrors.aliyun.com/g' /etc/apt/sources.list && \
    sed -i 's/security.ubuntu.com/mirrors.aliyun.com/g' /etc/apt/sources.list && \
    apt-get --fix-missing update  && \
    apt-get -y upgrade && \
    apt-get --fix-broken install && \
    # install dependencies
    apt-get install wget ca-certificates -y --no-install-recommends && \
    # install miniconda3
    MINICONDA_VERSION="4.5.12" && \
    MINICONDA_MD5_CHECKSUM="866ae9dff53ad0874e1d1a60b1ad1ef8" && \
    wget "https://repo.continuum.io/miniconda/Miniconda3-${MINICONDA_VERSION}-Linux-x86_64.sh" -O miniconda.sh && \
    echo "${MINICONDA_MD5_CHECKSUM}  miniconda.sh" | md5sum -c && \
    mkdir -p ${CONDA_DIR} && \
    bash miniconda.sh -f -b -p ${CONDA_DIR} && \
    echo "export PATH=$CONDA_DIR/bin:\$PATH" > /etc/profile && \
    rm miniconda.sh && \
    # conda setting
    export PATH=$CONDA_DIR/bin:$PATH && \
    conda config --set auto_update_conda False && \
    rm -rf ${CONDA_DIR}/pkgs/ && \
    # clean up
    apt-get remove wget ca-certificates -y && \
    apt-get -y autoremove && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*
