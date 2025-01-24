FROM ubuntu:24.10
# Add global TARGETARCH argument to this stage
ARG TARGETARCH
LABEL maintainer="Miguel Caballer <micafer1@upv.es>"
LABEL description="Container image to build faas-supervisor in amd64"
RUN apt update
RUN apt install -y zip build-essential zlib1g-dev libncurses5-dev autoconf libgdbm-dev libnss3-dev libssl-dev libreadline-dev libffi-dev wget binutils wget
RUN wget https://www.python.org/ftp/python/3.12.8/Python-3.12.8.tgz
RUN tar -xzf Python-3.12.8.tgz
RUN cd Python-3.12.8 && \
    ./configure --enable-optimizations && \
    make install
ENV LD_LIBRARY_PATH=/usr/local/lib
RUN python3 -m ensurepip
#RUN if [ "$TARGETARCH" = "arm64" ]; then \
RUN wget https://github.com/Kitware/CMake/releases/download/v3.22.1/cmake-3.22.1-linux-aarch64.sh; \
        chmod +x cmake-3.22.1-linux-aarch64.sh; \
        mkdir /opt/cmake; \
        ./cmake-3.22.1-linux-aarch64.sh --skip-license --exclude-subdir --prefix=/opt/cmake; \
        ln -s /opt/cmake/bin/* /usr/local/bin
#     fi
RUN python3 -m pip --no-cache-dir install pyinstaller
RUN python3 -m pip --no-cache-dir install boto3==1.20.38 \
                                            requests==2.27.1 \
                                            setuptools>=40.8.0 \
                                            pyyaml==6.0.1 \
                                            wheel==0.37.1 \
                                            awslambdaric==2.0.0
