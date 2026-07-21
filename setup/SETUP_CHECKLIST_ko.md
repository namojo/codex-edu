# 워크숍 사전 설치 체크리스트

> 설치 스크립트를 실행하기 **전에** 이 체크리스트를 완료하세요.
> 아래 항목들은 자동화가 불가능하며 직접 처리가 필요합니다.

---

## 1. 구독 확인 (최우선)

워크숍 실습에 사용하는 도구는 유효한 구독이 필요합니다.

| 도구 | 필요 플랜 | 확인 |
|------|----------|------|
| **Codex CLI** (`codex`) | Codex 사용 가능한 ChatGPT 플랜 (Plus / Pro / Team) | [ ] |

> ⚠️ **API Key 관련**: API Key는 구독 플랜 외부에서 별도 연동이 필요한 경우에만 사용합니다. 워크숍 실습은 ChatGPT 계정 로그인(`codex login`)으로 충분하며, API Key 발급은 꼭 필요한 경우에만 진행하세요.

---

## 2. 계정 준비

- [ ] **ChatGPT(OpenAI) 계정** — `codex login`에 필요 (Codex 사용 가능한 플랜이어야 함)
- [ ] **GitHub 계정** — `gh auth login` 및 PR 실습에 필요
  - 계정이 없으면 [github.com](https://github.com)에서 미리 가입하세요

---

## 3. 시스템 요구사항

- [ ] OS: Windows 11 (Intel) / macOS Sequoia 15 이상 Apple Silicon (M 시리즈) / Ubuntu 24.04 이상
- [ ] 여유 디스크 공간: **5 GB 이상**
- [ ] 관리자 / sudo 권한 보유
  - **Windows**: 시작 → **"PowerShell"** 검색 → 우클릭 → **"관리자 권한으로 실행"**
    - 또는: `Win + X` → **"터미널(관리자)"** / **"Windows PowerShell(관리자)"**
    - 이후 뜨는 UAC(사용자 계정 컨트롤) 확인 창에서 **"예"** 클릭
  - **macOS / Linux**: 명령어 앞에 `sudo`를 붙여서 실행
- [ ] 안정적인 인터넷 연결 (총 다운로드 용량 약 1–2 GB)

---

## 4. Git 사용자 설정

git 설치 후 아래 명령어로 사용자 정보를 등록하세요:

```bash
git config --global user.name  "홍길동"
git config --global user.email "you@example.com"
```

- [ ] `git config --global user.name` 설정 완료
- [ ] `git config --global user.email` 설정 완료

---

## 5. GitHub 인증

```bash
gh auth login
```

안내에 따라 브라우저에서 인증을 완료하세요.

- [ ] `gh auth status` 실행 시 "Logged in" 표시 확인

---

## 6. Codex 로그인

Codex CLI 설치 후 ChatGPT 계정으로 로그인하세요:

```bash
codex login
```

- [ ] `codex login status` 실행 시 로그인 상태 확인 완료

---

## 7. 실습별 Python 의존성 설치 (저장소 클론 후)

실습 트랙에 따라 아래 Python 패키지를 미리 설치해 두면 세션 중 대기 시간이 줄어듭니다.

**tool / mcp-server 실습** — MCP 서버 실습에 필요한 의존성:

```bash
cd tool/mcp-server
pip3 install -r requirements.txt
```

- [ ] `tool/mcp-server/` 폴더에서 `pip3 install -r requirements.txt` 완료

**codex-engineering 트랙 A 실습** — 테스트 실행용 pytest:

```bash
pip3 install pytest
```

- [ ] `pip3 install pytest` 완료 (`pytest --version`으로 확인)

> **Docker**는 선택 사항입니다. 운영자가 별도로 안내하는 경우에만 설치하세요.
> macOS/Linux: 설치 스크립트에 `--docker` 플래그 추가. Windows: `-Docker` 플래그.
> - [ ] *(선택)* Docker 설치 및 데몬 실행 확인

---

## 8. 최종 환경 확인 (워크숍 전 반드시 실행)

저장소 루트에서 아래 명령어를 실행하세요 (검증 스크립트는 `setup/` 폴더에 있습니다):

```bash
bun setup/setup-common.ts
```

출력 표의 모든 항목이 ✅로 표시되면 준비 완료입니다.

---

> 문의사항은 워크숍 시작 전에 운영자에게 연락하세요.
