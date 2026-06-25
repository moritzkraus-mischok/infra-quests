# Projekt 6: OpenSSH & VPN Setup

## 📋 Projektbeschreibung
Sichere Remote-Zugriff auf Systeme. Von SSH-Hardening bis zur Einrichtung von VPN-Netzwerken für sichere Datenübertragung.

## 🎯 Lernziele
- SSH erweiterte Konfiguration und Sicherheit
- SSH-Tunnel und Port-Forwarding
- VPN-Grundlagen (OpenVPN oder WireGuard)
- Netzwerk-Segmentierung mit VPNs
- Certificate-based Authentication
- Monitoring von Remote-Sessions

## 📊 Schwierigkeitsgrad
**Fortgeschritten**

## ⏱️ Dauer
2-3 Wochen

## 🔧 Anforderungen
- Ubuntu Server 22.04 LTS (mind. 2 Systeme)
- OpenSSH installiert
- Grundverständnis: PKI, Netzwerk, Kryptographie
- VPN-Testumgebung (mehrere VMs)

## 📝 Aufgaben

### Phase 1: SSH Erweiterte Konfiguration (Tag 1-3)
- [ ] SSH-Key-Paare mit verschiedenen Algorithmen:
  ```bash
  ssh-keygen -t ed25519  # Modern, 256-bit
  ssh-keygen -t rsa -b 4096  # Traditional, 4096-bit
  ```
- [ ] SSH-Config lokal für einfachere Verbindungen:
  ```
  Host server1
    HostName 192.168.1.10
    User alice
    IdentityFile ~/.ssh/server1_key
    Port 2222
  ```
- [ ] SSH-Agent für Key-Management
- [ ] SSH-Key-Passphrases
- [ ] Multiple Keys pro User
- [ ] Key-Rotation implementieren

### Phase 2: SSH Server Hardening (Tag 4-5)
- [ ] `/etc/ssh/sshd_config` optimieren:
  ```
  Port 2222
  PermitRootLogin no
  PasswordAuthentication no
  PubkeyAuthentication yes
  X11Forwarding no
  MaxAuthTries 3
  LoginGraceTime 1m
  MaxSessions 10
  ```
- [ ] AllowUsers / DenyUsers konfigurieren
- [ ] Match-Blöcke für conditional Config
- [ ] Fail2ban Integration
- [ ] Syntax prüfen: `sudo sshd -t`

### Phase 3: SSH-Tunneling & Port-Forwarding (Tag 6-7)
- [ ] Local Port Forwarding (Port auf Remote-System zugreifen):
  ```bash
  ssh -L 8080:localhost:80 user@remote.com
  ```
- [ ] Remote Port Forwarding (Remote-Port auf Local-System):
  ```bash
  ssh -R 8080:localhost:80 user@remote.com
  ```
- [ ] Dynamic Port Forwarding (SOCKS Proxy):
  ```bash
  ssh -D 1080 user@remote.com
  ```
- [ ] Persistente SSH-Tunnel mit systemd
- [ ] Anwendungsfall: Sichere Datenbank-Zugriffe

### Phase 4: Certificate-based Authentication (Tag 8)
- [ ] SSH CA (Certificate Authority) Setup
- [ ] Host-Keys mit Zertifikat signieren
- [ ] User-Zertifikate ausstellen
- [ ] Zertifikat-Validierung auf Server
- [ ] Zertifikat-Revocation-Listen (optional)

### Phase 5: OpenVPN Installation & Setup (Tag 9-11)
**Oder WireGuard als Alternative**

#### OpenVPN
- [ ] OpenVPN installieren: `sudo apt install openvpn easy-rsa`
- [ ] PKI (Public Key Infrastructure) aufbauen:
  ```bash
  /usr/share/easy-rsa/easyrsa init-pki
  /usr/share/easy-rsa/easyrsa build-ca
  /usr/share/easy-rsa/easyrsa gen-req server
  /usr/share/easy-rsa/easyrsa sign-req server server
  ```
- [ ] OpenVPN-Server konfigurieren (`/etc/openvpn/server.conf`)
- [ ] Netzwerk-Einstellungen (10.8.0.0/24)
- [ ] TLS-Authentication für DDoS-Schutz
- [ ] Server starten und testen

### Phase 6: OpenVPN Clients (Tag 12)
- [ ] Client-Zertifikate generieren
- [ ] Client-Konfiguration erstellen (`.ovpn` Datei)
- [ ] Mehrere Clients verbinden
- [ ] Verbindungsstabilität testen
- [ ] Logs analysieren

