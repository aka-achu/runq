FROM golang:latest as builder

LABEL maintainer="aka.achu.1612@gmail.com"
LABEL name="runq/redis"

ENV CGO_ENABLED 0
ENV GO111MODULE on

RUN  \
     git clone https://github.com/minio/minio && cd minio && \
     git checkout master && go install -v -ldflags "$(go run buildscripts/gen-ldflags.go)"

FROM ubuntu:20.04

ENV MINIO_UPDATE off
ENV MINIO_ACCESS_KEY_FILE=access_key \
    MINIO_SECRET_KEY_FILE=secret_key \
    MINIO_KMS_MASTER_KEY_FILE=kms_master_key \
    MINIO_SSE_MASTER_KEY_FILE=sse_master_key

EXPOSE 9000

COPY --from=builder /go/bin/minio /usr/bin/minio
COPY --from=builder /go/minio/CREDITS /third_party/
COPY --from=builder /go/minio/dockerscripts/docker-entrypoint.sh /usr/bin/

ENTRYPOINT ["/usr/bin/docker-entrypoint.sh"]
VOLUME ["/data"]
CMD ["minio"]