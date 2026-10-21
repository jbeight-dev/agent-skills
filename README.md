# agent-skills

개인 Claude Code 스킬 모음. 업무에 반복되는 작업(발표 자료, WBS, PRD 등)을 스킬로 만들어 재사용한다.

참고: https://github.com/mattpocock/skills

## 스킬 목록

| 스킬 | 용도 |
|---|---|
| [editorial-slide-deck](skills/editorial-slide-deck/) | 기술 가이드·교육용 4:3 HTML 슬라이드 생성 |
| [wbs](skills/wbs/) | Data Platform 기능 개발 WBS 작성 |
| [engineering](skills/engineering/) | diagnose, grill-with-docs, to-prd |

## 구조

```
agent-skills/
├── skills/<skill-name>/
│   ├── SKILL.md       # frontmatter(name, description) + 지침
│   ├── references/    # 필요할 때 읽는 참고 문서
│   └── assets/        # 템플릿 등
└── prompt/            # 스킬 실행용 프롬프트 예시
```

## 사용법

`~/.claude/skills/`에 심볼릭 링크로 연결한다.

```sh
ln -s "$PWD/skills/editorial-slide-deck" ~/.claude/skills/
```

## 새 스킬 추가

1. `skills/<name>/SKILL.md` 생성
2. frontmatter에 `name`, `description` 작성 (`description`이 트리거 조건)
3. 위 표에 한 줄 추가
