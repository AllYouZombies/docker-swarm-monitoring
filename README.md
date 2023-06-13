# Docker Swarm Monitoring Stack

This is a docker stack for monitoring a docker swarm cluster.
It uses [Prometheus](https://prometheus.io/) for metrics collection,
[Grafana](https://grafana.com/) for visualization,
[cAdvisor](https://github.com/google/cadvisor) for container metrics,
[Node Exporter](https://github.com/prometheus/node_exporter) for host metrics.

## Usage

### Prerequisites

* Docker Swarm cluster
* Traefik reverse proxy
* Domain name with DNS records pointing to the Traefik server
  * `monitoring.example.com`
  * `monitoring-prometheus.example.com`
  * or wildcard `*.example.com`

### Deploy

Create a docker config for Prometheus:

```shell
docker config create prometheus.yml prometheus.yml
```

Create an `.env` file with the following variables:

```shell
# Domain name for the monitoring stack
DOMAIN=example.com
# Stack name (needed for traefik labels)
STACK_NAME=monitoring
# Prometheus username
PROMETHEUS_USERNAME=admin
# Prometheus password (use `openssl passwd -apr1` to generate a hash)
PROMETHEUS_PASSWORD=$apr1$wnfYXqyI$2q.l9IxP.oGYP1j8Do9580
```

Deploy the stack:

```shell
docker stack deploy -c prometheus-stack.yml monitoring
```

### Access

* Grafana: `https://monitoring.example.com`
* Prometheus: `https://monitoring-prometheus.example.com`
