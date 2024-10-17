FROM ubuntu:20.04

ENV BASE_URL="https://releases.quilibrium.com" \
    NODE_VERSION=2.0.0.7

# 使用中科大镜像源
RUN sed -i 's@//.*archive.ubuntu.com@//mirrors.ustc.edu.cn@g' /etc/apt/sources.list \
    && sed -i 's/security.ubuntu.com/mirrors.ustc.edu.cn/g' /etc/apt/sources.list

# 安装必要的依赖
RUN apt-get update && apt-get install -y \
    netcat \
    && rm -rf /var/lib/apt/lists/*

RUN set -eux \
    && apt-get -y update  \
    && apt-get -y install --no-install-recommends \ 
    netcat \
    wget \
    apt-transport-https \
    ca-certificates \                                                                                                                                                                                                      
    && update-ca-certificates\
    && apt-get -y --purge autoremove \
    && apt-get -y clean \
    && rm -rf /var/lib/apt/lists/* \
    && rm -rf /tmp/* \
    && rm -rf /var/tmp/* 

# 创建应用目录
WORKDIR /app

# 下载二进制文件以及签名到容器中
RUN set -eux \
    && wget -c ${BASE_URL}/node-${NODE_VERSION}-linux-amd64 -O node-${NODE_VERSION}-linux-amd64 \
    && wget -c ${BASE_URL}/node-${NODE_VERSION}-linux-amd64.dgst -O node-${NODE_VERSION}-linux-amd64.dgst \
    && wget -c ${BASE_URL}/node-${NODE_VERSION}-linux-amd64.dgst.sig.1 -O node-${NODE_VERSION}-linux-amd64.dgst.sig.1  \
    && wget -c ${BASE_URL}/node-${NODE_VERSION}-linux-amd64.dgst.sig.2 -O node-${NODE_VERSION}-linux-amd64.dgst.sig.2  \
    && wget -c ${BASE_URL}/node-${NODE_VERSION}-linux-amd64.dgst.sig.3 -O node-${NODE_VERSION}-linux-amd64.dgst.sig.3  \
    && wget -c ${BASE_URL}/node-${NODE_VERSION}-linux-amd64.dgst.sig.4 -O node-${NODE_VERSION}-linux-amd64.dgst.sig.4  \
    && wget -c ${BASE_URL}/node-${NODE_VERSION}-linux-amd64.dgst.sig.5 -O node-${NODE_VERSION}-linux-amd64.dgst.sig.5  \
    && wget -c ${BASE_URL}/node-${NODE_VERSION}-linux-amd64.dgst.sig.6 -O node-${NODE_VERSION}-linux-amd64.dgst.sig.6  \
    && wget -c ${BASE_URL}/node-${NODE_VERSION}-linux-amd64.dgst.sig.9 -O node-${NODE_VERSION}-linux-amd64.dgst.sig.9  \
    && wget -c ${BASE_URL}/node-${NODE_VERSION}-linux-amd64.dgst.sig.13 -O node-${NODE_VERSION}-linux-amd64.dgst.sig.13  \
    && wget -c ${BASE_URL}/node-${NODE_VERSION}-linux-amd64.dgst.sig.15 -O node-${NODE_VERSION}-linux-amd64.dgst.sig.15

# 设置执行权限
RUN chmod +x node-${NODE_VERSION}-linux-amd64

# 设置默认命令
CMD ["sh", "-c", "./node-${NODE_VERSION}-linux-amd64"]
