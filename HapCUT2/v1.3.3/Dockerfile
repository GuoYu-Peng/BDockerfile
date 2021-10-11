FROM ubuntu:focal-20210416

LABEL author="matthewhakka@gmail.com"
LABEL HapCUT2="V1.3.3"

ARG USER_ID
ARG GROUP_ID
ARG USER_NAME

WORKDIR /app

# libffi-dev libssl-dev for python install.
RUN apt-get update \
    && apt-get install -y --no-install-recommends \
	less vim curl wget build-essential zlib1g-dev libbz2-dev liblzma-dev \
	libcurl4-openssl-dev libssl-dev libhts3 libffi-dev libssl-dev \
	&& apt-get clean \
	&& rm -rf /var/lib/apt/lists/*

RUN wget --no-check-certificate https://github.com/samtools/htslib/releases/download/1.12/htslib-1.12.tar.bz2 \
    && tar -jxf htslib-1.12.tar.bz2 \
	&& cd htslib-1.12 \
	&& ./configure \
	&& make \
	&& make install \
	&& cd /app \
	&& rm -rf htslib-1.12 htslib-1.12.tar.bz2 


RUN wget --no-check-certificate https://www.python.org/ftp/python/3.10.0/Python-3.10.0.tgz \
	&& tar -zxf Python-3.10.0.tgz \
	&& cd Python-3.10.0 \
	&& ./configure \
	&& make \
	&& make install \
	&& cd /app \
	&& rm -rf Python-3.10.0 Python-3.10.0.tgz 

RUN wget --no-check-certificate https://github.com/vibansal/HapCUT2/archive/refs/tags/v1.3.3.tar.gz \
	&& tar -zxf v1.3.3.tar.gz \
	&& cd HapCUT2-1.3.3/ \
	&& make \
	&& make install \
	&& cd /app \
	&& rm -rf v1.3.3.tar.gz 

RUN pip3 install pysam

RUN groupadd -r --gid ${GROUP_ID} ${USER_NAME} && useradd --no-log-init -r -g ${GROUP_ID} -u ${USER_ID} ${USER_NAME}
USER ${USER_NAME}

WORKDIR /work

VOLUME ["/data"]
CMD ["bash"]
