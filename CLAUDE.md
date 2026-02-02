# CLAUDE.md

This file provides guidance for AI assistants working with this repository.

## Repository Overview

This repository contains configuration for setting up a Model Context Protocol (MCP) filesystem server. The MCP filesystem server allows Claude and other AI assistants to securely access specified directories on your system.

## Project Structure

```
/
├── CLAUDE.md          # AI assistant guidance (this file)
├── README.md          # User-facing documentation with setup instructions
├── mcp-config.json    # MCP server configuration
└── .git/              # Git repository metadata
```

## Files Description

- **README.md**: Comprehensive documentation for users on how to set up and use the filesystem MCP server
- **mcp-config.json**: Configuration file containing MCP server settings for filesystem access
- **CLAUDE.md**: This file, providing context and guidance for AI assistants

## MCP Configuration

The `mcp-config.json` file configures a filesystem MCP server that:
- Uses the `@modelcontextprotocol/server-filesystem` package
- Grants access to `/Users/hyjseslove` directory (configurable)
- Runs via `npx` for execution without manual installation

## Development Workflow

This is a configuration repository with no build system or tests required. Changes should be:
1. Tested by validating JSON syntax
2. Verified by testing in Claude Desktop or other MCP clients
3. Documented in README.md if functionality changes

## Conventions

- Keep JSON configuration files properly formatted and valid
- Update README.md when configuration options change
- Document security considerations when modifying filesystem access paths
- Keep this file synchronized with actual project structure
