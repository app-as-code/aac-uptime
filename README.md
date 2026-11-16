<p align="center">
  <picture>
    <source media="(prefers-color-scheme: dark)" srcset="assets/icon-dark.svg">
    <img src="assets/icon.svg" alt="Uptime Kuma logo" width="128">
  </picture>
</p>

<h1 align="center">aac-uptime</h1>

<p align="center">Self-hosted deployment definition for Uptime Kuma, a self-hosted monitoring tool.</p>

<p align="center">
  <a href="https://github.com/louislam/uptime-kuma"><img alt="Upstream" src="https://img.shields.io/badge/upstream-louislam%2Fuptime--kuma-blue?logo=github"></a>
  <img alt="Image" src="https://img.shields.io/badge/image-louislam%2Fuptime--kuma%3Anightly2-2496ED?logo=docker&logoColor=white">
  <a href="https://github.com/louislam/uptime-kuma/blob/master/LICENSE"><img alt="License" src="https://img.shields.io/badge/license-MIT-green"></a>
</p>

## About

Uptime Kuma is a self-hosted monitoring tool that checks the availability of websites,
services and hosts and shows the results on a web dashboard. It can alert you when a
monitored target goes down or recovers, so you notice outages before users report them.

Key features (as provided by upstream):

- Monitors for HTTP(s), TCP, ping, DNS and many other check types
- Status pages for publishing service availability
- Notifications through a wide range of services
- Certificate expiry checks and response-time history
- Simple web-based setup with no external database required

## Upstream

- Project: <https://github.com/louislam/uptime-kuma>
- Documentation: <https://github.com/louislam/uptime-kuma/wiki>
- Container image: `louislam/uptime-kuma:nightly2` (Docker Hub)
- License: MIT (upstream project)

## Quick start (Docker Compose)

The Compose file is rendered from `service.yml` by the App-as-Code template engine. For a
manual run, the external networks used for routing must exist first:

```bash
docker network create services-secured
docker network create services-exposed

docker compose up -d
```

The application is available on the web port (`3001` inside the container). No secrets are
required for the default configuration.

## Configuration

Environment variables (defaults from `service.yml`):

| Variable | Default | Description |
|---|---|---|
| `HOMEPAGE_WIDGET_SLUG` | `status` | Slug used for the Homepage dashboard widget label |
| `PUID` | `1000` | User ID value passed to the container |
| `PGID` | `1000` | Group ID value passed to the container |
| `TZ` | `Europe/Berlin` | Time zone |

Ports:

| Port | Protocol | Purpose |
|---|---|---|
| `3001` | TCP | Web interface (`web`) |

Volumes:

| Mount | Description |
|---|---|
| `data` -> `/app/data` | Uptime Kuma persistent data storage (database and settings) |

## Deploy with App-as-Code

1. Edit `service.yml`. It is the single source of truth for image, ports, environment,
   volumes and per-stage overrides. Do not edit the rendered output.
2. Pushing to `main` (or a configured stage branch) runs the service pipeline, which renders
   the manifests with `aac-template-engine` and triggers the deployment.
3. Releases of this definition are published under <https://github.com/app-as-code/aac-uptime>.

## Credits and license

Uptime Kuma is developed by Louis Lam and contributors and licensed under the MIT License.
This repository only contains the deployment definition for it and is not a fork of the
application. The logo is provided by the Uptime Kuma project; see
[`assets/ICON_SOURCE.md`](assets/ICON_SOURCE.md) for icon sources and licenses.
