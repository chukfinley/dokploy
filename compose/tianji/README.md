# Tianji

This directory contains the Docker Compose setup for Tianji, a modern web analytics and monitoring platform.

## Files

- `compose.yml`: Defines the Tianji application service and its PostgreSQL database.
- `env`: Contains environment variables for Tianji configuration, including authentication secrets and API keys.
- `net`: Specifies network-related configurations for accessing the Tianji service.

## Configuration

### Environment Variables (`env` file)

The `env` file in this directory is used to set environment variables for the Tianji service. The following variables are expected:

- `NEXTAUTH_URL`: The base URL for NextAuth.js callbacks (e.g., `https://tianji.example.com`).
- `NEXTAUTH_SECRET`: A secret key used by NextAuth.js for session and JWT encryption. **Crucial for security.**
- `OPENAI_API_KEY`: Your OpenAI API key, if you plan to use features that integrate with OpenAI.
- `JWT_SECRET`: A secret key for JSON Web Token (JWT) generation. **Crucial for security.**

**Example `env` file content:**
```
NEXTAUTH_URL="https://tianji.example.com"
NEXTAUTH_SECRET=replace-me-with-32-chars-or-more
OPENAI_API_KEY=sk-placeholder-not-used #replace with real api key if you want
JWT_SECRET=replace-me-with-a-random-string
```
Remember to replace placeholder values with your actual configuration.

### Network Configuration (`net` file)

The `net` file provides specific network configuration parameters for accessing the Tianji service. The following parameters are used:

- `Service Name`: `tianji`
- `Host`: The domain name for accessing the Tianji instance (e.g., `tianji.example.com`).
- `Path`: The URL path for the service.
- `Internal Path`: The internal path within the container.
- `Stripe Path`: Boolean indicating if the path should be stripped.
- `Conatiner Port`: The internal port of the service within the container (default: `12345`).
- `HTTPS`: Boolean indicating if HTTPS is enabled.
- `Certificate Provider`: The certificate provider (e.g., Let's Encrypt).

**Example `net` file content:**
```
Service Name=tianji
Host=tianji.example.com
Path=/
Internal Path=/
Stripe Path=False
Conatiner Port=12345
HTTPS=True
Certificate Provider=Let's Encrypt
```

## Dokploy Deployment

It is highly recommended to include `pull_policy: always` for each service in your `compose.yml` file. This ensures that Dokploy always pulls the latest image from the registry when deploying or updating your application, preventing issues with outdated images.

The `compose.yml` for Tianji already includes `pull_policy: always` for the `tianji` service.

```yaml
services:
  tianji:
    image: moonrailgun/tianji:latest
    pull_policy: always
    # ... other configurations
