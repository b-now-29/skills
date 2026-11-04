# GLOSSARY.md 형식

## 구조

```md
# {컨텍스트 이름}

{이 컨텍스트가 무엇이며 왜 존재하는지에 대한 한두 문장의 설명.}

## 용어

**주문(Order)**:
{용어에 대한 한두 문장의 설명}
_사용하지 말 것_: 구매, 거래

**청구서(Invoice)**:
배송 후 고객에게 보내는 지불 요청.
_사용하지 말 것_: 계산서, 지불 요청

**고객(Customer)**:
주문을 하는 개인 또는 조직.
_사용하지 말 것_: 클라이언트, 구매자, 계정
```

## 규칙

- **분명한 입장을 취하십시오.** 같은 개념에 대해 여러 단어가 존재하는 경우, 가장 좋은 것을 선택하고 나머지는 `_사용하지 말 것_` 아래에 나열하십시오.
- **정의를 간결하게 유지하십시오.** 최대 한두 문장입니다. 무엇을 하는지가 아니라 무엇인지를 정의하십시오.
- **이 프로젝트의 컨텍스트에 고유한 용어만 포함하십시오.** 일반적인 프로그래밍 개념(타임아웃, 오류 타입, 유틸리티 패턴)은 프로젝트가 광범위하게 사용하더라도 포함하지 않습니다. 용어를 추가하기 전에 물으십시오. 이것은 이 컨텍스트에 고유한 개념인가, 아니면 일반적인 프로그래밍 개념인가? 전자만 포함됩니다.
- 자연스러운 묶음이 생기면 **하위 제목 아래로 용어를 그룹화하십시오**. 모든 용어가 하나의 응집된 영역에 속한다면, 평면 목록도 괜찮습니다.

## 단일 컨텍스트 대 다중 컨텍스트 저장소

**단일 컨텍스트(대부분의 저장소):** 저장소 루트에 하나의 `GLOSSARY.md`.

**다중 컨텍스트:** 저장소 루트의 `GLOSSARY-MAP.md`가 컨텍스트들과 그 위치, 그리고 서로 어떻게 관련되는지를 나열합니다.

```md
# Glossary Map

## Contexts

- [Ordering](./src/ordering/GLOSSARY.md): receives and tracks customer orders
- [Billing](./src/billing/GLOSSARY.md): generates invoices and processes payments
- [Fulfillment](./src/fulfillment/GLOSSARY.md): manages warehouse picking and shipping

## Relationships

- **Ordering → Fulfillment**: Ordering emits `OrderPlaced` events; Fulfillment consumes them to start picking
- **Fulfillment → Billing**: Fulfillment emits `ShipmentDispatched` events; Billing consumes them to generate invoices
- **Ordering ↔ Billing**: Shared types for `CustomerId` and `Money`
```

스킬은 어떤 구조가 적용되는지 추론합니다.

- `GLOSSARY-MAP.md`가 존재하면, 이를 읽어 컨텍스트를 찾습니다
- 루트 `GLOSSARY.md`만 존재하면, 단일 컨텍스트입니다
- 둘 다 존재하지 않으면, 첫 번째 용어가 확정될 때 루트 `GLOSSARY.md`를 지연 생성합니다

여러 컨텍스트가 존재하는 경우, 현재 주제가 어느 것과 관련되는지 추론하십시오. 불분명하다면 물어보십시오.