### Phase 7: VPN Netzwerk-Segmentierung (Tag 13)
- [ ] VPN als Zugang zu Private-Network
- [ ] Routing konfigurieren (iroute, push routes)
- [ ] Firewall-Regeln für VPN-Clients
- [ ] DNS über VPN pushen
- [ ] Split-Tunneling vs. Full-Tunneling

### Phase 8: WireGuard als Alternative (Tag 14)
- [ ] WireGuard installieren: `sudo apt install wireguard`
- [ ] Keys generieren: `wg genkey | tee private.key | wg pubkey > public.key`
- [ ] Interface konfigurieren (`wg0`)
- [ ] Clients hinzufügen
- [ ] Performance-Vergleich mit OpenVPN

### Phase 9: Monitoring & Troubleshooting (Tag 15)
- [ ] Aktive SSH-Sessions monitoring: `who`, `w`, `ss`
- [ ] SSH-Logs analysieren: `/var/log/auth.log`
- [ ] OpenVPN-Clients monitoring: `openvpn-status.log`
- [ ] VPN-Connectivity testen: `ping`, `traceroute`, `mtr`
- [ ] Häufige Probleme:
  - [ ] Authentifizierung fehlgeschlagen
  - [ ] Routing-Probleme
  - [ ] DNS nicht auflösend in VPN
  - [ ] Intermittent Connections

## ✅ Bewertungskriterien
- **SSH-Keys:** Korrekt generiert, Permissions 600/700
- **SSH-Hardening:** Sichere Konfiguration durchgeführt
- **Tunneling:** SSH-Tunnels funktionieren stabil
- **OpenVPN:** Server läuft, Clients können sich verbinden
- **Netzwerk:** VPN-Clients können untereinander kommunizieren
- **Sicherheit:** TLS, Verschlüsselung, Authentifizierung aktiv
- **Dokumentation:** Alle Schritte dokumentiert

## 🔐 Sicherheits-Best-Practices
- [ ] Niemals SSH-Keys mit Passphrase transportieren
- [ ] OpenVPN mit 2.4+ verwenden (mit modernen Ciphern)
- [ ] TLS-Version 1.2+ forcieren
- [ ] Starke Cipher verwenden (AES-256-GCM)
- [ ] VPN-Logs regelmäßig überprüfen
- [ ] Zertifikate mit angemessenen TTLs ausstellen

## 📚 Ressourcen & Dokumentation

### Wichtige Dateien
- `/etc/ssh/sshd_config` - SSH Server Config
- `~/.ssh/config` - SSH Client Config
- `/etc/openvpn/server.conf` - OpenVPN Server Config
- `/etc/wireguard/wg0.conf` - WireGuard Config (wenn genutzt)

### Wichtige Befehle
```bash
# SSH
ssh-keygen -t ed25519
ssh-copy-id -i ~/.ssh/id_ed25519.pub user@host
ssh -L 8080:localhost:80 user@host

# OpenVPN
openvpn --config /etc/openvpn/server.conf
openvpn --config client.ovpn

# WireGuard
sudo wg-quick up wg0
sudo wg show
wg-quick strip wg0 | tee wg0.conf

# Monitoring
who
w
ss -tlnp | grep ssh
cat /var/log/auth.log | grep ssh
```

## 💡 Hands-On Labs

### Lab 1: SSH Hardening & Tunneling
- SSH-Key-Auth implementieren
- Port ändern und testen
- SSH-Tunnel zu MySQL-DB einrichten
- Clients über Tunnel auf DB zugreifen

### Lab 2: OpenVPN Netzwerk
- OpenVPN-Server aufbauen
- 3 Clients verbinden
- Intra-VPN Kommunikation testen
- Client-zu-Client Routing aktivieren

### Lab 3: Sicherheits-Audit
- Nmap-Scan vor/nach SSH-Hardening
- Fail2ban Logs analysieren
- Brute-Force Protection testen
- OpenVPN Cipher-Suite überprüfen

## 💡 Trainer-Tipps
- Zeigen Sie echte VPN-Szenarien: Remote-Teams, Sicherheit in Cafés, etc.
- Demonstrieren Sie SSH-Tunneling für Datenbank-Admin
- Nutzen Sie openssl für Certificate-Debugging
- Zeigen Sie Performance-Unterschiede: SSH vs. VPN

## 📋 Deliverables
1. **SSH-Dokumentation:** Konfigurationen und Best-Practices
2. **VPN-Setup-Guide:** Schritt-für-Schritt Anleitung
3. **Client-Konfigurationen:** Ready-to-use Dateien für Clients
4. **Troubleshooting-Guide:** Häufige Probleme und Lösungen
5. **Monitoring-Setup:** Log-Analyse und Alerts

---

**Projektstand:** [ ] Nicht begonnen | [ ] In Arbeit | [ ] Abgeschlossen

**Notizen:**
