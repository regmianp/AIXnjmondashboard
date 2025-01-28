# Grafana Dashboard for AIX Monitoring using NJMON v86 and InfluxDB2

This repository provides a setup guide and Grafana dashboard configuration for monitoring AIX systems using NJMON v86 as the monitoring tool and InfluxDB2 as the backend database. The dashboard offers insights into system performance, resource utilization, and key metrics for effective AIX system management.

---

## Table of Contents

1. [Introduction](#introduction)
2. [Prerequisites](#prerequisites)
3. [Architecture](#architecture)
4. [Installation and Configuration](#installation-and-configuration)
   - [NJMON Setup on AIX](#njmon-setup-on-aix)
   - [InfluxDB2 Configuration](#influxdb2-configuration)
   - [Grafana Dashboard Setup](#grafana-dashboard-setup)
5. [Dashboards](#dashboards)
6. [Contributing](#contributing)

---

## Introduction

**NJMON (Nigel's Monitor)** is a lightweight monitoring tool for AIX and Linux systems that collects performance and resource utilization data. By pairing NJMON with **InfluxDB2** and **Grafana**, you can visualize near real-time and historical data to monitor AIX system health and performance.

---

## Prerequisites

Ensure you have the following components installed and running:

- **AIX system** with NJMON v86 installed.
- **InfluxDB2** instance for storing monitoring data.
- **Grafana** for visualizing the collected data.
- **Network connectivity** between the AIX system, InfluxDB2, and Grafana server.

---

## Architecture

The architecture consists of three main components:

1. **NJMON**: Installed on the AIX system, it collects system metrics and sends them to InfluxDB.
2. **InfluxDB2**: A time-series database that stores the metrics sent by NJMON.
3. **Grafana**: Connects to InfluxDB2 to visualize the metrics in a user-friendly dashboard.

---

## Installation and Configuration

### NJMON Setup on AIX

1. Download NJMON v86 from the official [NJMON repository](https://nmon.sourceforge.io/pmwiki.php?n=Site.Njmon).
2. Install NJMON on the AIX system, with root user privilege, executing ninstall file in the njmon package.
  ```bash
unzip njmon_aix_v86.zip
cd njmon_aix_v86
chmod +x ninstall
./ninstall
   ```  
3. Start NJMON to log monitoring data to InfluxDB.
   ```bash
   /usr/lbin/nimon -s 30 -k -i <IP of influxdb> -p 8086 -x njmon -O <organization-name> -T <API-Token-with-write-access-to-bucket>
   ```

### InfluxDB2 Configuration

1. Install and set up InfluxDB2 on your server. Refer to the [official InfluxDB2 documentation](https://docs.influxdata.com/influxdb/latest/get-started/).
2. Create a bucket for storing AIX metrics.
3. Generate an API token for NJMON to authenticate with InfluxDB2.
4. Verify NJMON is sending data by querying the bucket:
   ```bash
   influx query 'from(bucket: "<YOUR_BUCKET>") |> range(start: -1h)'
   ```

### Grafana Dashboard Setup

1. Install Grafana. Refer to the [official Grafana documentation](https://grafana.com/docs/grafana/latest/installation/).
2. Add InfluxDB2 as a data source in Grafana:
   - Navigate to **Configuration > Data Sources**.
   - Select **InfluxDB** and fill in the required details:
     - URL: `http://<INFLUXDB_SERVER>:<PORT>`
     - Organization: `<YOUR_ORG>`
     - Bucket: `<YOUR_BUCKET>`
     - Token: `<YOUR_TOKEN>`
3. Import the provided Grafana dashboard JSON file:
   - Go to **Dashboards > Import**.
   - Upload the `aix_dashboard.json` file from this repository.
4. Verify the dashboard displays metrics from your AIX system.

---

## Dashboards

The Grafana dashboard includes the following panels:

1. **CPU Utilization**: Displays CPU usage trends and per-core metrics.
2. **Memory Usage**: Tracks memory allocation, usage, and swap activity.
3. **Disk Busy**: Monitors disk read/write operations and throughput.
4. **Network Activity**: Shows incoming and outgoing network traffic.

---

## Contributing

Contributions are welcome! If you have suggestions for improvements or additional dashboards, feel free to open a pull request or create an issue.
