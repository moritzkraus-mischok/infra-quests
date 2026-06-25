# Projekt 9: BIND DNS Server

## 📋 Projektbeschreibung
Aufbau und Verwaltung eines produktiven DNS-Servers. DNS ist eine kritische Infrastruktur-Komponente, die jeder Systemintegrator verstehen muss.

## 🎯 Lernziele
- BIND9 Installation und Konfiguration
- Authoritative DNS Zones
- Zone-Dateien erstellen und pflegen
- DNS Records (A, AAAA, CNAME, MX, TXT, SRV)
- DNSSEC implementieren
- Recursive DNS Server
- DNS Logging und Monitoring
- Häufige DNS-Probleme beheben

## 📊 Schwierigkeitsgrad
**Fortgeschritten**

## ⏱️ Dauer
2-3 Wochen

## 🔧 Anforderungen
- Ubuntu Server 22.04 LTS
- Eine Domain (kann auch Subdomain oder lokal sein)
- Grundverständnis: DNS-Konzepte, Netzwerk
- Texteditor

## 📝 Aufgaben

### Phase 1: BIND Installation & Grundlagen (Tag 1-2)
- [ ] BIND9 installieren: `sudo apt install bind9 bind9-utils`
- [ ] BIND Architektur verstehen (Authoritative, Recursive, Caching)
- [ ] `/etc/bind/` Verzeichnis kennenlernen
- [ ] `named.conf` Hauptkonfiguration verstehen
- [ ] BIND Service starten: `sudo systemctl start bind9`
- [ ] Bind-Version prüfen: `named -v`
- [ ] Query-Tools:
  ```bash
  nslookup
  dig
  host
  ```

### Phase 2: Zone-Datei erstellen (Tag 3-4)
- [ ] Zone-Datei Syntax verstehen
- [ ] Example Zone für `example.com` erstellen:
  ```
  $TTL    604800
  @       IN      SOA     ns1.example.com. admin.example.com. (
                          2024010101      ; serial
                          604800          ; refresh
                          86400           ; retry
                          2419200         ; expire
                          604800 )        ; minimum
  
            IN      NS      ns1.example.com.
            IN      NS      ns2.example.com.
  
  ns1       IN      A       192.168.1.10
  ns2       IN      A       192.168.1.11
  
  @         IN      A       192.168.1.100
  www       IN      A       192.168.1.100
  mail      IN      A       192.168.1.20
  
  @         IN      MX      10 mail.example.com.
  ```
- [ ] Verschiedene Record-Types verstehen:
  - [ ] A (IPv4)
  - [ ] AAAA (IPv6)
  - [ ] CNAME (Alias)
  - [ ] MX (Mail Exchange)
  - [ ] TXT (Text Records, SPF, DKIM)
  - [ ] SRV (Service)
  - [ ] NS (Name Server)
  - [ ] SOA (Start of Authority)

### Phase 3: BIND Zones konfigurieren (Tag 5-6)
- [ ] `/etc/bind/named.conf.local` editieren:
  ```
  zone "example.com" {
    type master;
    file "/etc/bind/zones/db.example.com";
  };
  ```
- [ ] Zone-Dateien in `/etc/bind/zones/` erstellen
- [ ] Zone-Syntax prüfen: `named-checkzone example.com /etc/bind/zones/db.example.com`
- [ ] BIND neu laden: `sudo systemctl reload bind9`
- [ ] Zone-Transfer testen: `dig @localhost example.com`

### Phase 4: Reverse DNS Zones (Tag 7)
- [ ] Reverse Zone für Subnetz erstellen (z.B. 1.168.192.in-addr.arpa)
- [ ] Reverse DNS Records (PTR)
- [ ] Zone-Datei:
  ```
  1.168.192.in-addr.arpa
  100 PTR www.example.com.
  20  PTR mail.example.com.
  ```
- [ ] Reverse Lookup testen: `nslookup 192.168.1.100`
- [ ] Reverse Zone in named.conf.local

### Phase 5: DNS Records in Praxis (Tag 8-9)
- [ ] Mail-Setup (MX Records)
- [ ] SPF Records für Mail-Sicherheit
  ```
  TXT: v=spf1 mx -all
  ```
- [ ] DKIM Records vorbereiten
- [ ] DMARC Records
- [ ] Wildcard Records:
  ```
  *.example.com  IN  A  192.168.1.100
  ```
- [ ] ALIAS Records (wenn supported)

### Phase 6: DNSSEC (Day 10-11)
- [ ] DNSSEC Konzepte verstehen (KSK, ZSK)
- [ ] DNSSEC aktivieren für Zone:
  ```bash
  sudo dnssec-keygen -a RSASHA256 -b 2048 -f KSK example.com
  sudo dnssec-keygen -a RSASHA256 -b 1024 example.com
  ```
