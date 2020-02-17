# Copyright 2019 Tricot Inc.
# Use of this source code is governed by the license in the LICENSE file.

# The version of the image (in the tag).
# * Increase this whenever one or more of the dependencies is updated.
# * Increase the field corresponding to the field in the updated dependency (resetting lesser fields
#   to 0). If multiple dependencies are updated, increase the greatest field.
# * Use standard guidelines (major.minor.patch) for other Dockerfile changes.
DOCKER_TAG_VERSION=2.1.1

# The version of the upstream image. E.g., 1.11.5 for circleci/golang:1.11.5-node.
UPSTREAM_VERSION=1.13.8-stretch

# The version of Bazel.
BAZEL_VERSION=2.1.0

# The version of CMake.
CMAKE_VERSION=3.16.4

# The git revision for tricot-io/tools_public.
TRICOT_TOOLS_PUBLIC_REV=e635d202370a866341f9ca429744a27a4725168a

DOCKER_TAG=tricot/build-public-circleci:$(DOCKER_TAG_VERSION)

all: build

info:
	@echo "TAG IS: $(DOCKER_TAG)"

build: info
	docker build --build-arg UPSTREAM_VERSION=$(UPSTREAM_VERSION) \
		--build-arg BAZEL_VERSION=$(BAZEL_VERSION) \
		--build-arg CMAKE_VERSION=$(CMAKE_VERSION) \
		--build-arg TRICOT_TOOLS_PUBLIC_REV=$(TRICOT_TOOLS_PUBLIC_REV) \
		-t $(DOCKER_TAG) .

push: build
	docker push $(DOCKER_TAG)
