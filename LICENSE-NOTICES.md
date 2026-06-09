# License Notices

This repository contains configuration files for the NextMonitor-Core observability stack.

NextMonitor-Core uses third-party open-source software. Each component keeps its own license and copyright.

## Components

| Component | Project | License note |
|---|---|---|
| Prometheus | https://github.com/prometheus/prometheus | Apache License 2.0 |
| Grafana OSS | https://github.com/grafana/grafana | AGPLv3 for recent Grafana OSS releases |
| Loki | https://github.com/grafana/loki | AGPLv3 for recent Grafana Loki releases |
| Promtail | https://github.com/grafana/loki | AGPLv3 for recent Grafana Loki/Promtail releases |
| OpenTelemetry Collector Contrib | https://github.com/open-telemetry/opentelemetry-collector-contrib | Apache License 2.0 |
| Uptime Kuma | https://github.com/louislam/uptime-kuma | MIT License |

## Important note

This repository does not relicense third-party software. Container images and upstream projects are used under their own licenses.

If any third-party source code is modified or redistributed, the relevant upstream license obligations must be reviewed before production distribution.

For institutional or public deployments, keep this file updated and include upstream license files where required.
