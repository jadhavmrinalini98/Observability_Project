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
<img width="1080" height="593" alt="Screenshot 2025-08-11 at 10 32 22 AM" src="https://github.com/user-attachments/assets/56e78ba3-5cce-4d9c-b6b7-2bf152027a16" />
<img width="1440" height="900" alt="Screenshot 2025-08-10 at 9 49 58 PM" src="https://github.com/user-attachments/assets/332ef3d0-3ac3-4b8e-ab2e-1b0ed1f54730" />
<img width="1440" height="900" alt="Screenshot 2025-08-10 at 9 49 53 PM" src="https://github.com/user-attachments/assets/ea27f0ca-1dd1-4ec2-9556-d9568070d180" />
<img width="1440" height="900" alt="Screenshot 2025-08-09 at 8 35 54 PM" src="https://github.com/user-attachments/assets/35e0ba17-3c5f-4591-a5ce-b11960d55239" />


## 📥 Installation

```bash
# Clone repository
git clone https://github.com/<your-username>/Observability_Project.git
cd Observability_Project

# Install dependencies
npm install
Core dependencies:

npm install express prom-client response-time
▶️ Running the App Locally

npm start
# or for development with auto-reload:
npm run dev
The app will start on http://localhost:3000.

🔗 API Endpoints
Method	Path	Description
GET	/	Health check
GET	/slow	Simulates a slow task with random delays/errors
GET	/metrics	Prometheus metrics in exposition format

Example:
curl http://localhost:3000/
curl http://localhost:3000/slow
curl http://localhost:3000/metrics

📊 Prometheus Setup
prometheus-config.yml:

global:
  scrape_interval: 5s

scrape_configs:
  - job_name: prometheus
    static_configs:
      - targets: ['localhost:9090']

  - job_name: node_app
    metrics_path: /metrics
    static_configs:
      - targets: ['host.docker.internal:3000']  # macOS/Windows host
      # If running in the same Docker Compose network:
      # - targets: ['node_app:3000']
Run Prometheus:


docker run -d --name prometheus \
  -p 9090:9090 \
  -v "$PWD/prometheus-config.yml:/etc/prometheus/prometheus.yml:ro" \
  prom/prometheus

Prometheus UI: http://localhost:9090
Targets page: http://localhost:9090/targets

📈 Grafana Setup
Run Grafana:

docker run -d --name grafana -p 8080:3000 grafana/grafana-oss
Login: http://localhost:8080 (default: admin / admin)

Add Prometheus Data Source:

URL:

http://localhost:9090 (Grafana on host)

http://host.docker.internal:9090 (Grafana in Docker on macOS/Windows)

http://prometheus:9090 (same Compose network)

🐳 Docker Compose (Prometheus + Grafana)
docker-compose.yml:

services:
  prometheus:
    image: prom/prometheus
    ports:
      - "9090:9090"
    volumes:
      - ./prometheus-config.yml:/etc/prometheus/prometheus.yml:ro

  grafana:
    image: grafana/grafana-oss
    ports:
      - "8080:3000"
    depends_on:
      - prometheus
Run both:

docker compose up -d

📂 Project Structure
bash
Copy
Edit
.
├── index.js                  # Express app
├── utils.js                  # Heavy task simulation
├── prometheus-config.yml     # Prometheus configuration
├── docker-compose.yml        # Optional: Prometheus + Grafana
├── package.json
└── README.md

🛠 Troubleshooting
Prometheus target DOWN

If Node app is on host: use host.docker.internal:3000 in prometheus-config.yml

If in Compose: use service name (e.g., node_app:3000)

Ensure Node binds to 0.0.0.0

Grafana can’t connect to Prometheus

Grafana in Docker on macOS/Windows → host.docker.internal:9090

Both in Compose → prometheus:9090

prom-client error: Missing mandatory help parameter

All metrics need name and help:

new client.Counter({ name: 'http_requests_total', help: 'Total HTTP requests' });



