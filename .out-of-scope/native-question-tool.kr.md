# 하네스의 네이티브 질문 도구를 통한 그릴링

그릴링(grilling) 세션(`/grilling`, `/grill-me`, `/grill-with-docs`, 그리고 다른 스킬 내부의 그릴링)은 질문을 일반 채팅 텍스트로 묻습니다. 이를 하네스의 내장 질문 UI(Claude Code의 `AskUserQuestion`, 호스트의 "질문 도구", 구조화되거나 일괄 처리되는 설문 모드)를 통해 전달해 달라는 요청은 범위에서 제외됩니다.

## 범위에서 제외되는 이유

이 스킬들은 하네스 중립적인 텍스트입니다. Claude Code, Codex, Copilot, Cursor, 그리고 skills.sh가 설치하는 그 밖의 모든 환경에서 실행되며, 각 하네스는 서로 다른 질문 도구를 가지고 있거나, 아예 없습니다. 스킬에서 특정 하네스의 도구를 명시하면, 모든 그릴링 스킬에 하네스별 분기를 두거나, 한 곳에서만 제대로 동작하는 스킬이 되는 결과를 낳습니다.

질문 UI는 그릴링 자체도 바꿉니다. 구조화된 선택기는 모델이 미리 만들어진 답이 있는 객관식 질문을 하도록 유도하는데, 이는 그릴링의 목적과 정반대입니다. 그릴링은 사용자가 자신의 말로 답하는 열린 질문을, 결정 트리의 한 가지씩 차례로 다루는 것입니다. 저는 `AskUserQuestion` UI를 시도해 보았으며, 이 스킬들에 그것을 넣고 싶지 않습니다.

하네스의 질문 도구를 선호한다면, 본인의 `CLAUDE.md` / `AGENTS.md`에 그렇게 명시하십시오("그릴링할 때는 AskUserQuestion으로 질문하라"). 이는 한 줄짜리 사용자별 선호이며, 공유 스킬이 이를 알 필요는 없습니다.

## 이전 요청

- #19: "grill-me: not always using the question tool"
- #643: "Proposal: Use AskQuestion for structured input during grilling sessions"
- #840: "Use host's question tool for grilling sessions"
- #1107: "Grilling doesn't use Agent's native QA tool OOTB"
- #1152: "Proposal: experimental HTML questionnaire mode for batch grilling"
