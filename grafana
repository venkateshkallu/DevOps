# Grafana + Prometheus Monitoring Setup (Local Lab)

This guide explains how to create a simple monitoring stack using **Prometheus**, **Node Exporter**, and **Grafana**.  
The purpose of this setup is to understand how metrics flow from a system into dashboards.

This architecture is commonly used in production environments for monitoring infrastructure and services.

---

# Architecture Overview

```

Server Metrics
↓
Node Exporter
↓
Prometheus (collects metrics)
↓
Grafana (visualizes metrics)

````

Explanation:

| Component | Role |
|---|---|
| Node Exporter | Exposes system metrics (CPU, memory, disk) |
| Prometheus | Collects and stores metrics |
| Grafana | Creates dashboards using Prometheus data |

---

# Prerequisites

- Docker installed
- Docker Compose installed
- Basic understanding of metrics

---

# Step 1: Create Project Directory

```bash
mkdir monitoring-lab
cd monitoring-lab
````

---

# Step 2: Create Docker Compose File

Create a file called:

```
docker-compose.yml
```

Add the following content:

```yaml
version: '3'

services:

  prometheus:
    image: prom/prometheus
    container_name: prometheus
    ports:
      - "9090:9090"
    volumes:
      - ./prometheus.yml:/etc/prometheus/prometheus.yml

  grafana:
    image: grafana/grafana
    container_name: grafana
    ports:
      - "3000:3000"

  node-exporter:
    image: prom/node-exporter
    container_name: node-exporter
    ports:
      - "9100:9100"
```

---

# Step 3: Create Prometheus Configuration

Create a file:

```
prometheus.yml
```

Add:

```yaml
global:
  scrape_interval: 15s

scrape_configs:
  - job_name: "node"
    static_configs:
      - targets: ["node-exporter:9100"]
```

Explanation:

* Prometheus scrapes metrics every **15 seconds**
* Node exporter runs on **port 9100**

---

# Step 4: Start the Monitoring Stack

Run:

```bash
docker compose up -d
```

This starts three containers:

| Service       | Port |
| ------------- | ---- |
| Prometheus    | 9090 |
| Grafana       | 3000 |
| Node Exporter | 9100 |

---

# Step 5: Verify Prometheus

Open browser:

```
http://localhost:9090
```

Go to **Graph** and run:

```
up
```

Expected result:

```
up{job="node"} = 1
```

This means Prometheus is successfully scraping node exporter.

---

# Step 6: Access Grafana

Open:

```
http://localhost:3000
```

Default credentials:

```
username: admin
password: admin
```

---

# Step 7: Add Prometheus Datasource

In Grafana:

```
Settings → Data Sources → Add data source
```

Choose:

```
Prometheus
```

Set URL:

```
http://prometheus:9090
```

Click:

```
Save & Test
```

You should see:

```
Datasource connected successfully
```

---

# Step 8: Create Grafana Dashboard

Navigate:

```
Dashboards → New Dashboard → Add Panel
```

Select datasource:

```
Prometheus
```

---

# Example Queries

### CPU Usage

```
rate(node_cpu_seconds_total[5m])
```

---

### Memory Available

```
node_memory_MemAvailable_bytes
```

---

### Disk Read

```
node_disk_read_bytes_total
```

---

# Recommended Dashboard Panels

Create three panels:

| Panel            | Query                              |
| ---------------- | ---------------------------------- |
| CPU Usage        | `rate(node_cpu_seconds_total[5m])` |
| Memory Available | `node_memory_MemAvailable_bytes`   |
| Disk Reads       | `node_disk_read_bytes_total`       |

---

# Observability Flow

```
node-exporter
      ↓
Prometheus collects metrics
      ↓
Grafana queries Prometheus
      ↓
Dashboards display system health
```

---

# Why This Setup Is Important

This architecture is used in modern DevOps environments for monitoring:

* Kubernetes clusters
* Service meshes
* API gateways
* Microservices

Even systems like **service mesh gateways** expose metrics that follow this same pipeline.

---

# Key Learning Outcomes

After completing this setup you understand:

* How metrics are exposed
* How Prometheus collects metrics
* How Grafana visualizes data
* How dashboards are created

---

# Next Steps

You can extend this lab by adding:

* Database exporters
* Application metrics
* Alerting rules
* Kubernetes monitoring

---

# Conclusion

This setup demonstrates the **basic monitoring pipeline** used in modern infrastructure:

```
Metrics → Prometheus → Grafana → Dashboard
```

Understanding this pipeline is essential for DevOps engineers working with monitoring and observability systems.

```
```
