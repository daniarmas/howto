# DNS: Deploying a DNS Server with CoreDNS and Docker

This guide explains how to quickly deploy a DNS server using [CoreDNS](https://coredns.io/) and Docker on Ubuntu.

## 📦 Prerequisites

- Ubuntu server running (physical, VM, or cloud image)
- [Docker Engine](https://docs.docker.com/engine/install/ubuntu/#install-using-the-repository) installed

## 🛠️ Steps

### 1. Install Docker Engine on Ubuntu

Follow the official Docker documentation:  
https://docs.docker.com/engine/install/ubuntu/#install-using-the-repository

### 2. Clone or Create Your CoreDNS Docker Compose Setup

Make sure you have a `docker-compose.yml` file configured for CoreDNS.  
Example files and configuration can be found [here](docker-compose.yaml).

### 3. Deploy CoreDNS with Docker Compose

Start the CoreDNS service:

```bash
docker compose up -d
```

### 4. Verify CoreDNS is Running

Check the status of your containers:

```bash
docker ps
```

---

**References:**
- [CoreDNS Documentation](https://coredns.io/manual/toc/)
- [Docker Compose Documentation](https://docs.docker.com/compose/)