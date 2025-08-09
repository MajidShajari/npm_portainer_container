# Dockerized Nginx Proxy Manager & Portainer Setup with Auto Deployment

## Overview

This repository contains a `docker-compose.yml` setup to run:

- **Nginx Proxy Manager (NPM)**
- **PostgreSQL database** for NPM
- **Portainer** for Docker management

The project uses environment variables from a `.env` file (excluded from git) for sensitive information.

---

## Features

- Containers run inside a private Docker network (`npm_net`).
- Portainer service is exposed only internally and proxied through Nginx Proxy Manager.
- Environment variables handled via `.env` file.
- Auto-deployment on Hetzner server through GitHub Actions on push to `main` branch.
  
---

## Getting Started

### Prerequisites

- Docker & Docker Compose installed on the server.
- SSH access to the server.
- Git installed on the server.
- A domain name configured and pointing to your server (for Nginx Proxy Manager SSL).

---

### Setup

1. **Clone the repository on your server:**

   ```bash
   git clone git@github.com:YourUsername/YourRepo.git /path/to/project
   cd /path/to/project
   ```
2. **Create .env file based on .env.example:**

```bash
cp .env.example .env
# Edit `.env` with your actual credentials
```
3. **Start the stack manually for the first time:**

```bash
docker compose up -d
```
4. **Configure Nginx Proxy Manager to proxy Portainer and other services**

### Auto Deployment with GitHub Actions
On every push to the `main` branch, the following workflow runs:
- SSH into your Hetzner server.
- Navigate to the project directory.
- Pull latest changes.
- Pull updated Docker images.
Restart containers with updated configurations.
**Ensure** the following GitHub Secrets are configured:

| Secret     | Description                        |
| ---------- | ---------------------------------- |
| `SSH_HOST` | IP address of your Hetzner server  |
| `SSH_USER` | SSH user with access to project    |
| `SSH_KEY`  | Private SSH key for authentication |
---

### GitHub Actions Workflow
The workflow file is located at `.github/workflows/deploy.yml`. It triggers on pushes to `main`.

---
Troubleshooting
- If deployment fails, check GitHub Actions logs for error details.

- Verify SSH connectivity from GitHub Actions runner to your server.

- Ensure Docker and docker-compose are installed and in PATH on the server.

- Confirm that your SSH public key is correctly added to ~/.ssh/authorized_keys on the server user.
---

### License
MIT

---