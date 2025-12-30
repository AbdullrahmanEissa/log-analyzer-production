# 🔍 Log Analyzer – Dev vs Production Architecture (Docker + Nginx)

A **production-minded full-stack application** that analyzes raw logs and returns structured insights  
(Errors, Warnings, Info, timestamps, keywords).

This project is intentionally built **twice** to demonstrate the **real difference between Development and Production deployments** — not just “how to run Docker”.

---

## 🚀 Why This Project Exists

Most tutorials stop at:
> “It works on my machine.”

This project goes further and answers:
- Why Dev ≠ Production
- Why `localhost` works sometimes and fails other times
- Why frontend should NOT know backend location in production
- How Docker, networking, and Nginx actually fit together

This is **infrastructure thinking**, not just coding.

---

## 🧱 Tech Stack

### Backend
- Node.js + Express
- Stateless API
- Dockerized

### Frontend
- React (Vite)
- SPA (Single Page Application)
- Docker multi-stage build

### Infrastructure
- Docker & Docker Compose
- Nginx (Reverse Proxy + Static Server)
- Internal Docker networking

---

## 🧪 Architecture 1: Development (Docker Dev Server)

### Purpose
Fast iteration, debugging, and learning.

### How it works
- Frontend runs via **Vite Dev Server**
- Backend runs via **Node.js**
- Both run inside Docker containers
- Browser communicates directly with backend

### API Configuration
```js
const API_URL = 'http://localhost:5000';
````

### Request Flow

```
Browser → Frontend Dev Server → Backend
```

### Why this is OK

* Simple
* Explicit
* Ideal for development and teaching

---

## 🚀 Architecture 2: Production (Nginx + SPA Build)

### Purpose

Real-world, production-grade deployment.

### How it works

* Frontend is built once (`npm run build`)
* Static files served by **Nginx**
* Nginx acts as **Reverse Proxy** for `/api`
* Frontend has zero knowledge of backend location

### API Configuration

```js
const API_URL = '';
```

### Request Flow

```
Browser → Nginx → Backend
```

### Why this is the correct approach

* Cleaner architecture
* More secure
* Scales naturally
* Matches real production systems

---

## 📁 Project Structure

```
log-analyzer/
│
├── backend/
│   ├── Dockerfile
│   └── index.js
│
├── frontend/
│   ├── Dockerfile          # Multi-stage (build + nginx)
│   ├── nginx.conf          # SPA + reverse proxy
│   ├── src/
│   └── dist/
│
├── docker-compose.dev.yml
├── docker-compose.prod.yml
└── README.md
```

---

## 🐳 Docker – Key Concepts Demonstrated

### ✅ Multi-Stage Builds

* Build tools stay out of production images
* Smaller, safer containers

### ✅ Internal Docker DNS

* Containers communicate via service names (`backend`)
* Browser never sees internal addresses

### ✅ Port Mapping vs Internal Networking

| Context    | Address               |
| ---------- | --------------------- |
| Browser    | `localhost:5000`      |
| Containers | `http://backend:5000` |

---

## ▶️ How to Run

### Development

```bash
docker compose -f docker-compose.dev.yml up --build
```

Frontend:

```
http://localhost:5173
```

Backend:

```
http://localhost:5000
```

---

### Production

```bash
docker compose -f docker-compose.prod.yml up --build
```

Application:

```
http://localhost
```

---

## 🎓 Teaching Value

This project clearly demonstrates:

* Why Dev and Prod are different
* Why reverse proxies exist
* Why frontend should be backend-agnostic
* Why Docker networking matters

Students don’t just **run commands** — they **understand systems**.

---

## 🧠 Interview Talking Points

* “I separated development and production architectures intentionally.”
* “Frontend does not depend on backend location in production.”
* “Nginx handles routing and proxying, not the frontend.”
* “Docker DNS is internal; browsers never see service names.”

---

## 🏁 Final Note

This project is not about frameworks.

It’s about:

> **Thinking like an engineer who deploys systems, not just writes code.**

---

⭐ If you found this useful, feel free to fork, study, or extend it.

قول وأنا أظبطهولك 👊
```
