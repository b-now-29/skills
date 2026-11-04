---
name: setup-matt-pocock-skills
description: "엔지니어링 스킬을 위해 저장소를 구성합니다. 이슈 트래커, 트리아지 라벨 어휘, 도메인 문서 레이아웃을 설정합니다. 다른 엔지니어링 스킬을 처음 사용하기 전에 한 번 실행하십시오."
disable-model-invocation: true
---

# Matt Pocock 스킬 설정

엔지니어링 스킬이 전제로 하는 저장소별 구성의 뼈대를 만드십시오.

- **이슈 트래커**: 이슈가 있는 곳(기본값은 GitHub이며, 로컬 마크다운도 기본으로 지원됨)
- **트리아지 라벨**: 다섯 가지 표준 트리아지 역할에 사용되는 문자열
- **도메인 문서**: `GLOSSARY.md`와 ADR이 있는 곳, 그리고 이를 읽는 쪽의 규칙

이것은 결정적인 스크립트가 아니라 프롬프트 기반 스킬입니다. 탐색하고, 발견한 것을 제시하고, 사용자와 확인한 다음, 작성하십시오.

## 프로세스

### 1. 탐색

현재 저장소를 살펴보고 시작 상태를 이해하십시오. 존재하는 것은 무엇이든 읽고, 가정하지 마십시오.

- `git remote -v`와 `.git/config`: 이것이 GitHub 저장소입니까? 어느 저장소입니까?
- 저장소 루트의 `AGENTS.md`와 `CLAUDE.md`: 둘 중 하나라도 존재합니까? 둘 중 어느 쪽에 이미 `## Agent skills` 섹션이 있습니까?
- 저장소 루트의 `GLOSSARY.md`와 `GLOSSARY-MAP.md`, 그리고 레거시 `CONTEXT.md` / `CONTEXT-MAP.md`. 레거시 파일이 존재한다면, 그것을 `GLOSSARY` 이름으로 `git mv`하고 `docs/agents/domain.md`에 있는 그 이름들을 다시 쓰겠다고 제안하십시오.
- `docs/adr/` 및 모든 `src/*/docs/adr/` 디렉터리
- `docs/agents/`: 이 스킬의 이전 출력이 이미 존재합니까?
- `.scratch/`: 로컬 마크다운 이슈 트래커 관례가 이미 사용 중이라는 신호
- `triage` 스킬이 설치되어 있습니까? (이 스킬 옆에 `triage` 스킬 폴더가 있거나, 사용 가능한 스킬 목록에 `triage`가 있음.) 이것이 섹션 B를 실행할지 여부를 결정합니다.
- 모노레포 신호: `pnpm-workspace.yaml`, `package.json`의 `workspaces` 필드, 또는 자체 `src/`를 가진 채워진 `packages/*`. 이는 진정으로 큰 다중 패키지 저장소에만 존재합니다. 이것이 없다면 단일 컨텍스트이며, 거의 모든 저장소가 이에 해당합니다.

### 2. 발견 사항을 제시하고 질문

무엇이 있고 무엇이 없는지 요약하십시오. 그런 다음 섹션을 순서대로 진행하십시오. 한 섹션에 하나의 답, 그다음 섹션입니다.

사용자가 한 단어로 수락할 수 있도록, 각 섹션을 권장 답변으로 시작하십시오. 선택이 진정으로 분기될 때만 한 줄짜리 설명을 덧붙이고, 탐색 결과 이미 결정된 섹션은 완전히 건너뛰십시오(`triage`가 설치되지 않았을 때의 섹션 B, 모노레포가 아닐 때의 섹션 C).

**섹션 A: 이슈 트래커.**

> 설명: "이슈 트래커"는 이 저장소의 이슈가 있는 곳입니다. `to-tickets`, `triage`, `to-spec`과 같은 스킬이 이곳에서 읽고 씁니다. 이 스킬들은 `gh issue create`를 호출해야 하는지, `.scratch/` 아래에 마크다운 파일을 작성해야 하는지, 아니면 당신이 설명하는 다른 워크플로를 따라야 하는지 알아야 합니다. 이 저장소의 작업을 실제로 추적하는 곳을 선택하십시오.

기본 자세: 이 스킬들은 GitHub를 위해 설계되었습니다. `git remote`가 GitHub를 가리킨다면 그것을 제안하십시오. `git remote`가 GitLab(`gitlab.com` 또는 자체 호스팅 호스트)을 가리킨다면 GitLab을 제안하십시오. 그렇지 않다면(또는 사용자가 원한다면), 다음을 제시하십시오.

