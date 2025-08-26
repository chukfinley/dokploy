# Dokploy Docker Compose Files

This repository contains a collection of Docker Compose files designed for use with Dokploy. Each subdirectory within the `compose/` directory represents a different application, complete with its `compose.yml` file and additional configuration files.

## Project Structure

- `compose/`: Contains subdirectories for various applications.
  - `<application_name>/`:
    - `compose.yml`: The Docker Compose file defining the services for the application.
    - `env`: This file contains key-value pairs that directly correspond to the **Environment** section when deploying with Dokploy. Each line in this file should be in the format `KEY=VALUE`.
      **Example `env` file content:**
      ```
      YOUR_SECRET_KEY=your_key_here
      DATABASE_URL=postgres://user:password@host:port/database
      ```
      When creating your own `env` file, ensure each variable is on a new line.

    - `net`: This file specifies network-related configurations for the application, corresponding to the **Network** section in Dokploy. Unlike the `env` file, this file contains specific configuration parameters for network settings, often related to ingress or proxy configurations.
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
      The exact parameters in the `net` file will depend on the specific networking requirements of the application and how Dokploy handles ingress/proxy settings.

## Creating `env` and `net` files

If an `env` or `net` file is not provided for an application, you will need to create them based on the application's requirements and your Dokploy setup.

- **For `env` files:** Refer to the application's documentation or `compose.yml` file for a list of required environment variables. Create a new file named `env` in the application's directory and add each variable as `KEY=VALUE` on a new line.
- **For `net` files:** Consult the application's networking requirements and Dokploy's documentation on network configuration. Create a new file named `net` and add the necessary network parameters.

## Dokploy Deployment Notes

When deploying these applications using Dokploy, please note the following:

### Environment Variables

The `env` file within each application's directory is crucial for setting up the necessary environment variables. Ensure that all required variables are defined in this file before deployment.

### Network Configuration

The `net` file lists the networks that your application will connect to. Dokploy uses this information to configure the networking for your deployed services.

### Image Pull Policy

It is highly recommended to include `pull_policy: always` for each service in your `compose.yml` files. This ensures that Dokploy always pulls the latest image from the registry when deploying or updating your application, preventing issues with outdated images.

**Example `compose.yml` snippet with `pull_policy: always`:**

```yaml
services:
  your-service:
    image: your-image/name:latest
    pull_policy: always
    # ... other configurations
```

By following these guidelines, you can ensure a smooth deployment process for your applications with Dokploy.
