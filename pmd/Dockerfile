FROM java:8-jdk-alpine
ENV PMD_VERSION=5.5.5

WORKDIR /usr/workdir
RUN apk add --update \
    bash \
    curl \
    unzip \
    && rm -rf /var/cache/apk/*


# Download the latest pmd release
RUN curl -sLO \
      https://github.com/pmd/pmd/releases/download/pmd_releases%2F${PMD_VERSION}/pmd-bin-${PMD_VERSION}.zip && \
    unzip pmd-bin-*.zip && \
    rm pmd-bin-*.zip && \
    mv pmd-bin-* pmd-bin 

WORKDIR /usr/workdir/src
