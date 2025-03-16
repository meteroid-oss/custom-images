FROM quay.io/tembo/trunk:latest AS trunk
FROM ubuntu:22.04


# consider the new standard model (though barman plugin is experimental) https://github.com/cloudnative-pg/postgres-containers
FROM ghcr.io/cloudnative-pg/postgresql:17.4-5-bookworm
COPY --from=trunk /trunk /usr/bin/trunk

USER root

WORKDIR /

RUN set -eux; \
  trunk install pgmq;

RUN usermod -u 26 postgres
USER 26
