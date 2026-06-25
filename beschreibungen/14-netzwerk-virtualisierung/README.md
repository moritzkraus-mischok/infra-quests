# Projekt 14: Netzwerk-Virtualisierung (KVM/Proxmox)

## 📋 Projektbeschreibung
Aufbau einer Virtualisierungs-Plattform für effiziente Ressourcen-Nutzung. Moderne IT-Infrastruktur basiert auf Virtualisierung.

## 🎯 Lernziele
- KVM/QEMU Hypervisor verstehen
- Proxmox VE als Management-Plattform
- Virtual Machine Lifecycle
- Snapshots und Klone
- Live-Migration
- Networking mit virtuellen Komponenten
- Storage-Backends
- Performance-Optimierung

## 📊 Schwierigkeitsgrad
**Fortgeschritten → Expert**

## ⏱️ Dauer
2-3 Wochen

## 🔧 Anforderungen
- Physical Server mit Virtualisierungs-Support (Intel VT-x oder AMD-V)
- Min. 32GB RAM
- 500GB+ Storage
- Ubuntu Server oder Proxmox VE
- Grundverständnis: Linux, Netzwerk, Speicher

## 📝 Aufgaben

### Phase 1: KVM Grundlagen (Tag 1-2)
- [ ] Virtualisierungs-Extensions aktivieren
- [ ] KVM/QEMU installieren: `sudo apt install qemu-kvm libvirt-daemon`
- [ ] Virtualisierung prüfen: `kvm-ok`
- [ ] Libvirt verstehen (Management-Layer über KVM)
- [ ] virt-manager GUI (optional)
- [ ] QEMU-Befehle kennenlernen

### Phase 2: Proxmox VE Installation (Tag 3-4)
- [ ] Proxmox VE installieren (Debian-basiert)
- [ ] Web-GUI verstehen und konfigurieren
- [ ] Cluster-Konzepte (Single Node Start)
- [ ] Netzwerk-Konfiguration
- [ ] Storage-Konfiguration
- [ ] HTTPS/SSL für Proxmox

### Phase 3: Virtual Machines erstellen (Tag 5-6)
- [ ] VM-Templates
- [ ] VM von ISO installieren
- [ ] VM-Ressourcen allokieren:
  - [ ] vCPU Zuordnung
  - [ ] RAM Zuordnung
  - [ ] Storage/Disk Zuordnung
- [ ] Boot-Reihenfolge
- [ ] BIOS vs. UEFI
- [ ] Guest-Tools installieren (QEMU Guest Agent)

### Phase 4: Snapshots & Klone (Tag 7-8)
- [ ] Snapshots verstehen und nutzen
- [ ] VM vor Änderungen snapshotten
- [ ] Snapshot-Rollback
- [ ] Klone von Snapshots
- [ ] Linked Clones für schnelle Provisionierung
- [ ] Template-VMs erstellen

### Phase 5: Networking (Tag 9-10)
- [ ] Virtual Bridges verstehen
- [ ] NAT vs. Bridged Networking
- [ ] vlan-Tagging
- [ ] Mehrere virtuelle Netzwerk-Interfaces
- [ ] PCI Passthrough (advanced, optional)
- [ ] QoS für Netzwerk-Limiting
- [ ] VM-zu-VM Kommunikation

### Phase 6: Storage Backends (Tag 11-12)
- [ ] Verschiedene Storage-Typen in Proxmox:
  - [ ] Local Storage (direkt auf Hypervisor)
  - [ ] iSCSI (Network Block Storage)
  - [ ] NFS (Network File Storage)
  - [ ] Ceph (Distributed, advanced)
- [ ] Storage-Pool konfigurieren
- [ ] Disk I/O Monitoring
- [ ] Thin vs. Thick Provisioning
- [ ] Backup von VMs auf Storage

### Phase 7: Live-Migration & High-Availability (Tag 13-14)
- [ ] Live-Migration zwischen Hosts (wenn Cluster)
- [ ] Storage-Migration
- [ ] VM HA-Policies
- [ ] Automated Recovery bei Host-Fehler
- [ ] Migration-Performance testen
- [ ] Downtime-freie Migrations

