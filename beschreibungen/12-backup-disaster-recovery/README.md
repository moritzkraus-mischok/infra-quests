# Projekt 12: Backup & Disaster Recovery

## 📋 Projektbeschreibung
Strategische Planung und Implementierung von Backup- und Disaster-Recovery-Lösungen. Eine kritische Verantwortung für Systemintegratoren.

## 🎯 Lernziele
- Backup-Strategien verstehen (Full, Incremental, Differential)
- Backup-Software konfigurieren (Bacula, Bareos, Restic)
- RPO und RTO Konzepte
- Recovery-Planung und -Testing
- Verschlüsselte Backups
- Off-site Backup Storage
- Monitoring von Backup-Jobs
- Disaster-Recovery Runbooks

## 📊 Schwierigkeitsgrad
**Fortgeschritten → Expert**

## ⏱️ Dauer
3-4 Wochen

## 🔧 Anforderungen
- Ubuntu Server 22.04 LTS
- Mehrere VMs/Systeme zum Backup
- Backup-Storage (zusätzliches Verzeichnis oder Festplatte)
- Min. 50GB verfügbarer Speicher
- Grundverständnis: Partitionen, Dateisysteme

## 📝 Aufgaben

### Phase 1: Backup-Grundlagen & Strategien (Tag 1-2)
- [ ] Backup-Konzepte verstehen:
  - [ ] Full Backup - komplette Kopie
  - [ ] Incremental - nur seit letztem Backup geänderte Daten
  - [ ] Differential - nur seit letztem Full Backup
  - [ ] Mirror/Snapshot - aktuelle Kopie
- [ ] RPO (Recovery Point Objective) vs. RTO (Recovery Time Objective)
- [ ] 3-2-1 Backup-Regel verstehen (3 Kopien, 2 Medien, 1 off-site)
- [ ] Retention Policies planen
- [ ] Backup-Windows planen

### Phase 2: Rsync basierte Backups (Tag 3-4)
- [ ] Rsync Grundlagen
- [ ] Inkrementelle Backups mit Rsync:
  ```bash
  rsync -av --delete /home/ /backup/home/
  ```
- [ ] SSH-basierte Remote Backups:
  ```bash
  rsync -av -e ssh /home/ user@backup-server:/backups/home/
  ```
- [ ] Cron-Jobs für Automated Backups
- [ ] Bandbreite limitieren
- [ ] Dry-run testen: `rsync -av --dry-run`

### Phase 3: Bacula/Bareos Setup (Tag 5-8)
- [ ] Bacula/Bareos Architektur verstehen (Director, Storage Daemon, File Daemon)
- [ ] Installation:
  ```bash
  sudo apt install bareos-director bareos-storage bareos-filedaemon
  ```
- [ ] Konfiguration `/etc/bareos/`:
  - [ ] Director config
  - [ ] Storage Daemon config
  - [ ] File Daemon config
  - [ ] Pool Definitions
- [ ] Jobs definieren:
  ```
  Job {
    Name = "Full Backup"
    JobDefs = "DefaultJob"
    Level = Full
    Schedule = "WeeklyCycle"
    RunScript { Command = "pre-backup-check" }
  }
  ```
- [ ] Volumes und Pools
- [ ] Katalog (Database) Setup
- [ ] bconsole für Backup-Kontrolle

### Phase 4: Backup-Jobs Konfigurieren (Tag 9-10)
- [ ] Mehrere Clients hinzufügen
- [ ] Verschiedene Job-Typen:
  - [ ] Full Backups (Weekly)
  - [ ] Incremental (Daily)
  - [ ] Differential (Semi-daily)
- [ ] Schedules definieren
- [ ] Retention-Policies setzen
- [ ] Backup-Prioritäten
- [ ] Parallel-Jobs

### Phase 5: Restore & Recovery (Tag 11-12)
- [ ] Verschiedene Restore-Szenarien:
  - [ ] Einzelne Datei
  - [ ] Verzeichnis
  - [ ] Kompletter Filesystem
  - [ ] Kompletter Server
- [ ] Restore-Jobs durchführen
- [ ] Alternativer Restore-Ort
- [ ] Restore-Verificaton
- [ ] Point-in-Time Recovery üben

### Phase 6: Encryption & Security (Tag 13)
- [ ] Backup-Verschlüsselung:
  ```
  Storage {
    Name = MyStorage
    ...
    TLS Require = yes
    TLS Certificate = /etc/bareos/certs/storage.pem
  }
  ```
- [ ] TLS für Client-Server Kommunikation
- [ ] Passwort-Schutz für Backups
- [ ] Verschlüsselte Backups testen
- [ ] Key Management

### Phase 7: Off-site Backups (Tag 14)
- [ ] Externe Backup-Storage:
  - [ ] NAS
  - [ ] Cloud Storage (S3, Azure)
  - [ ] Tape (optional)
- [ ] Restic für Cloud-Backups:
  ```bash
  restic -r s3:s3.amazonaws.com/bucket init
  restic -r s3:s3.amazonaws.com/bucket backup /home/
  ```
