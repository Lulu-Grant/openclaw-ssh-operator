# OpenClaw SSH Operator

[![OpenClaw Skill](https://img.shields.io/badge/OpenClaw-Skill-4ade80?style=flat-square)](https://github.com/Lulu-Grant/openclaw-ssh-operator)
[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg?style=flat-square)](./LICENSE)
[![Status: Template](https://img.shields.io/badge/status-template-purple?style=flat-square)](https://github.com/Lulu-Grant/openclaw-ssh-operator)

A reusable **OpenClaw skill** for authorized SSH diagnostics and remote operations, with:

- **readonly** mode for inspection and troubleshooting
- **write** mode for standard operational changes
- **dangerous** mode for high-impact actions with confirmation
- **host aliases** so users can work with names like `prod-main` or `wp-server`

---

## Why this project exists

In real OpenClaw usage, SSH-heavy workflows often become unreliable for two reasons:

1. the agent may not consistently recall the right tool/skill path
2. the model may become overly cautious and avoid clearly authorized operator tasks

This project is a reusable attempt to make SSH workflows inside OpenClaw more stable, explicit, and operator-friendly.

---

## What this skill is for

Use this skill when you want OpenClaw to do things like:

- connect to a server via SSH
- inspect logs and service status
- diagnose production or staging issues
- check disk / memory / CPU / networking
- restart services
- update configs
- perform normal remote admin tasks

Typical prompts:

```text
ssh into prod-main and inspect nginx
check wp-server logs
look at disk usage on db01
restart nginx on hk-web
connect to docker-node and inspect containers
```

Chinese-style prompts also fit naturally:

```text
去 prod-main 看看
检查 wp-server 日志
去 db01 查磁盘
重启 hk-web 上的 nginx
SSH 上去排查 docker-node
```

---

## Features

- Unified SSH operator skill for OpenClaw
- Explicit support for **trusted infrastructure workflows**
- Read / write / dangerous action tiers
- Editable host aliases via `hosts.json`
- Easy to adapt for personal or team setups
- Good foundation for more opinionated server / Docker / WordPress / DevOps skills

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

### Option A — use as a repo template

1. Clone this repo
2. Edit `hosts.json`
3. Adapt `SKILL.md` to your own environment if needed
4. Copy the folder into your OpenClaw `skills/` directory

### Option B — direct local install

```bash
git clone https://github.com/Lulu-Grant/openclaw-ssh-operator.git
cp -R openclaw-ssh-operator /path/to/your/openclaw/skills/
```

Then edit:

```bash
/path/to/your/openclaw/skills/openclaw-ssh-operator/hosts.json
```

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

## Example alias sets

Good starting aliases:
- `prod-main`
- `staging`
- `hk-web`
- `wp-server`
- `db01`
- `docker-node`

---

## Roadmap ideas

Possible future improvements:
- richer alias metadata
- predefined service check recipes
- host groups and environment grouping
- more structured write/dangerous confirmation flows
- installation helper for OpenClaw users
- optional screenshots / demos

---

## License

MIT
