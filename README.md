# TianGong AI MCP Local Launcher

A local runtime environment for launching and managing TianGong AI MCP (Model Context Protocol) servers using PM2.

## Prerequisites

```bash
npm install -g pm2
```

## Installation

```bash
npm install

npm update && npm ci
```

## Usage

### Start MCP Servers

```bash
# Start TianGong AI MCP server
pm2 start "npx --no-install @tiangong-ai/mcp-server-local tiangong-ai-mcp-http" \
  --name tiangong-ai-mcp-local \
  --time \
  --output ./logs/tiangong-ai-mcp-out.log \
  --error ./logs/tiangong-ai-mcp-error.log

# Start TianGong LCA MCP server
pm2 start "npx --no-install -p @tiangong-lca/mcp-server tiangong-lca-mcp-http-local" \
  --name tiangong-lca-mcp-local \
  --time \
  --output ./logs/tiangong-lca-mcp-out.log \
  --error ./logs/tiangong-lca-mcp-error.log

# Start MCP Chart Server
pm2 start "npx --no-install -p @antv/mcp-server-chart mcp-server-chart --transport streamable --port 1122 --host 0.0.0.0" \
  --name mcp-server-chart-remote \
  --time \
  --output ./logs/mcp-server-chart-remote-out.log \
  --error ./logs/mcp-server-chart-remote-error.log

# Start VIS Server
pm2 start "npx --no-install @tiangong-ai/vis-server tiangong-ai-vis-private" \
  --name tiangong-ai-vis-server \
  --time \
  --output ./logs/tiangong-ai-vis-server-out.log \
  --error ./logs/tiangong-ai-vis-server-error.log

# Start MCP Chart Server
pm2 start "npx --no-install -p @antv/mcp-server-chart mcp-server-chart --transport streamable --port 1123 --host 0.0.0.0" \
  --name mcp-server-chart-local \
  --time \
  --env VIS_REQUEST_SERVER=http://localhost:3000 \
  --output ./logs/mcp-server-chart-local-out.log \
  --error ./logs/mcp-server-chart-local-error.log
```
### View Status

```bash
pm2 status
``` 

### View Logs

```bash
pm2 logs tiangong-ai-mcp-local
pm2 logs tiangong-lca-mcp-local
```

### Stop Servers

```bash
pm2 delete tiangong-ai-mcp-local
pm2 delete tiangong-lca-mcp-local
```

### MinIO Server
To start a MinIO server for local storage, use the following command:

```bash
docker run -d \
  --name minio \
  -p 9000:9000 \
  -p 9001:9001 \
  -e "MINIO_ROOT_USER=minioadmin" \
  -e "MINIO_ROOT_PASSWORD=yourpassword" \
  quay.io/minio/minio server /data --console-address ":9001"
``` 

### Default Credentials
- Access Key
  - MINIO_ROOT_USER: minioadmin
- Secret Key
  - MINIO_ROOT_PASSWORD: minioadmin
