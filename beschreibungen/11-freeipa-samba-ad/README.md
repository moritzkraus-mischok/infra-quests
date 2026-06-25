# Projekt 11: FreeIPA / Samba AD - Enterprise Identity Management

## 📋 Projektbeschreibung
Zentralisierte Benutzer- und Authentifizierungsverwaltung für Unix/Linux Netzwerke. Alternative zu Microsoft Active Directory mit Open Source Tools.

## 🎯 Lernziele
- FreeIPA Grundlagen und Setup
- LDAP Directory Service
- Kerberos Authentication
- Zentrale Benutzer-Verwaltung
- Samba AD (Samba Active Directory) als AD-Alternative
- Berechtigungen und Policies
- Integration mit Clients
- Häufige Probleme beheben

## 📊 Schwierigkeitsgrad
**Fortgeschritten → Expert**

## ⏱️ Dauer
3-4 Wochen

## 🔧 Anforderungen
- Ubuntu Server 22.04 LTS oder CentOS (FreeIPA auf RHEL besser)
- Min. 4GB RAM, 20GB Disk für FreeIPA Server
- Client-VMs für Joining zum Verzeichnis
- Grundverständnis: LDAP, Kerberos, Active Directory Konzepte

## 📝 Aufgaben

### Phase 1: FreeIPA Installation & Setup (Tag 1-3)
- [ ] Voraussetzungen prüfen (DNS, Hostname)
- [ ] FreeIPA installieren: `sudo apt install freeipa-server freeipa-server-trust-ad`
- [ ] Installation durchführen: `sudo ipa-server-install`
  ```
  Realm: EXAMPLE.COM
  Directory Manager password: (starkes Passwort)
  IPA admin password: (starkes Passwort)
  ```
