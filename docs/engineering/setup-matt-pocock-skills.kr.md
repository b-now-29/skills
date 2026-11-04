## 하는 일

`setup-matt-pocock-skills`는 하나의 저장소에 대한 세 가지 질문에 답합니다. 이슈가 어디에 있는지, 트리아지 라벨이 무엇이라고 불리는지, 도메인 문서가 어디에 있는지입니다. 그 답을 `docs/agents/` 아래에 마크다운 파일로 기록합니다.

그 파일들이 저장소마다 달라지는 유일한 것입니다. 스킬 자체는 어디서나 동일합니다. 스킬은 실행 시점에 `docs/agents/issue-tracker.md`를 읽고 그것이 말하는 대로 합니다. 그래서 세트가 GitHub에 묶여 있지 않으며, 다른 트래커를 가리키도록 스킬 파일을 편집할 일이 결코 없습니다. "스킬을 사용자 정의 이슈 트래커에 연결하라"라고 호출하면, 프로그래밍 방식으로 연결할 수 있는 무엇이든 스킬 변경 없이 동작합니다.

결정적인 스크립트가 아니라 프롬프트 기반 스킬입니다. `git remote`, `CLAUDE.md`, `GLOSSARY.md`를 읽고, 발견한 것을 제안하며, 무엇이든 작성하기 전에 사용자의 확인을 기다립니다.

## 언제 사용하는가

