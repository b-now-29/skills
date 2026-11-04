# 하네스 내장 명령을 피하기 위한 스킬 이름 변경

하네스가 같은 이름의 내장 명령이나 스킬(`/prototype`, `/research`, `/code-review` 등)을 제공한다는 이유로 스킬 이름을 변경하지 않습니다. 충돌을 피하기 위해 스킬 이름을 변경하거나 별칭을 추가해 달라는 요청은 범위에서 제외됩니다.

## 범위에서 제외되는 이유

하네스는 내장 기능을 끊임없이 추가하며, 각 하네스는 자체적으로 이름을 정합니다. 그중 하나가 이미 사용 중인 이름을 차지할 때마다 이름을 변경한다면, Claude Code, Copilot, Devin 등 전반에 걸쳐 움직이는 표적을 쫓아야 하며, 그때마다 모든 사용자의 손에 익은 사용 습관과 스킬 간의 모든 상호 참조가 깨지게 됩니다.

하네스가 같은 이름을 가진 두 항목을 어떻게 해석하는지는 스킬이 아니라 하네스의 동작입니다. 스킬 텍스트는 어느 쪽이든 올바릅니다.

해결 방법은 네임스페이스 호출입니다. Claude Code 플러그인은 모든 스킬을 플러그인 이름 아래에 노출하므로, 언제든지 명시적으로 이 저장소의 스킬에 접근할 수 있습니다.

```
/mattpocock-skills:research
/mattpocock-skills:code-review
```

skills.sh로 설치했다면 해당 파일은 사용자의 것입니다. 본인의 사본에서 폴더 이름과 `name:` 필드를 변경하십시오.

하네스가 네임스페이스가 지정되거나 이름이 변경된 스킬에 접근할 방법을 전혀 제공하지 않는다면, 이를 하네스에 보고하십시오.

## 이전 요청

- #423: "/code-review shadows Claude Code own review skill"
- #483: "/code-review name clash with Claude Code built-in"
- #857: "Rename the research skill to avoid conflict with Copilot's built-in /research command"
- #1019: "Shorthand `/prototype` conflicts with hidden new Claude Code built-in skill `/prototype`"
- #1037: "Skill name overlap with devin cli inbuilt commands"
