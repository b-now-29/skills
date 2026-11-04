---
name: migrate-to-shoehorn
description: 테스트 파일을 `as` 타입 단언에서 @total-typescript/shoehorn으로 마이그레이션합니다. 사용자가 shoehorn을 언급하거나, 테스트에서 `as`를 대체하고 싶어 하거나, 부분적인 테스트 데이터가 필요할 때 사용합니다.
---

# Shoehorn으로 마이그레이션

## 왜 shoehorn인가?

`shoehorn`을 사용하면 TypeScript를 만족시키면서도 테스트에서 부분적인 데이터를 전달할 수 있습니다. `as` 단언을 타입 안전한 대안으로 대체합니다.

**테스트 코드 전용입니다.** 프로덕션 코드에서는 절대 shoehorn을 사용하지 마십시오.

테스트에서 `as`를 사용할 때의 문제점:

- 사용하지 않도록 훈련되어 있음
- 대상 타입을 수동으로 지정해야 함
- 의도적으로 잘못된 데이터를 위해 이중 as(`as unknown as Type`)를 사용해야 함

## 설치

```bash
npm i @total-typescript/shoehorn
```

## 마이그레이션 패턴

### 필요한 속성이 적은 큰 객체

이전:

```ts
type Request = {
  body: { id: string };
  headers: Record<string, string>;
  cookies: Record<string, string>;
  // ...20 more properties
};

it("gets user by id", () => {
  // Only care about body.id but must fake entire Request
  getUser({
    body: { id: "123" },
    headers: {},
    cookies: {},
    // ...fake all 20 properties
  });
});
```

이후:

```ts
import { fromPartial } from "@total-typescript/shoehorn";

it("gets user by id", () => {
  getUser(
    fromPartial({
      body: { id: "123" },
    }),
  );
});
```

### `as Type` → `fromPartial()`

이전:

```ts
getUser({ body: { id: "123" } } as Request);
```

이후:

```ts
import { fromPartial } from "@total-typescript/shoehorn";

getUser(fromPartial({ body: { id: "123" } }));
```

### `as unknown as Type` → `fromAny()`

이전:

```ts
getUser({ body: { id: 123 } } as unknown as Request); // wrong type on purpose
```

이후:

```ts
import { fromAny } from "@total-typescript/shoehorn";

getUser(fromAny({ body: { id: 123 } }));
```

## 각각을 사용하는 경우

| 함수            | 사용 사례                                                  |
| --------------- | ---------------------------------------------------------- |
| `fromPartial()` | 여전히 타입 검사를 통과하는 부분 데이터 전달               |
| `fromAny()`     | 의도적으로 잘못된 데이터 전달(자동 완성 유지)              |
| `fromExact()`   | 전체 객체를 강제(나중에 fromPartial로 교체)                |

## 워크플로

1. **요구 사항 수집**: 사용자에게 질문하십시오.
   - 어떤 테스트 파일에 문제를 일으키는 `as` 단언이 있습니까?
   - 일부 속성만 중요한 큰 객체를 다루고 있습니까?
   - 오류 테스트를 위해 의도적으로 잘못된 데이터를 전달해야 합니까?

2. **설치 및 마이그레이션**:
   - [ ] 설치: `npm i @total-typescript/shoehorn`
   - [ ] `as` 단언이 있는 테스트 파일 찾기: `grep -r " as [A-Z]" --include="*.test.ts" --include="*.spec.ts"`
   - [ ] `as Type`을 `fromPartial()`로 교체
   - [ ] `as unknown as Type`을 `fromAny()`로 교체
   - [ ] `@total-typescript/shoehorn`에서 임포트 추가
   - [ ] 타입 검사를 실행하여 검증
