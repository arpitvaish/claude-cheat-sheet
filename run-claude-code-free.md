# 🚀 Run Claude Code for FREE in 2026 (Yes, Really)

> **You:** "Claude Code costs money 😭"
> **NVIDIA NIM:** "Hold my API key 😎"

So you want Claude Code — the AI coding assistant that basically writes better code than most juniors — but you don't want to pay Anthropic's API bills every time you ask it to refactor your spaghetti code?

Same. Let's fix that.

---

## 🤔 Wait, How Does This Even Work?

Claude Code normally talks to Anthropic's servers. This setup **intercepts those calls** and reroutes them through **NVIDIA NIM** — NVIDIA's free AI inference platform.

Think of it like call forwarding, but for AI models.

```
Claude Code → [Your Local Proxy] → NVIDIA NIM (FREE) → Back to Claude Code
```

You get:
- ✅ Full Claude Code experience
- ✅ **40 requests/minute** for free
- ✅ Actually powerful models (not watered-down ones)
- ❌ No credit card nightmares

---

## 📋 What You Need Before Starting

| Tool | Version | Why |
|------|---------|-----|
| Node.js | 18+ | Claude Code runs on it |
| Python | 3.10+ | Proxy server needs it |
| Git | Any | Cloning the repo |
| `uv` | Latest | Fast Python package manager |

> 💡 **Don't have `uv`?** Install it:
> ```bash
> # Mac/Linux
> curl -LsSf https://astral.sh/uv/install.sh | sh
>
> # Windows (PowerShell)
> powershell -c "irm https://astral.sh/uv/install.ps1 | iex"
> ```

---

## 🎯 Step 1: Get Your Free NVIDIA API Key

