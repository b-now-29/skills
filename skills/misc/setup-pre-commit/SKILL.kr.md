---
name: setup-pre-commit
description: 현재 저장소에 lint-staged(Prettier), 타입 검사, 테스트를 포함하는 Husky pre-commit 훅을 설정합니다. 사용자가 pre-commit 훅을 추가하거나, Husky를 설정하거나, lint-staged를 구성하거나, 커밋 시점의 포매팅/타입 검사/테스트를 추가하고자 할 때 사용합니다.
---

# Pre-Commit 훅 설정

## 설정되는 항목

- **Husky** pre-commit 훅
- 스테이징된 모든 파일에 Prettier를 실행하는 **lint-staged**
- **Prettier** 구성(없는 경우)
- pre-commit 훅의 **typecheck** 및 **test** 스크립트

## 단계

### 1. 패키지 매니저 감지

`package-lock.json`(npm), `pnpm-lock.yaml`(pnpm), `yarn.lock`(yarn), `bun.lockb`(bun)가 있는지 확인하십시오. 존재하는 것을 사용하십시오. 불분명하면 npm을 기본으로 사용하십시오.

### 2. 의존성 설치

devDependencies로 설치하십시오.

```
husky lint-staged prettier
```

### 3. Husky 초기화

```bash
npx husky init
```

이 명령은 `.husky/` 디렉터리를 생성하고 package.json에 `prepare: "husky"`를 추가합니다.

### 4. `.husky/pre-commit` 생성

다음 파일을 작성하십시오(Husky v9 이상에서는 셔뱅이 필요 없습니다).

```
npx lint-staged
npm run typecheck
npm run test
```

**조정**: `npm`을 감지된 패키지 매니저로 교체하십시오. 저장소의 package.json에 `typecheck` 또는 `test` 스크립트가 없다면, 해당 줄을 생략하고 사용자에게 알리십시오.

### 5. `.lintstagedrc` 생성

```json
{
  "*": "prettier --ignore-unknown --write"
}
```

### 6. `.prettierrc` 생성 (없는 경우)

Prettier 구성이 없는 경우에만 생성하십시오. 다음 기본값을 사용하십시오.

```json
{
  "useTabs": false,
  "tabWidth": 2,
  "printWidth": 80,
  "singleQuote": false,
  "trailingComma": "es5",
  "semi": true,
  "arrowParens": "always"
}
```

### 7. 검증

- [ ] `.husky/pre-commit`이 존재하며 실행 가능함
- [ ] `.lintstagedrc`가 존재함
- [ ] package.json의 `prepare` 스크립트가 `"husky"`임
- [ ] `prettier` 구성이 존재함
- [ ] `npx lint-staged`를 실행하여 동작하는지 확인

### 8. 커밋

변경되거나 생성된 모든 파일을 스테이징하고 다음 메시지로 커밋하십시오: `Add pre-commit hooks (husky + lint-staged + prettier)`

이 커밋은 새로운 pre-commit 훅을 거쳐 실행되므로, 모든 것이 동작하는지 확인하는 좋은 스모크 테스트가 됩니다.

## 참고

- Husky v9 이상에서는 훅 파일에 셔뱅이 필요 없습니다
- `prettier --ignore-unknown`은 Prettier가 파싱할 수 없는 파일(이미지 등)을 건너뜁니다
- pre-commit은 먼저 lint-staged(빠르며, 스테이징된 파일만 대상)를 실행한 다음, 전체 타입 검사와 테스트를 실행합니다
