---
name: setup-ts-deep-modules
description: TypeScript 저장소에 dependency-cruiser를 연결하여 각 패키지를 깊은 모듈로 만듭니다. 구현은 하위 폴더에 숨겨지며 진입점 파일을 통해서만 접근할 수 있습니다. 사용자 호출.
disable-model-invocation: true
---

# TS 깊은 모듈 설정

이 저장소의 모든 패키지를 **깊은 모듈(deep module)**로 만드십시오. 즉, 작은 인터페이스 뒤에 많은 동작을 두는 것입니다. 패키지의 공개 표면은 **진입점(entry points)**(패키지 루트에 있는 파일)이며, 하위 폴더에 있는 모든 것은 숨겨집니다. 이 스킬은 [dependency-cruiser](https://github.com/sverweij/dependency-cruiser)와, 진입점을 유일한 출입구로 만드는 규칙을 설치한 다음, 규칙이 실제로 작동함을 증명합니다.

어휘(deep module, interface, seam, depth)에 대해서는 "codebase-design"으로 Skill 도구를 호출하고, 전반에 걸쳐 그 언어를 사용하십시오.

## 이 스킬이 강제하는 형태

```
src/packages/
  <name>/
    index.ts        ← an entry point (public). Import this from outside.
    client.ts       ← another entry point. Packages may expose SEVERAL.
    lib/            ← implementation: hidden from outside, free to import each other.
    tests/          ← co-located tests + fixtures (a subfolder, so private).
```

공개 표면은 지정된 하나의 `index.ts`가 아니라 패키지의 **루트 파일**입니다. 관례상 구현은 `lib/`에, 테스트는 `tests/`에 두어, 모든 패키지가 같은 두 폴더 형태를 갖게 됩니다. 그러나 규칙 자체는 일반적입니다. *어떤* 하위 폴더에 있는 *무엇이든* 비공개이므로, 폴더를 추가하기 위해 구성을 확장할 필요가 없습니다.

네 가지 규칙이 있으며, 모두 `error`입니다.

1. **진입점 경계**: 패키지 외부의 코드(앱 코드 또는 다른 패키지)는 해당 패키지의 진입점(루트 파일)만 임포트할 수 있으며, 하위 폴더에 있는 것은 절대 임포트할 수 없습니다.
2. **패키지 내부의 자유**: 패키지 자신의 파일들은 서로 자유롭게 임포트합니다.
3. **진입점을 통한 테스트**: `<pkg>/tests/` 아래의 파일은 어떤 패키지의 진입점이든, 그리고 자신의 `tests/` 픽스처를 임포트할 수 있지만, 어떤 패키지의 하위 폴더 내부(자기 자신의 것조차)도 절대 임포트할 수 없습니다. 패키지 간 통합 테스트는 괜찮지만, 깊은 임포트는 안 됩니다.
4. **순환 금지**: 의존성 순환이 없어야 합니다.

**배럴(barrel)이 아니라 진입점.** 공개 표면이 *모든* 루트 파일이므로, 패키지는 모든 것을 하나의 거대한 `index.ts`로 몰아넣는 대신 여러 개의 작은 진입점(`index.ts`, `client.ts`, `server.ts`)을 노출할 수 있습니다. 하위 트리 전체를 다시 내보내는 배럴 파일은 권장하지 않습니다. 진입점을 작게 유지하고 구현은 하위 폴더에 숨기십시오.

계층화(어떤 패키지가 어떤 패키지에 의존할 수 있는지)는 *다른* 관심사이며, 이 저장소가 채울 수 있도록 구성 파일에 주석 처리된 스텁으로 남겨 둡니다.

## 단계

### 1. 환경 감지

- **패키지 매니저**: `pnpm-lock.yaml` → pnpm, `yarn.lock` → yarn, `bun.lockb` → bun, 그 외에는 npm. 아래의 모든 명령에 이를 사용하십시오(`pnpm`/`yarn`/`npm run`/`bunx`).
- **패키지 루트**: `src/`가 존재하면 `src/packages`를, 그렇지 않으면 `packages`를 사용하십시오. 저장소에 이미 다른 명백한 관례가 있다면 사용자와 선택을 확인하십시오.
- **기존 구성**: `.dependency-cruiser.*` 파일이 있는지 확인하십시오. 있다면 덮어쓰지 **마십시오**. 네 가지 규칙과 옵션을 병합하고, 무엇을 추가했는지 사용자에게 알리십시오.

**완료 조건:** 패키지 매니저, 패키지 루트, 기존 구성 상태가 모두 파악되었습니다.

### 2. dependency-cruiser 설치

감지된 패키지 매니저로 `dependency-cruiser`를 devDependency로 설치하십시오.

**완료 조건:** `dependency-cruiser`가 `devDependencies`에 있습니다.

### 3. 구성 작성

[`dependency-cruiser.config.cjs`](./dependency-cruiser.config.cjs)를 저장소 루트에 `.dependency-cruiser.cjs`로 복사하십시오. `PACKAGES_ROOT`를 1단계에서 감지한 루트로 설정하십시오. 규칙은 경로 깊이를 기반으로 하며 확장자와 무관하므로, 그 밖에 조정할 것은 없습니다.

**완료 조건:** `.dependency-cruiser.cjs`가 올바른 `PACKAGES_ROOT`와 함께 존재하며, 네 가지 금지 규칙이 들어 있습니다.

### 4. 검사에 연결

- `lint:boundaries` 스크립트를 추가하십시오: `depcruise <packages-root>`(또는 `depcruise src`).
- 이미 타입 검사를 실행하는 저장소의 포괄 검사 명령(예: `check` / `ci` / `validate` 스크립트)에 이를 포함시키십시오. `tsconfig`를 건드리거나 경로 별칭을 추가하지 **마십시오**.
- 포괄 스크립트가 없다면, `lint:boundaries`를 추가하고 사용자에게 이를 CI에 포함하라고 안내하십시오.

**완료 조건:** `lint:boundaries`가 존재하며 타입 검사와 같은 명령의 일부로 실행됩니다.

### 5. 예시 패키지 생성

복사해서 쓸 수 있는 템플릿으로서 `<packages-root>/example/`을 생성하여 커밋하십시오.

- `index.ts`는 진입점입니다. 내부 파일에 위임하는 함수 하나를 내보내십시오(그래야 패키지가 단순한 통과 지점이 아니라 눈에 보이게 *깊어집니다*).
- `lib/impl.ts`: `index.ts`가 임포트하며 외부에서는 도달할 수 없는, **하위 폴더**의 내부 파일입니다.
- `tests/example.test.ts`는 `../index`(진입점)**만** 임포트하며, 공개 함수에 대해 단언합니다.

이것이 복사하거나 삭제할 수 있는 시작용 템플릿이라고 사용자에게 알리십시오.

**완료 조건:** 예시 패키지가 존재하며, 루트 진입점을 통해 동작을 노출하고 `impl`을 하위 폴더에 숨깁니다.

### 6. 규칙이 작동함을 증명

이것이 스킬 전체의 완료 기준입니다. 위반에 대해 실패하지 않는 구성은 쓸모가 없습니다.

1. `lint:boundaries`를 실행하십시오. 깨끗한 예시에서 **통과**해야 합니다.
2. `tests/example.test.ts`에 임시로 깊은 임포트를 추가하십시오(예: `import { thing } from "../lib/impl"`). `lint:boundaries`를 다시 실행하십시오. `tests-through-entrypoints`와 함께 **실패**해야 합니다.
3. 깊은 임포트를 되돌리십시오. 한 번 더 실행하면 **통과**해야 합니다.

**완료 조건:** 통과, 깊은 임포트에 대한 실패, 그리고 다시 통과를 관찰했습니다. 2단계가 실패하지 않는다면 규칙이 올바르게 연결되지 않은 것이므로, 마치기 전에 수정하십시오.

### 7. 규칙 문서화

**패키지 폴더 안에**(`<packages-root>/README.md`, 그것이 관할하는 패키지 옆에) `README.md`를 작성하여 다음을 다루십시오. `src/packages/<name>/` 레이아웃(루트에 진입점, 구현은 `lib/`, 테스트는 `tests/`), "패키지의 진입점(루트 파일)을 통해서만 임포트하라", 그리고 `lint:boundaries`를 실행하는 방법입니다. **배럴 파일을** 명시적으로 **권장하지 마십시오**. 하나의 index를 통해 하위 트리 전체를 다시 내보내는 대신 여러 개의 작은 진입점을 노출하도록 하십시오. 복사용 스니펫과 네 가지 규칙을 각각 한 단락으로만 유지하십시오.

그런 다음 저장소의 에이전트 지침 파일(`CLAUDE.md`가 있으면 그것, 없으면 `AGENTS.md`, 둘 다 없으면 `AGENTS.md`를 생성)에서 이 문서로 가는 **컨텍스트 포인터**를 추가하십시오. 한 줄이면 충분합니다. 예: `Packages are deep modules: see [src/packages/README.md](./src/packages/README.md) before adding or importing one.` 이것이 에이전트가 경계 규칙에 걸려 넘어지는 대신 그것을 발견하게 만드는 방법입니다.

**완료 조건:** `<packages-root>/README.md`가 존재하며 배럴을 권장하지 않고, 저장소의 `CLAUDE.md`/`AGENTS.md`가 이를 링크합니다.

## 참고

- 구성의 `$1` 역참조(dependency-cruiser의 그룹 매칭)가 패키지는 자신의 내부에 접근할 수 있되 외부에서는 접근할 수 없게 하는 핵심입니다. 이를 패키지별 개별 규칙으로 평탄화하지 마십시오.
- 공개와 비공개는 **깊이**로 결정됩니다. 패키지의 루트 파일은 진입점이고, 하위 폴더에 있는 것은 모두 비공개입니다. 관례적인 하위 폴더는 `lib/`(구현)와 `tests/`이지만, 규칙은 이들을 하드코딩하지 않습니다. 어떤 하위 폴더든 비공개이므로, 새 폴더를 추가해도 구성을 변경할 필요가 없습니다. 진입점을 추가하는 것은 루트 파일을 추가하는 것일 뿐입니다(배럴 없음).
- 패키지는 **평평합니다**. 루트 아래에 직속 하위 항목이 한 계층만 있습니다. 패키지의 내부는 원하는 만큼 깊게 중첩될 수 있지만, 패키지가 다른 패키지를 포함할 수는 없습니다.
- `"type": "module"` 저장소에서도 구성의 `module.exports`가 동작하도록 `.js`가 아니라 `.cjs`를 사용하십시오.
