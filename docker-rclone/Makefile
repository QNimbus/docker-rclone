#Dockerfile vars
alpine_version=3.12.3
rclone_version=1.53.3

#vars
IMAGENAME=rclone
REPO=qnimbus
IMAGEFULLNAME=${REPO}/${IMAGENAME}

.PHONY: help build push all

help:
	@echo "Makefile arguments:"
	@echo ""
	@echo "alpine_version - Alpine version"
	@echo "rclone_version - RClone version"
	@echo ""
	@echo "Makefile commands:"
	@echo "build"
	@echo "push"
	@echo "all"

.DEFAULT_GOAL := all

build:
	@docker build \
	--build-arg BASE="alpine:${alpine_version}" \
	--build-arg VCS_REF=`git rev-parse --short HEAD` \
	--build-arg BUILD_DATE=`date -u +"%Y-%m-%dT%H:%M:%SZ"` \
	--build-arg RCLONE_VERSION="v${rclone_version}" \
	--build-arg RCLONE_BASE_PATH="/rclone" \
	--build-arg RCLONE_CONFIG_FILE="rclone.conf" \
	-t ${IMAGEFULLNAME} .

push:
	@docker push ${IMAGEFULLNAME}

all: build push
