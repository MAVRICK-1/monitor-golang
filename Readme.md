# MyApp with Prometheus and Grafana Integration

## Overview

This project demonstrates the integration of a Go-based web application with Prometheus and Grafana for monitoring and metrics visualization. The application simulates device management, providing endpoints to register devices, manage device firmware, and handle user logins.

## Prerequisites

Ensure you have the following installed on your machine:

- Docker
- Docker Compose

## Project Structure

```
.
├── my-app
│   ├── Dockerfile
│   └── main.go
├── prometheus
│   └── prometheus.yml
├── grafana
│   └── datasources.yaml
├── docker-compose.yml
└── README.md
```

## Getting Started

### Step 1: Clone the Repository

```bash
git clone https://github.com/yourusername/myapp-prometheus-grafana.git
cd myapp-prometheus-grafana
```

### Step 2: Build and Run the Containers

Using Docker Compose, you can build and start the application and its monitoring tools.

```bash
docker-compose up --build
```

This command will build the Go application and start the containers for the application, Prometheus, and Grafana.

### Step 3: Access the Services

- **MyApp API**: [http://localhost:8080](http://localhost:8080)
- **Prometheus**: [http://localhost:9090](http://localhost:9090)
- **Grafana**: [http://localhost:3000](http://localhost:3000)

### Grafana Default Credentials

- Username: `admin`
- Password: `devops123`

## API Endpoints

### `/devices`

- `GET /devices`: Retrieve the list of registered devices.
- `POST /devices`: Register a new device.

### `/devices/{id}`

- `PUT /devices/{id}`: Upgrade the firmware of a device.

### `/login`

- `POST /login`: Handle user login.

## Prometheus Metrics

The application exposes various metrics at [http://localhost:8081/metrics](http://localhost:8081/metrics).

### Metrics Exposed

- `myapp_connected_devices`: Number of currently connected devices.
- `myapp_info`: Information about the application version.
- `myapp_device_upgrade_total`: Number of device upgrades.
- `myapp_request_duration_seconds`: Duration of the requests.
- `myapp_login_request_duration_seconds`: Duration of login requests.

## Monitoring and Visualization

### Prometheus Configuration

The Prometheus configuration is defined in `prometheus/prometheus.yml`. This file sets up Prometheus to scrape metrics from the MyApp API.

### Grafana Configuration

Grafana is configured with a datasource to pull data from Prometheus. The configuration is defined in `grafana/datasources.yaml`.

### Creating Dashboards

To visualize the metrics:

1. Log in to Grafana at [http://localhost:3000](http://localhost:3000).
2. Create a new dashboard.
3. Add panels to visualize the metrics exposed by the application.

## Sample `prometheus.yml`

```yaml
global:
  scrape_interval: 15s

scrape_configs:
  - job_name: 'myapp'
    static_configs:
      - targets: ['myapp:8081']
```

## Sample `datasources.yaml`

```yaml
apiVersion: 1
datasources:
  - name: Prometheus
    type: prometheus
    access: proxy
    url: http://prometheus:9090
    isDefault: true
```

## Conclusion

With this setup, you have a Go application integrated with Prometheus for monitoring and Grafana for visualization. You can extend this setup by adding more metrics, creating sophisticated Grafana dashboards, and exploring alerting mechanisms using Prometheus.

Feel free to modify and extend this example to suit your needs. If you encounter any issues, please refer to the official documentation of [Prometheus](https://prometheus.io/docs/introduction/overview/) and [Grafana](https://grafana.com/docs/grafana/latest/getting-started/).

---

Enjoy monitoring your application! 🚀