# Cloud Storage MCP Server

A Model Context Protocol (MCP) server for Google Cloud Storage that enables interactions with Google Cloud Storage buckets and files.

## Features

- List Cloud Storage buckets in a project
- Get details of a specific bucket
- List files in a bucket
- Get details of a specific file
- Upload files to a bucket
- Download files from a bucket
- Delete files from a bucket

## Quick Start

```bash
npx -y @garrettheath4/cloudstorage-mcp
```

## Authentication

The MCP server supports two authentication methods:

1. **`GOOGLE_APPLICATION_CREDENTIALS` environment variable** (recommended)
   - Set this to the path of a service account JSON key file
   - Works with Docker, cloud environments, and local development

2. **Legacy `keys/` directory** (for backwards compatibility)
   - Place JSON key files in a `keys/` directory next to the package
   - Filename format: `keys/{project-id}.json`

Ensure the service account has appropriate permissions for Cloud Storage (e.g., `Storage Admin` or `Storage Object Viewer`).

## Environment Variables

| Variable | Required | Description |
|----------|----------|-------------|
| `GOOGLE_CLOUD_PROJECTS` | Yes | Comma-separated list of GCP project IDs. The first one is the default. |
| `GOOGLE_APPLICATION_CREDENTIALS` | No | Path to a service account JSON key file. |

## Setup

### Claude Desktop

Add the following to your `claude_desktop_config.json`:

```json
"cloudstorage-mcp": {
  "command": "npx",
  "args": ["-y", "@garrettheath4/cloudstorage-mcp"],
  "env": {
    "GOOGLE_CLOUD_PROJECTS": "my-project-id",
    "GOOGLE_APPLICATION_CREDENTIALS": "/path/to/service-account.json"
  }
}
```

### LibreChat (Docker)

1. Mount your service account key into the container:
   ```
   /app/keys/gcp-service-account.json:/path/on/host/gcp-service-account.json
   ```

2. Add the following to your `librechat.yaml`:

```yaml
mcpServers:
  google-cloud:
    command: npx
    args:
      - "-y"
      - "@garrettheath4/cloudstorage-mcp"
    customUserVars:
      GOOGLE_CLOUD_PROJECTS:
        title: "Google Cloud Project(s)"
        description: "Comma-separated list of Google Cloud Project IDs"
    env:
      GOOGLE_CLOUD_PROJECTS: "{{GOOGLE_CLOUD_PROJECTS}}"
      GOOGLE_APPLICATION_CREDENTIALS: "/app/keys/gcp-service-account.json"
```

## Available Tools

- `listBuckets`: List all Cloud Storage buckets in a project
- `getBucket`: Get details of a specific Cloud Storage bucket
- `listFiles`: List files in a Cloud Storage bucket
- `getFile`: Get details of a specific file in a Cloud Storage bucket
- `uploadFile`: Upload a file to a Cloud Storage bucket
- `downloadFile`: Download a file from a Cloud Storage bucket
- `deleteFile`: Delete a file from a Cloud Storage bucket
- `listProjects`: List all configured projects

## Example Prompts

### List Buckets

```
List all buckets in my Google Cloud project.
```

### Get Files in a Bucket

```
Show me all files in the backup-data bucket.
```

### Get File Details

```
Get details of the file reports/monthly_report.pdf in the data-analysis bucket.
```

## Development

```bash
# Install dependencies
npm install

# Build
npm run build

# Watch mode
npm run dev
```
