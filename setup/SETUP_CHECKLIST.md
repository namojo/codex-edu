# Workshop Pre-Installation Checklist

> Complete this checklist **before** running the setup scripts.
> Items here cannot be automated — they require manual action on your part.

---

## 1. Subscription (Priority #1)

The workshop tool requires an active subscription to run during the session.

| Tool | Required Plan | Check |
|------|--------------|-------|
| **Codex CLI** (`codex`) | ChatGPT plan with Codex access (Plus / Pro / Team) | [ ] |

> ⚠️ **API Key usage**: API keys are only needed if you are running tools outside a subscription plan (e.g., custom integrations). For workshop exercises, logging in with your ChatGPT account (`codex login`) is sufficient and preferred.

---

## 2. Accounts

- [ ] **ChatGPT (OpenAI) Account** — required for `codex login` (must be on a Codex-capable plan)
- [ ] **GitHub Account** — required for `gh auth login` and PR exercises
  - Sign up at [github.com](https://github.com) if you don't have one

---

## 3. System Requirements

- [ ] OS: Windows 11 (Intel) / macOS Sequoia 15+ on Apple Silicon (M-series) / Ubuntu 24.04+
- [ ] Free disk space: **5 GB or more**
- [ ] Admin / sudo privileges on your machine
  - **Windows**: Open Start → search **"PowerShell"** → right-click → **"Run as administrator"**
    - Or: `Win + X` → **"Terminal (Admin)"** / **"Windows PowerShell (Admin)"**
    - Confirm the UAC prompt that appears
  - **macOS / Linux**: prefix commands with `sudo` when prompted
- [ ] Stable internet connection (downloads ~1–2 GB total)

---

## 4. Git Configuration

After git is installed, set your identity:

```bash
git config --global user.name  "Your Name"
git config --global user.email "you@example.com"
```

- [ ] `git config --global user.name` is set
- [ ] `git config --global user.email` is set

---

## 5. GitHub Authentication

```bash
gh auth login
```

Follow the prompts to authenticate via browser.

- [ ] `gh auth status` shows "Logged in"

---

## 6. Codex Login

After the Codex CLI is installed, log in with your ChatGPT account:

```bash
codex login
```

- [ ] `codex login status` shows you are logged in

---

## 7. Per-Exercise Python Dependencies (after cloning)

Depending on the exercise track, install these Python packages ahead of time to avoid waiting during the session.

**tool / mcp-server exercise** — dependencies for the MCP server exercise:

```bash
cd tool/mcp-server
pip3 install -r requirements.txt
```

- [ ] Ran `pip3 install -r requirements.txt` from the `tool/mcp-server/` folder

**codex-engineering Track A exercise** — pytest for running tests:

```bash
pip3 install pytest
```

- [ ] Ran `pip3 install pytest` (verify with `pytest --version`)

> **Docker** is optional. Install only if the workshop organizer asks you to.
> macOS/Linux: pass `--docker` to the setup script. Windows: pass `-Docker`.
> - [ ] *(optional)* Docker installed and daemon running

---

## 8. Quick Verification (run before the workshop)

Run the common setup script from the repository root (the script lives in the `setup/` folder):

```bash
bun setup/setup-common.ts
```

All rows in the output table should show ✅.

---

> Questions? Contact the workshop organizer before the session date.
