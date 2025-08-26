# n8n

This directory contains the Docker Compose setup for n8n, a workflow automation tool.

## Files

- `compose.yml`: Defines the n8n service and its data volume.
- `env`: Contains environment variables for n8n configuration.
- `net`: Specifies network-related configurations for accessing the n8n instance.

## Configuration

### Environment Variables (`env` file)

The `env` file in this directory is used to set environment variables for the n8n service. The following variables are expected:

- `N8N_HOST`: The hostname where n8n will be accessible (e.g., `n8n.example.com`). This is used to construct the `WEBHOOK_URL`.
- `N8N_PORT`: The internal port n8n listens on (default: `5678`).
- `GENERIC_TIMEZONE`: The timezone for the n8n instance (e.g., `Europe/Berlin`).

**Example `env` file content:**
```
N8N_HOST=n8n.example.com
N8N_PORT=5678
GENERIC_TIMEZONE=Europe/Berlin
```
Remember to replace placeholder values with your actual configuration.

### Network Configuration (`net` file)

The `net` file provides specific network configuration parameters for accessing the n8n service. The following parameters are used:

- `Service Name`: `n8n`
- `Host`: The domain name for accessing the n8n instance (e.g., `n8n.example.com`).
- `Path`: The URL path for the service.
- `Internal Path`: The internal path within the container.
- `Stripe Path`: Boolean indicating if the path should be stripped.
- `Conatiner Port`: The internal port of the service within the container (default: `5678`).
- `HTTPS`: Boolean indicating if HTTPS is enabled.
- `Certificate Provider`: The certificate provider (e.g., Let's Encrypt).

**Example `net` file content:**
```
Service Name=n8n
Host=n8n.example.com
Path=/
Internal Path=/
Stripe Path=False
Conatiner Port=5678
HTTPS=True
Certificate Provider=Let's Encrypt
```

## Dokploy Deployment

It is highly recommended to include `pull_policy: always` for each service in your `compose.yml` file. This ensures that Dokploy always pulls the latest image from the registry when deploying or updating your application, preventing issues with outdated images.

**Note:** The current `compose.yml` for n8n does not explicitly include `pull_policy: always`. You might want to add it to ensure the latest image is always pulled.

```yaml
services:
  n8n:
    image: docker.n8n.io/n8nio/n8n:latest
    pull_policy: always # Consider adding this line
    # ... other configurations
