# Copyright 2019 Tricot Inc.
# Use of this source code is governed by the license in the LICENSE file.

ARG UPSTREAM_VERSION
FROM circleci/golang:${UPSTREAM_VERSION}-node

USER root
RUN apt-get update
RUN apt-get install -y curl g++ git ocl-icd-opencl-dev pkg-config python unzip zip zlib1g-dev
ARG BAZEL_VERSION
RUN curl -O -L https://github.com/bazelbuild/bazel/releases/download/${BAZEL_VERSION}/bazel-${BAZEL_VERSION}-installer-linux-x86_64.sh
RUN bash bazel-${BAZEL_VERSION}-installer-linux-x86_64.sh
RUN rm bazel-${BAZEL_VERSION}-installer-linux-x86_64.sh

USER circleci
