# Umschüler-Projekte - Fachinformatiker Systemintegration (1. Jahr)

## 📚 Projektübersicht

Eine umfassende Sammlung von 15 praktischen Projekten für Umschüler am Ende ihres ersten Jahres der Ausbildung zum Fachinformatiker mit Fachrichtung Systemintegration.

**Fokus:** Open Source Tools, Ubuntu Linux, praktische Hands-on-Erfahrung

---

## 🎯 Projektgruppen nach Komplexität

### 🟢 Basis-Projekte (1-2 Wochen)
Fundament-Wissen, muss beherrscht werden

1. **[01 - Ubuntu Server Setup & Hardening](./01-ubuntu-server-setup/README.md)**
   - Sichere Installation, SSH, Firewall, Backups
   - Erstes "echter" Server: Installation bis zum Betrieb
   - Dauer: 1-2 Wochen

2. **[02 - Linux Benutzer- und Rechteverwaltung](./02-linux-benutzerverwaltung/README.md)**
   - User, Gruppen, Berechtigungen, Sudo, ACLs
   - Zentral für Multi-User-Systeme
   - Dauer: 1-2 Wochen

3. **[03 - Netzwerk-Grundlagen mit Linux](./03-netzwerk-grundlagen/README.md)**
   - Netzwerk-Konfiguration, DNS, Routing, Troubleshooting
   - Essentiell für jeden Admin
   - Dauer: 1-2 Wochen

### 🟡 Mittlere Projekte (2-3 Wochen)
Praktische Services, realistisch einsetzbar

4. **[04 - LAMP/LEMP Stack Deployment](./04-lamp-lemp-stack/README.md)**
   - Web-Server, Datenbank, PHP, SSL/TLS
   - Apache/Nginx + MySQL + PHP komplett
   - Dauer: 2-3 Wochen

5. **[05 - Samba/NFS Dateifreigaben](./05-samba-nfs-freigaben/README.md)**
   - Windows-Integration, Linux-Netzwerk-Shares
   - Zentral für File-Server
   - Dauer: 2-3 Wochen

6. **[06 - OpenSSH & VPN Setup](./06-openssh-vpn-setup/README.md)**
   - SSH-Hardening, Tunneling, OpenVPN/WireGuard
   - Sicherer Remote-Zugriff
   - Dauer: 2-3 Wochen

7. **[07 - Monitoring & Logging (ELK/Prometheus)](./07-monitoring-logging/README.md)**
   - Prometheus, Grafana, Elasticsearch, Kibana
   - System-Überwachung und Troubleshooting
   - Dauer: 3-4 Wochen

### 🟠 Fortgeschrittene Projekte (3-4 Wochen)
Moderne Technologien, höhere Komplexität

8. **[08 - Docker & Container-Orchestration](./08-docker-container/README.md)**
   - Docker, Compose, Kubernetes (Microk8s)
   - Containerisierung und Orchestration
   - Dauer: 3-4 Wochen

9. **[09 - BIND DNS Server](./09-bind-dns/README.md)**
   - Authoritative DNS, Zones, DNSSEC
   - Kritische Infrastruktur
   - Dauer: 2-3 Wochen

10. **[10 - Ansible Infrastruktur-Automatisierung](./10-ansible-automatisierung/README.md)**
    - Playbooks, Roles, Automation
    - Infrastructure as Code
    - Dauer: 2-3 Wochen

11. **[11 - FreeIPA/Samba AD - Enterprise Identity](./11-freeipa-samba-ad/README.md)**
    - Zentralisierte Benutzerverwaltung, LDAP, Kerberos
    - Alternative zu Active Directory
    - Dauer: 3-4 Wochen

12. **[12 - Backup & Disaster Recovery](./12-backup-disaster-recovery/README.md)**
    - Backup-Strategien, Bacula/Bareos, Restic, DR-Planung
    - Kritische Verantwortung
    - Dauer: 3-4 Wochen

### 🔴 Integrations-Projekte (4-6 Wochen)
Kombination mehrerer Skills, realistische Szenarien

13. **[13 - Kleine Unternehmens-IT-Infrastruktur](./13-unternehmens-infrastruktur/README.md)**
    - Komplette IT für kleines Unternehmen
    - Integration aller vorherigen Projekte
    - Dauer: 4-6 Wochen

14. **[14 - Netzwerk-Virtualisierung (KVM/Proxmox)](./14-netzwerk-virtualisierung/README.md)**
    - Hypervisor, VMs, Live-Migration, Snapshots
    - Moderne Infrastruktur
    - Dauer: 2-3 Wochen

15. **[15 - Scripting Projekt (Bash/Python)](./15-scripting-projekt/README.md)**
    - Bash und Python Automatisierungs-Skripte
    - Praktische Tagesarbeit-Tools
    - Dauer: 2-3 Wochen

---

## 📊 Abhängigkeiten & Reihenfolge

