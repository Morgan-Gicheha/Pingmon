# 🧾 Product Requirements Document (PRD)

## 🧠 Product Name  
**Pingmon**

---

## 🔍 Purpose

**Pingmon** is a lightweight, autonomous AI agent that monitors the health of Linux servers. It watches for CPU, memory, and disk usage issues, analyzes logs from system and application sources (including PM2 logs), takes smart corrective action, and sends alerts — all with minimal configuration and zero external dependencies.

---

## 🎯 Goals

- ✅ Monitor core server metrics
- ✅ Analyze structured and unstructured logs
- ✅ Detect and respond to common system or app failures
- ✅ Provide configurable, autonomous self-healing
- ✅ Alert server admins via popular channels (Slack, Discord, etc.)
- ✅ Run on any Linux system with minimal resource usage
- ✅ Be easy to install, extend, and contribute to

---

## 🔩 Core Features

### 1. **System Monitoring**
- CPU load and spike detection
- Memory usage monitoring
- Disk usage per mount point
- Process health (zombie, runaway, stuck)

### 2. **Log Parsing & Intelligence**
- Watch logs from:
  - `/var/log/syslog`, `/var/log/messages`
  - `journalctl`
  - Custom app logs
  - PM2 logs (`~/.pm2/logs/*.log`)
- Detect:
  - Crashes, exceptions, OOM kills
  - Specific keywords (`error`, `segfault`, etc.)
  - Repeated or escalating patterns
- (Optional later) Use AI models for classifying log severity

### 3. **Autonomous Actions (Self-Healing)**
- Restart services (`systemctl`, `pm2`)
- Clean up space (logs, temp files)
- Kill high-resource or stuck processes
- Controlled reboot (only if critical and recurring)

### 4. **Alerting System**
- Webhook support for:
  - Slack
  - Discord
  - Telegram
  - Email (SMTP/Webhook combo)
- Custom payloads per channel
- Alert deduplication and suppression logic
- Alert payload includes:
  - Issue summary
  - Affected service/app
  - Suggested or taken action
  - Related log snippets

### 5. **Confidence-Based Decision Engine**
- Actions only taken when confidence is high (based on pattern frequency, severity, and system state)
- Confidence scores can be tuned via config
- Example:
  ```yaml
  actions:
    restart_service:
      confidence_threshold: 0.9
    alert_only:
      confidence_threshold: 0.6
  ```

---

## 🔐 Non-Functional Requirements

### Portability
- Works on all modern Linux distros (Debian, Ubuntu, CentOS, Arch)

### Performance
- Lightweight agent (<1% CPU usage idle, <50MB RAM)

### Security
- No open ports by default
- If API added: secured with tokens
- Minimal privileges (drop `root` where not needed)

### Extensibility
- Log parsers and actions are modular
- Alert channels are plug-and-play
- Configurable via `config.yaml` or ENV

---

## 🛠 Architecture Overview

```
+------------------------+
|   System Health Check  |
+------------------------+
           |
           v
+------------------------+     +------------------------+
|   Log Parser Engine    | --> | Confidence Engine      |
+------------------------+     +------------------------+
           |                            |
           v                            v
+------------------------+     +------------------------+
|  Self-Healing Actions  |     |   Alert Dispatcher     |
+------------------------+     +------------------------+
```

---

## 📦 Installation & Deployment

- Clone or install from GitHub
- Configure `config.yaml`
- Optional: install as `systemd` service
- (Future) `pip install pingmon` or `brew install pingmon`

---

## 🧪 Testing Plan

- Simulate:
  - High CPU load
  - Disk nearly full
  - Stuck process
  - Failed systemd and PM2 services
- Inject synthetic logs (errors, warnings)
- Validate:
  - Alert content
  - Action correctness
  - Confidence thresholds
  - Resource usage during monitoring

---

## 🚀 Roadmap

### Phase 1 — MVP
- [x] Monitor CPU, memory, disk
- [x] Tail logs (`syslog`, `journalctl`, PM2)
- [x] Detect errors via regex
- [x] Restart failed services
- [x] Send webhook alerts
- [x] YAML config system
- [ ] Package as systemd service

### Phase 2 — Advanced Logic
- [ ] Confidence scoring engine
- [ ] Deduplicated alerting
- [ ] Custom user actions
- [ ] Config validation

### Phase 3 — AI Intelligence
- [ ] Log severity classifier (OpenAI, LLaMA, or fine-tuned model)
- [ ] Anomaly detection in metrics
- [ ] Recommendations via local AI model

---

## 📁 Deliverables

- Agent script (`pingmon.py`)
- Config template (`config.yaml`)
- Docs:
  - Install + setup
  - Customizing alerts and actions
  - Adding new log sources
- GitHub Actions CI (lint + tests)
- Systemd service file

---

## 🧑‍💻 Contributors Guide

- Python 3.8+
- Black + Flake8 for formatting
- PRs welcome with issue references
- Label: `feature`, `bug`, `enhancement`, `docs`

---

## 📄 License

MIT — free to use, modify, distribute, and contribute to.

---

Let me know if you’d like a separate `config.yaml` schema or a real codebase starter next.
