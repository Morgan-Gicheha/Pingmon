# 🖥️ Pingmon

**Pingmon** is an open-source, lightweight AI agent for Linux servers that monitors system health, analyzes logs, and takes autonomous action when needed. Think of it as your server's silent guardian — watching over resources, catching errors, and responding smartly.

---

## ⚡ Features

- 🔍 **System Monitoring**  
  Monitors CPU, memory, disk usage, and critical processes.

- 📄 **Log Analysis**  
  Parses and analyzes:
  - System logs (`/var/log/syslog`, `journalctl`)
  - Custom application logs
  - **PM2 logs** (Node.js apps)

- 🧠 **Autonomous Actions**  
  - Restart failed services (`systemd` and `pm2`)
  - Clean up disk space (old logs, `/tmp`)
  - Kill runaway processes
  - (Optional) Reboot on repeated critical failure

- 📢 **Alerting**  
  Sends real-time alerts via:
  - Slack
  - Discord
  - Telegram
  - Webhooks
  With severity levels and smart deduplication.

- 🛡️ **Confidence-Based Decision Engine**  
  Avoids false alarms. Acts only when confidence is high, alerts otherwise.

- 🐧 **Minimal & Framework-Free**  
  - No bulky dependencies
  - No external dashboards
  - Just pure Python (or your language of choice)

---

