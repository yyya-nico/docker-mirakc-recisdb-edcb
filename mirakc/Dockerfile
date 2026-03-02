ARG ARCH=
FROM ${ARCH}mirakc/mirakc:debian

RUN BUILD_DEPENDENCIES="wget curl" && \
    apt update && \
    apt install -y --no-install-recommends \
    $BUILD_DEPENDENCIES \
    pcscd && \
\
    ( \
        cd /tmp && \
        wget https://github.com/kazuki0824/recisdb-rs/releases/download/1.2.4/recisdb_1.2.4-1_amd64.deb && \
        apt install -y ./recisdb_1.2.4-1_amd64.deb \
    ) && \
\
    ( \
        mkdir -p /var/www/mira-tuners && \
        cd /var/www/mira-tuners && \
        curl -L https://github.com/yyya-nico/mira-tuners/releases/download/v1.0.3/build.tar.gz | tar -zxvf - \
    ) && \
\
    rm -rf /tmp/recisdb_1.2.4-1_amd64.deb && \
    apt remove -y $BUILD_DEPENDENCIES && \
    apt clean && \
    rm -rf /var/lib/apt/lists/*

# polkitを無効としてpcscdを起動しないとスマートカードが読めない
# ref:https://github.com/LudovicRousseau/PCSC/issues/59#issuecomment-2633517579
ENTRYPOINT ["sh", "-c", "pcscd --disable-polkit && mirakc"]
CMD []