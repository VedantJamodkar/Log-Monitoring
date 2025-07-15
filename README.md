# 🚀 Grafana Loki Log Monitoring Pipeline

This project sets up a **Dockerized log monitoring and visualization pipeline** using:

- **Grafana** (visualization)
- **Loki** (log aggregation)
- **Promtail** (log shipper)
- **GitHub Actions** (CI/CD pipeline)

Logs are ingested from structured JSON files (e.g., robot logs) and visualized through Grafana with filtering capabilities.

---

## 📁 Project Structure
.
├── docker-compose.yml # Orchestrates Loki, Promtail, Grafana
├── loki-config.yaml # Loki configuration
├── promtail-config.yaml # Promtail configuration
├── logs/
│ └── sample.log # Input structured JSON log file
├── positions.yaml # File position tracking (Promtail)
├── .github/
│ └── workflows/
│ └── deploy.yml # GitHub Actions CI/CD pipeline


---

## 📦 Components

### 1. **Promtail**
- Reads JSON logs from `logs/sample.log`
- Applies label & field extraction using pipeline stages
- Sends logs to Loki

### 2. **Loki**
- Stores logs with extracted metadata
- Supports powerful log queries via LogQL

### 3. **Grafana**
- Connects to Loki
- Allows filtering by:
  - `observed_timestamp_rfc3339`
  - `instrumentation_scope`
  - `severity_text`
  - And others...

---

## 📸 Grafana Dashboard Features

- JSON logs parsed and indexed
- Filter logs by:
  - Severity (e.g., `CRITICAL`, `INFO`)
  - Instrumentation scope
  - Timestamps
- Search using LogQL

Example queries:
```logql
{job="robot-logs"}                              # All logs
{job="robot-logs", severity_text="CRITICAL"}    # Only critical logs
{job="robot-logs"} |= "redis"                   # Logs containing the word 'redis'

🐳 Dockerized Setup
🔧 To Run Locally:
docker compose up -d --build
Visit:

Grafana: http://localhost:3000

Username: admin

Password: admin

⚙️ CI/CD Pipeline
This project includes a GitHub Actions workflow:

Trigger: On push to main

Action:

Pull latest code

Install Docker & Compose

Deploy the stack using docker compose

You can find the workflow at:
.github/workflows/deploy.yml

🧪 Test It
Once running:

Open Grafana.

Add a Loki data source pointing to http://loki:3100.

Create dashboard with logs table.

Use filters such as:

{job="robot-logs"}

{job="robot-logs", severity_text="CRITICAL"}

