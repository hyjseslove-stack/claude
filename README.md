# Filesystem MCP Server Configuration

This repository contains configuration for setting up a Model Context Protocol (MCP) filesystem server.

## What is MCP?

The Model Context Protocol (MCP) is an open protocol that standardizes how applications provide context to LLMs. MCP servers allow AI assistants like Claude to securely access various data sources and tools.

## Configuration

The `mcp-config.json` file contains the configuration for the filesystem MCP server, which grants access to specified directories on your system.

### Current Configuration

```json
{
  "mcpServers": {
    "filesystem": {
      "type": "stdio",
      "command": "npx",
      "args": [
        "-y",
        "@modelcontextprotocol/server-filesystem",
        "/Users/hyjseslove"
      ],
      "env": {}
    }
  }
}
```

This configuration:
- Uses the `@modelcontextprotocol/server-filesystem` package
- Grants access to `/Users/hyjseslove` directory
- Runs via `npx` for easy execution without installation

## Setup Instructions

### For Claude Desktop

1. Locate your Claude Desktop configuration file:
   - **macOS**: `~/Library/Application Support/Claude/claude_desktop_config.json`
   - **Windows**: `%APPDATA%\Claude\claude_desktop_config.json`
   - **Linux**: `~/.config/Claude/claude_desktop_config.json`

2. Add the filesystem server configuration to the `mcpServers` section:

```json
{
  "mcpServers": {
    "filesystem": {
      "type": "stdio",
      "command": "npx",
      "args": [
        "-y",
        "@modelcontextprotocol/server-filesystem",
        "/Users/hyjseslove"
      ],
      "env": {}
    }
  }
}
```

3. Restart Claude Desktop for the changes to take effect.

### Customizing the Path

To grant access to a different directory, modify the last element in the `args` array:

```json
"args": [
  "-y",
  "@modelcontextprotocol/server-filesystem",
  "/path/to/your/directory"
]
```

**Security Note**: Only grant access to directories you want Claude to be able to read and write to.

## What Can Claude Do With Filesystem Access?

Once configured, Claude can:
- Read files from the specified directory
- Write and create files in the specified directory
- List directory contents
- Navigate subdirectories within the allowed path

## Prerequisites

- Node.js and npm must be installed on your system
- The `npx` command must be available in your PATH
- Appropriate read/write permissions for the specified directory

## Testing the Configuration

After setting up, you can test by asking Claude to:
- List files in the configured directory
- Read a specific file
- Create a test file

## Security Considerations

- **Principle of Least Privilege**: Only grant access to directories that Claude needs
- **Sensitive Data**: Avoid granting access to directories containing:
  - SSH keys
  - API credentials
  - Personal documents you want to keep private
- **Multiple Servers**: You can configure multiple filesystem servers with different paths for better control

## Troubleshooting

### Server Not Starting
- Ensure Node.js and npm are installed: `node --version && npm --version`
- Check that npx is available: `npx --version`
- Verify the directory path exists and is accessible

### Permission Issues
- Ensure you have read/write permissions for the specified directory
- On macOS, you may need to grant Claude Desktop full disk access in System Preferences

### Configuration Not Loading
- Verify the JSON syntax is valid (no trailing commas, proper quotes)
- Restart Claude Desktop after making changes
- Check Claude Desktop logs for error messages

## Additional Resources

- [MCP Documentation](https://modelcontextprotocol.io/)
- [MCP Filesystem Server](https://github.com/modelcontextprotocol/servers/tree/main/src/filesystem)
- [Claude Desktop Documentation](https://support.anthropic.com/en/articles/9517075-what-is-claude-desktop)

## License

This configuration is provided as-is for use with Claude and MCP-compatible applications.
