# 서브에이전트가 스킬로 재귀하는 것에 대한 방어 장치

스킬은 서브에이전트가 스킬을 재귀적으로 호출하거나 중첩된 에이전트를 생성하는 것(`/code-review` 서브에이전트가 `/code-review`를 다시 호출하거나, `/research` 에이전트가 다른 에이전트를 생성하는 것)에 대한 방어 장치를 추가하지 않습니다. 리프(leaf) 에이전트 지시, 깊이 제한, 또는 "이 스킬을 호출하지 마라"와 같은 줄을 추가해 달라는 요청은 범위에서 제외됩니다.

## 범위에서 제외되는 이유

무한한 서브에이전트 루프를 멈추는 책임은 스킬이 아니라 하네스에 있어야 합니다. 하네스는 서브에이전트가 접근할 수 있는 도구와 스킬, 그리고 중첩이 얼마나 깊어질 수 있는지를 결정하므로, 그곳에서 설정된 제한은 모든 스킬에 한꺼번에 적용됩니다. 하나의 스킬 서술에 작성된 방어 장치는 해당 스킬만을 다루고, 매 실행마다 토큰을 소비하며, 여전히 모델이 이를 따르기로 선택하는지에 의존합니다.

서브에이전트가 재귀하거나 제한 없이 확산된다면, 이를 하네스에 보고하십시오.

## 이전 요청

- #530: "research skill: spawned background agent can recursively re-spawn another agent (uncontrolled nesting)"
- #573: "code-review sub-agents recursively invoke /code-review and fan out" (PR #1186, "code-review: make the Standards and Spec sub-agents leaf reviewers", closed)
