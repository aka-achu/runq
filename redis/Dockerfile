FROM ubuntu:20.04 as builder

LABEL maintainer="aka.achu.1612@gmail.com"
LABEL name="runq/redis"

ENV REDIS_VERSION 6.0.8
ENV REDIS_DOWNLOAD_URL http://download.redis.io/releases/redis-6.0.8.tar.gz

RUN apt-get update
RUN apt-get install -y --no-install-recommends \
        wget \
        make \
        gcc \
        libc6-dev \
        libssl-dev

RUN wget -O redis.tar.gz "$REDIS_DOWNLOAD_URL" --no-check-certificate; \
        mkdir -p /usr/src/redis; \
        tar -xzf redis.tar.gz -C /usr/src/redis --strip-components=1; \
        rm redis-stable.tar.gz; \
        make BUILD_TLS=yes -C /usr/src/redis -j "$(nproc)" all; \
        make -C /usr/src/redis  install



FROM ubuntu:20.04

COPY --from=builder /usr/local/bin/redis-server /usr/local/bin/

RUN apt update; \
        export DEBIAN_FRONTEND=noninteractive; \
        apt-get install -y libssl-dev; \
        rm -rf /var/lib/apt/lists/*

RUN mkdir /data /etc/redis
VOLUME [ "/data" ]
EXPOSE 6379
WORKDIR /data
COPY redis.conf /etc/redis/redis.conf

CMD ["redis-server", "/etc/redis/redis.conf"]