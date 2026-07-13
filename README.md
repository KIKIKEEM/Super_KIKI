# 🪐 Super KIKI — Aurora Planet OS v1.1

멀티 에이전트 시스템: 오케스트레이터 1 + 인프라 4 + 도메인 5

```
super-kiki/
├── CLAUDE.md                    # 헌법 (북극성, 의사결정 매트릭스, 라우팅)
├── .claude/agents/
│   ├── 01-scribe.md             # 서기 — 인풋 (노션/미트/텔레그램/디스코드/메일)
│   ├── 02-mirror.md             # 거울 — 아침 6시 회고 + CBT + 오늘의 집중
│   ├── 03-chronicler.md         # 사관 — 키키실록 (인간 깃허브)
│   ├── 04-alchemist.md          # 연금술사 — 암묵지→명시지 스킬 패키지
│   ├── 05-ceo-aurora.md         # CEO — 오로라플래닛 법인/지분/Hermes 인터페이스
│   ├── 06-scholar.md            # 학자 — 박사논문 + 논문지도 4명
│   ├── 07-educator.md           # 교육자 — 연세대/홍익/한양/안그라픽스/자체캠프
│   ├── 08-creator.md            # 크리에이터 — 유튜브 채널
│   └── 09-community.md          # 커뮤니티 — 살롱/길드/주민 파이프라인
├── docs/
│   ├── kiki-inc.md          # 주식회사 키키 정관 (버추얼 기업 구조)
│   └── discord-blueprint.md # 오로라플래닛 디스코드 설계도
└── README.md
```

## 설치 (Claude Code)

1. 이 폴더를 작업 디렉토리로 복사 (또는 git init 해서 진짜 "키키 깃허브"로)
2. Claude Code 실행 → CLAUDE.md 자동 로드 → `/agents`로 서브에이전트 확인
3. MCP 연결: Notion, Gmail, Google Calendar (이미 연결돼 있으면 생략)

## 아침 6시 자동화 (n8n)

```
[Cron 06:00 KST]
  → Gmail/Notion/캘린더 수집 (전날 21:00 서기 브리프 포함)
  → Claude API 호출 (mirror 프롬프트 + 수집 데이터)
  → 결과를 노션 데일리 노트에 기록
  → 텔레그램으로 "오늘의 One Thing" 푸시
```
전날 21:00에 scribe 파이프라인이 먼저 돌아야 아침 브리프가 완성된다 (Cron 2개).

## 가동 로드맵

| Phase | 기간 | 가동 에이전트 | 성공 기준 |
|---|---|---|---|
| 1 | ~2주 | scribe + mirror | 아침 6시 회고 14일 연속 |
| 2 | 3-4주차 | chronicler + **ceo-aurora** | 주간 실록 2편 + 지분 협상 체크리스트 완료 |
| 3 | 5-8주차 | scholar, educator | 논문 주간 블록 정착, 강의 모듈화 1개 |
| 4 | 2개월~ | creator, community, alchemist | 유튜브 1편 발행, 첫 스킬 패키지 🟢 |

※ 법인 설립이 진행 중이므로 ceo-aurora는 Phase 2로 앞당김. 지분 계약 서명 전에 반드시 가동할 것.
