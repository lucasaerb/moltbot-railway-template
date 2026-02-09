# Railway CLI Documentation

## Overview

The Railway Command Line Interface (CLI) lets you interact with your Railway projects from the command line.

## Installation Methods

### Homebrew (macOS)
```bash
brew install railway
```

### npm (macOS, Linux, Windows)
```bash
npm i -g @railway/cli
```
Requires Node.js 16 or higher.

### Shell Script
```bash
bash <(curl -fsSL cli.new)
```
On Windows, requires Windows Subsystem for Linux with Bash.

### Scoop (Windows)
```ps1
scoop install railway
```

### Additional Options
Pre-built binaries are available via the GitHub repository, and source builds are supported.

## Authentication

### Initial Login
```bash
railway login
```

For environments without browser access:
```bash
railway login --browserless
```

### Token-Based Authentication
For CI/CD pipelines, use environment variables:
- `RAILWAY_TOKEN` for project-level operations
- `RAILWAY_API_TOKEN` for account/workspace operations

```bash
RAILWAY_TOKEN=xxx railway up
```

## Command Categories

### Authentication Commands
- `railway login` — Access your account
- `railway logout` — Sign out
- `railway whoami` — Verify current user

### Project Management
- `railway init` — Create new projects
- `railway link` — Connect to existing projects
- `railway list` — View all projects
- `railway status` — Display project information
- `railway open` — Launch in browser

### Deployment Operations
- `railway up` — Deploy from current directory
- `railway up --detach` — Deploy without log streaming
- `railway deploy --template postgres` — Use templates
- `railway redeploy` — Relaunch latest version
- `railway restart` — Reboot services
- `railway down` — Remove active deployment

### Service Management
- `railway add` — Add services interactively
- `railway add --database postgres` — Add databases
- `railway add --repo user/repo` — Deploy GitHub repositories
- `railway service` — Connect services
- `railway scale` — Adjust service capacity
- `railway delete` — Remove projects

### Variable Management
```bash
railway variable list
railway variable set KEY=value
railway variable delete KEY
```

### Environment Operations
```bash
railway environment
railway environment new staging
railway environment delete dev
```

### Local Development
- `railway run npm start` — Execute commands with environment variables
- `railway shell` — Interactive shell with loaded variables
- `railway dev` — Run services locally via Docker

### Logs & Debugging
- `railway logs` — Stream deployment logs
- `railway logs --build` — View build-specific logs
- `railway logs -n 100` — Retrieve specific line counts
- `railway ssh` — Access service containers
- `railway connect` — Open database shells

### Networking
```bash
railway domain
railway domain example.com
```

### Volume Management
```bash
railway volume list
railway volume add
railway volume delete
```

### Functions
```bash
railway functions list
railway functions new
railway functions push
```

### Utilities
- `railway completion bash` — Generate shell completions
- `railway docs` — Access documentation
- `railway upgrade` — Update CLI version

## Global Options

| Flag | Purpose |
|------|---------|
| `-s, --service` | Specify target service |
| `-e, --environment` | Specify target environment |
| `--json` | Format output as JSON |
| `-y, --yes` | Bypass confirmation dialogs |
| `-h, --help` | Show help text |
| `-V, --version` | Display version info |

## SSH Access

Launch interactive sessions in deployed services:
```bash
railway ssh
```

## OpenClaw Railway Deployment Notes

### Project Details
- **URL**: moltbot-railway-template-production-9705.up.railway.app
- **GitHub Repo**: lucasaerb/moltbot-railway-template
- **Data Volume**: /data (persists configs and skills)

### Key Environment Variables
- `SETUP_PASSWORD` — Password for /setup web UI
- `OPENCLAW_GATEWAY_TOKEN` — Gateway auth token (auto-generated if not set)
- `OPENCLAW_STATE_DIR` — State directory (default: /data/.openclaw)
- `OPENCLAW_WORKSPACE_DIR` — Workspace directory (default: /data/.openclaw/workspace)
- `PORT` — HTTP port (Railway sets to 8080)

### Useful Commands for This Project
```bash
# Link to the project
railway link

# Check deployment status
railway status

# View logs
railway logs

# Redeploy with latest changes
railway redeploy

# SSH into the container
railway ssh

# View/set environment variables
railway variable list
railway variable set KEY=value
```

### Volume Configuration
The /data volume persists:
- OpenClaw configuration (`/data/.openclaw/openclaw.json`)
- Gateway tokens (`/data/.openclaw/gateway.token`)
- Workspace files (`/data/.openclaw/workspace/`)
- Skills and plugins
