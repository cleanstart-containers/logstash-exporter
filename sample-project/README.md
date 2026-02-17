# Logstash Exporter Sample Project

This sample shows how to run the **CleanStart Logstash Exporter** container and optionally run it with Logstash so the exporter can scrape the Logstash monitoring API and expose Prometheus metrics.

## Project structure

| File | Description |
|------|-------------|
| `.env` | Config for the exporter (required; copy from `.env.example` if missing). Sets `LOGSTASH_URL`. |
| `.env.example` | Template for `.env`. |
| `docker-compose.yaml` | Runs Logstash and the exporter together. |
| `README.md` | This file. |

## Option A: Run with Docker Compose (recommended)

Runs Logstash and the exporter. The exporter scrapes Logstash at `http://logstash:9600` and serves metrics on port 9198.

```bash
# From the sample-project directory
docker compose up -d
```

- **Logstash** listens on 9600 (monitoring API) and 5044 (Beats). It may take 60–90 seconds to become ready.
- **Exporter** listens on 9198. You may see “connection refused” in logs until Logstash is up; the exporter will then connect.

**Metrics:** http://localhost:9198/metrics  

**Stop:**

```bash
docker compose down
```

## Option B: Run the exporter only (`docker run`)

Use this when Logstash runs elsewhere (host or another stack). The container **requires a `.env` file**; without it you get: `open .env: no such file or directory`.

From the **sample-project** directory (so `.env` exists):

```bash
docker run --rm -p 9198:9198 \
  -w /app \
  -v "$(pwd)/.env:/app/.env:ro" \
  cleanstart/logstash-exporter:latest
```

- `-w /app` — working directory so the app finds `.env` at `/app/.env`.
- `-v .../.env:/app/.env:ro` — mount your `.env` into the container.

If no Logstash is reachable at the URL in `.env`, you will see **connection refused** to port 9600. The exporter still listens on 9198 and serves http://localhost:9198/metrics (metrics will be empty or partial until Logstash is reachable).

To point at Logstash on your **host**: set in `.env`:

```bash
LOGSTASH_URL=http://host.docker.internal:9600
```

(Mac/Windows Docker; on Linux you may need your host IP.)

## Configuration

| Variable | Description |
|----------|-------------|
| `LOGSTASH_URL` | Logstash monitoring API URL (default: `http://localhost:9600`). |

Edit `.env` or pass `-e LOGSTASH_URL=...` (with a mounted `.env` so the file open still succeeds).

## Pull the image

```bash
docker pull cleanstart/logstash-exporter:latest
docker pull cleanstart/logstash-exporter:latest-dev
```

## Access the metrics endpoint

Open: **http://localhost:9198/metrics**

You should see Prometheus-format metrics for Logstash (once Logstash is running and reachable at `LOGSTASH_URL`).

## Resources

- [CleanStart](https://cleanstart.com/)
- [Logstash Exporter (prometheus-community)](https://github.com/prometheus-community/logstash_exporter)

## License

This project is open source and available under the [MIT License](LICENSE).
