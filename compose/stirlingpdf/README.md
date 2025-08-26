# Stirling-PDF

This directory contains the Docker Compose setup for Stirling-PDF, a powerful local PDF manipulation tool.

## Files

- `compose.yml`: Defines the Stirling-PDF service and its volumes.
- `env`: Contains additional environment variables for Stirling-PDF configuration (if any).
- `net`: Specifies network-related configurations for accessing the Stirling-PDF web interface.

## Configuration

### Environment Variables (`env` file)

The `env` file in this directory is intended for additional environment variables. In this setup, no specific environment variables are defined in the `env` file. All necessary environment variables are directly set within the `compose.yml` file:

- `DOCKER_ENABLE_SECURITY`: Set to `false` in the `compose.yml` for this setup.
- `LANGS`: Specifies the OCR languages to be used (e.g., `en_GB`).

### Network Configuration (`net` file)

The `net` file provides specific network configuration parameters for accessing the Stirling-PDF service. The following parameters are used:

- `Service Name`: `stirlingpdf`
- `Host`: The domain name for accessing the Stirling-PDF instance (e.g., `pdf.example.com`).
- `Path`: The URL path for the service.
- `Internal Path`: The internal path within the container.
- `Stripe Path`: Boolean indicating if the path should be stripped.
- `Conatiner Port`: The internal port of the service within the container (default: `8080`).
- `HTTPS`: Boolean indicating if HTTPS is enabled.
- `Certificate Provider`: The certificate provider (e.g., Let's Encrypt).

**Example `net` file content:**
```
Service Name=stirlingpdf
Host=pdf.example.com
Path=/
Internal Path=/
Stripe Path=False
Conatiner Port=8080
HTTPS=True
Certificate Provider=Let's Encrypt
```

### Volumes

The `compose.yml` defines several volumes for Stirling-PDF, including:

- `stirling_pdf_trainingdata`: Required for extra OCR languages.
- `stirling_pdf_extraconfigs`: For additional configuration files.
- `stirling_pdf_customfiles`: For custom files.
- `stirling_pdf_logs`: For application logs.
- `stirling_pdf_pipeline`: For pipeline data.

## Dokploy Deployment

It is highly recommended to include `pull_policy: always` for each service in your `compose.yml` file. This ensures that Dokploy always pulls the latest image from the registry when deploying or updating your application, preventing issues with outdated images.

The `compose.yml` for Stirling-PDF already includes `pull_policy: always`.

```yaml
services:
  stirling-pdf:
    image: docker.stirlingpdf.com/stirlingtools/stirling-pdf:latest
    pull_policy: always
    # ... other configurations
