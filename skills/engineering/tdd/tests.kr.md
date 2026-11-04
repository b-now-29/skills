# 좋은 테스트와 나쁜 테스트

## 좋은 테스트

**통합 스타일**: 내부 부분의 목이 아니라 실제 인터페이스를 통해 테스트합니다.

```typescript
// GOOD: Tests observable behavior
test("user can checkout with valid cart", async () => {
  const cart = createCart();
  cart.add(product);
  const result = await checkout(cart, paymentMethod);
  expect(result.status).toBe("confirmed");
});
```

특징:

- 사용자/호출자가 신경 쓰는 동작을 테스트합니다
- 공개 API만 사용합니다
- 내부 리팩터링에도 살아남습니다
- 어떻게(HOW)가 아니라 무엇을(WHAT) 기술합니다
- 테스트당 하나의 논리적 단언

## 나쁜 테스트

**구현 세부 사항 테스트**: 내부 구조에 결합되어 있습니다.

```typescript
// BAD: Tests implementation details
test("checkout calls paymentService.process", async () => {
  const mockPayment = jest.mock(paymentService);
  await checkout(cart, payment);
  expect(mockPayment.process).toHaveBeenCalledWith(cart.total);
});
```

위험 신호:

- 내부 협력자를 목으로 대체함
- private 메서드를 테스트함
- 호출 횟수/순서에 대해 단언함
- 동작 변경 없이 리팩터링할 때 테스트가 깨짐
- 테스트 이름이 무엇을(WHAT)이 아니라 어떻게(HOW)를 기술함
- 인터페이스 대신 외부 수단을 통해 검증함

```typescript
// BAD: Bypasses interface to verify
test("createUser saves to database", async () => {
  await createUser({ name: "Alice" });
  const row = await db.query("SELECT * FROM users WHERE name = ?", ["Alice"]);
  expect(row).toBeDefined();
});

// GOOD: Verifies through interface
test("createUser makes user retrievable", async () => {
  const user = await createUser({ name: "Alice" });
  const retrieved = await getUser(user.id);
  expect(retrieved.name).toBe("Alice");
});
```

**동어 반복적 테스트**: 기대값이 구현을 다시 진술하므로, 테스트가 구조적으로 통과합니다.

```typescript
// BAD: Expected value is recomputed the way the code computes it
test("calculateTotal sums line items", () => {
  const items = [{ price: 10 }, { price: 5 }];
  const expected = items.reduce((sum, i) => sum + i.price, 0);
  expect(calculateTotal(items)).toBe(expected);
});

// GOOD: Expected value is an independent, known literal
test("calculateTotal sums line items", () => {
  expect(calculateTotal([{ price: 10 }, { price: 5 }])).toBe(15);
});
```