1. Go to **build.nvidia.com** → Settings → API Keys
2. Create a free NVIDIA Developer account (it's actually free, not "free trial" free)
3. Generate your key — it looks like `nvapi-xxxxxxxxxxxxxxxxxxxx...`

⚠️ **IMPORTANT:** Don't truncate the key when copying. It's long (~50+ chars). Copy the whole thing.

---

## 🔧 Step 2: Clone the Proxy

```bash
git clone https://github.com/Alishahryar1/free-claude-code.git
cd free-claude-code
```

---

## ⚙️ Step 3: Configure Your `.env` File

```bash
cp .env.example .env
```

Open `.env` and fill it in:

```env
NVIDIA_API_KEY=nvapi-your-key-goes-here

# Model mapping (more on these below 👇)
CLAUDE_OPUS_MODEL=nvidia/kimi-k2-thinking
CLAUDE_SONNET_MODEL=nvidia/devstral-2-123b
CLAUDE_HAIKU_MODEL=nvidia/kimi-k2.5

# Only enable for kimi-k2-thinking!
NIM_ENABLE_THINKING=true

# Bump this up for thinking models — they're slow but smart
NIM_READ_TIMEOUT=180
```

---

## 🧠 Step 4: Pick Your Models Wisely

Here's the cheat code for which model to use when:

| Claude Tier | NIM Model | Best For |
|------------|-----------|----------|
| **Opus** | `kimi-k2-thinking` | Complex refactoring, architecture decisions |
| **Sonnet** | `devstral-2-123b` | Everyday coding tasks (your daily driver) |
| **Haiku** | `kimi-k2.5` | Quick edits, multimodal stuff |

> 🏆 **devstral-2-123b** is your go-to for 90% of tasks. Fast + smart.
> **kimi-k2-thinking** is like calling in a consultant — powerful, but takes time.

---

## 🚀 Step 5: Start the Proxy

```bash
# Activate venv and start proxy
uv run uvicorn server:app --host 0.0.0.0 --port 8083
```

> 🔑 **Why port 8083?** Port 8082 conflicts with Streamlit. Save yourself the headache.

You should see something like:
```
INFO:     Uvicorn running on http://0.0.0.0:8083 (Press CTRL+C to quit)
```

---

## 💻 Step 6: Launch Claude Code

Open a **new terminal** and run:

```bash
# Mac/Linux
export ANTHROPIC_AUTH_TOKEN="ccnim"
export ANTHROPIC_BASE_URL="http://localhost:8083"
claude

# Windows (PowerShell)
$env:ANTHROPIC_AUTH_TOKEN="ccnim"
$env:ANTHROPIC_BASE_URL="http://localhost:8083"
claude
```

**That's it.** You're now running Claude Code for free. 🎉

---

## ⚡ Bonus: One-Click Launch Script

Tired of running two terminals? Create a launcher script.

**Mac/Linux** — save as `claude-free.sh`:
```bash
#!/bin/bash
# Start proxy in background if not running
if ! lsof -i :8083 > /dev/null 2>&1; then
    echo "Starting proxy..."
    cd /path/to/free-claude-code
    uv run uvicorn server:app --host 0.0.0.0 --port 8083 &
    sleep 2
fi

export ANTHROPIC_AUTH_TOKEN="ccnim"
export ANTHROPIC_BASE_URL="http://localhost:8083"
claude
```

```bash
chmod +x claude-free.sh
./claude-free.sh
```

---

## 🔥 Pro Tips to Squeeze More Out of This

**1. Make env vars permanent (so you don't retype every session)**

```bash
# Add to ~/.zshrc or ~/.bashrc
export ANTHROPIC_AUTH_TOKEN="ccnim"
export ANTHROPIC_BASE_URL="http://localhost:8083"
```

**2. Keep MCP servers lean**
More than 5-6 active MCP servers = slow performance. Only enable what you use.

**3. Match model to task**
- Debugging a quick typo? Use Haiku.
- Building a feature from scratch? Use Sonnet.
- Rearchitecting your whole app at 2am? Opus (and sleep more).

**4. Test your NVIDIA key is working**
```bash
curl https://integrate.api.nvidia.com/v1/models \
  -H "Authorization: Bearer nvapi-your-key-here"
```
Should return a list of models. If it errors → key is wrong/truncated.

---

## 🚨 Troubleshooting (aka "Why Isn't This Working")

| Error | What's Wrong | Fix |
|-------|-------------|-----|
| `403 Forbidden` | Wrong port or auth token | Verify port is 8083, token is `ccnim` |
| `401 Unauthorized` | Bad NVIDIA key | Re-copy key, don't truncate |
| `Port in use` | Something else on 8082 | Use 8083 explicitly |
| `uv not recognized` | PATH not updated | Close & reopen terminal after install |
| Thinking model errors | `NIM_ENABLE_THINKING` on wrong model | Only enable for `kimi-k2-thinking` |
| Env vars not working | Set in wrong terminal | Set vars in same terminal you run `claude` in |

---

## 📊 Free vs Paid — Is It Worth It?

| | Free (NVIDIA NIM) | Paid (Anthropic) |
|--|-------------------|-----------------|
| Cost | $0 | Pay per token |
| Rate limit | 40 req/min | Higher limits |
| Models | Powerful alternatives | Official Claude |
| Setup | 10 mins | 2 mins |
| Good for | Personal projects, learning | Production, teams |

**Verdict:** For solo devs and learners? Free is absolutely worth it.

---

## 🎯 Quick Reference Card

```
┌─────────────────────────────────────────────┐
│         CLAUDE CODE FREE CHEAT SHEET         │
├─────────────────────────────────────────────┤
│  1. Get NVIDIA key → build.nvidia.com        │
│  2. git clone free-claude-code               │
│  3. Configure .env with your key             │
│  4. uv run uvicorn server:app --port 8083    │
│  5. Set ANTHROPIC_AUTH_TOKEN=ccnim           │
│  6. Set ANTHROPIC_BASE_URL=localhost:8083    │
│  7. Run: claude                              │
├─────────────────────────────────────────────┤
│  MODELS:                                     │
│  Opus  → kimi-k2-thinking  (heavy tasks)    │
│  Sonnet→ devstral-2-123b   (daily driver)   │
│  Haiku → kimi-k2.5         (quick edits)    │
└─────────────────────────────────────────────┘
```

---

## 💬 Final Thoughts

This setup is genuinely useful. NVIDIA's free tier is surprisingly generous, and the models available through NIM are legitimately capable.

Will it replace a paid Anthropic subscription for serious production work? Probably not. But for learning, side projects, or just vibing with AI coding tools without burning through credits?

**Absolutely worth the 10-minute setup.**

---

*Found this helpful? Drop a ⭐ on the repo and share with your dev friends who are still manually writing boilerplate in 2026.*

**→ More guides:** [arpitvaish/claude-cheat-sheet](https://github.com/arpitvaish/claude-cheat-sheet)

