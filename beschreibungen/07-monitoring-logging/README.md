# Projekt 7: Monitoring & Logging (ELK/Prometheus)

## 📋 Projektbeschreibung
Aufbau einer Infrastruktur zur Überwachung von Systemen und zentralisierten Logging. Essentiell für Troubleshooting, Performance-Analyse und Security-Audits.

## 🎯 Lernziele
- Prometheus für Metriken-Erfassung
- Grafana für Visualisierung
- Elasticsearch/Logstash/Kibana (ELK Stack) für Log-Aggregation
- Custom Alerts und Notifications
- Log-Parsing und Analyse
- Performance-Monitoring
- Security Event Logging

## 📊 Schwierigkeitsgrad
**Fortgeschritten**

## ⏱️ Dauer
3-4 Wochen

## 🔧 Anforderungen
- Ubuntu Server 22.04 LTS (mindestens 4GB RAM für Stack)
- Docker installiert (optional aber empfohlen)
- Mehrere Systeme zum Monitoren
- Grundverständnis: JSON, REST APIs

## 📝 Aufgaben

### Phase 1: Prometheus Setup (Tag 1-4)
- [ ] Prometheus installieren oder Docker nutzen
- [ ] prometheus.yml konfigurieren:
  ```yaml
  global:
    scrape_interval: 15s
  scrape_configs:
    - job_name: 'linux'
      static_configs:
        - targets: ['localhost:9100']
  ```
- [ ] Node Exporter installieren auf Ziel-Systemen
- [ ] Prometheus UI testen (`http://localhost:9090`)
- [ ] PromQL (Prometheus Query Language) lernen
- [ ] Basis-Queries schreiben:
  ```
  node_memory_MemAvailable_bytes / 1024 / 1024 / 1024
  rate(node_cpu_seconds_total[5m])
  ```
- [ ] Service-Discovery (optional)

### Phase 2: Grafana Dashboards (Tag 5-7)
- [ ] Grafana installieren oder Docker
- [ ] Prometheus als Data Source hinzufügen
- [ ] Vordefinierte Dashboards importieren
- [ ] Custom Dashboards erstellen:
  - [ ] CPU Usage
  - [ ] Memory Usage
  - [ ] Disk I/O
  - [ ] Network Traffic
- [ ] Variables für Systeme/Instanzen
- [ ] Alert-Bedingungen definieren
- [ ] Dashboard exportieren/versionieren

### Phase 3: Alerting (Tag 8-9)
- [ ] Alertmanager installieren
- [ ] Alert-Regeln definieren:
  ```yaml
  groups:
  - name: node_alerts
    rules:
    - alert: HighMemoryUsage
      expr: (1 - (node_memory_MemAvailable_bytes / node_memory_MemTotal_bytes)) > 0.85
      for: 5m
  ```
- [ ] Alert-Benachrichtigungen:
  - [ ] Email
  - [ ] Slack
  - [ ] PagerDuty (optional)
- [ ] Alert-Templates
- [ ] Alert-Routing konfigurieren

### Phase 4: Elasticsearch/Logstash Setup (Tag 10-12)
- [ ] Elasticsearch installieren (oder Docker)
- [ ] Logstash konfigurieren für Log-Parsing
- [ ] Input-Plugins (File, Syslog, Beats)
- [ ] Filter für Log-Parsing (Grok-Patterns)
- [ ] Output zu Elasticsearch
- [ ] Beispiel-Logstash-Pipeline:
  ```
  input { syslog { port => 5000 } }
  filter { grok { match => { "message" => "%{SYSLOGLINE}" } } }
  output { elasticsearch { hosts => ["localhost"] } }
  ```
- [ ] Logstash Performance testen

### Phase 5: Kibana Visualisierungen (Tag 13-14)
- [ ] Kibana installieren (oder Docker)
- [ ] Elasticsearch Index-Patterns erstellen
- [ ] Discover - Log-Daten durchsuchen
- [ ] Visualisierungen erstellen:
  - [ ] Error-Rate Trends
  - [ ] Top Error Messages
  - [ ] Request Duration Distribution
  - [ ] Geographic Map (falls IP-Geolokalisation)
- [ ] Dashboards zusammenstellen
- [ ] Saved Searches für häufige Queries
- [ ] Alert-Bedingungen basierend auf Log-Patterns

### Phase 6: Log-Sources integrieren (Tag 15-16)
- [ ] Verschiedene Log-Sources:
  - [ ] Systemd Logs (journalctl)
  - [ ] Syslog
  - [ ] Application Logs (z.B. Apache, Nginx)
  - [ ] Custom App Logs
