FROM ekidd/rust-musl-builder:latest as build

COPY --chown=rust:rust Cargo.toml Cargo.lock ./
RUN cargo build --release || true

COPY --chown=rust:rust . ./
RUN cargo build --release

FROM scratch

COPY --from=build \
    /home/rust/src/target/x86_64-unknown-linux-musl/release/auth .
EXPOSE ${PORT}
CMD ["./auth"]