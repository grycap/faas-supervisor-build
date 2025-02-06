FROM alpine:3.16
# Add global TARGETARCH argument to this stage
ARG TARGETARCH
ENV PYTHON_VERSION=3.12.4
LABEL maintainer="Miguel Caballer <micafer1@upv.es>"
LABEL description="Container image to build faas-supervisor in alpine"
RUN apk add --no-cache \
        build-base \
        libffi-dev \
        zlib-dev \
        bzip2-dev \
        readline-dev \
        ncurses-dev \
        sqlite-dev \
        tk-dev \
        libssl1.1 \
        openssl-dev \
        musl-dev \
        curl \
        git \
        xz-dev \
        make \
        gcc \
        g++ && \
    curl -O https://www.python.org/ftp/python/${PYTHON_VERSION}/Python-${PYTHON_VERSION}.tgz && \
     tar -xvzf Python-${PYTHON_VERSION}.tgz && \
     cd Python-${PYTHON_VERSION} && \
     ./configure \
        --prefix=/usr/ \
        --enable-shared \
        --enable-optimizations \
        --enable-ipv6 \
        LDFLAGS=-Wl,-rpath=/usr/lib,--disable-new-dtags  && \
     make && \
     make install && \
     rm -rf /Python-${PYTHON_VERSION} && \
     apk del \
        build-base \
        libffi-dev \
        zlib-dev \
        bzip2-dev \
        readline-dev \
        ncurses-dev \
        sqlite-dev \
        tk-dev \
        libssl1.1 \
        openssl-dev \
        musl-dev \
        git \
        xz-dev

RUN apk add --no-cache autoconf libcurl zip unzip cmake make automake curl-dev libtool autoconf libexecinfo-dev
RUN python3 -m ensurepip
RUN pip3 --no-cache-dir install --upgrade pip setuptools>=40.8.0
RUN pip3 --no-cache-dir install pyinstaller 
RUN pip3 install --no-deps --ignore-installed    wheel==0.37.1 
RUN apk add --no-cache --virtual .build-deps gcc musl-dev \
 && pip3 install cython \
 && apk del .build-deps
RUN pip3 --no-cache-dir install awslambdaric==2.0.12
RUN pip3 --no-cache-dir install boto3==1.20.38 \
                               webdavclient3==3.14.6 \
                               requests==2.27.1 \
                               setuptools>=40.8.0 \
                               wheel==0.37.1 \
                               pyyaml==6.0.1 \
                               rucio-clients==1.31.7
