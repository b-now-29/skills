# In Progress

베타입니다. 이 스킬들은 의도적으로 공개되어 있습니다. 사용해 보고 무엇이 망가지는지 알려 주십시오. 안정적인 버킷으로 졸업할 때까지 플러그인과 최상위 README에서 제외되며, 문서 페이지를 갖지 않고, 예고 없이 변경되거나 사라질 수 있습니다.

플러그인은 이 스킬들을 제공하지 않습니다. 직접 설치하십시오.

```bash
npx skills@latest add mattpocock/skills --skill=<name>
```

- **[loop-me](./loop-me/SKILL.md)**: 현재 디렉터리를 상태 저장 작업 공간으로 사용하여, 여러 세션에 걸쳐 스스로를 그릴링하며 구현 가능한 워크플로 명세를 만들어 냅니다. 사용자 호출.
- **[writing-beats](./writing-beats/SKILL.md)**: 선택형 모험 방식으로, 글을 비트(beat)의 여정으로 구성합니다. 시작 비트를 선택하여 그 비트만 작성한 다음, 글이 자연스럽게 끝날 때까지 다음 비트로 전환합니다.
- **[writing-fragments](./writing-fragments/SKILL.md)**: 사용자로부터 조각(fragment, 이질적인 글의 알맹이)을 캐내어 향후 글의 원재료로서 단일 문서에 덧붙이는 그릴링 세션입니다.
- **[writing-shape](./writing-shape/SKILL.md)**: 원재료가 담긴 마크다운 파일을 받아 단락 단위로 글의 형태를 잡으며, 각 단계마다 형식 선택에 대해 논증합니다.
- **[claude-handoff](./claude-handoff/SKILL.md)**: `claude --bg`를 통해 인계 요약을 전달하여, 즉시 작업을 이어받는 새로운 백그라운드 에이전트에게 현재 대화를 넘깁니다. 사용자 호출.
- **[setup-ts-deep-modules](./setup-ts-deep-modules/SKILL.md)**: TypeScript 저장소에 dependency-cruiser를 연결하여 각 패키지를 깊은 모듈로 만듭니다. 구현은 하위 폴더에 숨겨지고, 진입점 파일을 통해서만 접근할 수 있으며, 테스트도 해당 진입점을 통해 실행됩니다. 사용자 호출.
- **[software-factory](./software-factory/SKILL.md)**: 소프트웨어 팩토리를 설계하기 위한 공유 언어입니다. 팩토리가 실행하는 작업과 팩토리가 연결되는 서비스를 다룹니다. 그릴링 세션과 함께 호출하십시오. 사용자 호출.
