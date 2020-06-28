FROM rust
RUN set -eux; \
    cargo install panamax; \
    panamax init my-mirror; \
    panamax sync my-mirror
