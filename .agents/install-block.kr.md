# 표준 설치 블록

하나의 설치 방법, 하나의 문구. `README.md`, `.changeset/*`, 그리고 `docs/` 아래의 모든 페이지는 **이 내용**만을 기술해야 하며 그 외의 내용을 기술해서는 안 됩니다. 먼저 이곳을 변경한 뒤 다른 곳으로 전파하십시오.

## 관리형 설치 우선

스스로 업데이트되는 설치 방법을 먼저 제시하십시오. 그러한 설치 방법이 없는 에이전트에 대해서만 "수동 업데이트"라는 라벨을 붙여 skills.sh로 대체하십시오. 사용자가 명령을 실행하지 않아도 업데이트되는 경우에만 해당 경로를 관리형이라고 부르십시오. 일회성 옵트인이 필요하다면 해당 설치 명령 옆에 두십시오. "즉시"라는 약속은 절대 하지 마십시오.

Claude Code는 공식 마켓플레이스인 `claude-plugins-official`에서 설치합니다. 그 외의 모든 관리형 경로는 이 저장소 자체의 마켓플레이스인 `.claude-plugin/marketplace.json`과 `plugin.json`에서 설치합니다. 이 경로들은 `plugin.json`의 `version`이 변경될 때만 재설치됩니다. Release 워크플로는 `npm run version`을 실행하며, 이 명령은 해당 필드를 `package.json`에서 복사합니다. 따라서 사용자는 "chore: version skills" PR이 병합될 때 릴리스를 받게 됩니다.

| 에이전트      | 경로                             | 자동 업데이트 여부                                               |
| ------------- | -------------------------------- | ---------------------------------------------------------------- |
| Claude Code   | `@claude-plugins-official`       | 예, 기본값                                                       |
| Codex         | `@mattpocock` 마켓플레이스       | 예, 시작 시, 기본값                                              |
| Copilot CLI   | `@mattpocock` 마켓플레이스       | 예, 일회성 `autoUpdate: true` 설정 후                            |
| VS Code       | Chat: Install Plugin From Source | 예, 매일, 기본값                                                 |
| Gemini CLI    | `gemini skills install` (복사)   | 아니요. Gemini 확장은 평면적인 `skills/<name>/` 구조가 필요함    |
| 그 외 모두    | skills.sh                        | 아니요. `npx skills update`를 실행하고, 새 스킬은 `add`를 재실행 |

출처(2026-10-08): Codex `core-plugins/src/manager.rs`; Copilot [cli-config-dir-reference](https://docs.github.com/en/copilot/reference/copilot-cli-reference/cli-config-dir-reference); VS Code `pluginAutoUpdate.ts`; Gemini `skillLoader.ts`.

아직 아무도 이 저장소를 대상으로 Auggie, Droid, Qwen, Goose를 실행해 보지 않았으므로, 누군가 실행해 볼 때까지 이들은 skills.sh를 사용합니다.

## Claude Code

<canonical-block name="claude-code">

```bash
claude plugin install mattpocock-skills@claude-plugins-official
```

기본적으로 스스로 업데이트됩니다.

</canonical-block>

## Codex

<canonical-block name="codex">

```bash
codex plugin marketplace add mattpocock/skills
codex plugin add mattpocock-skills@mattpocock
```

시작 시 스스로 업데이트됩니다.

</canonical-block>

## GitHub Copilot (CLI 및 VS Code)

`copilot plugin install mattpocock/skills`가 아니라 마켓플레이스를 사용하십시오. Copilot은 저장소 직접 설치를 더 이상 권장하지 않으며, 해당 방식은 자동 업데이트가 불가능합니다. `extraKnownMarketplaces` 항목은 문서화된 스키마를 따르지만, 아직 아무도 실행해 보지 않았습니다.

<canonical-block name="copilot">

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

</canonical-block>

## Gemini CLI

Gemini는 `.claude-plugin`을 읽지 않으며, `--path`는 하나의 버킷만 받습니다. 승격된 버킷마다 한 번씩 설치하면 정확히 승격된 세트(27개 스킬, 2026-10-07 검증)를 얻을 수 있습니다.

<canonical-block name="gemini">

```bash
gemini skills install https://github.com/mattpocock/skills.git --path skills/engineering
gemini skills install https://github.com/mattpocock/skills.git --path skills/productivity
```

업데이트하려면 두 명령을 모두 다시 실행하십시오.

</canonical-block>

## 그 외 모든 에이전트, 또는 편집 가능한 파일 (skills.sh)

`-a`는 에이전트를 미리 선택합니다. 주석에 있는 각 에이전트는 2026-10-07에 실행해 보았습니다. `amp skill add`나 `pi install git:…`과 같은 에이전트 자체의 저장소 설치 도구보다 skills.sh를 우선하십시오. 그러한 도구는 `misc/`와 `in-progress/`까지 가져오기 때문입니다. `npx skills update`는 `add` 이후 업스트림에 추가된 스킬을 건너뛰므로, 이 블록은 사용자에게 `add`를 다시 실행하도록 안내합니다.

<canonical-block name="other-agents">

```bash
npx skills@latest add mattpocock/skills -a <agent>  # cursor, opencode, devin, windsurf, amp, pi; omit -a to choose
```

설치 도구가 어떤 스킬을 가져올지 물으면 `setup-matt-pocock-skills`를 포함하십시오. 업데이트하려면 `npx skills@latest update`를 실행하고, 새 스킬을 가져오려면 `add`를 다시 실행하십시오.

</canonical-block>

하나의 스킬만 단독으로 언급되는 곳에서는 단일 스킬 형식을 사용하십시오. `docs/` 페이지는 이 블록을 사용하지 않습니다. ai-hero가 페이지 본문 위에 설치 위젯을 렌더링하기 때문입니다. [writing-docs.md](./writing-docs.md)를 참조하십시오.

<canonical-block name="skills-sh-one-skill">

```bash
npx skills@latest add mattpocock/skills --skill=<name>
```

```bash
npx skills@latest update <name>
```

</canonical-block>

`skills@latest`가 모든 곳에서 고정된 표기법입니다.

## 두 경로는 상호 배타적이다

플러그인은 사용자가 구독하는 관리형 읽기 전용 번들입니다. skills.sh는 사용자가 소유하고 편집하는 파일을 작성합니다. 둘 다 설치하면 사용자는 모든 스킬을 두 개씩 갖게 됩니다. 항상 "하나를 선택하십시오"라고 안내하십시오.
