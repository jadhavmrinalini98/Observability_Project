# Observability Project (Node.js + Express + Prometheus + Grafana)

A Node.js/Express application instrumented with [prom-client](https://github.com/siimon/prom-client) for Prometheus metrics and visualized in Grafana.  
It exposes HTTP request counters, latency histograms, and simulates variable workloads for observability testing.

---

## 🚀 Features
- REST API endpoints (`/`, `/slow`)
- Prometheus metrics at `/metrics`
- Request duration histogram
- Total request counter
- Simulated slow tasks & errors
- Dockerized Prometheus & Grafana setup

---

## 📦 Requirements
- **Node.js** ≥ 18
- **npm** ≥ 9
- **Docker Desktop** (or Colima/OrbStack for macOS)
- **Git** (to clone this repository)

---

## 📥 Installation

```bash
# Clone repository
git clone https://github.com/<your-username>/Observability_Project.git
cd Observability_Project

# Install dependencies
npm install
