# Example Application

This directory contains the Docker Compose setup for an example application, demonstrating how to configure services for Dokploy.

## Files

- `compose.yml`: Defines the services, volumes, and networks for the example application.
- `env`: Contains environment variables required by the services.
- `net`: Specifies network-related configurations for the application's ingress/proxy settings.

## Configuration

### Environment Variables (`env` file)

The `env` file in this directory is used to set environment variables for the services defined in `compose.yml`. For this example, the following variable is expected:

- `your_secret_key`: A placeholder for a secret key.

**Example `env` file content:**
```
your_secret_key=your_key_here
```

### Network Configuration (`net` file)

The `net` file provides specific network configuration parameters for the application. For this example, the following parameters are used:

- `Service Name`: The name of the service.
- `Host`: The domain name for accessing the service.
- `Path`: The URL path for the service.
- `Internal Path`: The internal path within the container.
- `Stripe Path`: Boolean indicating if the path should be stripped.
- `Conatiner Port`: The internal port of the service within the container.
- `HTTPS`: Boolean indicating if HTTPS is enabled.
- `Certificate Provider`: The certificate provider (e.g., Let's Encrypt).

**Example `net` file content:**
```
Service Name=Your Service
Host=yourdomain.example.com
Path=/
Internal Path=/
Stripe Path=False
Conatiner Port=The Intenral Port of the Service
HTTPS=True
Certificate Provider=Let's Encrypt
```

## Dokploy Deployment

It is highly recommended to include `pull_policy: always` for each service in your `compose.yml` file. This ensures that Dokploy always pulls the latest image from the registry when deploying or updating your application, preventing issues with outdated images.

The `compose.yml` for this example already includes `pull_policy: always` for the `open-webui` service.

```yaml
services:
  open-webui:
    image: your_image_here
    pull_policy: always
    # ... other configurations
