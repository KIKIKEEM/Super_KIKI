# 출처

- 원본: https://github.com/itsbluetic/expert-panel-by-ebp
- 버전: v3.1.0 (author: anmen)
- 라이선스: MIT
- 설치일: 2026-08-29
- 설치 위치: 프로젝트 로컬 (`.claude/skills/expert-panel/`)

원본 리포의 `skills/expert-panel/`(SKILL.md + references/)를 그대로 복사했고,
SKILL.md가 참조하는 `examples/EBP_타이핑vs말하기속도비교.md`가 스킬 디렉토리
기준으로 해석되도록 `examples/` 하위에 함께 배치했다. 그 외 내용 수정 없음.

업데이트 방법:
```bash
git clone --depth 1 https://github.com/itsbluetic/expert-panel-by-ebp /tmp/ebp
cp -r /tmp/ebp/skills/expert-panel/. .claude/skills/expert-panel/
cp /tmp/ebp/examples/*.md .claude/skills/expert-panel/examples/
```
