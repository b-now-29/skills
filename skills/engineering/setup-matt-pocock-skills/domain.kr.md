# 도메인 문서

엔지니어링 스킬이 코드베이스를 탐색할 때 이 저장소의 도메인 문서를 어떻게 활용해야 하는지에 대한 내용입니다.

## 탐색하기 전에 다음을 읽으십시오

- 저장소 루트의 **`GLOSSARY.md`**, 또는
- 존재한다면 저장소 루트의 **`GLOSSARY-MAP.md`**: 컨텍스트별로 하나의 `GLOSSARY.md`를 가리킵니다. 주제와 관련된 각 파일을 읽으십시오.
- **`docs/adr/`**: 작업하려는 영역과 관련된 ADR을 읽으십시오. 다중 컨텍스트 저장소에서는 컨텍스트 범위의 결정을 위해 `src/<context>/docs/adr/`도 확인하십시오.

이 파일들 중 어느 것이 존재하지 않더라도, **조용히 진행하십시오**. 없다는 것을 지적하지 말고, 미리 생성하라고 제안하지 마십시오. `/domain-modeling` 스킬(`/grill-with-docs`와 `/improve-codebase-architecture`를 통해 도달)이 용어나 결정이 실제로 확정될 때 이를 지연 생성합니다.

## 파일 구조

단일 컨텍스트 저장소(대부분의 저장소):

```
/
├── GLOSSARY.md
├── docs/adr/
│   ├── 0001-event-sourced-orders.md
│   └── 0002-postgres-for-write-model.md
└── src/
```

다중 컨텍스트 저장소(루트에 `GLOSSARY-MAP.md`가 있음):

```
/
├── GLOSSARY-MAP.md
├── docs/adr/                          ← system-wide decisions
└── src/
    ├── ordering/
    │   ├── GLOSSARY.md
    │   └── docs/adr/                  ← context-specific decisions
    └── billing/
        ├── GLOSSARY.md
        └── docs/adr/
```

## 용어집의 어휘를 사용하십시오

출력에서 도메인 개념을 명명할 때(이슈 제목, 리팩터링 제안, 가설, 테스트 이름), `GLOSSARY.md`에 정의된 대로 용어를 사용하십시오. 용어집이 명시적으로 피하는 동의어로 표류하지 마십시오.

필요한 개념이 아직 용어집에 없다면, 그것은 신호입니다. 프로젝트가 사용하지 않는 언어를 만들어 내고 있거나(재고하십시오), 실제 공백이 있는 것입니다(`/domain-modeling`을 위해 기록하십시오).

## ADR 충돌을 표시하십시오

출력이 기존 ADR과 모순된다면, 조용히 무시하지 말고 명시적으로 드러내십시오.

> _ADR-0007(이벤트 소싱 주문)과 모순되지만, …때문에 다시 열어 볼 가치가 있음_
