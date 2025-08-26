# Kutt

This directory contains the Docker Compose setup for Kutt, a modern URL shortener with custom domains and many features.

## Files

- `compose.yml`: Defines the Kutt service and its volumes.
- `env`: Contains environment variables for Kutt configuration, including JWT secret, domain settings, and mail server details.
- `net`: Specifies network-related configurations for accessing the Kutt service.

## Configuration

### Environment Variables (`env` file)

The `env` file in this directory is used to set environment variables for the Kutt service. The following variables are expected:

- `JWT_SECRET`: A secret key for JSON Web Token (JWT) generation. **Crucial for security.**
- `DOMAIN`: The default domain for shortened URLs (e.g., `kutt.example.com`).
- `TRUST_PROXY`: Set to `true` if Kutt is behind a proxy (e.g., Dokploy's ingress).
- `DISALLOW_ANONYMOUS_LINKS`: Set to `true` to prevent anonymous users from creating links.
- `CUSTOM_DOMAIN_USE_HTTPS`: Set to `true` to force HTTPS for custom domains.
- `MAIL_ENABLED`: Set to `true` to enable email features (e.g., for user registration, password reset).
- `MAIL_HOST`: SMTP host for sending emails.
- `MAIL_PORT`: SMTP port.
- `MAIL_SECURE`: Set to `true` for secure SMTP connection (TLS/SSL).
- `MAIL_USER`: SMTP username.
- `MAIL_FROM`: Email address to send from.
- `MAIL_PASSWORD`: SMTP password.
- `CONTACT_EMAIL`: Contact email address for users.

**Example `env` file content:**
```
JWT_SECRET=your_jwt_secret_here
DOMAIN=kutt.example.com
TRUST_PROXY=false
DISALLOW_ANONYMOUS_LINKS=true
CUSTOM_DOMAIN_USE_HTTPS=true
MAIL_ENABLED=false
MAIL_HOST=''
MAIL_PORT='22'
MAIL_SECURE=true
MAIL_USER=''
MAIL_FROM=''
MAIL_PASSWORD=''
CONTACT_EMAIL=''
```
Remember to replace placeholder values with your actual configuration.

### Network Configuration (`net` file)

The `net` file provides specific network configuration parameters for accessing the Kutt service. The following parameters are used:

- `Service Name`: `kutt`
- `Host`: The domain name for accessing the Kutt service (e.g., `kutt.example.com`).
- `Path`: The URL path for the service.
- `Internal Path`: The internal path within the container.
- `Stripe Path`: Boolean indicating if the path should be stripped.
- `Conatiner Port`: The internal port of the service within the container (default: `3000`).
- `HTTPS`: Boolean indicating if HTTPS is enabled.
- `Certificate Provider`: The certificate provider (e.g., Let's Encrypt).

**Example `net` file content:**
```
Service Name=kutt
Host=kutt.example.com
Path=/
Internal Path=/
Stripe Path=False
Conatiner Port=3000
HTTPS=True
Certificate Provider=Let's Encrypt
```

### Volumes

The `compose.yml` defines a volume for custom Kutt files:

```yaml
volumes:
  - ./kutt/custom:/kutt/custom
```
This volume maps a local `kutt/custom` directory to `/kutt/custom` inside the container, allowing you to add custom files or configurations.

## Dokploy Deployment

It is highly recommended to include `pull_policy: always` for each service in your `compose.yml` file. This ensures that Dokploy always pulls the latest image from the registry when deploying or updating your application, preventing issues with outdated images.

The `compose.yml` for Kutt already includes `pull_policy: always`.

```yaml
services:
  kutt:
    image: kutt/kutt:main
    pull_policy: always
    # ... other configurations
