# Base image
FROM buildpack-deps:xenial-curl
ENV INFER_VERSION=v0.10.0

MAINTAINER Infer

# Debian config
RUN apt-get update && \
    apt-get install -y --no-install-recommends \
            aspcud \
            autoconf \
            gcc \
            g++ \
            git \
            groff-base \
            gradle \
            libc6-dev \
            libffi-dev \
            libgmp-dev \
            libmpc-dev \
            libmpfr-dev \
            m4 \
            make \
            maven \
            ncurses-dev \
            ocaml \
            opam \
            openjdk-8-jdk-headless \
            pkg-config \
            python2.7 \
            rsync \
            unzip \
            zlib1g-dev && \
    rm -rf /var/lib/apt/lists/*

# Download the latest Infer release
RUN cd /opt && \
    curl -sL \
      https://github.com/facebook/infer/releases/download/${INFER_VERSION}/infer-linux64-${INFER_VERSION}.tar.xz | \
    tar xJ && \
    rm -f /infer && \
    ln -s ${PWD}/infer-linux64-$INFER_VERSION /infer

# Compile Infer
RUN cd /infer && \
    ./build-infer.sh && \
    rm -rf /root/.opam

# Install Infer
ENV INFER_HOME /infer/infer
ENV PATH ${INFER_HOME}/bin:${PATH}

# Install dependencies for Android sample
RUN apt-get update && \
    apt-get install -y --no-install-recommends \
            libc6-dev \
            libc6-i386 \
            lib32z1 \
            lib32stdc++6 && \
    rm -rf /var/lib/apt/lists/*

ENV ANDROID_HOME /opt/android-sdk-linux
RUN mkdir -p /opt/android-sdk-linux/licenses
RUN echo -e "\n8933bad161af4178b1185d1a37fbf41ea5269c55" > ${ANDROID_HOME}/licenses/android-sdk-license
RUN echo "sdk.dir=${ANDROID_HOME}" > /infer/examples/android_hello/local.properties

WORKDIR /usr/workdir/src
