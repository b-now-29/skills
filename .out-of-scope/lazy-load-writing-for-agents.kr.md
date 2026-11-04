# 에이전트용 글을 평가하는 스킬에서 `writing-for-agents`를 지연 로드하기

`retro`는 작성하기 직전뿐만 아니라 매 실행마다 `writing-for-agents`를 로드합니다. 스킬이 스킬, `AGENTS.md`/`CLAUDE.md`, 또는 문서를 편집할 때까지 해당 로드를 미뤄 달라는 요청은 범위에서 제외됩니다.

## 범위에서 제외되는 이유

`writing-for-agents`는 단순한 스타일 가이드 이상의 것입니다. 이 스킬은 무효(no-op) 지시가 무엇인지, 좋은 스킬을 만드는 요소가 무엇인지를 정의하며, `retro`는 무언가를 작성하기 전에 이 정의를 사용하여 자신이 읽는 지침 파일을 평가합니다. 읽고 보고만 하는 회고(retro)에도 여전히 이것이 필요합니다. 이를 지연 로드하면 No-ops 및 Skills 후보가 아무런 기준 없이 평가됩니다.

## 이전 요청

- #1238: "retro: load writing-for-agents only before writing" (closed)
