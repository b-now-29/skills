# 스킬 세트를 네이티브 Claude Code 플러그인으로 배포하고, 네이티브 Codex 플러그인은 보류한다

이 스킬들은 항상 [skills.sh](https://skills.sh/mattpocock/skills)(`npx skills add mattpocock/skills`)를 통해 설치할 수 있었으며, 이 방식은 Claude Code, Codex 및 기타 Agent-Skills 표준 하네스 전반에 걸쳐 편집 가능한 스킬 파일을 사용자의 프로젝트에 복사합니다. 반복적으로 제기되는 요청은 **플러그 앤 플레이(plug-and-play)** 방식의 배포입니다. 즉, 사용자가 소유하는 포크(fork)가 아니라, 편집하지 않는 읽기 전용이자 항상 최신 상태로 유지되는 번들로서 스킬 세트를 구독하는 방식입니다. 이것이 바로 네이티브 플러그인 시스템이 제공하는 기능입니다.

우리는 네이티브 **Claude Code 플러그인**을 배포하고, 당분간 네이티브 **Codex 플러그인**은 **보류**합니다. 이러한 분리는 각 생태계의 플러그인 매니페스트가 스킬을 선택하는 방식과 이 저장소의 버킷 구조 간의 관계에 의해 불가피하게 결정됩니다.

## 제약 사항: 버킷 구조의 스킬 대 단일 경로 선택

스킬은 `skills/` 아래의 버킷 폴더에 위치합니다. `engineering/`과 `productivity/`는 **승격된(promoted)** 버킷(배포 대상)이며, `misc/`, `personal/`, `in-progress/`, `deprecated/`는 **승격되지 않은** 버킷입니다. 플러그인은 승격된 세트만을 노출해야 하며, 이 세트는 두 개의 버킷 폴더에 걸쳐 있습니다.

- **Claude Code**: `.claude-plugin/plugin.json`은 `skills`를 **명시적인 스킬 디렉터리 경로의 배열**로 받습니다. 우리는 승격된 스킬을 하나씩 나열하여 그 외의 모든 것을 모호함 없이 제외하고, `.claude-plugin/marketplace.json`을 추가하여 이 저장소 자체가 단일 플러그인 마켓플레이스가 되도록 합니다. 처음부터 끝까지 검증되었습니다. `claude plugin validate . --strict`가 통과하며, `marketplace add` → `install`이 모든 승격된 스킬을 해석합니다.

- **Codex**: `.codex-plugin/plugin.json`은 `skills`를 **단일 경로 문자열**로만 받으며(배열은 `missing or invalid plugin.json` 오류와 함께 거부됩니다), Codex는 해당 경로 아래에서 `SKILL.md` 파일을 재귀적으로 탐색합니다. 하나의 경로로 두 개의 버킷 폴더를 지정하거나 일부만 선별할 방법이 없습니다. 두 가지 우회 방법을 시험했으나 모두 기각되었습니다.
  - `./skills/`를 가리키면 `deprecated/`, `in-progress/`, `personal/`, `misc/`까지 함께 배포됩니다. 즉, 우리가 의도적으로 승격하지 않은 폐기된 스킬, 초안 스킬, 개인용 스킬이 포함됩니다.
  - 버킷을 가리키는 **심볼릭 링크**로 구성된 선별된 평면 디렉터리는 설치 과정에서 유지되지 않습니다. Codex는 플러그인 트리를 자체 캐시로 복사하면서 **심볼릭 링크를 제거**하므로, 스킬이 빈 상태로 도착합니다.

Codex에 승격된 스킬만 담긴 단일 경로를 제공하는 견고한 방법은 다음 두 가지뿐입니다. (a) `skills/`가 승격된 스킬만 포함하도록 **구조를 변경**하는 방법(승격되지 않은 버킷을 밖으로 옮기는 것으로, `CLAUDE.md`, `scripts/link-skills.sh`, 버킷 README, 그리고 `in-progress/`와 `personal/`에 의존하는 로컬 개발 워크플로 전반에 큰 영향을 미칩니다), 또는 (b) 승격된 스킬의 **중복 사본을 평면 디렉터리에 커밋**하는 방법(동기화 부담과 두 번째 진실 공급원이 생깁니다)입니다. 두 방법 모두 구조적인 결정이며, Claude 플러그인 배포와 함께 묶어서 처리할 사안이 아닙니다. 이것이 아마도 이전에 플러그인을 배포하지 않았던, 반쯤 기억나는 원래 이유였을 가능성이 매우 높습니다. 즉, 매니페스트 형식이 버킷 구조 저장소의 선별된 부분 집합을 깔끔하게 표현하지 못했던 것입니다.

## 결정

- **Claude Code 플러그인**(`.claude-plugin/plugin.json` + `.claude-plugin/marketplace.json`)을 승격된 세트로 선별하여 지금 배포하며, 이를 v1.2의 핵심 산출물로 삼습니다.
- **skills.sh**를 범용 설치 도구로 유지합니다. 이 도구는 이미 오늘날 Codex 및 기타 하네스를 지원하므로, 설치 경로가 없는 Codex 사용자는 발생하지 않습니다.
- `skills/`를 승격된 스킬 전용으로 구조 변경할지, 아니면 생성된 평면 사본을 커밋할지 결정할 때까지 네이티브 Codex 플러그인을 **보류**합니다. Codex가 `skills` 배열 또는 포함 목록을 지원하거나, 설치 시 심볼릭 링크를 보존하게 되면 다시 검토합니다.

## 이로 인해 생기는 불변 조건

- 모든 승격된 스킬은 `.claude-plugin/plugin.json`의 `skills` 배열에 항목을 가집니다(이는 이미 `CLAUDE.md` 규칙으로 존재했으며, 이제 플러그인의 내용물도 결정합니다).
- `.claude-plugin/plugin.json`의 `version`은 `package.json`의 버전을 따릅니다. 릴리스 시 두 값을 함께 올리십시오. Claude는 플러그인 `version`을 사용하여 설치된 사용자에게 업데이트를 표시할 시점을 결정합니다.

## 업데이트, 2026-08-05

`mattpocock-skills`가 **Claude Code의 공식 마켓플레이스**(구성 이름 `claude-plugins-official`, 소스 저장소 `anthropics/claude-plugins-official`)에 등록되었습니다. 이 마켓플레이스는 모든 Claude Code 설치에 기본으로 포함되어 있습니다. 이제 `claude plugins install mattpocock-skills`가 문서화된 경로이며, 위의 `marketplace add` → `install` 경로는 대체되었습니다. 설치 문구는 [.agents/install-block.md](../install-block.md)에 있습니다.

공식 목록은 이 저장소의 git URL을 가리키고 `.claude-plugin/plugin.json`을 직접 읽으므로, `.claude-plugin/marketplace.json`에 의존하지 않습니다. 해당 파일은 저장소를 직접 설치하는 경우(릴리스되지 않은 커밋 또는 포크)를 위한 대안으로만 유지됩니다.

2026-08-05에 Claude Code 2.1.222에서 실제 목록을 대상으로 검증했습니다.

- `claude plugins install mattpocock-skills`는 마켓플레이스를 먼저 추가하지 않아도 해석되며, `mattpocock-skills@claude-plugins-official`로 보고됩니다.
- 이후 `claude plugin details mattpocock-skills`는 버전 1.2.0을 보고하고 승격된 스킬을 로드합니다.
- 목록의 `source`는 `{"source": "url", "url": "https://github.com/mattpocock/skills.git", "sha": …}`입니다. **sha가 고정되어 있으므로**, 릴리스는 우리가 태그를 다는 순간이 아니라 해당 고정 값이 이동할 때 설치된 사용자에게 도달합니다. 작성 시점에 고정 값은 `main`보다 두 커밋 뒤에 있으며, 이 때문에 `plugin.json`의 24개가 아닌 22개의 스킬이 나열됩니다.
- 세션 내 `/plugin install mattpocock-skills`는 **실행해 보지 않았습니다**. `/plugin`은 헤드리스(`claude -p`) 세션에서 사용할 수 없기 때문입니다. 이 명령은 CLI와 동일한 해석기를 실행하며, 문서화된 예시 형식은 `/plugin install <name>@claude-plugins-official`입니다.

## 업데이트, 2026-10-07

위의 Codex 제약 사항은 더 이상 유효하지 않습니다. Codex `main`은 `skills` 문자열 배열을 받으며, `.codex-plugin/`이 없으면 `.claude-plugin/`으로 대체합니다([manifest.rs](https://github.com/openai/codex/blob/main/codex-rs/core-plugins/src/manifest.rs)). Codex는 여전히 심볼릭 링크를 제거합니다.

Codex 0.161.0에서 `@mattpocock` 마켓플레이스 설치는 승격된 모델 호출(model-invoked) 스킬을 로드하며, `misc/` 또는 `in-progress/`에서는 아무것도 로드하지 않습니다. Copilot CLI는 동일한 매니페스트를 읽으며 "Installed 27 skills"를 보고합니다.

## 업데이트, 2026-10-08: 관리형 설치 우선

이제 `@mattpocock`이 Codex, Copilot, VS Code에서 주요 경로이며, 그 대가로 Copilot에서는 일회성 옵트인이 필요합니다. Claude Code는 2026-08-05 업데이트에서와 같이 `claude-plugins-official`을 유지합니다. 기본적으로 자동 업데이트되며 `marketplace add`가 필요 없기 때문입니다.

위의 버전 불변 조건은 이제 모든 관리형 경로에 적용됩니다. `npm run version`은 이미 `scripts/sync-plugin-version.mjs`를 실행하여 이를 유지합니다. `marketplace.json`에는 `version` 필드가 없으므로 값이 어긋날 수 없습니다.
