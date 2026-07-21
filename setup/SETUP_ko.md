# 워크숍 환경 설치 가이드

워크숍 **시작 전**에 설치를 완료하세요. 목표는 세션이 시작될 때 별도의 환경 설정 없이 바로 실습에 진입할 수 있는 상태를 만드는 것입니다.

---

## 설치 흐름

```
1. OS 업데이트
   └─ Windows: winget upgrade --all
   └─ macOS:   brew update && brew upgrade
   └─ Linux:   apt update && apt upgrade

2. 기반 도구
   └─ Windows: PowerShell 7+, Windows Terminal, Git (+ Git Bash)
   └─ macOS / Linux: curl, git

3. 런타임
   └─ bun  (기본 런타임 & 패키지 매니저)
   └─ python3
   └─ uv   (Python 패키지 매니저)

4. CLI 도구
   └─ gh  (GitHub CLI)
   └─ codex  (Codex CLI)

5. 데스크탑 앱
   └─ Google Chrome
   └─ Mark  (Markdown 뷰어)

6. 로그인 & 최종 확인 ✅
   └─ codex login  (ChatGPT 계정)
   └─ bun setup/setup-common.ts
```

---

## Step 1 — 체크리스트 완료

스크립트 실행 전 [`SETUP_CHECKLIST_ko.md`](SETUP_CHECKLIST_ko.md)를 먼저 읽고 완료하세요.

주요 확인 사항:
- **Codex 사용 가능한 ChatGPT 플랜** (Plus / Pro / Team — API Key가 아닌 구독 플랜) 보유
- **GitHub 계정** 생성 및 `gh auth login` 준비
- 여유 디스크 공간 **5 GB 이상**, **관리자/sudo 권한** 보유 확인

---

## Step 2 — OS별 스크립트 실행

터미널을 관리자 / sudo 권한으로 열고 본인 OS에 맞는 스크립트를 실행하세요.

### macOS

```bash
bash setup-mac.sh
# 선택: WezTerm (GPU 가속 터미널) 함께 설치
bash setup-mac.sh --wezterm
# 선택: Docker Desktop 함께 설치
bash setup-mac.sh --docker
# 둘 다:
bash setup-mac.sh --wezterm --docker
```

### Linux (Ubuntu / Debian)

```bash
bash setup-linux.sh
# 선택: WezTerm 함께 설치
bash setup-linux.sh --wezterm
# 선택: Docker 함께 설치
bash setup-linux.sh --docker
# 둘 다:
bash setup-linux.sh --wezterm --docker
```

### Windows

**PowerShell을 관리자 권한으로 실행**한 뒤 아래 명령어를 입력하세요:

```powershell
# 기본 실행 (Execution Policy은 스크립트가 자동으로 설정합니다)
.\setup-windows.ps1

# 옵션:
.\setup-windows.ps1 -WSL2             # WSL2 함께 설치 (재시작 필요)
.\setup-windows.ps1 -WezTerm          # WezTerm 함께 설치
.\setup-windows.ps1 -Docker            # Docker Desktop 함께 설치
.\setup-windows.ps1 -Force             # 이미 설치된 도구도 모두 재설치
.\setup-windows.ps1 -WSL2 -WezTerm -Docker  # 선택 옵션 전부 설치
```

> **실행 후**: 터미널을 닫고 다시 열어 PATH 변경 사항을 반영하세요.

---

## Step 3 — Codex 로그인

ChatGPT 계정으로 로그인하세요 (브라우저 인증 창이 열립니다):

```bash
codex login
```

로그인이 완료되었는지 확인하세요:

```bash
codex login status
```

---

## Step 4 — 설치 확인

저장소 루트에서 실행하세요 (검증 스크립트는 `setup/` 폴더에 있습니다):

```bash
bun setup/setup-common.ts
```

설치된 도구의 검증 표를 출력합니다. **모든 항목이 ✅로 표시되면 준비 완료입니다.**

---

## 설치 도구 목록

