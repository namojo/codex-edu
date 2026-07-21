# Codex에 MCP Tool 등록하기

`production-metrics` 서버를 Codex에 붙입니다. **server.py는 한 줄도 바꾸지 않습니다** —
MCP는 오픈 표준이라, 표준을 따르는 서버는 어떤 클라이언트든 등록만 하면 그대로 씁니다.

## 등록

```bash
# stdio 서버 등록 (mac/Linux). Codex는 실행 위치가 달라질 수 있으니 절대경로를 권장.
codex mcp add production-metrics -- python3 /absolute/path/to/codex-edu/tool/mcp-server/server.py
```

Windows 예 (Windows는 보통 `python3`가 아니라 `python` 실행기를 씁니다):
```bash
codex mcp add production-metrics -- python C:\Work\codex-edu\tool\mcp-server\server.py
```

venv를 쓴다면 파이썬 대신 venv 파이썬 절대경로를 주세요:
```bash
codex mcp add production-metrics -- C:\Work\codex-edu\tool\mcp-server\.venv\Scripts\python.exe C:\Work\codex-edu\tool\mcp-server\server.py
```

## 관리 명령

```bash
codex mcp list                       # 등록된 MCP 서버 목록
codex mcp get production-metrics --json
codex mcp remove production-metrics
```

## 사용

**대화형** — `codex`를 실행한 뒤 입력합니다. Codex가 도구를 호출하기 전에 **승인을
묻습니다**. 내용을 확인하고 허용하세요.

```
production-metrics 도구로 07-14 B라인 OEE를 구해줘.
```

- 모델이 OEE를 직접 암산하려 하면(도구를 안 부르면), "compute_oee 도구를 사용해서"라고
  명시하면 됩니다. 도구 설명(docstring)이 구체적일수록 자동 호출이 잘 됩니다.

**자동화** — `codex exec`(비대화형)는 사람이 없으므로 승인 대신 **샌드박스**로 통제합니다:

```bash
codex exec --sandbox read-only \
  "production-metrics MCP로 07-14 A·B·C 세 라인의 OEE를 구하고,
   가장 낮은 라인의 병목 축과 개선 포인트를 표로 정리해라"
```

- `--sandbox read-only`: 이 도구는 CSV를 읽기만 하므로 읽기 전용 샌드박스로 충분합니다.
  자동화의 가장 안전한 기본값입니다.
- 결과를 파일로 받으려면 `--output-last-message /tmp/oee.md`를 붙이세요.

## 설정 파일로 등록 (재현성)

`codex mcp add`는 결국 `~/.codex/config.toml`에 아래 형태를 씁니다. 직접 편집해도 됩니다:

```toml
[mcp_servers.production-metrics]
command = "python"
args = ["C:\\Work\\codex-edu\\tool\\mcp-server\\server.py"]
```

이 블록을 팀 문서에 공유하면 누구나 같은 도구 환경을 재현할 수 있습니다.

## 다른 MCP 클라이언트에서의 재사용

MCP 클라이언트는 각자 자기 방식(설정 파일·등록 명령)으로 도구 풀을 관리하므로,
클라이언트가 여러 개라면 **각각 등록**해야 합니다. 하지만 등록 대상인 server.py는
완전히 동일합니다 — **도구의 원본은 하나**이고, 계산 로직을 고치면 등록해 둔 모든
클라이언트에 즉시 반영됩니다. 이것이 사내 도구를 자산으로 굳히는 방식입니다.

## 자주 나는 오류

| 증상 | 원인 / 해결 |
|---|---|
| `spawn python3 ENOENT` 류 실행 실패 | 등록에 쓴 파이썬(`python3`/`python`)이 PATH에 없음. 파이썬 절대경로로 등록. |
| 도구 목록에 안 뜸 | `codex mcp list`로 등록부터 확인. 등록 후 새 세션에서 사용. |
| `ModuleNotFoundError: mcp` | 서버를 실행하는 파이썬에 `pip3 install -r requirements.txt`가 안 됨 (venv 경로 확인). |
| 데이터 못 찾음 | server.py는 자기 위치 기준으로 `data/production.csv`를 찾음. 파일 이동 시 경로 수정. |
