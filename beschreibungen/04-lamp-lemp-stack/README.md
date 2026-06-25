# Projekt 4: LAMP/LEMP Stack Deployment

## 📋 Projektbeschreibung
Aufbau eines produktionsreifen Web-Application Stacks. LAMP (Linux, Apache, MySQL, PHP) oder LEMP (Linux, Nginx, MySQL, PHP) sind Standard-Architekturen für Web-Services.

## 🎯 Lernziele
- Apache oder Nginx Installation und Konfiguration
- MySQL/MariaDB Datenbankserver einrichten
- PHP-Umgebung konfigurieren
- Virtual Hosts / Server Blocks verstehen
- SSL/TLS mit Let's Encrypt
- Web-Anwendungen deployen (z.B. WordPress, Nextcloud)
- Performance-Optimierung

## 📊 Schwierigkeitsgrad
**Fortgeschritten**

## ⏱️ Dauer
2-3 Wochen

## 🔧 Anforderungen
- Ubuntu Server 22.04 LTS
- Grundverständnis: HTTP, DNS, Netzwerk
- Texteditor (nano, vim)
- Domain oder Subdomain (oder lokal testen)
- Mindestens 2GB RAM, 20GB Disk

## 📝 Aufgaben

### Phase 1: Apache Webserver (LAMP) oder Nginx (LEMP) (Tag 1-3)
**Wähle eine Variante:**

#### Option A: Apache (LAMP)
- [ ] Apache installieren: `sudo apt install apache2`
- [ ] Module aktivieren:
  ```bash
  sudo a2enmod rewrite
  sudo a2enmod ssl
  sudo a2enmod proxy
  ```
- [ ] Virtual Hosts konfigurieren in `/etc/apache2/sites-available/`
- [ ] `.htaccess` verstehen und nutzen
- [ ] Apache-Syntax prüfen: `apache2ctl configtest`

#### Option B: Nginx (LEMP)
- [ ] Nginx installieren: `sudo apt install nginx`
- [ ] Server-Blocks in `/etc/nginx/sites-available/` erstellen
- [ ] Nginx-Syntax prüfen: `sudo nginx -t`
- [ ] Performance-Tuning (Worker, Caching)

### Phase 2: MySQL/MariaDB Setup (Tag 4-5)
- [ ] Installation: `sudo apt install mysql-server` oder `mariadb-server`
- [ ] Initial-Setup: `sudo mysql_secure_installation`
  - [ ] Root-Passwort setzen
  - [ ] Anonyme User löschen
  - [ ] Remote Root-Login deaktivieren
  - [ ] Test-Datenbanken löschen
- [ ] Datenbank und User erstellen:
  ```sql
  CREATE DATABASE myapp;
  CREATE USER 'appuser'@'localhost' IDENTIFIED BY 'secure_password';
  GRANT ALL PRIVILEGES ON myapp.* TO 'appuser'@'localhost';
  FLUSH PRIVILEGES;
  ```
- [ ] Backup-Strategie (mysqldump, Automation)

### Phase 3: PHP-Umgebung (Tag 6-7)
- [ ] PHP installieren: `sudo apt install php php-mysql php-fpm`
- [ ] PHP-Module für Anwendungen:
  ```bash
  sudo apt install php-curl php-gd php-mbstring php-xml php-zip
  ```
- [ ] PHP-Konfiguration prüfen: `phpinfo();`
- [ ] Dateirechte: `/var/www/html/` mit `www-data` user
- [ ] Upload-Limits einstellen in `php.ini`

### Phase 4: Virtual Hosts / Server Blocks (Tag 8-9)
- [ ] Domain 1 (z.B. example.com) konfigurieren
- [ ] Domain 2 (z.B. app.example.com) konfigurieren
- [ ] Jede Domain mit eigenem Dokumenten-Verzeichnis
- [ ] Test mit `/var/www/domain1/index.html`
- [ ] DNS für lokale Tests in `/etc/hosts` eintragen

### Phase 5: SSL/TLS mit Let's Encrypt (Tag 10-11)
- [ ] Certbot installieren: `sudo apt install certbot python3-certbot-apache` (oder nginx)
- [ ] Zertifikat generieren:
  ```bash
  sudo certbot certonly --standalone -d example.com -d www.example.com
  ```
- [ ] Apache/Nginx für HTTPS konfigurieren
- [ ] Auto-Renewal testen: `sudo certbot renew --dry-run`
- [ ] HTTP → HTTPS Redirect
- [ ] HSTS Header hinzufügen

### Phase 6: Web-Anwendung Deployment (Tag 12-14)
**Wähle eine Anwendung:**

