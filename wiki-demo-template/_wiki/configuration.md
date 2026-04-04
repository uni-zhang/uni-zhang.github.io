---
title: "Configuration"
description: "All configuration options explained"
category: "User Guide"
order: 2
last_updated: "2024-01-01"
toc: true
tags: [configuration, settings, options]
related:
  - Getting Started
  - API Reference
---

## Configuration File

The project is configured via `config.yaml` (or `config.json`). The file is located at:

- **Default:** `~/.your-tool/config.yaml`
- **Project-level:** `./config.yaml`
- **Environment variable:** `YOUR_TOOL_CONFIG=/path/to/config.yaml`

## Complete Configuration Reference

```yaml
# ==========================================
# Your Tool Configuration Reference
# ==========================================

# --- General Settings ---
name: "My Project"             # Project name (required)
version: "1.0"                 # Config schema version
debug: false                   # Enable debug logging

# --- Connection Settings ---
server:
  host: "localhost"            # Server hostname
  port: 3000                   # Port to listen on (default: 3000)
  timeout: 30                  # Request timeout in seconds

# --- Authentication ---
auth:
  enabled: true                # Enable authentication
  method: "token"              # "token", "oauth", or "none"
  token: ""                    # API token (or use env: YOUR_TOOL_TOKEN)
  
# --- Storage ---
storage:
  backend: "local"             # "local", "s3", "gcs"
  path: "./data"               # Local storage path
  
  # S3 settings (if backend: "s3")
  s3:
    bucket: ""
    region: "us-east-1"
    prefix: ""

# --- Features ---
features:
  feature_one:
    enabled: true
    option_a: "default"
  feature_two:
    enabled: false
    
# --- Logging ---
logging:
  level: "info"                # "debug", "info", "warn", "error"
  format: "text"               # "text" or "json"
  file: ""                     # Log file path (empty = stdout only)
```

## Environment Variables

All configuration options can be set via environment variables. The format is:

```
YOUR_TOOL_<SECTION>_<KEY>=value
```

| Environment Variable | Config Key | Default |
|---------------------|-----------|---------|
| `YOUR_TOOL_SERVER_PORT` | `server.port` | `3000` |
| `YOUR_TOOL_AUTH_TOKEN` | `auth.token` | `` |
| `YOUR_TOOL_DEBUG` | `debug` | `false` |
| `YOUR_TOOL_LOG_LEVEL` | `logging.level` | `info` |

## Configuration Profiles

You can maintain multiple configuration profiles:

```bash
# Use a specific profile
your-tool --profile production

# Create a new profile
your-tool config init --profile staging
```

Profiles are stored in `~/.your-tool/profiles/`.

## Secrets Management

<div class="warning">
<strong>⚠️ Never commit secrets to version control!</strong>
Use environment variables or a secrets manager for sensitive values like API tokens and passwords.
</div>

Recommended approach:

```bash
# Set token via environment variable
export YOUR_TOOL_TOKEN="your-secret-token"

# Or use a .env file (add to .gitignore)
echo "YOUR_TOOL_TOKEN=your-secret-token" >> .env
```

## Validation

Validate your configuration file:

```bash
your-tool config validate
# ✓ Configuration is valid

your-tool config validate --file custom-config.yaml
```

## Configuration Examples

### Minimal Configuration

```yaml
name: "My Project"
server:
  port: 8080
```

### Production Configuration

```yaml
name: "My Project"
debug: false
server:
  host: "0.0.0.0"
  port: 443
auth:
  enabled: true
  method: "oauth"
storage:
  backend: "s3"
  s3:
    bucket: "my-production-bucket"
    region: "us-west-2"
logging:
  level: "warn"
  format: "json"
  file: "/var/log/your-tool.log"
```
