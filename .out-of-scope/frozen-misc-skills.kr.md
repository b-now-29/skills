# `misc/` 스킬에 대한 변경

`skills/misc/` 아래의 스킬(`git-guardrails-claude-code`, `migrate-to-shoehorn`, `scaffold-exercises`, `setup-pre-commit`, 그리고 그곳에 들어오는 그 밖의 모든 스킬)은 동결되어 있습니다. 이들에 대한 버그 보고, 기능 요청, PR은 종료 처리됩니다.

## 범위에서 제외되는 이유

`misc/`는 보관은 하지만 거의 사용하지 않는 스킬이 가는 곳입니다. 이 스킬들은 승격되지 않았습니다. 즉, Claude Code 플러그인에 포함되어 배포되지 않고, 문서 페이지도 없으며, 저는 이 스킬들을 매일 실행하지 않으므로 수정 사항이 올바른지 판단하거나 수정 사항이 다른 무언가를 망가뜨리는 것을 알아챌 수 없습니다. 이 스킬들을 승격된 스킬과 같은 기준으로 유지 관리하려면 사용량은 극히 일부에 불과한데도 승격된 스킬과 같은 비용이 듭니다.

이 스킬들은 일부 사람들에게는 여전히 있는 그대로 동작하므로, 유지 관리되지 않은 상태로 저장소에 남아 있습니다. 어떤 스킬이 동작하지 않는다면 skills.sh로 설치한 뒤 본인의 사본을 수정하십시오. 해당 파일은 사용자가 자유롭게 편집할 수 있습니다.

나중에 `misc/` 스킬이 `engineering/` 또는 `productivity/`로 다시 승격되면, 그 시점부터 다시 범위에 포함됩니다.

## 이전 요청

- #14: "Potential typo in setup-pre-commit/SKILL.md"
- #301: "`block-dangerous-git.sh` is bypassed by any git global option (e.g. `git -C <dir> push`)"
- #465: "git-guardrails-claude-code documentation is missing benefits over built in Claude code deny rules"
- #898: "git-guardrails-claude-code: hook fails open without jq and misses common git spellings"
