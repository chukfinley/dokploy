# Linkwarden

This directory contains the Docker Compose setup for Linkwarden, a self-hosted, open-source solution for bookmark management.

## Files

- `compose.yml`: Defines the Linkwarden application service and its PostgreSQL database.
- `env`: Contains environment variables for Linkwarden and PostgreSQL configuration.
- `net`: Specifies network-related configurations for accessing the Linkwarden service.

## Configuration

### Environment Variables (`env` file)

The `env` file in this directory is used to set environment variables for the Linkwarden and PostgreSQL services. The following variables are expected:

- `POSTGRES_PASSWORD`: The password for the PostgreSQL user `linkwarden`. **Crucial for database security.**
- `NEXTAUTH_SECRET`: A secret key used by NextAuth.js for session and JWT encryption. **Crucial for security.**
- `NEXTAUTH_URL`: The base URL for NextAuth.js callbacks (e.g., `https://link.example.com/api/auth`).

**Example `env` file content:**
```
POSTGRES_PASSWORD=your_postgres_password
NEXTAUTH_SECRET=your_nextauth_secret
NEXTAUTH_URL=https://link.example.com/api/v1/auth
```
Remember to replace placeholder values with your actual configuration.

### Network Configuration (`net` file)

The `net` file provides specific network configuration parameters for accessing the Linkwarden service. The following parameters are used:

- `Service Name`: `linkwarden`
- `Host`: The domain name for accessing the Linkwarden instance (e.g., `link.example.com`).
- `Path`: The URL path for the service.
- `Internal Path`: The internal path within the container.
- `Stripe Path`: Boolean indicating if the path should be stripped.
- `Conatiner Port`: The internal port of the service within the container (default: `3000`).
- `HTTPS`: Boolean indicating if HTTPS is enabled.
- `Certificate Provider`: The certificate provider (e.g., Let's Encrypt).

**Example `net` file content:**
```
Service Name=linkwarden
Host=link.example.com
Path=/
Internal Path=/
Stripe Path=False
Conatiner Port=3000
HTTPS=True
Certificate Provider=Let's Encrypt
```

## Dokploy Deployment

It is highly recommended to include `pull_policy: always` for each service in your `compose.yml` file. This ensures that Dokploy always pulls the latest image from the registry when deploying or updating your application, preventing issues with outdated images.

The `compose.yml` for Linkwarden already includes `pull_policy: always` for both `linkwarden` and `postgres` services.

```yaml
services:
  linkwarden:
    image: ghcr.io/linkwarden/linkwarden:latest
    pull_policy: always
    # ... other configurations
  postgres:
    image: postgres:17-alpine
    pull_policy: always
    # ... other configurations
