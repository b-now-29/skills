# Matt Pocock Skills

Claude Code가 로드하는 에이전트 스킬(슬래시 명령 및 동작)의 모음입니다. 스킬은 버킷으로 구성되며, `/setup-matt-pocock-skills`가 생성하는 저장소별 구성을 통해 사용됩니다.

## 용어

**이슈 트래커(Issue tracker)**:
저장소의 이슈를 호스팅하는 도구입니다. GitHub Issues, Linear, 로컬 `.scratch/` 마크다운 규칙, 또는 그와 유사한 것입니다. `to-tickets`, `to-spec`, `triage`와 같은 스킬이 이 도구에서 읽고 씁니다.
_사용하지 말 것_: backlog manager, backlog backend, issue host

**이슈(Issue)**:
**이슈 트래커** 내부에서 추적되는 단일 작업 단위입니다. 버그, 작업, 명세, 또는 `to-tickets`가 생성한 슬라이스(slice)입니다.
_사용하지 말 것_: ticket (티켓이라고 부르는 외부 시스템을 인용할 때, 또는 아래의 **결정 티켓**에 대해서만 사용)

**결정 티켓(Decision ticket)**:
`wayfinder`의 단위입니다. `wayfinder:map`의 하위 **이슈**로서, 실행할 빌드의 슬라이스가 아니라 해결 결과가 결정인 *질문*을 담고 있습니다. **결정**이라는 수식어가 구현 티켓과 구별되게 해 줍니다. `wayfinder`는 이 용어를 도입한 후 "티켓"이라는 표현을 사용합니다.

**트리아지 역할(Triage role)**:
트리아지 중에 **이슈**에 적용되는 표준 상태 기계 라벨입니다(예: `needs-triage`, `ready-for-afk`). 각 역할은 `docs/agents/triage-labels.md`를 통해 **이슈 트래커**의 실제 라벨 문자열에 매핑됩니다.

## 관계

- **이슈 트래커**는 여러 **이슈**를 담습니다
- **이슈**는 한 번에 하나의 **트리아지 역할**을 가집니다
- **결정 티켓**은 **이슈**입니다(`wayfinder:map`의 하위 항목)

## 표시된 모호성

- "backlog"는 이전에 이슈를 호스팅하는 *도구*와 그 안에 있는 *작업의 총체* 둘 다를 의미하는 데 사용되었습니다. 해결됨: 도구는 **이슈 트래커**이며, "backlog"는 더 이상 도메인 용어로 사용되지 않습니다.
- "backlog backend" / "backlog manager". 해결됨: **이슈 트래커**로 통합되었습니다.
