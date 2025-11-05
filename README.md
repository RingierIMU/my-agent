# my-agent

A workshop project for building a simple CLI agent using [Fast-Agent](https://fast-agent.ai/).

The objective is to build an agent which is capable of reading and writing files in the local file system, execute commands in the terminal, and use web search to gather information.

Implement the agent using the Fast-Agent framework and Claude Code's architecture as the inspiration to create a custom agent that can act as a partner for software development tasks and automation.

# installation

First install the package manager [uv](https://docs.astral.sh/uv/).

macOS and Linux:
```bash
curl -LsSf https://astral.sh/uv/install.sh | sh
```

Windows:
```powershell
powershell -ExecutionPolicy ByPass -c "irm https://astral.sh/uv/install.ps1 | iex"
```

Then sync the packages:
```bash
uv sync
```

# usage

Run the agent with:
```bash
uv run fast-agent
```

This will start the agent, which will interact with you via the command line.

# useful references

- [Claude Code system prompt - May 2025](https://gist.github.com/oneryalcin/0efa1730b680f57e4eb97a40666cd54f)
- [Claude Code Built-in Tools Reference](https://www.vtrivedy.com/posts/claudecode-tools-reference)
- [Claude system prompts](https://github.com/gregkonush/claude-system-prompts)

# useful services

- [SerpAPI](https://serpapi.com/) - for web search tool with API
- [Serper](https://serper.dev/) - another web search tool with API

# useful mcp servers

- [Desktop Commander](https://desktopcommander.app/)
- [Filesystem](https://github.com/modelcontextprotocol/servers/tree/main/src/filesystem)
- [Sequential Thinking](https://github.com/modelcontextprotocol/servers/tree/main/src/sequentialthinking)

# hints

- Bash tool - Fast-agent can execute bash commands natively, start the agent with `-x`:
```bash
uv run fast-agent -x
```
