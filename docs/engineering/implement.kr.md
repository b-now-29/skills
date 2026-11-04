## 하는 일

`implement`는 이미 결정된 작업을 구현합니다. [티켓](https://www.aihero.dev/ai-coding-dictionary/ticket), [명세](https://www.aihero.dev/ai-coding-dictionary/spec), 또는 방금 대화에서 합의한 계획을 가리키면, 코드를 작성하고, 시임에서 [tdd](https://aihero.dev/skills-tdd)를 진행하고, 진행하면서 타입 검사를 하고, 마지막에 [code-review](https://aihero.dev/skills-code-review)를 실행하고, 현재 브랜치에 커밋합니다.

계획을 결코 다시 열지 않습니다. 인터뷰도, 명확화 라운드도, 다른 접근 방식의 제안도 없습니다. 상류에서 확정된 것이 무엇이든 그것이 입력이며, 스킬의 일은 오직 그것을 커밋으로 바꾸는 것입니다. 그것이 새로운 [에이전트](https://www.aihero.dev/ai-coding-dictionary/agent)에게 "이것을 만들어라"라고 입력하는 것과의 차이입니다. 그런 에이전트는 구현하면서 작업을 다시 설계하는 일이 많습니다.

## 언제 사용하는가

직접 `/implement`를 입력하여 호출하며, 에이전트가 스스로 사용하지는 않습니다. `disable-model-invocation: true`로 배포되므로, 다른 어떤 스킬도 이를 호출할 수 없습니다. [ask-matt](https://aihero.dev/skills-ask-matt)나 [to-tickets](https://aihero.dev/skills-to-tickets)가 "그다음 티켓마다 `/implement`"라고 말하는 곳은 어디든, 그것은 에이전트가 지시 없이 할 일이 아니라 사용자에게 하는 지시입니다.

작업이 현재 어디에 있는지가 이것이 올바른 스킬인지 결정합니다.

| 작업은… | 사용할 것 |
| --- | --- |
| 트래커의 티켓 | `/implement #42`, [세션](https://www.aihero.dev/ai-coding-dictionary/session)당 하나의 티켓, 티켓 사이에 컨텍스트 [비우기](https://www.aihero.dev/ai-coding-dictionary/clearing) |
| 아직 분할되지 않은 명세이며, 구현이 여러 세션에 걸침 | 먼저 [to-tickets](https://aihero.dev/skills-to-tickets), 그다음 티켓마다 `/implement` |
| 명세이며, 구현이 작음 | 명세에 대해 바로 `/implement` |
| 방금 나눈 대화 안에만 있으며, 여전히 작음 | 바로 거기, 같은 윈도우에서 `/implement` |
| 아직 어디에도 기록되지 않음 | [grill-with-docs](https://aihero.dev/skills-grill-with-docs), 또는 코드베이스가 없다면 [grill-me](https://aihero.dev/skills-grill-me) |
| 명세 없이 테스트 우선으로 원하는 하나의 구체적인 동작 | 바로 [tdd](https://aihero.dev/skills-tdd) |
| 이미 구현되었으며, 확인을 원함 | 바로 [code-review](https://aihero.dev/skills-code-review) |

같은 세션의 경우는 명시할 가치가 있습니다. 스킬 자신의 첫 줄이 그것을 다루지 않기 때문입니다. `SKILL.md`는 "명세나 티켓"이라고 말하는데, 이는 [모델](https://www.aihero.dev/ai-coding-dictionary/model)이 존재하지 않는 파일을 찾게 만듭니다. 계획이 스레드 안에만 있다면, 호출할 때 그렇다고 말하십시오.

## 사전 요구 사항

`implement`는 현재 있는 브랜치에 커밋합니다. 브랜치를 만들지 않으며, 묻지도 않습니다. 시작하기 전에 작업을 두고 싶은 브랜치에 있는지 확인하십시오.

티켓이 [to-tickets](https://aihero.dev/skills-to-tickets)에서 왔다면, [setup-matt-pocock-skills](https://aihero.dev/skills-setup-matt-pocock-skills)가 그 티켓이 있는 트래커를 구성했습니다. `code-review`는 마무리 단계에서 원래 명세를 찾기 위해 같은 구성을 읽습니다.

## 한 번의 실행이 하는 일

실행은 다섯 단계를 순서대로 거칩니다.

1. 티켓이나 명세를 읽고 시임을 파악합니다.
2. 사전에 합의된 시임에서, 한 번에 하나의 red-green 슬라이스씩 [tdd](https://aihero.dev/skills-tdd)를 진행합니다.
3. 자주 타입 검사를 하고, 진행하면서 단일 테스트 파일을 실행합니다.
4. 마지막에 전체 테스트 스위트를 한 번 실행합니다.
5. [code-review](https://aihero.dev/skills-code-review)를 실행한 다음, 현재 브랜치에 커밋합니다.

한 번의 실행은 하나의 티켓을 다룹니다. [to-tickets](https://aihero.dev/skills-to-tickets)가 만드는 티켓은 하나의 새로운 [컨텍스트 윈도우](https://www.aihero.dev/ai-coding-dictionary/context-window)에 맞는 크기의 트레이서 불릿 수직 슬라이스이므로, 의도된 리듬은 다음과 같습니다. 컨텍스트를 비우고, 하나의 티켓을 구현하고, 커밋하고, 다시 비웁니다. 각 티켓은 독립적이므로, 이전 티켓의 컨텍스트는 버려도 됩니다.

## 사전 합의된 시임

이 스킬의 핵심 개념은 **시임(seam)**, 즉 내부로 손을 뻗지 않고 동작을 관찰하는 공개 경계입니다. 테스트는 시임에 위치합니다. 어떤 코드도 존재하기 전에 시임이 합의되면, 테스트는 오래 유지되며, 그 아래의 구현을 테스트 변경 없이 다시 작성할 수 있습니다.

"사전 합의"라는 부분이 중요하며, 그것이 이 스킬의 가장 약한 지점이기도 합니다. `implement` 내부의 어떤 것도 시임을 합의하지 않습니다. 묻는 스킬은 `tdd`이며, 확인되지 않은 시임에서는 테스트 작성을 거부합니다. 따라서 실제로 합의는 상류의 명세에서, 또는 실행의 첫 대화에서 일어납니다. 어디에서도 일어나지 않으면, 실행은 "그냥 코드를 작성하라"가 되며 아무것도 경고하지 않습니다. 명세에서 시임을 명시하는 것이 그것을 막는 방법입니다.

## 자주 묻는 질문

**끝났는데, 티켓은 여전히 열려 있고 수락 기준도 여전히 체크되지 않았습니다.**

맞으며, 예상된 일입니다. `implement`에는 완료 단계가 없습니다. 커밋에서 끝나며 작업 항목은 결코 건드리지 않습니다. GitHub Issues와 로컬 마크다운 트래커에서 똑같으므로, 트래커 통합 문제가 아닙니다. 또한 `code-review`가 만든 발견 사항에 대해 조치하지 않으며, 원래 이슈의 `- [ ]` 상자도 체크하지 않습니다. 티켓을 종료하고 기준을 직접 맞추십시오. 이는 의존성 연쇄에서 가장 중요합니다. `to-tickets`는 전선을 차단하는 티켓이 모두 종료된 티켓으로 정의하기 때문입니다. 아무것도 종료되지 않으면, 아무것도 눈에 보이게 차단 해제되지 않습니다.

**모든 티켓을 한꺼번에 가리키거나, 여러 개를 병렬로 실행할 수 있습니까?**

`/implement`로는 안 됩니다. 한 번의 호출, 하나의 티켓입니다. 명세 전체를 한 번의 실행으로 하려면, 준비된 전선의 각 티켓을 자체 워크트리의 [서브에이전트](https://www.aihero.dev/ai-coding-dictionary/subagent)에게 주고 결과를 하나의 통합 브랜치에 병합하는 [implement-spec](https://aihero.dev/skills-implement-spec)을 사용하십시오. 하나의 체크아웃에서 여러 `/implement` 세션을 나란히 실행하는 것은 지원되지 않는 정도가 아니라 더 나쁩니다. 한 현장 보고서는 한 세션의 `git commit --amend`가 다른 세션의 커밋에 적용되고, 스태시가 `refs/stash`에서 사라지고, 커밋이 잘못된 브랜치에 반영된 일을, 세 개의 이슈에 걸친 한 오후 동안 모두 기술합니다. 세션들은 하나의 작업 디렉터리, 하나의 인덱스, 하나의 HEAD를 공유합니다. 사용자들은 git 워크트리로 이를 우회하지만, `refs/stash`는 워크트리 간에도 공유되므로, 워크트리만으로는 스태시 문제를 해결하지 못합니다.

**커밋 대신 풀 리퀘스트를 열 수 있습니까?**

내장되어 있지 않습니다. 현재 브랜치에 바로 커밋합니다. 여러 사람이 이것이 너무 성급하다고 느낍니다. 동작하는지 검증하기 전에 코드가 반영되기 때문입니다. 구성 플래그도 PR 모드도 없습니다. 사람들은 호출 시("브랜치에 커밋하고 PR을 열어라") 또는 스킬의 로컬 사본을 편집하여 이를 재정의합니다. 에이전트가 PR을 작성할 때는 [pr](https://aihero.dev/skills-pr)이 그 본문의 형태를 잡습니다.

**`code-review`가 제 변경 사항을 볼 수 없다고 합니다.**

`code-review`는 `git diff <fixed-point>...HEAD`를 리뷰하는데, 이는 스테이징된 변경과 작업 트리 변경을 제외합니다. `implement`는 커밋하기 전에 이를 실행하므로, 중간 커밋이 이미 존재하지 않는 한 그 diff에는 리뷰할 것이 없습니다. 여러 사람이 이를 보고했으며 양쪽 모두에서 수정되지 않았습니다. 먼저 커밋한 다음, 분기한 지점을 기준으로 리뷰하십시오.

별개로, 일부 사람들은 실행 안에서 리뷰하는 것을 전혀 원하지 않습니다. 방금 작성한 코드를 리뷰하는 에이전트는 자신의 해결책에 편향되기 때문입니다. 새 세션에서 고정된 시점을 기준으로 [code-review](https://aihero.dev/skills-code-review)를 실행하는 것은 유효한 대안입니다. 같은 편향이 그 스킬이 두 축을 별도의 서브에이전트에서 실행하는 이유입니다.

**티켓 하나가 150k 토큰을 소비했습니다. 잘못 사용하고 있는 것입니까?**

아마 아닐 것입니다. 티켓이 너무 클 가능성이 더 큽니다. 실행은 코드베이스 탐색, 시임마다의 red-green 루프, 전체 스위트, 리뷰를 수행하므로, 사소하지 않은 티켓이 100k [토큰](https://www.aihero.dev/ai-coding-dictionary/token)을 넘는 것은 무언가 망가졌다는 신호가 아니라 정상입니다. 해결책은 상류에 있습니다. [to-tickets](https://aihero.dev/skills-to-tickets)에서 각 티켓이 하나의 새로운 윈도우에 맞도록 티켓의 크기를 적절히 정하십시오. 하나의 티켓이 계속 넘어간다면, [노력(effort)](https://www.aihero.dev/ai-coding-dictionary/effort) 수준을 높이는 대신 그것을 나누십시오.

**새 세션에서 `/implement #2`가 완전히 관련 없는 작업을 했습니다.**

에이전트가 `#2`를 구성된 트래커가 아니라 컨텍스트의 다른 번호 목록(할 일 파일이나 체크리스트 등)에 대해 해석한 것입니다. `implement`는 이제 전달된 참조를 이슈 트래커에서 가져와 시작하기 전에 그 제목을 명시하며, 참조가 모호하면 묻습니다. 그 제목이 의도한 티켓과 일치하는지 확인하십시오. 이슈 URL이나 `owner/repo#2`를 전달하면 모호함이 완전히 사라집니다.

## 제대로 동작하고 있다면

- 세션이 무엇을 만들지 묻는 대신, 티켓이나 명세를 읽고 무엇을 구현할지 다시 진술하며 시작합니다.
- diff에 테스트가 나타나는 것만이 아니라, 기록에서 실제 `tdd` Skill 도구 호출을 볼 수 있습니다.
- 실행 중에 타입 검사와 단일 테스트 파일이 반복적으로 실행되며, 전체 스위트는 끝 무렵에 한 번 실행됩니다.
- 계속하라고 지시하지 않아도 실행이 현재 브랜치의 커밋에 도달합니다.
- diff가 하나의 티켓 분량의 변경입니다. 여러 티켓을 함께 쓸어 담은 것이 아니라, 모든 계층을 관통하는 하나의 수직 슬라이스입니다.

## 어디에 위치하는가

`implement`는 주 연쇄의 구현 단계입니다.

```txt
grill-with-docs → to-spec → to-tickets → implement → code-review → retro
```

이웃은 이 스킬이 소비하는 티켓을 만들고 그 순서를 정하는 차단 관계를 선언하는 [to-tickets](https://aihero.dev/skills-to-tickets), 각 시임에서 내부적으로 진행하는 [tdd](https://aihero.dev/skills-tdd), 그리고 커밋하기 전에 실행하는 [code-review](https://aihero.dev/skills-code-review)입니다. 계획 스킬의 하류에 위치하며 그것들을 신뢰합니다. 넘겨받은 것의 형태를 다시 검증하지 않으므로, 잘못 구조화된 지도나 수평으로 계층화된 티켓은 작성된 그대로 구현됩니다.

그 신뢰가 [wayfinder](https://aihero.dev/skills-wayfinder)가 지도를 곧바로 `implement`로 넘기지 않고 [to-spec](https://aihero.dev/skills-to-spec)에서 연쇄에 합류하는 이유입니다. 작업이 작은 것으로 밝혀졌을 때만 지도에서 곧바로 `implement`로 가십시오.

어떤 흐름에 있는지 확실하지 않을 때는 [ask-matt](https://aihero.dev/skills-ask-matt)가 세트 전체에 대한 라우터입니다.
