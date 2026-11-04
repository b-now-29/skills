# Engineering

코드 작업을 위해 매일 사용하는 스킬입니다.

## 사용자 호출

사용자가 직접 입력할 때만 도달할 수 있습니다(Claude Code: `disable-model-invocation: true`, Codex: `agents/openai.yaml`의 `policy.allow_implicit_invocation: false`).

- **[ask-matt](./ask-matt/SKILL.md)**: 상황에 맞는 스킬이나 흐름이 무엇인지 묻습니다. 이 저장소의 사용자 호출 스킬에 대한 라우터입니다.
- **[grill-with-docs](./grill-with-docs/SKILL.md)**: 프로젝트의 도메인 모델도 함께 구축하는 그릴링 세션으로, 용어를 정제하고 `GLOSSARY.md`와 ADR을 즉석에서 업데이트합니다.
- **[triage](./triage/SKILL.md)**: 트리아지 역할의 상태 기계를 따라 이슈를 이동시킵니다.
- **[improve-codebase-architecture](./improve-codebase-architecture/SKILL.md)**: 코드베이스에서 심화 기회를 탐색하여 시각적인 HTML 보고서로 제시한 다음, 사용자가 선택한 항목에 대해 그릴링을 진행합니다.
- **[setup-matt-pocock-skills](./setup-matt-pocock-skills/SKILL.md)**: 엔지니어링 스킬을 위해 저장소를 구성합니다(이슈 트래커, 트리아지 라벨, 도메인 문서 레이아웃). 저장소마다 한 번 실행하십시오.
- **[to-spec](./to-spec/SKILL.md)**: 현재 대화를 명세로 변환하여 이슈 트래커에 게시합니다.
- **[to-tickets](./to-tickets/SKILL.md)**: 어떤 계획, 명세, 대화든 트레이서 불릿 티켓 세트로 분해합니다. 각 티켓은 로컬 파일의 텍스트로든 실제 트래커의 네이티브 차단 링크로든 자신의 차단 관계를 선언합니다.
- **[implement](./implement/SKILL.md)**: 명세나 티켓 세트가 기술하는 작업을 구현합니다. 사전에 합의된 시임에서 `/tdd`를 진행하고, 커밋하기 전에 `/code-review`로 마무리합니다.
- **[implement-spec](./implement-spec/SKILL.md)**: 하나의 통합 브랜치에서 명세 전체를 구현합니다. 티켓을 작업 그래프로 다루며, 최대 동시성을 위해 준비된 전선 전반에 걸쳐 구현자 서브에이전트를 실행한 다음, `/code-review`로 마무리합니다.
- **[wayfinder](./wayfinder/SKILL.md)**: 대규모 작업(하나의 에이전트 세션이 담을 수 있는 것보다 큰 작업)을 이슈 트래커 위의 결정 티켓으로 이루어진 공유 지도로 계획하고, 목적지로 가는 길이 명확해질 때까지 하나씩 해결합니다.
- **[retro](./retro/SKILL.md)**: 세션이 끝난 후 코딩 에이전트의 환경(탐색, 자동화된 검사, 코딩 표준, 지침 파일, 도구)에 대한 개선 사항을 가장 심각한 것부터 제안합니다.

## 모델 호출

모델 또는 사용자가 도달할 수 있습니다(모델이 사용할 수 있도록 풍부한 트리거 문구를 가집니다).

- **[prototype](./prototype/SKILL.md)**: 설계 질문에 답하기 위한 일회용 프로토타입을 만듭니다. 상태/로직을 위한 공유 가능한 단일 HTML 파일, 또는 전환 가능한 여러 UI 변형입니다.

- **[diagnosing-bugs](./diagnosing-bugs/SKILL.md)**: 어려운 버그와 성능 회귀를 위한 규율 있는 진단 루프입니다. 이 버그에서 red가 되는 피드백 루프 구축 → 최소화 → 가설 수립 → 계측 → 수정 → 회귀 테스트.
- **[research](./research/SKILL.md)**: 신뢰도 높은 1차 자료를 바탕으로 질문을 조사하고, 그 결과를 출처가 명시된 마크다운 파일로 저장소에 기록합니다. 백그라운드 에이전트로 실행됩니다.
- **[tdd](./tdd/SKILL.md)**: red-green-refactor 루프를 사용하는 테스트 주도 개발입니다. 한 번에 하나의 수직 슬라이스씩 기능을 구축하거나 버그를 수정합니다.
- **[domain-modeling](./domain-modeling/SKILL.md)**: 용어에 이의를 제기하고, 시나리오로 스트레스 테스트를 하며, `GLOSSARY.md`와 ADR을 즉석에서 업데이트하여 프로젝트의 도메인 모델을 능동적으로 구축하고 정제합니다.
- **[codebase-design](./codebase-design/SKILL.md)**: 깊은 모듈을 설계하기 위한 공유 규율과 어휘입니다. 작은 인터페이스, 깔끔한 시임, 인터페이스를 통한 테스트 가능성을 다룹니다.
- **[code-review](./code-review/SKILL.md)**: 고정된 시점 이후의 diff에 대한 두 축의 리뷰입니다. **Standards**(저장소의 코딩 표준과 Fowler 코드 스멜 기준선을 따르는가?)와 **Spec**(원래의 이슈/명세를 충실하게 구현하는가?)이며, 병렬 서브에이전트로 실행됩니다.
- **[pr](./pr/SKILL.md)**: 풀 리퀘스트 본문이 갖추어야 할 형태입니다. 변경 사항을 명확하게 보여 주는 가장 작은 시각 자료로서의 요약, 동작한다는 전후 증거, 그리고 병합 위험도 판단(일방향 문 또는 양방향 문, 그리고 영향 범위)입니다.
- **[wizard](./wizard/SKILL.md)**: 사람만이 수행할 수 있는 단계를 안내하는 대화형 bash 마법사를 생성합니다. 인프라 프로비저닝, 자격 증명이나 CI 시크릿 설정, 익숙하지 않은 서드파티 대시보드 탐색, 또는 일회성 마이그레이션이나 전환 실행 등이 해당합니다.
