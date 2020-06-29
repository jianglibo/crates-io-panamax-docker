FROM rust

WORKDIR /

RUN set -eux; \
    cargo install panamax; \
    panamax init my-mirror
ADD ./panamax/mirror.toml my-mirror
RUN panamax sync my-mirror