- [ ] Installation verifizieren
- [ ] IPA Web UI zugreifen (https://ipa.example.com)
- [ ] LDAP-Backend verstehen
- [ ] Kerberos KDC konfiguriert

### Phase 2: FreeIPA Benutzer & Gruppen (Tag 4-5)
- [ ] Admin-Benutzer kennenlernen
- [ ] Neue Benutzer erstellen:
  ```bash
  ipa user-add alice --first=Alice --last=Smith --email=alice@example.com
  ipa user-add bob --first=Bob --last=Jones
  ```
- [ ] Benutzer-Passwörter setzen
- [ ] Benutzer deaktivieren/aktivieren
- [ ] Gruppen erstellen:
  ```bash
  ipa group-add developers --desc="Development Team"
  ipa group-add-member developers --users=alice,bob
  ```
- [ ] Nested Groups
- [ ] Benutzer-Policies (Passwort-Ablauf, etc.)

### Phase 3: LDAP & Kerberos Verständnis (Tag 6-7)
- [ ] LDAP Directory-Struktur verstehen
- [ ] LDAP Queries durchführen:
  ```bash
  ldapsearch -H ldap://ipa.example.com -x -b "dc=example,dc=com"
  ```
- [ ] Kerberos Tickets anzeigen: `klist`
- [ ] TGT (Ticket Granting Ticket) verstehen
- [ ] Kinit für Authentifizierung:
  ```bash
  kinit alice@EXAMPLE.COM
  ```
- [ ] Kerberos Service Principals
- [ ] Cross-Realm Trust (optional)

### Phase 4: Linux Clients zu FreeIPA joinen (Tag 8-9)
- [ ] FreeIPA Client-Tools installieren
- [ ] Client zu FreeIPA Domain joinen:
  ```bash
  sudo apt install freeipa-client
  sudo ipa-client-install --domain=example.com --realm=EXAMPLE.COM --mkhomedir
  ```
- [ ] Nss-ldap für Benutzer-Auflösung
- [ ] PAM für Login-Authentifizierung
- [ ] Auto Home Directory Erstellung bei Login
- [ ] SSSD (System Security Services Daemon) Konfiguration
- [ ] Test: Mit FreeIPA-User einloggen

### Phase 5: Samba AD Alternative (Tag 10-12)
- [ ] Samba AD Unterschied zu Samba klassisch
- [ ] Samba AD als Domain Controller:
  ```bash
  sudo apt install samba-dsdb-modules samba-vfs-modules samba-testsuite
  samba-tool domain provision --use-rfc2307 --realm EXAMPLE.COM --domain EXAMPLE
  ```
- [ ] Samba als Kerberos KDC
- [ ] Windows Client Joining (optional)
- [ ] Benutzer in Samba AD verwalten:
  ```bash
  samba-tool user create alice Password123!
  samba-tool group add developers
  samba-tool group addmembers developers alice,bob
  ```
- [ ] Berechtigungen in Samba AD

### Phase 6: Berechtigungen & Policies (Tag 13-14)
- [ ] FreeIPA/Samba Berechtigungen verstehen
- [ ] Sudo-Regeln in FreeIPA:
  ```bash
  ipa sudorule-add "Allow developers to sudo"
  ipa sudorule-add-host "Allow developers to sudo" --hosts=web1
  ipa sudorule-add-user "Allow developers to sudo" --users=alice,bob
  ipa sudorule-add-allow-command "Allow developers to sudo" --allow-cmds=/usr/bin/systemctl
  ```
- [ ] Host-basierte Zugriffskontrolle (HBAC)
- [ ] Passwort-Policies
- [ ] Account Lockout Policies

### Phase 7: Integration mit Services (Tag 15-16)
- [ ] Postfix mit LDAP-Authentifizierung
- [ ] Apache mit Kerberos Auth
- [ ] Samba File Shares mit Domain-Benutzer
- [ ] SSH Public Key Management über FreeIPA
- [ ] Web-Anwendungen mit LDAP-Auth

### Phase 8: Backup & Disaster Recovery (Tag 17)
- [ ] FreeIPA Backup durchführen:
  ```bash
  sudo ipa-backup
  ```
- [ ] Restore durchführen
- [ ] LDAP-Dumps für Backup
- [ ] Kerberos DB Backup

### Phase 9: Troubleshooting & Monitoring (Tag 18)
- [ ] Häufige Probleme:
  - [ ] Benutzer kann sich nicht anmelden
  - [ ] Kerberos Ticket-Probleme
  - [ ] SSSD Caching Issues
  - [ ] LDAP Connection Errors
- [ ] sssd-debuglog für Debugging
- [ ] LDAP Queries für Verifikation
- [ ] Kerberos KDC Logs: `/var/log/krb5kdc.log`

## ✅ Bewertungskriterien
- **FreeIPA Setup:** Server läuft, Web-UI erreichbar
- **Benutzer/Gruppen:** Management via CLI und Web-UI funktioniert
- **Client-Join:** Clients können zu FreeIPA joinen
- **Authentication:** Benutzer können sich anmelden
- **Berechtigungen:** Sudo-Regeln, HBAC funktionieren
- **Samba AD:** Alternative Setup funktioniert (falls Samba gewählt)
- **Dokumentation:** Setup und Troubleshooting dokumentiert

## 🔐 Sicherheits-Best-Practices
- [ ] Starke Passwörter für Directory Manager und Admin
- [ ] Kerberos Verschlüsselung aktivieren
- [ ] LDAP über TLS (LDAPS)
- [ ] SSH Public Key nur für autorisierten Zugriff
- [ ] Sudo-Regeln nach Least-Privilege-Prinzip
- [ ] Audit-Logging für Directory-Änderungen

## 📚 Ressourcen & Dokumentation

### Wichtige Dateien
- `/etc/ipa/` - FreeIPA Config
- `/etc/sssd/sssd.conf` - SSSD Config
- `/etc/krb5.conf` - Kerberos Config
- `/etc/samba/smb.conf` - Samba Config (wenn genutzt)

### Wichtige Befehle
```bash
# FreeIPA
ipa user-add, ipa user-list, ipa user-del
ipa group-add, ipa group-add-member
ipa sudorule-add, ipa hbactest

# Kerberos
kinit user@REALM
klist
kdestroy

# LDAP
ldapsearch, ldapmodify
getent passwd alice

# Samba
samba-tool user add, samba-tool group add
samba-tool domain demote (wenn Migration)
```

### Wichtige Links
- https://www.freeipa.org
- https://wiki.samba.org/index.php/Samba4
- Kerberos: https://web.mit.edu/kerberos/

## 💡 Hands-On Labs

### Lab 1: FreeIPA Basis-Setup
- FreeIPA Server installieren
- 5 Benutzer und 2 Gruppen erstellen
- 2 Linux Clients joinen
- Benutzer-Logins testen

### Lab 2: Advanced Authentication
- Sudo-Regeln für verschiedene Gruppen
- HBAC Policies implementieren
- SSH Public Key Management
- Multi-Faktor Authentication (optional)

### Lab 3: Samba AD oder FreeIPA Vergleich
- Beide Systeme aufbauen
- Clients mit beiden joinen
- Performance und Skalierbarkeit vergleichen

## 💡 Trainer-Tipps
- Zeigen Sie die Unterschiede zu Windows AD
- Demonstrieren Sie LDAP-Queries zum Debuggen
- Lassen Sie Umschüler Authentifizierungsfehler debuggen
- Zeigen Sie Sicherheits-Implikationen von schlechten Policies

## 📋 Deliverables
1. **Installation Guide:** FreeIPA/Samba AD Setup
2. **Client-Join Guide:** Anleitung für Clients
3. **Policies & Rules:** Dokumentierte Sudo-Rules, HBAC
4. **Troubleshooting:** Common Issues & Solutions
5. **Backup & Recovery:** Disaster Recovery Procedures

---

**Projektstand:** [ ] Nicht begonnen | [ ] In Arbeit | [ ] Abgeschlossen

**Notizen:**
