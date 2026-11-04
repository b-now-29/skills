# 러너

> 2026-10에 조사되었으며, 최신 상태임을 보장하지 않습니다. 방향을 잡는 데 사용한 다음, 현재의 선택지를 직접 조사하십시오. 제품, 가격, 제한, 베타 상태는 빠르게 변합니다.

러너는 **일회용(disposable)**입니다. 모든 실행은 새로운 머신에서 시작하며 아무것도 남기지 않습니다. 다섯 가지 유형이 이 자리를 채웁니다. 주로 에이전트 루프를 누가 소유하고 머신을 누가 소유하는지에 따라 다릅니다.

| 유형 | 에이전트 루프 | 머신 | 함께 채우는 자리 |
| --- | --- | --- | --- |
| CI 러너 | 사용자 소유, CI 작업 내부 | CI 벤더 소유, 또는 사용자 소유 | 오케스트레이터, 관측 플랫폼 |
| MicroVM API | 사용자 소유, 오케스트레이터 또는 러너에서 | 제공자 소유 | 없음 |
| 번들형 에이전트 플랫폼 | 벤더 소유 | 벤더 소유 | 오케스트레이터 일부, 관측 플랫폼 |
| 자체 워커 연결 | 벤더 소유 | 사용자 소유 | 오케스트레이터 일부, 관측 플랫폼 |
| 자체 VPS 또는 컨테이너 | 사용자 소유 | 사용자 소유 | 없음 |

러너 선택은 실행 단위로 이루어집니다. 리뷰 실행에는 저렴한 CI 러너를, 구현자 실행에는 microVM을 사용하는 것은 일반적인 설계입니다.

## CI 러너

git 호스트 자체의 워크플로 엔진이 시작하는, CI 작업마다 새로 생성되는 VM 또는 파드입니다. 에이전트 CLI는 작업 내의 한 단계입니다. 오케스트레이터는 워크플로 트리거(이슈, PR, 일정, 수동 디스패치)로 실행을 시작하며, 동시성 그룹이 두 실행이 같은 티켓을 다루지 않도록 합니다. 호스팅 러너는 구조적으로 일회용이며, 자체 호스팅 러너는 임시(ephemeral) 모드를 통해 그렇게 됩니다. 작업당 하나의 파드를 만들고, 이후 삭제합니다. 비용은 분 단위입니다.

**다음의 경우에 선택하십시오.** git 호스트가 GitHub 또는 GitLab이고 모든 트리거가 git 호스트 이벤트나 시계인 경우입니다. 워크플로 파일이 오케스트레이터이고 실행 페이지가 관측 플랫폼이므로, 하나의 제품이 세 자리를 채웁니다.

