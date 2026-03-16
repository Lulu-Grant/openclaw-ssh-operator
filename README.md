# OpenClaw SSH Operator

A reusable **OpenClaw skill** for authorized SSH diagnostics and remote operations.

It is designed for people who regularly ask OpenClaw to:
- connect to servers via SSH
- inspect logs and service health
- diagnose production or staging issues
- perform normal remote admin actions
- handle write operations with clearer action tiers

This project exists to make SSH-based workflows more reliable and less likely to be derailed by vague tool recall or overly cautious model behavior.

---

## Why this exists

In real OpenClaw usage, SSH-heavy workflows can become unstable for two reasons:

1. the agent may not reliably recall the right skill/tool path
2. the model may become overly cautious and avoid normal, explicitly authorized operator tasks

This skill is an attempt to create a stronger, more reusable SSH operator entry point for trusted infrastructure work.

---

## What it does

OpenClaw SSH Operator provides a structured SSH operations skill with:

- **Readonly mode** for diagnostics and inspection
- **Write mode** for normal operational changes
- **Dangerous mode** for destructive or high-impact actions
- **Host aliases** so users can say things like:
  - `go check prod-main`
  - `inspect wp-server logs`
  - `restart nginx on docker-node`

---

## Features

- Unified SSH operations skill for OpenClaw
- Explicit support for authorized infrastructure workflows
- Read / write / dangerous action tiers
- Editable host alias config via `hosts.json`
- Reusable template for personal or team setups
- Friendly starting point for building more opinionated SSH/admin skills

---

## Project structure

```text
openclaw-ssh-operator/
├── SKILL.md
├── README.md
├── README.local.md
├── hosts.example.json
├── hosts.json
└── LICENSE
```

### File guide

- `SKILL.md` — main OpenClaw skill definition
- `hosts.example.json` — example alias configuration
- `hosts.json` — editable alias configuration for real use
- `README.local.md` — quick local customization notes
- `LICENSE` — MIT

---

## Host aliases

This project includes a simple alias system so users do not need to repeat host/IP/user/port every time.

Example `hosts.json`:

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

Example prompts:
- `go check prod-main`
- `ssh into hk-web`
- `inspect wp-server logs`
- `restart nginx on docker-node`

---

## Action tiers

### 1. Readonly
For diagnostics and safe inspection:
- logs
- service status
- disk / CPU / memory / networking
- config reads
- docker / pm2 / nginx / mysql / redis inspection

### 2. Write
For normal operational changes:
- restart / reload services
- git pull / deploy updates
- config edits
- cache cleanup
- chmod / chown / directory fixes

### 3. Dangerous
For destructive or high-impact changes:
- recursive deletion
- dropping databases
- overwriting critical config
- changing SSH / firewall / system identity
- other irreversible actions

Dangerous actions should require explicit confirmation.

---

## Installation

You can use this project as a standalone template or copy it into an OpenClaw skills directory.

Typical pattern:

1. clone the repo
2. edit `hosts.json`
3. copy or link the skill into your OpenClaw `skills/` directory
4. adapt `SKILL.md` to your own environment if needed

---

## Intended usage style

This skill is designed for **trusted, explicitly authorized infrastructure**.

It is not meant to normalize untrusted or unauthorized access. Instead, it is meant to make legitimate operator workflows more stable inside OpenClaw.

The main idea is:
- if the user is operating their own infrastructure
- and explicitly authorizes the action
- the agent should prefer execution over generic refusal

---

## Customization ideas

You can easily extend this into:
- a personal production-ops skill
- a WordPress server operator skill
- a Docker/K8s troubleshooting skill
- a team-specific SSH admin template

You can also add:
- environment tags
- service presets
- standard diagnosis workflows
- confirmation templates for dangerous actions

---

## Roadmap ideas

Possible future improvements:
- richer alias metadata
- predefined service check recipes
- host groups and environment grouping
- more structured write/dangerous confirmation flows
- installation helper for OpenClaw users

---

## License

MIT
