# Hermes Agent for Obsidian

Hermes Agent now uses a smart-note-agent style architecture: persistent chat, vault tools, diff approval for note edits, and Hermes CLI connectivity.

## Installation

1. Copy the plugin files to your Obsidian plugins directory:
   ```
   ~/.obsidian/plugins/obsidian-hermes-agent/
   ```

2. Enable the plugin in Obsidian:
   - Open Settings
   - Go to Community Plugins
   - Browse and search for "Hermes Agent"
   - Click "Install"
   - Enable the plugin

3. Configure the plugin:
   - Settings → Community Plugins → Obsidian Plugins → Settings (gear icon)
   - Find "Hermes Agent" in the list
   - Click "Open settings"

## Configuration Options

### Connection Mode
Choose how the plugin talks to Hermes.

- `Local CLI`: Runs the local `hermes` command on your machine
- `SSH Remote CLI`: Connects to a remote machine over SSH and runs the Hermes CLI there

### Hermes Executable Path
Path to the Hermes CLI executable.

Default: `hermes`

Examples:
```
hermes
/Users/user1/.local/bin/hermes
```

### Hermes Home Path
Working directory used when running Hermes.

Default: `~/.hermes`

Example:
```
/Users/user1/.hermes
```

Configure both options in Obsidian under Settings → Community plugins → Hermes Agent.

### SSH Host
Used only in `SSH Remote CLI` mode.

This is the hostname or IP of the remote machine where Hermes is installed.

### SSH Port
Optional SSH port. Default: `22`

### SSH User
Optional SSH username. If omitted, your local SSH configuration decides which user is used.

### Remote Hermes Executable Path
Used only in `SSH Remote CLI` mode.

This is the Hermes executable on the remote machine, for example:
```text
hermes
/usr/local/bin/hermes
```

### Remote Hermes Home Directory
Used only in `SSH Remote CLI` mode.

The plugin changes into this directory on the remote machine before running Hermes.

Important:
- SSH authentication is handled by your local SSH setup, such as SSH keys or your SSH agent
- The plugin does not manage passwords or interactive SSH prompts
- The remote machine must accept non-interactive `ssh` commands from the Obsidian host

## Environment Variables

You can also set these in your shell profile (`.bashrc`, `.zshrc`, etc.):

```bash
export HERMES_HOME=~/.hermes
export HERMES_BIN=hermes
export HERMES_SSH_HOST=server.example.com
export HERMES_SSH_PORT=22
export HERMES_SSH_USER=ubuntu
export HERMES_SSH_BIN=hermes
export HERMES_SSH_HOME=~/.hermes
export OBSIDIAN_VAULT_PATH=~/Documents/Obsidian\ Vault
```

## Usage

### Command Palette

Press `Ctrl/Cmd + P` and type "Hermes" to see available commands:

- **Open Hermes Agent** - Open the persistent Hermes chat view
- **New Hermes chat** - Start a fresh conversation

### Chat Workflow

The chat behaves like a vault-aware agent:

- It can search the vault, read notes, inspect backlinks and outgoing links, and use the active note/selection as context.
- In edit mode it can propose note changes and queue them for approval, similar to smart-note-agent.
- Hermes connectivity is provided through the local CLI or an SSH remote CLI.

### Chat Interface

1. Press `Ctrl/Cmd + P` and run `Open Hermes Agent`
2. Ask questions about notes, folders, links, or editing tasks
3. Review any queued note edits before applying them
4. Start a new conversation with `New Hermes chat` when needed

## Troubleshooting

### Plugin not loading

1. Check the Obsidian console: `Ctrl/Cmd + Shift + I`
2. Look for errors related to the plugin
3. Ensure the plugin files are in the correct location

### Hermes Agent not found

1. Check if Hermes Agent is installed: `hermes doctor`
2. Verify the configured executable path and home directory
3. Check the plugin settings for the selected connection mode

### Connection errors

1. Ensure the `hermes` CLI works in the same environment as Obsidian
2. For SSH mode, verify non-interactive SSH access first
3. Confirm the configured host, user, port, executable path, and home path

### Notes not found

1. Check whether the agent should be in Ask or Edit mode
2. Use explicit note paths or folder paths when possible
3. Ask the agent to search the vault first before editing

## Notes

- This rewrite is based on the smart-note-agent interaction model, but uses Hermes as the backend connection.
- Hermes tool use inside the plugin is mediated through the chat protocol, so good Hermes prompting and CLI availability matter.

## Support

For issues or questions:
1. Check the Obsidian console for errors
2. Verify Hermes Agent installation and configuration
3. Review the plugin settings
4. Check the Hermes Agent documentation

## Resources

- [Hermes Agent Documentation](https://hermes-agent.nousresearch.com/docs/)
- [Obsidian Plugin API](https://docs.obsidian.md/Plugins/Getting+started/Build+a+plugin)
- [Obsidian Community Plugins](https://obsidian.md/plugins/)