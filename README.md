# <img src="./pingmon.png" alt="Pingmon Logo" />

# Pingmon

Pingmon is a lightweight, self-hosted, AI-powered Linux monitoring tool that lets you observe logs and server health in real time, and analyze them with your choice of LLM (OpenAI, Anthropic, local models, etc.).

## Key Features

- Runs a root-level agent to tail logs and gather metrics (safely)
- Sends data to a Node.js backend (Express) in minimal, secure batches
- Displays logs and system health in a clean React-based dashboard
- Users prompt an AI assistant to understand logs, diagnose problems, and get suggestions
- 100% self-hosted and privacy-respecting — your API keys never leave your machine

## Features

- Live log viewer by source (e.g., nginx, system, pm2, docker)
- AI assistant to explain logs, summarize crashes, and recommend actions
- Supports any LLM provider: OpenAI, Anthropic, Cohere, Ollama, etc.
- Minimal impact — no auto-fixing, no persistent logging by default
- Modular design with future support for templates, alerts, and local LLMs

## How It Works

```
[Agent (Python/Node)] → [Express Backend (Log API + AI)] → [React Dashboard]
```

### Workflow:
1. Agent tails selected logs and sends batches to backend
2. Backend buffers logs (in memory), handles AI requests
3. Users select a service block (e.g. nginx) and prompt the AI
4. Pingmon sends that context + user prompt to their chosen LLM

## Supported LLMs

Pingmon supports any provider via API key:

| Provider | Support |
|----------|---------|
| OpenAI | ✅ (GPT-3.5, 4) |
| Anthropic | ✅ (Claude) |
| Cohere | ✅ |
| Ollama | ✅ (Local) |
| Mistral API | ✅ |
| Groq | ✅ |

You choose the provider + supply your own API key (we don't store it).

## Security & Philosophy

- Agent has read-only access to logs and system info
- Backend stores logs only in memory (unless configured otherwise)
- All LLM prompts are initiated by the user — no autonomous actions
- No cloud dependency — everything runs on your machine

## Contributing

We welcome PRs, issues, and new ideas.

### How to Contribute

1. Fork this repo

2. Clone your fork:
```bash
git clone https://github.com/YOUR_USER/Pingmon.git
```

3. Make your changes in a new branch:
```bash
git checkout -b my-feature
```

4. Commit your work:
```bash
git commit -m "Add my cool feature"
```

5. Push and open a Pull Request:
```bash
git push origin my-feature
```

### Dev Notes
- Follow clean code practices
- Use clear commits and descriptive PR titles
- Stick to lightweight dependencies
- Focus on modularity and portability

## License

MIT — open source, free to use, self-host forever.

## Contact / Feedback

Want to share feedback or collaborate?
- File an issue
- Start a discussion
- Reach out via GitHub or open a PR

---

**Pingmon — Watch smarter. Act wiser.** 