```
Empfohlene Reihenfolge für optimales Lernen:

MONAT 1-2 (Fundament)
├── 01 Ubuntu Server Setup      ✅ Start
├── 02 Benutzer & Rechte        ✅ Nach 01
├── 03 Netzwerk-Grundlagen      ✅ Nach 02
└── 15 Scripting (Bash-Teil)    ✅ Parallel

        ↓

MONAT 3-4 (Services)
├── 04 LAMP/LEMP Stack          ✅ Nach 01-03
├── 05 Samba/NFS                ✅ Nach 02
├── 06 SSH & VPN                ✅ Nach 03
└── 09 BIND DNS                 ✅ Nach 03

        ↓

MONAT 5-6 (Advanced)
├── 07 Monitoring & Logging     ✅ Nach 04/09
├── 08 Docker                   ✅ Optional, nach 04
├── 10 Ansible                  ✅ Nach 04
├── 11 FreeIPA/Samba            ✅ Nach 02
├── 12 Backup & DR              ✅ Nach 04
└── 14 Virtualisierung          ✅ Optional, nach 01

        ↓

WOCHE 25-30 (Integrations-Projekt)
└── 13 Unternehmens-Infrastruktur  ✅ Nach 01-12
```

---

## 🎓 Lernziele Pro Stufe

### Nach Basis-Projekten (01-03)
- [ ] Linux System-Administration Fundamentals
- [ ] Sichere Systeminstallation
- [ ] Benutzer- und Zugriffsverwaltung
- [ ] Netzwerk-Konfiguration und Troubleshooting

### Nach Mittleren Projekten (04-07)
- [ ] Web-Services betreiben (LAMP/LEMP)
- [ ] Dateifreigaben managen (Samba/NFS)
- [ ] Sichere Remote-Zugriffe (SSH, VPN)
- [ ] System-Monitoring und Log-Analyse

### Nach Fortgeschrittenen Projekten (08-12)
- [ ] Containerisierung und Orchestration
- [ ] DNS-Server-Betrieb
- [ ] Infrastructure as Code (Ansible)
- [ ] Enterprise-Identity Management
- [ ] Backup- und Recovery-Strategien

### Nach Integrationsprojekten (13-15)
- [ ] Komplette IT-Infrastruktur aufbauen
- [ ] Virtualisierung praktizieren
- [ ] Automatisierungs-Skripte entwickeln
- [ ] Unternehmens-Anforderungen umsetzen

---

## 🔧 Voraussetzungen

### Hardware/Umgebung
- PC mit mind. 32GB RAM für umfassende Labs
- Oder Cloud-VM mit entsprechenden Ressourcen
- Ubuntu 22.04 LTS als Basis-OS

### Software (wird während Projekten installiert)
- Docker
- VirtualBox/KVM
- Ansible
- Git
- Python 3.9+
- Bash 5.0+

### Grundwissen
- Linux Shell-Befehle
- Grundlegende Netzwerk-Konzepte
- Dateisystem-Grundlagen
- Text-Editoren (nano, vim)

---

## ✅ Bewertung & Erfolgskriterien

Jedes Projekt hat folgende Bewertungskriterien:

1. **Funktionalität** - Löst das Problem
2. **Sicherheit** - Best-Practices beachtet
3. **Dokumentation** - Nachvollziehbar dokumentiert
4. **Wartbarkeit** - Code/Config ist wartbar
5. **Performance** - Angemessene Optimierungen

---

## 📚 Zusätzliche Ressourcen

### Dokumentation
- [Ubuntu Server Guide](https://ubuntu.com/server/docs)
- [Linux Manual Pages](https://man7.org/)
- [Open Source Project Docs](https://www.linux.org/docs/)

### Communities
- Ubuntu Community
- Red Hat & CentOS Community
- Docker Community
- Kubernetes Community

### Tools & IDEs
- VS Code mit Remote SSH
- PyCharm Professional (Student License)
- Postman für API-Testing

---

## 🎯 Trainer-Empfehlungen

### Für schnellere Lerner
- Projekte 01-03 kombinieren
- Optional zu 08, 14 hinzufügen
- Projekt 13 erweitern

### Für Umschüler mit Schwierigkeiten
- Mehr Zeit bei 01-03 nehmen
- Projekt 15 Bash-Teil mehr Übungen
- Pair-Programming für 04-07

### Für gemischte Gruppen
- Differenzierungsaufgaben in 04-07
- Erweiterte Anforderungen in 13
- Optionale Advanced Topics (Cluster, HA)

---

## 📝 Projektablauf

Jedes Projekt folgt diesem Schema:

1. **Anforderungen** - Was muss getan werden
2. **Phasen** - Detaillierte Schritte
3. **Hands-On Labs** - Praktische Übungen
4. **Bewertungskriterien** - Was wird bewertet
5. **Deliverables** - Was wird abgegeben
6. **Tipps** - Häufige Fehler und Lösungen

---

## 🚀 Los gehts!

Wähle ein Projekt aus der Liste oben und öffne die entsprechende README.md

**Viel Erfolg beim Lernen! 🎓**

---

**Stand:** Juni 2026  
**Version:** 1.0  
**Für:** Umschulung Fachinformatiker (Systemintegration)
