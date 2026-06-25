# Projekt 5: Samba/NFS Dateifreigaben

## 📋 Projektbeschreibung
Einrichtung von Netzwerk-Dateisystemen für Linux-zu-Windows und Linux-zu-Linux Umgebungen. Zentral für Datenaustausch in heterogenen Netzwerken.

## 🎯 Lernziele
- Samba (SMB/CIFS) für Windows-Kompatibilität
- NFS (Network File System) für Linux-Netzwerke
- Freigabe-Konfiguration und Berechtigungen
- Benutzer-Authentifizierung und ACLs
- Performance-Optimierung
- Häufige Probleme debuggen und beheben

## 📊 Schwierigkeitsgrad
**Fortgeschritten**

## ⏱️ Dauer
2-3 Wochen

## 🔧 Anforderungen
- Ubuntu Server 22.04 LTS (als Server)
- Windows-VM oder physischer PC (für Samba-Tests)
- Linux-VMs (für NFS-Tests)
- Grundverständnis: Netzwerk, Berechtigungen

## 📝 Aufgaben

### Phase 1: Samba Installation & Grundlagen (Tag 1-3)
- [ ] Samba installieren: `sudo apt install samba samba-tools`
- [ ] Samba-Konfig verstehen: `/etc/samba/smb.conf`
- [ ] Samba-Benutzer erstellen:
  ```bash
  sudo smbpasswd -a username
  ```
- [ ] Samba-Syntax prüfen: `testparm`
- [ ] Samba-Service starten: `sudo systemctl start smbd`
- [ ] Freigaben auflisten: `smbclient -L localhost`

### Phase 2: Samba Freigaben konfigurieren (Tag 4-6)
- [ ] Öffentliche Freigabe (read-only):
  ```ini
  [public]
  path = /srv/samba/public
  browseable = yes
  read only = yes
  guest ok = yes
  ```
- [ ] Benutzer-Freigabe (mit Authentication):
  ```ini
  [users]
  path = /srv/samba/users
  browseable = yes
  read only = no
  valid users = alice, bob
  ```
- [ ] Gruppen-Freigabe (mit Gruppen-Berechtigungen)
- [ ] Home-Verzeichnis-Freigabe
- [ ] Drucker-Freigabe (optional)
- [ ] Konfiguration testen: `testparm -v`

### Phase 3: Samba Berechtigungen (Tag 7-8)
- [ ] POSIX-Berechtigungen kombiniert mit Samba-Rechten
- [ ] Force-Benutzer und Force-Gruppe
- [ ] Create-Mask und Directory-Mask verstehen
- [ ] Vererbte Berechtigungen
- [ ] Freigabe-Level vs. Datei-Level Permissions

### Phase 4: Windows-Zugriff testen (Tag 9)
- [ ] Windows-PC mit Samba verbinden
- [ ] Freigabe mounten: `\\server\share`
- [ ] Read/Write-Berechtigungen überprüfen
- [ ] Verschiedene Benutzer testen
- [ ] Dateien erstellen, bearbeiten, löschen
- [ ] Probleme debuggen (Permissions, Access Denied)

### Phase 5: NFS Installation & Grundlagen (Tag 10-11)
- [ ] NFS-Server installieren: `sudo apt install nfs-kernel-server`
- [ ] NFS-Konfiguration: `/etc/exports`
- [ ] Freigaben exportieren:
  ```
  /srv/nfs/share  192.168.1.0/24(rw,sync,no_root_squash)
  ```
- [ ] Exports laden: `sudo exportfs -a`
- [ ] Exportierte Freigaben anzeigen: `showmount -e localhost`

### Phase 6: NFS Clients mounten (Tag 12-13)
- [ ] NFS-Client installieren: `sudo apt install nfs-common`
- [ ] NFS-Freigabe mounten:
  ```bash
  sudo mount -t nfs server:/srv/nfs/share /mnt/nfs/
  ```
- [ ] Persistent mounten in `/etc/fstab`:
  ```
  server:/srv/nfs/share  /mnt/nfs  nfs  defaults,_netdev  0  0
  ```
- [ ] Mehrere Clients testen
- [ ] Concurrent Access testen
- [ ] Unmount und Re-mount testen

