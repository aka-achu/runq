FROM ubuntu:18.04 as builder

LABEL maintainer="aka.achu.1612@gmail.com"
LABEL name="imgclub/redis"
LABEL vcs-url="https://github.com/aka-achu/imgclub"
LABEL version=$6.0.5

RUN apt-get update
RUN apt-get install -y --no-install-recommends \
        wget \
        make \
        gcc \
        libc6-dev

RUN wget http://download.redis.io/redis-stable.tar.gz; \
        mkdir -p /usr/src/redis; \
        tar -xzf redis-stable.tar.gz -C /usr/src/redis --strip-components=1; \
        rm redis-stable.tar.gz; \
        make -C /usr/src/redis -j "$(nproc)" all; \
        make -C /usr/src/redis  install



FROM ubuntu:18.04

COPY --from=builder /usr/local/bin/redis-server /usr/local/bin/

EXPOSE 6379
WORKDIR /data
COPY redis.conf ./redis.conf


CMD ["redis-server", "/data/redis.conf"]