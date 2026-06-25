# Projekt 2: Linux Benutzer- und Rechteverwaltung

## 📋 Projektbeschreibung
Umfassendes Verständnis von Benutzer-, Gruppen- und Dateirechteverwaltung in Linux. Ein zentrales Konzept für Multi-User-Systeme und Sicherheit.

## 🎯 Lernziele
- Benutzer und Gruppen erstellen, modifizieren, löschen
- Dateirechte verstehen und konfigurieren (chmod, chown)
- Sudo-Berechtigungen granular vergeben
- ACLs (Access Control Lists) anwenden
- Passwort-Policies implementieren
- Sicherheits-Logging überwachen

## 📊 Schwierigkeitsgrad
**Anfänger → Fortgeschritten**

## ⏱️ Dauer
1-2 Wochen

## 🔧 Anforderungen
- Ubuntu Server 22.04 LTS
- Administrativen Zugriff (sudo)
- Verständnis grundlegender Linux-Befehle
- VM für Test-Szenarien

## 📝 Aufgaben

### Phase 1: Benutzer-Management (Tag 1-3)
- [ ] Systembenutzer verstehen (root, www-data, etc.)
- [ ] Neue Benutzer erstellen:
  ```bash
  sudo useradd -m -s /bin/bash alice
  sudo passwd alice
  ```
- [ ] Benutzer-Eigenschaften ändern:
  - [ ] Home-Directory wechseln
  - [ ] Shell ändern
  - [ ] GECOS-Info ändern
- [ ] Benutzer löschen und archivieren
- [ ] `/etc/passwd` und `/etc/shadow` verstehen
- [ ] Benutzer-Limits setzen (`ulimit`)

### Phase 2: Gruppen-Management (Tag 4-5)
- [ ] Standard- und Zusatzgruppen verstehen
- [ ] Gruppen erstellen: `sudo groupadd developers`
- [ ] Benutzer zu Gruppen hinzufügen: `sudo usermod -aG developers alice`
- [ ] Gruppenmitgliedschaft verwalten
- [ ] Gruppen-Eigenschaften ändern
- [ ] `/etc/group` und `/etc/gshadow` analysieren

### Phase 3: Dateiberechtigungen - Grundlagen (Tag 6-7)
- [ ] Oktalzahlen verstehen (755, 644, 700)
- [ ] Kategorien kennen: User, Group, Others
- [ ] Berechtigungen auf Dateien setzen:
  ```bash
  chmod 644 document.txt  # rw-r--r--
  chmod 755 script.sh     # rwxr-xr-x
  chmod 700 secrets       # rwx------
  ```
- [ ] Rekursive Änderungen: `chmod -R 755 /var/www`
- [ ] Berechtigungen für Verzeichnisse vs. Dateien

### Phase 4: Ownership (Tag 8)
- [ ] Dateien-Owner wechseln: `chown alice file.txt`
- [ ] Gruppen-Owner wechseln: `chown :developers file.txt`
- [ ] Kombinierte Änderungen: `chown alice:developers file.txt`
- [ ] Rekursive Ownership-Änderungen
- [ ] Umask verstehen und setzen (Standard Berechtigungen)

### Phase 5: Sudo-Konfiguration (Tag 9-10)
- [ ] `/etc/sudoers` sicher bearbeiten: `sudo visudo`
- [ ] Verschiedene Sudo-Szenarien konfigurieren:
  - [ ] Spezifische Benutzer Befehle erlauben
  - [ ] Passwort-freie Befehle
  - [ ] Befehl-Aliase
  - [ ] Gruppen-basierte Regeln
- [ ] Sudo-Logging überprüfen
- [ ] Beispiele:
  ```
  alice ALL=(ALL) /usr/bin/apt
  %developers ALL=(ALL) NOPASSWD: /usr/bin/systemctl
  ```

### Phase 6: ACLs (Access Control Lists) (Tag 11)
- [ ] ACLs aktivieren auf Dateisystem
- [ ] Erweiterte Rechte setzen: `setfacl`
  ```bash
  setfacl -m u:alice:rwx /shared/
  setfacl -m g:developers:rx /data/
  ```
