# Projekt 1: Ubuntu Server Setup & Hardening

## 📋 Projektbeschreibung
Installation und Konfiguration eines sicheren Ubuntu Server-Systems von Grund auf. Dieses Projekt vermittelt die Fundamentals der Linux-Systemadministration und Best Practices für Server-Sicherheit.

## 🎯 Lernziele
- Sichere Installation und Partitionierung von Ubuntu Server
- Grundlegende Systemkonfiguration und Bootloader-Management
- SSH-Zugriff konfigurieren und absichern
- Firewall-Regeln mit UFW verstehen und anwenden
- Software-Updates und Patch-Management durchführen
- Automatisierte Backups mit rsync einrichten

## 📊 Schwierigkeitsgrad
**Anfänger → Fortgeschritten**

## ⏱️ Dauer
1-2 Wochen

## 🔧 Anforderungen
- VirtualBox/KVM VM oder physischer Server
- Ubuntu Server 22.04 LTS oder aktueller
- Mind. 20GB Speicher
- Internetzugang
- Texteditor (nano, vim)

## 📝 Aufgaben

### Phase 1: Installation (Tag 1-2)
- [ ] Ubuntu Server ISO herunterladen
- [ ] VM/Server erstellen mit verschiedenen Partitionierungsoptionen testen
  - [ ] Standard LVM
  - [ ] Custom Partitionierung
- [ ] Systemsprache, Tastaturlayout, Zeitzone konfigurieren
- [ ] Netzwerk-Einstellungen vornehmen
- [ ] Software-Auswahl (SSH-Server, build-essential)

### Phase 2: Initiale Konfiguration (Tag 3-4)
- [ ] Systemupdate durchführen: `sudo apt update && sudo apt upgrade`
- [ ] Hostname setzen: `/etc/hostname`, `/etc/hosts`
- [ ] Statische IP-Adresse konfigurieren (netplan)
- [ ] Sudo-Benutzer erstellen (nicht als root arbeiten)
- [ ] Root-Login per SSH deaktivieren

### Phase 3: SSH-Hardening (Tag 5-6)
- [ ] SSH-Key-Pair generieren (RSA 4096 oder Ed25519)
- [ ] Public Key in `~/.ssh/authorized_keys` eintragen
- [ ] SSH-Config anpassen:
  - [ ] Port ändern (z.B. 2222 statt 22)
  - [ ] PermitRootLogin no
  - [ ] PasswordAuthentication no
  - [ ] PubkeyAuthentication yes
- [ ] SSH-Dienst neu starten und testen

### Phase 4: Firewall-Setup (Tag 7-8)
- [ ] UFW aktivieren: `sudo ufw enable`
- [ ] Regeln definieren:
  - [ ] SSH-Port erlauben (neuer Port)
  - [ ] HTTP/HTTPS öffnen (falls Web-Service später)
  - [ ] Logging aktivieren
- [ ] Firewall-Status überprüfen: `sudo ufw status verbose`

### Phase 5: Updates & Backups (Tag 9-10)
- [ ] Automatische Updates aktivieren:
  ```bash
  sudo apt install unattended-upgrades
  sudo dpkg-reconfigure -plow unattended-upgrades
  ```
- [ ] Cron-Job für automatische Backups:
  ```bash
  0 2 * * * rsync -av /home/ /backup/home/ --delete
  ```
- [ ] Backup-Lösung testen (Recovery durchführen)

### Phase 6: Sicherheits-Audits (Tag 11-12)
- [ ] fail2ban installieren und konfigurieren
- [ ] Log-Datei analysieren: `/var/log/auth.log`
- [ ] Sicherheits-Checklist durchgehen (siehe unten)

## ✅ Bewertungskriterien
- **Installation:** System läuft stabil, alle Partitionen richtig
- **Netzwerk:** Statische IP eingestellt, Konnektivität hergestellt
- **SSH:** Passwort-Login deaktiviert, nur Key-Auth aktiv
- **Firewall:** Alle Regeln dokumentiert und funktionsfähig
- **Backups:** Automated Backup läuft, Recovery getestet
- **Dokumentation:** Alle Schritte dokumentiert, Screenshots bei wichtigen Konfigurationen

