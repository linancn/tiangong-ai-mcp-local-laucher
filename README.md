# TianGong Local MCP Launcher

A local runtime environment for launching and managing TianGong MCP (Model Context Protocol) servers using PM2.

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
pm2 start "npx --no-install @tiangong-ai/mcp-server-local tiangong-ai-mcp-http" --name tiangong-ai-mcp-local --time

# Start TianGong LCA MCP server
pm2 start "npx --no-install @tiangong-lca/mcp-server tiangong-lca-mcp-http-local" --name tiangong-lca-mcp-local --time
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
