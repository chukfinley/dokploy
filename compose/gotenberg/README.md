# Gotenberg

This directory contains the Docker Compose setup for Gotenberg, a Docker-powered stateless API for converting HTML, Markdown, and URL to PDF.

## Files

- `compose.yml`: Defines the Gotenberg service.
- `env`: Contains environment variables for Gotenberg's API basic authentication.
- `net`: Specifies network-related configurations for accessing the Gotenberg API.

## Configuration

### Environment Variables (`env` file)

The `env` file in this directory is used to set environment variables for the Gotenberg service. The following variables are expected:

- `GOTENBERG_API_BASIC_AUTH_USERNAME`: Username for basic authentication to the Gotenberg API.
- `GOTENBERG_API_BASIC_AUTH_PASSWORD`: Password for basic authentication to the Gotenberg API.

**Example `env` file content:**
```
GOTENBERG_API_BASIC_AUTH_USERNAME=your_username
GOTENBERG_API_BASIC_AUTH_PASSWORD=your_password
```
Remember to replace `your_username` and `your_password` with your desired credentials.

### Network Configuration (`net` file)

The `net` file provides specific network configuration parameters for accessing the Gotenberg service. The following parameters are used:

- `Service Name`: `gotenberg`
- `Host`: The domain name for accessing the Gotenberg API (e.g., `gotenberg.example.com`).
- `Path`: The URL path for the service.
- `Internal Path`: The internal path within the container.
- `Stripe Path`: Boolean indicating if the path should be stripped.
- `Conatiner Port`: The internal port of the service within the container (default: `3000`).
- `HTTPS`: Boolean indicating if HTTPS is enabled.
- `Certificate Provider`: The certificate provider (e.g., Let's Encrypt).

**Example `net` file content:**
```
Service Name=gotenberg
Host=gotenberg.example.com
Path=/
Internal Path=/
Stripe Path=False
Conatiner Port=3000
HTTPS=True
Certificate Provider=Let's Encrypt
```

## Dokploy Deployment

It is highly recommended to include `pull_policy: always` for each service in your `compose.yml` file. This ensures that Dokploy always pulls the latest image from the registry when deploying or updating your application, preventing issues with outdated images.

The `compose.yml` for Gotenberg already includes `pull_policy: always`.

```yaml
services:
  gotenberg:
    image: gotenberg/gotenberg:latest
    pull_policy: always
    # ... other configurations
