# HTML 보고서 형식

아키텍처 리뷰는 OS 임시 디렉터리에 있는 하나의 독립적인 HTML 파일로 렌더링됩니다. Tailwind와 Mermaid는 모두 CDN에서 가져옵니다. Mermaid는 그래프 형태의 다이어그램을 안정적으로 처리하고, 직접 만든 div와 인라인 SVG는 더 편집적인 시각 자료(질량 다이어그램, 단면도)를 처리합니다. 둘을 섞으십시오. 모든 것을 Mermaid에 의존하지 마십시오. 그러면 획일적으로 보이기 시작합니다.

## 뼈대

```html
<!doctype html>
<html lang="en">
  <head>
    <meta charset="utf-8" />
    <title>Architecture review for {{repo name}}</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <script type="module">
      import mermaid from "https://cdn.jsdelivr.net/npm/mermaid@11/dist/mermaid.esm.min.mjs";
      mermaid.initialize({ startOnLoad: true, theme: "neutral", securityLevel: "loose" });
    </script>
    <style>
      /* small custom layer for things Tailwind doesn't cover cleanly:
         dashed seam lines, hand-drawn-feeling arrow heads, etc. */
      .seam { stroke-dasharray: 4 4; }
      .leak { stroke: #dc2626; }
      .deep { background: linear-gradient(135deg, #0f172a, #1e293b); }
    </style>
  </head>
  <body class="bg-stone-50 text-slate-900 font-sans">
    <main class="max-w-5xl mx-auto px-6 py-12 space-y-12">
      <header>...</header>
      <section id="candidates" class="space-y-10">...</section>
      <section id="top-recommendation">...</section>
    </main>
  </body>
</html>
```

## 헤더

저장소 이름, 날짜, 그리고 간결한 범례입니다. 실선 상자 = 모듈, 점선 = 시임, 빨간 화살표 = 누수, 굵고 어두운 상자 = 깊은 모듈. 소개 단락은 없습니다. 바로 후보로 들어갑니다.

## 후보 카드

다이어그램이 무게를 짊어집니다. 산문은 드물고 평이하며, 용어집 용어(`/codebase-design` 스킬의 용어)를 격식 없이 사용합니다.

각 후보는 하나의 `<article>`입니다.

- **제목**: 짧게, 심화를 명명합니다(예: "Order 접수 파이프라인 축약").
- **배지 행**: 권장 강도(`Strong` = 에메랄드, `Worth exploring` = 앰버, `Speculative` = 슬레이트), 그리고 의존성 범주 태그(`in-process`, `local-substitutable`, `ports & adapters`, `mock`).
- **파일**: 고정폭 글꼴 목록, `font-mono text-sm`.
- **전 / 후 다이어그램**: 핵심 요소입니다. 두 열을 나란히 배치합니다. 아래의 패턴을 참조하십시오.
- **문제**: 한 문장. 무엇이 고통스러운가.
- **해결책**: 한 문장. 무엇이 바뀌는가.
- **이점**: 글머리 기호, 각각 6단어 이하. 예: "테스트가 하나의 인터페이스를 거침", "가격 로직 누수 중단", "얕은 래퍼 4개 삭제".
- **ADR 콜아웃**(해당하는 경우): 앰버 색조 상자 안의 한 줄.

설명 단락은 없습니다. 다이어그램을 이해하는 데 단락이 필요하다면, 다이어그램을 다시 그리십시오.

## 다이어그램 패턴

후보에 맞는 패턴을 선택하십시오. 섞어 쓰십시오. 모든 다이어그램을 똑같이 보이게 만들지 마십시오. 다양성도 요점의 일부입니다.

### Mermaid 그래프 (의존성 / 호출 흐름을 위한 주력 도구)

요점이 "X가 Y를 호출하고 Y가 Z를 호출하는데, 이 엉망진창을 보라"일 때 Mermaid `flowchart` 또는 `graph`를 사용하십시오. 갑자기 떨어진 것처럼 느껴지지 않도록 Tailwind 스타일의 카드로 감싸십시오. classDef로 스타일을 지정하여 누수 엣지는 빨간색으로, 깊은 모듈은 어둡게 칠하십시오. 시퀀스 다이어그램은 "이전: 왕복 6회, 이후: 1회"에 잘 맞습니다.

```html
<div class="rounded-lg border border-slate-200 bg-white p-4">
  <pre class="mermaid">
    flowchart LR
      A[OrderHandler] --> B[OrderValidator]
      B --> C[OrderRepo]
      C -.leak.-> D[PricingClient]
      classDef leak stroke:#dc2626,stroke-width:2px;
      class C,D leak
  </pre>
</div>
```

