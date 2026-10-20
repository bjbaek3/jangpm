# reconcile-skill

AI가 쓴 초안을 내가 고쳐서 썼다면, 그 교정에는 "지시문의 어디가 부족했는지"가 들어 있습니다.
`reconcile`은 초안과 최종본을 비교해, 같은 교정을 다시 하지 않도록 **지시문을 가장 작게 고치는 방법**을 제안하는 Claude Code 스킬입니다.

교정할 때마다 규칙을 하나씩 더하면 지시문이 부풀고 오히려 덜 지켜집니다.
그래서 이 스킬은 지우기, 합치기, 옮기기, 고쳐 쓰기를 먼저 검토하고 규칙 추가는 마지막에 둡니다.

## 설치

저장소를 받은 뒤 `.claude/skills/reconcile` 폴더를 통째로 복사합니다.

**모든 프로젝트에서 쓰기 (유저 스코프)**

macOS / Linux

```bash
git clone https://github.com/byungjunjang/reconcile-skill.git
mkdir -p ~/.claude/skills
cp -r reconcile-skill/.claude/skills/reconcile ~/.claude/skills/
```

Windows PowerShell

```powershell
git clone https://github.com/byungjunjang/reconcile-skill.git
New-Item -ItemType Directory -Force "$env:USERPROFILE\.claude\skills" | Out-Null
Copy-Item -Recurse reconcile-skill\.claude\skills\reconcile "$env:USERPROFILE\.claude\skills\"
```

**한 프로젝트에서만 쓰기 (프로젝트 스코프)**

같은 폴더를 그 프로젝트의 `.claude/skills/` 아래에 복사합니다.

설치한 뒤 Claude Code를 새로 시작하면 `/reconcile`로 부를 수 있습니다.

## 쓰는 법

**같은 대화 안에서 결과물을 교정한 직후**

```
/reconcile
```

대화 안에 초안과 교정본(또는 교정 지시)이 있으면 그것을 비교합니다.

**초안과 최종본을 따로 가지고 있을 때**

```
/reconcile 아래 두 글을 비교해줘.

[초안]
...

[최종본]
...
```

**고칠 지시문을 지정하고 싶을 때**

```
/reconcile 이번 교정을 .claude/skills/my-skill/SKILL.md 에 어떻게 반영할지 봐줘
```

스킬은 수정안을 제안만 하고, 승인하기 전에는 어떤 파일도 고치지 않습니다.

## 돌려주는 것

- 결론 한 문장: 의미 있는 차이가 몇 건이고 무엇을 권하는지
- 의미 있는 차이 목록: `초안 → 최종`과 그 차이가 보여 주는 것
- 수정 제안: 현재 문구, 바꿀 문구, 넣을 위치. 그대로 붙여 넣을 수 있는 형태
- 보류하거나 버린 항목과 그 이유

## 수정안을 고르는 순서

1. **줄인다**: 낡은 규칙 지우기, 겹치는 규칙 합치기
2. **고친다**: 작업 시점에 보이는 자리로 옮기기, 모호한 규칙 고쳐 쓰기, 금지 목록을 기준 하나로 바꾸기
3. **밖으로 뺀다**: 지시문 대신 코드나 검사로 강제하기
4. **미룬다**: 근거가 한 번뿐이면 보류
5. **늘린다**: 위 어느 것도 아닐 때만 규칙 추가

## 출처

초안과 최종본의 차이에서 지시문 수정안을 뽑는다는 발상은 Jeff Su의 [Cowork Academy](https://coworkacademy.ai/)에서 소개된 reconcile 워크플로에서 얻었습니다.
이 저장소의 스킬 문서는 그 자료를 옮기거나 번역한 것이 아니라, 실제 에이전트 구축 프로젝트에서 써 본 경험을 바탕으로 한국어로 새로 쓴 것입니다.

## 라이선스

MIT
