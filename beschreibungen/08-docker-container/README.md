# Projekt 8: Docker & Container-Orchestration

## 📋 Projektbeschreibung
Containerisierung von Anwendungen mit Docker und Grundlagen der Orchestration. Ein modernes, essentielles Skill für DevOps und Systemintegration.

## 🎯 Lernziele
- Docker Installation und Grundlagen
- Dockerfile schreiben und Images bauen
- Container lifecycle verwalten
- Docker Volumes und Networking
- Docker Compose für Multi-Container Apps
- Kubernetes Grundlagen (Microk8s)
- Registry und Image Management
- Container Security

## 📊 Schwierigkeitsgrad
**Fortgeschritten → Expert**

## ⏱️ Dauer
3-4 Wochen

## 🔧 Anforderungen
- Ubuntu Server 22.04 LTS oder Desktop
- Min. 8GB RAM, 40GB Disk
- Docker installiert
- Grundverständnis: Linux, Netzwerk

## 📝 Aufgaben

### Phase 1: Docker Grundlagen (Tag 1-3)
- [ ] Docker installieren: `sudo apt install docker.io`
- [ ] Docker Daemon verstehen
- [ ] Container vs. Images
- [ ] Images pullen: `docker pull ubuntu`
- [ ] Containers laufen lassen: `docker run -it ubuntu bash`
- [ ] Container Lifecycle: create, start, stop, remove
- [ ] Docker CLI Befehle:
  ```bash
  docker ps, docker images, docker logs
  docker exec, docker inspect, docker stats
  ```
- [ ] Container-Ressourcen limitieren (CPU, Memory)

### Phase 2: Dockerfile schreiben (Tag 4-6)
- [ ] Dockerfile Syntax verstehen
- [ ] Base Images wählen
- [ ] Application in Container packen
- [ ] Multi-Stage Builds
- [ ] Layer Caching verstehen
- [ ] Beispiel: Python Flask App in Docker
  ```dockerfile
  FROM python:3.9-slim
  WORKDIR /app
  COPY requirements.txt .
  RUN pip install -r requirements.txt
  COPY . .
  CMD ["python", "app.py"]
  ```
- [ ] Image bauen: `docker build -t myapp:1.0 .`
- [ ] Image optimieren (Größe reduzieren)
- [ ] Best Practices (Non-root user, .dockerignore)

### Phase 3: Docker Volumes & Networking (Tag 7-8)
- [ ] Volumes erstellen und mounten:
  ```bash
  docker volume create mydata
  docker run -v mydata:/data ubuntu
  ```
- [ ] Bind Mounts für Development
- [ ] Volume-Typen verstehen (named, anonymous, bind)
- [ ] Docker Networks:
  - [ ] Bridge (default)
  - [ ] Host
  - [ ] Overlay (für Swarm)
- [ ] Container-zu-Container Kommunikation
- [ ] Port-Mapping: `-p 8080:80`

### Phase 4: Docker Compose (Tag 9-11)
- [ ] docker-compose.yml schreiben
- [ ] Services definieren (Web, DB, Cache)
- [ ] Environment Variables
- [ ] Volumes in Compose
- [ ] Networks in Compose
- [ ] Example Stack:
  ```yaml
  version: '3'
  services:
    web:
      build: .
      ports:
        - "8080:5000"
      environment:
        - DB_HOST=db
    db:
      image: postgres:13
      environment:
        - POSTGRES_PASSWORD=secret
      volumes:
        - db_data:/var/lib/postgresql/data
  volumes:
    db_data:
  ```
- [ ] `docker-compose up/down`
- [ ] Logs aggregieren: `docker-compose logs`
- [ ] Services skalieren: `docker-compose up --scale web=3`

### Phase 5: Docker Registry & Security (Tag 12-13)
- [ ] Docker Hub Account erstellen
- [ ] Images pushen: `docker push username/image:tag`
- [ ] Private Registry (optional: Registry Helm Chart)
- [ ] Image Security:
  - [ ] Minimal Base Images
  - [ ] Non-root User in Container
  - [ ] Image Scanning (Trivy)
  - [ ] Secrets Management
- [ ] Docker Security Best Practices

