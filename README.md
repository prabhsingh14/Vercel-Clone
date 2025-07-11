# 🚀 CodeDrop: Deployment Engine

A **scalable backend system** inspired by Vercel, enhanced with a unique feature:  
📦 Upload any `.zip` folder → ⚙️ Auto-build → 🌐 Deploy to subdomain → 🔐 Control visibility (public/private)

---

## 🏗 Architecture
<img width="2553" height="709" alt="architecture" src="https://github.com/user-attachments/assets/55553814-4c6f-48b4-ae5b-8f9a784d7eb0" />

---

## 🛠 Tech Stack

- **Node.js** – Core backend logic
- **Docker** – Containerized build & deploy
- **Redis** – Async job queue for processing builds
- **MongoDB** – Stores deployment metadata and visibility state
- **AWS ECS** – Serverless container execution for isolated builds
- **JWT Auth** – Authenticated access to private deployments
- **Multer** – Handles `.zip` uploads for user projects

---

## 📦 Core Features

### 🔧 Project Deployment
- Upload `.zip` frontend → system builds it inside Docker container
- Skips unchanged files using **content hashing**
- Deploys automatically to a live subdomain (e.g., `project.localhost:8000`)

### 🧠 Smart Build Diffing
- Avoids redundant builds by comparing file hashes with previous versions

### 🌐 Dynamic Subdomain Proxy
- Reverse proxy maps subdomains to correct project folders
- JWT protection for private deployments

### 🔐 Private/Public Access Control
- Easily toggle a project’s visibility with a secure API endpoint

### 🔄 Git Integration  
- Trigger builds directly from GitHub webhooks

### 📦 Dockerized Builds  
- Each project is built in an isolated Docker container to ensure environment parity and security.

### 🧵 Redis Queue System  
- Asynchronous build execution using Redis-backed task queue

### 📡 Dynamic Routing  
- All projects served on their own unique subdomain for instant access

### ☁️ Cloud Hosted (Infra-ready)
- Architecture mimics real-world scale using AWS ECS, S3, and EC2

---

## 📁 Folder Structure
- /api-server → Auth, deployment logic, queue trigger
- /build-server → Docker builder image, file extraction, build
- /s3-reverse-proxy → Serves deployments by subdomain, with auth

---

## 🧪 Getting Started (Local Dev)

```bash
# 1. Install dependencies
cd api-server && npm install
cd build-server && npm install
cd s3-reverse-proxy && npm install

# 2. Set up your .env files with Mongo, Redis, AWS keys

# 3. Start the servers
cd s3-reverse-proxy && npm run dev     # Serve deployments
cd api-server && npm run dev           # Handle uploads + deploy queue
```
