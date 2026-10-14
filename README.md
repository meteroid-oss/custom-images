### Custom images

This repository builds and publishes custom images for some of Meteroid's dependencies.

## Images

### Postgres

Published to `ghcr.io/meteroid-oss/meteroid-postgres`.

#### Tag convention (from 18.3+)

| Tag | Base                                | Use case |
|-----|-------------------------------------|----------|
| `{version}-standard` | `postgres:{version}` (official)     | Docker / docker-compose |
| `{version}-cnpg` | `ghcr.io/cloudnative-pg/postgresql` | Kubernetes via CNPG operator |

> **Note:** Tag `18.3` was published without a suffix before this convention was established. Use `18.3-standard` for the standard variant and `18.3-cnpg` for CNPG going forward.

#### Extensions

Both variants include:
- [pgmq](https://github.com/pgmq/pgmq) — durable message queue for Postgres

The CNPG variant additionally includes everything bundled by the [CloudNativePG](https://cloudnative-pg.io) base image (pg_audit, pg_failover_slots, barman-cloud, ...).

### Smokescreen

Published to `ghcr.io/meteroid-oss/smokescreen` (`{version}` without the `v`, e.g. `0.1.0`, plus `latest`).

[Smokescreen](https://github.com/stripe/smokescreen) is Stripe's egress proxy, used to keep outbound requests (e.g. webhooks) away from internal networks. It is built from the upstream release tag on a distroless `nonroot` base and listens on `0.0.0.0:4750`.

```bash
docker run --rm -p 4750:4750 ghcr.io/meteroid-oss/smokescreen:0.1.0
```

## Publishing

### Postgres

Trigger the `Build and Push Docker Image` workflow manually with:
- `version`: Postgres version (e.g. `18.4`)
- `target`: `standard`, `cnpg`, or `all`

### Smokescreen

Pushes to `main` touching `smokescreen/` build the default version pinned in the workflow and tag it `latest`. To publish another release, trigger the `Build and Push Smokescreen Image` workflow with `version` set to an upstream tag (e.g. `v0.1.0`).
