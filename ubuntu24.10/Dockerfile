FROM ubuntu:24.10
# Add global TARGETARCH argument to this stage
ARG TARGETARCH
LABEL maintainer="Miguel Caballer <micafer1@upv.es>"
LABEL description="Container image to build faas-supervisor in amd64"
RUN apt update
RUN apt install -y zip build-essential zlib1g-dev libncurses5-dev autoconf libgdbm-dev libnss3-dev libssl-dev libreadline-dev libffi-dev wget libssl3 binutils  wget
RUN apt install -y python3 cmake pip
ENV LD_LIBRARY_PATH=/usr/local/lib
RUN python3 -m pip config set global.break-system-packages true
RUN python3 -m pip --no-cache-dir install pyinstaller
RUN python3 -m pip --no-cache-dir install boto3==1.20.38 \
                                            requests==2.27.1 \
                                            setuptools>=40.8.0 \
                                            pyyaml==6.0.1 \
                                            awslambdaric==2.0.12
