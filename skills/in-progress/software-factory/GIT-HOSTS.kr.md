# Git 호스트

> 2026-10에 조사되었으며, 최신 상태임을 보장하지 않습니다. 방향을 잡는 데 사용한 다음, 현재의 선택지를 직접 조사하십시오. 제품, 가격, 제한, 베타 상태는 빠르게 변합니다.

## 유형

### 올인원 플랫폼

티켓 트래커, 오케스트레이터 역할을 하는 CI 시스템, 호스팅 러너가 함께 묶인 git 호스트로, 모두 하나의 이벤트 스트림과 하나의 권한 모델을 공유합니다. 하나의 제품이 git 호스트, 티켓 트래커, 오케스트레이터, 러너를 채우며, CI 실행 페이지가 관측 플랫폼까지 커버하는 경우도 많습니다. 모든 PR, 리뷰, 라벨, 검사 이벤트가 웹훅인 동시에 네이티브 트리거이므로, 이 유형은 가장 풍부한 트리거 목록을 가집니다.

**다음의 경우에 선택하십시오.** 팩토리가 작게 시작하는 경우, 코드가 이미 그곳에 있는 경우, 또는 사용자가 하나의 청구서와 하나의 로그인을 원하는 경우입니다. 이는 [SKILL.md](SKILL.md)의 "모두 GitHub에서" 설계입니다. 벤더들은 자체 에이전트도 제공하는데, 이는 사용자의 실행과 경쟁하거나 그중 하나로 끼워 넣을 수 있습니다.

