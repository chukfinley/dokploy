# Postiz

This directory contains the Docker Compose setup for Postiz, a self-hosted platform for managing and publishing content.

## Files

- `compose.yml`: Defines the Postiz application service, along with its PostgreSQL database and Redis cache.
- `env`: Contains environment variables for Postiz configuration, including URLs, secrets, and registration settings.
- `net`: Specifies network-related configurations for accessing the Postiz service.

## Configuration

### Environment Variables (`env` file)

The `env` file in this directory is used to set environment variables for the Postiz service. The following variables are expected:

- `MAIN_URL`: The main URL for the Postiz application.
- `FRONTEND_URL`: The URL for the Postiz frontend.
- `NEXT_PUBLIC_BACKEND_URL`: The public URL for the Postiz backend API.
- `JWT_SECRET`: A secret key for JSON Web Token (JWT) generation. **Crucial for security.**
- `DISABLE_REGISTRATION`: Set to `true` to disable new user registrations.

**Example `env` file content:**
```
DOMAIN=example.com
MAIN_URL=https://postiz.example.com
FRONTEND_URL=https://postiz.example.com
NEXT_PUBLIC_BACKEND_URL=https://postiz.example.com/api
POSTIZ_SECRET_KEY=your_postiz_secret_key_here
JWT_SECRET=replace-me-with-a-long-random-string
DISABLE_REGISTRATION=false
```
Remember to replace placeholder values with your actual configuration.

### Network Configuration (`net` file)

The `net` file provides specific network configuration parameters for accessing the Postiz service. The following parameters are used:

- `Service Name`: `Postiz`
- `Host`: The domain name for accessing the Postiz instance (e.g., `postiz.yourdomain.com`).
- `Path`: The URL path for the service.
- `Internal Path`: The internal path within the container.
- `Stripe Path`: Boolean indicating if the path should be stripped.
- `Conatiner Port`: The internal port of the service within the container (default: `80`).
- `HTTPS`: Boolean indicating if HTTPS is enabled.
- `Certificate Provider`: The certificate provider (e.g., Let's Encrypt).

**Example `net` file content:**
```
Service Name=Postiz
Host=postiz.yourdomain.com
Path=/
Internal Path=/
Stripe Path=False
Conatiner Port=80
HTTPS=True
Certificate Provider=Let's Encrypt
```

## Dokploy Deployment

It is highly recommended to include `pull_policy: always` for each service in your `compose.yml` file. This ensures that Dokploy always pulls the latest image from the registry when deploying or updating your application, preventing issues with outdated images.

**Note:** The current `compose.yml` for Postiz does not explicitly include `pull_policy: always` for any of its services (`postiz`, `postgres`, `redis`). You might want to add it to ensure the latest images are always pulled.

```yaml
services:
  postiz:
    image: ghcr.io/gitroomhq/postiz-app:latest
    pull_policy: always # Consider adding this line
    # ... other configurations
  postgres:
    image: postgres:17-alpine
    pull_policy: always # Consider adding this line
    # ... other configurations
  redis:
    image: redis:7.2-alpine
    pull_policy: always # Consider adding this line
    # ... other configurations
