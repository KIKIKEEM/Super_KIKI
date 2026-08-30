# Ouroboros 설치 · 설정 메모

> 대상: [Q00/ouroboros](https://github.com/Q00/ouroboros) — "Agent OS".
> 모호한 요청 → 소크라테스식 인터뷰 → Seed 스펙 고정 → 실행 → 3단계 평가 → 수렴할 때까지 진화(Evolve)하는 루프를 돌린다.
> 검증 버전: `ouroboros-ai 0.51.17` (2026-08-30)

---

## 1. 설치

Python **3.12 이상**이 필요하다. 시스템 파이썬이 3.11이어도 `uv`가 3.12를 따로 받아오므로 아래 방법이 가장 안전하다.

```bash
uv tool install 'ouroboros-ai[mcp,tui]' --python 3.12
```

설치되는 실행 파일 3개: `ouroboros`, `ooo`(짧은 별칭), `ozo`.

다른 방법 (README 기준):

```bash
# 원라이너
curl -fsSL https://raw.githubusercontent.com/Q00/ouroboros/main/scripts/install.sh | bash

# Homebrew (macOS/Linux)
brew tap q00/tap && brew install ouroboros-ai

# pip / pipx
pip install 'ouroboros-ai[mcp,tui]'
pipx install 'ouroboros-ai[mcp,tui]'
```

## 2. 런타임 설정 (1회)

Claude Code CLI를 실행 런타임으로 붙인다.

```bash
ouroboros setup --runtime claude-cli --non-interactive
```

- 설정 파일: `~/.ouroboros/config.yaml`
- 자격증명: `~/.ouroboros/credentials.yaml`
- 로그: `~/.ouroboros/logs/ouroboros.log`
- DB: `~/.ouroboros/data/ouroboros.db` (첫 실행 시 생성)

설정 GUI는 아무 때나 `ooo config`.

## 3. Claude Code에서 MCP로 쓰기

레포 루트의 `.mcp.json`에 `ouroboros` 서버가 등록돼 있다. Claude Code를 이 폴더에서 실행하면 `ouroboros_*` 툴이 붙는다.

```json
{
  "mcpServers": {
    "ouroboros": {
      "command": "uvx",
      "args": ["--python", "3.12", "--from", "ouroboros-ai[mcp]", "ouroboros", "mcp", "serve"]
    }
  }
}
```

`uv` 없이 이미 `ouroboros`가 PATH에 있다면 이렇게 바꿔도 된다:

```json
{ "mcpServers": { "ouroboros": { "command": "ouroboros", "args": ["mcp", "serve"] } } }
```

⚠️ `ouroboros_*` 툴은 **deferred(지연 로딩)** 로 노출된다. 툴 목록에 안 보인다고 없는 게 아니라, `+ouroboros <기능>` 같은 질의로 스키마를 먼저 불러와야 호출된다.

## 4. 첫 사용

```bash
# 터미널에서
ouroboros init start --orchestrator "만들고 싶은 것 한 줄"

# 에이전트 세션 안에서
ooo interview "만들고 싶은 것 한 줄"
ooo auto
```

핵심 게이트:

| 단계 | 기준 |
|---|---|
| Interview → Seed | 모호도(ambiguity) ≤ 0.2 |
| Evaluate | 3단계(기계검증 → 의미분석 → 다중모델 합의), 만족도 ≥ 0.8 |
| Evolve 종료 | 온톨로지 유사도 ≥ 0.95, 최대 30세대 |

## 5. 진단 · 제거

```bash
ouroboros doctor install   # 패키지/플러그인/MCP 설치면 점검
ouroboros mcp doctor       # MCP 실행 환경 점검
ouroboros status health    # 설정/DB/런타임/자격증명 상태
ouroboros uninstall        # 설정·MCP 등록·데이터 전부 제거
```

## 6. 알아둘 것

- **텔레메트리가 기본 ON**이다. 익명 사용 통계(명령어·버전·성공률; 코드/프롬프트/파일 내용은 아니라고 명시)를 보낸다. 끄려면:
  ```bash
  export OUROBOROS_TELEMETRY=0
  # 또는 ~/.ouroboros/config.yaml 의 telemetry.enabled: false
  ```
- `~/.ouroboros/credentials.yaml`의 anthropic 키는 아직 템플릿 값이다. Claude CLI를 런타임으로 쓰면 필수는 아니지만, Stage 3 다중모델 합의(OpenRouter 경유 GPT/Gemini)까지 쓰려면 키가 필요하다.
- 실행 시 `~/.ouroboros/worktrees/` 아래에 git worktree를 만들어 작업한다. 프로젝트 안에는 `.ouroboros/mechanical.toml`이 생길 수 있으니 필요하면 `.gitignore`에 넣는다.
- Claude Code 웹 세션 컨테이너는 휘발성이다. 세션이 끝나면 `uv tool install`로 깐 바이너리는 사라지고, 레포에 커밋된 `.mcp.json`과 이 문서만 남는다. 새 세션에서는 1번 설치부터 다시 하면 된다.