#### Option A: WordPress
- [ ] WordPress herunterladen
- [ ] wp-config.php konfigurieren
- [ ] Installation durchführen
- [ ] Themes und Plugins installieren
- [ ] Permalink-Struktur konfigurieren

#### Option B: Nextcloud
- [ ] Nextcloud herunterladen
- [ ] Datenbank-Setup
- [ ] Installation durchführen
- [ ] Storage-Konfiguration

#### Option C: Simple PHP-App selbst bauen
- [ ] CRUD-Anwendung schreiben (z.B. Todo-Liste)
- [ ] MySQL-Integration
- [ ] Formular-Verarbeitung
- [ ] Datei-Upload

### Phase 7: Performance & Sicherheit (Tag 15)
- [ ] Caching aktivieren (Browser, Server)
- [ ] Gzip-Kompression
- [ ] Database-Indizes
- [ ] Security-Header (X-Frame-Options, CSP)
- [ ] Log-Analyse und Monitoring

## ✅ Bewertungskriterien
- **Installation:** Alle Komponenten korrekt installiert
- **Konfiguration:** Virtual Hosts/Server Blocks funktionieren
- **Datenbank:** User, Datenbanken, Backups konfiguriert
- **SSL:** HTTPS funktioniert, gültiges Zertifikat
- **Anwendung:** Web-App läuft stabil und ist erreichbar
- **Sicherheit:** Sichere Konfiguration, Standardhärtung durchgeführt
- **Dokumentation:** Installation und Konfiguration dokumentiert

## 🔐 Sicherheits-Checklist
- [ ] Root-Login für MySQL deaktiviert
- [ ] Standard-Accounts gelöscht (WordPress admin, etc.)
- [ ] File-Permissions korrekt gesetzt
- [ ] HTTPS aktiviert und erzwungen
- [ ] Security-Headers konfiguriert
- [ ] Regelmäßige Backups eingerichtet
- [ ] Logs überprüft auf verdächtige Aktivitäten

## 📚 Ressourcen & Dokumentation

### Wichtige Dateien
**Apache:**
- `/etc/apache2/apache2.conf` - Main Config
- `/etc/apache2/sites-available/` - Virtual Hosts
- `/etc/apache2/mods-enabled/` - Module

**Nginx:**
- `/etc/nginx/nginx.conf` - Main Config
- `/etc/nginx/sites-available/` - Server Blocks

**PHP:**
- `/etc/php/8.x/fpm/php.ini` - PHP Config
- `/etc/php/8.x/cli/php.ini` - CLI Config

**MySQL:**
- `/etc/mysql/mysql.conf.d/mysqld.cnf` - Server Config

### Nützliche Befehle
```bash
# Apache
sudo systemctl restart apache2
sudo a2ensite example.com
sudo a2dissite example.com
apache2ctl configtest

# Nginx
sudo systemctl restart nginx
sudo nginx -t

# MySQL
mysql -u root -p
mysqldump -u user -p database > backup.sql

# Certbot
sudo certbot certonly --standalone -d domain.com
sudo certbot renew --dry-run
```

## 💡 Hands-On Übungen

### Übung 1: LAMP-Stack mit WordPress
- Installieren Sie WordPress auf LAMP
- Erstellen Sie 2 virtuelle Hosts
- Implementieren Sie SSL
- WordPress-Plugins installieren und konfigurieren

### Übung 2: LEMP-Stack mit Custom-App
- Setzen Sie LEMP-Stack auf
- Entwickeln Sie eine einfache PHP-CRUD-App
- Datenbank-Integration
- Performanz-Tuning (Caching)

### Übung 3: Sicherheits-Härtung
- Nehmen Sie einen bestehenden LAMP-Stack
- Führen Sie ein Security-Audit durch
- Implementieren Sie Sicherheits-Best-Practices
- Dokumentieren Sie alle Änderungen

## 💡 Trainer-Tipps
- Zeigen Sie die Unterschiede zwischen Apache und Nginx (Flexibilität vs. Performance)
- Lassen Sie Umschüler Load-Tests durchführen (Apache Bench, JMeter)
- Demonstrieren Sie echte Produktions-Konfigurationen
- Zeigen Sie häufige Fehler: File-Permissions, Datenbank-Zugriff, DNS-Probleme

## 📋 Deliverables
1. **Installationsdokumentation:** Schritt-für-Schritt Anleitung
2. **Konfigurationsdateien:** Backup aller wichtigen Configs
3. **Betriebshandbuch:** Wie man die Anwendung wartet
4. **Security-Bericht:** Sicherheits-Audit und Hardening-Schritte
5. **Performance-Report:** Benchmark-Ergebnisse

---

**Projektstand:** [ ] Nicht begonnen | [ ] In Arbeit | [ ] Abgeschlossen

**Notizen:**