| 도구 | 용도 | macOS | Linux | Windows |
|------|------|-------|-------|---------|
| **bun** | 런타임 & 패키지 매니저 | `bun.sh/install` | `bun.sh/install` | `bun.sh/install.ps1` |
| **git** | 버전 관리 | `brew install git` | `apt install git` | `winget Git.Git` |
| **gh** | GitHub CLI | `brew install gh` | apt (공식 저장소) | `winget GitHub.cli` |
| **python3** | Python 런타임 | `brew install python3` | `apt install python3` | `winget Python.Python.3.13` |
| **uv** | Python 패키지 매니저 | `brew install uv` | `astral.sh/uv/install.sh` | `winget astral-sh.uv` |
| **codex** | Codex CLI | `bun install -g @openai/codex` (또는 `brew install codex`) | `bun install -g @openai/codex` | `bun install -g @openai/codex` |
| **Google Chrome** | 브라우저 | `brew install --cask google-chrome` | `.deb` 직접 다운로드 | `winget Google.Chrome` |
| **Mark** | Markdown 뷰어 | ⚠️ 수동 설치 | ⚠️ 수동 설치 | ⚠️ 수동 설치 |
| **PowerShell 7+** | 셸 | — | — | `winget Microsoft.PowerShell` |
| **Windows Terminal** | 터미널 | — | — | `winget Microsoft.WindowsTerminal` |
| **unzip** | 압축 해제 | — (기본 내장) | `apt install unzip` | — (기본 내장) |
| **curl** | HTTP 클라이언트 | — (기본 내장) | `apt install curl` | — (기본 내장) |

> ⚠️ 항목은 직접 다운로드 및 수동 설치가 필요합니다.
> `bun install -g @openai/codex` 실패 시 스크립트가 `npm install -g @openai/codex`로 자동 폴백합니다.

### 선택 도구 (`--wezterm`, `--docker`)

| 도구 | macOS | Linux | Windows |
|------|-------|-------|---------|
| **WezTerm** (`--wezterm`) | `brew install --cask wezterm` | apt (fury.io 저장소) | `winget wez.wezterm` |
| **Docker** (`--docker`) | `brew install --cask docker` | `get.docker.com` 스크립트 | `winget Docker.DockerDesktop` |
| **WSL2** (`-WSL2`, Windows 전용) | — | — | `wsl --install` |

---

## 터미널 앱 추천 (Windows)

| 앱 | 설명 | 설치 |
|----|------|------|
| **Windows Terminal** ⭐ | Microsoft 공식, 탭·WSL 통합 — 기본 권장 | `winget install Microsoft.WindowsTerminal` |
| **WezTerm** | GPU 가속·멀티플렉서 내장·크로스플랫폼 — 파워유저 추천 | `winget install wez.wezterm` |

WezTerm 자동 설치: `.\setup-windows.ps1 -WezTerm`

---

## 문제 해결

**설치 후 `bun: command not found`**
터미널을 재시작하세요. Windows에서는 bun이 User 환경변수에 자동으로 등록됩니다. macOS/Linux:
```bash
export PATH="$HOME/.bun/bin:$PATH"
```

**`bun install -g` 후 `codex: command not found`**
스크립트가 bun 실패 시 npm fallback으로 자동 재시도합니다. 여전히 문제가 있다면 `bun pm ls -g`로 경로를 확인한 뒤 PATH에 추가하세요. macOS에서는 Homebrew로도 설치할 수 있습니다:
```bash
brew install codex
```

**`codex login`이 완료되지 않는 경우**
로그인은 브라우저에서 ChatGPT 계정 인증으로 진행됩니다. 브라우저가 열리는지 확인하고 인증을 완료한 뒤 `codex login status`로 다시 확인하세요. Codex 사용 가능한 ChatGPT 플랜(Plus / Pro / Team)이 필요합니다.

**Windows: `스크립트 실행이 비활성화되어 있습니다`**
스크립트가 자동으로 `RemoteSigned`로 설정합니다. 수동으로 변경하려면:
```powershell
Set-ExecutionPolicy RemoteSigned -Scope CurrentUser
```

**Windows: 관리자 권한 없이 실행한 경우**
스크립트가 경고를 표시하지만 계속 진행됩니다. winget 등 일부 설치에서 오류가 발생할 수 있으므로 권장: PowerShell을 관리자 권한으로 재실행하세요.

**설치 로그 확인**
Windows 스크립트 실행 로그는 `%USERPROFILE%\workshop-setup-logs\`에 자동 저장됩니다.

---

> 저장소 루트에서 `bun setup/setup-common.ts`를 실행해서 모든 항목이 ✅로 표시되면 워크숍 준비 완료입니다.