- [ ] Zone signieren: `dnssec-signzone`
- [ ] DS Records für Parent-Zone generieren
- [ ] DNSSEC Validation testen:
  ```bash
  dig +dnssec example.com
  delv @localhost example.com
  ```

### Phase 7: Recursive DNS & Caching (Tag 12)
- [ ] Recursive Queries konfigurieren (falls gewünscht)
- [ ] Forwarders definieren:
  ```
  forwarders {
    8.8.8.8;
    8.8.4.4;
  };
  ```
- [ ] Caching-Parameter konfigurieren
- [ ] ACLs für Recursive Queries (nicht offen zur Welt!)

### Phase 8: Logging & Troubleshooting (Tag 13-14)
- [ ] DNS Logging aktivieren:
  ```
  logging {
    channel default_file {
      file "/var/log/named/default.log" versions 3 size 250m;
      severity dynamic;
      print-time yes;
    };
    category default { default_file; };
  };
  ```
- [ ] Logs analysieren: `tail -f /var/log/named/default.log`
- [ ] Query Logging für Debugging
- [ ] Häufige Probleme:
  - [ ] Zone Transfer fehlgeschlagen
  - [ ] Record nicht gefunden
  - [ ] Syntax Fehler in Zone-Dateien
  - [ ] Permission-Probleme

### Phase 9: Monitoring & Automation (Tag 15)
- [ ] BIND Status überwachen
- [ ] Automated Zone-Updates (Dynamic DNS, optional)
- [ ] Zone-File Backups
- [ ] Zone-Reload-Tests
- [ ] nagios/icinga Plugins für DNS Monitoring

## ✅ Bewertungskriterien
- **Installation:** BIND läuft und antwortet auf Queries
- **Zones:** Zones korrekt konfiguriert und funktional
- **Records:** Alle Record-Types funktionieren korrekt
- **Reverse DNS:** PTR Records auflösen korrekt
- **DNSSEC:** DNSSEC aktiviert und validiert
- **Logging:** Logs werden gesammelt und analysiert
- **Dokumentation:** Zone-Dateien und Konfiguration dokumentiert

## 🔐 Sicherheits-Best-Practices
- [ ] DNSSEC aktivieren
- [ ] Zone Transfer nur auf Secondary NS
- [ ] Recursive Queries limitieren (ACLs)
- [ ] AXFR nur auf authorized Clients
- [ ] Query Logging für Sicherheits-Audit
- [ ] Regelmäßige Zone-Integrität Checks

## 📚 Ressourcen & Dokumentation

### Wichtige Dateien
- `/etc/bind/named.conf` - Main Configuration
- `/etc/bind/named.conf.local` - Local Zone Definitions
- `/etc/bind/zones/db.example.com` - Zone Database Files
- `/var/log/named/` - Logs

### Wichtige Befehle
```bash
# Configuration Check
named-checkconf /etc/bind/named.conf
named-checkzone example.com /etc/bind/zones/db.example.com

# Service Control
sudo systemctl restart bind9
sudo systemctl reload bind9

# Query Tools
nslookup example.com @127.0.0.1
dig example.com @127.0.0.1
host example.com 127.0.0.1

# Zone Transfer
dig @ns1.example.com example.com axfr

# DNSSEC
dnssec-keygen -a RSASHA256 -b 2048 -f KSK example.com
dnssec-signzone -o example.com -k Kexample.com.+008+12345.key db.example.com
```

## 💡 Hands-On Labs

### Lab 1: Einfache Zone
- Zone für `mycompany.local` erstellen
- A, CNAME, MX Records definieren
- Clients konfigurieren DNS auf Server
- DNS-Queries testen

### Lab 2: Mehrere Zones
- Mehrere Domains hosten
- Reverse DNS für Subnetz
- Recursive Queries vs. Authoritative
- Zone Transfer zu Secondary Server

### Lab 3: DNSSEC & Sicherheit
- DNSSEC für Zone aktivieren
- DNSSEC Validation testen
- DS Records generieren
- Signing-Key Rotation

## 💡 Trainer-Tipps
- Nutzen Sie `dig` für tieferes Debugging als `nslookup`
- Zeigen Sie echte Zone-Dateien aus Produktionsumgebungen
- Demonstrieren Sie DNS Propagation Delays
- Lassen Sie Umschüler DNS-Probleme debuggen (z.B. MX Record nicht gefunden)

## 📋 Deliverables
1. **Zone-Dateien:** Vollständig konfigurierte Zones
2. **named.conf:** Dokumentierte BIND-Konfiguration
3. **DNSSEC Setup:** Signings Keys und DS Records
4. **Troubleshooting-Guide:** Häufige Fehler und Lösungen
5. **Betriebshandbuch:** Zone-Management Prozeduren

---

**Projektstand:** [ ] Nicht begonnen | [ ] In Arbeit | [ ] Abgeschlossen

**Notizen:**
