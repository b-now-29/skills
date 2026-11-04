# 목을 사용해야 하는 경우

**시스템 경계**에서만 목(mock)을 사용하십시오.

- 외부 API(결제, 이메일 등)
- 데이터베이스(경우에 따라. 테스트 DB를 선호하십시오)
- 시간/무작위성
- 파일 시스템(경우에 따라)

목을 사용하지 말아야 할 것:

- 자신의 클래스/모듈
- 내부 협력자
- 직접 제어할 수 있는 모든 것

## 목으로 대체하기 쉬운 설계

시스템 경계에서는 목으로 대체하기 쉬운 인터페이스를 설계하십시오.

**1. 의존성 주입을 사용하십시오**

외부 의존성을 내부에서 생성하지 말고 전달받으십시오.

```typescript
// Easy to mock
function processPayment(order, paymentClient) {
  return paymentClient.charge(order.total);
}

// Hard to mock
function processPayment(order) {
  const client = new StripeClient(process.env.STRIPE_KEY);
  return client.charge(order.total);
}
```

**2. 범용 fetcher보다 SDK 스타일 인터페이스를 선호하십시오**

조건 로직을 가진 하나의 범용 함수 대신, 각 외부 작업에 대한 구체적인 함수를 만드십시오.

```typescript
// GOOD: Each function is independently mockable
const api = {
  getUser: (id) => fetch(`/users/${id}`),
  getOrders: (userId) => fetch(`/users/${userId}/orders`),
  createOrder: (data) => fetch('/orders', { method: 'POST', body: data }),
};

// BAD: Mocking requires conditional logic inside the mock
const api = {
  fetch: (endpoint, options) => fetch(endpoint, options),
};
```

SDK 방식은 다음을 의미합니다.
- 각 목은 하나의 구체적인 형태를 반환합니다
- 테스트 설정에 조건 로직이 없습니다
- 테스트가 어떤 엔드포인트를 실행하는지 보기 쉽습니다
- 엔드포인트별 타입 안전성
