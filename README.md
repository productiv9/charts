[![Artifact Hub](https://img.shields.io/endpoint?url=https://artifacthub.io/badge/repository/ghost)](https://artifacthub.io/packages/search?repo=ghost)

# Productiv9 Charts

This Helm chart is designed to deploy a suite of applications including Ghost (a powerful blogging platform), Litestream (for real-time SQLite replication), Rclone (for command-line cloud storage synchronization), and Cloudflared (for secure network tunnels). This configuration is tailored for high availability, secure access, and persistent storage, making it ideal for production environments.

## Prerequisites

- Kubernetes 1.19+
- Helm 3.0+
- PV provisioner support in the underlying infrastructure (for persistent storage)
- A Cloudflare account and a configured tunnel token for `cloudflared`
- A sendgrid account for sending email

## Installing the Chart

To install the chart with the release name `my-release`:

```shell
helm repo add productiv9 https://github.com/productiv9/charts
helm install my-release productiv9/ghost
```

## Configuration

The following table lists the configurable parameters of the chart and their default values.

| Parameter | Description | Default |
|-----------|-------------|---------|
| `image.ghost.tag` | The Ghost image tag | `5.79.0` |
| `image.litestream.tag` | The Litestream image tag | `0.3` |
| `image.rclone.tag` | The Rclone image tag | `latest` |
| `image.cloudflared.tag` | The Cloudflared image tag | `latest` |
| `cloudflared.token` | Cloudflare tunnel token | `YOUR_TOKEN` |
| `cloudflared.replicaCount` | Number of Cloudflared replicas | `2` |
| `r2.bucket` | The name of your R2 bucket | `YOUR_BUCKET` |
| `r2.endpoint` | R2 endpoint URL | `YOUR_ENDPOINT` |
| `r2.accessKeyId` | R2 access key ID | `YOUR_ACCESS_KEY_ID` |
| `r2.secretAccessKey` | R2 secret access key | `YOUR_SECRET_ACCESS` |
| `ghost.url` | The URL for your Ghost installation | `https://example.com` |
| `ghost.mailFrom` | Email address for sending emails from Ghost | `` |
| `ghost.sendgridApiKey` | SendGrid API key for email service | `YOUR_API_KEY` |
| `ghost.imageSyncInterval` | Interval for syncing images (in seconds) | `60` |
| `volumeClaims.ghostContent.size` | Size of the persistent volume claim for Ghost content | `5Gi` |

### Customizing the Chart Before Installing

To configure the chart with custom values:

1. Create a file named `my-values.yaml` with your changes.

For example:

```yaml
cloudflared:
  token: "<your-cloudflared-token>"
ghost:
  url: "https://yourdomain.com"
  sendgridApiKey: "<your-sendgrid-api-key>"
```

2. Install the chart with the custom values:

```shell
helm install my-release productiv9/<chart-name> -f my-values.yaml
```

### Upgrading Your Deployment

To upgrade your deployment with a new version of the chart or to change the configuration:

```shell
helm upgrade my-release productiv9/ghost -f my-values.yaml
```

## Persistence

The Ghost application is configured to use a Persistent Volume Claim (PVC) to store data. The size of the PVC is configurable through the `volumeClaims.ghostContent.size` parameter.