`/setup-matt-pocock-skills`를 입력하여 호출하며, [에이전트](https://www.aihero.dev/ai-coding-dictionary/agent)가 스스로 사용하지는 않습니다. 메타데이터가 의도적으로 이를 호출 불가로 표시하므로, 다른 어떤 스킬도 대신 이를 실행할 수 없습니다.

다른 엔지니어링 스킬을 처음 사용하기 전에, 저장소마다 한 번 사용하십시오. [triage](https://aihero.dev/skills-triage), [to-spec](https://aihero.dev/skills-to-spec), [to-tickets](https://aihero.dev/skills-to-tickets), [wayfinder](https://aihero.dev/skills-wayfinder)가 이슈가 어디로 가는지 추측하기 시작하거나, 트래커에 없는 라벨을 적용한다면, 이 저장소는 아직 설정되지 않은 것입니다. 프로젝트 도중의 저장소에서도 실행할 수 있습니다. 스킬은 이미 있는 것을 읽으므로, 이전 작업이 사라지지 않습니다.

## 사전 요구 사항

실행한 저장소에 다음을 작성합니다.

| 작성하는 것 | 위치 |
| --- | --- |
| `issue-tracker.md` | `docs/agents/` |
| `domain.md` | `docs/agents/` |
| `triage-labels.md` | `docs/agents/`, `triage` 스킬이 설치된 경우에만 |
| `## Agent skills` 블록 | `CLAUDE.md` 또는 `AGENTS.md` 중 이미 존재하는 것 |

모두 마크다운으로 커밋합니다. 사용자 수준 또는 전역 모드는 없습니다. 구성은 저장소에 있으므로, 모든 저장소가 자체 사본을 가집니다.

## 세 가지 결정

각 섹션을 권장 답변으로 시작하며, 탐색에서 이미 답이 나온 질문은 건너뜁니다. 대부분의 실행에서는 두 번의 확인만 필요합니다.

| 결정 | 제안하는 것 | 묻는 경우 |
| --- | --- | --- |
| **이슈 트래커** | `git remote`와 일치하는 것 | 항상. 이것이 유일한 실제 선택이기 때문입니다 |
| **트리아지 라벨** | 다섯 가지 표준 이름(`needs-triage`, `needs-info`, `ready-for-agent`, `ready-for-human`, `wontfix`) 유지 | `triage` 스킬이 설치된 경우에만 |
| **도메인 문서** | 단일 컨텍스트: 루트에 하나의 `GLOSSARY.md`와 `docs/adr/` | 모노레포 신호를 발견한 경우에만이며, 그때 다중 컨텍스트 `GLOSSARY-MAP.md`를 제안합니다 |

트래커 선택지:

| 선택지 | 이슈가 있는 곳 | 필요한 것 |
| --- | --- | --- |
| **GitHub** | 저장소의 GitHub Issues | `gh` CLI |
| **GitLab** | 저장소의 GitLab Issues | `glab` CLI |
| **로컬 마크다운** | 이 저장소의 `.scratch/<feature>/` 아래 파일 | 아무것도 필요 없음. 원격 저장소조차 필요 없음 |
| **기타** | 사용자가 말하는 어디든 | 워크플로를 설명하는 사용자의 한 단락 |

처음 세 가지는 스킬에 템플릿으로 포함되어 있으며 바로 동작합니다. 로컬 마크다운은 대체 수단이 아니라 완전한 선택지입니다. 스킬은 원격 저장소가 없는 개인 프로젝트를 지원합니다. 한 가지 주의 사항: GitHub를 사용한다면 로컬 마크다운을 사용하지 마십시오. 둘은 대안이므로 하나를 고르십시오.

"기타"도 완전한 선택지입니다. Jira, Linear, Azure DevOps, Beads가 모두 이 방식으로 동작합니다. 사용자가 워크플로를 설명하면, 스킬이 그 서술을 `docs/agents/issue-tracker.md`에 기록하고, 하위 스킬들이 그 서술을 따릅니다. 사용자들은 이미 이를 구축했습니다. [MCP](https://www.aihero.dev/ai-coding-dictionary/mcp)를 통한 Jira 변형, `gh`와 같은 형태의 Gitea CLI, 직접 만든 로컬 대시보드 등입니다.

## 자주 묻는 질문

**GitHub를 꼭 사용해야 합니까?**

아니요. GitHub, GitLab, `.scratch/` 아래의 로컬 마크다운은 모두 기성 템플릿으로 제공되며, 그 밖의 것은 "기타" 경로를 통해 동작합니다. 이것이 가장 많이 반복되는 질문이며, 대략 이런 말로 나옵니다: *"GitHub에 하드 락이 걸려 있다"*, *"GitLab / Jira를 쓸 수 있는가"*, *"Azure DevOps는 어떤가"*. 답은 항상 같습니다. 트래커를 고르는 것은 스킬이 아니라 설정입니다.

**스킬을 업데이트한 후 다시 실행해야 합니까?**

v1.1 이후의 직접적인 답은 '예'였습니다. 스킬 자체의 마무리 메시지는 더 부드럽습니다. 트래커를 바꾸거나 처음부터 다시 시작할 때만 다시 실행하라고 안내합니다. 둘 다 옹호할 수 있습니다. 시드 템플릿은 버전마다 바뀌므로, 이전 릴리스의 `docs/agents/issue-tracker.md`는 이제 그것을 읽는 스킬에 비해 낡을 수 있습니다. 하위 스킬이 문서가 기술하는 것과 다르게 동작한다면, 설정을 다시 실행하십시오. 비용이 적습니다.

**`CLAUDE.md`에 작성했는데, 저는 Codex를 사용합니다.**

이것은 알려진 빈틈이며, 아직 열려 있습니다. 파일 선택 규칙은 "`CLAUDE.md`가 있으면 그것을, 없으면 `AGENTS.md`를 편집한다"입니다. 어떤 [하네스](https://www.aihero.dev/ai-coding-dictionary/harness)가 실행 중인지가 아니라 어떤 파일이 존재하는지를 확인합니다. Claude Code에서 남은 `CLAUDE.md`가 있는 저장소에서는, 스킬이 Codex가 결코 읽지 않는 파일에 `## Agent skills` 블록을 작성합니다. 사용자들에게는 두 가지 우회책이 있습니다. 블록을 직접 `AGENTS.md`로 옮기거나, `AGENTS.md`를 표준으로 유지하고 `CLAUDE.md`를 그것을 가리키는 한 줄짜리 포인터로 만드는 것입니다. 둘 다 존재하지 않으면, 스킬은 하나를 고르는 대신 어느 것을 생성할지 묻습니다. 스킬이 결정해 줄 것으로 기대한 사람들은 이에 혼란을 겪었습니다.

**트리아지 라벨을 생성하지 않았습니다.**

생성하지 않습니다. `docs/agents/triage-labels.md`는 *매핑*입니다. 트래커의 어떤 문자열이 다섯 가지 표준 역할에 대응하는지 `/triage`에게 알려 줍니다. `gh label create`를 실행하지 않습니다. 새 GitHub 저장소에서는 라벨이 아직 존재하지 않으며, 사용자들은 이를 여러 번 버그로 제출했습니다. 두 가지 결과가 있습니다.

- 트래커가 이미 표준 이름을 사용한다면, 매핑은 항등 표이며 구성할 것이 없습니다. 그것이 의도된 일반적인 경우이며, 빠진 단계가 아닙니다.
- 이 스킬은 [wayfinder](https://aihero.dev/skills-wayfinder)의 `wayfinder:map`과 `wayfinder:<type>` 라벨도 생성하지 않으며, `gh issue create --label <missing>`은 라벨을 생성하는 대신 실패합니다. GitHub 저장소에서 첫 wayfinder 실행 전에 직접 생성하십시오.

**여기서 다른 스킬의 동작([그릴링](https://www.aihero.dev/ai-coding-dictionary/grilling) 진행 방식, 질문 형식, 어조)을 구성할 수 있습니까?**

아니요. 세 가지, 즉 트래커, 라벨, 문서 레이아웃만 구성합니다. 사용자들은 이곳을 사용자별 선호의 장소로 만들자고 요청했습니다. 답은 스킬이 분명한 입장을 유지하며 사용자별 구성을 받지 않는다는 것입니다. 선호는 모든 스킬이 이미 읽는 `CLAUDE.md`에 평이한 지시로 두십시오.

**모든 저장소에 커밋하는 대신 `~/.claude`에 구성을 보관할 수 있습니까?**

현재는 아닙니다. 여러 저장소에서 스킬을 실행하는 한 사용자가 이에 대한 열린 요청을 가지고 있지만, 사용자 수준 모드는 존재하지 않습니다. 모든 저장소가 자체 `docs/agents/`를 가집니다.

**다른 스킬을 구성하는 스킬이 있다는 것이 이상하지 않습니까?**

오래된 불만 하나는 그렇다고, 이렇게 말합니다: *"다른 스킬을 설정하는 스킬이 있다는 것이 맞지 않게 느껴진다. 그것은 LLM이 자신의 스킬을 구성한다는 뜻이다."* 트레이드오프는 실재합니다. 설정 단계가 없다면, 이슈를 다루는 모든 스킬이 트래커 지시의 자체 사본을 필요로 할 것입니다. 출력은 읽고 편집할 수 있는 마크다운이며, 그것이 위험을 제한합니다. 작성된 모든 파일을 읽고 직접 바꿀 수 있습니다. 일상적인 변경은 다시 실행하는 대신 그런 방식으로 하십시오.

## 제대로 동작하고 있다면

- `docs/agents/issue-tracker.md`와 `docs/agents/domain.md`가 존재하며, `triage`가 설치되어 있다면 `triage-labels.md`도 존재합니다.
- 하네스가 읽는 지침 파일에 `## Agent skills` 섹션이 나타나며, 그 파일들 각각을 가리키는 한 줄 요약이 있습니다.
- 제안한 트래커가 사용하는 원격 저장소와 일치하며, 라벨 문자열이 트래커에 존재하는 라벨과 일치합니다.
- 이후 `/to-tickets`가 이슈가 어디 있는지 묻지 않고 게시하며, `/triage`가 라벨을 만들어 내는 대신 적용합니다.
- 스킬 파일 자체는 아무것도 바뀌지 않았습니다. 설정이 `SKILL.md`를 편집했다면, 무언가 잘못된 것입니다.

## 어디에 위치하는가

`setup-matt-pocock-skills`는 엔지니어링 흐름을 위한 **일회성 설정**으로, 연쇄의 한 단계라기보다 다른 모든 것이 전제로 하는 전제 조건입니다. 이웃은 그 독자들입니다. 여기서 작성된 라벨 어휘를 적용하는 [triage](https://aihero.dev/skills-triage), 여기서 명시된 트래커에 게시하는 [to-spec](https://aihero.dev/skills-to-spec)과 [to-tickets](https://aihero.dev/skills-to-tickets), 그리고 같은 트래커 파일의 "Wayfinding operations" 섹션을 읽어 지도와 하위 [티켓](https://www.aihero.dev/ai-coding-dictionary/ticket)을 저장하는 방법을 배우는 [wayfinder](https://aihero.dev/skills-wayfinder)입니다. [domain-modeling](https://aihero.dev/skills-domain-modeling)이 나중에 설정이 기록한 도메인 문서 레이아웃을 채웁니다. 용어나 결정을 확정할 때만 `GLOSSARY.md`와 ADR을 생성하므로, 설정 후 도메인 문서가 없는 저장소는 정상입니다. 다음에 어떤 스킬을 사용할지는 [ask-matt](https://aihero.dev/skills-ask-matt)가 세트 전체에 걸쳐 안내합니다.
