스킬은 `skills/` 아래의 버킷 폴더로 구성됩니다.

- `engineering/`: 일상적인 코드 작업
- `productivity/`: 코드 외의 일상적인 워크플로 도구
- `misc/`: 보관은 하지만 거의 사용하지 않으며, 승격되지 않음
- `in-progress/`: 베타. 의도적으로 공개되어 있으며 피드백을 환영하지만, 플러그인에는 포함되어 배포되지 않음
- `deprecated/`: 더 이상 사용하지 않음

`engineering/` 또는 `productivity/`(**승격된(promoted)** 버킷)에 있는 모든 스킬은 최상위 `README.md`에 참조가 있어야 하며, `.claude-plugin/plugin.json`의 `skills` 배열에 항목이 있어야 합니다(Claude Code 플러그인은 정확히 승격된 세트만 배포합니다). `misc/`, `in-progress/`, `deprecated/`에 있는 스킬은 둘 중 어디에도 나타나서는 안 됩니다.

설치 명령은 [.agents/install-block.md](./.agents/install-block.md)에서 그대로 복사합니다. `.claude-plugin/marketplace.json`은 이 저장소 자체의 마켓플레이스입니다. Claude Code를 제외한 모든 에이전트는 자동 업데이트를 받기 위해 이곳에서 설치하며, Claude Code는 `claude-plugins-official`을 사용합니다. 두 매니페스트 중 하나라도 수정한 후에는 `claude plugin validate . --strict`를 실행하십시오. 그 이유는 [ADR 0002](./.agents/adr/0002-ship-as-a-claude-code-plugin.md)에 기록되어 있습니다.

최상위 `README.md`의 각 스킬 항목은 스킬 이름을 해당 `SKILL.md`에 링크해야 합니다.

각 버킷 폴더에는 버킷 내의 모든 스킬을 한 줄 설명과 함께 나열하는 `README.md`가 있으며, 스킬 이름은 해당 `SKILL.md`에 링크됩니다. 승격된 버킷의 `README.md`와 최상위 `README.md`는 항목을 **사용자 호출(User-invoked)**과 **모델 호출(Model-invoked)**로 그룹화합니다. 승격되지 않은 버킷의 `README.md`(`misc/`, `in-progress/`)는 평면 목록을 사용합니다.

`engineering/`과 `productivity/`에 있는 스킬은 `docs/<bucket>/<skill-name>.md`에 사람을 위한 문서 페이지도 가집니다(문서 트리는 `skills/` 아래의 이 두 버킷 폴더 구조를 그대로 반영합니다). 게시되는 URL은 버킷과 관계없이 `https://aihero.dev/skills-<skill-name>`입니다. 문서 경로는 저장소 구성을 위한 것일 뿐입니다. `engineering/` 또는 `productivity/`에 스킬을 추가하거나, 이름을 변경하거나, 동작을 변경할 때는 [.agents/writing-docs.md](./.agents/writing-docs.md)에 따라 해당 문서 페이지를 생성하거나 다시 동기화하십시오. 완성된 페이지는 네 개의 섹션을 가집니다. **What it does**, **When to reach for it**, **Common questions**, **It's working if**입니다. `writing-docs.md`에는 템플릿, 섹션 순서, 그리고 질문을 찾아볼 곳이 담겨 있습니다. 승격되지 않은 버킷(`misc/`, `in-progress/`, `deprecated/`)의 스킬은 문서 페이지를 **갖지 않습니다**. 유일한 예외는 완전히 제거된 승격 스킬입니다. 그 페이지는 보관됨(archived)으로 표시된 채 유지됩니다(`writing-docs.md` 참조).

모든 `SKILL.md`는 사용자 호출(`disable-model-invocation: true` 및 `agents/openai.yaml`의 `policy.allow_implicit_invocation: false`, 사람만 도달 가능) 또는 모델 호출(모델 또는 사용자가 도달 가능) 중 하나입니다. [.agents/invocation.md](./.agents/invocation.md)를 참조하십시오.

[`ask-matt`](./skills/engineering/ask-matt/SKILL.md)는 사용자가 도달할 수 있는 모든 스킬과 그 관계를 지도로 나타내는 라우터입니다. 문서 페이지를 다시 동기화하는 것과 같은 트리거가 이 라우터에도 적용됩니다. 사용자가 도달할 수 있는 스킬을 추가하거나, 이름을 변경하거나, 제거하거나, 그 스킬이 흐름에 들어맞는 방식을 변경할 때마다, `ask-matt`의 `SKILL.md`를 다시 읽고 지도가 정확하게 유지되도록 업데이트하십시오. 한 번도 언급하지 않은 새 스킬이 있거나, 여전히 낡은 스킬로 라우팅한다면, 그 라우터는 거짓을 말하는 것입니다.

`deprecated/`와 `misc/` 외부의 모든 스킬을 로컬 하네스 스킬 디렉터리(`~/.claude/skills`, `~/.agents/skills`)에 (다시) 링크하려면 `scripts/link-skills.sh`를 실행하십시오. 각 항목은 이 저장소를 가리키는 심볼릭 링크이므로, `git pull`을 하면 설치된 스킬이 최신 상태로 유지됩니다. 스킬을 추가, 제거, 또는 이름 변경한 후에는 스크립트를 다시 실행하십시오.

이 저장소의 서술(`SKILL.md` 파일, 문서, `README.md`, `CHANGELOG.md`, ADR, 체인지셋, 코드 주석) 어디에도 엠 대시(em-dash)를 사용하지 않습니다. 문장이 엠 대시를 필요로 하는 경우, 대신 쉼표, 콜론, 마침표, 괄호, 또는 접속사 중 문장이 실제로 원하는 것을 사용하여 다시 작성하십시오. 맹목적으로 문자만 치환하는 일은 절대 하지 마십시오.

서브에이전트를 디스패치하는 모든 스킬은 새로운 컨텍스트 윈도우로 서브에이전트를 시작하라고 명시합니다. 일부 하네스(예: Codex)는 기본적으로 부모 대화를 포크하며, 포크는 부모의 컨텍스트를 상속합니다. 이는 서브에이전트가 벗어나려 했던 바로 그것입니다.

## 에이전트 스킬

### 트리아지 라벨

표준 이름을 변경 없이 사용합니다. `docs/agents/triage-labels.md`를 참조하십시오. 이슈는 [`SCOPE.md`](./SCOPE.md)를 기준으로 판단합니다.
