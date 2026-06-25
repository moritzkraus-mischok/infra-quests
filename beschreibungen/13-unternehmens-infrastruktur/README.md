# Projekt 13: Kleine Unternehmens-IT-Infrastruktur

## 📋 Projektbeschreibung
Integrationsprojekt, das mehrere Fähigkeiten kombiniert. Aufbau einer kompletten, funktionsfähigen IT-Infrastruktur für ein kleines Unternehmen mit realistischen Anforderungen.

## 🎯 Lernziele
- Integration mehrerer Systeme und Services
- Unternehmens-Anforderungen umsetzen
- Skalierbarkeit und Wartbarkeit
- Sicherheit auf allen Ebenen
- Dokumentation für Betrieb
- Support und Troubleshooting in Produktivumgebung

## 📊 Schwierigkeitsgrad
**Expert**

## ⏱️ Dauer
4-6 Wochen

## 🔧 Anforderungen
- Ubuntu Server 22.04 LTS (mehrere VMs)
- Min. 16GB RAM Gesamt
- 100GB+ Speicherplatz
- Alle vorherigen Projekt-Skills empfohlen
- Grundverständnis: Business Requirements, Project Management

## 📝 Aufgaben

### Infrastruktur-Anforderungen

#### Szenario: "TechStart GmbH"
- 50 Mitarbeiter
- Gemischte Umgebung: Windows + Linux
- 2 Office-Standorte
- Einige Remote-Worker
- Datenschutz-Anforderungen (DSGVO)

### Phase 1: Anforderungsanalyse & Planung (Tag 1-3)
- [ ] Geschäfts-Anforderungen definieren:
  - [ ] Verfügbarkeitsanforderungen (wie viel Downtime ist akzeptabel?)
  - [ ] Performance-Anforderungen
  - [ ] Compliance-Anforderungen (DSGVO, etc.)
  - [ ] Budget-Constraints
- [ ] IT-Infrastruktur auswählen
- [ ] Disaster-Recovery RTO/RPO
- [ ] Skalierungspläne
- [ ] Security-Level definieren
- [ ] Dokumentations-Struktur planen

### Phase 2: Kern-Infrastruktur (Tag 4-8)
- [ ] **Virtualisierung / Bare Metal:**
  - [ ] Hypervisor (KVM/Proxmox)
  - [ ] Netzwerk-Segmentierung
  
- [ ] **Zentrales Verzeichnis (FreeIPA/Samba AD):**
  - [ ] User Management
  - [ ] Group Policies
  - [ ] Authentication für alle Services
  
- [ ] **Dateiserver:**
  - [ ] Samba für Windows-Clients
  - [ ] NFS für Linux
  - [ ] Quotas und Berechtigungen
  - [ ] Snapshots für schnelle Recovery
  
- [ ] **Backup & DR:**
  - [ ] Automatisierte Backups
  - [ ] Off-site Backups
  - [ ] Recovery-Testing

### Phase 3: Sicherheitsinfrastruktur (Tag 9-12)
- [ ] **Firewall & Segmentierung:**
  - [ ] DMZ für öffentliche Services
  - [ ] Interne Netzwerk-Segmente
  - [ ] VPN für Remote-Worker
  
- [ ] **Mail-Server:**
  - [ ] Postfix/Dovecot
  - [ ] SPF, DKIM, DMARC
  - [ ] Mail-Filtering (Spam, Malware)
  
- [ ] **Monitoring & Logging:**
  - [ ] Prometheus + Grafana für Metrics
  - [ ] ELK Stack für Logs
  - [ ] Alerts für kritische Events
  
- [ ] **Patch Management:**
  - [ ] Automated Security Updates
  - [ ] Update-Testing
  - [ ] Patch-Scheduling

### Phase 4: Services & Anwendungen (Tag 13-16)
- [ ] **Web-Infrastruktur:**
  - [ ] LAMP/LEMP Stack
  - [ ] SSL/TLS für alle Web-Services
  - [ ] Load-Balancing (optional)
  
- [ ] **Datenbank-Services:**
  - [ ] PostgreSQL/MySQL für Geschäfts-Apps
  - [ ] Backup-Strategie
  - [ ] HA-Setup (optional)
  
- [ ] **Interne Services:**
  - [ ] Wiki/Dokumentation
  - [ ] Issue-Tracker
  - [ ] Git-Repository (optional)

### Phase 5: Automation & Verwaltung (Tag 17-19)
- [ ] **Ansible für Configuration Management:**
  - [ ] Playbooks für jeden Service-Typ
  - [ ] Automatische Provisioning
  - [ ] Change-Management
  
- [ ] **Deployment-Pipeline:**
  - [ ] Automated Testing
  - [ ] Blue-Green Deployments
  - [ ] Rollback-Pläne

### Phase 6: Dokumentation (Tag 20-22)
- [ ] **Technische Dokumentation:**
  - [ ] Infrastruktur-Diagramme (Netzwerk, Systeme)
  - [ ] Service-Dokumentation
  - [ ] API-Dokumentation
  
- [ ] **Runbooks:**
  - [ ] Daily/Weekly/Monthly Tasks
  - [ ] Troubleshooting-Guides
  - [ ] Disaster-Recovery Procedures
  - [ ] Escalation-Procedures
  
- [ ] **Policies & Procedures:**
  - [ ] Passwort-Policy
  - [ ] Backup-Policy
  - [ ] Security-Policy
  - [ ] Change-Management-Procedure

