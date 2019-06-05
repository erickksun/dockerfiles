FROM nvidia/cuda:10.0-cudnn7-devel-ubuntu18.04
ENV DEBIAN_FRONTEND=noninteractive
RUN \
    # change source to aliyun
    sed -i 's/archive.ubuntu.com/mirrors.aliyun.com/g' /etc/apt/sources.list && \
    sed -i 's/security.ubuntu.com/mirrors.aliyun.com/g' /etc/apt/sources.list && \
    apt-get update && \
    #apt-get upgrade -y --no-install-recommends && \
    apt-get install libopenblas-dev libopencv-dev libprotobuf-dev protobuf-compiler \
                    libboost-all-dev libsnappy-dev libgoogle-glog-dev libhdf5-dev \
                    libleveldb-dev liblmdb-dev \
                    -y --no-install-recommends && \
    apt-get install ca-certificates make cmake g++ gcc build-essential \
                    python-dev python-pip \
                    -y --no-install-recommends && \
    #apt-get autoremove && \
    apt-get clean