- [ ] Filebeat/Metricbeat für einfache Log-Forwarding
- [ ] Log-Format standardisieren
- [ ] Zentralisierte Log-Sammlung

### Phase 7: ELK Stack mit Docker (Tag 17-18)
- [ ] Docker Compose für kompletten Stack:
  ```yaml
  services:
    elasticsearch:
      image: docker.elastic.co/elasticsearch/elasticsearch:8.0.0
    logstash:
      image: docker.elastic.co/logstash/logstash:8.0.0
    kibana:
      image: docker.elastic.co/kibana/kibana:8.0.0
  ```
- [ ] Stack starten und testen
- [ ] Daten-Persistierung
- [ ] SSL/TLS aktivieren
- [ ] X-Pack Sicherheit (falls Enterprise)

### Phase 8: Advanced Use Cases (Tag 19-20)
- [ ] Anomaly Detection
- [ ] Machine Learning mit ELK (X-Pack)
- [ ] Custom Metrics mit Prometheus Pushgateway
- [ ] Distributed Tracing (optional, mit Jaeger)
- [ ] Log-Retention-Policies
- [ ] Backup/Restore von Elasticsearch

## ✅ Bewertungskriterien
- **Prometheus:** Metriken werden gesammelt, Queries funktionieren
- **Grafana:** Dashboards vorhanden und aussagekräftig
- **Alerting:** Alerts definiert und funktionieren
- **ELK:** Logs werden zentralisiert gesammelt und durchsuchbar
- **Kibana:** Visualisierungen vorhanden und informativ
- **Integration:** Mehrere Log-Sources integriert
- **Dokumentation:** Alle Konfigurationen dokumentiert

## 🔐 Sicherheits-Best-Practices
- [ ] Elasticsearch mit Authentication absichern
- [ ] Kibana nur internen Zugriff
- [ ] Log-Daten verschlüsseln (in Transit und Rest)
- [ ] RBAC für Dashboards und Logs
- [ ] Audit-Logs für Zugriff auf Logs
- [ ] Sensitive Daten maskieren (Passwörter, etc.)

## 📚 Ressourcen & Dokumentation

### Wichtige Dateien
- `/etc/prometheus/prometheus.yml`
- `/etc/prometheus/alert.rules.yml`
- `/etc/logstash/conf.d/*.conf`
- `/etc/grafana/provisioning/`
- `docker-compose.yml` (für ELK)

### Wichtige Links & Befehle
```bash
# Prometheus
curl http://localhost:9090/api/v1/query?query=node_memory_MemAvailable_bytes

# Grafana
http://localhost:3000 (default: admin/admin)

# Elasticsearch
curl http://localhost:9200/_cat/indices

# Kibana
http://localhost:5601

# Systemd Logs
journalctl -u nginx -f
journalctl --since today
```

## 💡 Hands-On Labs

### Lab 1: Prometheus + Grafana Monitoring
- 3 Linux-Systeme mit Node Exporter
- Grafana Dashboards für alle Systeme
- Alerts für High CPU/Memory
- Email-Benachrichtigungen

### Lab 2: ELK Stack für Application Logging
- Custom PHP/Python App mit Logging
- Logs zu Elasticsearch via Logstash
- Kibana Visualisierungen
- Error-Rate Alerts

### Lab 3: Kompletter Monitoring Stack
- Prometheus + Grafana für Metrics
- ELK Stack für Application Logs
- Alertmanager mit Slack Integration
- 24/7 Monitoring Dashboard

## 💡 Trainer-Tipps
- Nutzen Sie Docker Compose für schnellere Deployments
- Zeigen Sie echte Monitoring-Szenarien (z.B. Disk-Space Alert)
- Lassen Sie Umschüler von Alerts überrumpelt werden und dann Dashboards bauen
- Demonstrieren Sie Troubleshooting über Logs

## 📋 Deliverables
1. **Prometheus-Konfiguration:** Scrape-Configs dokumentiert
2. **Grafana-Dashboards:** Exportierte JSON-Dateien
3. **Alert-Rules:** Dokumentierte Alert-Definitionen
4. **ELK-Stack:** Docker Compose oder Installation Guide
5. **Betriebshandbuch:** Wie man Alerts reagiert, Logs durchsucht

---

**Projektstand:** [ ] Nicht begonnen | [ ] In Arbeit | [ ] Abgeschlossen

**Notizen:**
