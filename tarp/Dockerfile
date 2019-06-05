FROM sunxing/ubuntu-cuda-conda3:0.1

LABEL maintainer=sunxing@hopechart.com \
      version=0.1

RUN \
    # change source to aliyun
    #sed -i 's/archive.ubuntu.com/mirrors.aliyun.com/g' /etc/apt/sources.list && \
    #sed -i 's/security.ubuntu.com/mirrors.aliyun.com/g' /etc/apt/sources.list && \
    apt-get --fix-missing update  && \
    apt-get --fix-broken install && \
    apt-get -y upgrade && \
    apt-get -y autoremove && \
    # install dependency
    apt-get install wget python3 python3-dev -y --no-install-recommends && \
    apt-get install  git make cmake g++ -y --no-install-recommends && \
    # try 3 times because there are serveral large files to download.
    TRY_TIMES=3 && \
    for _ in `seq ${TRY_TIMES}`; do conda install pytorch=0.4.0 torchvision -c pytorch     --yes; done && \
    for _ in `seq ${TRY_TIMES}`; do conda install caffe2                    -c caffe2      --yes; done && \
    for _ in `seq ${TRY_TIMES}`; do conda install onnx onnx-caffe2          -c conda-forge --yes; done && \ 
    conda clean --all --yes && \
    # clean up
    apt-get remove git make cmake g++ gcc python3-dev -y && \
    apt-get autoremove -y && \
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*
    