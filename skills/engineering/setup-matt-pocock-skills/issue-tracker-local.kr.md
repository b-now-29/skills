# 이슈 트래커: 로컬 마크다운

이 저장소의 이슈와 명세는 `.scratch/`에 마크다운 파일로 존재합니다.

## 규칙

- 디렉터리당 하나의 기능: `.scratch/<feature-slug>/`
- 명세는 `.scratch/<feature-slug>/spec.md`입니다
- 구현 이슈는 `.scratch/<feature-slug>/issues/<NN>-<slug>.md`에 티켓당 하나의 파일로 두며, `01`부터 번호를 매깁니다. 하나로 합친 티켓 파일은 절대 사용하지 않습니다
- 트리아지 상태는 각 이슈 파일 상단 근처의 `Status:` 줄에 기록됩니다(역할 문자열은 `triage-labels.md` 참조)
- 댓글과 대화 이력은 파일 하단의 `## Comments` 제목 아래에 덧붙입니다

## 스킬이 "이슈 트래커에 게시하라"고 할 때

`.scratch/<feature-slug>/` 아래에 새 파일을 생성하십시오(필요하면 디렉터리도 생성).

## 스킬이 "관련 티켓을 가져오라"고 할 때

참조된 경로의 파일을 읽으십시오. 사용자는 대개 경로나 이슈 번호를 직접 전달합니다.

## Wayfinding 작업

`/wayfinder`가 사용합니다. **지도(map)**는 티켓당 하나의 **하위(child)** 파일을 가지는 하나의 파일입니다.

- **지도**: `.scratch/<effort>/map.md`(Notes / Decisions-so-far / Fog 본문).
- **하위 티켓**: `.scratch/<effort>/issues/NN-<slug>.md`, `01`부터 번호를 매기며, 본문에 질문이 있습니다. `Type:` 줄은 티켓 유형(`research`/`prototype`/`grilling`/`task`)을 기록하고, `Status:` 줄은 `claimed`/`resolved`를 기록합니다.
- **차단**: 상단 근처의 `Blocked by: NN, NN` 줄. 나열된 모든 파일이 `resolved`이면 티켓의 차단이 해제됩니다.
- **전선**: `.scratch/<effort>/issues/`에서 열려 있고, 차단되지 않았으며, 아무도 맡지 않은 파일을 찾으십시오. 번호상 첫 번째 것이 선택됩니다.
- **맡기**: 어떤 작업을 하기 전에 `Status: claimed`로 설정하고 저장하십시오.
- **해결**: `## Answer` 제목 아래에 답을 덧붙이고, `Status: resolved`로 설정한 다음, `map.md`의 Decisions-so-far에 컨텍스트 포인터(요지 + 링크)를 덧붙이십시오.