- [ ] Verschlüsselung bei Cloud-Backups
- [ ] Bandbreiten-Management
- [ ] Kosten-Analyse

### Phase 8: Disaster Recovery Planung (Tag 15-16)
- [ ] DR Runbook erstellen
- [ ] Recovery Procedures:
  - [ ] Hardware-Fehler
  - [ ] Datenbank-Corruption
  - [ ] Ransomware/Sicherheitsvorfall
  - [ ] Kompletter Datencenter-Ausfall
- [ ] Recovery-Testing durchführen
- [ ] Recovery-Zeitestimate
- [ ] Automatisierte Recovery (Disaster Recovery Automation)

### Phase 9: Monitoring & Verification (Tag 17)
- [ ] Backup-Job Logs analysieren
- [ ] Failed Jobs identifizieren und beheben
- [ ] Catalog-Integrität überprüfen:
  ```bash
  dbcheck
  ```
- [ ] Regelmäßige Restore-Tests
- [ ] Monitoring und Alerting für Backups
- [ ] SLA-Compliance überprüfen

### Phase 10: Praxisprojekt: Enterprise Backup (Tag 18-20)
- [ ] Mehrere Server mit verschiedenen Backup-Profilen
- [ ] Mix von Full, Incremental, Differential
- [ ] Off-site Backups
- [ ] Encryption und TLS
- [ ] Disaster Recovery Simulations
- [ ] Dokumentierte Runbooks

## ✅ Bewertungskriterien
- **Strategie:** Backup-Plan dokumentiert mit RPO/RTO
- **Implementierung:** Backups laufen regelmäßig und erfolgreich
- **Restore:** Recovery-Tests erfolgreich durchführen
- **Sicherheit:** Verschlüsslung, TLS, Access Control
- **Monitoring:** Backup-Status überwacht, Alerts funktionieren
- **Dokumentation:** Runbooks, Recovery-Procedures dokumentiert

## 🔐 Sicherheits-Best-Practices
- [ ] Backups immer verschlüsseln
- [ ] TLS für Backup-Übertragung
- [ ] Off-site Backups (nicht lokal nur)
- [ ] Separate Credentials für Backup-Zugriff
- [ ] Regelmäßig Recovery-Tests durchführen
- [ ] Backups vor Ransomware schützen (immutable, air-gapped)

## 📚 Ressourcen & Dokumentation

### Wichtige Tools
- **Bacula/Bareos** - Enterprise Backup
- **Restic** - Modern, einfach, verschlüsselt
- **Duplicity** - Encrypted incremental backups
- **rsync** - Simple file sync
- **Amanda** - Network backup system

### Wichtige Befehle
```bash
# Rsync
rsync -av /source/ /dest/

# Bareos
bconsole
*run job="Full Backup"
*restore
*estimate job="JobName"

# Restic
restic backup /path/
restic restore latest -t /restore/

# Testing
*show schedule
*estimate job="JobName"
```

### Wichtige Dateien
- `/etc/bareos/bareos-dir.conf` - Director Config
- `/etc/bareos/bareos-sd.conf` - Storage Daemon Config
- `/etc/bareos/bareos-fd.conf` - File Daemon Config

## 💡 Hands-On Labs

### Lab 1: Rsync Basis-Backups
- Full + Incremental Backups mit Rsync
- Automatische tägliche Backups
- Recovery aus Backup
- Bandwidth Limiting

### Lab 2: Bacula kompletter Stack
- Bacula Director, Storage, File Daemon
- Multiple Clients
- Full + Incremental Schedule
- Restore-Tests

### Lab 3: Disaster Recovery Szenario
- Simulieren Sie einen Festplattenfehler
- Kompletten Server aus Backup wiederherstellen
- Überprüfen Sie Datenkonsistenz
- Dokumentieren Sie Zeit zum Recovery (RTO)

### Lab 4: Cloud-Backups
- Restic mit Cloud-Storage (S3, B2)
- Verschlüsselte off-site Backups
- Verschlüsselung überprüfen
- Restore aus Cloud

## 💡 Trainer-Tipps
- Zeigen Sie echte Disaster-Szenarien (Festplattenausfall, Ransomware)
- Lassen Sie Umschüler Recovery durchführen, nicht nur Backups nehmen
- Demonstrieren Sie die Bedeutung von "regelmäßigen Tests"
- Zeigen Sie Backup-Kosten vs. Datenverlust-Kosten

## 📋 Deliverables
1. **Backup-Strategie:** Dokumentierter Plan mit RPO/RTO
2. **Backup-Konfiguration:** Bacula/Restic/Rsync Configs
3. **Recovery Runbooks:** Schritt-für-Schritt Recovery Guides
4. **Test-Reports:** Backup & Recovery Tests dokumentiert
5. **Monitoring-Setup:** Alerts und Logging für Backups

---

**Projektstand:** [ ] Nicht begonnen | [ ] In Arbeit | [ ] Abgeschlossen

**Notizen:**