### Phase 8: Monitoring & Logging (Tag 15)
- [ ] Proxmox Monitoring Dashboard
- [ ] VM-Ressourcen überwachen
- [ ] Host-Ressourcen überwachen
- [ ] Event-Logging
- [ ] Syslog-Integration
- [ ] Externe Monitoring-Tools (Zabbix, Nagios)

### Phase 9: Backup & Recovery (Tag 16)
- [ ] VM-Backups in Proxmox
- [ ] Backup-Retention Policies
- [ ] Restore aus Backup
- [ ] Incremental Backups
- [ ] Backup-Validierung
- [ ] Off-site Backups

### Phase 10: Praxisprojekt: Multi-Tier Infrastructure (Tag 17-20)
- [ ] 5-10 VMs mit verschiedenen Rollen
- [ ] Netzwerk-Segmentierung zwischen VMs
- [ ] Storage-Pools für verschiedene Workloads
- [ ] Monitoring und Alerting
- [ ] VM-Backups und Recovery-Testing
- [ ] Performance-Tuning

## ✅ Bewertungskriterien
- **Setup:** Proxmox läuft, VMs können erstellt werden
- **VMs:** Multiple VMs mit verschiedenen OSes
- **Snapshots:** Snapshots und Klone funktionieren
- **Networking:** VMs können untereinander und nach außen kommunizieren
- **Monitoring:** VM und Host-Ressourcen überwacht
- **Backup:** Automatisierte VM-Backups und Recovery getestet
- **Dokumentation:** Proxmox-Setup und Verwaltungs-Procedures

## 🔐 Sicherheits-Best-Practices
- [ ] Strong Passwords/Certs für Proxmox
- [ ] Firewall für Proxmox-Management
- [ ] VM-Isolation
- [ ] Encrypted Backups
- [ ] RBAC für Proxmox Multi-User
- [ ] Regelmäßige Proxmox Updates

## 📚 Ressourcen & Dokumentation

### Wichtige Tools & Befehle
```bash
# KVM/Libvirt
virsh list
virsh start vm-name
virsh snapshot-create vm-name
virt-clone

# Proxmox API/CLI
qm list
qm create 100 --name vm-name
qm snapshot 100 --snapname snapshot1
```

### Wichtige Dateien
- `/etc/pve/` - Proxmox Konfiguration
- `/etc/pve/qemu-server/` - VM Configs
- `/var/lib/vz/` - VM Data (default)

## 💡 Hands-On Labs

### Lab 1: Basis-Setup
- Proxmox installieren
- 3 VMs (Ubuntu, CentOS, Debian) erstellen
- Netzwerk-Connectivity testen
- Snapshots und Klone üben

### Lab 2: Multi-Node Cluster (advanced)
- 2-3 Proxmox Hosts in Cluster
- Shared Storage (NFS oder iSCSI)
- Live-Migration testen
- HA-Policies

### Lab 3: Backup & Disaster Recovery
- Automated VM Backups konfigurieren
- Restore-Szenarien üben
- Backup-Validierung
- Disaster-Recovery Time messen

## 💡 Trainer-Tipps
- Zeigen Sie den Vorteil von Snapshots vor großen Änderungen
- Demonstrieren Sie Live-Migration "unter Last"
- Lassen Sie Umschüler VMs vor Experimenten snapshotten
- Zeigen Sie Storage-Performance-Unterschiede

## 📋 Deliverables
1. **Proxmox-Setup:** Dokumentierte Installation und Konfiguration
2. **VM-Templates:** Ready-to-use Template VMs
3. **Backup-Strategie:** Automated Backup-Setup
4. **Runbooks:** VM-Verwaltung und Disaster-Recovery
5. **Performance-Report:** Baseline Metrics und Tuning-Ergebnisse

---

**Projektstand:** [ ] Nicht begonnen | [ ] In Arbeit | [ ] Abgeschlossen

**Notizen:**
