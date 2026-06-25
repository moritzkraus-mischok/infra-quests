# Projekt 15: Scripting Projekt - Automation mit Bash/Python

## 📋 Projektbeschreibung
Entwicklung von Automatisierungs-Skripten für häufige System-Administration Aufgaben. Praktische Fähigkeit, die die tägliche Arbeit deutlich effizienter macht.

## 🎯 Lernziele
- Bash Scripting fortgeschritten (nicht nur Grundlagen)
- Python für System-Administration
- Error Handling und Logging
- Argument-Verarbeitung und Konfiguration
- Produktions-ready Code
- Testing von Skripten
- Git für Versionskontrolle
- Script-Distribution und Updates

## 📊 Schwierigkeitsgrad
**Fortgeschritten**

## ⏱️ Dauer
2-3 Wochen

## 🔧 Anforderungen
- Ubuntu Server 22.04 LTS
- Grundverständnis: Bash, Systemadministration
- Optional: Python-Kenntnisse
- Text-Editor oder IDE (VS Code, PyCharm, vim)
- Git grundlegend nutzen können

## 📝 Aufgaben

### Phase 1: Bash Scripting Fundamentals (Tag 1-2)
- [ ] Shebang und Script-Struktur
- [ ] Variablen und Arrays
- [ ] Kontrollfluss: if/else, case, loops
- [ ] Funktionen schreiben
- [ ] Parameter/Argumente verarbeiten: `$1, $2, shift`
- [ ] getopts für optionale Parameter
- [ ] Fehlerbehandlung: exit codes, trap
- [ ] Logging und Debug-Output

### Phase 2: Praktische Bash-Skripte (Tag 3-5)
Schreiben Sie folgende Skripte:

#### Skript 1: Backup-Script
```bash
#!/bin/bash
# backup.sh - Automated backup of directories

SOURCE=$1
DEST=$2
DATE=$(date +%Y%m%d_%H%M%S)
LOGFILE="/var/log/backup_${DATE}.log"

# Argument validation
[[ -z "$SOURCE" || -z "$DEST" ]] && {
  echo "Usage: $0 SOURCE DEST"
  exit 1
}

# Backup mit Fehlerbehandlung
rsync -av "$SOURCE" "$DEST/backup_${DATE}/" 2>&1 | tee "$LOGFILE" || {
  echo "Backup fehlgeschlagen!" >&2
  exit 1
}

echo "Backup erfolgreich: $DEST/backup_${DATE}/"
```

#### Skript 2: User-Management Script
```bash
#!/bin/bash
# user-manage.sh - Benutzer-Verwaltung

case "$1" in
  add)
    [[ $# -ne 3 ]] && { echo "Usage: $0 add USERNAME GROUPS"; exit 1; }
    sudo useradd -m -G "$3" "$2"
    sudo passwd "$2"
    ;;
  del)
    [[ $# -ne 2 ]] && { echo "Usage: $0 del USERNAME"; exit 1; }
    sudo userdel -r "$2"
    ;;
  list)
    getent passwd | cut -d: -f1
    ;;
  *)
    echo "Unknown command: $1"
    exit 1
    ;;
esac
```

#### Skript 3: System-Health Check
```bash
#!/bin/bash
# health-check.sh - System-Überwachung

check_disk() {
  USAGE=$(df / | awk 'NR==2 {print $5}' | sed 's/%//')
  if [[ $USAGE -gt 80 ]]; then
    echo "WARNING: Disk usage at ${USAGE}%"
    return 1
  fi
  return 0
}

check_memory() {
  FREE=$(free | awk '/^Mem:/ {print $7}')
  if [[ $FREE -lt 1000000 ]]; then
    echo "WARNING: Low memory: ${FREE}KB"
    return 1
  fi
  return 0
}

check_disk && check_memory && echo "System OK" || echo "System ISSUES"
```

### Phase 3: Python für System-Administration (Tag 6-8)
- [ ] Python Basics für Sysadmin
- [ ] subprocess Module für Command-Ausführung
- [ ] os und sys Module
- [ ] Datei-Operations
- [ ] Regular Expressions (re)
- [ ] Logging in Python
- [ ] argparse für CLI-Arguments
- [ ] Exception Handling

