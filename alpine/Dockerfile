FROM alpine:3.12
LABEL maintainer="Miguel Caballer <micafer1@upv.es>"
LABEL description="Container image to build faas-supervisor in alpine"
RUN apk add --no-cache binutils libexecinfo-dev libcurl zip unzip cmake automake make curl-dev libtool autoconf gcc g++ zlib-dev musl-dev py3-pip python3 python3-dev && \
    python3 -m ensurepip && \
    pip --no-cache-dir install pyinstaller  && \
    pip --no-cache-dir install boto3==1.20.38 \
                               requests==2.27.1 \
                               setuptools>=40.8.0 \
                               wheel==0.37.1 \
                               pyyaml==6.0 \
                               awslambdaric==2.0.1 && \
    apk del libexecinfo-dev libcurl cmake automake make curl-dev libtool autoconf gcc g++ zlib-dev musl-dev python3-dev
