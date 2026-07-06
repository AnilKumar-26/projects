# Dockerized Flask API

A small Flask API demonstrating a **multi-stage Docker build** — separating dependency installation from the final runtime image to keep the production image lean.

## What it does
- `GET /` — returns a JSON response with hostname and timestamp (proves the container is actually serving requests)
- `GET /health` — health check endpoint used by Docker's built-in `HEALTHCHECK`

## Why multi-stage build
The `Dockerfile` uses two stages:
1. **Builder stage** — installs Python dependencies (Flask and its requirements)
2. **Runtime stage** — starts fresh from a slim base image and copies only the installed packages and application code from the builder stage

This keeps build tools and intermediate files out of the final image, resulting in a smaller, more secure production image (44.8MB content size).

## Running locally
```bash
docker build -t dockerized-api .
docker run -d -p 5000:5000 --name dockerized-api dockerized-api
curl http://localhost:5000/
curl http://localhost:5000/health
```

Or with Docker Compose:
```bash
docker compose up -d
```

## Tech stack
- Python 3.12 (slim base image)
- Flask 3.0.3
- Docker multi-stage build
