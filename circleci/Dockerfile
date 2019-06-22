# Copyright 2019 Tricot Inc.
# Use of this source code is governed by the license in the LICENSE file.

# Start with the CircleCI golang (+ node) convenience image.
ARG UPSTREAM_VERSION
FROM circleci/golang:${UPSTREAM_VERSION}-node

USER root

# Packages from distribution:
RUN apt-get update
RUN apt-get install -y \
        curl \
        g++ \
        gawk \
        git \
        ocl-icd-opencl-dev \
        pkg-config \
        python \
        python3 \
        python3-requests \
        python-pip \
        unzip \
        zip \
        zlib1g-dev

# Bazel:
ARG BAZEL_VERSION
RUN curl -O -L https://github.com/bazelbuild/bazel/releases/download/${BAZEL_VERSION}/bazel-${BAZEL_VERSION}-installer-linux-x86_64.sh
RUN bash bazel-${BAZEL_VERSION}-installer-linux-x86_64.sh
RUN rm bazel-${BAZEL_VERSION}-installer-linux-x86_64.sh

# Buildifier:
# TODO(vtl): Version?
RUN go get github.com/bazelbuild/buildtools/buildifier

USER circleci

# Make ~/bin and add it to our path.
RUN mkdir ${HOME}/bin
# TODO(vtl): Can we reasonably do this without hard-coding our home directory?
ENV PATH="/home/circleci/bin:${PATH}"

# CMake:
ARG CMAKE_VERSION
RUN curl -O -L https://github.com/Kitware/CMake/releases/download/v${CMAKE_VERSION}/cmake-${CMAKE_VERSION}-Linux-x86_64.tar.gz
RUN tar xfC cmake-${CMAKE_VERSION}-Linux-x86_64.tar.gz ${HOME}
RUN rm cmake-${CMAKE_VERSION}-Linux-x86_64.tar.gz
RUN ln -s ${HOME}/cmake-${CMAKE_VERSION}-Linux-x86_64/bin/* ${HOME}/bin

# tricot-io/tools_public:
ARG TRICOT_TOOLS_PUBLIC_REV
RUN git -C ${HOME} clone -n -q https://github.com/tricot-io/tools_public.git tools_public
RUN git -C ${HOME}/tools_public checkout -q ${TRICOT_TOOLS_PUBLIC_REV}
RUN ln -s ${HOME}/tools_public/*.sh ${HOME}/tools_public/*.py ${HOME}/bin