출발점:
- [GitHub Actions](https://docs.github.com/en/actions/reference/limits): 모두 GitHub로 구성된 팩토리의 기본값. [가격](https://docs.github.com/en/billing/reference/actions-runner-pricing).
- [Claude Code GitHub Action](https://code.claude.com/docs/en/github-actions): 워크플로 단계로서의 Claude Code.
- [GitLab 호스팅 러너](https://docs.gitlab.com/ci/runners/hosted_runners/linux/): 작업당 하나의 임시 VM.
- [Actions Runner Controller](https://docs.github.com/en/actions/concepts/runners/actions-runner-controller): 자체 호스팅. 사용자의 Kubernetes에서 작업당 하나의 임시 파드.

## MicroVM API

SDK 호출로 약 1초 만에 격리된 microVM(벤더들은 "샌드박스"라고 부름)을 생성합니다. 오케스트레이터는 그 안에서 명령을 실행하거나, 그 안에서 에이전트 CLI를 시작합니다. 비용은 vCPU와 RAM의 초 단위입니다. 오케스트레이터는 실행마다 하나를 생성하고, 끝나면 종료하며, 안전장치로 타임아웃을 설정합니다. 제공자들은 지속성 기능(일시 중지/재개, 스냅샷, 드라이브)도 판매합니다. 팩토리는 이를 캐시로 사용하며, 실행 간의 기억은 티켓 트래커, git 호스트, 오케스트레이터에 보관합니다.

**다음의 경우에 선택하십시오.** 팩토리가 자체 오케스트레이터(서버, 큐)를 가지고 있으며, 관리할 머신 없이 수명이 짧은 병렬 실행을 많이 원하는 경우입니다. 최대 실행 시간, 동시성 상한, 그리고 모델을 기다리는 시간이 청구되는지를 비교하십시오. 2026-10 기준으로 Vercel은 활성 CPU만 청구하므로, 그곳에서는 모델 대기 시간이 거의 무료입니다.

출발점: [E2B](https://e2b.dev/pricing), [Daytona](https://www.daytona.io/pricing), [Modal Sandboxes](https://modal.com/docs/guide/sandboxes), [Vercel Sandbox](https://vercel.com/docs/vercel-sandbox/pricing).

## 번들형 에이전트 플랫폼

러너가 포함된 호스팅 코딩 에이전트입니다. 벤더가 실행마다 새로운 VM이나 컨테이너를 프로비저닝하고, 그곳에서 자체 에이전트 루프를 실행하며, 브랜치나 PR을 푸시합니다. 브랜치만 남습니다. 실행은 git 호스트나 티켓 트래커에서의 @멘션 또는 할당, 채팅 메시지, 일정, 또는 HTTP 호출로 시작되므로, 플랫폼이 오케스트레이터의 상당 부분을 채웁니다. 대화 기록 뷰가 관측 플랫폼을 채웁니다. 비용은 좌석이나 구독에 포함되거나, 실행 단위로 청구됩니다.

**다음의 경우에 선택하십시오.** 사용자가 움직이는 부품을 최소화하기를 원하며 해당 벤더의 에이전트에 만족하는 경우입니다. 그 트리거가 사용자의 티켓 트래커를 지원하는지 확인하십시오.

출발점:
- [Claude Code cloud](https://code.claude.com/docs/en/claude-code-on-the-web), cron, API, GitHub 이벤트 트리거를 위한 [scheduled tasks](https://code.claude.com/docs/en/routines)와 함께.
- [Claude Managed Agents](https://platform.claude.com/docs/en/managed-agents/overview): API 우선. 환경에 대해 실행을 생성하고 이벤트를 스트리밍합니다.
- [Codex cloud](https://developers.openai.com/codex/cloud): 작업당 하나의 컨테이너.
- [Copilot coding agent](https://docs.github.com/en/copilot/concepts/agents/coding-agent/about-coding-agent): 이슈를 Copilot에 할당합니다. 러너는 GitHub Actions 러너입니다.

## 자체 워커 연결 (Bring-your-own worker)

번들형 플랫폼이 에이전트 루프와 실행 큐를 유지하지만, 도구 호출은 사용자가 호스팅하는 워커에서 실행됩니다. 워커는 벤더 쪽으로 아웃바운드 폴링을 하여 실행을 가져가고, 실행한 뒤 종료합니다. 자체 호스팅 CI 러너와 같은 형태입니다. 일회성은 사용자의 몫입니다. 각 실행이 새로운 디스크를 갖도록 Kubernetes나 microVM API 아래에서 워커를 실행하십시오. 비용은 벤더의 좌석 또는 사용량에 사용자의 머신 비용을 더한 것입니다.

**다음의 경우에 선택하십시오.** 사용자가 번들형 에이전트를 원하지만, 실행이 사설 네트워크에 접근해야 하거나, 데이터를 사용자의 머신에 보관해야 하거나, 사용자 정의 하드웨어를 사용해야 하는 경우입니다.

출발점: [Claude Code self-hosted environments](https://code.claude.com/docs/en/self-hosted-environments), [Cursor self-hosted pool](https://cursor.com/docs/cloud-agent/self-hosted-pool), [Copilot coding agent on ARC](https://docs.github.com/en/copilot/how-tos/use-copilot-agents/coding-agent/customize-the-agent-environment).

## 자체 VPS 또는 컨테이너

사용자가 임대하거나 운영하는 머신에서 실행마다 새로운 컨테이너(또는 머신)를 사용합니다. 머신은 몇 달 동안 유지될 수 있지만, 컨테이너는 한 번의 실행 동안만 유지됩니다. 최대 실행 시간은 오케스트레이터가 설정하는 기한입니다. 일회성은 `docker run --rm`, `ttlSecondsAfterFinished: 0`인 Kubernetes Job, 또는 끝날 때 파기되는 머신에서 나옵니다. 모든 캐시는 다음 실행이 선택 사항으로 취급하는 경로에 둡니다. 비용은 월 정액, 또는 실행 중인 동안의 초 단위입니다.

**다음의 경우에 선택하십시오.** 실행이 길거나, 꾸준하거나, 무거운 경우, 시간당 비용이 지배적인 경우, 또는 서버가 이미 오케스트레이터를 호스팅하고 있는 경우입니다.

출발점: [Fly Machines](https://docs.fly.io/machines/overview) ([가격](https://docs.fly.io/about/pricing)), [Hetzner Cloud](https://www.hetzner.com/cloud/)와 Docker, [Kubernetes Jobs](https://kubernetes.io/docs/concepts/workloads/controllers/job/).

## 추가 조사

### 자리를 결정하는 질문

팩토리의 실행을 염두에 두고, 각 후보를 다음 질문에 비추어 확인하십시오.

1. **오케스트레이터는 어떻게 러너를 시작합니까?** 워크플로 트리거, SDK 호출, @멘션, HTTP 호출, 또는 워커가 가져가는 벤더 큐. 설계가 이미 명시한 오케스트레이터에 들어맞습니까?
2. **최대 실행 시간과 동시성 상한은 얼마입니까?** 요금제 등급별로 기본 타임아웃과 최대치를 모두 찾고, 상한에 도달하면 어떻게 되는지 확인하십시오. 이를 설계에서 가장 긴 실행 및 가장 바쁜 순간과 비교하십시오.
3. **비용 구조는 어떻습니까?** 분 단위, vCPU 및 RAM의 초 단위, 활성 CPU만, 실행당, 좌석당, 또는 월 정액. 모델을 기다리는 시간이 청구됩니까? 모델 토큰이 가격에 포함됩니까, 아니면 별도입니까?
4. **일회성은 어떻게 달성됩니까?** 기본적으로 새로 생성되는지, 임시 플래그가 있는지, 또는 오케스트레이터 자체의 정리 작업인지. 어떤 지속성 기능이 있으며, 설계에서 이를 캐시로 제한할 수 있습니까?
5. **실행이 무엇에 접근할 수 있습니까?** 사설 네트워크 접근, 아웃바운드 방화벽 또는 허용 목록, 시크릿이 러너에 전달되는 방식, 그리고 그 밖에 누가 시크릿을 읽을 수 있는지.
6. **그 밖에 어떤 자리를 채웁니까?** 읽어 들이는 트리거를 오케스트레이터 커버리지로, 실행 페이지나 대화 기록을 관측 플랫폼 커버리지로 계산하십시오.

### 답이 있는 곳

- 랜딩 페이지보다는 벤더의 **제한 또는 할당량 페이지**와 **가격 페이지**.
- 생성 호출에 대한 **SDK 또는 API 참조**: 타임아웃, 수명 주기, 네트워크 매개변수.
- 방화벽, 허용 목록, 시크릿 처리에 대한 **보안 또는 네트워킹 문서**.
- 베타, 프리뷰, 정식 출시 상태와 요금제 제한(Team, Enterprise)에 대한 **변경 로그 또는 릴리스 노트**.
- CI 러너의 경우, git 호스트의 **청구 문서**.

### 가장 빨리 낡는 것

- **가격과 무료 제공량.** 2026-10 기준으로, GitHub는 자체 호스팅 러너에 대한 분당 요금을 발표했다가 연기했습니다.
- **베타, 프리뷰, 조기 접근 상태**, 그리고 어떤 요금제가 기능을 여는지. 2026-10 기준으로, Claude Managed Agents와 Claude Code self-hosted environments는 둘 다 베타였습니다.
- 등급별 **기본 타임아웃과 최대 실행 시간**.
- 번들형 플랫폼의 **트리거 통합**: 어떤 티켓 트래커와 채팅 도구가 실행을 시작하는지.
- **시작 시간**은 벤더의 주장입니다. 중요하다면 직접 측정하십시오.

위의 유형별 특성(누가 루프를 소유하는지, 누가 머신을 소유하는지, 어떤 자리를 채우는지)은 천천히 변합니다. 이곳의 어떤 수치보다 그 특성을 신뢰하십시오.
