ARG POSTGRESQL_VERSION=18
ARG PGMQ_VERSION

FROM postgres:${POSTGRESQL_VERSION} AS builder
USER root
RUN apt-get update && apt-get install --no-install-recommends --yes \
    make=4.* \
    && rm -r /var/lib/apt/lists/*
WORKDIR /build
ADD https://github.com/pgmq/pgmq.git#v${PGMQ_VERSION}:pgmq-extension ./
RUN make && make install

FROM postgres:${POSTGRESQL_VERSION}
COPY --from=builder /usr/share/postgresql /usr/share/postgresql/
