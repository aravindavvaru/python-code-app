# Python Flask App

A minimal Python Flask microservice with health and info endpoints, packaged for Kubernetes deployment.

## Features

- Flask web application
- `/api/v1/info` endpoint returns current time, hostname, message, and deployment target
- `/api/v1/healthz` endpoint returns a simple health status
- Kubernetes manifests under `k8s/`
- Helm chart under `charts/python-app/`
- Backstage scaffolder template in `template.yaml`

## Project Structure

- `src/app.py` — Flask application source code
- `requirements.txt` — Python dependency lockfile
- `k8s/` — Kubernetes manifests for Deployment, Service, and Ingress
- `charts/python-app/` — Helm chart package files
- `docs/index.md` — quick documentation for endpoints and access
- `template.yaml` — Backstage software template definitions
- `catalog-info.yaml` — Backstage component metadata

## Local Development

1. Create a Python virtual environment:

   ```bash
   python3 -m venv .venv
   source .venv/bin/activate
   ```

2. Install dependencies:

   ```bash
   pip install -r requirements.txt
   ```

3. Run the application:

   ```bash
   python src/app.py
   ```

4. Access endpoints:

   - `http://localhost:5000/api/v1/info`
   - `http://localhost:5000/api/v1/healthz`

## Docker

The repository does not include a built image, but you can containerize the app using a Dockerfile.

Example Docker build command:

```bash
docker build -t python-app:local .
```

Run it locally:

```bash
docker run -p 5000:5000 python-app:local
```

## Kubernetes Deployment

The `k8s/` folder contains example Kubernetes manifests:

- `k8s/deploy.yaml`
- `k8s/service.yaml`
- `k8s/ingress.yaml`

Apply them with:

```bash
kubectl apply -f k8s/deploy.yaml
kubectl apply -f k8s/service.yaml
kubectl apply -f k8s/ingress.yaml
```

The app listens on port `5000`, while the Kubernetes Service exposes port `8080`.

### Helm Chart

A Helm chart is available under `charts/python-app/`.

Install the chart with:

```bash
helm install python-app charts/python-app
```

Update chart values in `charts/python-app/values.yaml`, including image repository, tag, replicas, and ingress host.

## Backstage Template

This repository includes a Backstage scaffolder template in `template.yaml` for provisioning a new Python Flask service.

## API Endpoints

- `GET /api/v1/info`
- `GET /api/v1/healthz`

## Notes

- The `/api/v1/healthz` endpoint currently returns a static `up` response. You can extend it with real health checks.
- The app is configured to run on `0.0.0.0` so it is ready for container and Kubernetes deployments.
