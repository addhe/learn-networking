# 🔧 Panduan Implementasi Monitoring System

## 📋 Komponen Monitoring

### 1. Prometheus Setup
```yaml
# prometheus.yml
global:
  scrape_interval: 15s
  evaluation_interval: 15s

scrape_configs:
  - job_name: 'network_devices'
    static_configs:
      - targets: ['192.168.1.10:9100']  # Router
      - targets: ['192.168.1.11:9100']  # Switch
      - targets: ['192.168.1.12:9100']  # Firewall

  - job_name: 'snmp_exporter'
    static_configs:
      - targets: ['localhost:9116']

  - job_name: 'blackbox_exporter'
    metrics_path: /probe
    params:
      module: [http_2xx, icmp]
    static_configs:
      - targets:
        - http://internal-app.local
        - 8.8.8.8  # External connectivity check
```

### 2. Grafana Dashboard Examples

#### Network Overview
```json
{
  "dashboard": {
    "title": "Network Overview",
    "panels": [
      {
        "title": "Interface Bandwidth",
        "type": "graph",
        "datasource": "Prometheus",
        "targets": [
          {
            "expr": "rate(ifHCInOctets{device=~\"$device\"}[5m])*8",
            "legendFormat": "{{interface}} - In"
          },
          {
            "expr": "rate(ifHCOutOctets{device=~\"$device\"}[5m])*8",
            "legendFormat": "{{interface}} - Out"
          }
        ]
      }
    ]
  }
}
```

## 🛠 Konfigurasi Alert Manager

### 1. Basic Configuration
```yaml
# alertmanager.yml
global:
  smtp_smarthost: 'smtp.company.com:587'
  smtp_from: 'alertmanager@company.com'
  smtp_auth_username: 'alerts'
  smtp_auth_password: 'password'

route:
  group_by: ['alertname', 'device']
  group_wait: 30s
  group_interval: 5m
  repeat_interval: 4h
  receiver: 'team-network'

receivers:
- name: 'team-network'
  email_configs:
  - to: 'network-team@company.com'
  webhook_configs:
  - url: 'http://alerts.company.com/webhook'
```

### 2. Alert Rules
```yaml
# network_alerts.yml
groups:
- name: network_alerts
  rules:
  - alert: HighInterfaceUtilization
    expr: rate(ifHCInOctets[5m]) * 8 / ifSpeed * 100 > 90
    for: 15m
    labels:
      severity: warning
    annotations:
      summary: "High interface utilization (instance {{ $labels.instance }})"
      description: "Interface utilization is above 90%"

  - alert: InterfaceDown
    expr: ifOperStatus == 2
    for: 5m
    labels:
      severity: critical
    annotations:
      summary: "Interface down (instance {{ $labels.instance }})"
      description: "Interface {{ $labels.interface }} has been down for 5 minutes"
```

## 📊 Visualisasi Data

### 1. Network Performance Dashboard
```
+-------------------------+-------------------------+
|    Interface Traffic    |    Error Rates         |
| [Line Graph]           | [Bar Graph]            |
|                        |                        |
+-------------------------+-------------------------+
|    Packet Loss         |    Latency             |
| [Gauge]               | [Heatmap]             |
|                        |                        |
+-------------------------+-------------------------+
```

### 2. Security Dashboard
```
+-------------------------+-------------------------+
|    Firewall Events     |    VPN Status          |
| [Table]               | [Status Panel]         |
|                        |                        |
+-------------------------+-------------------------+
|    IPS/IDS Alerts      |    Auth Failures       |
| [Alert List]          | [Counter]             |
|                        |                        |
+-------------------------+-------------------------+
```

## 🔄 Data Collection

### 1. SNMP Configuration
```yaml
# snmp.yml
auth:
  community: public
  version: 2
modules:
  router:
    walk:
      - 1.3.6.1.2.1.2  # Interfaces
      - 1.3.6.1.2.1.31 # Interface Extensions
    metrics:
      - name: ifOperStatus
        oid: 1.3.6.1.2.1.2.2.1.8
        type: gauge
```

### 2. Netflow Setup
```yaml
# netflow.conf
collectors:
  - host: 192.168.1.100
    port: 2055
sampling:
  rate: 100
  mode: deterministic
aggregation:
  interval: 60
```

## 📈 Capacity Planning

### 1. Storage Requirements
```
Retention Period: 30 days
Data Points/Second: ~1000
Storage per Day: ~2GB
Total Storage: ~60GB

Recommended Setup:
- SSD Storage
- RAID Configuration
- Regular Backup
```

### 2. Performance Tuning
```yaml
# prometheus.yml tuning
global:
  scrape_interval: 30s     # Default scrape interval
  scrape_timeout: 10s      # Timeout for scrape
  evaluation_interval: 30s  # Rule evaluation interval

storage:
  tsdb:
    retention.time: 30d    # How long to retain data
    retention.size: 60GB   # Maximum storage size
```

## 🔍 Troubleshooting Monitoring

### 1. Common Issues
```
1. Data Collection Issues
   - Check SNMP connectivity
   - Verify port accessibility
   - Review authentication

2. Performance Issues
   - Monitor CPU/Memory usage
   - Check disk I/O
   - Review query performance
```

### 2. Debug Commands
```bash
# Check Prometheus targets
curl localhost:9090/api/v1/targets

# Verify metrics collection
curl localhost:9100/metrics

# Test AlertManager
curl -H "Content-Type: application/json" -d '[{"labels":{"alertname":"TestAlert"}}]' localhost:9093/api/v1/alerts
```

## 📚 Best Practices

### 1. Data Collection
- Use appropriate intervals
- Implement data retention policies
- Monitor collector health
- Regular configuration review

### 2. Alert Configuration
- Define clear thresholds
- Avoid alert fatigue
- Include context in alerts
- Regular alert review

### 3. Dashboard Design
- Keep it simple
- Use appropriate visualizations
- Include documentation
- Regular updates

## 🔄 Maintenance Tasks

### 1. Daily Checks
```
[ ] Verify data collection
[ ] Check alert status
[ ] Monitor system resources
[ ] Review critical metrics
```

### 2. Weekly Tasks
```
[ ] Backup configurations
[ ] Review alert thresholds
[ ] Update dashboards
[ ] Performance optimization
```

### 3. Monthly Review
```
[ ] Capacity planning
[ ] Retention policy review
[ ] System upgrades
[ ] Documentation updates
```