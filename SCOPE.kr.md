# 범위

이 저장소는 제가 매일 사용하는 스킬의 집합입니다. 선별된 저장소입니다. 아이디어는 환영하며, 각 아이디어는 아래의 기준에 따라 판단됩니다. 이슈는 스킬에 대한 변경을 추적하기 위한 것입니다. 질문과 논의는 [GitHub Discussions](https://github.com/mattpocock/skills/discussions)를 이용하십시오.

## 기준

아이디어 또는 피드백 이슈는 다음 **두** 가지 조건을 모두 충족하는 경우에만 열린 상태로 유지됩니다.

1. **관찰된 실패.** 실제 세션에서 잘못된 무언가를 설명해야 합니다. 무엇을 실행했는지, 스킬이 무엇을 했는지, 무엇을 기대했는지를 기술합니다. 가정적인 개선 사항("…하면 더 좋을 것 같다")은 이 조건을 충족하지 않습니다.
2. **철학에 부합.** [`.out-of-scope/`](./.out-of-scope/)의 어떤 항목이나 과거의 거절 사항과 일치하지 않아야 하며, 구성 옵션, 하네스별 분기, 또는 한 사람의 워크플로에 맞춘 조정이 아니어야 합니다. 그러한 것들은 본인의 `CLAUDE.md` / `AGENTS.md`, 또는 포크(skills.sh는 편집 가능한 사본을 제공합니다)에 속합니다.

크기는 관계없습니다. 한 단어짜리 수정이든 전체 재작성이든 같은 기준이 적용됩니다. 반응과 +1 댓글은 기준에 반영되지 않습니다.

## 버킷별

- **`engineering/`, `productivity/`, `in-progress/`**: 위의 기준이 적용됩니다.
- **`misc/`**: 동결되어 있으며 유지 관리되지 않습니다. 모든 이슈는 종료됩니다. [`frozen-misc-skills.md`](./.out-of-scope/frozen-misc-skills.md)를 참조하십시오.
- **새로운 스킬**: 제안과 기여는 받지 않습니다. 기존 스킬로 동작을 조합할 수 있다면 새로운 스킬로 만들지 않습니다. [`new-skills.md`](./.out-of-scope/new-skills.md)를 참조하십시오.

## 이미 결정된 사항

[`.out-of-scope/`](./.out-of-scope/)의 각 파일은 거절된 개념 하나와 그 이유를 기록합니다. 제출하기 전에 읽어 보십시오.

- [`frozen-misc-skills.md`](./.out-of-scope/frozen-misc-skills.md)
- [`harness-name-collisions.md`](./.out-of-scope/harness-name-collisions.md)
- [`mainstream-issue-trackers-only.md`](./.out-of-scope/mainstream-issue-trackers-only.md)
- [`native-question-tool.md`](./.out-of-scope/native-question-tool.md)
- [`new-skills.md`](./.out-of-scope/new-skills.md)
- [`question-limits.md`](./.out-of-scope/question-limits.md)
- [`setup-skill-verify-mode.md`](./.out-of-scope/setup-skill-verify-mode.md)
- [`subagent-recursion.md`](./.out-of-scope/subagent-recursion.md)

## 불명확한 이슈

기준에 따라 판단할 수 없는 이슈는 한 차례의 질문과 함께 `needs-info` 라벨을 받습니다. 14일 이내에 보고자의 답변이 없으면 종료됩니다. 거절된 이슈는 "not planned"로 종료됩니다.
