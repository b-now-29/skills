# Productivity

코드에 국한되지 않는 일반적인 워크플로 도구입니다.

## 사용자 호출

사용자가 직접 입력할 때만 도달할 수 있습니다(Claude Code: `disable-model-invocation: true`, Codex: `agents/openai.yaml`의 `policy.allow_implicit_invocation: false`).

- **[grill-me](./grill-me/SKILL.md)**: 설계 트리의 모든 가지가 해결될 때까지 계획이나 설계에 대해 끈질기게 인터뷰를 받습니다.
- **[handoff](./handoff/SKILL.md)**: 다른 에이전트가 작업을 이어갈 수 있도록 현재 대화를 인계 문서로 압축합니다.
- **[teach](./teach/SKILL.md)**: 현재 디렉터리를 상태 저장 교육 작업 공간으로 사용하여, 여러 세션에 걸쳐 사용자에게 새로운 기술이나 개념을 가르칩니다.
- **[to-questionnaire](./to-questionnaire/SKILL.md)**: 혼자서는 답할 수 없는 결정을, 답할 수 있는 단 한 사람을 위한 마크다운 설문지로 변환합니다(비동기로 작성하거나, 회의에서 함께 작성).
- **[wait-what](./wait-what/SKILL.md)**: 메시지가 이해되지 않는 순간 바로 실행하십시오. 에이전트가 사용자에게 부족한 맥락을 보충하여, `GLOSSARY.md`의 어휘를 사용해 평이한 언어로 다시 설명합니다.

## 모델 호출

모델 또는 사용자가 도달할 수 있습니다(모델이 사용할 수 있도록 풍부한 트리거 문구를 가집니다).

- **[grilling](./grilling/SKILL.md)**: 설계 트리의 모든 가지가 해결될 때까지 계획, 결정, 또는 아이디어에 대해 사용자를 끈질기게 인터뷰합니다.
- **[writing-for-agents](./writing-for-agents/SKILL.md)**: 에이전트를 위한 문서 작성입니다. 스킬, AGENTS.md/CLAUDE.md, 그리고 에이전트가 포인터를 통해 도달하는 모든 문서가 해당합니다.
