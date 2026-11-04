# 관측 플랫폼

> 2026-10에 조사되었으며, 최신 상태임을 보장하지 않습니다. 방향을 잡는 데 사용한 다음, 현재의 선택지를 직접 조사하십시오. 제품, 가격, 제한, 베타 상태는 빠르게 변합니다.

관측 플랫폼 자리를 채우거나, 의도적으로 없음을 결정하기 위한 안내입니다. 유형은 **사람이 실행 내부에서 무엇을 보아야 하는가**에 따라 나뉩니다. 실행의 로그, 에이전트 트레이스(각 모델 호출과 도구 호출을 스팬으로), 또는 사용자 시스템의 나머지와 결합된 그 트레이스입니다. 자체 호스팅 대 SaaS 구분은 마지막 세 유형에 걸쳐 적용됩니다. 플랫폼이 보는 것에 따라 실행이 동작해야 할 때는, 플랫폼을 티켓 소스로 만드십시오. 모니터가 티켓을 제출하고, 실행이 그것을 읽습니다.

## 러너가 연결되는 방식

모든 유형은 다섯 가지 연결 방식 중 하나를 통해 데이터를 받습니다. 자리를 채울 때 제품과 함께 연결 방식을 명시하십시오.

- **하네스 OTel**: 에이전트 하네스가 직접 OpenTelemetry를 내보냅니다. Claude Code와 Claude Agent SDK는 `CLAUDE_CODE_ENABLE_TELEMETRY=1`과 `OTEL_*` 변수를 받으며, 프롬프트와 도구 출력은 옵트인입니다. Codex CLI는 `config.toml`의 `[otel]` 블록을 받습니다. ([Claude Agent SDK](https://code.claude.com/docs/en/agent-sdk/observability), [Claude Code](https://code.claude.com/docs/en/monitoring-usage), [Codex config](https://developers.openai.com/codex/config-advanced))
- **플랫폼 푸시**: 모델 플랫폼이 대신 트레이스를 보냅니다. Claude Managed Agents가 Claude Console에서 설정한 OTLP 대상으로 보내는 것이 그 예입니다. ([Claude docs](https://platform.claude.com/docs/en/manage-claude/opentelemetry/api))
- **SDK 래퍼**: 러너 코드에서의 한 번의 호출입니다. LangSmith의 `configure_claude_agent_sdk()`와 같은 것입니다.
- **훅 플러그인**: Claude Code 훅이 각 Stop 시점에 세션 기록을 읽어 전송합니다. Langfuse의 Claude Code 플러그인이 그 예입니다.
- **게이트웨이**: 러너의 모델 기본 URL이 로깅 프록시를 가리킵니다. 러너 코드가 전혀 필요 없지만, 모델 호출만 볼 수 있습니다. 하네스 내부의 도구 호출은 보이지 않습니다.

OpenTelemetry는 공통 전송 규격입니다. 하네스 OTel과 플랫폼 푸시는 어떤 OTLP 백엔드에든 도착합니다. GenAI 시맨틱 규약(`invoke_agent`, `chat`, `execute_tool` 스팬)은 아직 정착 중이므로, 스팬 이름이 바뀔 것으로 예상하십시오. ([OTel GenAI agent spans](https://opentelemetry.io/docs/specs/semconv/gen-ai/gen-ai-agent-spans))

## 유형 1: 없음 (러너나 오케스트레이터 제품이 충분히 보여 줌)

**무엇인가**: 사람이 러너나 오케스트레이터가 이미 보여 주는 곳에서 각 실행을 읽습니다. CI 실행 페이지, 샌드박스 대시보드, 실행 산출물로 저장된 에이전트의 대화 기록 등입니다. 만들 연결 방식이 없고, 러너만큼 자체 호스팅되며, 러너의 비용에 포함됩니다.

**팩토리가 선택하는 경우**: 하루에 실행이 적고, 한 사람이 지켜보며, 질문이 "실패했는가, 그리고 무엇을 출력했는가?"인 경우입니다. 대부분의 팩토리는 여기서 시작하며, 실행 간 검색, 실행별 토큰이나 비용 집계, 또는 러너가 보관하는 것보다 긴 보존 기간이 필요해지면 여기서 벗어납니다.

**출발점**: [GitHub Actions 실행 로그](https://docs.github.com/en/organizations/managing-organization-settings/configuring-the-retention-period-for-github-actions-artifacts-and-logs-in-your-organization), [E2B 샌드박스 로그 및 지표](https://e2b.dev/docs), [Daytona 샌드박스 텔레메트리](https://www.daytona.io/docs/en/observability/otel-collection/), [OpenAI Agents SDK 트레이스](https://openai.github.io/openai-agents-python/tracing/). 샌드박스 제품은 종종 같은 데이터를 OTLP로 전달하며, 이것이 유형 2로 나가는 경로입니다.

**검증할 것**: 러너 제품별 보존 일수. 일부 샌드박스는 아주 짧게만 보관합니다(Daytona: 3일, 2026-10 기준).

## 유형 2: LLM 및 에이전트 트레이싱 플랫폼

**무엇인가**: 에이전트 트레이스를 중심으로 구축된 백엔드입니다. 각 실행을 모델 호출과 도구 호출의 트리로 보여 주며, 토큰 비용, 프롬프트, 세션을 함께 제공하고, 대개 그 위에 평가와 데이터셋 기능이 있습니다.

**팩토리가 선택하는 경우**: 사람이 여러 실행에 걸쳐 "에이전트가 왜 그렇게 했는가?"를 묻는 경우, 회고 실행이나 사람이 실행들을 비교하는 경우, 토큰 지출에 실행별 집계가 필요한 경우입니다. 오픈 소스 제품을 자체 호스팅하면 대화 기록을 내부에 보관할 수 있습니다.

**유형의 특성**: 하네스 OTel, SDK 래퍼, 또는 훅 플러그인을 받으며, 플랫폼 푸시도 받는 경우가 많습니다. 사용량에 따라 청구되며, 에이전트 실행은 스팬이 많으므로(도구 호출당 스팬 하나), 요청당이 아니라 실행당 예산을 잡으십시오.

**출발점**: [Langfuse](https://langfuse.com/pricing)와 [Arize Phoenix](https://phoenix.arize.com)(오픈 소스, 자체 호스팅 가능), [LangSmith](https://www.langchain.com/pricing-langsmith), [Braintrust](https://www.braintrust.dev/pricing).

**검증할 것**: 무료 등급 제한, 청구 단위(트레이스, 스팬, 단위 또는 GB. Braintrust는 2026-03에 GB로 전환함), 어떤 등급이 자체 호스팅을 허용하는지, 그리고 현재의 소유 관계.

## 유형 3: 범용 APM 및 로깅 백엔드

**무엇인가**: 사용자의 기존 관측 스택(모든 서비스의 로그, 지표, 분산 트레이스)에 에이전트 또는 LLM 뷰를 추가한 것입니다.

**팩토리가 선택하는 경우**: 팀이 이미 비용을 지불하고 있는 경우, 실행을 앱 자체의 트레이스와 결합해야 하는 경우(Agent SDK는 `TRACEPARENT`를 전파하므로, 실행이 호출자의 트레이스 안에 중첩됨), 또는 모니터 티켓 소스가 이미 이 백엔드에서 읽고 있는 경우입니다.

**유형의 특성**: 하네스 OTel이 벤더의 OTLP 엔드포인트로 바로 전송됩니다. GB, 이벤트, 또는 호스트 단위로 가격이 매겨지므로, 팩토리의 사용량은 기존 청구서에서는 반올림 오차 수준이지만 새 청구서에서는 놀랄 만한 금액이 됩니다.

**출발점**: [Datadog Agent Observability](https://www.datadoghq.com/product/llm-observability/), [Grafana Cloud](https://grafana.com/pricing/), [Honeycomb](https://www.honeycomb.io/pricing), [SigNoz](https://signoz.io/pricing/)(오픈 소스).

**검증할 것**: 에이전트 뷰가 정식 출시(GA)인지 프리뷰인지, 어떤 하네스에 설정 가이드가 있는지, 그리고 무료 등급 사용량.

## 유형 4: 요청 로깅을 갖춘 LLM 게이트웨이

**무엇인가**: 러너와 모델 제공자 사이의 프록시로, 모든 요청과 응답을 기록하며, 라우팅, 키, 예산, 캐싱을 함께 제공합니다.

**팩토리가 선택하는 경우**: 사용자가 실행별 지출 상한이나 여러 러너를 위한 하나의 키 보관소를 원하며 로깅이 그에 딸려 오는 경우, 또는 하네스에 자체 내보내기 기능이 없는 경우입니다. 모델 호출만 볼 수 있으므로, 도구 호출을 위해 유형 2 또는 3과 짝을 지으십시오.

**출발점**: [LiteLLM Proxy](https://docs.litellm.ai/docs/proxy/logging)(오픈 소스, 로그를 Langfuse나 OTel로 전달), [Portkey](https://portkey.ai/pricing).

**검증할 것**: SaaS의 요청당 가격, 그리고 제품이 여전히 활발히 개발되고 있는지(Helicone은 인수 후 유지 관리 모드에 들어감, 2026-10 기준).

## 추가 조사

이 자리를 결정하는 질문에 비추어 각 후보를 확인하십시오.

1. **러너나 오케스트레이터가 이미 충분히 보여 줍니까?** 사람이 필요로 하는 것(실행 간 검색, 실행별 비용, 보존 기간)을 실행 페이지나 샌드박스 대시보드가 제공하는 것과 비교하십시오. 여기서 '예'라면 의도적인 없음을 의미합니다.
2. **에이전트 하네스는 트레이스를 어떻게 내보냅니까?** 하네스가 다섯 가지 연결 방식 중 무엇을 지원하는지, 그리고 제품이 무엇을 받는지 찾으십시오. 도구 호출이 스팬으로 도착하는지, 프롬프트와 도구 출력에 옵트인이 필요한지 확인하십시오.
3. **자체 호스팅이 가능합니까?** 라이선스, 어떤 등급이 이를 허용하는지, 그리고 무엇 위에서 실행되는지. 대화 기록을 내부에 보관해야 할 때 결정적입니다.
4. **비용 구조는 어떻습니까?** 청구 단위, 무료 등급, 그리고 도구 호출당 스팬 하나를 전제로 한 실행당 추정치에 하루 실행 수를 곱한 값.
5. **보존 기간은 얼마나 됩니까?** 각 등급에서 보관되는 일수를, 실행이 잘못되었을 때 사람이 얼마나 과거까지 살펴보는지와 비교하십시오.

**답이 있는 곳**: 벤더의 가격 페이지(단위, 등급, 보존 기간), 특정 하네스에 대한 벤더의 통합 문서, 하네스 자체의 모니터링 문서(무엇을 내보내는지, 어떤 플래그가 베타인지), OpenTelemetry GenAI 시맨틱 규약, 라이선스와 릴리스 활동을 위한 제품의 저장소, 소유 관계 변경을 위한 벤더의 변경 로그나 블로그.

**가장 빨리 낡는 것**: 무료 등급 제한과 가격, 베타 및 프리뷰 플래그(Claude Code 트레이스 내보내기, Console 플랫폼 푸시, 벤더의 에이전트 뷰), 소유 관계와 유지 관리 상태, 청구 단위, 보존 일수, GenAI 스팬 이름.
