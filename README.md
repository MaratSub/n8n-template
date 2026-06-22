### Telegram SMM Automation Bot

#### How to run

1. **Add XRAY config**  
   Copy your VLESS/Reality configuration into the file:  
   `xray_config.json`

2. **Add n8n credentials**  
   Place all your credentials (Telegram bot tokens, API keys, etc.) into:  
   `n8n-backups/credentials.json`

3. **Run the system**

```bash
cd ~/n8n
docker compose down
docker compose up -d --build
```

---

### Project Structure

- `docker-compose.yml` — Main services (n8n, xray, nginx)
- `nginx.conf` — Reverse proxy configuration
- `xray_config.json` — Proxy outbound settings (VLESS + Reality)
- `n8n-backups/credentials.json` — All API credentials
- `n8n_data/` — Persistent storage for n8n workflows and settings

---

### Useful Commands

```bash
# Check running containers
docker ps

# View logs
docker logs n8n-n8n-1 --tail 50
docker logs nginx_proxy --tail 50
docker logs xray --tail 30

# Check proxy IP from inside n8n
docker exec -it n8n-n8n-1 wget -q -O - ifconfig.me

# Restart all services
docker compose restart

# Full rebuild
docker compose up -d --build
```

---

### Main Components

- **n8n** — Core automation engine
- **Xray** — Outbound proxy (to bypass restrictions)
- **Nginx** — Web server and reverse proxy
- **Telegram** — Bot automation via HTTP Request polling
