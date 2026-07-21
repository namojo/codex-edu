# Workshop Environment Setup Guide

Complete this setup **before** the workshop. The goal: when the session starts, your machine is ready to run all exercises without interruption.

---

## Installation Flow

```
1. OS Update
   └─ Windows: winget upgrade --all
   └─ macOS:   brew update && brew upgrade
   └─ Linux:   apt update && apt upgrade

2. Base Tools
   └─ Windows: PowerShell 7+, Windows Terminal, Git (+ Git Bash)
   └─ macOS / Linux: curl, git

3. Runtimes
   └─ bun  (primary runtime & package manager)
   └─ python3
   └─ uv   (Python package manager)

4. CLI Tools
   └─ gh  (GitHub CLI)
   └─ codex  (Codex CLI)

5. Desktop Apps
   └─ Google Chrome
   └─ Mark  (Markdown viewer)

6. Login & Verify ✅
   └─ codex login  (ChatGPT account)
   └─ bun setup/setup-common.ts
```

---

## Before You Start — Opening a Terminal

Every command in this guide is typed into a **terminal** — the window where you tell your computer what to do with text instead of mouse clicks. **Copy each command, paste it into the terminal, and press Enter** to run it.

**Windows — open PowerShell as Administrator**

1. Click the **Start button** (⊞) at the bottom-left of the screen.
2. Type `PowerShell`.
3. **Right-click** on **Windows PowerShell** (or **PowerShell 7**) in the results.
4. Click **"Run as administrator"**.
5. If a **"Do you want to allow this app to make changes to your device?"** prompt appears, click **"Yes"**.

> All setup commands and the `codex` command in this course are run in this **PowerShell window**.

**macOS — open Terminal**

1. Press **⌘(Command) + Space** to open Spotlight search.
2. Type `Terminal` and press Enter.
3. Paste commands into the Terminal window and press Enter. Commands that need elevated rights will tell you to prefix them with `sudo`.

---

## Three Ways to Use Codex

Codex runs in several places. **This course's exercises use ① the Codex CLI.** Where a document says "open in the app," you can also use method ②.

