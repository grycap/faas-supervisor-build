FROM alpine:3.16
# Add global TARGETARCH argument to this stage
ARG TARGETARCH
LABEL maintainer="Miguel Caballer <micafer1@upv.es>"
LABEL description="Container image to build faas-supervisor in alpine"
#RUN apk add --no-cache nghttp2-libs binutils libexecinfo-dev libcurl zip unzip cmake automake make curl-dev libtool autoconf gcc g++ zlib-dev musl-dev py3-pip python3 python3-dev libxml2-dev libxslt-dev 
RUN apk add --no-cache python3 python3-dev autoconf libcurl curl zip unzip cmake make automake curl-dev libtool autoconf gcc g++ libexecinfo-dev
RUN python3 -m ensurepip
RUN pip3 --no-cache-dir install --upgrade pip setuptools>=40.8.0
RUN pip3 --no-cache-dir install pyinstaller 
RUN pip3 install --no-deps --ignore-installed    wheel==0.37.1 
RUN apk add --no-cache --virtual .build-deps gcc musl-dev \
 && pip3 install cython \
 && apk del .build-deps
RUN pip3 --no-cache-dir install boto3==1.20.38 \
                               webdavclient3==3.14.6 \
                               requests==2.27.1 \
                               setuptools>=40.8.0 \
                               wheel==0.37.1 \
                               pyyaml==6.0.1 \
                               awslambdaric==2.0.12 \
                               rucio-clients==1.31.7
