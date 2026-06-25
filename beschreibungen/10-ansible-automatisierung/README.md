# Projekt 10: Ansible Infrastruktur-Automatisierung

## 📋 Projektbeschreibung
Infrastructure as Code mit Ansible. Automatisierung von Konfiguration, Deployment und Management über viele Server hinweg.

## 🎯 Lernziele
- Ansible Installation und Grundlagen
- Playbooks und Tasks schreiben
- Rollen (Roles) für Wiederverwendbarkeit
- Inventory Management
- Facts und Conditional Logic
- Error Handling und Debugging
- Beste Praktiken und Performance

## 📊 Schwierigkeitsgrad
**Fortgeschritten → Expert**

## ⏱️ Dauer
2-3 Wochen

## 🔧 Anforderungen
- Ubuntu Server 22.04 LTS (Control Node)
- Min. 3 zusätzliche VMs (Managed Nodes)
- SSH-Keys konfiguriert zwischen Nodes
- Grundverständnis: YAML, Shell Scripting

## 📝 Aufgaben

### Phase 0: VM-Initialisierung mit Cloud-Init (Tag 0 - Vorbereitung)

Bevor Ansible zum Einsatz kommt: VMs automatisch mit cloud-init initialisieren. Dies spart Zeit und zeigt "Infrastructure as Code" auf der ersten Schicht.

#### Cloud-Init User-Data für Ansible-Nodes
```yaml
#cloud-config
hostname: managed-node-1
package_update: true
package_upgrade: true

packages:
  - openssh-server
  - python3
  - python3-pip
  - sudo

users:
  - name: ansible-user
    sudo: ALL=(ALL) NOPASSWD:ALL
    ssh_authorized_keys:
      - ssh-rsa AAAAB3NzaC1... your-public-key

runcmd:
  - systemctl enable ssh
  - systemctl restart ssh
```

#### Praktische Schritte
- [ ] Cloud-Init User-Data schreiben (für Control Node + 3 Managed Nodes)
- [ ] VMs mit cloud-init hochfahren (z.B. KVM/VirtualBox)
- [ ] Automatische Netzwerk-Konfiguration überprüfen
- [ ] SSH-Konnektivität von Control Node zu allen Managed Nodes testen

**Ergebnis:** 3-4 VMs sind vorbereitet, mit Python installiert, SSH-Keys konfiguriert → Ansible kann direkt arbeiten.

---

### Phase 1: Ansible Installation & Setup (Tag 1-2)
- [ ] Ansible installieren: `sudo apt install ansible`
- [ ] SSH-Keys zwischen Nodes konfigurieren
- [ ] Inventory Datei erstellen: `/etc/ansible/hosts`
  ```ini
  [webservers]
  web1 ansible_host=192.168.1.10
  web2 ansible_host=192.168.1.11

  [databases]
  db1 ansible_host=192.168.1.20
  ```
- [ ] Connectivity testen: `ansible all -m ping`
- [ ] Ansible.cfg verstehen
- [ ] Verschiedene Inventory-Formate (INI, YAML)

### Phase 2: Basic Commands & Ad-Hoc Tasks (Tag 3)
- [ ] Ad-hoc Commands:
  ```bash
  ansible all -m apt -a "name=vim state=present"
  ansible webservers -m service -a "name=nginx state=started"
  ansible all -m shell -a "cat /etc/hostname"
  ```
- [ ] Verschiedene Module kennenlernen:
  - [ ] apt, yum (Package Management)
  - [ ] service, systemd (Service Management)
  - [ ] file, copy (File Management)
  - [ ] user, group (User Management)
- [ ] Variablen in Ad-hoc Commands

### Phase 3: Playbooks schreiben (Tag 4-6)
- [ ] Playbook YAML-Struktur verstehen
- [ ] Einfaches Playbook:
  ```yaml
  ---
  - hosts: webservers
    become: yes
    tasks:
      - name: Update apt cache
        apt:
          update_cache: yes

      - name: Install nginx
        apt:
          name: nginx
          state: present

      - name: Start nginx
        service:
          name: nginx
          state: started
          enabled: yes
  ```
- [ ] Variables definieren und nutzen
- [ ] Handlers für Notifications
- [ ] Multiple Plays in einem Playbook
- [ ] Playbooks ausführen: `ansible-playbook site.yml`

### Phase 4: Roles für Wiederverwendbarkeit (Tag 7-8)
- [ ] Role Struktur verstehen:
  ```
  roles/
    nginx/
      tasks/
      handlers/
      templates/
      files/
      vars/
  ```
- [ ] Nginx Role erstellen
- [ ] Role Templates verwenden (Jinja2)
- [ ] Role Variables
- [ ] Multiple Roles in Playbooks
- [ ] Role Dependencies
- [ ] Galaxy Roles (optional): `ansible-galaxy install`

### Phase 5: Facts & Conditionals (Tag 9)
- [ ] Facts sammeln: `setup` Module
- [ ] Custom Facts
- [ ] Facts in Playbooks nutzen:
  ```yaml
  - name: Install vim on Ubuntu
    apt:
      name: vim
      state: present
    when: ansible_distribution == "Ubuntu"
  ```
- [ ] Loop-Strukturen:
  ```yaml
  - name: Create users
    user:
      name: "{{ item }}"
      state: present
    loop:
      - alice
      - bob
      - charlie
  ```
- [ ] Conditional Loops

