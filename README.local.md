# Local configuration

Edit `hosts.json` to define your own host aliases.

Fields:
- `host`: IP or domain
- `port`: SSH port, usually 22
- `user`: SSH user
- `auth`: `ssh-key`, `password`, or `agent`
- `description`: free-form note

Examples:
- go check prod-main
- ssh into hk-web
- inspect wp-server logs
- restart nginx on docker-node

Recommended naming:
- `prod-main`
- `staging`
- `hk-web`
- `wp-server`
- `db01`
- `docker-node`