### Phase 4: Python-Skripte schreiben (Tag 9-11)
Schreiben Sie folgende Python-Skripte:

#### Skript 1: Log-Parser
```python
#!/usr/bin/env python3
import re
import sys
from collections import defaultdict

def parse_access_log(logfile):
    """Parse Apache Access Log"""
    errors = defaultdict(int)
    
    try:
        with open(logfile, 'r') as f:
            for line in f:
                match = re.search(r'(\d{3})', line)
                if match:
                    status = match.group(1)
                    if status.startswith('4') or status.startswith('5'):
                        errors[status] += 1
    except FileNotFoundError:
        print(f"Error: {logfile} nicht gefunden", file=sys.stderr)
        return None
    
    return errors

if __name__ == '__main__':
    if len(sys.argv) != 2:
        print(f"Usage: {sys.argv[0]} LOGFILE")
        sys.exit(1)
    
    errors = parse_access_log(sys.argv[1])
    if errors:
        for status, count in sorted(errors.items()):
            print(f"{status}: {count} Fehler")
```

#### Skript 2: Systemüberwachung
```python
#!/usr/bin/env python3
import psutil
import logging
import sys

logging.basicConfig(level=logging.INFO)

def check_system_health():
    """Prüfe System-Health"""
    
    # CPU
    cpu_percent = psutil.cpu_percent(interval=1)
    if cpu_percent > 80:
        logging.warning(f"High CPU: {cpu_percent}%")
    
    # Memory
    memory = psutil.virtual_memory()
    if memory.percent > 85:
        logging.warning(f"High Memory: {memory.percent}%")
    
    # Disk
    disk = psutil.disk_usage('/')
    if disk.percent > 90:
        logging.warning(f"High Disk: {disk.percent}%")
    
    return cpu_percent < 80 and memory.percent < 85

if __name__ == '__main__':
    healthy = check_system_health()
    sys.exit(0 if healthy else 1)
```

#### Skript 3: Backup-Automator
```python
#!/usr/bin/env python3
import argparse
import subprocess
import logging
from pathlib import Path
from datetime import datetime

def backup_directory(source, destination, name):
    """Backup mit Logging"""
    timestamp = datetime.now().strftime("%Y%m%d_%H%M%S")
    dest_path = Path(destination) / f"{name}_{timestamp}"
    
    logging.info(f"Starting backup: {source} → {dest_path}")
    
    try:
        result = subprocess.run(
            ["rsync", "-av", source, str(dest_path)],
            capture_output=True,
            text=True,
            check=True
        )
        logging.info(f"Backup successful: {dest_path}")
        return True
    except subprocess.CalledProcessError as e:
        logging.error(f"Backup failed: {e.stderr}")
        return False

if __name__ == '__main__':
    parser = argparse.ArgumentParser(description="Backup Script")
    parser.add_argument('source', help='Source directory')
    parser.add_argument('destination', help='Backup destination')
    parser.add_argument('--name', default='backup', help='Backup name')
    
    args = parser.parse_args()
    success = backup_directory(args.source, args.destination, args.name)
    exit(0 if success else 1)
```

### Phase 5: Testing & Error Handling (Tag 12-13)
- [ ] Bash Unit Testing (bats, shunit2)
- [ ] Python unittest/pytest
- [ ] Input Validation
- [ ] Edge Cases testen
- [ ] Error Messages aussagekräftig machen
- [ ] Logging strategisch nutzen
- [ ] Script-Exit-Codes richtig setzen

