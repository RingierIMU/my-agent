# Setup Instructions

This guide will help you set up the Fast-Agent CLI with MCP servers.

## Prerequisites

- Python 3.13+ with `uv` package manager installed
- Node.js 18.0.0+ (for desktop-commander MCP server)

## Installation Steps

### 1. Install Python Dependencies

```bash
uv sync
```

### 2. Install Desktop-Commander MCP Server

The desktop-commander MCP server requires local installation due to a dependency issue with `@vscode/ripgrep` binary downloads.

```bash
npm install --no-save @wonderwhy-er/desktop-commander --ignore-scripts
```

**Why `--ignore-scripts`?**
The desktop-commander package depends on `@vscode/ripgrep`, which attempts to download binaries during installation. This can fail due to GitHub API rate limiting (403 errors). The `--ignore-scripts` flag bypasses this issue.

### 3. Configure API Keys

Copy the example secrets file:

```bash
cp fastagent.secrets.yaml.example fastagent.secrets.yaml
```

Edit `fastagent.secrets.yaml` and add your API keys:

```yaml
anthropic:
  api_key: your-anthropic-api-key-here
```

Alternatively, you can set environment variables:
- `ANTHROPIC_API_KEY` for Anthropic Claude
- `OPENAI_API_KEY` for OpenAI models

### 4. Run the Agent

```bash
uv run agent.py
```

To use a different model:

```bash
uv run agent.py --model=<model>
```

## MCP Servers Included

After successful setup, your agent will have access to:

- **fetch**: Web content fetching capabilities
- **desktop-commander**: Desktop automation, file operations, and terminal commands

Total: **2 MCP Servers with 26 tools**

## Troubleshooting

### Desktop-Commander Connection Errors

If you see "MCP error -32000: Connection closed" for desktop-commander:

1. Ensure Node.js 18+ is installed: `node --version`
2. Reinstall with the ignore-scripts flag:
   ```bash
   npm install --no-save @wonderwhy-er/desktop-commander --ignore-scripts
   ```
3. Verify the path in `fastagent.config.yaml` points to:
   ```yaml
   desktop-commander:
     command: "node"
     args: ["node_modules/@wonderwhy-er/desktop-commander/dist/index.js"]
   ```

### API Key Issues

If you see "Provider Configuration Error":

1. Check that `fastagent.secrets.yaml` exists and contains your API key
2. Or set the environment variable: `export ANTHROPIC_API_KEY=your-key`
3. Ensure the secrets file is not in `.gitignore` before you create it (only the actual file should be gitignored, not the example)

## Resources

- [Fast-Agent Documentation](https://fast-agent.ai/llms.txt)
- [MCP Protocol Documentation](https://modelcontextprotocol.io)