- **GitHub**: 이슈가 저장소의 GitHub Issues에 있음(`gh` CLI 사용)
- **GitLab**: 이슈가 저장소의 GitLab Issues에 있음([`glab`](https://gitlab.com/gitlab-org/cli) CLI 사용)
- **로컬 마크다운**: 이슈가 이 저장소의 `.scratch/<feature>/` 아래에 파일로 있음(개인 프로젝트나 원격 저장소가 없는 저장소에 적합)
- **기타**(Jira, Linear 등): 사용자에게 워크플로를 한 단락으로 설명해 달라고 요청하십시오. 스킬이 이를 자유 형식의 서술로 기록합니다

선택을 `docs/agents/issue-tracker.md`에 기록하십시오. GitHub와 GitLab 템플릿에는 "요청 창구로서의 PR(PRs as a request surface)" 플래그가 있으며, 기본값은 **꺼짐**입니다. 꺼진 상태로 두고 언급하지 마십시오. 외부 PR을 트리아지 대기열에 넣고 싶은 사용자는 나중에 파일에서 플래그를 바꿀 수 있습니다.

GitHub 또는 GitLab 트래커에는 접근 가능한 저장소가 필요합니다. 사용자가 그중 하나를 선택했는데 그 호스트를 가리키는 `git remote`가 없다면, 더 진행하기 전에 사용자에게서 저장소 URL을 받아 연결하십시오(필요하면 `git init`, `git remote add origin <url>`). 이 디렉터리 안에서 `gh repo view` / `glab repo view`가 프로젝트를 출력하면 완료입니다. 그렇게 할 수 없다면, 멈추고 무엇이 빠져 있는지 사용자에게 알리십시오.

**섹션 B: 트리아지 라벨 어휘.** `triage` 스킬이 설치되어 있지 않다면(탐색에서 알게 됨) 이 섹션을 완전히 건너뛰십시오. 설치되지 않은 스킬에는 라벨이 필요 없기 때문입니다.

설치되어 있다면, 정확히 하나의 질문을 하십시오.

> 기본 트리아지 라벨을 유지하시겠습니까? (권장: **예**)

기본값은 다섯 가지 표준 역할이며, 각 라벨 문자열은 그 이름과 같습니다: `needs-triage`, `needs-info`, `ready-for-agent`, `ready-for-human`, `wontfix`. **예**라면 그대로 작성하십시오. 사용자가 아니라고 하는 경우에만(대개 트래커가 이미 다른 이름을 사용하기 때문입니다. 예: `needs-triage` 대신 `bug:triage`), `triage`가 중복을 만들지 않고 기존 라벨을 적용하도록 재정의 값을 수집하십시오.

**섹션 C: 도메인 문서.** **단일 컨텍스트**(저장소 루트에 하나의 `GLOSSARY.md` + `docs/adr/`)를 기본으로 하십시오. 이는 거의 모든 저장소에 맞습니다. 묻지 말고 작성하십시오.

탐색에서 모노레포 신호를 발견한 경우에만 **다중 컨텍스트**(컨텍스트별 `GLOSSARY.md` 파일을 가리키는 루트 `GLOSSARY-MAP.md`)를 제안하십시오. 그런 다음 어떤 레이아웃을 원하는지 확인하십시오.

### 3. 확인 및 편집

사용자에게 다음의 초안을 보여 주십시오.

- `CLAUDE.md` / `AGENTS.md` 중 편집 대상인 파일에 추가할 `## Agent skills` 블록(선택 규칙은 4단계 참조)
- `docs/agents/issue-tracker.md`, `docs/agents/domain.md`, `docs/agents/triage-labels.md`의 내용(마지막 것은 `triage`가 설치된 경우에만)

작성하기 전에 사용자가 편집할 수 있게 하십시오.

### 4. 작성

**편집할 파일을 선택하십시오.**

- `CLAUDE.md`가 존재하면 그것을 편집하십시오.
- 그렇지 않고 `AGENTS.md`가 존재하면 그것을 편집하십시오.
- 둘 다 존재하지 않으면, 어느 것을 생성할지 사용자에게 물으십시오. 대신 선택하지 마십시오.

`CLAUDE.md`가 이미 존재할 때 `AGENTS.md`를 생성하지 마십시오(그 반대도 마찬가지). 항상 이미 있는 것을 편집하십시오.

선택한 파일에 `## Agent skills` 블록이 이미 존재한다면, 중복을 추가하지 말고 해당 위치에서 내용을 업데이트하십시오. 주변 섹션에 대한 사용자의 편집을 덮어쓰지 마십시오.

블록:

```markdown
## Agent skills

### Issue tracker

[one-line summary of where issues are tracked]. See `docs/agents/issue-tracker.md`.

### Triage labels

[one-line summary of the label vocabulary]. See `docs/agents/triage-labels.md`.

### Domain docs

[one-line summary of layout: "single-context" or "multi-context"]. See `docs/agents/domain.md`.
```

`### Triage labels` 하위 블록을 포함하고 `docs/agents/triage-labels.md`를 작성하는 것은 `triage`가 설치되어 있고 섹션 B가 실행된 경우에만 하십시오. 그렇지 않다면 둘 다 생략합니다.

GitHub 또는 GitLab에서 섹션 B가 실행된 경우, 트래커에 없는 구성된 라벨을 각각 생성하십시오(`gh label create` / `glab label create`).

그런 다음 이 스킬 폴더의 시드 템플릿을 출발점으로 삼아 문서 파일을 작성하십시오.

- [issue-tracker-github.md](./issue-tracker-github.md): GitHub 이슈 트래커
- [issue-tracker-gitlab.md](./issue-tracker-gitlab.md): GitLab 이슈 트래커
- [issue-tracker-local.md](./issue-tracker-local.md): 로컬 마크다운 이슈 트래커
- [triage-labels.md](./triage-labels.md): 라벨 매핑(`triage`가 설치된 경우에만)
- [domain.md](./domain.md): 도메인 문서를 읽는 쪽의 규칙 + 레이아웃

"기타" 이슈 트래커의 경우, 사용자의 설명을 사용하여 `docs/agents/issue-tracker.md`를 처음부터 작성하십시오.

### 5. 완료

설정이 완료되었으며 이제 어떤 엔지니어링 스킬이 이 파일들을 읽을지 사용자에게 알리십시오. 나중에 `docs/agents/*.md`를 직접 편집할 수 있으며, 이 스킬을 다시 실행하는 것은 이슈 트래커를 바꾸거나 처음부터 다시 시작하고 싶을 때만 필요하다고 언급하십시오.
