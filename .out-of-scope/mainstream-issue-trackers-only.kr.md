# 이슈 트래커 통합: GitHub, GitLab, 로컬 마크다운만 지원

`setup-matt-pocock-skills`는 정확히 세 가지 이슈 트래커에 대해 일급 지원을 제공하며, 각각 `skills/engineering/setup-matt-pocock-skills/`에 있는 시드 템플릿 하나에 대응합니다.

- **GitHub** (`issue-tracker-github.md`, `gh` 사용)
- **GitLab** (`issue-tracker-gitlab.md`, `glab` 사용)
- **로컬 마크다운** (`issue-tracker-local.md`, `.scratch/` 아래의 파일)

그 밖의 다른 트래커에 대한 일급 백엔드를 추가해 달라는 요청은 범위에서 제외됩니다. 여기에는 Jira, Linear, Azure DevOps, Trello, YouTrack, 그리고 에이전트 중심의 새로운 트래커가 포함됩니다.

## 범위에서 제외되는 이유

모든 이슈 트래커 백엔드는 CLI 형태(명령, 플래그, 출력 파싱)를 스킬에 하드코딩합니다. 각각의 새로운 백엔드는 영구적인 유지 관리 대상이 됩니다. 도구의 CLI가 발전함에 따라 계속 동작해야 하며, `/to-spec`, `/to-tickets`, `/triage` 등을 대상으로 계속 테스트되어야 하기 때문입니다. 저는 GitHub을 사용하므로, 실제로 올바르게 유지할 수 있는 백엔드는 GitHub입니다. GitLab은 형태가 충분히 비슷하여 함께 지원할 수 있으며, 로컬 마크다운은 CLI가 전혀 필요하지 않습니다.

인기도는 이를 바꾸지 않습니다. Jira는 널리 사용되고 공식 CLI(`acli`)도 있지만, 여전히 템플릿을 제공하지 않습니다. Jira는 제가 운영하지 않는 백엔드이며, 테스트를 유지해야 하는 고유한 링크 의미 체계, 워크플로 상태, CLI의 특이 사항을 가지고 있습니다. 해당 도구가 주류인지 여부와 관계없이 그 비용은 저에게 돌아옵니다.

그 밖의 모든 트래커는 `/setup-matt-pocock-skills`의 **Other** 옵션을 사용합니다. 사용자가 워크플로를 한 단락으로 설명하면, 스킬이 이를 `docs/agents/issue-tracker.md`에 서술 형태로 기록합니다. 그 파일은 사용자의 것입니다. 잘 동작하는 Jira 또는 Linear 워크플로를 다듬었다면, 이를 본인의 저장소에 보관하거나 게시하고, 설정이 그것을 가리키도록 하십시오.

## 이전 요청

- #99: "Add dex as an issue tracker backend" (요청 당시 dex는 약 3개월 되었고 별이 약 300개였습니다)
- #258: "Add Jira as first-class issue tracker via Rovo MCP"
- #1137: "Add Jira as a first-class issue tracker, via Atlassian's official CLI (`acli`)"
