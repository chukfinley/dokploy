# OpenGist

This directory contains the Docker Compose setup for OpenGist, a self-hosted pastebin/gist service.

## Files

- `compose.yml`: Defines the OpenGist service.
- `env`: Contains environment variables for OpenGist configuration, including user/group IDs and logging level.
- `net`: Specifies network-related configurations for accessing the OpenGist service.

## Configuration

### Environment Variables (`env` file)

The `env` file in this directory is used to set environment variables for the OpenGist service. The following variables are expected:

- `UID`: User ID for the OpenGist process within the container.
- `GID`: Group ID for the OpenGist process within the container.
- `OG_LOG_LEVEL`: Logging level for OpenGist (e.g., `info`, `debug`, `warn`, `error`).

**Example `env` file content:**
```
UID=1001
GID=1001
OG_LOG_LEVEL=info
```
Adjust `UID` and `GID` to match your system's user and group IDs if necessary for volume permissions.

### Network Configuration (`net` file)

The `net` file provides specific network configuration parameters for accessing the OpenGist service. The following parameters are used:

- `Service Name`: `opengist`
- `Host`: The domain name for accessing the OpenGist instance (e.g., `gist.example.com`).
- `Path`: The URL path for the service.
- `Internal Path`: The internal path within the container.
- `Stripe Path`: Boolean indicating if the path should be stripped.
- `Conatiner Port`: The internal port of the service within the container (default: `6157`).
- `HTTPS`: Boolean indicating if HTTPS is enabled.
- `Certificate Provider`: The certificate provider (e.g., Let's Encrypt).

**Example `net` file content:**
```
Service Name=opengist
Host=gist.example.com
Path=/
Internal Path=/
Stripe Path=False
Conatiner Port=6157
HTTPS=True
Certificate Provider=Let's Encrypt
```

## Dokploy Deployment

It is highly recommended to include `pull_policy: always` for each service in your `compose.yml` file. This ensures that Dokploy always pulls the latest image from the registry when deploying or updating your application, preventing issues with outdated images.

The `compose.yml` for OpenGist already includes `pull_policy: always`.

```yaml
services:
  opengist:
    image: ghcr.io/thomiceli/opengist:latest
    pull_policy: always
    # ... other configurations