## 🔐 Sicherheits-Checklist
- [ ] Root-Konto deaktivieren (nur sudo verwenden)
- [ ] SSH auf Non-Standard-Port
- [ ] Firewall aktiv mit restriktiven Rules
- [ ] Regelmäßige Updates aktiviert
- [ ] fail2ban gegen Brute-Force aktiv
- [ ] Backups vorhanden und getestet
- [ ] Logs regelmäßig überprüft

## 📚 Ressourcen & Dokumentation

### Offizielle Dokumentation
- Ubuntu Server Guide: https://ubuntu.com/server/docs
- UFW Dokumentation: https://help.ubuntu.com/community/UFW
- SSH Best Practices: https://man7.org/linux/man-pages/man5/sshd_config.5.html

### Wichtige Konfigurationsdateien
- `/etc/ssh/sshd_config` - SSH Server Config
- `/etc/ufw/` - Firewall Rules
- `/etc/hostname` - Hostname
- `/etc/netplan/` - Netzwerk-Konfiguration
- `/etc/apt/apt.conf.d/50unattended-upgrades` - Auto-Updates

### Nützliche Befehle
```bash
# System-Info
uname -a
lsb_release -a
df -h

# Netzwerk
ip a show
netplan apply
systemctl restart networking

# SSH
ssh -i ~/.ssh/id_ed25519 -p 2222 user@server
sudo systemctl restart ssh

# Firewall
sudo ufw status numbered
sudo ufw allow 2222/tcp
```

## 🚀 Alternative: Cloud-Init Automatisierung

Cloud-init ermöglicht vollautomatische Server-Initialisierung. Dies ist eine Vorschau auf Infrastructure as Code (wird in Projekt 10 & 13 vertieft).

### Cloud-Init User-Data Script
Statt manueller Schritte: Ein User-Data-Skript für automatisiertes Setup:

```yaml
#cloud-config
hostname: ubuntu-server
fqdn: ubuntu-server.local

# System Updates
package_update: true
package_upgrade: true

packages:
  - openssh-server
  - vim
  - curl
  - ufw
  - fail2ban

# Network Configuration
network:
  version: 2
  ethernets:
    eth0:
      dhcp4: false
      addresses:
        - 192.168.1.100/24
      gateway4: 192.168.1.1
      nameservers:
        addresses: [8.8.8.8, 8.8.4.4]

# SSH Key Setup
ssh_authorized_keys:
  - ssh-ed25519 AAAAC3NzaC1lZDI1NTE5... user@localhost

ssh_config:
  Port: 2222
  PermitRootLogin: "no"
  PasswordAuthentication: "no"
  PubkeyAuthentication: "yes"

# Firewall Configuration
runcmd:
  - ufw enable
  - ufw allow 2222/tcp
  - systemctl restart ssh
  - systemctl enable fail2ban
  - fail2ban-client start

# User Management
users:
  - name: ubuntu
    sudo: ALL=(ALL) NOPASSWD:ALL
    ssh_authorized_keys:
      - ssh-ed25519 AAAAC3NzaC1lZDI1NTE5... user@localhost
```

### Praktische Übung: Cloud-Init Lab
- [ ] User-Data-Skript schreiben
- [ ] VM mit cloud-init initialisieren (z.B. in KVM/VirtualBox)
- [ ] Automatische Konfiguration vs. manuelle Konfiguration vergleichen
- [ ] Time-Savings messen

**Hinweis:** Cloud-init wird in Projekten 10 & 13 intensiver eingesetzt.

## 💡 Trainer-Tipps
- Lassen Sie die Umschüler zuerst in einer VM arbeiten, bevor sie auf einem echten Server praktizieren
- Fordern Sie eine "Recovery Übung" ein: Server bewusst beschädigen und reparieren lassen
- Ergänzen Sie mit Hands-On Security-Tests: Nmap-Scan vor/nach Hardening
- Diskutieren Sie Trade-offs: Sicherheit vs. Usability (z.B. Port-Änderung kann Connectivity-Probleme verursachen)
- **Optionale Erweiterung:** Vergleichen Sie Projekt 1 manuell mit cloud-init: Wie viel Zeit sparen Sie?

## 📋 Deliverables
1. **Dokumentation:** Installationsanleitung mit Screenshots
2. **Konfigurationsdateien:** Backup der wichtigsten Config-Files
3. **Runbook:** Schritt-für-Schritt Wiederherstellungsanleitung
4. **Checklisten:** Security-Hardening Checklist

---

**Projektstand:** [ ] Nicht begonnen | [ ] In Arbeit | [ ] Abgeschlossen

**Notizen:**
