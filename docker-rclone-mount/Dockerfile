ARG BASE=alpine:3.12.3
FROM ${BASE}

ARG RCLONE_VERSION="v1.53.3"
ARG OVERLAY_VERSION="v2.1.0.2"
ARG OVERLAY_ARCH="amd64"

ENV DEBUG="false" \
    GOPATH="/go" \
    # https://dev.to/maelvls/why-is-go111module-everywhere-and-everything-about-go-modules-24k
    GO111MODULE="on"

ENV REMOTE_PATH="mediaefs:" \
    MOUNT_PATH="/mnt/mediaefs" \
    CONFIG_PATH="/config" \
    CONFIG_FILE="rclone.conf" \
    MOUNT_COMMANDS="--allow-other --allow-non-empty" \
    UNMOUNT_COMMANDS="-u -z"

## Alpine with Go Git
RUN apk --no-cache upgrade \
    && apk add --no-cache --update alpine-sdk ca-certificates go git fuse fuse-dev gnupg \
    && echo "Installing S6 Overlay" \
    && curl -o /tmp/s6-overlay.tar.gz -L \
    "https://github.com/just-containers/s6-overlay/releases/download/${OVERLAY_VERSION}/s6-overlay-${OVERLAY_ARCH}.tar.gz" \
    && curl -o /tmp/s6-overlay.tar.gz.sig -L \
    "https://github.com/just-containers/s6-overlay/releases/download/${OVERLAY_VERSION}/s6-overlay-${OVERLAY_ARCH}.tar.gz.sig" \
    && curl https://keybase.io/justcontainers/key.asc | gpg --import \
    && gpg --verify /tmp/s6-overlay.tar.gz.sig /tmp/s6-overlay.tar.gz \
    && tar xfz /tmp/s6-overlay.tar.gz -C / \
    && echo "Download and compile rclone" \
    && go get -v github.com/rclone/rclone@${RCLONE_VERSION} \
    && cp ${GOPATH}/bin/rclone /usr/sbin/ \
    && rm -rf ${GOPATH} || true \
    && apk del alpine-sdk go git gnupg \
    && rm -rf /tmp/* /var/cache/apk/* /var/lib/apk/lists/*

COPY rootfs/ /

VOLUME ["/mnt"]

ENTRYPOINT ["/init"]