- [ ] ACLs auslesen: `getfacl /path/`
- [ ] Default-ACLs für neue Dateien
- [ ] Praxisbeispiel: Shared Project Folder

### Phase 7: Passwort-Policies (Tag 12)
- [ ] PAM konfigurieren (`/etc/pam.d/`)
- [ ] Passwort-Komplexität erzwingen
- [ ] Ablaufdaten setzen: `chage`
- [ ] Locked-out Benutzer entsperren
- [ ] Login-Versuche limitieren (fail2ban Integration)

## ✅ Bewertungskriterien
- **Benutzer-Ops:** User/Gruppen sauber erstellt und verwaltet
- **Berechtigungen:** Konsistente rwx-Struktur, keine zu lockerer Rechte
- **Sudo:** Least-Privilege Prinzip befolgt, keine `ALL=(ALL)`
- **ACLs:** Korrekt angewendet bei Shared-Resources
- **Dokumentation:** Alle Befehle mit Erklärung dokumentiert
- **Sicherheit:** Keine kritischen Berechtigungsfehler

## 🔐 Sicherheits-Best-Practices
- [ ] Niemals `chmod 777` verwenden
- [ ] Root-Dateien gehören `root:root`
- [ ] Sudo für Unprivileged-Users, nicht `su`
- [ ] Regelmäßige Audit mit: `sudo lastlog`, `sudo faillog`
- [ ] Inaktive Accounts deaktivieren

## 📚 Ressourcen & Dokumentation

### Befehle Referenz
- `useradd`, `usermod`, `userdel` - User Management
- `groupadd`, `groupmod`, `groupdel` - Group Management
- `chmod`, `chown` - Berechtigungen
- `setfacl`, `getfacl` - ACL Management
- `visudo` - Sudo Config (SICHER!)
- `chage`, `passwd` - Passwort Management
- `id`, `groups` - Aktuelle Berechtigungen

### Wichtige Dateien
- `/etc/passwd` - Benutzer-Datenbank
- `/etc/shadow` - Passwort-Hashes (nur root)
- `/etc/group` - Gruppen-Datenbank
- `/etc/sudoers` - Sudo-Regeln (immer mit visudo bearbeiten!)
- `/var/log/auth.log` - Login-Logs

## 💡 Hands-On Übungen

### Szenario 1: Web-Projekt-Team
- Erstellen Sie 3 Benutzer: alice, bob, charlie
- Erstellen Sie Gruppe: developers
- Erstellen Sie `/var/www/project` mit ACLs
- Jeder Entwickler kann lesen/schreiben, aber nicht löschen

### Szenario 2: System-Administration
- Groß alice sudo für `systemctl` ohne Passwort
- Groß bob sudo für `apt` mit Passwort
- charlie darf nur `ls` verwenden

### Szenario 3: Security Audit
- Finden Sie alle Dateien mit `chmod 777`
- Korrigieren Sie Besitz in `/home/`
- Überprüfen Sie `/etc/sudoers` auf schlechte Praktiken

## 💡 Trainer-Tipps
- Lassen Sie Umschüler absichtlich Fehler machen (z.B. `chmod 777`) und dann wieder reparieren
- Demonstrieren Sie Security-Folgen: Ein Webserver mit zu hohen Rechten ist ein kritisches Risiko
- Verwenden Sie Szenarien aus der Praxis (Dev-Teams, System-Administration)
- Zeigen Sie `sudo -l` um aktuelle Berechtigungen zu sehen

## 📋 Deliverables
1. **Dokumentation:** Schrittweise Anleitung aller Operationen
2. **Scripts:** Automatisierungs-Skripte (User-Creation in Bulk)
3. **Audit-Bericht:** Sicherheitsanalyse eines bestehenden Systems
4. **Checklisten:** Best-Practices Checkliste für File-Permissions

---

**Projektstand:** [ ] Nicht begonnen | [ ] In Arbeit | [ ] Abgeschlossen

**Notizen:**
