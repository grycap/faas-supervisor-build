FROM ubuntu:16.04
LABEL maintainer="Miguel Caballer <micafer1@upv.es>"
LABEL description="Container image to build faas-supervisor in amd64"
RUN apt update
RUN apt install -y build-essential zlib1g-dev libncurses5-dev libgdbm-dev libnss3-dev libssl-dev libreadline-dev libffi-dev wget
RUN wget https://www.python.org/ftp/python/3.8.12/Python-3.8.12.tgz
RUN tar -xzf Python-3.8.12.tgz
RUN cd Python-3.8.12 && \
    ./configure --enable-optimizations --enable-shared && \
    make altinstall



FROM ubuntu:16.04
# Add global TARGETARCH argument to this stage
ARG TARGETARCH
LABEL maintainer="Miguel Caballer <micafer1@upv.es>"
LABEL description="Container image to build faas-supervisor in amd64"
RUN apt update
RUN apt install -y zip libssl1.0.0 binutils libffi6 wget
COPY --from=0 /usr/local/lib /usr/local/lib
COPY --from=0 /usr/local/bin /usr/local/bin
COPY --from=0 /usr/local/include /usr/local/include
ENV LD_LIBRARY_PATH /usr/local/lib
RUN if [ "$TARGETARCH" = "arm64" ]; then \
          wget https://github.com/Kitware/CMake/releases/download/v3.22.1/cmake-3.22.1-linux-aarch64.sh; \
          chmod +x cmake-3.22.1-linux-aarch64.sh; \
          mkdir /opt/cmake; \
          ./cmake-3.22.1-linux-aarch64.sh --skip-license --exclude-subdir --prefix=/opt/cmake; \
          ln -s /opt/cmake/bin/* /usr/local/bin; \
    fi
RUN python3.8 -m ensurepip
RUN python3.8 -m pip --no-cache-dir install pyinstaller
RUN python3.8 -m pip --no-cache-dir install boto3==1.20.38 \
                                            requests==2.27.1 \
                                            setuptools>=40.8.0 \
                                            wheel==0.37.1 \
                                            pyyaml==6.0 \
                                            awslambdaric==2.0.1
