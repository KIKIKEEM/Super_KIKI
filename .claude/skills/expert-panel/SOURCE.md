# 출처

- 원본: https://github.com/itsbluetic/expert-panel-by-ebp
- 버전: v3.1.0 (author: anmen)
- 라이선스: MIT
- 설치일: 2026-08-29
- 설치 위치: 프로젝트 로컬 (`.claude/skills/expert-panel/`)

원본 리포의 `skills/expert-panel/`(SKILL.md + references/)를 복사했고,
SKILL.md가 참조하는 `examples/EBP_타이핑vs말하기속도비교.md`가 스킬 디렉토리
기준으로 해석되도록 `examples/` 하위에 함께 배치했다.

## 로컬 수정 (원본과 다른 부분)

**`▶ [V] 독립 검증` 단계 추가** (6단계와 7단계 사이, 2026-08-29)

원본의 검증 축은 `✓ Gate` + `Checklist Before Stopping`뿐인데, 둘 다
**산출물을 만든 컨텍스트가 자기를 채점하는 구조**다. 같은 추론이 만든 오류를
같은 추론이 잡을 확률은 낮다. 그래서 별도 컨텍스트에서 도는
`ebp-verifier` 서브에이전트(`.claude/agents/10-ebp-verifier.md`)를 만들고,
저장 직전 호출하도록 SKILL.md에 단계를 끼워 넣었다.

수정된 지점 3곳:
- 6축 매핑 표의 "검증" 행
- `▶ [V] 독립 검증` 섹션 신설 (단계 번호는 재넘버링하지 않음 — 원본 대조 용이하게)
- `Checklist Before Stopping`에 V단계 항목 추가

업스트림이 갱신되면 이 3곳을 다시 얹어야 한다.

업데이트 방법:
```bash
git clone --depth 1 https://github.com/itsbluetic/expert-panel-by-ebp /tmp/ebp
cp -r /tmp/ebp/skills/expert-panel/. .claude/skills/expert-panel/
cp /tmp/ebp/examples/*.md .claude/skills/expert-panel/examples/
```
