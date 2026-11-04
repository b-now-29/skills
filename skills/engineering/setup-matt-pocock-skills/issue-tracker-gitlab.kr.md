# 이슈 트래커: GitLab

이 저장소의 이슈와 명세는 GitLab 이슈로 존재합니다. 모든 작업에 [`glab`](https://gitlab.com/gitlab-org/cli) CLI를 사용하십시오.

## 규칙

- **이슈 생성**: `glab issue create --title "..." --description "..."`. 여러 줄의 설명에는 heredoc을 사용하십시오. 편집기를 열려면 `--description -`를 전달하십시오.
- **이슈 읽기**: `glab issue view <number> --comments`. 기계가 읽을 수 있는 출력에는 `-F json`을 사용하십시오.
- **이슈 목록**: 적절한 `--label` 필터와 함께 `glab issue list -O json`.
- **이슈에 댓글 달기**: `glab issue note <number> --message "..."`. GitLab은 댓글을 "노트(notes)"라고 부릅니다.
- **라벨 적용 / 제거**: `glab issue update <number> --label "..."` / `--unlabel "..."`. 여러 라벨은 쉼표로 구분하거나 플래그를 반복하여 지정할 수 있습니다.
- **종료**: `glab issue close <number>`. `glab issue close`는 종료 댓글을 받지 않으므로, 먼저 `glab issue note <number> --message "..."`로 설명을 게시한 다음 종료하십시오.
- **머지 리퀘스트**: GitLab은 PR을 "머지 리퀘스트(merge requests)"라고 부릅니다. `glab mr create`, `glab mr view`, `glab mr note` 등을 사용하십시오. `gh pr ...`과 같은 형태이며, `pr` 대신 `mr`을, `comment`/`--body` 대신 `note`/`--message`를 사용합니다.

저장소는 `git remote -v`에서 추론하십시오. `glab`은 클론 내부에서 실행될 때 이를 자동으로 수행합니다.

## 트리아지 창구로서의 머지 리퀘스트

**요청 창구로서의 MR: 아니요.** _(이 저장소가 외부 머지 리퀘스트를 기능 요청으로 취급한다면 `yes`로 설정하십시오. `/triage`가 이 플래그를 읽습니다.)_

`yes`로 설정하면, MR은 `glab mr`의 동등한 명령을 사용하여 이슈와 같은 라벨과 상태를 거칩니다.

- **MR 읽기**: `glab mr view <number> --comments`, 그리고 diff를 위해 `glab mr diff <number>`.
- **트리아지할 외부 MR 목록**: `glab mr list -O json`을 실행한 다음, 작성자가 프로젝트 멤버/소유자가 아닌 MR만 남기십시오(유지 관리자의 진행 중인 작업이 아니라 기여자의 MR).
- **댓글 / 라벨 / 종료**: `glab mr note`, `glab mr update --label`/`--unlabel`, `glab mr close`.

GitHub와 달리 GitLab은 이슈와 MR에 번호를 따로 매기므로, 유지 관리자가 어느 창구를 의미하는지 알면 `#42`는 모호하지 않습니다.

## 스킬이 "이슈 트래커에 게시하라"고 할 때

GitLab 이슈를 생성하십시오.

## 스킬이 "관련 티켓을 가져오라"고 할 때

`glab issue view <number> --comments`를 실행하십시오.

## Wayfinding 작업

`/wayfinder`가 사용합니다. **지도(map)**는 **하위(child)** 이슈를 티켓으로 가지는 하나의 이슈입니다.

- **지도**: `wayfinder:map` 라벨이 붙은 하나의 이슈로, Notes / Decisions-so-far / Fog 본문을 담습니다. `glab issue create --label wayfinder:map`. (네이티브 에픽이 있는 GitLab 등급에서는 에픽이 대신 지도를 담을 수 있습니다. 라벨이 붙은 이슈는 어디서나 동작합니다.)
- **하위 티켓**: 설명 맨 위에 `Part of #<map>`을 담고, 지도에 연결되며(`glab issue create --linked-issues <map> --link-type relates_to`), `wayfinder:<type>`(`research`/`prototype`/`grilling`/`task`) 라벨을 가진 이슈입니다. 맡게 되면, 티켓은 진행하는 개발자에게 할당됩니다.
- **차단**: GitLab의 **네이티브 차단 링크**로, UI에서 보이는 표준 표현입니다. `/blocked_by #<n>` 빠른 액션을 노트로 게시하여 추가하십시오(`glab issue note <child> --message "/blocked_by #<blocker>"`). 네이티브 차단 링크는 Premium/Ultimate 기능입니다. 무료 등급(또는 사용할 수 없는 경우)에서는 설명 맨 위에 `Blocked by: #<n>, #<n>` 줄을 두는 방식으로 대체하십시오. 모든 차단 이슈가 종료되면 티켓의 차단이 해제됩니다.
- **전선 조회**: `glab api projects/:id/issues/<map>/links`로 지도의 하위 이슈를 나열하고, `wayfinder:<type>` 라벨을 가진 열린 이슈만 남긴 다음, 열린 차단 이슈가 있는 것을 제외하십시오. 열린 이슈로의 네이티브 `blocked_by` 링크(`glab api projects/:id/issues/<child-iid>/links`), `Blocked by` 줄의 열린 이슈, 또는 담당자가 있는 경우입니다. 지도 순서상 첫 번째 것이 선택됩니다.
- **맡기**: `glab issue update <n> --assignee @me`. 세션의 첫 번째 쓰기 작업입니다.
- **해결**: `glab issue note <n> --message "<answer>"`, 그다음 `glab issue close <n>`, 그다음 지도의 Decisions-so-far에 컨텍스트 포인터(요지 + 링크)를 덧붙입니다.