| Method | Where | When to use it |
|--------|-------|----------------|
| **① Codex CLI** (course default) | `codex` command in a terminal | Build code and run commands directly inside a project folder that has your files |
| **② Codex in the ChatGPT web/desktop app** | Browser at [chatgpt.com/codex](https://chatgpt.com/codex) | Try Codex in the browser with no install, or do an "open in the app" exercise |
| **③ IDE extension** | Inside an editor like VS Code | Work with Codex while viewing your code in your usual editor |

> All three sign in with the same ChatGPT account. This guide covers installing and logging in to method ① (the CLI).

---

## Step 1 — Complete the Checklist

Before running any script, read and complete [`SETUP_CHECKLIST.md`](SETUP_CHECKLIST.md).

Key items:
- Have a **ChatGPT plan with Codex access** (Plus / Pro / Team — a subscription, not an API key)
- Create a **GitHub account** and be ready to run `gh auth login`
- Ensure you have **5 GB** free disk space and **admin/sudo** rights

---

## Step 2 — Run the OS Script

Open a terminal with administrator / sudo privileges and run the script for your OS.

### macOS

```bash
bash setup-mac.sh
# Optional: install WezTerm (GPU-accelerated terminal)
bash setup-mac.sh --wezterm
# Optional: install Docker Desktop
bash setup-mac.sh --docker
# Both optional tools:
bash setup-mac.sh --wezterm --docker
```

### Linux (Ubuntu / Debian)

```bash
bash setup-linux.sh
# Optional: install WezTerm
bash setup-linux.sh --wezterm
# Optional: install Docker
bash setup-linux.sh --docker
# Both optional tools:
bash setup-linux.sh --wezterm --docker
```

### Windows

Open **PowerShell as Administrator** and run:

```powershell
# Run setup (Execution Policy is auto-configured by the script)
.\setup-windows.ps1

# Options:
.\setup-windows.ps1 -WSL2      # also install WSL2 (requires restart)
.\setup-windows.ps1 -WezTerm   # also install WezTerm
.\setup-windows.ps1 -Docker    # also install Docker Desktop
.\setup-windows.ps1 -Force      # reinstall all tools even if already installed
.\setup-windows.ps1 -WSL2 -WezTerm -Docker  # all optional tools
```

> **After running**: close and reopen the terminal so PATH changes take effect.

> **Details for Windows users**
> - The Codex CLI is both **installed and run in the PowerShell window** you opened above.
> - Installing the Codex CLI with `npm install -g @openai/codex` requires **Node.js** (npm) or **bun** to be present first. The `setup-windows.ps1` script installs bun and the tools it needs automatically, so **if you run the script you don't have to worry about this step.** To confirm they are installed, check that these print a version:
>   ```powershell
>   bun --version
>   node --version
>   ```
>   If either prints a version, you're ready. If neither does, run `setup-windows.ps1` first.
> - Right after installing, the `codex` command may not be recognized yet, because the terminal doesn't know the location (PATH) of the newly installed program. **Close the PowerShell window and open a new one** and `codex` will be recognized.

---

## Step 3 — Log in to Codex

Before using the Codex CLI for the first time, log in with your ChatGPT account. Type this command in the terminal:

```bash
codex login
```

Here is what happens next:

1. Running the command **opens a web browser automatically.**
2. **Log in with your ChatGPT account** in the browser (it must be a Codex-capable Plus / Pro / Team plan).
3. When login finishes, the browser shows a success message. **Return to the terminal** — you are now logged in.

Confirm the login succeeded:

```bash
codex login status
```

> **If the browser does not open automatically (e.g., on a work computer)**: the terminal also prints a **login URL**. Copy that URL, paste it into your browser's address bar, log in, then return to the terminal and check with `codex login status`.

---

## Step 4 — Verify Installation

Run from the repository root (the verification script lives in the `setup/` folder):

```bash
bun setup/setup-common.ts
```

This prints a verification table of all installed tools. **All rows must show ✅ before the workshop.**

---

## Installed Tools Summary

| Tool | Purpose | macOS | Linux | Windows |
|------|---------|-------|-------|---------|
| **bun** | Runtime & package manager | `bun.sh/install` | `bun.sh/install` | `bun.sh/install.ps1` |
| **git** | Version control | `brew install git` | `apt install git` | `winget Git.Git` |
| **gh** | GitHub CLI | `brew install gh` | apt (official repo) | `winget GitHub.cli` |
| **python3** | Python runtime | `brew install python3` | `apt install python3` | `winget Python.Python.3.13` |
| **uv** | Python package manager | `brew install uv` | `astral.sh/uv/install.sh` | `winget astral-sh.uv` |
| **codex** | Codex CLI | `bun install -g @openai/codex` (or `brew install codex`) | `bun install -g @openai/codex` | `bun install -g @openai/codex` |
| **Google Chrome** | Browser | `brew install --cask google-chrome` | `.deb` direct download | `winget Google.Chrome` |
| **Mark** | Markdown viewer | ⚠️ manual | ⚠️ manual | ⚠️ manual |
| **PowerShell 7+** | Shell | — | — | `winget Microsoft.PowerShell` |
| **Windows Terminal** | Terminal | — | — | `winget Microsoft.WindowsTerminal` |
| **unzip** | Archive tool | — (built-in) | `apt install unzip` | — (built-in) |
| **curl** | HTTP client | — (built-in) | `apt install curl` | — (built-in) |

> ⚠️ items require manual download and install.
> If `bun install -g @openai/codex` fails, the scripts automatically fall back to `npm install -g @openai/codex`.

### Optional tools (`--wezterm`, `--docker`)

| Tool | macOS | Linux | Windows |
|------|-------|-------|---------|
| **WezTerm** (`--wezterm`) | `brew install --cask wezterm` | apt (fury.io repo) | `winget wez.wezterm` |
| **Docker** (`--docker`) | `brew install --cask docker` | `get.docker.com` script | `winget Docker.DockerDesktop` |
| **WSL2** (`-WSL2`, Windows only) | — | — | `wsl --install` |

---

## Terminal App Recommendation (Windows)

| App | Description | Install |
|-----|-------------|---------|
| **Windows Terminal** ⭐ | Microsoft official, tabbed, WSL-integrated — recommended default | `winget install Microsoft.WindowsTerminal` |
| **WezTerm** | GPU-accelerated, multiplexer built-in, cross-platform — power user upgrade | `winget install wez.wezterm` |

Use `.\setup-windows.ps1 -WezTerm` to install WezTerm automatically.

---

## Troubleshooting

**`bun: command not found` after install**
Restart your terminal. On Windows, bun is automatically registered in the User PATH. macOS/Linux:
```bash
export PATH="$HOME/.bun/bin:$PATH"
```

**`codex: command not found` after `bun install -g`**
This is almost always a PATH issue. **Close the terminal (PowerShell) and open a new one** — the terminal re-reads the location of the program you just installed. If it still fails, check `bun pm ls -g` and add the bin dir to PATH. On macOS you can also install via Homebrew:
```bash
brew install codex
```

**`npm: command not found` (Codex CLI won't install)**
Node.js (npm) or bun isn't installed yet. The setup script installs these for you, so **run your OS's setup script first** (Windows: `.\setup-windows.ps1`, macOS: `bash setup-mac.sh`, Linux: `bash setup-linux.sh`). Then open a new terminal and confirm with `bun --version`.

**A plan message appears when logging in**
`codex` requires a **Codex-capable ChatGPT plan (Plus / Pro / Team)**. If you can log in but hit a usage-limit notice during exercises, confirm you are on one of these plans. An API key is not required for the exercises — signing in with your ChatGPT account (`codex login`) is enough.

**`codex login` does not complete**
The login opens a browser window for ChatGPT authentication. Make sure a browser is available, complete the sign-in, then check again with `codex login status`. A ChatGPT plan with Codex access (Plus / Pro / Team) is required.

**Windows: `execution of scripts is disabled`**
The script auto-configures `RemoteSigned`. To set manually:
```powershell
Set-ExecutionPolicy RemoteSigned -Scope CurrentUser
```

**Windows: running without admin privileges**
The script warns but continues. Some installs (winget, WSL2) may fail. Recommended: re-run PowerShell as Administrator.

**Installation logs**
Windows setup logs are automatically saved to `%USERPROFILE%\workshop-setup-logs\`.

---

> Run `bun setup/setup-common.ts` from the repository root as a final check. If all rows show ✅ you're ready for the workshop.
