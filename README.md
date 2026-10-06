# Grafana Node Observability Dashboard

A reusable Grafana-based observability solution for monitoring node health, infrastructure metrics, and system logs using Prometheus, Node Exporter, Loki, and Promtail.

## Project Overview

This project provides a standardized and reusable Grafana dashboard template for monitoring Linux nodes and servers. The dashboard collects and visualizes infrastructure metrics while also providing centralized log monitoring capabilities.

The solution was built as a proof-of-concept (POC) and can be extended to monitor multiple nodes in future deployments.

---

## Objectives

- Create a reusable Grafana dashboard template
- Monitor node-level metrics
- Integrate centralized log monitoring
- Provide deployment and setup documentation
- Enable future scalability for additional nodes

---

## Technology Stack

### Visualization

- Grafana

### Metrics Collection

- Prometheus
- Node Exporter

### Log Monitoring

- Loki
- Promtail

### Deployment

- Docker
- Docker Compose

---

## Architecture

```text
+--------------------+
|    Node Exporter   |
+---------+----------+
          |
          v
+--------------------+
|    Prometheus      |
+---------+----------+
          |
          v
+--------------------+
|      Grafana       |
+--------------------+

System Logs
     |
     v
+--------------------+
|     Promtail       |
+---------+----------+
          |
          v
+--------------------+
|       Loki         |
+---------+----------+
          |
          v
+--------------------+
|      Grafana       |
+--------------------+
```

Architecture diagram:

```text
architecture/architecture.png
```

---

## Dashboard Features

### Infrastructure Monitoring

The dashboard provides visibility into the following node metrics:

- CPU Utilization
- Memory Utilization
- Disk Utilization
- Network Receive Traffic
- Network Transmit Traffic

### Log Monitoring

The dashboard integrates Loki for centralized log collection and visualization.

Features include:

- Recent System Logs
- Log Exploration
- Centralized Log Visibility
- Troubleshooting Support

---

## Dashboard Panels

### CPU Usage

Monitors processor utilization in real time.

### Memory Usage

Tracks RAM consumption and available memory.

### Disk Usage

Provides storage utilization insights.

### Network Receive

Displays incoming network traffic.

### Network Transmit

Displays outgoing network traffic.

### Recent System Logs

Provides log visibility using Loki and Promtail.

---

## Repository Structure

```text
grafana-node-observability/

├── README.md
├── docker-compose.yml

├── dashboards/
│   └── node-monitoring-dashboard.json

├── prometheus/
│   └── prometheus.yml

├── loki/
│   └── local-config.yaml

├── promtail/
│   └── promtail-config.yaml

├── screenshots/
│   ├── dashboard-overview.png
│   ├── cpu-metrics.png
│   ├── memory-metrics.png
│   ├── disk-metrics.png
│   └── logs-view.png

├── docs/
│   └── setup-guide.md

└── architecture/
    └── architecture.png
```

---

## Deployment

Start the monitoring stack:

```bash
docker compose up -d
```

Verify running containers:

```bash
docker ps
```

Expected services:

- Grafana
- Prometheus
- Node Exporter
- Loki
- Promtail

---

## Access URLs

### Grafana

```text
http://<SERVER-IP>:3000
```

### Prometheus

```text
http://<SERVER-IP>:9090
```

### Loki

```text
http://<SERVER-IP>:3100
```

---

## Dashboard Import

To reuse this dashboard:

1. Open Grafana
2. Navigate to Dashboards
3. Click Import
4. Upload:

```text
dashboards/node-monitoring-dashboard.json
```

5. Select the appropriate data sources
6. Import the dashboard

---

## Screenshots

### Dashboard Overview

screenshots/dashboard-overview.png

### CPU Metrics

screenshots/cpu-metrics.png

### Memory Metrics

screenshots/memory-metrics.png

### Disk Metrics

screenshots/disk-metrics.png

### Logs View

screenshots/logs-view.png

---

## Future Enhancements

- Multi-node monitoring
- Alerting and notifications
- Kubernetes integration
- AlertManager integration
- Cloud monitoring expansion
- Dashboard variables for node selection

---

## Outcome

Successfully implemented a reusable Grafana observability dashboard that provides:

- Infrastructure monitoring
- System health visibility
- Log monitoring integration
- Docker-based deployment
- Future scalability for additional nodes

---

## Author

**Muhammad Ramzan**

Cloud & DevOps Engineer
