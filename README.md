# Influx & Grafana in Docker

If you need specific security settings, rename the `.env.example` file to `.env` and fill it out.

## Setup Instructions

### InfluxDB Initialization

1. Run the following command to initialize InfluxDB:

    ```bash
    docker compose up influxdb_cli
    ```

    Press `Ctrl + C` after the database initialization (wait 10-15 seconds).

2. Start the services:

    ```bash
    docker compose up -d
    ```

### Start grafana only

    ```bash
    docker compose up -d grafana
    ```

### Services

- **Grafana**: Accessible at `http://localhost:3000`
- **InfluxDB**: Accessible at `http://localhost:8086`

### Configuration

- **Grafana**: Configuration is managed via environment variables in the `docker-compose.yml` file.
- **InfluxDB**: Data is stored in the `influxdb2` directory and configured via environment variables in the `docker-compose.yml` file.
- **Telegraf**: Configuration is managed in the `telegraf/telegraf.conf` file.

### Network and Volumes

- **Network**: `lab240-monitoring`
- **Volumes**:
  - `grafana-data`: Stores Grafana data
  - `./influxdb2`: Stores InfluxDB data
