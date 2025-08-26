# Gotify

This directory contains the Docker Compose setup for Gotify, a simple server for sending and receiving messages.

## Files

- `compose.yml`: Defines the Gotify server and its PostgreSQL database service.
- `env`: Contains environment variables for Gotify configuration.
- `net`: Specifies network-related configurations for accessing the Gotify server.

## Configuration

### Environment Variables (`env` file)

The `env` file in this directory is used to set environment variables for the Gotify service. The following variables are expected:

- `GOTIFY_SERVER_WEBSOCKET_ORIGIN`: The WebSocket origin for the Gotify server (e.g., `"go.example.com"`).
- `GOTIFY_DEFAULTUSER_PASS`: The default password for the `admin` user.

**Example `env` file content:**
```
GOTIFY_SERVER_WEBSOCKET_ORIGIN="go.example.com"
GOTIFY_DEFAULTUSER_PASS=yourpassword #user is admin
```
Remember to replace `yourpassword` with a strong, secure password.

### Network Configuration (`net` file)

The `net` file provides specific network configuration parameters for accessing the Gotify service. The following parameters are used:

- `Service Name`: `gotify`
- `Host`: The domain name for accessing the Gotify server (e.g., `go.example.com`).
- `Path`: The URL path for the service.
- `Internal Path`: The internal path within the container.
- `Stripe Path`: Boolean indicating if the path should be stripped.
- `Conatiner Port`: The internal port of the service within the container (default: `80`).
- `HTTPS`: Boolean indicating if HTTPS is enabled.
- `Certificate Provider`: The certificate provider (e.g., Let's Encrypt).

**Example `net` file content:**
```
Service Name=gotify
Host=go.example.com
Path=/
Internal Path=/
Stripe Path=False
Conatiner Port=80
HTTPS=True
Certificate Provider=Let's Encrypt
```

## Dokploy Deployment

It is highly recommended to include `pull_policy: always` for each service in your `compose.yml` file. This ensures that Dokploy always pulls the latest image from the registry when deploying or updating your application, preventing issues with outdated images.

The `compose.yml` for Gotify already includes `pull_policy: always` for both `gotify` and `postgres` services.

```yaml
services:
  gotify:
    image: gotify/server:latest
    pull_policy: always
    # ... other configurations
  postgres:
    image: postgres:17.2
    pull_policy: always
    # ... other configurations
