<p>
  <a href="https://www.aihero.dev/s/skills-newsletter">
    <picture>
      <source media="(prefers-color-scheme: dark)" srcset="https://res.cloudinary.com/total-typescript/image/upload/v1777382277/skills-repo-dark_2x.png">
      <source media="(prefers-color-scheme: light)" srcset="https://res.cloudinary.com/total-typescript/image/upload/v1777382277/skill-repo-light_2x.png">
      <img alt="Skills" src="https://res.cloudinary.com/total-typescript/image/upload/v1777382277/skill-repo-light_2x.png" width="369">
    </picture>
  </a>
</p>

# 진짜 엔지니어를 위한 스킬

[![skills.sh](https://skills.sh/b/mattpocock/skills)](https://skills.sh/mattpocock/skills)

바이브 코딩(vibe coding)이 아닌, 진짜 엔지니어링을 위해 제가 매일 사용하는 에이전트 스킬입니다.

실제 애플리케이션을 개발하는 것은 어렵습니다. GSD, BMAD, Spec-Kit과 같은 접근 방식은 프로세스를 소유함으로써 도움을 주려고 합니다. 그러나 그렇게 하는 과정에서 사용자의 통제권을 빼앗고, 프로세스 내의 버그를 해결하기 어렵게 만듭니다.

이 스킬들은 작고, 적용하기 쉬우며, 조합 가능하도록 설계되었습니다. 어떤 모델에서도 동작합니다. 수십 년간의 엔지니어링 경험을 기반으로 합니다. 이리저리 고쳐 보십시오. 자신만의 것으로 만드십시오. 즐기십시오.

이 스킬들의 변경 사항과 제가 새로 만드는 스킬에 대한 소식을 계속 받아 보고 싶다면, 약 60,000명의 다른 개발자와 함께 뉴스레터를 구독할 수 있습니다.

[뉴스레터 구독하기](https://www.aihero.dev/s/skills-newsletter)

## 설치 (30초 설정)

플러그인은 스스로 업데이트됩니다. [skills.sh](https://skills.sh/mattpocock/skills)는 편집 가능한 파일을 프로젝트에 복사하며, 사용자가 직접 업데이트해야 합니다. 에이전트마다 하나를 선택하십시오. 둘 다 설치하면 모든 스킬이 두 개씩 생기기 때문입니다.

### 1. 스킬 받기

<details>
<summary><strong>Claude Code</strong></summary>

```bash
claude plugin install mattpocock-skills@claude-plugins-official
```

기본적으로 스스로 업데이트됩니다.

</details>

<details>
<summary><strong>Codex</strong></summary>

```bash
codex plugin marketplace add mattpocock/skills
codex plugin add mattpocock-skills@mattpocock
```

시작 시 스스로 업데이트됩니다.

</details>

<details>
<summary><strong>GitHub Copilot</strong> (CLI 및 VS Code)</summary>

```bash
copilot plugin marketplace add mattpocock/skills
copilot plugin install mattpocock-skills@mattpocock
```

그런 다음, 한 번만 `~/.copilot/settings.json`에 다음을 추가합니다.

```json
{
  "extraKnownMarketplaces": {
    "mattpocock": { "source": { "source": "github", "repo": "mattpocock/skills" }, "autoUpdate": true }
  }
}
```

VS Code에서는 **Chat: Install Plugin From Source**를 실행하고 `https://github.com/mattpocock/skills`를 입력합니다. 매일 업데이트됩니다.

</details>

<details>
<summary><strong>Gemini CLI</strong> (수동 업데이트)</summary>

```bash
gemini skills install https://github.com/mattpocock/skills.git --path skills/engineering
gemini skills install https://github.com/mattpocock/skills.git --path skills/productivity
```

업데이트하려면 두 명령을 모두 다시 실행하십시오.

</details>

<details>
<summary><strong>그 외 모든 에이전트, 또는 편집 가능한 파일</strong> (수동 업데이트)</summary>

```bash
npx skills@latest add mattpocock/skills -a <agent>  # cursor, opencode, devin, windsurf, amp, pi; omit -a to choose
```

설치 도구가 어떤 스킬을 가져올지 물으면 `setup-matt-pocock-skills`를 포함하십시오. 업데이트하려면 `npx skills@latest update`를 실행하고, 새 스킬을 가져오려면 `add`를 다시 실행하십시오.

</details>

### 2. `/setup-matt-pocock-skills` 실행

에이전트에서 저장소마다 한 번씩 실행하십시오. 이 스킬은 다음을 수행합니다.

- 사용할 이슈 트래커(GitHub, GitLab, 로컬 파일, 또는 사용자가 설명하는 그 밖의 무엇이든)를 묻습니다
- 트리아지할 때 티켓에 적용하는 라벨을 묻습니다(`/triage`는 라벨을 사용합니다)
- 생성되는 문서를 저장할 위치를 묻습니다

### 3. 짠, 준비가 끝났습니다.

## 이 스킬들이 존재하는 이유

저는 Claude Code, Codex 및 기타 코딩 에이전트에서 흔히 볼 수 있는 실패 유형을 해결하기 위한 방법으로 이 스킬들을 만들었습니다.

### #1: 에이전트가 내가 원하는 것을 하지 않았다

> "자신이 원하는 것을 정확히 아는 사람은 아무도 없다"
>
> David Thomas & Andrew Hunt, [The Pragmatic Programmer](https://www.amazon.co.uk/Pragmatic-Programmer-Anniversary-Journey-Mastery/dp/B0833F1T3V)

**문제**: 소프트웨어 개발에서 가장 흔한 실패 유형은 정렬 불일치(misalignment)입니다. 개발자가 내가 원하는 것을 안다고 생각합니다. 그러다 그들이 만든 것을 보고 나서야, 그들이 나를 전혀 이해하지 못했다는 것을 깨닫게 됩니다.

AI 시대에도 이는 마찬가지입니다. 사용자와 에이전트 사이에는 의사소통의 간극이 있습니다. 이에 대한 해결책은 **그릴링 세션(grilling session)**입니다. 즉, 만들고자 하는 것에 대해 에이전트가 사용자에게 상세한 질문을 하도록 하는 것입니다.

**해결책**은 다음을 사용하는 것입니다.

- [`/grill-me`](./skills/productivity/grill-me/SKILL.md): 코드 외의 용도
- [`/grill-with-docs`](./skills/engineering/grill-with-docs/SKILL.md): [`/grill-me`](./skills/productivity/grill-me/SKILL.md)와 같지만, 추가 기능이 더해짐(아래 참조)

이 스킬들은 가장 인기 있는 스킬입니다. 시작하기 전에 에이전트와 정렬을 맞추고, 만들고자 하는 변경에 대해 깊이 생각하도록 도와줍니다. 변경을 하고자 할 때마다 _매번_ 사용하십시오.

### #2: 에이전트가 지나치게 장황하다

> 유비쿼터스 언어를 사용하면, 개발자들 간의 대화와 코드의 표현이 모두 동일한 도메인 모델에서 파생된다.
>
> Eric Evans, [Domain-Driven-Design](https://www.amazon.co.uk/Domain-Driven-Design-Tackling-Complexity-Software/dp/0321125215)

**문제**: 프로젝트를 시작할 때, 개발자와 그들이 소프트웨어를 만들어 주는 대상(도메인 전문가)은 대개 서로 다른 언어를 사용합니다.

저는 에이전트와의 관계에서도 같은 긴장을 느꼈습니다. 에이전트는 대개 프로젝트에 투입되어 진행하면서 전문 용어를 파악하도록 요구받습니다. 그래서 한 단어면 될 것을 스무 단어로 표현합니다.

이에 대한 **해결책**은 공유 언어입니다. 이는 에이전트가 프로젝트에서 사용되는 전문 용어를 해독하도록 돕는 문서입니다.

<details>
<summary>
예시
</summary>

다음은 제 `course-video-manager` 저장소의 예시 [용어집](https://github.com/mattpocock/course-video-manager/blob/076a5a7a182db0fe1e62971dd7a68bcadf010f1c/CONTEXT.md)입니다(스킬이 규칙의 이름을 변경하기 전이므로, 고정된 해당 커밋에서는 여전히 `CONTEXT.md`라는 이름입니다). 어느 쪽이 더 읽기 쉽습니까?

- **이전**: "강좌의 섹션 내부에 있는 레슨이 '실제'가 될 때(즉, 파일 시스템에 자리를 부여받을 때) 문제가 있습니다"
- **이후**: "구체화 연쇄(materialization cascade)에 문제가 있습니다"

이러한 간결함은 세션을 거듭할수록 효과를 발휘합니다.

</details>

이 기능은 [`/grill-with-docs`](./skills/engineering/grill-with-docs/SKILL.md)에 내장되어 있습니다. 그릴링 세션이지만, AI와 공유 언어를 구축하고 설명하기 어려운 결정을 ADR에 문서화하도록 도와줍니다.

이것이 얼마나 강력한지 설명하기는 어렵습니다. 이 저장소에서 가장 멋진 단일 기법일지도 모릅니다. 직접 시도해 보십시오.

> [!TIP]
> 공유 언어에는 장황함을 줄이는 것 외에도 많은 이점이 있습니다.
>
> - 공유 언어를 사용하여 **변수, 함수, 파일의 이름이 일관되게 지어집니다**
> - 그 결과, 에이전트가 **코드베이스를 탐색하기가 더 쉬워집니다**
> - 에이전트는 더 간결한 언어를 사용할 수 있으므로 **사고에 소비하는 토큰도 줄어듭니다**

### #3: 코드가 동작하지 않는다

> "항상 작고 신중한 단계를 밟아라. 피드백의 속도가 곧 당신의 속도 제한이다. 너무 큰 작업은 절대 맡지 마라."
>
> David Thomas & Andrew Hunt, [The Pragmatic Programmer](https://www.amazon.co.uk/Pragmatic-Programmer-Anniversary-Journey-Mastery/dp/B0833F1T3V)

**문제**: 사용자와 에이전트가 무엇을 만들지에 대해 정렬되었다고 가정해 봅시다. 그런데도 에이전트가 _여전히_ 형편없는 결과물을 만들어 낸다면 어떻게 될까요?

이제 피드백 루프를 살펴볼 때입니다. 자신이 생성한 코드가 실제로 어떻게 실행되는지에 대한 피드백이 없으면, 에이전트는 눈을 가린 채 비행하는 것과 같습니다.

**해결책**: 일반적인 피드백 루프 묶음이 필요합니다. 정적 타입, 브라우저 접근, 자동화된 테스트입니다.

자동화된 테스트의 경우, red-green-refactor 루프가 매우 중요합니다. 이는 에이전트가 먼저 실패하는 테스트를 작성한 다음, 그 테스트를 통과하도록 수정하는 방식입니다. 이를 통해 에이전트에게 일관된 수준의 피드백을 제공할 수 있으며, 그 결과 훨씬 더 나은 코드가 만들어집니다.

저는 어떤 프로젝트에도 끼워 넣을 수 있는 **[`/tdd`](./skills/engineering/tdd/SKILL.md) 스킬**을 만들었습니다. 이 스킬은 red-green-refactor를 장려하며, 좋은 테스트와 나쁜 테스트가 무엇인지에 대해 에이전트에게 충분한 지침을 제공합니다.

디버깅을 위해서는 **[`/diagnosing-bugs`](./skills/engineering/diagnosing-bugs/SKILL.md)** 스킬도 만들었습니다. 이 스킬은 최선의 디버깅 관행을 단계별로 관문이 있는 규율 있는 루프로 감쌉니다.

### #4: 우리는 진흙 덩어리를 만들었다

> "시스템의 설계에 _매일_ 투자하라."
>
> Kent Beck, [Extreme Programming Explained](https://www.amazon.co.uk/Extreme-Programming-Explained-Embrace-Change/dp/0321278658)

> "최고의 모듈은 깊다. 단순한 인터페이스를 통해 많은 기능에 접근할 수 있게 해 준다."
>
> John Ousterhout, [A Philosophy Of Software Design](https://www.amazon.co.uk/Philosophy-Software-Design-2nd/dp/173210221X)

**문제**: 에이전트로 만든 대부분의 앱은 복잡하고 변경하기 어렵습니다. 에이전트는 코딩 속도를 급격히 높일 수 있기 때문에, 소프트웨어 엔트로피도 가속화합니다. 코드베이스는 전례 없는 속도로 복잡해집니다.

이에 대한 **해결책**은 AI 기반 개발에 대한 급진적인 새로운 접근 방식, 즉 코드의 설계에 관심을 기울이는 것입니다.

이는 이 스킬들의 모든 계층에 내장되어 있습니다.

- [`/to-spec`](./skills/engineering/to-spec/SKILL.md)은 명세를 작성하기 전에 어떤 모듈을 수정하는지 사용자에게 질문합니다

그리고 결정적으로, [`/improve-codebase-architecture`](./skills/engineering/improve-codebase-architecture/SKILL.md)는 코드베이스에서 심화(deepening) 기회를 조사하고 후보를 제시합니다. 며칠에 한 번씩 코드베이스에 실행해 보기를 권장합니다. 이 스킬은 구조 작업이 아니라 조사입니다. 정말 오래된 코드베이스에서도 실제 후보를 찾아내겠지만, 진흙을 대신 풀어 주지는 않습니다.

### 요약

소프트웨어 엔지니어링의 기본기는 그 어느 때보다 중요합니다. 이 스킬들은 이러한 기본기를 반복 가능한 관행으로 압축하여, 여러분이 경력 최고의 앱을 출시할 수 있도록 돕기 위한 저의 최선의 노력입니다. 즐기십시오.

## 참조

이 스킬들은 하나의 축, 즉 누가 호출할 수 있는가에 따라 나뉩니다. **사용자 호출(User-invoked)** 스킬은 사용자가 직접 입력할 때만(예: `/grill-me`) 도달할 수 있으며, 그 역할은 조율하는 것입니다. **모델 호출(Model-invoked)** 스킬은 사용자가 호출할 수도 _있고_, 작업이 적합할 때 에이전트가 자동으로 사용할 수도 있으며, 재사용 가능한 규율을 담고 있습니다. 사용자 호출 스킬은 모델 호출 스킬을 호출할 수 있지만, 다른 사용자 호출 스킬은 결코 호출할 수 없습니다.

### 엔지니어링

코드 작업을 위해 매일 사용하는 스킬입니다.

**사용자 호출**

- **[ask-matt](./skills/engineering/ask-matt/SKILL.md)**: 상황에 맞는 스킬이나 흐름이 무엇인지 묻습니다. 이 저장소의 사용자 호출 스킬에 대한 라우터입니다.
- **[grill-with-docs](./skills/engineering/grill-with-docs/SKILL.md)**: 프로젝트의 도메인 모델도 함께 구축하는 그릴링 세션으로, 용어를 정제하고 `GLOSSARY.md`와 ADR을 즉석에서 업데이트합니다.
- **[triage](./skills/engineering/triage/SKILL.md)**: 트리아지 역할의 상태 기계를 따라 이슈를 이동시킵니다.
- **[improve-codebase-architecture](./skills/engineering/improve-codebase-architecture/SKILL.md)**: 코드베이스에서 심화 기회를 탐색하여 시각적인 HTML 보고서로 제시한 다음, 사용자가 선택한 항목에 대해 그릴링을 진행합니다.
- **[setup-matt-pocock-skills](./skills/engineering/setup-matt-pocock-skills/SKILL.md)**: 엔지니어링 스킬을 위해 저장소를 구성합니다(이슈 트래커, 트리아지 라벨, 도메인 문서 레이아웃). 다른 엔지니어링 스킬을 사용하기 전에 저장소마다 한 번 실행하십시오.
- **[to-spec](./skills/engineering/to-spec/SKILL.md)**: 현재 대화를 명세로 변환하여 이슈 트래커에 게시합니다. 인터뷰 없이, 이미 논의한 내용을 종합할 뿐입니다.
- **[to-tickets](./skills/engineering/to-tickets/SKILL.md)**: 어떤 계획, 명세, 대화든 트레이서 불릿(tracer-bullet) 티켓 세트로 분해합니다. 각 티켓은 자신의 차단 관계를 선언하며, 로컬 파일의 텍스트로 작성되거나 실제 트래커의 네이티브 차단 링크로 작성됩니다.
- **[implement](./skills/engineering/implement/SKILL.md)**: 명세나 티켓 세트가 기술하는 작업을 구현합니다. 사전에 합의된 시임(seam)에서 `/tdd`를 진행하고, 커밋하기 전에 `/code-review`로 마무리합니다.
- **[implement-spec](./skills/engineering/implement-spec/SKILL.md)**: 하나의 통합 브랜치에서 명세 전체를 구현합니다. 티켓을 작업 그래프로 다루며, 최대 동시성을 위해 준비된 전선(frontier) 전반에 걸쳐 구현자 서브에이전트를 실행한 다음, `/code-review`로 마무리합니다.
- **[wayfinder](./skills/engineering/wayfinder/SKILL.md)**: 하나의 에이전트 세션이 담을 수 있는 것보다 큰 대규모 작업을, 이슈 트래커 위의 결정 티켓으로 이루어진 공유 지도로 계획하고, 목적지로 가는 길이 명확해질 때까지 하나씩 해결합니다.
- **[retro](./skills/engineering/retro/SKILL.md)**: 세션이 끝난 후 코딩 에이전트의 환경(탐색, 자동화된 검사, 코딩 표준, 지침 파일, 도구)에 대한 개선 사항을 가장 심각한 것부터 제안합니다.

**모델 호출**

- **[prototype](./skills/engineering/prototype/SKILL.md)**: 설계 질문에 답하기 위한 일회용 프로토타입을 만듭니다. 상태/로직 질문을 위한 공유 가능한 단일 HTML 파일이거나, 하나의 라우트에서 전환할 수 있는 근본적으로 다른 여러 UI 변형입니다.
- **[diagnosing-bugs](./skills/engineering/diagnosing-bugs/SKILL.md)**: 어려운 버그와 성능 회귀를 위한 규율 있는 진단 루프입니다. 이 버그에서 red가 되는 피드백 루프 구축 → 최소화 → 가설 수립 → 계측 → 수정 → 회귀 테스트.
- **[research](./skills/engineering/research/SKILL.md)**: 신뢰도 높은 1차 자료를 바탕으로 질문을 조사하고, 그 결과를 출처가 명시된 마크다운 파일로 저장소에 기록합니다. 백그라운드 에이전트로 실행됩니다.
- **[tdd](./skills/engineering/tdd/SKILL.md)**: red-green-refactor 루프를 사용하는 테스트 주도 개발입니다. 한 번에 하나의 수직 슬라이스씩 기능을 구축하거나 버그를 수정합니다.
- **[domain-modeling](./skills/engineering/domain-modeling/SKILL.md)**: 프로젝트의 도메인 모델을 능동적으로 구축하고 정제합니다. 용어집을 기준으로 용어에 이의를 제기하고, 엣지 케이스 시나리오로 스트레스 테스트를 하며, `GLOSSARY.md`와 ADR을 즉석에서 업데이트합니다.
- **[codebase-design](./skills/engineering/codebase-design/SKILL.md)**: 깊은 모듈(deep module)을 설계하기 위한 공유 규율과 어휘입니다. 작은 인터페이스 뒤에 많은 동작을 두고, 깔끔한 시임에 배치하며, 해당 인터페이스를 통해 테스트할 수 있도록 합니다.
- **[code-review](./skills/engineering/code-review/SKILL.md)**: 고정된 시점 이후의 diff에 대한 두 축의 리뷰입니다. **Standards**(저장소의 코딩 표준과 Fowler 코드 스멜 기준선을 따르는가?)와 **Spec**(원래의 이슈/명세를 충실하게 구현하는가?)이며, 서로 오염시키지 않도록 병렬 서브에이전트로 실행됩니다.
- **[pr](./skills/engineering/pr/SKILL.md)**: 풀 리퀘스트 본문이 갖추어야 할 형태입니다. 변경 사항을 명확하게 보여 주는 가장 작은 시각 자료로서의 요약, 동작한다는 전후 증거, 그리고 병합 위험도 판단(일방향 문 또는 양방향 문, 그리고 영향 범위)입니다.
- **[wizard](./skills/engineering/wizard/SKILL.md)**: 사람만이 수행할 수 있는 단계를 안내하는 대화형 bash 마법사를 생성합니다. 인프라 프로비저닝, 자격 증명이나 CI 시크릿 설정, 익숙하지 않은 서드파티 대시보드 탐색, 또는 일회성 마이그레이션이나 전환 실행 등이 해당합니다.

### 생산성

코드에 국한되지 않는 일반적인 워크플로 도구입니다.

**사용자 호출**

- **[grill-me](./skills/productivity/grill-me/SKILL.md)**: 설계 트리의 모든 가지가 해결될 때까지 계획이나 설계에 대해 끈질기게 인터뷰를 받습니다.
- **[handoff](./skills/productivity/handoff/SKILL.md)**: 다른 에이전트가 작업을 이어갈 수 있도록 현재 대화를 인계 문서로 압축합니다.
- **[teach](./skills/productivity/teach/SKILL.md)**: 현재 디렉터리를 상태 저장 교육 작업 공간으로 사용하여, 여러 세션에 걸쳐 사용자에게 새로운 기술이나 개념을 가르칩니다.
- **[to-questionnaire](./skills/productivity/to-questionnaire/SKILL.md)**: 혼자서는 답할 수 없는 결정을, 답할 수 있는 단 한 사람을 위한 마크다운 설문지로 변환합니다. 비동기로 작성하거나, 회의에서 함께 작성합니다. 주제가 아니라 보내는 일(누구를 위한 것인지, 무엇을 돌려받아야 하는지)에 대해 사용자에게 질문합니다.
- **[wait-what](./skills/productivity/wait-what/SKILL.md)**: 메시지가 이해되지 않는 순간 바로 실행하십시오. 에이전트가 사용자에게 부족한 맥락을 보충하여, `GLOSSARY.md`의 어휘를 사용해 평이한 언어로 다시 설명합니다.

**모델 호출**

- **[grilling](./skills/productivity/grilling/SKILL.md)**: 설계 트리의 모든 가지가 해결될 때까지 계획, 결정, 또는 아이디어에 대해 사용자를 끈질기게 인터뷰합니다. `grill-me`, `grill-with-docs`, `triage`, `wayfinder`, `improve-codebase-architecture` 뒤에 있는 재사용 가능한 인터뷰 기본 요소입니다.
- **[writing-for-agents](./skills/productivity/writing-for-agents/SKILL.md)**: 에이전트를 위한 문서 작성입니다. 스킬, AGENTS.md/CLAUDE.md, 그리고 에이전트가 포인터를 통해 도달하는 모든 문서가 해당합니다.
