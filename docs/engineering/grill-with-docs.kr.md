## 하는 일

`grill-with-docs`는 사용자와 [에이전트](https://www.aihero.dev/ai-coding-dictionary/agent)가 계획이나 설계에 대해 하나의 이해를 공유할 때까지 사용자를 인터뷰하며, 그러는 동안 어휘와 어려운 결정을 저장소에 기록합니다. [grill-me](https://aihero.dev/skills-grill-me)가 실행하는 것과 같은 인터뷰(한 라운드의 질문, 기다림, 그다음 라운드)를 코드베이스를 향해 실행하는 것입니다.

이 스킬은 **[상태를 유지합니다(stateful)](https://www.aihero.dev/ai-coding-dictionary/stateful)**. 다른 모든 그릴링 스킬은 [세션](https://www.aihero.dev/ai-coding-dictionary/session)을 사용자의 머릿속에 남기지만, 이 스킬은 디스크에 파일을 남깁니다. 용어가 확정되면, 스킬은 마지막에 일괄로가 아니라 즉시 그것을 `GLOSSARY.md`에 작성합니다. 결정이 세 가지 관문을 통과하면, 스킬은 그것을 ADR로 작성합니다. 그것이 차이의 전부이며, 사람들이 이 스킬에서 겪는 문제의 대부분도 그것 때문에 생깁니다. 산출물은 실제 저장소의 실제 파일이므로, 기대했을 때 없을 수도 있고, 여러 사람이 작성하면 어긋날 수도 있습니다.

## 언제 사용하는가

`/grill-with-docs`를 입력하여 호출하며, 에이전트가 스스로 사용하지는 않습니다.

저장소에서 변경을 시작할 때, 계획이 아직 모호하고 그것을 부르는 말이 아직 정해지지 않았을 때 사용하십시오. 단일 세션용 도구입니다. 어떤 그릴링 스킬이 필요한지는 눈앞에 무엇이 있는지에 따라 다릅니다.

| 가지고 있는 것 | 사용할 것 |
| --- | --- |
| 작업 디렉터리에서 전혀 작업하고 있지 않음 | [grill-me](https://aihero.dev/skills-grill-me) |
| 저장소, 그리고 한 세션에 해결할 수 있는 변경 | `grill-with-docs` |
| 한 세션에 담기에 너무 큰 작업(그린필드 구축, 대규모 기능) | [wayfinder](https://aihero.dev/skills-wayfinder) |
| 도메인 문서가 전혀 없고 특정한 기능을 염두에 두지 않은 저장소 | 변경이 아니라 저장소를 겨냥한 `grill-with-docs` |
| 다른 사람의 머릿속에 있는 지식에 막힌 결정 | [to-questionnaire](https://aihero.dev/skills-to-questionnaire) |

wayfinder와의 구분은 세션 수로 결정됩니다. 단일 세션 계획에는 `/grill-with-docs`, 다중 세션 계획에는 `/wayfinder`입니다.

## 사전 요구 사항

스킬은 저장소에 내용을 작성하므로, 작성해도 안전한 곳에 있어야 합니다. 확정된 용어는 루트의 `GLOSSARY.md` 용어집으로 가거나, 루트의 `GLOSSARY-MAP.md`가 저장소를 다중 컨텍스트로 표시한다면 해당 컨텍스트의 `GLOSSARY.md`로 갑니다. 결정은 `docs/adr/`로 갑니다. 스킬은 둘 다 필요할 때만 생성합니다. 첫 번째 용어나 결정이 확정될 때까지는 아무것도 존재하지 않으므로, 미리 설정할 것이 없습니다.

두 개의 다른 스킬도 있어야 합니다. 자신의 `SKILL.md`는 그것들에 위임하는 한 줄이기 때문입니다. [grilling](https://aihero.dev/skills-grilling)이 인터뷰를 제공하고, [domain-modeling](https://aihero.dev/skills-domain-modeling)이 기록을 제공합니다. `grill-with-docs`만 설치하면 동작하지 않는 스킬을 얻게 됩니다.

## 기록

세션에서는 세 가지가 나오며, 그것들은 동등하지 않습니다.

| 확정된 것 | 놓이는 곳 |
| --- | --- |
| 용어: 무언가를 부르는 프로젝트 고유의 단어 | 확정되는 순간 즉석에서 `GLOSSARY.md` |
| 되돌리기 어렵고, 맥락 없이는 놀라우며, 실제 트레이드오프인 결정 | `docs/adr/` 아래의 ADR |
| 결정한 그 밖의 모든 것 | 대화, 그리고 그 외에는 어디에도 없음 |

세 번째 행이 사람들을 당황하게 만드는 것입니다. `GLOSSARY.md`는 용어집일 뿐입니다. 구현 세부 사항도, [명세](https://www.aihero.dev/ai-coding-dictionary/spec)도, 메모도 담지 않습니다. ADR은 세 가지 조건을 동시에 필요로 하므로, 대부분의 결정은 해당하지 않으며 대부분의 세션은 ADR을 만들지 않습니다. 더 날카로운 용어집과 ADR 0개를 낳은 세션은 설계대로 동작한 것이지만, 합의한 것의 대부분이 합의한 그 [컨텍스트 윈도우](https://www.aihero.dev/ai-coding-dictionary/context-window) 안에만 존재한다는 의미입니다. 그 대화를 [비우지(clear)](https://www.aihero.dev/ai-coding-dictionary/clearing) 말고 [to-spec](https://aihero.dev/skills-to-spec)에 넘기십시오.

용어집이 주된 출력입니다. 이 스킬은 도메인 언어, 즉 한 번 합의하여 사용자, 에이전트, 동료가 다시 알아낼 필요가 없는 프로젝트 고유의 단어를 구축합니다. 이것이 에이전트의 성능을 개선한다는 데 모든 사람이 동의하는 것은 아닙니다. 가장 강력한 반론은 용어와 그것을 평이한 영어로 풀어 쓴 것이 [모델](https://www.aihero.dev/ai-coding-dictionary/model)에게서 같은 결과를 얻으며, 어휘는 주로 그것을 공유하는 사람들 사이의 소통을 짧게 만든다는 것입니다. 그 관점에서도 용어집은 여전히 가치가 있지만, 그 가치는 사람에게 돌아갑니다.

## 자주 묻는 질문

**이것을 사용해야 합니까, `/wayfinder`를 사용해야 합니까?**
범위가 결정합니다. 한 세션에 해결할 수 있는 모든 것에는 이것을 사용하고, 작업이 한 세션에 담기에 너무 클 때는 [wayfinder](https://aihero.dev/skills-wayfinder)를 사용하십시오. wayfinder는 먼저 작업을 결정 [티켓](https://www.aihero.dev/ai-coding-dictionary/ticket)의 지도로 그립니다. wayfinder는 더 느리고 밀도가 높으며, 범위가 잘 정해진 기능에 그것을 사용하는 것이 흔한 실수입니다. 이 스킬을 대체하지 않으며, 지도에서 그릴링 세션에 맞는 부분에 대해 그릴링 세션을 시작할 수 있습니다.

**실행되었지만, `GLOSSARY.md`도 ADR도 나타나지 않았습니다.**
두 가지 알려진 원인이 있습니다. 첫째는 해당하는 것이 없었던 경우입니다. ADR은 세 가지 관문을 모두 필요로 하며, 새로운 어휘가 없는 변경에 관한 세션에는 작성할 것이 없습니다. 둘째는 실제 버그입니다. 스킬이 다른 조율 계층(명세 주도 개발 래퍼, 다중 에이전트 프레임워크, 다른 사람의 파이프라인의 한 단계로 이를 호출하는 규칙) 안에서 실행될 때, 사용자들은 인터뷰는 여전히 실행되지만 파일을 작성하는 절반이 조용히 일어나지 않는다고 보고합니다. 버그는 제출되었으며 수정되지 않았습니다. 그런 설정이라면, 세션의 출력을 신뢰하기 전에 작업 디렉터리를 확인하십시오.

**권장 답변 없이 모든 것을 한꺼번에 물었고, `GLOSSARY.md`는 언급하지도 않았습니다.**
그것은 스킬이 두 의존성을 로드하지 못한 것입니다. `SKILL.md`가 한 줄짜리 위임이므로, [grilling](https://aihero.dev/skills-grilling)과 [domain-modeling](https://aihero.dev/skills-domain-modeling)을 가져오지 않은 에이전트는 그릴링이 무엇을 의미하는지 추측하며, 구조 없이 모든 질문을 한꺼번에 받게 됩니다. 부분적인 로드는 더 혼란스럽습니다. `grilling`은 로드되고 `domain-modeling`은 로드되지 않으면, 기록 없는 좋은 인터뷰를 얻게 됩니다. 얼마나 자주 일어나는지는 모델과 [노력(effort)](https://www.aihero.dev/ai-coding-dictionary/effort) 수준에 따라 다르며, 이 스킬에서 가장 많이 보고되는 문제입니다. 의심된다면, 에이전트에게 어떤 스킬을 로드했는지 직접 물어보십시오.

**제 다른 결정들은 모두 어디로 갔습니까?**
대화 안으로만 갔습니다. 이것이 이 스킬에 대한 가장 심각한 미해결 불만입니다. 용어집은 명세가 아니고, 대부분의 답은 ADR을 받을 자격이 없으며, 확정된 각 답을 명세, 티켓, 테스트에 연결하는 기록이 없습니다. 이후 단계는 정밀한 답(순서 보장, 부정적 요구 사항, 수치 기본값)을 더 약한 산문으로 누그러뜨리며, 결과는 결정한 것을 빠뜨린 채 완전해 보일 수 있습니다. 현재로서는 세션을 유지하고 곧바로 [to-spec](https://aihero.dev/skills-to-spec)에 넣으십시오. 그런 다음 명세가 답을 담았다고 가정하지 말고, 자신의 답과 대조하며 명세를 다시 읽으십시오.

**문서가 전혀 없는 기존 저장소를 가리킬 수 있습니까?**
예. ADR도, 도메인 언어도, 설계 원칙도 없는 코드베이스에 맞는 스킬입니다. 호출하고 "내 저장소를 문서화하는 것을 도와줘"라고 말하십시오. 사용자들은 `GLOSSARY.md`를 구축하거나 고치기 위해 종종 이를 [improve-codebase-architecture](https://aihero.dev/skills-improve-codebase-architecture)와 짝지어 사용합니다. 방향을 잡아 줄 것으로 예상하십시오. 코드를 읽고 발견한 것에 대해 묻으며, 코드베이스에 이미 있는 단어 중 어느 것이 올바른지는 사용자가 결정합니다.

**세션이 끝나면 무엇을 해야 합니까?**
스킬의 마무리 메시지는 종종 열려 있는데, 이는 알려진 문제입니다. 주 흐름에서의 답은 같은 대화에서의 [to-spec](https://aihero.dev/skills-to-spec)입니다. 변경이 즉시 구현할 만큼 작다면, 대신 바로 [implement](https://aihero.dev/skills-implement)로 가십시오.

**왜 그런 이름입니까?**
아무도 그 이름에 만족하지 않습니다. 동작을 더 정확하게 기술하는 `grill-domain-model`로 이름을 바꾸자는 열린 제안이 있습니다. 진전은 없습니다. 이름 변경이 반영된다면, 문서 페이지도 함께 이동하고 URL이 바뀝니다.

## 제대로 동작하고 있다면

- `GLOSSARY.md`가 마지막에 한 덩어리로 나타나는 것이 아니라, 세션 *도중에* 용어 하나하나 바뀝니다.
- 용어집이 순수한 어휘(간결한 정의를 가진 프로젝트의 단어)로 읽히며, 구현 세부 사항이나 명세 같은 산문을 담지 않습니다.
- 코드베이스가 답할 수 있는 질문은 사용자에게 묻지 않고 코드베이스를 읽어 답합니다.
- ADR이 거의 없거나 전혀 없으며, 생긴 ADR은 다시 논쟁해야 한다면 짜증이 날 결정입니다.
- 기존 용어집이 다르게 정의하고 있기 때문에 사용자가 쓴 단어에 이의를 제기합니다.

## 어디에 위치하는가

`grill-with-docs`는 주 구현 연쇄의 머리입니다.

```txt
grill-with-docs → to-spec → to-tickets → implement → code-review → retro
```

무엇이든 명세로 기록되기 전에 옵니다. [to-spec](https://aihero.dev/skills-to-spec)이 다시 인터뷰하지 않고 종합하는 공유된 이해와 확정된 어휘를 만들어 냅니다. 가까운 이웃은 저장소도 파일도 없는 같은 인터뷰인 [grill-me](https://aihero.dev/skills-grill-me), 그리고 이 스킬이 진행하는 용어집과 ADR 규율인 [domain-modeling](https://aihero.dev/skills-domain-modeling)입니다. 둘 다 인터뷰에 [grilling](https://aihero.dev/skills-grilling) 기본 요소를 사용합니다. 그 상류에서는 [wayfinder](https://aihero.dev/skills-wayfinder)가 한 세션에 담기에 너무 큰 작업을 그리며, 지도의 일부를 다시 이 스킬로 넘길 수 있습니다. 어떤 스킬이나 흐름이 맞는지 확실하지 않다면, [ask-matt](https://aihero.dev/skills-ask-matt)가 안내합니다.