### Phase 7: Testing & Validation (Tag 23-25)
- [ ] **Functional Testing:**
  - [ ] Alle Services funktionieren
  - [ ] User-Logins funktionieren
  - [ ] File-Zugriff funktioniert
  
- [ ] **Performance Testing:**
  - [ ] Response Times akzeptabel
  - [ ] Unter Last stabil
  
- [ ] **Security Testing:**
  - [ ] Schwachstellen-Scan
  - [ ] Penetration Testing Grundlagen
  
- [ ] **DR Testing:**
  - [ ] Recovery-Szenarien durchspielen
  - [ ] RTO/RPO überprüfen

### Phase 8: Produktion & Übergabe (Tag 26-30)
- [ ] **Go-Live Planning:**
  - [ ] Migration-Plan
  - [ ] Cutover-Window
  - [ ] Rollback-Plan
  
- [ ] **User-Schulung:**
  - [ ] Passwort-Reset Prozess
  - [ ] VPN-Zugang
  - [ ] Dateiserver-Nutzung
  
- [ ] **Handover:**
  - [ ] Dokumentations-Review
  - [ ] Support-Team Training
  - [ ] Operations-Übersicht
  
- [ ] **Post-Go-Live Support:**
  - [ ] Issue-Tracking und Fixes
  - [ ] Performance-Monitoring
  - [ ] User-Feedback Integration

## ✅ Bewertungskriterien

### Funktionale Kriterien
- [ ] Alle definierten Services laufen
- [ ] Users können sich authentifizieren
- [ ] Datei-Zugriff funktioniert zuverlässig
- [ ] Backups werden regelmäßig durchgeführt
- [ ] Monitoring und Alerting funktionieren

### Qualitäts-Kriterien
- [ ] System stabil über längeren Zeitraum
- [ ] Performance akzeptabel (< 2sec Response)
- [ ] Security-Best-Practices befolgt
- [ ] Redundanz wo nötig

### Dokumentations-Kriterien
- [ ] Infrastruktur-Diagramme vorhanden
- [ ] Runbooks für wichtige Prozesse
- [ ] Troubleshooting-Guides
- [ ] DR-Dokumentation

### Wartbarkeits-Kriterien
- [ ] Ansible-Playbooks für Automation
- [ ] Dokumentierte Prozesse
- [ ] Monitoring-Alerts funktionieren
- [ ] Change-Management-Prozess definiert

## 🔐 Sicherheits-Checklist
- [ ] VPN für Remote-Worker
- [ ] Firewall-Regeln implementiert
- [ ] User-Passwörter verschlüsselt
- [ ] TLS für alle Web-Services
- [ ] Regelmäßige Backups
- [ ] Security-Updates aktuell
- [ ] Logging für Audit-Trail

## 📚 Ressourcen & Dokumentation

### Typische Architektur
```
┌─────────────────────────────────────┐
│  Internet                           │
└────────────────┬────────────────────┘
                 │
          ┌──────┴──────┐
          │   Firewall  │
          └──────┬──────┘
                 │
      ┌──────────┼──────────┐
      │                     │
   ┌──┴──┐            ┌────┴────┐
   │ DMZ │ Web-Stack  │ Internal │
   │     │ Mail       │ Network  │
   │     │ VPN        │          │
   └─────┘            └────┬────┘
                           │
         ┌─────────────────┼─────────────────┐
         │                 │                 │
    ┌────┴────┐      ┌────┴────┐      ┌────┴────┐
    │   FreeIPA      │ Fileserver     │ Backup  │
    │   (Auth)       │ (NAS/Samba)    │ Storage │
    └─────────┘      └─────────┘      └─────────┘
```

## 💡 Hands-On Implementation

### Team-Struktur für Projekt
- **Architektur-Team:** Überblick & Planung
- **Security-Team:** Firewall, VPN, Compliance
- **Services-Team:** Datenbank, Mail, Web
- **Ops-Team:** Monitoring, Backups, DR
- **Dokumentation-Team:** Runbooks, Policies

### Iterativer Aufbau
1. **Sprint 1:** Basis-Infrastruktur (FreeIPA, Fileserver)
2. **Sprint 2:** Sicherheitsservices (Firewall, VPN, Mail)
3. **Sprint 3:** Monitoring und Backup
4. **Sprint 4:** Zusätzliche Services, Automation
5. **Sprint 5:** Testing, Dokumentation, Optimierung
6. **Sprint 6:** Go-Live und Support

## 💡 Trainer-Tipps
- Setzen Sie realistische Business-Anforderungen
- Lassen Sie Teams zusammenarbeiten
- Simulieren Sie echte Probleme (Server-Ausfall, Datenverlust)
- Fordern Sie Entscheidungen basierend auf Trade-offs ein
- Betonen Sie Dokumentation und Support

## 📋 Deliverables

1. **Infrastruktur-Dokumentation**
   - Netzwerk-Diagramm
   - System-Architektur
   - Service-Matrix

2. **Operative Dokumentation**
   - Runbook für Daily Operations
   - Troubleshooting-Guide
   - Escalation-Procedures
   - DR-Plan

3. **Automatisierung**
   - Ansible Playbooks
   - Automated Backup-Scripts
   - Monitoring-Configuration

4. **Test-Reports**
   - Funktions-Tests
   - Performance-Tests
   - Security-Audit
   - DR-Test-Ergebnisse

5. **Übergabe-Dokumentation**
   - User-Guides
   - IT-Admin-Manual
   - Support-Procedures

---

**Projektstand:** [ ] Nicht begonnen | [ ] In Arbeit | [ ] Abgeschlossen

**Notizen:**
