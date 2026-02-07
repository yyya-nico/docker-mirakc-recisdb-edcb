ARG ARCH=
FROM ${ARCH}mirakc/mirakc:debian

RUN BUILD_DEPENDENCIES="ca-certificates git build-essential cmake libpcsclite-dev pkg-config wget" && \
  apt-get update && \
  apt-get upgrade -y && \
  apt-get install -y --no-install-recommends \
    $BUILD_DEPENDENCIES \
    libpcsclite1 \
    pcscd && \
\
  ( \
  cd /tmp && \
  wget https://github.com/kazuki0824/recisdb-rs/releases/download/1.2.3/recisdb_1.2.3-1_amd64.deb && \
  apt-get install -y ./recisdb_1.2.3-1_amd64.deb \
  ) && \
\
  rm -rf /tmp/recisdb_1.2.3-1_amd64.deb && \
  apt-get remove -y $BUILD_DEPENDENCIES && \
  apt-get clean && \
  rm -rf /var/lib/apt/lists/*

ENTRYPOINT ["sh", "-c", "pcscd --disable-polkit && /usr/local/bin/mirakc"]
