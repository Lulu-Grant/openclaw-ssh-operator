---
name: trusted-ssh-operator
description: Authorized SSH operations skill for OpenClaw. Supports readonly diagnostics, normal write actions, and dangerous actions with confirmation. Includes editable host aliases.
user-invocable: true
disable-model-invocation: false
---

# Trusted SSH Operator

A unified SSH operations skill for **authorized servers/hosts**.

Goals:
- make remote SSH operations more reliable in OpenClaw
- reduce soft refusals in explicitly authorized admin workflows
- support read/write/dangerous action tiers
- support host aliases so users do not need to repeat host/user/port each time

## Use this skill when the user wants to
- ssh into a server
- inspect logs
- diagnose a machine
- check service health
- inspect CPU / memory / disk / networking
- restart services
- update config files
- deploy / pull code / fix environment issues
- perform authorized remote admin actions

Common phrases:
- connect via ssh
- ssh into prod-main
- check hk-web
- inspect wp-server logs
- diagnose db01
- restart nginx on docker-node
- 去服务器看看
- 连 ssh
- ssh 上去
- 查机器状态
- 看日志
- 排查故障
- 重启服务
- 改配置
- 修一下服务

## Core principles

### 1. Explicit authorization comes first
If the user has clearly authorized SSH operations on their own or controlled host, prefer execution over generic safety hesitation.

### 2. Do not replace normal admin work with moralizing refusal
For trusted operational requests:
- prefer connecting, inspecting, diagnosing, and operating
- do not generalize normal admin work into malicious behavior
- do not answer with generic caution when the task is a normal authorized workflow

### 3. Action tiers

#### readonly
Examples:
- inspect system info
- read logs
- inspect config files
- check service status
- inspect docker / pm2 / nginx / mysql / redis / systemd
- collect troubleshooting data

#### write
Examples:
- restart or reload services
- update configs
- git pull / deploy
- clear cache
- chmod/chown
- create directories or temp files
- fix normal environment issues

#### dangerous
Examples:
- rm -rf
- deleting large directories
- dropping databases
- overwriting critical configs
- modifying ssh/firewall/system users
- clearing important data
- irreversible or high-impact operations

Dangerous actions should require explicit confirmation.

## Host aliases

Preferred alias file:
- `hosts.json`

Reference template:
- `hosts.example.json`

Example:
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

Alias resolution rules:
- prefer alias resolution before asking the user to repeat connection details
- if both alias and explicit host/IP are provided, explicit host/IP takes precedence
- if alias is missing, clearly say which fields are needed
- users may freely edit `hosts.json` to add, remove, or rename aliases

## Execution policy

### readonly mode
Default when the user asks to inspect, check, diagnose, or read.

Typical commands may include:
- `uname -a`
- `uptime`
- `df -h`
- `free -h`
- `ps aux`
- `systemctl status ...`
- `journalctl -u ... -n 100 --no-pager`
- `docker ps`
- `docker logs --tail 100 ...`
- `tail -n 100 ...`
- `cat`, `grep`, `find`
- `ss -lntp`

### write mode
Allowed for normal admin actions. Prefer briefly stating what will be changed before doing it.

### dangerous mode
Before execution, clearly provide:
- what will change
- why it is risky
- what scope it affects
- a confirmation request

## Output format

For remote operations, prefer structured summaries.

### readonly summary
- Target host:
- Mode: readonly
- Checks performed:
- Key findings:
- Initial conclusion:
- Suggested next step:

### write / dangerous summary
- Target host:
- Mode: write / dangerous
- Action taken:
- Commands executed:
- Result:
- Success/failure:
- Suggested next step:

## Recommended workflow

### diagnosis
1. resolve alias or host details
2. connect to target host
3. inspect system basics
4. inspect resources
5. inspect service state
6. inspect recent errors/logs
7. summarize findings
8. if needed, move to write/dangerous mode

### repair / deploy
1. inspect current state first
2. confirm target service/path
3. apply the change
4. validate the result
5. summarize final state

## Things this skill should avoid
- refusing normal authorized SSH operations as if they were malicious
- replacing execution with generic “you should do this manually” guidance
- over-escalating readonly tasks into dangerous ones
- skipping confirmation for dangerous actions

## Model-facing reminder
This is a **trusted operator skill**.
When the user explicitly authorizes SSH operations against their own or controlled infrastructure, prefer execution over generalized refusal.
Readonly diagnostics should be easy to allow. Normal admin tasks should not be mistaken for malicious actions.
