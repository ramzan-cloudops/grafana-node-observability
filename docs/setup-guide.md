# Setup Guide

This document provides step-by-step instructions for deploying and configuring the Grafana Node Observability Dashboard.

---

# Prerequisites

Before starting, ensure the following requirements are available:

- Linux Server (Ubuntu Recommended)
- Docker Installed
- Docker Compose Installed
- Internet Connectivity
- Ports Opened in Security Group

Required ports:

| Service | Port |
|----------|----------|
| Grafana | 3000 |
| Prometheus | 9090 |
| Loki | 3100 |
| Node Exporter | 9100 |

---

# Project Structure

```text
grafana-node-observability/

├── docker-compose.yml
├── prometheus/
├── loki/
├── promtail/
├── dashboards/
├── screenshots/
├── docs/
└── architecture/
```

---

# Clone Repository

```bash
git clone <repository-url>
cd grafana-node-observability
```

---

# Verify Docker Installation

Check Docker version:

```bash
docker --version
```

Check Docker Compose version:

```bash
docker compose version
```

---

# Start Monitoring Stack

Launch all monitoring services:

```bash
docker compose up -d
```

Verify containers:

```bash
docker ps
```

Expected containers:

- grafana
- prometheus
- node-exporter
- loki
- promtail

---

# Access Services

## Grafana

```text
http://<SERVER-IP>:3000
```

## Prometheus

```text
http://<SERVER-IP>:9090
```

## Loki

```text
http://<SERVER-IP>:3100
```

---

# Configure Prometheus Data Source

1. Login to Grafana
2. Navigate to:

```text
Connections → Data Sources
```

3. Select:

```text
Prometheus
```

4. Configure URL:

```text
http://prometheus:9090
```

5. Click:

```text
Save & Test
```

Successful message:

```text
Successfully queried the Prometheus API
```

---

# Configure Loki Data Source

1. Navigate to:

```text
Connections → Data Sources
```

2. Add:

```text
Loki
```

3. Configure URL:

```text
http://loki:3100
```

4. Click:

```text
Save & Test
```

---

# Import Dashboard

1. Open Grafana
2. Navigate to:

```text
Dashboards → Import
```

3. Upload:

```text
dashboards/node-monitoring-dashboard.json
```

4. Select data sources
5. Complete import

---

# Dashboard Metrics

The dashboard includes monitoring for:

## CPU Utilization

Tracks processor usage percentage.

## Memory Utilization

Monitors RAM consumption and available memory.

## Disk Utilization

Displays storage capacity and usage statistics.

## Network Utilization

Tracks incoming and outgoing network traffic.

## Log Monitoring

Displays centralized system logs collected through Promtail and stored in Loki.

---

# Log Monitoring

Logs are collected using:

```text
Promtail → Loki → Grafana
```

Log dashboard capabilities:

- Recent System Logs
- Centralized Log Visibility
- Operational Troubleshooting
- Infrastructure Monitoring

---

# Verify Metrics Collection

Open Explore in Grafana and verify metrics:

CPU:

```promql
100 - (avg by(instance) (rate(node_cpu_seconds_total{mode="idle"}[5m])) * 100)
```

Memory:

```promql
100 * (1 - (node_memory_MemAvailable_bytes / node_memory_MemTotal_bytes))
```

Network Receive:

```promql
rate(node_network_receive_bytes_total[5m])
```

Network Transmit:

```promql
rate(node_network_transmit_bytes_total[5m])
```

---

# Verify Log Collection

Use the Loki query:

```logql
{job=~".+"}
```

Expected result:

```text
Recent system logs displayed in Grafana
```

---

# Stop Services

```bash
docker compose down
```

---

# Restart Services

```bash
docker compose restart
```

---

# Future Expansion

This dashboard can be extended to support:

- Multiple Nodes
- Kubernetes Clusters
- AlertManager Integration
- Email Notifications
- Slack Notifications
- Cloud Infrastructure Monitoring

---

# Troubleshooting

## Container Health

Check running containers:

```bash
docker ps
```

Container logs:

```bash
docker logs grafana
docker logs prometheus
docker logs loki
docker logs promtail
```

---

# Outcome

Following this guide will deploy a complete observability stack consisting of Grafana, Prometheus, Node Exporter, Loki, and Promtail, providing reusable infrastructure monitoring and centralized log management 
