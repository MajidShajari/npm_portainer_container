# 🚀 Dockerized Nginx Proxy Manager & Portainer Setup with Auto Deployment

## 📌 Overview

This repository contains a `docker-compose.yml` setup to run:

- 🌐 **Nginx Proxy Manager (NPM)**
- 🗄️ **PostgreSQL database** for NPM
- 📦 **Portainer** for Docker management

Sensitive information is managed via a `.env` file (excluded from git).  

---

## ✨ Features

- 🔒 Containers run inside a **private Docker network** (`npm_net`).
- 🔐 Portainer service is exposed **only internally** and proxied through Nginx Proxy Manager.
- ⚙️ Environment variables handled via `.env` file.
- 🤖 **Auto-deployment** on Hetzner server via GitHub Actions on every push to `master` branch.

---

## 🛠️ Getting Started

### ✅ Prerequisites
- 🐳 **Docker** & **Docker Compose** installed on the server
- 🔑 SSH access to the server
- 📂 Git installed on the server
- 🌍 A domain name pointing to your server (for SSL in NPM)

---

### ⚡ Setup

1. **Clone the repository on your server:**
   ```bash
   git clone git@github.com:YourUsername/YourRepo.git /path/to/project
   cd /path/to/project
2. **Create `.env` file based on `.env.example`:**

```bash
cp .env.example .env
# Edit `.env` with your actual credentials
```
3. **Start the stack manually for the first time:**

```bash
docker compose up -d
```
4. **Configure Nginx Proxy Manager** to proxy Portainer and other services.
---
## 🤖 Auto Deployment with GitHub Actions
On **every push** to the `master` branch, the workflow will:
1. SSH into your Hetzner server.
2. Navigate to the project directory.
3. Pull the latest changes.
4. Pull updated Docker images.
5. Restart containers with updated configurations.
**Required GitHub Secrets:**

| Secret     | Description                          |
| ---------- | ------------------------------------ |
| `SSH_HOST` | 🌐 IP address of your Hetzner server  |
| `SSH_USER` | 👤 SSH user with access to project    |
| `SSH_KEY`  | 🔑 Private SSH key for authentication |

---
### 📜 GitHub Actions Workflow
Location: `.github/workflows/deploy.yml`

Trigger: Push to `master` branch

---
### 🐞 Troubleshooting
- ❌ Deployment failed? **Check GitHub Actions** logs for error details.

- 🔍 Verify SSH connectivity from GitHub Actions runner to your server.

- 🐳 Ensure Docker & Docker Compose are installed on the server.

- 🔑 Confirm your SSH public key is added to **~/.ssh/authorized_keys**.
---
## 📄 License
MIT