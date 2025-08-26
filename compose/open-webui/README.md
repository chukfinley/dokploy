# Open WebUI

This directory contains the Docker Compose setup for Open WebUI, a user-friendly interface for LLMs.

## Files

- `compose.yml`: Defines the Open WebUI service.
- `env`: Contains environment variables for Open WebUI configuration.
- `net`: Specifies network-related configurations for accessing the Open WebUI.

## Configuration

### Environment Variables (`env` file)

The `env` file in this directory is used to set environment variables for the Open WebUI service. The following variables are expected:

- `WEBUI_SECRET_KEY`: A secret key for Open WebUI. **Crucial for security.**
- `OLLAMA_BASE_URL`: The base URL for the Ollama service, if you are using it (default: `http://ollama:11434`).

**Example `env` file content:**
```
webui_secret_key=your_key_here
```
Remember to replace `your_key_here` with a strong, secure key.

### Network Configuration (`net` file)

The `net` file provides specific network configuration parameters for accessing the Open WebUI service. The following parameters are used:

- `Service Name`: `open-webui`
- `Host`: The domain name for accessing the Open WebUI (e.g., `llm.example.com`).
- `Path`: The URL path for the service.
- `Internal Path`: The internal path within the container.
- `Stripe Path`: Boolean indicating if the path should be stripped.
- `Conatiner Port`: The internal port of the service within the container (default: `8080`).
- `HTTPS`: Boolean indicating if HTTPS is enabled.
- `Certificate Provider`: The certificate provider (e.g., Let's Encrypt).

**Example `net` file content:**
```
Service Name=open-webui
Host=llm.exmaple.com
Path=/
Internal Path=/
Stripe Path=False
Conatiner Port=8080
HTTPS=True
Certificate Provider=Let's Encrypt
```

## Dokploy Deployment

It is highly recommended to include `pull_policy: always` for each service in your `compose.yml` file. This ensures that Dokploy always pulls the latest image from the registry when deploying or updating your application, preventing issues with outdated images.

The `compose.yml` for Open WebUI already includes `pull_policy: always`.

```yaml
services:
  open-webui:
    image: ghcr.io/open-webui/open-webui:latest
    pull_policy: always
    # ... other configurations
