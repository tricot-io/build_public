# Copyright 2019 Tricot Inc.
# Use of this source code is governed by the license in the LICENSE file.

# The version of the upstream image. E.g., 1.11.5 for circleci/golang:1.11.5-node.
UPSTREAM_VERSION=1.12.6

# The version of bazel.
BAZEL_VERSION=0.27.0

# Use this to detect changes in the Dockerfile and tag it appropriately.
DOCKERFILE_CRC32=$(shell crc32 Dockerfile)

DOCKER_TAG=tricot/build-public-circleci:$(UPSTREAM_VERSION)-$(BAZEL_VERSION)-$(DOCKERFILE_CRC32)

all: build

info:
	@echo "TAG IS: $(DOCKER_TAG)"

build: info
	docker build --build-arg UPSTREAM_VERSION=$(UPSTREAM_VERSION) \
		--build-arg BAZEL_VERSION=$(BAZEL_VERSION) \
		-t $(DOCKER_TAG) .

push: build
	docker push $(DOCKER_TAG)
