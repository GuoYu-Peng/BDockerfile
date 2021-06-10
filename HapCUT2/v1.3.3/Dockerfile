FROM ubuntu:focal-20210416

LABEL author="matthewhakka@gmail.com"
LABEL HapCUT2="V1.3.3"

WORKDIR /workspace

RUN apt-get update \
    && apt-get install -y --no-install-recommends \
	less vim curl wget build-essential zlib1g-dev libbz2-dev liblzma-dev \
	libcurl4-openssl-dev libssl-dev libhts3 \
	&& apt-get clean \
	&& rm -rf /var/lib/apt/lists/*

RUN wget --no-check-certificate https://github.com/samtools/htslib/releases/download/1.12/htslib-1.12.tar.bz2 \
    && tar -jxf htslib-1.12.tar.bz2 \
	&& cd htslib-1.12 \
	&& ./configure \
	&& make \
	&& make install \
	&& cd /workspace/ \
	&& wget --no-check-certificate https://github.com/vibansal/HapCUT2/archive/refs/tags/v1.3.3.tar.gz \
	&& tar -zxf v1.3.3.tar.gz \
	&& cd HapCUT2-1.3.3/ \
	&& make \
	&& make install \
	&& cd /workspace \
	&& rm -rf /workspace/*

VOLUME ["/data"]
CMD ["bash"]