- [GitHub](https://docs.github.com/en/rest/using-the-rest-api/rate-limits-for-the-rest-api): 기본값. Issues, Actions, Apps, 그리고 가장 큰 통합 생태계.
- [GitLab](https://about.gitlab.com/pricing/): 이슈, 머지 리퀘스트, CI/CD, 러너를 하나의 제품으로 제공하며, SaaS 또는 자체 관리형.

### 제품군 git 호스트

더 넓은 제품군의 한 모듈로 판매되는 git 호스트로, 티켓 트래커는 링크와 웹훅으로 연결된 형제 제품(Jira, Azure Boards)입니다. 트래커 이벤트는 두 번째 스트림으로 도착하므로, 오케스트레이터가 두 개의 이벤트 소스를 결합합니다.

**다음의 경우에 선택하십시오.** 조직이 이미 해당 제품군을 운영하고 있으며 구성원들이 Jira나 Azure Boards에서 생활하는 경우입니다. 팩토리는 그 트래커를 사람용 인터페이스로 이어받습니다.

- [Bitbucket Cloud](https://support.atlassian.com/bitbucket-cloud/docs/api-request-limits/): Atlassian의 git 호스트로, Jira 및 Bitbucket Pipelines와 짝을 이룹니다.
- [Azure DevOps (Azure Repos)](https://learn.microsoft.com/en-us/azure/devops/integrate/concepts/rate-limits): 하나의 조직 안에 Repos, Boards, Pipelines, Entra ID가 있으므로 네 자리를 모두 채웁니다.
- [AWS CodeCommit](https://aws.amazon.com/blogs/devops/aws-codecommit-returns-to-general-availability/): IAM ID를 가진 기본적인 git 호스트. 외부 트래커 및 CI와 짝을 지으십시오.

### 자체 호스팅 git 호스트

사용자가 자신의 인프라에서 운영하는 git 호스트로, 종종 같은 네트워크에서 오케스트레이터 및 러너와 나란히 운영됩니다. 운영자가 속도 제한을 설정하므로, 상한은 하드웨어입니다. 사용자는 그것이 채우는 모든 자리에 대해 업그레이드, 백업, 가동 시간을 책임집니다.

**다음의 경우에 선택하십시오.** 코드가 온프레미스나 에어갭 환경에 있어야 하는 경우, 사용자가 좌석당 비용을 0으로 원하는 경우, 또는 SaaS API 예산이 바쁜 팩토리를 제한하는 경우입니다. Forgejo와 Gitea는 소규모 팀에 적합하며 이슈와 GitHub Actions 호환 CI를 함께 제공합니다. GitLab 자체 관리형과 GitHub Enterprise Server는 조직에 적합하며 Apps와 서비스 계정을 유지합니다.

- [Forgejo](https://forgejo.org/2026-10-release-v17-0/): 커뮤니티가 관리하며 가볍고, Forgejo Actions를 갖추었습니다.
- [Gitea](https://about.gitea.com/): Gitea Actions를 갖춘 가벼운 호스트. 관리형으로도 판매됩니다.
- [GitLab 자체 관리형](https://about.gitlab.com/install/) 및 [GitHub Enterprise Server](https://docs.github.com/en/enterprise-server@latest): 사용자 자신의 인프라 위에서 동작하는 완전한 플랫폼.

### 리뷰 우선 및 탈중앙화 git 호스트

리뷰 모델이 브랜치와 PR 형태에서 벗어난 git 호스트입니다. 투표 라벨이 있는 커밋별 패치셋, 또는 사용자가 운영하는 노드들에 걸쳐 연합된 저장소입니다. 대부분의 팩토리 도구는 PR을 전제로 하므로, 연결 코드를 더 많이 만들어야 할 것으로 예상하십시오. Gerrit에서는 자동화된 검사 실행이 봇 계정에서 `Verified`에 투표하고, 사람이 `Code-Review`에 투표합니다.

**다음의 경우에 선택하십시오.** 사용자의 팀이 이미 이런 방식으로 리뷰하거나, 생태계보다 연합을 중시하는 경우입니다.

- [Gerrit](https://www.gerritcodereview.com/): 라벨 투표가 있는 패치셋 리뷰. Android와 Chromium의 모델입니다.
- [Tangled](https://blog.tangled.org/ci/): 스택형 PR과 자체 CI 러너를 갖춘, AT Protocol 기반의 git 호스팅.

### 에이전트 네이티브 git 호스트

에이전트를 주 작성자로 삼아 설계된 새로운 git 호스트입니다. 높은 커밋 처리량, 클론 대신 서버 측 읽기, 에이전트별 귀속 기록을 제공합니다. 이 유형 전체가 초기 단계이므로(2026-10 기준), 관문과 속도 제한이 공개되지 않았을 수 있습니다. 벤더에게 문의하십시오.

**다음의 경우에 선택하십시오.** 팩토리가 하나의 큰 저장소를 대상으로 많은 실행을 동시에 수행하며 클론 시간이나 API 제한이 지배적인 경우입니다. 단일 저장소의 미러에서 시범 운영하고, GitHub를 대안으로 유지하십시오.

- [Cursor Origin](https://cursor.com/origin): Graphite 팀이 만들었으며, GitHub 동기화와 서명된 PR, 리뷰, 푸시 웹훅을 갖추었습니다.
- [GitLab next-gen SCM](https://about.gitlab.com/blog/gitlab-next-gen-scm/): 클론이 필요 없는 에이전트 API를 갖춘, 재구축된 GitLab 백엔드.

### 실행을 위한 Git 저장소

수천 개 단위로 생성되는 헤드리스 API 우선 git 저장소입니다. 브랜치, 커밋, diff만 있으며, PR, 리뷰, 관문은 없습니다. 실행마다 발급되는 저장소별 단기 토큰과 함께 자리의 절반을 채웁니다.

**다음의 경우에 선택하십시오.** 실행에 저렴한 실행별 임시 저장소나 포크(티켓당 포크, 에이전트의 작업 상태)가 필요하고, PR은 여전히 위 유형 중 하나의 완전한 git 호스트에 올라가는 경우입니다.

- [Cloudflare Artifacts](https://www.cloudflare.com/product/artifacts/): Workers 위의 git 호환 저장소. 작업마다 기준선을 포크합니다.
- [Pierre code.storage](https://code.storage/docs): 임시 브랜치를 갖춘 화이트 라벨 git API.

## 추가 조사

각 후보를 다음 질문에 비추어 확인하십시오.

1. **트리거**: 어떤 이벤트(PR 열림, 푸시, 리뷰 제출, 라벨 추가, 검사 완료)가 웹훅으로 오케스트레이터에 도달하며, 전송은 서명됩니까?
2. **ID**: 실행이 전용 봇이나 앱 ID로 동작할 수 있습니까? 그래야 실행의 귀속이 유지되고, 자동화된 리뷰 실행이 다른 ID가 작성한 PR을 승인할 수 있으며, 실행 자체의 푸시가 다음 실행을 트리거하는지가 결정됩니다.
3. **관문**: 필수 검사, 필수 승인, 브랜치 보호가 사용자의 요금제와 저장소 공개 범위에서 사용 가능하며, 봇을 우회 목록에 올릴 수 있습니까?
4. **속도 제한**: 모든 러너의 모든 실행이 공유하는 API 예산은 얼마이며, 어떤 단위(설치, 토큰, 사용자, 작업 공간)이고, 어떻게 확장됩니까?
5. **채우는 자리**: 같은 제품이 티켓 트래커, 오케스트레이터, 러너, 관측 플랫폼 중 무엇을 커버합니까?

1차 자료에서 답을 찾으십시오. REST API 및 웹훅 참조, 속도 제한 페이지, 가격 및 요금제 비교 페이지, 액세스 토큰 또는 앱 문서, 변경 로그 또는 릴리스 노트입니다.

가장 빨리 낡는 것: 베타 및 프리뷰 상태(에이전트 네이티브 유형과 git 저장소 유형 전체), 속도 제한 수치, 어떤 요금제가 관문을 여는지, 그리고 인수, 서비스 종료, 재개 이후의 가용성입니다. 예를 들어 2026-10 기준으로, AWS CodeCommit은 신규 고객에게 다시 문을 열었으며 Bitbucket Data Center는 Cloud와의 하이브리드 라이선스로만 판매되었습니다.

## 오래 지속되는 함정

설계가 이에 의존하기 전에 각각이 여전히 유효한지 검증하십시오.

- **GitHub `GITHUB_TOKEN`은 연쇄를 끊습니다.** 내장 Actions 토큰으로 발생한 이벤트는 새로운 워크플로 실행을 시작하지 않으므로(`workflow_dispatch`와 `repository_dispatch` 제외), 이 토큰으로 푸시하는 실행은 다음 실행을 조용히 멈춥니다. 첫날부터 실행에 GitHub App ID를 부여하십시오.
- **관문은 종종 유료 요금제 뒤에 있습니다.** 2026-10 기준으로, 비공개 저장소의 GitHub 규칙 세트는 Pro, Team 또는 Enterprise가 필요하고, GitLab 승인 규칙은 Premium이 필요하며, 강제되는 Bitbucket 병합 검사는 Premium이 필요합니다.
- **속도 제한은 ID별이며, 봇의 유형에 따라 달라집니다.** 2026-10 기준으로, GitHub App 설치는 `GITHUB_TOKEN`의 1,000건에 비해 시간당 5,000건의 요청을 받습니다. Bitbucket 사용자 토큰은 기본 속도에 머무르는 반면 액세스 토큰은 확장됩니다. Azure DevOps는 접근 수준에 따라 봇의 예산을 높입니다.
- **제품군 트래커는 두 개의 이벤트 스트림을 의미합니다.** 오케스트레이터가 git 호스트와 티켓 트래커 이벤트를 직접 결합합니다.