### Phase 6: Code Quality & Best Practices (Tag 14)
- [ ] Code-Style (ShellCheck für Bash, pylint für Python)
- [ ] Documentation (Kommentare, README)
- [ ] Variable Naming
- [ ] DRY-Prinzip (Don't Repeat Yourself)
- [ ] Security überprüfen (keine hardcoded Passwörter!)
- [ ] Performance-Optimierung

### Phase 7: Versionskontrolle & Distribution (Tag 15)
- [ ] Git Repository erstellen
- [ ] Scripts mit Versionsnummern
- [ ] Changelog erstellen
- [ ] README mit Nutzungs-Dokumentation
- [ ] Installation/Update-Script
- [ ] Distribution (z.B. über Ansible)

### Phase 8: Praxisprojekt: Monitoring-Suite (Tag 16-20)
Erstellen Sie eine komplette Monitoring-Suite aus mehreren Skripten:

1. **System-Health-Check** (Bash)
   - CPU, Memory, Disk
   - Alert bei Schwellenwert-Überschreitung
   
2. **Log-Analyzer** (Python)
   - Parse verschiedene Log-Formate
   - Fehler-Trends identifizieren
   
3. **Backup-Manager** (Bash + Python)
   - Automatisierte tägliche Backups
   - Rotation (altes Backup löschen)
   - Status-Reports
   
4. **Service-Monitor** (Bash)
   - Überprüfe ob kritische Services laufen
   - Auto-Restart bei Fehler
   
5. **Report-Generator** (Python)
   - Wöchentliche Report aus allen Tools
   - Email-Versand

## ✅ Bewertungskriterien
- **Bash Scripts:** Funktionieren, Error-Handling vorhanden
- **Python Scripts:** Python-Best-Practices befolgt
- **Robustheit:** Auch bei falschen Eingaben stabil
- **Dokumentation:** README, Kommentare vorhanden
- **Testing:** Unit-Tests geschrieben und grün
- **Code Quality:** ShellCheck / pylint ohne kritische Warnungen
- **Versionskontrolle:** Git mit sauberen Commits

## 🔐 Sicherheits-Best-Practices
- [ ] Niemals Passwörter in Skripten
- [ ] File-Permissions richtig setzen (740 für Scripts)
- [ ] Input-Validierung gegen Injection-Attacks
- [ ] Sudo mit Vorsicht nutzen (nicht alles als root)
- [ ] Keine sensiblen Daten in Logs
- [ ] SSH-Keys nur mit 600 Permissions

## 📚 Ressourcen & Dokumentation

### Tools
- **ShellCheck:** Bash-Code Quality
- **pylint/flake8:** Python Code Quality
- **bats:** Bash Automated Testing System
- **pytest:** Python Testing Framework
- **GitHub/GitLab:** Hosting und Collaboration

### Wichtige Befehle
```bash
# Bash
bash -x script.sh  # Debug-Modus
shellcheck script.sh

# Python
python3 -m py_compile script.py
pylint script.py
pytest test_script.py
```

## 💡 Hands-On Labs

### Lab 1: Basis-Scripts
- Schreiben Sie 3 praktische Bash-Skripte
- Unit-Tests dafür
- Code-Review (ShellCheck)

### Lab 2: Python-Skripte
- Schreiben Sie 3 Python-Skripte
- pytest Tests
- pylint/flake8 Compliance

### Lab 3: Komplettes Projekt
- Monitoring-Suite aus 5+ Skripten
- Git-Repository mit History
- Dokumentation und Tests
- Automation (z.B. via Cron)

## 💡 Trainer-Tipps
- Zeigen Sie echte Production-Skripte (Redacted)
- Demonstrieren Sie häufige Fehler (unquoted variables, etc.)
- Lassen Sie Umschüler über Edge-Cases nachdenken
- Betonen Sie Readability über Cleverness
- Zeigen Sie die Kraft von Good Logging beim Troubleshooting

## 📋 Deliverables
1. **Skript-Sammlung:** Alle funktionsfähigen Skripte
2. **Git-Repository:** Mit saubener History
3. **Tests:** Unit-Tests für alle Skripte
4. **Dokumentation:** README, Usage-Guide, Troubleshooting
5. **Code-Quality:** ShellCheck / pylint Reports
6. **Integration:** Z.B. Cronjobs, Ansible-Integration

---

**Projektstand:** [ ] Nicht begonnen | [ ] In Arbeit | [ ] Abgeschlossen

**Notizen:**
