# OpenCode DevContainer

A secure development container for [OpenCode](https://github.com/sst/opencode) with network isolation via iptables firewall.

Based on [Claude Code's devcontainer](https://github.com/anthropics/claude-code/tree/main/.devcontainer).

## Features

- **OpenCode pre-installed** via `go install`
- **Network isolation** - Only whitelisted domains are accessible
- **Zsh with Powerlevel10k** - Beautiful terminal with git integration
- **Git Delta** - Syntax highlighting for git diffs
- **Persistent history** - Command history survives container rebuilds

## Allowed Domains

The firewall allows access to:

| Category | Domains |
|----------|---------|
| GitHub | Dynamic IP ranges from GitHub API |
| NPM | registry.npmjs.org |
| AI APIs | api.anthropic.com, api.openai.com, generativelanguage.googleapis.com, aistudio.google.com |
| GitHub Copilot | copilot.github.com, api.githubcopilot.com, copilot-proxy.githubusercontent.com, copilot-telemetry.githubusercontent.com |
| VS Code | marketplace.visualstudio.com, vscode.blob.core.windows.net, update.code.visualstudio.com |
| Go Modules | proxy.golang.org, sum.golang.org, storage.googleapis.com |
| Telemetry | sentry.io, statsig.anthropic.com, statsig.com |

## Usage

### Option 1: Copy to your project

Copy the `.devcontainer` folder to your project root:

```bash
cp -r .devcontainer /path/to/your/project/
```

### Option 2: Use as a template

1. Clone this repository
2. Open in VS Code
3. Click "Reopen in Container" when prompted

### Option 3: Use with Dev Container CLI

```bash
devcontainer up --workspace-folder .
devcontainer exec --workspace-folder . opencode
```

## Configuration

### Environment Variables

| Variable | Description | Default |
|----------|-------------|---------|
| `TZ` | Timezone | America/Los_Angeles |
| `OPENCODE_VERSION` | OpenCode version to install | latest |
| `OPENCODE_CONFIG_DIR` | OpenCode config directory | /home/node/.opencode |

### Customizing Allowed Domains

Edit `init-firewall.sh` to add or remove domains from the whitelist.

## VS Code Extensions

The following extensions are pre-installed:

- ESLint
- Prettier
- GitLens
- Go

## Requirements

- Docker
- VS Code with Dev Containers extension (or Dev Container CLI)

## Troubleshooting

### Firewall blocks a required domain

Add the domain to the whitelist in `init-firewall.sh`:

```bash
for domain in \
    "your-domain.com" \
    # ... existing domains
```

### Container fails to start

Check if the firewall script has execute permissions:

```bash
chmod +x .devcontainer/init-firewall.sh
```

### OpenCode not found

Ensure Go is properly installed and `$GOPATH/bin` is in your PATH:

```bash
export PATH=$PATH:/home/node/go/bin
```

## License

MIT
