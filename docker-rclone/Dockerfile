ARG BASE=alpine:3.12.3
FROM ${BASE}

ARG BUILD_DATE
ARG VCS_REF
ARG GO_PATH="/go"
ARG RCLONE_VERSION="v1.53.3"
ARG RCLONE_BASE_PATH="/rclone"
ARG RCLONE_BIN_PATH="${RCLONE_BASE_PATH}/bin"
ARG RCLONE_CONFIG_PATH="${RCLONE_BASE_PATH}/config"
ARG RCLONE_CONFIG_FILE="rclone.conf"

ENV RCLONE_OPTS="--config ${RCLONE_CONFIG_PATH}/${RCLONE_CONFIG_FILE}" \
    RCLONE_BASE_PATH="${RCLONE_BASE_PATH}" \
    RCLONE_BIN_PATH="${RCLONE_BIN_PATH}" \
    RCLONE_CONFIG_PATH="${RCLONE_CONFIG_PATH}" \
    RCLONE_CONFIG_FILE="${RCLONE_CONFIG_FILE}"

LABEL \
    org.opencontainers.image.authors="bas@vanwetten.com" \
    org.opencontainers.image.created=$BUILD_DATE \
    org.opencontainers.image.revision=$VCS_REF \
    org.opencontainers.image.version=$RCLONE_VERSION \
    org.opencontainers.image.url="https://github.com/QNimbus/docker-rclone/tree/main/docker-rclone" \
    org.opencontainers.image.documentation="https://github.com/QNimbus/docker-rclone/blob/main/docker-rclone/README.md" \
    org.opencontainers.image.source="https://github.com/QNimbus/docker-rclone/tree/main/docker-rclone" \
    org.opencontainers.image.title="docker-rclone" \
    org.opencontainers.image.description="Rclone syncs your files to cloud storage"

RUN mkdir -p "${RCLONE_BIN_PATH}" "${RCLONE_CONFIG_PATH}"

RUN export GOPATH=$GO_PATH && \
    export GO111MODULE="on" && \
    apk --no-cache upgrade && \
    apk add --no-cache --update alpine-sdk ca-certificates go git fuse fuse-dev gnupg && \
    echo "Download and compile rclone" && \
    go get -v github.com/rclone/rclone@${RCLONE_VERSION} && \
    cp ${GO_PATH}/bin/rclone ${RCLONE_BIN_PATH} && \
    rm -rf ${GO_PATH} && \
    apk del alpine-sdk go git gnupg && \
    rm -rf /tmp/* /var/cache/apk/* /var/lib/apk/lists/* && \
    unset GO111MODULE && \
    unset GOPATH

COPY init /

VOLUME ["${RCLONE_CONFIG_PATH}"]

ENTRYPOINT ["/init"]
