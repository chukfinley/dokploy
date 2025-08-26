# Jellyfin

This directory contains the Docker Compose setup for Jellyfin, a free software media system that puts you in control of managing and streaming your media.

## Files

- `compose.yml`: Defines the Jellyfin service and its volumes.
- `env`: Contains environment variables for Jellyfin configuration.
- `net`: Specifies network-related configurations for accessing the Jellyfin server.

## Configuration

### Environment Variables (`env` file)

The `env` file in this directory is used to set environment variables for the Jellyfin service. The following variable is expected:

- `JELLYFIN_PUB`: The public URL where your Jellyfin server will be accessible. This is used by Jellyfin to correctly generate links and serve content.

**Example `env` file content:**
```
JELLYFIN_PUB=https://jelly.example.com
```
Remember to replace `https://jelly.example.com` with your actual public URL.

### Network Configuration (`net` file)

The `net` file provides specific network configuration parameters for accessing the Jellyfin service. The following parameters are used:

- `Service Name`: `jellyfin`
- `Host`: The domain name for accessing the Jellyfin server (e.g., `jelly.example.com`).
- `Path`: The URL path for the service.
- `Internal Path`: The internal path within the container.
- `Stripe Path`: Boolean indicating if the path should be stripped.
- `Conatiner Port`: The internal port of the service within the container (default: `8096`).
- `HTTPS`: Boolean indicating if HTTPS is enabled.
- `Certificate Provider`: The certificate provider (e.g., Let's Encrypt).

**Example `net` file content:**
```
Service Name=jellyfin
Host=jelly.example.com
Path=/
Internal Path=/
Stripe Path=False
Conatiner Port=8096
HTTPS=True
Certificate Provider=Let's Encrypt
```

### Volumes

The `compose.yml` defines several volumes for Jellyfin. Pay special attention to the `media-music` volume:

```yaml
volumes:
  media-music:
    driver: local
    driver_opts:
      type: none
      o: bind
      device: /path/to/your/media
```
You **must** change `/path/to/your/media` to the actual path on your host system where your media files are stored.

## Dokploy Deployment

It is highly recommended to include `pull_policy: always` for each service in your `compose.yml` file. This ensures that Dokploy always pulls the latest image from the registry when deploying or updating your application, preventing issues with outdated images.

The `compose.yml` for Jellyfin already includes `pull_policy: always`.

```yaml
services:
  jellyfin:
    image: jellyfin/jellyfin:latest
    pull_policy: always
    # ... other configurations
