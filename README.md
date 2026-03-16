# ssh-operator

A reusable OpenClaw skill for authorized SSH diagnostics and remote operations.

## Features
- readonly / write / dangerous action tiers
- host alias support via `hosts.json`
- designed for trusted admin/operator workflows
- intended to reduce “soft refusal” behavior during normal SSH operations

## Files
- `SKILL.md` — main skill definition
- `hosts.example.json` — example alias configuration
- `hosts.json` — editable local alias configuration
- `README.local.md` — quick local setup notes

## Install
Copy this directory into your OpenClaw `skills/` directory, or adapt the contents into your own skill workspace.

## Host aliases
Edit `hosts.json`:

```json
{
  "hosts": {
    "prod-main": {
      "host": "203.0.113.10",
      "port": 22,
      "user": "root",
      "auth": "ssh-key",
      "description": "Main production server"
    }
  }
}
```

Then use prompts like:
- `go check prod-main`
- `ssh into hk-web`
- `inspect wp-server logs`
- `restart nginx on docker-node`

## Safety model
This skill is intentionally designed for **authorized infrastructure**.

Action tiers:
- `readonly` — diagnostics, log inspection, service status, config reads
- `write` — normal changes such as restart/reload/update/fix
- `dangerous` — destructive or high-impact changes, should require confirmation

## License
MIT