### Phase 6: Kubernetes Grundlagen mit Microk8s (Tag 14-16)
- [ ] Microk8s installieren: `snap install microk8s --classic`
- [ ] Kubernetes Architektur verstehen (Master, Nodes, Pods)
- [ ] Pod YAML schreiben:
  ```yaml
  apiVersion: v1
  kind: Pod
  metadata:
    name: myapp
  spec:
    containers:
    - name: app
      image: myapp:1.0
      ports:
      - containerPort: 5000
  ```
- [ ] Deployments erstellen (für Pod-Replicas)
- [ ] Services exposieren (ClusterIP, NodePort, LoadBalancer)
- [ ] kubectl Befehle:
  ```bash
  kubectl apply -f deployment.yaml
  kubectl get pods, kubectl logs, kubectl describe
  kubectl scale deployment myapp --replicas=3
  ```
- [ ] Persistent Volumes in K8s

### Phase 7: Praxisprojekt: Microservices (Tag 17-20)
- [ ] 3-4 Microservices entwickeln:
  - [ ] Frontend (Nginx/HTML)
  - [ ] API Service (Python/Node)
  - [ ] Database (Postgres)
  - [ ] Cache (Redis)
- [ ] Dockerfiles für jeden Service
- [ ] docker-compose.yml für Development
- [ ] Kubernetes Manifests für Production
- [ ] Service-Discovery
- [ ] Health-Checks und Restarts

## ✅ Bewertungskriterien
- **Docker Basics:** Images, Containers, lifecycle funktionieren
- **Dockerfile:** Efficient, sicher, Best-Practices befolgt
- **Compose:** Multi-Service App läuft mit `docker-compose up`
- **K8s:** Deployments, Services, Pods funktionieren
- **Security:** Non-root, minimale Images, Secrets richtig behandelt
- **Dokumentation:** Dockerfiles, Compose, Manifests gut dokumentiert

## 🔐 Sicherheits-Best-Practices
- [ ] Non-root User in Dockerfile
- [ ] Minimale Base Images (alpine, scratch)
- [ ] Read-only Filesystems wo möglich
- [ ] Network Policies in K8s
- [ ] Secrets nicht in Environment Variables hardcoden
- [ ] Image Scanning mit Trivy
- [ ] Registry mit TLS/Auth

## 📚 Ressourcen & Dokumentation

### Wichtige Dateien
- `Dockerfile` - Container Definition
- `docker-compose.yml` - Multi-Container Definition
- `k8s-deployment.yaml` - Kubernetes Deployment
- `.dockerignore` - Files ausschließen vom Build

### Wichtige Befehle
```bash
# Docker
docker build -t image:tag .
docker run -d --name container image:tag
docker ps, docker logs, docker exec
docker volume create, docker network create

# Docker Compose
docker-compose up -d
docker-compose down
docker-compose logs -f

# Kubernetes
kubectl create deployment myapp --image=myapp:1.0
kubectl expose deployment myapp --port=80 --type=NodePort
kubectl scale deployment myapp --replicas=3
kubectl get all
```

## 💡 Hands-On Labs

### Lab 1: Eigene Anwendung containerisieren
- Kleine Anwendung (Python/Node/PHP)
- Dockerfile schreiben
- Image bauen und testen
- Docker Hub pushen

### Lab 2: Multi-Container App mit Compose
- Web + Database + Cache
- Docker Compose up starten
- Daten persistieren
- Skalierung testen

### Lab 3: Kubernetes Deployment
- Docker Image zu Microk8s deployen
- Deployment mit Replicas
- Service exponieren
- Rolling Update durchführen

## 💡 Trainer-Tipps
- Zeigen Sie die Unterschiede: Docker vs. VMs vs. Bare Metal
- Demonstrieren Sie Image-Größen-Unterschiede
- Lassen Sie Umschüler echte Probleme debuggen (Networking, Volumes)
- Zeigen Sie Security-Scanning mit Trivy

## 📋 Deliverables
1. **Dockerfiles:** Für jede Anwendung
2. **docker-compose.yml:** Vollständiger Stack
3. **Kubernetes Manifests:** Deployments, Services
4. **Security Audit:** Image Security Report
5. **Betriebshandbuch:** Wie man Apps deployt, scaled, updatet

---

**Projektstand:** [ ] Nicht begonnen | [ ] In Arbeit | [ ] Abgeschlossen

**Notizen:**
