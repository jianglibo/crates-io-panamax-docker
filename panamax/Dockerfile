FROM rust

WORKDIR /

RUN set -eux; \
    cargo install panamax; \
    panamax init my-mirror
ADD mirror.toml my-mirror
# line bellow will cause disk space full.
# RUN panamax sync my-mirror
CMD [ "panamax", "sync", "my-mirror" ]