### 직접 만든 상자와 화살표 (Mermaid의 레이아웃이 말을 듣지 않을 때)

테두리와 라벨이 있는 `<div>`로 모듈을 나타냅니다. 화살표는 relative 컨테이너 위에 absolute로 배치된 인라인 SVG `<line>` 또는 `<path>` 요소로 나타냅니다. "이후" 다이어그램이 내부가 회색으로 처리된 하나의 굵은 테두리를 가진 깊은 모듈처럼 느껴지기를 원할 때 사용하십시오. Mermaid는 그것을 적절한 무게감으로 렌더링하지 못합니다.

### 단면도 (계층화된 얕음에 적합)

수평 띠(`h-12 border-l-4`)를 쌓아 호출이 통과하는 계층을 보여 줍니다. 이전: 아무것도 하지 않는 6개의 얇은 계층. 이후: 통합된 책임이 라벨로 붙은 1개의 두꺼운 띠.

### 질량 다이어그램 ("구현만큼 넓은 인터페이스"에 적합)

모듈당 두 개의 직사각형입니다. 하나는 인터페이스 표면적, 하나는 구현입니다. 이전: 인터페이스 직사각형이 구현 직사각형과 거의 같은 높이(얕음). 이후: 인터페이스 직사각형은 짧고, 구현 직사각형은 높음(깊음).

### 호출 그래프 축약

이전: 중첩된 상자로 렌더링된 함수 호출 트리. 이후: 같은 트리가 하나의 상자로 축약되고, 이제 내부가 된 호출은 그 안에 흐리게 표시됩니다.

## 스타일 지침

- 기업 대시보드가 아니라 편집물 쪽으로 기울이십시오. 넉넉한 여백. 제목에는 세리프 글꼴을 선택적으로 사용합니다(`font-serif`는 stone/slate와 잘 어울립니다).
- 색상은 아껴 쓰십시오. 하나의 강조색(에메랄드 또는 인디고)에 누수를 위한 빨간색과 경고를 위한 앰버를 더합니다.
- 전/후가 스크롤 없이 편안하게 나란히 놓이도록 다이어그램 높이를 약 320px로 유지하십시오.
- 다이어그램 내부의 모듈 라벨에는 `text-xs uppercase tracking-wider`를 사용하여, UI가 아니라 도식처럼 읽히도록 하십시오.
- 스크립트는 Tailwind CDN과 Mermaid ESM 임포트뿐입니다. 그 외에 보고서는 정적입니다. 앱 코드가 없으며, Mermaid 자체의 렌더링 외에는 상호 작용이 없습니다.

## 최우선 권고 섹션

하나의 더 큰 카드입니다. 후보 이름, 이유에 대한 한 문장, 해당 카드로의 앵커 링크. 그것이 전부입니다.

## 어조

평이한 언어로 간결하게 쓰되, 아키텍처 명사와 동사는 `/codebase-design` 스킬에서 그대로 가져옵니다. 간결함이 표류의 핑계가 되어서는 안 됩니다.

**정확히 사용할 것:** module, interface, implementation, depth, deep, shallow, seam, adapter, leverage, locality.

**절대 대체하지 말 것:** component, service, unit(module 대신) · API, signature(interface 대신) · boundary(seam 대신) · layer, wrapper(module을 의미할 때 module 대신).

**스타일에 맞는 표현:**

- "Order 접수 모듈은 얕다: 인터페이스가 구현과 거의 일치한다."
- "가격 책정이 시임을 넘어 누수된다."
- "심화하라: 하나의 인터페이스, 테스트할 하나의 장소."
- "두 개의 어댑터가 시임을 정당화한다: 프로덕션에서는 HTTP, 테스트에서는 메모리 내."

**이점 글머리 기호**는 용어집 용어로 이득을 명명합니다. *"지역성: 버그가 하나의 모듈에 집중됨"*, *"레버리지: 하나의 인터페이스, N개의 호출 지점"*, *"인터페이스가 줄어들고, 구현이 래퍼를 흡수함"*. *"유지 관리하기 쉬움"*이나 *"더 깔끔한 코드"*라고 쓰지 마십시오. 그러한 용어는 용어집에 없으며 자리를 차지할 자격이 없기 때문입니다.

얼버무리지 말고, 헛기침하지 말고, "…라는 점은 주목할 만하다"라고 쓰지 마십시오. 문장이 글머리 기호가 될 수 있다면 글머리 기호로 만드십시오. 글머리 기호를 잘라 낼 수 있다면 잘라 내십시오. 용어가 `/codebase-design` 용어집에 없다면, 새로운 용어를 만들어 내기 전에 용어집에 있는 용어를 찾으십시오.
