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

## 시작하기 전에 — 터미널 열기

이 가이드의 명령들은 모두 **터미널**에 입력합니다. 터미널은 마우스 클릭 대신 글자로 컴퓨터에 명령을 내리는 검은(또는 흰) 창입니다. 아래 명령들은 **복사해서 터미널에 붙여넣고 Enter**를 누르면 실행됩니다.

**Windows — PowerShell 관리자 권한으로 열기**

1. 화면 왼쪽 아래 **시작 버튼**(⊞)을 누릅니다.
2. `PowerShell`이라고 타이핑합니다.
3. 검색 결과에 나온 **Windows PowerShell**(또는 **PowerShell 7**) 위에서 **마우스 오른쪽 버튼**을 누릅니다.
4. **"관리자 권한으로 실행"**을 클릭합니다.
5. **"이 앱이 디바이스를 변경할 수 있도록 허용하시겠어요?"** 창이 뜨면 **"예"**를 누릅니다.

> 이 과정의 설치 명령과 `codex` 명령은 모두 이 **PowerShell 창**에서 실행합니다.

**macOS — 터미널 열기**

1. **⌘(Command) + Space**를 눌러 Spotlight 검색을 엽니다.
2. `터미널`(또는 `Terminal`)이라고 타이핑하고 Enter를 누릅니다.
3. 열린 터미널 창에 명령을 붙여넣고 Enter를 누릅니다. 권한이 필요한 명령은 앞에 `sudo`를 붙이라고 안내가 나옵니다.

---

## Codex를 쓰는 3가지 방법

Codex는 여러 환경에서 쓸 수 있습니다. **이 과정의 실습은 ① Codex CLI 기준**입니다. 문서에서 "앱에서 열기"라고 적힌 부분은 ②번 방법으로도 진행할 수 있습니다.

| 방법 | 어디서 | 언제 쓰나 |
|------|--------|-----------|
| **① Codex CLI** (이 과정 기본) | 터미널에서 `codex` 명령 | 파일이 있는 프로젝트 폴더에서 직접 코드를 만들고 명령을 실행할 때 |
| **② ChatGPT 웹/데스크톱 앱의 Codex** | 브라우저에서 [chatgpt.com/codex](https://chatgpt.com/codex) | 설치 없이 브라우저에서 가볍게 Codex를 써 보거나, "앱에서 열기" 실습을 할 때 |
| **③ IDE 확장** | VS Code 등 편집기 안 | 평소 쓰는 편집기 화면 안에서 코드를 보며 Codex와 함께 작업할 때 |

> 세 방법 모두 같은 ChatGPT 계정으로 로그인합니다. 이 가이드는 ①번 CLI 설치·로그인을 기준으로 안내합니다.

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

> **Windows 사용자를 위한 상세 안내**
> - Codex CLI의 **설치와 실행은 모두 위에서 연 PowerShell 창**에서 이루어집니다.
> - Codex CLI를 `npm install -g @openai/codex`로 설치하려면 먼저 **Node.js**(npm) 또는 **bun**이 있어야 합니다. `setup-windows.ps1` 스크립트가 bun과 필요한 도구를 자동으로 설치하므로, **스크립트를 실행하면 이 과정은 신경 쓸 필요가 없습니다.** 직접 설치를 확인하려면 아래 명령으로 버전이 출력되는지 보세요:
>   ```powershell
>   bun --version
>   node --version
>   ```
>   둘 중 하나라도 버전이 나오면 준비된 것입니다. 아무것도 안 나오면 `setup-windows.ps1`을 먼저 실행하세요.
> - 설치 직후에는 `codex` 명령이 인식되지 않을 수 있습니다. 새로 설치한 프로그램의 위치(PATH)를 터미널이 아직 모르기 때문입니다. **PowerShell 창을 닫고 새로 열면** `codex` 명령이 인식됩니다.

---

## Step 3 — Codex 로그인

Codex CLI를 처음 쓰기 전에 ChatGPT 계정으로 로그인합니다. 아래 명령을 터미널에 입력하세요:

```bash
codex login
```

이후 흐름은 다음과 같습니다:

1. 명령을 실행하면 **웹 브라우저가 자동으로 열립니다.**
2. 브라우저에서 **ChatGPT 계정으로 로그인**합니다 (Codex 사용 가능한 Plus / Pro / Team 플랜이어야 합니다).
3. 로그인이 끝나면 브라우저에 완료 메시지가 뜨고, **터미널로 돌아오면** 로그인이 완료된 상태입니다.

로그인이 완료되었는지 확인하세요:

```bash
codex login status
```

> **회사 PC 등에서 브라우저가 자동으로 열리지 않을 때**: 터미널에 **로그인용 URL**이 함께 표시됩니다. 그 URL을 복사해 브라우저 주소창에 직접 붙여넣고 로그인한 뒤, 터미널로 돌아와 `codex login status`로 확인하세요.

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
대부분 PATH 문제입니다. **터미널(PowerShell)을 닫고 새로 열어** 보세요 — 방금 설치한 프로그램의 위치를 터미널이 새로 읽어 들입니다. 그래도 안 되면 `bun pm ls -g`로 경로를 확인한 뒤 PATH에 추가하세요. macOS에서는 Homebrew로도 설치할 수 있습니다:
```bash
brew install codex
```

**`npm: command not found` (Codex CLI 설치가 안 될 때)**
Node.js(npm)나 bun이 아직 설치되지 않은 상태입니다. 설치 스크립트가 이 도구들을 자동으로 깔아 주므로, **본인 OS의 설치 스크립트를 먼저 실행**하세요 (Windows: `.\setup-windows.ps1`, macOS: `bash setup-mac.sh`, Linux: `bash setup-linux.sh`). 실행 후 터미널을 새로 열고 `bun --version`으로 준비 여부를 확인할 수 있습니다.

**로그인 시 플랜 관련 안내가 나올 때**
`codex`는 **Codex 사용 가능한 ChatGPT 플랜(Plus / Pro / Team)**으로 로그인해야 합니다. 로그인은 되는데 실습 중 사용 제한 안내가 나온다면 해당 플랜인지 확인하세요. API Key는 실습에 필수가 아니며, ChatGPT 계정 로그인(`codex login`)으로 충분합니다.

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
