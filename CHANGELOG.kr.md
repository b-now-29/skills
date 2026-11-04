# mattpocock-skills

## 1.3.2

### 패치 변경 사항

- [#1194](https://github.com/mattpocock/skills/pull/1194) [`b645f47`](https://github.com/mattpocock/skills/commit/b645f47de3e17ed3bf60586c9bebb8092e0f79fd) [@mattpocock](https://github.com/mattpocock) 님께 감사드립니다! - `ask-matt`는 이제 스킬이 무엇을 하는지 설명하거나 어떤 단계를 건너뛰라고 권장하기 전에, 자신의 한 줄 요약을 신뢰하는 대신 해당 스킬의 `SKILL.md`를 읽습니다([#614](https://github.com/mattpocock/skills/issues/614)).

- [#1304](https://github.com/mattpocock/skills/pull/1304) [`5beb35b`](https://github.com/mattpocock/skills/commit/5beb35b040e3de97e54fa9e386d7e42d15c295c2) [@mattpocock](https://github.com/mattpocock) 님께 감사드립니다! - `chief-of-staff`는 이제 기억을 LLM 위키(`index.md`와 주제당 하나의 페이지로 구성되며, 수집, 조회, 점검을 통해 유지됨)에 보관하고, 이를 역사적 기록으로 작성합니다. 모든 주장에 날짜가 기록되며, 코드에 관한 모든 주장은 그것이 참이었던 커밋을 인용합니다.

- [#1208](https://github.com/mattpocock/skills/pull/1208) [`3da8c01`](https://github.com/mattpocock/skills/commit/3da8c01116264675eeefbd6e9d59c734de9095cc) [@mattpocock](https://github.com/mattpocock) 님께 감사드립니다! - `code-review`는 이제 저장소에서 표준 파일을 검색하고 항상 `CODING_STANDARDS.md` / `CONTRIBUTING.md`를 Standards 서브에이전트에 넘기며([#1065](https://github.com/mattpocock/skills/issues/1065)), 두 서브에이전트를 포그라운드에서 실행하여 반환된 보고서를 사용하고([#1073](https://github.com/mattpocock/skills/issues/1073)), 하드코딩된 경로 대신 제공된 트래커 문서를 통해 이슈 트래커를 해석합니다([#937](https://github.com/mattpocock/skills/issues/937)).

- [#1209](https://github.com/mattpocock/skills/pull/1209) [`f3fc563`](https://github.com/mattpocock/skills/commit/f3fc5632f401156837ee3872f14fe33ccf1024ea) [@mattpocock](https://github.com/mattpocock) 님께 감사드립니다! - `diagnosing-bugs` 5단계는 이제 red를 신뢰하기 전에 강제로 가한 변경을 깨끗한 사본과 `diff`하도록 에이전트에게 지시하므로, 조용히 아무것도 바꾸지 않은 편집이 실패하는 테스트로 통과할 수 없습니다([#955](https://github.com/mattpocock/skills/issues/955)).

- [#1187](https://github.com/mattpocock/skills/pull/1187) [`e0efb6e`](https://github.com/mattpocock/skills/commit/e0efb6e7435ebb420d8a25d6816ed1ebaa2d23d2) [@mattpocock](https://github.com/mattpocock) 님께 감사드립니다! - `authorAssociation`에서 실패하던 GitHub 트래커 템플릿의 외부 PR 목록을 수정했습니다([#468](https://github.com/mattpocock/skills/issues/468), @lofi-coding 님께 감사드립니다). `docs/agents/issue-tracker.md`를 갱신하려면 `/setup-matt-pocock-skills`를 다시 실행하십시오.

- [#1169](https://github.com/mattpocock/skills/pull/1169) [`59db609`](https://github.com/mattpocock/skills/commit/59db609eb1e18aaf59b63284d0e52255aff0c63c) [@mattpocock](https://github.com/mattpocock) 님께 감사드립니다! - `setup-matt-pocock-skills`가 작성하는 GitHub 이슈 트래커 템플릿은 이제 에이전트에게 이슈를 `mattpocock/skills`가 아니라 사용자 자신의 저장소에만 제출하고, 첫 번째 `gh issue create` 전에 대상 저장소를 확인하라고 지시합니다. 이 저장소의 클론이나 포크에서 작업하던 에이전트들이 자신의 명세와 티켓을 이곳에 제출했었습니다([#541](https://github.com/mattpocock/skills/issues/541)부터 [#550](https://github.com/mattpocock/skills/issues/550)까지).

- [#1193](https://github.com/mattpocock/skills/pull/1193) [`95249b0`](https://github.com/mattpocock/skills/commit/95249b0b49782349740fd9b8c6ce32b4e59e497a) [@mattpocock](https://github.com/mattpocock) 님께 감사드립니다! - `grilling`은 "예"라고 답하면 권장 답변을 수락하는 것이 되도록 각 질문의 문구를 작성하므로, 동의하는 것이 결코 "아니요"라고 답하는 것이 되지 않습니다([#706](https://github.com/mattpocock/skills/issues/706)).

- [#1184](https://github.com/mattpocock/skills/pull/1184) [`4f4e943`](https://github.com/mattpocock/skills/commit/4f4e9433bbb7c4957ef33b1ea26686fb7c2a4cf4) [@mattpocock](https://github.com/mattpocock) 님께 감사드립니다! - `handoff`는 이제 OS 임시 디렉터리가 어디인지(`$TMPDIR`, 없으면 `/tmp`, Windows에서는 `%TEMP%`) 명시하므로, 에이전트가 더 이상 추측하지 않습니다([#272](https://github.com/mattpocock/skills/issues/272)).

- [#1189](https://github.com/mattpocock/skills/pull/1189) [`e48341a`](https://github.com/mattpocock/skills/commit/e48341a3d412cfeba4b9a79d3fd0331fc376ba82) [@mattpocock](https://github.com/mattpocock) 님께 감사드립니다! - `implement`는 이제 단순한 `/skill` 서술 대신 `tdd`와 `code-review`에 대해 Skill 도구를 호출하며, [#878](https://github.com/mattpocock/skills/issues/878)과 일치합니다.

- [#1196](https://github.com/mattpocock/skills/pull/1196) [`6d6a5b9`](https://github.com/mattpocock/skills/commit/6d6a5b9072f47ee7ba1d972d8ce0ee98b7ed4394) [@mattpocock](https://github.com/mattpocock) 님께 감사드립니다! - `implement`는 전달된 티켓 참조를 이슈 트래커에서 가져와 시작하기 전에 그 제목을 명시하며, 참조가 모호하면 묻습니다([#700](https://github.com/mattpocock/skills/issues/700)).

- [#1228](https://github.com/mattpocock/skills/pull/1228) [`ed0de59`](https://github.com/mattpocock/skills/commit/ed0de59eb5de8c2730a650cc69f588ffa64c1040) [@mattpocock](https://github.com/mattpocock) 님께 감사드립니다! - `setup-matt-pocock-skills`는 이제 아무것도 도달할 수 없는 GitHub/GitLab 트래커를 작성하기 전에 git 원격 저장소를 연결하며([#1201](https://github.com/mattpocock/skills/issues/1201)), 레거시 `CONTEXT.md` / `CONTEXT-MAP.md`를 `GLOSSARY` 이름으로 `git mv`하겠다고 제안합니다([#1176](https://github.com/mattpocock/skills/issues/1176)). GitHub 템플릿은 종료하기 전에 댓글을 달고([#873](https://github.com/mattpocock/skills/issues/873)), PR의 댓글뿐만 아니라 본문도 읽으며([#1138](https://github.com/mattpocock/skills/issues/1138)), **Blocking**을 네이티브 `gh` 플래그와 함께 Conventions로 옮기고([#855](https://github.com/mattpocock/skills/issues/855)), 열린 차단 이슈를 세는 명령을 명시합니다([#1118](https://github.com/mattpocock/skills/issues/1118)). GitLab 템플릿은 `-O json`으로 MR을 나열하고 전선 조회의 명령을 명시합니다([#1143](https://github.com/mattpocock/skills/issues/1143)). `docs/agents/`를 갱신하려면 `/setup-matt-pocock-skills`를 다시 실행하십시오.

- [#1197](https://github.com/mattpocock/skills/pull/1197) [`5b7cade`](https://github.com/mattpocock/skills/commit/5b7cade4d68947f34dae71326a0ce89f09e22c9c) [@mattpocock](https://github.com/mattpocock) 님께 감사드립니다! - `setup-matt-pocock-skills`는 이제 GitHub/GitLab에서 누락된 트리아지 라벨을 생성하고([#616](https://github.com/mattpocock/skills/issues/616)), GitLab 템플릿의 `glab` 명령을 수정하며([#635](https://github.com/mattpocock/skills/issues/635)), 라벨과 본문이 함께 오도록 `--json`으로 GitHub 이슈를 읽고([#733](https://github.com/mattpocock/skills/issues/733)), `triage-labels.md`의 "Label in our tracker" 열을 명시합니다([#801](https://github.com/mattpocock/skills/issues/801)). `docs/agents/`를 갱신하려면 `/setup-matt-pocock-skills`를 다시 실행하십시오.

- [#1341](https://github.com/mattpocock/skills/pull/1341) [`7739eae`](https://github.com/mattpocock/skills/commit/7739eaed7f8f3915437a8def198a6d0d7206dbc7) [@mattpocock](https://github.com/mattpocock) 님께 감사드립니다! - 서브에이전트를 디스패치하는 스킬(`implement-spec`, `code-review`, `codebase-design`, `improve-codebase-architecture`, `wayfinder`, `research`, `grilling`, `chief-of-staff`)은 이제 현재 대화를 포크하는 대신 각 서브에이전트를 새로운 컨텍스트 윈도우로 시작하라고 명시합니다. 일부 하네스(Codex)는 기본적으로 포크하며, 그것은 서브에이전트가 존재하는 이유인 깨끗한 컨텍스트를 버리게 만듭니다.

- [#1192](https://github.com/mattpocock/skills/pull/1192) [`3f59913`](https://github.com/mattpocock/skills/commit/3f599139104dfceabc7754eeb91319802f85e042) [@mattpocock](https://github.com/mattpocock) 님께 감사드립니다! - `tdd`는 이제 제안하는 각 시임에 그것이 무엇을 잡아내고 무엇을 놓치는지에 대한 한 줄 메모를 덧붙이므로, 시임 사이에서 고르는 것이 더 이상 추측이 아닙니다([#607](https://github.com/mattpocock/skills/issues/607)).

- [#1183](https://github.com/mattpocock/skills/pull/1183) [`ad5400b`](https://github.com/mattpocock/skills/commit/ad5400b930b297b0c0cb231ff1ffe42a7da666aa) [@mattpocock](https://github.com/mattpocock) 님께 감사드립니다! - `teach` 퀴즈는 정답이 놓이는 위치를 바꿉니다([#611](https://github.com/mattpocock/skills/issues/611)).

- [#1183](https://github.com/mattpocock/skills/pull/1183) [`ad5400b`](https://github.com/mattpocock/skills/commit/ad5400b930b297b0c0cb231ff1ffe42a7da666aa) [@mattpocock](https://github.com/mattpocock) 님께 감사드립니다! - `teach`는 작업 공간을 스킬 폴더가 아니라 실행한 디렉터리에 작성합니다([#377](https://github.com/mattpocock/skills/issues/377)).

- [#1188](https://github.com/mattpocock/skills/pull/1188) [`cffab50`](https://github.com/mattpocock/skills/commit/cffab50350e3d96688f63f890f4d7ca0e6007cfe) [@mattpocock](https://github.com/mattpocock) 님께 감사드립니다! - `to-tickets`는 각 티켓을 출처 이슈의 하위 이슈로 만들며(GitHub 트래커 템플릿이 이제 그 명령을 제공합니다), 차단 관계가 네이티브 관계일 때는 `## Blocked by`를 생략합니다. `docs/agents/issue-tracker.md`를 갱신하려면 `/setup-matt-pocock-skills`를 다시 실행하십시오. @richardwhatever 님([#554](https://github.com/mattpocock/skills/issues/554))과 @adamslowe 님([#262](https://github.com/mattpocock/skills/issues/262))께 감사드립니다.

- [#1181](https://github.com/mattpocock/skills/pull/1181) [`8295b8e`](https://github.com/mattpocock/skills/commit/8295b8e10d4cdb6cce772a56dda7b7c37075074d) [@mattpocock](https://github.com/mattpocock) 님께 감사드립니다! - `wayfinder`는 더 이상 지도나 티켓에 `ready-for-agent` 라벨을 붙이지 않고([#518](https://github.com/mattpocock/skills/issues/518)), 실제 이슈 id로만 상호 참조를 작성하며([#507](https://github.com/mattpocock/skills/issues/507)), 조사 브랜치에서 PR을 열지 않고([#576](https://github.com/mattpocock/skills/issues/576)), 각 티켓을 그 라벨이 지정하는 유형으로 해결합니다([#625](https://github.com/mattpocock/skills/issues/625)). @jcwayne, @baob, @rynz, @sponge-b0b 님께 감사드립니다.

- [#1237](https://github.com/mattpocock/skills/pull/1237) [`49dd158`](https://github.com/mattpocock/skills/commit/49dd158d1076134a641b33efb035946536778336) [@mattpocock](https://github.com/mattpocock) 님께 감사드립니다! - `wizard` 템플릿 수정: `_existing`이 큰따옴표로 감싼 `.env` 값을 디코딩하므로, Enter로 현재 값 유지 시 더 이상 따옴표가 저장되지 않습니다([#1220](https://github.com/mattpocock/skills/issues/1220)). 단계가 `run_wizard` 안에서 실행되므로, 실행 도중 스크립트를 편집해도 중단되지 않습니다([#1142](https://github.com/mattpocock/skills/issues/1142)). `tput clear`가 실패하면 `_clear`가 ANSI로 대체합니다([#1081](https://github.com/mattpocock/skills/issues/1081)). `write_env`가 셸 변수도 설정합니다([#1041](https://github.com/mattpocock/skills/issues/1041)). 사용되지 않는 `RED`를 제거했습니다([#1003](https://github.com/mattpocock/skills/issues/1003)).

- [#1198](https://github.com/mattpocock/skills/pull/1198) [`868c4cf`](https://github.com/mattpocock/skills/commit/868c4cf20cb7e08bc805c388ff1f305dbedd261a) [@mattpocock](https://github.com/mattpocock) 님께 감사드립니다! - `wizard` 템플릿 수정: `ask`가 Readline을 사용하므로 화살표 키로 커서가 이동합니다([#741](https://github.com/mattpocock/skills/issues/741)). `write_env`가 값을 작은따옴표로 감싸므로 공백, `#`, `$`, 따옴표가 `source`와 dotenv에서도 보존됩니다([#770](https://github.com/mattpocock/skills/issues/770)). 브라우저 오프너가 없을 때 `open_url`이 직접 열라는 경고를 출력합니다([#774](https://github.com/mattpocock/skills/issues/774)). `write_env`가 심볼릭 링크된 `.env`를 통해 작성하며 기존 파일의 모드를 유지합니다([#811](https://github.com/mattpocock/skills/issues/811)). `ask`와 `ask_secret`이 EOF에서 반복하는 대신 실패합니다([#852](https://github.com/mattpocock/skills/issues/852)).

## 1.3.1

### 패치 변경 사항

- [#1121](https://github.com/mattpocock/skills/pull/1121) [`c5b9869`](https://github.com/mattpocock/skills/commit/c5b98691982c4f0d3a5e40ab09566b3b84721e00) [@mattpocock](https://github.com/mattpocock) 님께 감사드립니다! - `ask-matt`는 더 이상 `diagnosing-bugs`가 사후 분석에서 `improve-codebase-architecture`로 인계한다고 말하지 않습니다. 그 단계는 제거되었습니다. 이제 수정이 반영되면 무엇이 버그를 막을 수 있었는지 묻기 위해 `/retro`를 가리키고, 발견 사항이 빠진 시임인 경우에는 `/improve-codebase-architecture`를 가리킵니다. `diagnosing-bugs` 문서 페이지도 같은 낡은 인계를 제거합니다. 이를 발견해 주신 @Ygilany 님께 감사드립니다([#1117](https://github.com/mattpocock/skills/issues/1117)).

## 1.3.0

### 마이너 변경 사항

- [#1120](https://github.com/mattpocock/skills/pull/1120) [`2aecca1`](https://github.com/mattpocock/skills/commit/2aecca12ea9ff047f76c8178cb64dfeafd192abe) [@mattpocock](https://github.com/mattpocock) 님께 감사드립니다! - **`implement-spec`**을 **Engineering** 버킷으로 졸업시켜, Claude Code 플러그인에 포함되어 배포되고, 문서 페이지를 가지며, 티켓별 `implement`의 병렬 대안으로서 `ask-matt`가 안내하도록 합니다.

  `implement-spec`(사용자 호출)은 한 번의 실행으로 명세 전체를 구현합니다. 티켓을 **작업 그래프**로 읽고, 준비된 **전선** 전반에 걸쳐 자체 워크트리에서 구현자 서브에이전트를 실행하며, 모든 것을 하나의 **통합 브랜치**에 반영하고, `code-review`로 마무리합니다. 졸업에 앞서:

  - 목표는 이제 PR이 아니라 통합 브랜치입니다. 초안 PR은 이슈 트래커가 PR을 통해 작업을 종료하거나 사용자가 요청할 때만, 그리고 첫 번째 병합 후에만 열립니다(main보다 앞선 커밋이 없는 브랜치는 PR을 열 수 없습니다). PR이 없으면, 티켓은 트래커가 작업을 종료하는 방식대로 해결됩니다.
  - 형제 스킬들처럼 이슈 트래커를 가리키며, 제공된 것이 없을 때 조용히 `gh`를 기본값으로 삼는 대신 `/setup-matt-pocock-skills`를 실행하라고 안내합니다.
  - 각 구현자는 자신의 워크트리가 통합 브랜치를 기반으로 하는지 확인하고, `tdd`로 티켓을 구현하며, 완료를 보고하기 전에 통합 브랜치의 최신 커밋을 자신의 브랜치에 병합하므로, 각 병합은 fast-forward가 됩니다.

- [#1120](https://github.com/mattpocock/skills/pull/1120) [`2aecca1`](https://github.com/mattpocock/skills/commit/2aecca12ea9ff047f76c8178cb64dfeafd192abe) [@mattpocock](https://github.com/mattpocock) 님께 감사드립니다! - **`pr`**을 **Engineering** 버킷으로 졸업시켜, Claude Code 플러그인에 포함되어 배포되고, 문서 페이지를 가지며, PR 본문 마무리로서 `ask-matt`가 안내하도록 합니다.

  `pr`(모델 호출)은 풀 리퀘스트 본문이 갖추어야 할 형태입니다. 변경을 명확하게 만드는 가장 작은 시각 자료로서의 요약(의사 코드, 호출 트리, 파일 트리, Mermaid, diff), 동작한다는 전후 증거, 그리고 병합 위험도 판단(일방향 문 또는 양방향 문, 그리고 영향 범위)입니다. Summary 시각 자료는 Dex Horthy의 `show-me`에서 가져왔으며, 스킬의 `CREDITS.md`에 출처가 표시되어 있습니다.

- [#1120](https://github.com/mattpocock/skills/pull/1120) [`2aecca1`](https://github.com/mattpocock/skills/commit/2aecca12ea9ff047f76c8178cb64dfeafd192abe) [@mattpocock](https://github.com/mattpocock) 님께 감사드립니다! - **`retro`**를 **Engineering** 버킷으로 졸업시켜, Claude Code 플러그인에 포함되어 배포되고, 문서 페이지를 가지며, `code-review` 다음의 주 흐름 마지막 단계로서 `ask-matt`가 안내하도록 합니다.

  `retro`(사용자 호출)는 코딩 세션을 되돌아보며 코드가 아니라 에이전트의 환경에 대한 변경을 제안합니다. 탐색 포인터, 자동화된 검사, 코딩 표준, 지침 파일, 도구 경제성, 정보 접근입니다. 각 코딩 표준 발견 사항을 먼저 분류합니다. 기계적인 위반은 결정적인 검사(린터 규칙, pre-commit 훅, 또는 CI 작업)를 받으며, `CODING_STANDARDS.md`는 진정한 판단의 문제를 위해 남겨 둡니다. 안전장치가 전혀 없는 저장소는 그 자체로 하나의 발견 사항입니다.

- [#1120](https://github.com/mattpocock/skills/pull/1120) [`daa01d8`](https://github.com/mattpocock/skills/commit/daa01d8aa68ad5c61b68970ec2018d0ce9567be6) [@mattpocock](https://github.com/mattpocock) 님께 감사드립니다! - **`resolving-merge-conflicts`** 스킬을 제거합니다. 더 이상 필요하지 않으며, 그것을 대체하는 것은 없습니다. 에이전트는 전용 스킬 없이 진행 중인 병합이나 리베이스 충돌을 처리합니다. Claude Code 플러그인, README, `ask-matt` 라우터에서 빠집니다. `https://aihero.dev/skills-resolving-merge-conflicts`의 문서 페이지는 보관됨으로 표시된 채 유지됩니다.

- [#1120](https://github.com/mattpocock/skills/pull/1120) [`006a52b`](https://github.com/mattpocock/skills/commit/006a52be23e0178375e083e30535fa8224471f3e) [@mattpocock](https://github.com/mattpocock) 님께 감사드립니다! - 스킬들이 읽고 쓰는 모든 곳(`domain-modeling`, `grill-with-docs`, `improve-codebase-architecture`, `setup-matt-pocock-skills`, `triage`, `tdd`, `diagnosing-bugs`, `ask-matt`, `codebase-design`, `wait-what`, `pr`), 그리고 문서 페이지와 이 저장소 자체의 루트 용어집에서 `CONTEXT.md`/`CONTEXT-MAP.md` 도메인 문서 규칙의 이름을 `GLOSSARY.md`/`GLOSSARY-MAP.md`로 바꿉니다.

  이 변경 이전의 기존 `CONTEXT.md`(또는 `CONTEXT-MAP.md`)가 있다면, 새 이름으로 `git mv`하십시오. 앞으로 스킬은 `GLOSSARY.md`/`GLOSSARY-MAP.md`만 찾습니다.

### 패치 변경 사항

- [#848](https://github.com/mattpocock/skills/pull/848) [`f02e2ed`](https://github.com/mattpocock/skills/commit/f02e2ed3624d031272f8547742d23bf6bca8b072) [@mattpocock](https://github.com/mattpocock) 님께 감사드립니다! - domain-modeling: 더 좁았던 "도메인 용어나 유비쿼터스 언어를 확정하라" / "아키텍처 결정을 기록하라" 문구를 대체하여, 코드베이스 용어를 논의할 때와 GLOSSARY.md나 ADR을 직접 작성하거나 편집할 때 트리거됩니다. 또한 "다른 스킬이 도메인 모델을 유지해야 한다"는 단서를 제거합니다. 그것은 이 description이 아니라 호출하는 스킬이 명시적으로 기술해야 할 일이기 때문입니다.

- [#911](https://github.com/mattpocock/skills/pull/911) [`4f28947`](https://github.com/mattpocock/skills/commit/4f289474bad013fe2be8f8769d733f59d9103d6b) [@mattpocock](https://github.com/mattpocock) 님께 감사드립니다! - `to-spec`, `code-review`, `setup-matt-pocock-skills`, `writing-fragments`, `writing-shape`, `wait-what`의 `description` 프런트매터를 따옴표로 감쌉니다. [#905](https://github.com/mattpocock/skills/issues/905)의 엠 대시 일괄 제거에서 남은 따옴표 없는 콜론-공백이 각 블록을 유효하지 않은 YAML로 만들어, `skills.sh`가 탐색 중에 여섯 개 모두를 건너뛰었으며 `npx skills`를 통해 나열하거나 설치할 수 없었습니다.

- [#917](https://github.com/mattpocock/skills/pull/917) [`85f83d3`](https://github.com/mattpocock/skills/commit/85f83d3fde1d3a90d5c9a657f6998c79a6c37308) [@mattpocock](https://github.com/mattpocock) 님께 감사드립니다! - grilling: 연속된 질문이 이어 붙지 않고 수평선(`---`)으로 구분되도록 라운드 템플릿을 업데이트합니다.

- [#879](https://github.com/mattpocock/skills/pull/879) [`d419977`](https://github.com/mattpocock/skills/commit/d419977fe07d9e1607d3523f3579310bbb076b93) [@mattpocock](https://github.com/mattpocock) 님께 감사드립니다! - grilling: `SKILL.md`에서 엠 대시를 제거하고 콜론과 세미콜론으로 대체하여 지시가 평이한 텍스트로 읽히도록 합니다.

- [#905](https://github.com/mattpocock/skills/pull/905) [`e6e9577`](https://github.com/mattpocock/skills/commit/e6e957797d8cceb5b351c0dc840369523f9fb8fb) [@mattpocock](https://github.com/mattpocock) 님께 감사드립니다! - 저장소의 서술(문서, `SKILL.md` 파일, ADR, `README.md`, 스크립트, JSON/YAML 메타데이터)에서 모든 엠 대시를 제거하며, 문자를 기계적으로 치환하는 대신 각 문장을 쉼표, 콜론, 마침표, 괄호, 또는 접속사로 직접 다시 작성합니다. `CLAUDE.md`/`AGENTS.md`는 이제 그것을 다시 도입하지 말라고 명시합니다.

- [#878](https://github.com/mattpocock/skills/pull/878) [`e3e547b`](https://github.com/mattpocock/skills/commit/e3e547b57d549110a0aa6ff40fd7b871c01c76c9) [@mattpocock](https://github.com/mattpocock) 님께 감사드립니다! - `code-review`, `diagnosing-bugs`, `grill-with-docs`, `grill-me`, `improve-codebase-architecture`, `tdd`, `to-spec`, `to-tickets`, `triage`, `wayfinder` 전반에서, 스킬 간 호출을 단순한 `/skill` 형식의 서술 대신 명시적인 "Skill 도구를 호출하라" 지시로 표준화합니다.

  - 서술에서 다른 스킬의 이름을 명시하는 스킬("`/grilling` 스킬을 실행하라")은 그 스킬을 안정적으로 로드하게 만들지 못합니다. 이것이 `grill-with-docs`에서 가장 많이 보고되는 문제 이면의 문서화된 거친 부분입니다. 도구를 직접 명시하는 것(`Call the Skill tool with "grilling"`)은 적중률을 높이기 위한 것입니다. 앞의 `/`를 빼면 지시의 하네스 중립성도 높아집니다. 더 이상 Claude Code의 트리거 문법을 가정하지 않습니다.
  - 둘 이상의 스킬이 필요한 단계는 이제 두 개의 이름을 담은 한 번의 호출이 아니라 여러 번의 호출로 그렇게 명시합니다("`grilling`과 `domain-modeling`에 대해 각각 한 번씩 Skill 도구를 두 번 호출하라").
  - 향후 스킬이 따를 수 있도록 `.agents/invocation.md`에 이 규칙을 문서화합니다.

- [#880](https://github.com/mattpocock/skills/pull/880) [`1dab982`](https://github.com/mattpocock/skills/commit/1dab98299c3b81f560026c01b7ebf55ed5d91373) [@mattpocock](https://github.com/mattpocock) 님께 감사드립니다! - 스킬이 Skill 도구를 통해 사용자 호출 스킬에 도달하려 하지 않도록 합니다. `to-spec`, `wayfinder`, `to-tickets`, `triage`, `code-review`, `diagnosing-bugs`에서 `.agents/invocation.md`의 "다른 어떤 스킬도 그것을 호출할 수 없다" 불변 조건을 위반한 스킬 간 참조를 수정합니다.

  - `to-spec`, `wayfinder`, `to-tickets`, `triage`, `code-review`는 각각 전제 조건("...그렇지 않다면 `/setup-matt-pocock-skills`를 실행하라")을 가지고 있었는데, PR [#878](https://github.com/mattpocock/skills/issues/878)이 이를 문자 그대로의 `Call the Skill tool with "setup-matt-pocock-skills"` 지시로 다시 작성했습니다. `setup-matt-pocock-skills`는 사용자 호출이므로, 이 스킬들 중 어느 것도(사용자 호출이든 모델 호출이든) 그것을 호출할 수 없습니다. 다섯 개 모두를 에이전트가 사람에게 그것을 실행하라고 안내하는 지시로 다시 표현했습니다.
  - `diagnosing-bugs`의 6단계 사후 분석은 같은 방식으로 `improve-codebase-architecture`(역시 사용자 호출)에 인계했으며, 그것도 실패한 호출을 잡아낼 사람이 루프에 없는, 자율적이고 종종 무인으로 실행되는 버그 수정 흐름에서였습니다. 실제로 거의 실행되지 않았으므로, 완화하는 대신 인계를 완전히 제거했습니다. 6단계는 이제 "정리"만이며, 기계적인 체크리스트는 그대로입니다.
  - `.agents/invocation.md`의 "둘 사이의 의존성" 섹션에 예외 단락을 추가했습니다. `Call the Skill tool with "name"` 규칙은 명시된 스킬이 모델 호출일 때만 적용됩니다. 이 섹션은 PR [#878](https://github.com/mattpocock/skills/issues/878)이 그보다 여덟 줄 위에 명시된 사용자 호출/모델 호출 불변 조건과 조정하지 않은 채 도입한 섹션이며, 그 빈틈이 이 버그가 한 곳이 아니라 여섯 곳의 호출 지점에 도달한 이유의 대부분입니다.

  [#453](https://github.com/mattpocock/skills/issues/453)을 수정합니다.

- [#904](https://github.com/mattpocock/skills/pull/904) [`594f0f8`](https://github.com/mattpocock/skills/commit/594f0f83188921a60d45d63d6cdac509de20df2c) [@mattpocock](https://github.com/mattpocock) 님께 감사드립니다! - wait-what: 저장소가 하나의 루트 `GLOSSARY.md`를 유지하는 대신 그런 방식으로 여러 컨텍스트를 색인하는 경우, `GLOSSARY-MAP.md`를 따라 올바른 `GLOSSARY.md`를 찾습니다.

## 1.2.3

### 패치 변경 사항

- [#779](https://github.com/mattpocock/skills/pull/779) [`efce423`](https://github.com/mattpocock/skills/commit/efce423018fc6468a3239621f1c1bcaacc723801) [@mattpocock](https://github.com/mattpocock) 님께 감사드립니다! - `diagnosing-bugs`가 시크릿을 삭제하도록 합니다.

  - `SKILL.md`에 **Redact** 섹션을 추가합니다. 스킬은 에이전트가 명령, 출력, 캡처한 산출물을 보여 주게 하며, 이 섹션은 각각에 대해 민감 정보 삭제를 첫 번째 동작으로 만듭니다. `<REDACTED>`를 쓰고, 자격 증명이 환경에 머물도록 환경 변수를 기반으로 루프를 구축하며, 캡처한 산출물에서는 신호를 담은 줄만 인용합니다.
  - 1단계 완료 기준은 "호출과 그 출력을 붙여 넣으라"고 했습니다. 이제는 민감 정보를 삭제하여 보여 주라고 말하며, 1단계는 사용자에게 **민감 정보가 삭제된** 캡처 산출물을 요청합니다.
  - `scripts/hitl-loop.template.sh`에 `capture`가 그 값을 터미널에 다시 출력한다는 메모를 추가하여, 관찰 값을 받는 데는 그것을 쓰고 로그인은 `step`으로 남도록 합니다.

- [#781](https://github.com/mattpocock/skills/pull/781) [`14bfbbd`](https://github.com/mattpocock/skills/commit/14bfbbd8654a8d2910299e1a004c19c1979687d8) [@mattpocock](https://github.com/mattpocock) 님께 감사드립니다! - `code-review`, `codebase-design`, `improve-codebase-architecture`의 서브에이전트 디스패치 지시에서 Claude Code의 도구 및 에이전트 유형 이름을 제거하여, Codex와 다른 하네스에서도 그 단계를 따를 수 있도록 합니다.

- [#783](https://github.com/mattpocock/skills/pull/783) [`c0fd1e9`](https://github.com/mattpocock/skills/commit/c0fd1e973e040347d424e09934099f1bd6c2dee0) [@mattpocock](https://github.com/mattpocock) 님께 감사드립니다! - wizard: 시간 추정을 제거합니다. 템플릿은 `TOTAL_MINUTES`와 남은 시간 표시를 제거하며, `stage`는 이름만 받고, 진행 상황은 단계 수로 계산됩니다.

## 1.2.2

### 패치 변경 사항

- [#766](https://github.com/mattpocock/skills/pull/766) [`4aaccb5`](https://github.com/mattpocock/skills/commit/4aaccb58d40559d7e3c59a029b2290ae5ba538de) [@mattpocock](https://github.com/mattpocock) 님께 감사드립니다! - Codex에서 `writing-for-agents`를 다시 모델 호출 가능하게 합니다.

  - `agents/openai.yaml`에서 `policy.allow_implicit_invocation: false`를 제거합니다. Codex가 모델이 볼 수 있는 스킬 목록에서 이 스킬을 걸러 냈으므로, description이 이를 트리거할 수 없었으며 명시적인 `$writing-for-agents` 언급만 동작했습니다.
  - 여전히 이전 `writing-great-skills` 스킬의 이름을 담고 있던 낡은 `interface.display_name`과 `interface.short_description`을 업데이트합니다.
  - `README.md`와 `skills/productivity/README.md`에서 스킬을 **사용자 호출** 목록에서 **모델 호출** 목록으로 옮깁니다.

## 1.2.0

### 마이너 변경 사항

- [#551](https://github.com/mattpocock/skills/pull/551) [`697d4ce`](https://github.com/mattpocock/skills/commit/697d4ce9742da558fd1ba6697c8e9775e2e302dd) [@mattpocock](https://github.com/mattpocock) 님께 감사드립니다! - 세트가 생성된 사본 없이 두 하네스 모두에서 동작하도록, 각 스킬의 Claude Code 프런트매터 옆에 Codex 메타데이터를 추가합니다.

  - 모든 `SKILL.md` 옆에 Codex UI 메타데이터(`interface.display_name`, `interface.short_description`)를 담은 `agents/openai.yaml`을 추가합니다.
  - 모든 사용자 호출 스킬에 `disable-model-invocation: true`의 Codex 대응물인 `policy.allow_implicit_invocation: false`를 표시하여, 명시적인 `$skill` 호출은 여전히 동작하면서 Codex가 암묵적 호출에서 이를 제외하도록 합니다.
  - `.agents/invocation.md`, `CLAUDE.md`, 승격된 버킷 README에 이중 하네스 호출 모델을 문서화합니다.
  - Codex가 같은 저장소 지침을 읽도록 `CLAUDE.md`에 대한 심볼릭 링크로 `AGENTS.md`를 추가합니다.

- [#593](https://github.com/mattpocock/skills/pull/593) [`0f2bdbd`](https://github.com/mattpocock/skills/commit/0f2bdbdb06220d2df3718b8f0483157c6c8a8600) [@mattpocock](https://github.com/mattpocock) 님께 감사드립니다! - **`to-questionnaire`**를 `in-progress/`에서 **Productivity** 버킷으로 졸업시켜, 플러그인에 포함되어 배포되도록 합니다. 혼자서는 답할 수 없는 결정을, 답할 수 있는 단 한 사람을 위한 마크다운 설문지로 변환합니다. 비동기로 작성하거나, 회의에서 함께 진행합니다.

  핵심 동작은 주제가 아니라 **보내는 일**에 대해 사용자를 그릴링하는 것입니다. 일반적인 그릴링 세션은 주제를 심문하는데, 그것이 바로 여기서 답할 수 없는 것이므로, 인터뷰는 설문지를 누구에게 보내는지와 무엇을 돌려받아야 하는지만 묻고, 모든 질문이 그 둘 사이의 간극을 겨냥하도록 합니다.

  이제 승격된 스킬로 연결되었습니다. 플러그인 항목, **사용자 호출** 아래의 최상위 및 Productivity README, `docs/productivity/to-questionnaire.md`의 문서 페이지, 그리고 `/grill-me`의 반대(자신이 아니라 다른 사람을 캐냄)로 설명하는 `ask-matt`의 독립형 경로입니다.

- [#680](https://github.com/mattpocock/skills/pull/680) [`b3376f8`](https://github.com/mattpocock/skills/commit/b3376f8d39848dd08572ec2667da4739a67c8c04) [@mattpocock](https://github.com/mattpocock) 님께 감사드립니다! - **`wizard`**를 `in-progress/`에서 **Engineering** 버킷으로 졸업시켜 플러그인에 포함되어 배포되도록 하고, 모델 호출로 만듭니다. 서드파티 설정, 일회성 마이그레이션, A→B 상태 전환과 같은 수동 절차를 사람에게 안내하는 대화형 bash 스크립트를 생성하며, 각 URL을 열고, 무엇을 클릭할지 알려 주고, 값을 받아, `.env` 파일과 GitHub Actions 시크릿에 기록합니다.

  쾌적한 UX는 번들된 `template.sh`가 미리 해결해 두었습니다(남은 시간이 표시되는 진행 상황, 확인 관문, WSL을 포함한 크로스 플랫폼 URL 열기, 숨겨진 시크릿 입력, 멱등적인 `.env` upsert, 우아한 성능 저하를 갖춘 `gh secret`/`gh variable` 쓰기, 건너뛴 항목의 마무리 요약). `STAGES` 표시 위의 모든 것은 결코 손으로 편집하지 않는 고정된 라이브러리입니다. 스킬의 일은 절차의 범위를 정하고 그 **단계(stages)**를 작성하는 것뿐입니다.

  Productivity가 아니라 Engineering인 이유: 범위를 정하기 위해 `.env*`, `docker-compose*`, 프레임워크 구성, `.github/workflows/`의 모든 `secrets.*`/`vars.*` 참조를 읽고, CI 시크릿을 작성하며, `bash -n`과 `shellcheck`로 출력을 검증하기 때문입니다.

  모델 호출이므로, 에이전트는 사람만이 수행할 수 있는 단계에 부딪히는 순간, 채팅에 번호 매긴 지시를 쏟아 내고 사용자가 따르기를 바라는 대신 이를 사용할 수 있습니다. `/wizard`를 입력하는 것은 이전과 정확히 같이 동작합니다. 모델 호출은 에이전트의 접근을 _더할_ 뿐입니다. description은 언제 실행될지 결정하는 포인터로 작성되었습니다. 무엇을 만들어 내는지, 네 가지 트리거 분기(인프라 프로비저닝, 자격 증명이나 CI 시크릿 설정, 익숙하지 않은 서드파티 대시보드 탐색, 일회성 마이그레이션이나 전환), 그리고 명시적인 비트리거입니다. 에이전트가 직접 수행할 수 있는 단계에는 호출하지 마십시오. 에이전트가 할 수 있는 일은 에이전트가 해야 하며, 마법사는 에이전트에게 맡기지 않을 클릭, 승인, 대시보드 방문을 위한 것입니다. 한 줄이라도 작성되기 전의 단계 목록 확인은 이제 에이전트가 구현 도중에 이를 실행할 때 제안 역할도 합니다.

  이제 승격된 스킬로 연결되었습니다. 플러그인 항목, **모델 호출** 아래의 최상위 및 Engineering README, `docs/engineering/wizard.md`의 문서 페이지, 그리고 사람만이 할 수 있는 단계를 위한 `ask-matt`의 독립형 경로입니다. 모델 호출은 또한 Claude의 데스크톱 및 웹 화면에서 사용자 호출 스킬을 목록에서 누락하는 [#693](https://github.com/mattpocock/skills/issues/693)의 영향에서 벗어나게 합니다.

- [#763](https://github.com/mattpocock/skills/pull/763) [`77d207e`](https://github.com/mattpocock/skills/commit/77d207ef03219cc603e2832e1159cbdd1c91818e) [@mattpocock](https://github.com/mattpocock) 님께 감사드립니다! - **`prototype`** 스킬을 두 가지 개념을 중심으로 재구성합니다. 데모는 **하나의 공유 가능한 HTML 파일**이며, 프로토타입은 **1차 자료**입니다.

  로직 분기는 이제 터미널 앱 대신 하나의 독립적인 파일(평범한 HTML/CSS/JS, 빌드 없음, 서버 없음)을 만들어 냅니다. 개발자가 아닌 사람도 더블 클릭으로 열어 자신의 도메인 언어로 조작할 수 있습니다. 라벨이 붙은 상태 패널, 항상 사용 가능한 자유 조작 버튼, 그리고 탭으로 구분된 **안내형 시연** 세트로, 각각은 그 아래에 눌러야 할 순서대로의 버튼을 가진 시나리오입니다. 이식 가능한 순수 로직 모듈은 여전히 실제 코드로 옮겨지며, HTML 셸이 일회용입니다.

  일회용은 더 이상 삭제를 의미하지 않습니다. 질문에 답한 후 제거되는 대신, 프로토타입은 main 밖의 일회용 브랜치(`prototype/<name>`)에 실행 가능한 증거로 보존되며, 구현 이슈에 그것을 가리키는 컨텍스트 포인터가 남습니다. 그래서 main 브랜치는 검증된 결정만 유지하면서 탐색은 여전히 찾을 수 있습니다. 답(판정 + 질문)은 여전히 이슈/ADR/커밋에 지속적으로 보존됩니다.

- [#536](https://github.com/mattpocock/skills/pull/536) [`42a5b70`](https://github.com/mattpocock/skills/commit/42a5b70fcacc7baff1977b13f3919fb2f63af14e) [@mattpocock](https://github.com/mattpocock) 님께 감사드립니다! - 스킬 세트를 Claude Code의 공식 마켓플레이스에 등록된 네이티브 **Claude Code 플러그인**으로 배포합니다. 이제 편집 가능한 파일을 복사하는 대신, 승격된 스킬을 관리형 읽기 전용 번들로 구독할 수 있습니다.

  ```bash
  claude plugins install mattpocock-skills
  ```

  또는, 세션 내에서:

  ```
  /plugin install mattpocock-skills
  ```

  먼저 추가할 마켓플레이스는 없습니다. 공식 마켓플레이스가 기본적으로 구성되어 있습니다.

  `.claude-plugin/plugin.json`은 전체 플러그인 메타데이터(버전, 설명, 작성자, 라이선스, 키워드)와 승격된 스킬의 명시적인 목록을 담습니다. `skills.sh`는 범용 설치 도구(그리고 현재 Codex와 다른 하네스를 위한 경로)로 남습니다. 네이티브 Codex 플러그인은 보류되었으며, 그 이유는 `.agents/adr/0002-ship-as-a-claude-code-plugin.md`를 참조하십시오.

- [#751](https://github.com/mattpocock/skills/pull/751) [`355fa74`](https://github.com/mattpocock/skills/commit/355fa7420b418af838998f7ec4365ceda1c8dfcc) [@mattpocock](https://github.com/mattpocock) 님께 감사드립니다! - 모델의 장황함에 대한 한 단어짜리 교정 수단인 **`wait-what`**을 추가합니다. 메시지가 이해되지 않는 순간 입력하면, 에이전트가 약간의 맥락, ASD-STE100 간이 기술 영어, 그리고 `CONTEXT.md`의 유비쿼터스 언어로 다시 설명합니다. 사용자 호출이며, 세 줄짜리입니다.

  작동 원리는 이름입니다. 간결성 스킬은 커지면서 실패합니다. 400줄짜리 스킬은 여전히 모델을 장황하게 둡니다. 그래서 이 스킬은 하나의 정밀한 핵심 단어이며 그 외에는 아무것도 없습니다. _출력_을 기술하는 이름(`/tldr`, `/no-fluff`)은 모델이 단어를 잘라 내어 사용자를 더 멀리 잃게 만듭니다. _듣는 사람_의 상태를 명명하면 두 가지를 동시에 요청하게 됩니다. 더 적은 단어 **그리고** 부족했던 맥락입니다. 또한 전역 `CLAUDE.md`에 이미 있는 핵심 단어를 재사용하므로, 스킬, `CLAUDE.md`, 모든 `CONTEXT.md`가 같은 토큰을 사용합니다.

  하나의 메시지를 고칠 뿐, 다음 메시지를 막지는 않습니다. 전문 용어에 대한 치료법은 `/grill-with-docs`로 미리 구축한 공유 언어이며, 이것은 아직 그것이 없을 때 사용하는 것입니다.

- [#763](https://github.com/mattpocock/skills/pull/763) [`77d207e`](https://github.com/mattpocock/skills/commit/77d207ef03219cc603e2832e1159cbdd1c91818e) [@mattpocock](https://github.com/mattpocock) 님께 감사드립니다! - `/wayfinder`의 단위를 **결정 티켓(decision ticket)**으로 명명하고, 서브에이전트로 조사 티켓을 처리합니다.

  wayfinder는 티켓을 **결정 티켓**, 즉 해결 결과가 결정인 질문으로 사용하는데, 사람들은 계속 wayfinder 티켓을 일반적인 _구현_ 티켓, 즉 실행할 빌드의 슬라이스로 읽었습니다. 스킬 description과 그 첫 줄이 이제 이 용어를 도입하며(그리고 무엇이 그것을 결정 티켓으로 만드는지 말하며), `ask-matt` / 엔지니어링 README 요약과 문서 페이지도 이에 맞춥니다. 용어가 확립된 후에는 "티켓"이 일상적인 단어로 남습니다. `CONTEXT.md`는 **Decision ticket**을 도메인 용어로 기록하므로, "사용하지 말 것: ticket" 지침이 더 이상 wayfinder의 의도적인 단어 사용과 모순되지 않습니다.

  조사 티켓은 더 이상 별도로 시작하는 세션을 위해 보류되지 않습니다. 조사는 여전히 실제 티켓 유형입니다. 하류의 결정들이 달려 있는 진정한 공유 차단 요소이며, 그 의존성이 바로 전선의 차단 관계가 보여 주기 위해 존재하는 것입니다. 바뀌는 것은 해결 방식입니다. 조사는 AFK이므로, 지도 그리기가 멈추고 그것을 읽지 않습니다. 티켓을 생성한 후, 지도 그리기 세션은 각 조사 티켓에 대해 `/research` 서브에이전트를 실행하여 병렬로 처리하며, 결과를 컨텍스트 포인터와 함께 일회용 `research/<name>` 브랜치에 기록합니다. 조사 티켓은 _세션당 하나의 티켓_의 유일한 예외입니다.

- [#763](https://github.com/mattpocock/skills/pull/763) [`77d207e`](https://github.com/mattpocock/skills/commit/77d207ef03219cc603e2832e1159cbdd1c91818e) [@mattpocock](https://github.com/mattpocock) 님께 감사드립니다! - **호환성 파괴:** **`writing-great-skills`**의 이름을 **`writing-for-agents`**로 바꾸고, 재구성하며, 새로운 핵심 단어를 추가합니다.

  이 참조는 이제 스킬뿐만 아니라 에이전트가 사용하는 모든 문서, 즉 스킬, `AGENTS.md` / `CLAUDE.md`, 포인터로 도달하는 문서를 다룹니다. `GLOSSARY.md`는 `SKILL.md`에 병합되었습니다(용어당 하나의 권위 있는 설명. `_Avoid_` 동의어 목록과 독립적인 Predictability 정의는 사라졌습니다). 스킬 전용 작동 방식(프런트매터, 모델 호출 대 사용자 호출, 라우터 스킬, 분할의 호출 기준)은 새로운 `SKILL-MECHANICS.md`로 공개됩니다. 스킬은 이제 **모델 호출**입니다. 스킬을 생성하거나 편집할 때, 또는 `AGENTS.md`/`CLAUDE.md`를 수정할 때 실행됩니다. `ask-matt`의 포인터가 업데이트되었습니다. 새 이름으로 다시 설치하십시오. 이전 이름은 사라졌습니다(별칭 없음).

  가지치기 섹션에 **캐시(cache)**가 추가됩니다. 단일 진실 공급원이 이제 문서를 넘어 환경까지 확장됩니다. `package.json` 스크립트, 구성 파일, 디렉터리 구조, `--help` 출력은 그 자체로 권위가 있으므로, 그것을 다시 진술하는 문서는 조회 결과의 캐시이며, 조회 비용이 클 때만 그 부하를 감당할 자격이 있습니다. 긍정적인 목표: 에이전트가 살펴보아서는 찾을 수 없는 것(문서화되지 않은 관례, 선택의 이면에 있는 이유, 어떤 구성 파일도 알려 주지 않는 함정)을 캐시하고, 파일 하나, 명령 하나로 조회할 수 있는 것은 낡을 수 없는 환경에 맡기십시오.

- [#533](https://github.com/mattpocock/skills/pull/533) [`45afd80`](https://github.com/mattpocock/skills/commit/45afd8074a8b7de5fe073845d080fa9dd6c429fa) [@mattpocock](https://github.com/mattpocock) 님께 감사드립니다! - **`improve-codebase-architecture`** 스킬의 탐색 단계에 YAGNI 범위 필터를 추가합니다. 저장소 전체를 고르게 탐색하는 대신, 이제 변경이 실제로 일어나고 있는 곳으로 범위를 정합니다. 방향을 지정하면 그것을 따르고, 그렇지 않으면 최근 약 20개의 커밋 메시지를 읽어 활발히 개발되는 경로 쪽으로 탐색을 치우치게 합니다. 아무도 건드리지 않는 코드의 심화 기회는 결코 현금화하지 못할 리팩터링입니다. 레버리지는 계속 편집하는 곳에서만 보답하므로, 보고서는 저장소의 휴면 구석을 정리하는 것을 멈춥니다.

### 패치 변경 사항

- [#763](https://github.com/mattpocock/skills/pull/763) [`77d207e`](https://github.com/mattpocock/skills/commit/77d207ef03219cc603e2832e1159cbdd1c91818e) [@mattpocock](https://github.com/mattpocock) 님께 감사드립니다! - `/ask-matt`를 다듬습니다. 라우터는 이제 단계 경계, 두 가지 wayfinder 실수, 그리고 한 번도 언급하지 않았던 두 스킬을 다룹니다.

  **단계 경계.** **단계(phase)**는 세션 내의 작업 덩어리(그릴링, 구현, QA)이며, 두 단계 사이의 경계는 구축한 컨텍스트로 무엇을 할지 결정하는 곳입니다. 두 개의 글머리 기호로 된 `Crossing sessions` 섹션은 다섯 가지 선택지(**계속**, `/clear`, `/handoff`, **서브에이전트**, `/compact`)를 순서대로 담은 결정 트리로 대체되며, 그 근거는 새로운 `PHASE-BOUNDARIES.md`에 공개됩니다. 세 가지 수정이 함께 옵니다.

  - **`/handoff`가 과대 포장되었습니다.** 컨텍스트 윈도우 사이의 일반적인 다리처럼 읽혔습니다. 용도가 좁습니다. 무언가가 _이동해야_ 할 때만 필요합니다. 새 하네스, 새 디렉터리, 동료, 또는 단계 중간에 분기한 곁가지 작업입니다. 얻는 것은 이식성입니다.
  - **`/compact`는 첫 번째로 손을 뻗는 선택이 아니라 기본값입니다.** 그 위의 더 저렴하거나 더 정밀한 네 가지 질문 다음, 트리의 맨 아래에 있습니다. 거기서 시작하면 요약이 납작하게 만든 것에 대해 자신 있게 틀리는 세션이 만들어집니다.
  - **두 개의 분기가 완전히 빠져 있었습니다.** **계속**은 가장 먼저 배제해야 할 것입니다. 대화를 요약이 아니라 1차 자료로 유지하는 유일한 수이기 때문입니다. 그리고 **서브에이전트**는 AFK로 실행될 만큼 범위가 좁게 한정된 모든 것을 처리합니다.

  컨텍스트 위생의 탈출구는 이제 `/handoff`가 아니라 `/compact`라고 말하며(같은 하네스, 같은 디렉터리, 경계에서이므로 handoff 조항이 적용되지 않음), smart zone 수치는 약 120k에서 약 150k 토큰으로 업데이트됩니다.

  **Wayfinder 라우팅.** 가장 무겁고 인지적으로 가장 까다로운 흐름에서 사람들이 가장 자주 하는 두 가지 실수:

  - **과도하게 사용함.** 단일 그릴링보다 느리고 밀도가 높으므로, 가장 무거운 흐름으로 표시되며 진정으로 한 세션에 들어가지 않는 아이디어를 위해 남겨 둡니다. 범위가 잘 정해진 기능은 여기가 아니라 `/grill-with-docs`에 속합니다.
  - **인계에서 길을 잃음.** 지도가 명확해지면, wayfinder는 구현하지 않고 인계합니다. 지도를 곧바로 `/implement`로 넘기지 말고, `/to-spec`(지도의 연결된 결정들을 구현 가능한 계획으로 압축함)에서 주 흐름에 합류하십시오. 바로 `/implement`로 가는 것은 실제로 작은 것으로 밝혀진 작업에만 해당합니다.

  **빠진 경로.** `/grilling`과 `/resolving-merge-conflicts`는 라우터에서 완전히 빠져 있었으며 이제 포함되었고, `grill-me`는 작업 디렉터리에 있는지 여부에 따라 `grill-with-docs`와 구분됩니다.

- [#502](https://github.com/mattpocock/skills/pull/502) [`44eed54`](https://github.com/mattpocock/skills/commit/44eed545186ffd0263e8004867750b80cfddd215) [@mattpocock](https://github.com/mattpocock) 님께 감사드립니다! - `/setup-matt-pocock-skills`를 더 친절하게 만들고 로컬 마크다운 트래커를 현재 명세에 맞춥니다.

  - **트리아지 라벨**은 이제 `triage` 스킬이 설치된 경우에만 묻고, 그때도 재정의 심문 대신 권장 답이 '예'인 하나의 질문("기본 트리아지 라벨을 유지하시겠습니까?")으로 묻습니다. `triage`가 설치되지 않은 경우, 그 섹션과 `docs/agents/triage-labels.md`는 건너뜁니다.
  - **요청 창구로서의 외부 PR**은 더 이상 설정 질문이 아닙니다. GitHub/GitLab 템플릿은 여전히 기본값이 꺼짐인 플래그를 담고 있으며, 사용자는 나중에 `docs/agents/issue-tracker.md`에서 그것을 바꿀 수 있습니다.
  - **도메인 문서**는 묻지 않고 단일 컨텍스트를 기본으로 하며, 다중 컨텍스트는 저장소가 모노레포 신호를 보일 때만 제안됩니다.
  - **로컬 마크다운 티켓**은 이제 `.scratch/<feature>/issues/<NN>-<slug>.md` 아래에 티켓당 하나의 파일이며, 결코 하나로 합친 `tickets.md`가 아닙니다. `/to-tickets`와 로컬 이슈 트래커 템플릿이 이제 일치하며, 명세 파일은 `/to-spec`에 맞추어 (`PRD.md`가 아니라) `spec.md`입니다.

  `setup-matt-pocock-skills`와 `to-tickets`의 문서 페이지가 다시 동기화되었습니다.

- [#532](https://github.com/mattpocock/skills/pull/532) [`170ad48`](https://github.com/mattpocock/skills/commit/170ad48655825783d0193e850e31a9aac957bb95) [@mattpocock](https://github.com/mattpocock) 님께 감사드립니다! - 범용 사용을 위해 **`grilling`**의 문구를 바꿉니다. description과 본문은 더 이상 인터뷰를 소프트웨어 계획으로 한정하지 않습니다. "this plan" → "this", "enact the plan" → "act on it", "exploring the codebase" → "exploring the environment"입니다. 기법은 바뀌지 않았으며, 이제 어떤 계획, 결정, 아이디어든 스트레스 테스트하는 것으로 읽힙니다.

- [#593](https://github.com/mattpocock/skills/pull/593) [`a4b2009`](https://github.com/mattpocock/skills/commit/a4b2009a1a3ac9575506c10b4c84f08f9bba7a38) [@mattpocock](https://github.com/mattpocock) 님께 감사드립니다! - **`grilling`**을 한 번에 하나의 질문에서 라운드 단위로 다시 작업합니다. 이제 결정 트리를 매핑하고 **전선** 전체, 즉 전제 조건이 이미 확정된 모든 질문을 하나의 번호 매긴 라운드로 물은 다음, 사용자의 답에서 전선을 다시 계산하고 다음 라운드를 묻습니다. 같은 13개의 질문이 13번이 아니라 약 3번의 라운드에 나옵니다. 환경이 답할 수 있는 사실은 백그라운드 서브에이전트에게 디스패치되므로 조사가 라운드를 막지 않습니다. 실행 중인 탐색의 하류에 있는 질문만 그것을 기다립니다. 전선이 비면 세션이 끝납니다.

  라운드의 모든 질문은 하나의 고정된 형태로 출력됩니다. `❓ **Q1** - **<title>**`, 그다음 본문(산문 또는 여러 선택지), 그다음 자체 `➡️` 줄의 권장 답변입니다. 라운드는 각 권장 답변이 질문과 시각적으로 분리된, 훑어보기 쉬운 번호 매긴 목록으로 읽히므로, 질문을 인용하는 대신 번호로 답할 수 있습니다.

  `grill-me`, `grill-with-docs`, `triage`도 한 번에 한 라운드씩 전선을 실행합니다. `triage`의 그릴링 단계와 `grilling`의 Codex `short_description`이 이제 이전 리듬을 기술하는 대신 그렇게 말합니다. 한 번에 하나의 질문으로 돌아가는 옵트아웃(전역 `CLAUDE.md`의 한 줄)은 바뀌지 않았습니다.

- [#752](https://github.com/mattpocock/skills/pull/752) [`c66bdee`](https://github.com/mattpocock/skills/commit/c66bdeeee002d81e3f8b21403c07f9a0d7bea6da) [@mattpocock](https://github.com/mattpocock) 님께 감사드립니다! - 저장소에서 여섯 개의 스킬을 제거합니다. 그중 어느 것도 Claude Code 플러그인에 없었지만, 여섯 개 모두 저장소의 모든 스킬을 제공하는 [skills.sh](https://skills.sh/mattpocock/skills)를 통해 설치할 수 있었습니다. 그래서 이것이 그 목록에서 빠지는 것이며, 각각이 어디로 갔는지입니다.

  네 개의 폐기된 스킬은 각각 그 일을 더 잘하는 스킬에 이미 흡수되었습니다.

  - **`ubiquitous-language`** → **`/domain-modeling`**. 하나의 대화에서 용어집을 쏟아 내는 대신 도메인 모델 전체를 구축하고 유지합니다.
  - **`design-an-interface`** → **`/codebase-design`**. 잃는 것은 없습니다. "두 번 설계하라" 기법(Ousterhout에게서 가져온, 근본적으로 다른 설계를 만드는 병렬 서브에이전트)이 그 스킬 안에 `DESIGN-IT-TWICE.md`로 포함되어 있습니다.
  - **`qa`** → **`/triage`**와 **`/to-tickets`**.
  - **`request-refactor-plan`** → **`/to-spec`**과 **`/improve-codebase-architecture`**.

  그리고 오직 제 것이었던 두 개입니다. 제 머신에 묶여 있었으며 다른 사람을 위한 것이 결코 아니었습니다. `personal/` 버킷도 함께 사라집니다.

  - **`edit-article`**
  - 제 Obsidian 볼트 경로를 하드코딩한 **`obsidian-vault`**.

  `skills/deprecated/`는 이제 빈 버킷으로 남습니다. `skills/in-progress/`는 바뀌지 않았으며 이제 실제로 그것이 무엇인지에 맞게 기술됩니다. 의도적으로 게시되며, skills.sh를 통해 한 번에 하나의 스킬씩 설치할 수 있는 베타 채널입니다.

- [#734](https://github.com/mattpocock/skills/pull/734) [`a2f9333`](https://github.com/mattpocock/skills/commit/a2f9333669ff53db762c87ecda5a15442060a3be) [@mattpocock](https://github.com/mattpocock) 님께 감사드립니다! - `to-prd` → `to-spec` 이름 변경을 마무리합니다. "spec"이 이제 배포되는 텍스트의 유일한 용어입니다.

  - **`to-spec`**은 더 이상 "이 문서를 PRD로 알고 있을 수도 있다"로 시작하지 않습니다. 그 괄호 문구는 스킬과 문서 페이지에서 제거되었습니다. 로컬 마크다운 트래커 템플릿도 같은 단서를 제거합니다.
  - **`code-review`**는 프런트매터 description, 두 축 요약, 명세 출처 검색 순서에서 이슈/PRD가 아니라 원래의 이슈/명세에 대해 말합니다. 두 README가 다시 동기화되었습니다.
  - **GitHub와 GitLab 트래커 템플릿**은 이제 "이 저장소의 이슈와 명세는 GitHub/GitLab 이슈로 존재한다"고 말합니다. 로컬 템플릿이 업데이트될 때 "PRDs"에 남겨져 있었으므로, 낡은 용어가 그것들이 작성된 모든 저장소로 퍼졌습니다.
  - **`docs/engineering/research.md`**는 이름이 바뀐 스킬의 죽은 슬러그인 `https://aihero.dev/skills-to-prd`를 가리켰습니다. 이제 다른 열아홉 개의 문서 페이지처럼 `to-spec`에 링크합니다.

  CHANGELOG와 기존 체인지셋은 이름 변경 자체를 문서화하는 곳에서 여전히 PRD를 명시하며, 이는 올바릅니다.

## 1.1.0 및 이전 버전

1.1.0 이하 버전의 변경 사항은 아직 번역되지 않았습니다. 원문 [CHANGELOG.md](./CHANGELOG.md)를 참조하십시오.
