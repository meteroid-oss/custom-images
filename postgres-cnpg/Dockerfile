ARG POSTGRESQL_VERSION=17.4-5-bookworm
ARG PGMQ_VERSION=1.5.0

# consider the new standard model (though barman plugin is experimental) https://github.com/cloudnative-pg/postgres-containers
FROM ghcr.io/cloudnative-pg/postgresql:${POSTGRESQL_VERSION} AS base

# trunk doesn't support arm
FROM base AS builder
USER root
RUN apt-get update && apt-get install --no-install-recommends --yes \
    make=4.* \
    && rm -r /var/lib/apt/lists/*
WORKDIR /build
ARG PGMQ_VERSION
ADD https://github.com/tembo-io/pgmq.git#v${PGMQ_VERSION}:pgmq-extension ./
RUN make && make install

FROM base
COPY --from=builder /usr/share/postgresql /usr/share/postgresql/