### Phase 7: NFS Sicherheit & Optimierung (Tag 14)
- [ ] NFS-Sicherheitsoptionen:
  - [ ] `no_root_squash` vs. `root_squash`
  - [ ] `read-only` vs. `read-write`
  - [ ] `sync` vs. `async`
- [ ] UID/GID Mapping über NFSv4 mit Kerberos (optional)
- [ ] Firewall-Regeln für NFS (Port 111, 2049)
- [ ] Performance-Tuning (rsize, wsize)
- [ ] Logging und Monitoring

### Phase 8: Troubleshooting & Praxisszenarien (Tag 15)
- [ ] Häufige Probleme:
  - [ ] Permission Denied beim Zugriff
  - [ ] Langsame Transfers
  - [ ] Client kann nicht mounten
  - [ ] Timeout-Fehler
- [ ] Debug-Tools: `showmount`, `nfsstat`, `rpcinfo`
- [ ] Log-Analyse: `/var/log/syslog`

## ✅ Bewertungskriterien
- **Samba:** Installation, Konfiguration, Freigaben funktionieren
- **Windows-Zugriff:** Freigaben erreichbar von Windows, Berechtigungen funktionieren
- **NFS:** Installation, Export, Client-Mounting funktioniert
- **Sicherheit:** Berechtigungen korrekt, kein überflüssiger Zugriff
- **Debugging:** Kann Fehler systematisch beheben
- **Dokumentation:** Konfiguration ausführlich dokumentiert

## 🔐 Sicherheits-Best-Practices
- [ ] `root_squash` aktiviert (verhindert Root-Privileleg auf NFS)
- [ ] Berechtigungen begrenzen (nicht 777)
- [ ] Firewall für NFS Port 2049
- [ ] SMB-Signing aktivieren (SMB 3.0+)
- [ ] Samba-Benutzer ohne Shell-Zugriff
- [ ] Verschlüsselung für SMB3

## 📚 Ressourcen & Dokumentation

### Wichtige Dateien
- `/etc/samba/smb.conf` - Samba-Konfiguration
- `/etc/exports` - NFS-Freigabe-Definition
- `/etc/fstab` - Persistente Mounts

### Wichtige Befehle
```bash
# Samba
sudo smbpasswd -a user
sudo smbpasswd -d user  # disable
testparm
testparm -v
smbclient -L server
sudo systemctl restart smbd

# NFS Server
sudo exportfs -a
showmount -e localhost
sudo systemctl restart nfs-server

# NFS Client
sudo mount -t nfs server:/path /mnt/
sudo umount /mnt/
sudo showmount -e server
nfsstat
```

## 💡 Hands-On Labs

### Lab 1: Samba für gemischte Umgebung
- 3 Benutzer (alice, bob, charlie)
- Öffentliche Freigabe (alle read-only)
- Team-Freigabe (alice + bob read-write, charlie read-only)
- Home-Freigaben für jeden

### Lab 2: NFS für Linux-Cluster
- NFS-Server mit 2 Freigaben
- 3 NFS-Clients mounten beide
- Concurrent File-Zugriff testen
- Performance-Tests durchführen

### Lab 3: Mixed Setup
- Samba für Windows-Clients
- NFS für Linux-Clients
- Zentrale Datenspeicherung
- Automatisches Mounting beim Boot

## 💡 Trainer-Tipps
- Zeigen Sie echte Integrations-Probleme: Windows versteht `no_root_squash` nicht
- Demonstrieren Sie Performance-Unterschiede: SMB vs. NFS
- Lassen Sie Umschüler echte Fehler beheben (z.B. "Zugriff verweigert")
- Ergänzen Sie mit Samba-Tool für GUI-Management

## 📋 Deliverables
1. **Samba-Dokumentation:** smb.conf mit Kommentaren
2. **NFS-Dokumentation:** exports mit Erklärung
3. **Troubleshooting-Guide:** Häufige Probleme und Lösungen
4. **Test-Bericht:** Funktionierende Freigaben und Berechtigungen
5. **Performance-Report:** Benchmark-Ergebnisse

---

**Projektstand:** [ ] Nicht begonnen | [ ] In Arbeit | [ ] Abgeschlossen

**Notizen:**
