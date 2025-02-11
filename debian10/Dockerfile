FROM debian:10
# Add global TARGETARCH argument to this stage
ARG TARGETARCH
LABEL maintainer="Miguel Caballer <micafer1@upv.es>"
LABEL description="Container image to build faas-supervisor in amd64"
RUN echo "deb http://deb.debian.org/debian bullseye main" | tee /etc/apt/sources.list.d/bullseye.list
RUN apt update
RUN apt install binutils python3.9 python3.9-distutils python3.9-dev curl zip -y
RUN curl -sS https://bootstrap.pypa.io/get-pip.py -o get-pip.py && python3.9 get-pip.py
ENV LD_LIBRARY_PATH /usr/local/lib
RUN python3.9 -m pip --no-cache-dir install pyinstaller
RUN python3.9 -m pip --no-cache-dir install boto3==1.20.38 \
                                            requests==2.27.1 \
                                            setuptools>=40.8.0 \
                                            wheel==0.37.1 \
                                            pyyaml==6.0 \
                                            awslambdaric==2.0.12 \
                                            rucio-clients==1.31.7
