# archive-doc 설정

이 파일이 스킬의 유일한 설정 지점이다. **SKILL.md는 고치지 말고 여기만 고친다.**

## 노션

```yaml
notion_data_source_id: 08ce8717-d658-4c97-a71f-937e7a25c9fc
notion_database_url: https://app.notion.com/p/526dc2b8f31c4e20a6f483c9b041aea6
notion_database_title: 🗄️ 스킬 산출물 아카이브
```

**속성 스키마** (페이지 생성 시 이 이름 그대로 써야 한다):

| 속성 | 타입 | 값 |
|---|---|---|
| `제목` | title | 문서 제목 |
| `생성일` | date | YYYY-MM-DD |
| `스킬` | select | `expert-panel` / `kikitv-video-production` / `kikitv-daily-sns` / `mongolia-documentary` / `기타` |
| `주제 분야` | multi_select | `임상역학` / `브랜드전략` / `플랫폼알고리즘` / `교육설계` / `법인·거버넌스` / `콘텐츠` / `기타` |
| `검증 판정` | select | `PASS` / `PASS WITH FIXES` / `FAIL` / `미검증` / `해당없음` |
| `근거 강도` | select | `Strong` / `Moderate` / `Expert` / `Contested` / `Emerging` / `해당없음` |
| `한 줄 결론` | text | 2~3문장 |
| `볼트 경로` | text | 볼트 내 상대 경로 |
| `깃 커밋` | url | 커밋 permalink |
| `상태` | status | `시작 전` / `진행 중` / `완료` |

> 새 select 옵션이 필요하면 **노션에서 직접 추가**하고 이 표도 갱신할 것.
> 스키마에 없는 값을 보내면 페이지 생성이 실패한다.

## 옵시디언 볼트

```yaml
vault_repo: <미설정>          # 예: KIKIKEEM/my-vault
vault_branch: main
vault_subdir: 3.Resource/skill-outputs
local_clone: /home/user/vault
```

⚠️ **`vault_repo`가 `<미설정>`이면** 옵시디언 경로는 건너뛰고,
`Super_KIKI/vault-outbox/`에 파일만 만든 뒤 사용자에게 알린다. 노션 저장은 정상 진행한다.

**볼트 리포 연결 절차** (최초 1회):
1. `add_repo(owner, repo, access: "push")` — 푸시 권한으로 붙인다
2. `git clone` → `local_clone` 경로
3. 이 파일의 `vault_repo`를 채운다

## 폴더 규칙

```
{vault_subdir}/
├── EBP_{주제}.md              # expert-panel 산출물
├── EBP_{주제}_검증.md         # 검증 리포트 (있으면 본문과 함께)
└── {스킬}_{주제}.md           # 그 외 스킬
```
