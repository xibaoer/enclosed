# Self-Host Configuration

Configuring your self-hosted instance of Enclosed allows you to customize the application to better suit your environment and requirements. This guide covers the key environment variables you can set to control various aspects of the application, including port settings, security options, and storage configurations.

## Environment Variables

Enclosed is configured primarily through environment variables. Below is a list of the available variables, along with their descriptions and default values.

| Environment Variable | Description | Default Value |
| -------------------- | ----------- | ------------- |
| `PORT` | The port to listen on when using node server | `8787` |
| `SERVER_API_ROUTES_TIMEOUT_MS` | The maximum time in milliseconds for a route to complete before timing out | `5000` |
| `SERVER_CORS_ORIGINS` | The CORS origin for the api server | _No default value_ |
| `NOTES_MAX_ENCRYPTED_PAYLOAD_LENGTH` | The maximum length of the encrypted content of a note allowed by the api | `5242880` |
| `TASK_DELETE_EXPIRED_NOTES_ENABLED` | Whether to enable a periodic task to delete expired notes (not available for cloudflare) | `true` |
| `TASK_DELETE_EXPIRED_NOTES_CRON` | The frequency with which to run the task to delete expired notes (cron syntax) | `0 * * * *` |
| `TASK_DELETE_EXPIRED_NOTES_RUN_ON_STARTUP` | Whether the task to delete expired notes should run on startup | `true` |
| `STORAGE_DRIVER_FS_LITE_PATH` | (only in node env) The path to the directory where the data will be stored | `./.data` |
| `STORAGE_DRIVER_CLOUDFLARE_KV_BINDING` | (only in cloudflare env) The name of the Cloudflare KV binding to use | `notes` |

## Applying Configuration Changes

To apply your configuration changes, ensure that you have exported the environment variables in your shell or included them in your environment configuration file. Then, restart your Enclosed instance to apply the changes.

For Docker deployments, you can pass the environment variables directly when running the container:

```bash
docker run \
    -d --name enclosed \
    --restart unless-stopped \
    -p 8787:8787 \
    -v /path/to/local/data:/app/.data \
    -e SERVER_CORS_ORIGINS="https://example.com" \
    ghcr.io/corentin-th/enclosed
```

## Next Steps

Once your instance is configured, you can proceed to explore advanced deployment options or set up monitoring to ensure your Enclosed instance runs smoothly. For a more complex setup, consider using [Docker Compose](./docker-compose) or deploying on a cloud provider.