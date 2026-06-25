# Projekt 3: Netzwerk-Grundlagen mit Linux

## 📋 Projektbeschreibung
Praktische Netzwerk-Administration unter Linux. Von Konfiguration bis zum Troubleshooting - ein essentielles Skill für jeden Systemintegrator.

## 🎯 Lernziele
- Netzwerk-Interfaces konfigurieren (Netplan, ethtool)
- Statische und dynamische IP-Adressierung
- DNS-Auflösung verstehen und konfigurieren
- Netzwerk-Troubleshooting (ping, traceroute, netstat, ss)
- Routing und Gateway-Konfiguration
- Netzwerk-Monitoring und Diagnostik

## 📊 Schwierigkeitsgrad
**Anfänger → Fortgeschritten**

## ⏱️ Dauer
1-2 Wochen

## 🔧 Anforderungen
- Ubuntu Server 22.04 LTS
- Mindestens 2 VMs für Netzwerk-Tests
- Grundverständnis: IPv4, DHCP, DNS
- Netzwerk-Lab-Setup (Virtual Bridge)

## 📝 Aufgaben

### Phase 1: Netzwerk-Interface Grundlagen (Tag 1-2)
- [ ] Interfaces auflisten: `ip link show`, `ifconfig`
- [ ] Interface-Informationen: `ethtool eth0`
- [ ] MAC-Adressen verstehen
- [ ] Interface-Status prüfen (UP, DOWN, RUNNING)
- [ ] `/etc/netplan/` Verzeichnis verstehen

### Phase 2: Statische IP-Konfiguration (Tag 3-4)
- [ ] Netplan YAML-Format kennenlernen
- [ ] Statische IP einrichten:
  ```yaml
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
  ```
- [ ] Konfiguration aktivieren: `sudo netplan apply`
- [ ] Persistent Einstellungen überprüfen

### Phase 3: DHCP-Konfiguration (Tag 5)
- [ ] DHCP aktivieren: `dhcp4: true`
- [ ] DHCP-Lease prüfen: `dhclient -v`
- [ ] Lease-Renewal testen
- [ ] DHCP-Fallbacks konfigurieren

### Phase 4: DNS-Konfiguration (Tag 6-7)
- [ ] Nameserver-Konfiguration (Netplan)
- [ ] `/etc/resolv.conf` verstehen (wird oft auto-generiert)
- [ ] DNS-Auflösung testen:
  ```bash
  nslookup google.com
  dig google.com
  host google.com
  ```
- [ ] Lokale DNS-Einträge in `/etc/hosts`
- [ ] DNS-Caching mit `systemd-resolved`
- [ ] Beschädigte DNS-Einträge debuggen

### Phase 5: Routing & Gateway (Tag 8)
- [ ] Routing-Tabelle anzeigen: `ip route show`
- [ ] Default-Gateway verstehen
- [ ] Statische Routen hinzufügen:
  ```bash
  sudo ip route add 10.0.0.0/8 via 192.168.1.1
  ```
- [ ] Persistente Routen via Netplan
- [ ] Traceroute-Pfade nachverfolgern

### Phase 6: Netzwerk-Troubleshooting (Tag 9-10)
- [ ] Basis-Diagnose-Tools:
  ```bash
  ping
  traceroute / tracepath
  mtr (My TraceRoute)
  netstat / ss
  ```
- [ ] Verbindungstests: `nc` (netcat), `telnet`
- [ ] Paket-Capture: `tcpdump`
- [ ] Netzwerk-Statistiken: `ethtool -S eth0`
- [ ] Häufige Probleme beheben:
  - [ ] Keine Connectivity
  - [ ] Langsames Netzwerk
  - [ ] DNS-Probleme
  - [ ] Duplikate IPs

### Phase 7: Fortgeschrittene Diagnose (Tag 11-12)
- [ ] ARP-Table: `arp -a`, `ip neigh show`
- [ ] Socket-Status: `ss -tlnp`
- [ ] Paket-Analyse mit tcpdump/Wireshark
- [ ] Netzwerk-Monitoring: `iftop`, `nethogs`
- [ ] Bandbreite-Tests

## ✅ Bewertungskriterien
- **Konfiguration:** Statische/DHCP-IPs funktionieren
- **DNS:** Auflösung funktioniert, DNS korrekt konfiguriert
- **Routing:** Default-Route und Gateways korrekt
- **Troubleshooting:** Kann systematisch Netzwerk-Probleme diagnostizieren
- **Dokumentation:** Alle Schritte und Befehle dokumentiert
- **Labs:** Alle Szenarien erfolgreich absolviert

## 📚 Ressourcen & Dokumentation

### Wichtige Konfigurationsdateien
- `/etc/netplan/*.yaml` - Netzwerk-Konfiguration
- `/etc/resolv.conf` - DNS (oft auto-generiert)
- `/etc/hostname` - Hostname
- `/etc/hosts` - Lokale Host-Einträge

### Wichtige Befehle
```bash
# IP/Interface
ip link show
ip addr show
ip route show
ifconfig (deprecated)
ethtool

# DNS
nslookup
dig
host
systemd-resolve --status

# Troubleshooting
ping
traceroute / tracepath
mtr
netstat / ss
tcpdump
nc (netcat)

# Monitoring
iftop
nethogs
sar
```

### RFC Standards
- RFC 791: IPv4
- RFC 1918: Private IP Ranges
- RFC 1035: DNS

## 💡 Hands-On Labs

### Lab 1: Basis Netzwerk-Setup
- 2 VMs mit Statischen IPs im gleichen Netzwerk
- Gegenseitige Erreichbarkeit mit Ping
- DNS-Namen auflösen

### Lab 2: Multi-Interface Setup
- Server mit 2 Netzwerk-Interfaces
- Zwei verschiedene Subnets
- Routing zwischen den Subnets

### Lab 3: Netzwerk-Fehler Behebung
- Bewusst Fehler in Konfiguration einbauen
- Umschüler müssen Fehler finden und beheben
- Szenarien:
  - [ ] Falscher Gateway
  - [ ] DNS nicht konfiguriert
  - [ ] IP-Konflikt
  - [ ] Interface nicht aktiviert

### Lab 4: Troubleshooting mit tcpdump
- HTTP-Request mit tcpdump capture
- Paketstruktur analysieren
- DNS-Queries anschauen

## 💡 Trainer-Tipps
- Zeigen Sie den Unterschied zwischen Netzwerk-Lasten (lokal vs. WAN)
- Nutzen Sie `mtr` für bessere Visualization als `traceroute`
- Zeigen Sie echte Fehler-Szenarien aus der Praxis
- Ergänzen Sie mit Wireshark GUI für visuelle Packet-Analyse

## 📋 Deliverables
1. **Dokumentation:** Netplan-Konfigurationen mit Erklärung
2. **Troubleshooting-Guide:** Schritt-für-Schritt Fehlersuche
3. **Lab-Reports:** Ergebnisse aller Netzwerk-Szenarien
4. **Checkliste:** Netzwerk-Diagnose Checklist

---

**Projektstand:** [ ] Nicht begonnen | [ ] In Arbeit | [ ] Abgeschlossen

**Notizen:**
