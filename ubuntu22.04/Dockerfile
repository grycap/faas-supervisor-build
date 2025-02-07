FROM ubuntu:22.04
# Add global TARGETARCH argument to this stage
ARG TARGETARCH
LABEL maintainer="Miguel Caballer <micafer1@upv.es>"
LABEL description="Container image to build faas-supervisor in amd64"
RUN apt update
RUN apt install -y libboost-python-dev cmake make gcc libgfal2-dev gfal2 python3 python3-pip && \
    pip install --no-deps --ignore-installed gfal2-python==1.11.0-post3 && \
    apt remove -y gcc cmake make libboost-python-dev libgfal2-dev
ENV LD_LIBRARY_PATH=/usr/local/lib
RUN pip config set global.break-system-packages true
RUN pip --no-cache-dir install pyinstaller
RUN pip install --no-cache-dir boto3==1.20.38 \
                                requests==2.32.3 \
                                setuptools>=40.8.0 \
                                wheel==0.37.1 \
                                pyyaml==6.0.1 \
                                awslambdaric==2.0.12 \
                                rucio-clients==36.2.0