### Phase 6: Templates & Dynamic Content (Tag 10)
- [ ] Jinja2 Templates verstehen
- [ ] Config-Files mit Templates:
  ```jinja2
  server {
    listen {{ nginx_port }};
    server_name {{ server_name }};
    ...
  }
  ```
- [ ] Template Module nutzen
- [ ] Variable Interpolation
- [ ] Conditionals in Templates
- [ ] Loops in Templates

### Phase 7: Error Handling & Debugging (Tag 11)
- [ ] ignore_errors, failed_when
- [ ] register für Output-Handling
- [ ] block/rescue für Error Handling
- [ ] debug Module nutzen
- [ ] Verbose Logging: `ansible-playbook -vvv`
- [ ] Playbook-Syntax prüfen: `ansible-playbook --syntax-check`

### Phase 8: Erweiterte Konzepte (Tag 12-13)
- [ ] Include/Import
- [ ] Pre-tasks, Post-tasks
- [ ] Tags für Selektive Ausführung
- [ ] Vault für Secrets:
  ```bash
  ansible-vault encrypt secrets.yml
  ```
- [ ] Limits und Batching
- [ ] Dry-run: `--check` Mode

### Phase 9: Praxisprojekt: Multi-Tier App (Tag 14-15)
- [ ] Web Tier (Nginx)
- [ ] Application Tier (Python/Node)
- [ ] Database Tier (PostgreSQL)
- [ ] Load Balancer
- [ ] Komplettes Playbook für gesamte Stack
- [ ] Idempotenz gewährleisten
- [ ] Rolling Updates

## ✅ Bewertungskriterien
- **Ansible Setup:** Installation, Inventory, SSH funktioniert
- **Ad-hoc Commands:** Können einfache Tasks ausführen
- **Playbooks:** Schreiben funktionierende, idempotente Playbooks
- **Roles:** Strukturieren Code in wiederverwendbare Roles
- **Erweitert:** Nutzen Conditionals, Loops, Templates
- **Dokumentation:** Playbooks gut dokumentiert

## 🔐 Sicherheits-Best-Practices
- [ ] Vault für Secrets nutzen (nicht in Code)
- [ ] Benutzer für Ansible mit eingeschränkten Rechten
- [ ] SSH-Key-Auth, nicht Passwörter
- [ ] Keine Credentials in Inventory-Dateien
- [ ] Audit-Logging für Ansible-Runs
- [ ] ansible-lint für Code-Quality

## 📚 Ressourcen & Dokumentation

### Wichtige Dateien
- `/etc/ansible/ansible.cfg` - Config
- `/etc/ansible/hosts` - Inventory
- `playbook.yml` - Playbook Definition
- `roles/` - Role Directory

### Wichtige Befehle
```bash
# Setup & Connectivity
ansible all -m ping
ansible all -m setup

# Ad-hoc Commands
ansible all -m apt -a "name=vim state=present"
ansible webservers -m service -a "name=nginx state=started"

# Playbooks
ansible-playbook site.yml
ansible-playbook site.yml -t webservers
ansible-playbook site.yml --check
ansible-playbook site.yml -vvv

# Vault
ansible-vault encrypt vars.yml
ansible-playbook site.yml --ask-vault-pass

# Syntax Check
ansible-lint playbook.yml
```

## 🚀 Integration: Cloud-Init + Ansible

Eine typische produktive Workflow kombiniert beide Tools:

1. **Cloud-Init (Phase 0):** Server-Initialisierung (OS-Updates, Basis-Pakete, SSH-Keys)
2. **Ansible (Phase 1+):** Komplexe Konfiguration (Services, Apps, Monitoring)

### Praktisches Beispiel
```bash
# 1. VMs mit cloud-init starten (automatisch)
# 2. Von Ansible konfigurieren
ansible-playbook -i inventory.ini site.yml

# 3. Neue Server hinzufügen: Wieder mit cloud-init + Ansible
```

**Vorteil:** Cloud-init ist immutable (VM ist nach Init fertig), Ansible ist idempotent (kann mehrfach laufen, gleich Ergebnis).

---

## 💡 Hands-On Labs

### Lab 1: Basis Web-Server Setup
- 3 Nodes mit verschiedenen Rollen
- Ansible Role für Nginx
- Firewall-Konfiguration via Ansible
- SSL-Zertifikate deployen

### Lab 2: Multi-Tier Application
- Web, App, Database Tier
- Jede Tier separate Role
- Configuration Management
- Secrets mit Vault

### Lab 3: Rolling Updates & Maintenance
- Update Playbooks
- Health-Check Tasks
- Graceful Restarts
- Monitoring Integration

## 💡 Trainer-Tipps
- Beginnen Sie mit Ad-hoc Commands bevor Sie Playbooks schreiben
- Zeigen Sie Idempotenz: Playbooks 2x ausführen sollte gleich sein
- Demonstrieren Sie `--check` Mode für sichere Deployments
- Lassen Sie Umschüler mit Jinja2 Templates spielen

## 📋 Deliverables
1. **Inventory:** Organisierte Host-Definition
2. **Playbooks:** Funktionsfähige Automation
3. **Roles:** Wiederverwendbare, dokumentierte Roles
4. **Documentation:** Best-Practices Guide
5. **Troubleshooting:** Debugging Guide

---

**Projektstand:** [ ] Nicht begonnen | [ ] In Arbeit | [ ] Abgeschlossen

**Notizen:**
