
# InfluxDB, Telegraf, and Grafana in Docker

This Docker setup deploys a fully integrated stack of InfluxDB, Telegraf, and Grafana, connecting all services with a single token. It includes two sample dashboards as examples.
In essence, this is a ready-to-use system for collecting data from any sensors or any data sources.

## Setup

If you need specific security settings, rename the `.env.example` file to `.env` and fill it out.

### InfluxDB Initialization

1. To initialize the InfluxDB database, run the following command once:
   ```bash
   docker compose up influxdb_cli
   ```
   After initialization (wait 10–15 seconds), press `Ctrl + C`.

2. Start all services:
   ```bash
   docker compose up -d
   ```

3. Stop all services:
   ```bash
   docker compose down
   ```

### Start Grafana Only

```bash
docker compose up -f docker-compose-only-grafana.yml -d
```

### Folder Structure

- `telegraf/telegraf-conf/` – Telegraf configuration files
  - `telegraf.conf` – contains the configured output to InfluxDB.
  - `telegraf.d/` – folder with input configurations for various data sources.
- `telegraf/mibs/` – MIB files for polling SNMP devices (replaces `/usr/share/snmp/mibs`).

### Services

- Grafana: http://localhost:3000  
  Login/Password: admin / admingrafana

- InfluxDB: http://localhost:8086  
  Login/Password: admin / admininflux

## Important

Tokens and passwords are fixed – this setup is for learning and getting familiar with the technologies.

Recommended:
- Generate a new token in the InfluxDB interface.
- Insert this token into the `telegraf.conf` configuration file.
- Add a new data source in Grafana using this token.
- Finally, change the passwords for the InfluxDB and Grafana web interfaces to secure and unique ones.

### Configuration

- Grafana: Configured via environment variables in `docker-compose.yml`.
- InfluxDB: Data is stored in the `influxdb2` directory and configured via environment variables in `docker-compose.yml`.
- Telegraf: Configurations are specified in `telegraf/telegraf.conf`.

### Network and Volumes

- Network: lab240-monitoring
- Volumes:
  - grafana-data: Grafana data
  - ./influxdb2: InfluxDB data