# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a workshop project for building a custom CLI agent using the Fast-Agent framework. The goal is to create an agent capable of reading/writing files, executing terminal commands, and using web search - essentially acting as a partner for software development tasks and automation.

## Running the Agent

Start the agent:
```bash
uv run agent.py
```

Override the default model:
```bash
uv run agent.py --model=<model>
```

## Package Management

This project uses `uv` as the package manager (not pip or poetry).

Install dependencies:
```bash
uv sync
```

## Architecture

### Core Components

- **agent.py**: The main entry point containing the FastAgent application definition. Defines a single agent with:
  - Custom instruction prompt with template variables (`{{serverInstructions}}`, `{{agentSkills}}`, `{{currentDate}}`)
  - MCP servers configured: `fetch` (web fetching) and `desktop-commander` (desktop automation)
  - Interactive mode for CLI interaction

### Configuration Files

- **fastagent.config.yaml**: Main configuration for:
  - Default model (currently set to `sonnet` = Anthropic Claude)
  - MCP server definitions (fetch via uvx, desktop-commander via npx)
  - Logger settings (file logging to fast-agent.log with debug level)
  - Console display options for chat, tools, and streaming
  - MCP timeline visualization settings

- **fastagent.secrets.yaml.example**: Template for API keys
  - Actual secrets should be in `fastagent.secrets.yaml` (gitignored)
  - Supports multiple providers: OpenAI, Anthropic, DeepSeek, Google, Azure, xAI, Groq, HuggingFace, OpenRouter
  - Environment variables override config file settings

- **.env**: Contains ANTHROPIC_API_KEY for Claude Code usage
  - The `.claude/settings.json` uses this via `apiKeyHelper` to source the key

### Fast-Agent Framework

Model specification format: `<provider>.<model_string>.<reasoning_effort?>`
- Examples: `anthropic.claude-3-5-sonnet-20241022`, `openai.o3-mini.low`
- Aliases available: haiku, haiku3, sonnet, sonnet35, opus, opus3, gpt-4.1, gpt-4.1-mini, o1, o1-mini, o3-mini

The framework provides:
- MCP (Model Context Protocol) server integration
- Template-based instruction system
- Interactive CLI mode
- Automatic tool/skill discovery from connected MCP servers

### MCP Servers

Currently configured:
- **fetch**: Web content fetching (via mcp-server-fetch)
- **desktop-commander**: Desktop automation capabilities

The agent automatically includes server instructions and skills in the prompt via template variables.

## Reference Resources

- [Fast-Agent llms.txt](https://fast-agent.ai/llms.txt) - Framework documentation for AI understanding
- [Claude Code system prompt](https://gist.github.com/oneryalcin/0efa1730b680f57e4eb97a40666cd54f)
- [Claude Code Built-in Tools Reference](https://www.vtrivedy.com/posts/claudecode-tools-reference)
