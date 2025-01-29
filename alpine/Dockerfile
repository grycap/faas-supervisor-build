FROM alpine:3.12
# Add global TARGETARCH argument to this stage
ARG TARGETARCH
LABEL maintainer="Miguel Caballer <micafer1@upv.es>"
LABEL description="Container image to build faas-supervisor in alpine"
RUN apk add --no-cache nghttp2-libs binutils libexecinfo-dev libcurl zip unzip cmake automake make curl-dev libtool autoconf gcc g++ zlib-dev musl-dev py3-pip python3 python3-dev libxml2-dev libxslt-dev 
RUN    python3 -m ensurepip
RUN    python3 -m pip --no-cache-dir install --upgrade pip setuptools>=40.8.0
RUN    python3 -m pip --no-cache-dir install pyinstaller 
RUN python3 -m pip install --no-deps --ignore-installed    wheel==0.37.1 
RUN apk add --no-cache --virtual .build-deps gcc musl-dev \
 && python3 -m  pip install cython \
 && apk del .build-deps
RUN python3 -m  pip --no-cache-dir install boto3==1.20.38 \
                               webdavclient3==3.14.6 \
                               requests==2.27.1 \
                               setuptools>=40.8.0 \
                               wheel==0.37.1 \
                               pyyaml==6.0.1
RUN python3 -m  pip --no-cache-dir install  awslambdaric==2.0.12

