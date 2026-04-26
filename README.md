### Custom images

This repository builds and publishes custom images for some of Meteroid's dependencies.

## Images

All images are published to `ghcr.io/meteroid-oss/meteroid-postgres`.

### Tag convention (from 18.3+)

| Tag | Base                                | Use case |
|-----|-------------------------------------|----------|
| `{version}-standard` | `postgres:{version}` (official)     | Docker / docker-compose |
| `{version}-cnpg` | `ghcr.io/cloudnative-pg/postgresql` | Kubernetes via CNPG operator |

> **Note:** Tag `18.3` was published without a suffix before this convention was established. Use `18.3-standard` for the standard variant and `18.3-cnpg` for CNPG going forward.

### Extensions

Both variants include:
- [pgmq](https://github.com/pgmq/pgmq) — durable message queue for Postgres

The CNPG variant additionally includes everything bundled by the [CloudNativePG](https://cloudnative-pg.io) base image (pg_audit, pg_failover_slots, barman-cloud, ...).

## Publishing

Trigger the `Build and Push Docker Image` workflow manually with:
- `version`: Postgres version (e.g. `18.4`)
- `target`: `standard`, `cnpg`, or `all`
