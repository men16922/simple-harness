# Simple Harness

Codex·Claude Code용 플러그인입니다. 작업을 기록해 이어가고, Git으로 저장·되돌리고, 결과를 실제로 실행해 검수합니다.

## 시작하기

1. Git을 설치합니다. Windows PowerShell: `winget install Git.Git`
2. 플러그인을 설치합니다.

   ```text
   # Claude Code 대화창
   /plugin marketplace add men16922/simple-harness
   /plugin install simple-harness@simple-harness

   # Codex 터미널
   codex plugin marketplace add men16922/simple-harness
   codex plugin add simple-harness@simple-harness
   ```

3. 프로젝트 폴더에서 Agent를 열고 처음 한 번 말합니다.

   > 하네스 준비해줘. 할 일을 적고 체크하는 웹페이지를 만들고 싶어.

이후에는 하고 싶은 일만 말하면 됩니다.
준비를 요청할 때만 지침과 기록 문서를 만듭니다. 다시 요청하면 기존 내용은 보존하고
빠진 파일과 규칙 연결을 보완합니다. 준비에는 별도 스크립트나 Python 설치가 필요하지 않습니다.

## 평소에 하는 말

| 말 | 동작 |
| --- | --- |
| 하네스 준비해줘 | 작업 규칙과 기록 문서 생성 (sync) |
| 이어서 하자 | 지난 작업과 다음 할 일 요약 (sync) |
| 확인해줘 | 실제로 실행해 검수하고 문제를 고침 (verify) |
| 저장해줘 | 진행 상황 기록, 커밋 제안 (checkpoint) |
| 문서 정리해줘 | 긴 기록을 보관하고 줄임 (tidy-docs) |
| 마지막 저장 시점으로 되돌려줘 | Git으로 되돌림 |

웹 화면 검수는 Agent에 브라우저 도구(예: [Playwright MCP](https://github.com/microsoft/playwright-mcp))가 있을 때 합니다.

## 만들어지는 파일

- `AGENTS.md`: 작업 규칙. 기존 파일에는 규칙 블록만 덧붙입니다.
- `CLAUDE.md`: `@AGENTS.md`로 같은 규칙을 읽습니다.
- `docs/CONTEXT.md`: 목표와 다음 할 일. 매 세션 읽습니다.
- `docs/WORKLOG.md`: 작업 기록. 길어지면 `docs/archive/`로 옮깁니다.

## 업데이트와 삭제

```text
# Claude Code 대화창
/plugin marketplace update simple-harness
/plugin update simple-harness@simple-harness
/plugin uninstall simple-harness@simple-harness

# Codex 터미널
codex plugin marketplace upgrade simple-harness
codex plugin remove simple-harness@simple-harness
```

## 0.6.1 검증 — 2026-10-13

- 두 strict 검증과 Codex marketplace 등록·설치 통과.
- Codex 0.162.1·Claude Code 2.1.296에서 준비를 두 번 요청해 기존 내용 보존·누락 파일 복구·중복 방지 확인.
- Codex가 파일 도구로 준비하고, 준비 요청 없는 검수·저장에서 문서를 생성하지 않는 것 확인.
- macOS 로컬 검증이며 Windows 실제 실행·브라우저 검수는 미검증.
