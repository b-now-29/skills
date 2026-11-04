# 이슈 트래커: GitHub

이 저장소의 이슈와 명세는 GitHub 이슈로 존재합니다. 모든 작업에 `gh` CLI를 사용하십시오.

## 규칙

- **이슈 생성**: `gh issue create --title "..." --body "..."`. 여러 줄의 본문에는 heredoc을 사용하십시오.
- **이슈 읽기**: `gh issue view <number> --json number,title,body,labels,comments`.
- **이슈 목록**: 적절한 `--label` 및 `--state` 필터와 함께 `gh issue list --state open --json number,title,body,labels,comments --jq '[.[] | {number, title, body, labels: [.labels[].name], comments: [.comments[].body]}]'`.
- **이슈를 상위 이슈의 하위 이슈로 만들기**: `gh issue create --parent <parent> ...`, 또는 사후에 `gh issue edit <parent> --add-sub-issue <child>`(`gh` 2.94 이상). 이전 버전의 `gh`: `gh api --method POST repos/<owner>/<repo>/issues/<parent>/sub_issues -F sub_issue_id=<child-db-id>`(아래 **차단**에서와 같은 데이터베이스 id). 하위 이슈 기능이 없다면, 하위 이슈 본문 맨 위에 `Part of #<parent>`를 넣으십시오.
- **차단**: GitHub의 **네이티브 이슈 의존성**으로, UI에서 보이는 표준 표현입니다. `gh issue create --blocked-by <n>,<n> ...` 또는 `gh issue edit <child> --add-blocked-by <blocker>`(`gh` 2.94 이상)로 관계를 추가하십시오. 이전 버전의 `gh`: `gh api --method POST repos/<owner>/<repo>/issues/<child>/dependencies/blocked_by -F issue_id=<blocker-db-id>`. 여기서 `<blocker-db-id>`는 차단하는 이슈의 숫자 **데이터베이스 id**입니다(`gh api repos/<owner>/<repo>/issues/<n> --jq .id`, `#number`나 `node_id`가 _아님_). 의존성 기능을 사용할 수 없다면, 하위 이슈 본문 맨 위에 `Blocked by: #<n>, #<n>` 줄을 두는 방식으로 대체하십시오. 모든 차단 이슈가 종료되면 티켓의 차단이 해제됩니다.
- **열린 차단 이슈 수 세기**: `gh api repos/<owner>/<repo>/issues/<n> --jq .issue_dependencies_summary.blocked_by`(열린 차단 이슈만, 0이면 시작 가능). `gh issue view <n> --json blockedBy`는 종료된 차단 이슈도 나열하므로 필터링하십시오: `--jq '[.blockedBy.nodes[] | select(.state == "OPEN")] | length'`.
- **이슈에 댓글 달기**: `gh issue comment <number> --body "..."`
- **라벨 적용 / 제거**: `gh issue edit <number> --add-label "..."` / `--remove-label "..."`
- **종료**: `gh issue comment <number> --body "..."`로 설명을 게시한 다음, `gh issue close <number>`. 이미 종료된 이슈에서 `gh issue close --comment`는 댓글을 버리면서도 종료 코드 0을 반환합니다.

저장소는 `git remote -v`에서 추론하십시오. `gh`는 클론 내부에서 실행될 때 이를 자동으로 수행합니다.

이슈는 사용자 자신의 저장소에만 제출하십시오. 사용자가 소유하지 않는 한 `mattpocock/skills`(이 스킬들의 출처 저장소)에는 절대 제출하지 마십시오. 포크에서는 `gh`가 업스트림 상위 저장소를 기본값으로 삼을 수 있으므로, 세션의 첫 번째 `gh issue create` 전에 `gh repo view --json nameWithOwner`로 대상을 확인하고, 사용자의 저장소가 아니라면 사용자에게 확인하십시오.

## 트리아지 창구로서의 풀 리퀘스트

**요청 창구로서의 PR: 아니요.** _(이 저장소가 외부 PR을 기능 요청으로 취급한다면 `yes`로 설정하십시오. `/triage`가 이 플래그를 읽습니다.)_

`yes`로 설정하면, PR은 `gh pr`의 동등한 명령을 사용하여 이슈와 같은 라벨과 상태를 거칩니다.

- **PR 읽기**: `gh pr view <number>`, 그다음 `gh pr view <number> --comments`(TTY가 아닌 환경에서 `--comments`는 본문이 아니라 댓글만 출력합니다), 그리고 diff를 위해 `gh pr diff <number>`.
- **트리아지할 외부 PR 목록**: `gh api --paginate 'repos/{owner}/{repo}/pulls?state=open' --jq '.[] | select(.author_association | IN("OWNER","MEMBER","COLLABORATOR") | not) | {number, title, author: .user.login, author_association, labels: [.labels[].name]}'`.
- **댓글 / 라벨 / 종료**: `gh pr comment`, `gh pr edit --add-label`/`--remove-label`, `gh pr close`.

GitHub는 이슈와 PR에 하나의 번호 공간을 공유하므로, 단순한 `#42`는 둘 중 어느 것일 수도 있습니다. `gh pr view 42`로 확인하고, 실패하면 `gh issue view 42`로 대체하십시오.

## 스킬이 "이슈 트래커에 게시하라"고 할 때

GitHub 이슈를 생성하십시오.

## 스킬이 "관련 티켓을 가져오라"고 할 때

위의 **이슈 읽기**와 같이 읽으십시오.

## Wayfinding 작업

`/wayfinder`가 사용합니다. **지도(map)**는 **하위(child)** 이슈를 티켓으로 가지는 하나의 이슈입니다.

- **지도**: `wayfinder:map` 라벨이 붙은 하나의 이슈로, Notes / Decisions-so-far / Fog 본문을 담습니다. `gh issue create --label wayfinder:map`.
- **하위 티켓**: GitHub 하위 이슈로 지도에 연결된 이슈입니다(**이슈를 상위 이슈의 하위 이슈로 만들기** 참조). 하위 이슈 기능이 활성화되지 않은 경우, 지도 본문의 작업 목록에 하위 이슈를 추가하고 하위 이슈 본문 맨 위에 `Part of #<map>`을 넣으십시오. 라벨: `wayfinder:<type>`(`research`/`prototype`/`grilling`/`task`). 맡게 되면, 티켓은 진행하는 개발자에게 할당됩니다.
- **차단**: 규칙 아래의 **차단**을 참조하십시오.
- **전선 조회**: 지도의 열린 하위 이슈를 나열하고(`gh issue list --state open`, 지도의 하위 이슈 / 작업 목록으로 범위를 한정), 열린 차단 이슈가 있는 것(**열린 차단 이슈 수 세기** 참조, 또는 `Blocked by` 줄의 열린 이슈)이나 담당자가 있는 것을 제외하십시오. 지도 순서상 첫 번째 것이 선택됩니다.
- **맡기**: `gh issue edit <n> --add-assignee @me`. 세션의 첫 번째 쓰기 작업입니다.
- **해결**: `gh issue comment <n> --body "<answer>"`, 그다음 `gh issue close <n>`, 그다음 지도의 Decisions-so-far에 컨텍스트 포인터(요지 + 링크)를 덧붙입니다.
