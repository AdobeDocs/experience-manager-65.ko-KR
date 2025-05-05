---
title: 작업 오프로드
description: 토폴로지에서 AEM 인스턴스를 구성 및 사용하여 특정 유형의 처리를 수행하는 방법을 알아봅니다.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring
content-type: reference
feature: Configuring
exl-id: 429c96ff-4185-4215-97e8-9bd2c130a9b1
solution: Experience Manager, Experience Manager Sites
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '2318'
ht-degree: 1%

---

# 작업 오프로드{#offloading-jobs}

## 소개 {#introduction}

오프로드는 토폴로지의 Experience Manager 인스턴스 간에 처리 작업을 분산합니다. 오프로딩을 사용하면 특정 유형의 처리를 수행하기 위해 특정 Experience Manager 인스턴스를 사용할 수 있습니다. 특화된 처리를 통해 사용 가능한 서버 리소스의 사용을 극대화할 수 있습니다.

오프로딩은 [Apache Sling Discovery](https://sling.apache.org/documentation/bundles/discovery-api-and-impl.html) 및 Sling JobManager 기능을 기반으로 합니다. 오프로딩을 사용하려면 토폴로지에 Experience Manager 클러스터를 추가하고 클러스터가 처리하는 작업 항목을 식별합니다. 클러스터는 하나 이상의 Experience Manager 인스턴스로 구성되므로 단일 인스턴스가 클러스터로 간주됩니다.

토폴로지에 인스턴스를 추가하는 방법에 대한 자세한 내용은 [토폴로지 관리](/help/sites-deploying/offloading.md#administering-topologies)를 참조하십시오.

### 작업 배포 {#job-distribution}

Sling JobManager 및 JobConsumer를 사용하면 토폴로지에서 처리되는 작업을 만들 수 있습니다.

* 작업 관리자: 특정 주제에 대한 작업을 생성하는 서비스입니다.
* JobConsumer: 하나 이상의 주제의 작업을 실행하는 서비스입니다. 동일한 주제에 대해 여러 JobConsumer 서비스를 등록할 수 있습니다.

JobManager가 작업을 생성할 때 오프로딩 프레임워크는 토폴로지에서 Experience Manager 클러스터를 선택하여 작업을 실행합니다.

* 클러스터에는 작업 주제에 대해 등록된 JobConsumer를 실행 중인 인스턴스가 하나 이상 포함되어야 합니다.
* 클러스터에서 하나 이상의 인스턴스에 대해 항목을 활성화해야 합니다.

작업 배포 개선에 대한 자세한 내용은 [항목 사용량 구성](/help/sites-deploying/offloading.md#configuring-topic-consumption)을 참조하십시오.

![chlimage_1-109](assets/chlimage_1-109.png)

오프로딩 프레임워크가 작업을 실행할 클러스터를 선택하고 클러스터가 여러 인스턴스로 구성된 경우 Sling 배포는 클러스터에서 작업을 실행할 인스턴스를 결정합니다.

### 작업 페이로드 {#job-payloads}

오프로딩 프레임워크는 작업을 저장소의 리소스와 연결하는 작업 페이로드를 지원합니다. 작업 페이로드는 처리 리소스를 위해 작업을 만들고 작업을 다른 컴퓨터로 오프로드할 때 유용합니다.

작업 생성 시 페이로드는 작업을 생성하는 인스턴스에만 위치할 수 있습니다. 작업을 오프로드할 때 복제 에이전트는 페이로드가 작업을 최종적으로 소비하는 인스턴스에 생성되는지 확인합니다. 작업 실행이 완료되면 역복제를 통해 페이로드가 작업을 생성한 인스턴스로 다시 복사됩니다.

## 토폴로지 관리 {#administering-topologies}

토폴로지는 오프로딩에 참여하는 느슨하게 결합된 Experience Manager 클러스터입니다. 클러스터는 하나 이상의 Experience Manager 서버 인스턴스로 구성됩니다(단일 인스턴스는 클러스터로 간주됨).

각 Experience Manager 인스턴스는 다음 오프로딩 관련 서비스를 실행합니다.

* 검색 서비스: 토폴로지 커넥터에 토폴로지에 가입하도록 요청을 보냅니다.
* 토폴로지 커넥터: 조인 요청을 수신하고 각 요청을 수락하거나 거부합니다.

토폴로지의 모든 구성원에 대한 검색 서비스는 한 구성원의 토폴로지 커넥터를 가리킵니다. 다음 섹션에서 이 멤버를 루트 멤버라고 합니다.

![chlimage_1-110](assets/chlimage_1-110.png)

토폴로지의 각 클러스터에는 리더로 인식되는 인스턴스가 포함되어 있습니다. 클러스터 리더는 클러스터의 다른 구성원을 대신하여 토폴로지와 상호 작용합니다. 지시선이 클러스터를 떠나면 클러스터에 대한 새 지시선이 자동으로 선택됩니다.

### 토폴로지 보기 {#viewing-the-topology}

토폴로지 브라우저를 사용하여 Experience Manager 인스턴스가 참여하고 있는 토폴로지의 상태를 살펴봅니다. 토폴로지 브라우저에는 토폴로지의 클러스터 및 인스턴스가 표시됩니다.

각 클러스터에 대해 각 멤버가 클러스터에 가입된 순서와 리더인 멤버를 나타내는 클러스터 멤버 목록이 표시됩니다. Current 속성은 현재 관리 중인 인스턴스를 나타냅니다.

클러스터의 각 인스턴스에 대해 몇 가지 토폴로지 관련 속성을 볼 수 있습니다.

* 인스턴스의 작업 소비자에 대한 주제 허용 목록.
* 토폴로지와의 연결을 위해 노출되는 엔드포인트입니다.
* 오프로드용으로 인스턴스가 등록된 작업 주제입니다.
* 인스턴스가 처리하는 작업 주제입니다.

1. Touch UI를 사용하여 도구 탭을 클릭합니다. ([http://localhost:4502/tools.html](http://localhost:4502/tools.html))
1. Granite 작업 영역에서 오프로딩 브라우저 를 클릭합니다.
1. 탐색 패널에서 토폴로지 브라우저 를 클릭합니다.

   토폴로지에 참여하는 클러스터가 나타납니다.

   ![chlimage_1-111](assets/chlimage_1-111.png)

1. 클러스터를 눌러 클러스터의 인스턴스 목록과 해당 ID, 현재 상태 및 지시선 상태를 확인합니다.
1. 자세한 속성을 보려면 인스턴스 ID를 클릭하십시오.

웹 콘솔을 사용하여 토폴로지 정보를 볼 수도 있습니다. 콘솔은 토폴로지 클러스터에 대한 추가 정보를 제공합니다.

* 로컬 인스턴스는 무엇입니까?
* 이 인스턴스가 토폴로지에 연결하는 데 사용하는 토폴로지 커넥터 서비스(송신) 및 이 인스턴스에 연결하는 서비스(수신)
* 토폴로지 및 인스턴스 속성에 대한 변경 내역.

다음 절차를 사용하여 웹 콘솔의 토폴로지 관리 페이지를 엽니다.

1. 브라우저에서 웹 콘솔을 엽니다. ([http://localhost:4502/system/console](http://localhost:4502/system/console))
1. 메인 > 토폴로지 관리 를 클릭합니다.

   ![chlimage_1-112](assets/chlimage_1-112.png)

### 토폴로지 멤버십 구성 {#configuring-topology-membership}

Apache Sling 리소스 기반 검색 서비스는 각 인스턴스에서 실행되어 Experience Manager 인스턴스가 토폴로지와 상호 작용하는 방법을 제어합니다.

검색 서비스는 토폴로지와의 연결을 설정하고 유지하기 위해 Topology Connector 서비스에 정기적인 POST 요청(하트비트)을 보냅니다. 토폴로지 커넥터 서비스는 토폴로지에 연결할 수 있는 IP 주소 또는 호스트 이름의 허용 목록을 유지 관리합니다.

* 인스턴스를 토폴로지에 연결하려면 루트 멤버의 토폴로지 커넥터 서비스 URL을 지정하십시오.
* 인스턴스가 토폴로지에 연결할 수 있도록 하려면 루트 멤버의 토폴로지 커넥터 서비스 허용 목록에 인스턴스를 추가하십시오.

웹 콘솔 또는 sling:OsgiConfig 노드를 사용하여 org.apache.sling.discovery.impt.Config 서비스의 다음 속성을 구성합니다.

<table>
 <tbody>
  <tr>
   <th>속성 이름</th>
   <th>OSGi 이름</th>
   <th>설명</th>
   <th>기본 값</th>
  </tr>
  <tr>
   <td>하트비트 시간 초과(초)</td>
   <td>heartbeatTime</td>
   <td>타겟팅된 인스턴스가 사용할 수 없는 것으로 간주되기 전에 하트비트 응답을 기다리는 시간(초)입니다. </td>
   <td>20</td>
  </tr>
  <tr>
   <td>하트비트 간격(초)</td>
   <td>하트비트 간격</td>
   <td>하트비트 사이의 시간(초)입니다.</td>
   <td>15</td>
  </tr>
  <tr>
   <td>최소 이벤트 지연(초)</td>
   <td>minEventDelay</td>
   <td><p>토폴로지가 변경되면 TOPOLOGY_CHANGING에서 TOPOLOGY_CHANGED로의 상태 변경을 지연할 시간입니다. 상태가 TOPOLOGY_CHANGING일 때 발생하는 각 변경은 이 시간만큼 지연을 증가시킨다.</p> <p>이 지연으로 인해 리스너가 이벤트로 넘치지 않습니다. </p> <p>지연을 사용하지 않으려면 0이나 음수를 지정하십시오.</p> </td>
   <td>3</td>
  </tr>
  <tr>
   <td>토폴로지 커넥터 URL</td>
   <td>topologyConnectorUrl</td>
   <td>하트비트 메시지를 보낼 토폴로지 커넥터 서비스의 URL입니다.</td>
   <td>http://localhost:4502/libs/sling/topology/connector</td>
  </tr>
  <tr>
   <td>토폴로지 커넥터 허용 목록</td>
   <td>topologyConnectorWhitelist</td>
   <td>로컬 토폴로지 커넥터 서비스에서 토폴로지에 허용하는 IP 주소 또는 호스트 이름 목록입니다. </td>
   <td><p>localhost</p> <p>127.0.0.1</p> </td>
  </tr>
  <tr>
   <td>저장소 설명자 이름</td>
   <td>leaderSelectionRepositoryDescriptor</td>
   <td> </td>
   <td>&lt;값 없음&gt;</td>
  </tr>
 </tbody>
</table>

다음 절차에 따라 CQ 인스턴스를 토폴로지의 루트 멤버에 연결합니다. 이 절차에서는 인스턴스를 루트 토폴로지 멤버의 토폴로지 커넥터 URL로 지정합니다. 토폴로지의 모든 멤버에 대해 이 절차를 수행합니다.

1. 브라우저에서 웹 콘솔을 엽니다. ([http://localhost:4502/system/console](http://localhost:4502/system/console))
1. 메인 > 토폴로지 관리 를 클릭합니다.
1. 검색 서비스 구성을 클릭합니다.
1. Topology Connector URL 속성에 항목을 추가하고 루트 토폴로지 멤버의 Topology Connector 서비스 URL을 지정합니다. URL의 형식은 https://rootservername:4502/libs/sling/topology/connector입니다.

토폴로지의 루트 멤버에 대해 다음 절차를 수행합니다. 이 절차에서는 다른 토폴로지 멤버의 이름을 해당 검색 서비스 허용 목록에 추가합니다.

1. 브라우저에서 웹 콘솔을 엽니다. ([http://localhost:4502/system/console](http://localhost:4502/system/console))
1. 메인 > 토폴로지 관리 를 클릭합니다.
1. 검색 서비스 구성을 클릭합니다.
1. 토폴로지의 각 멤버에 대해 Topology Connector 허용 목록 속성에 항목을 추가하고 토폴로지 멤버의 호스트 이름 또는 IP 주소를 지정합니다.

## 주제 사용량 구성 {#configuring-topic-consumption}

오프로딩 브라우저를 사용하여 토폴로지의 Experience Manager 인스턴스에 대한 항목 소비를 구성합니다. 각 인스턴스에 대해 인스턴스가 사용하는 주제를 지정할 수 있습니다. 예를 들어 하나의 인스턴스만 특정 유형의 주제를 사용하도록 토폴로지를 구성하려면 하나를 제외한 모든 인스턴스에서 주제를 비활성화합니다.

작업은 라운드 로빈 논리를 사용하여 관련 주제가 활성화된 인스턴스에 배포됩니다.

1. Touch UI를 사용하여 도구 탭을 클릭합니다. ([http://localhost:4502/tools.html](http://localhost:4502/tools.html))
1. Granite 작업 영역에서 오프로딩 브라우저 를 클릭합니다.
1. 탐색 패널에서 오프로딩 브라우저 를 클릭합니다.

   오프로딩 주제와 해당 주제를 사용할 수 있는 서버 인스턴스가 나타납니다.

   ![chlimage_1-113](assets/chlimage_1-113.png)

1. 인스턴스에 대한 주제 소비를 비활성화하려면 주제 이름 아래에서 인스턴스 옆에 있는 비활성화 를 클릭합니다.
1. 인스턴스에 대한 모든 주제 소비를 구성하려면 주제 아래의 인스턴스 식별자를 클릭합니다.

   ![chlimage_1-114](assets/chlimage_1-114.png)

1. 항목 옆에 있는 다음 단추 중 하나를 클릭하여 인스턴스에 대한 소비 동작을 구성한 다음 저장을 클릭합니다.

   * 활성화됨: 이 인스턴스는 이 주제의 작업을 사용합니다.
   * 비활성화됨: 이 인스턴스는 이 주제의 작업을 사용하지 않습니다.
   * 제외: 이 인스턴스는 이 주제의 작업만 사용합니다.

   **참고:** 항목에 대해 [제외]를 선택하면 다른 모든 항목이 자동으로 [사용 안 함]으로 설정됩니다.

### 설치된 작업 소비자 {#installed-job-consumers}

Experience Manager과 함께 여러 JobConsumer 구현이 설치됩니다. 이러한 JobConsumer가 등록된 항목이 오프로딩 브라우저에 나타납니다. 표시되는 추가 항목은 사용자 정의 JobConsumer가 등록한 항목입니다. 다음 표에서는 기본 JobConsumer에 대해 설명합니다.

| 작업 항목 | 서비스 PID | 설명 |
|---|---|---|
| / | org.apache.sling.event.impl.jobs.deprecated.EventAdminBridge | Apache Sling과 함께 설치됩니다. 이전 버전과의 호환성을 위해 OSGi 이벤트 관리자가 생성하는 작업을 처리합니다. |
| com/day/cq/replication/job/&ast; | com.day.cq.replication.impl.AgentManagerImpl | 작업 페이로드를 복제하는 복제 에이전트입니다. |

<!--
| com/adobe/granite/workflow/offloading |com.adobe.granite.workflow.core.offloading.WorkflowOffloadingJobConsumer |Processes jobs that the DAM Update Asset Offloader workflow generates. |
-->

### 인스턴스에 대한 항목 비활성화 및 활성화 {#disabling-and-enabling-topics-for-an-instance}

Apache Sling 작업 소비자 관리자 서비스는 주제 허용 목록 및 차단 목록 속성을 제공합니다. Experience Manager 인스턴스에서 특정 항목의 처리를 활성화 또는 비활성화하도록 이러한 속성을 구성합니다.

**참고:** 인스턴스가 토폴로지에 속해 있으면 토폴로지의 모든 컴퓨터에서 오프로딩 브라우저를 사용하여 항목을 사용하거나 사용하지 않도록 설정할 수 있습니다.

활성화된 주제 목록을 만드는 논리는 먼저 허용 목록에 있는 모든 주제를 허용한 다음 차단 목록에 있는 주제를 제거합니다. 기본적으로 모든 항목이 활성화되어 있고(허용 목록 값은 `*`), 비활성화된 항목이 없습니다(차단 목록에 값이 없음).

웹 콘솔 또는 `sling:OsgiConfig` 노드를 사용하여 다음 속성을 구성하십시오. `sling:OsgiConfig` 노드의 경우 작업 소비자 관리자 서비스의 PID는 org.apache.sling.event.impl.jobs.JobConsumerManager입니다.

| 웹 콘솔의 속성 이름 | OSGi ID | 설명 |
|---|---|---|
| 주제 허용 목록 | job.consumermanager.whitelist | 로컬 JobManager 서비스가 처리하는 항목 목록입니다. &ast;의 기본값은 모든 주제를 등록된 TopicConsumer 서비스로 보냅니다. |
| 주제 차단 목록 | job.consumermanager.blacklist | 로컬 JobManager 서비스가 처리하지 않는 항목 목록입니다. |

## 오프로드용 복제 에이전트 생성 {#creating-replication-agents-for-offloading}

오프로딩 프레임워크는 복제를 사용하여 작성자와 작업자 간에 리소스를 전송합니다. 인스턴스가 토폴로지에 참여할 때 오프로딩 프레임워크는 복제 에이전트를 자동으로 생성합니다. 에이전트는 기본값으로 생성됩니다. 에이전트가 인증에 사용하는 암호를 수동으로 변경합니다.

>[!CAUTION]
>
>자동으로 생성된 복제 에이전트에 대해 알려진 문제는 새 복제 에이전트를 수동으로 생성해야 합니다.

오프로드할 인스턴스 간에 작업 페이로드를 전송하는 복제 에이전트를 만듭니다. 다음 그림은 작성자에서 작업자 인스턴스로 오프로드하는 데 필요한 에이전트를 보여 줍니다. 작성자의 Sling ID는 1이고 작업자 인스턴스의 Sling ID는 2입니다.

![chlimage_1-115](assets/chlimage_1-115.png)

이 설정에는 다음 세 가지 에이전트가 필요합니다.

1. 작성자 인스턴스에서 작업자 인스턴스로 복제하는 송신 에이전트입니다.
1. 작업자 인스턴스의 보낼 편지함에서 가져오는 작성자 인스턴스의 역방향 에이전트입니다.
1. 작업자 인스턴스의 보낼 편지함 에이전트.

이 복제 체계는 작성자 및 게시 인스턴스 간에 사용되는 것과 유사합니다. 그러나 오프로딩 상황의 경우 관련된 모든 인스턴스는 인스턴스를 작성하는 것입니다.

>[!NOTE]
>
>오프로딩 프레임워크는 토폴로지를 사용하여 오프로딩 인스턴스의 IP 주소를 가져옵니다. 그런 다음 프레임워크는 이러한 IP 주소를 기반으로 복제 에이전트를 자동으로 생성합니다. 나중에 오프로딩 인스턴스의 IP 주소가 변경되면 인스턴스가 다시 시작된 후 토폴로지에 변경 내용이 자동으로 전파됩니다. 그러나 오프로딩 프레임워크는 새 IP 주소를 반영하도록 복제 에이전트를 자동으로 업데이트하지 않습니다. 이러한 상황을 방지하려면 토폴로지의 모든 인스턴스에 고정 IP 주소를 사용하십시오.

### 오프로드용 복제 에이전트 이름 지정 {#naming-the-replication-agents-for-offloading}

오프로딩 프레임워크에서 특정 작업자 인스턴스에 대해 올바른 에이전트를 자동으로 사용하도록 복제 에이전트의 ***이름*** 속성에 특정 형식을 사용하십시오.

**작성자 인스턴스에서 나가는 에이전트 이름 지정:**

`offloading_<slingid>`. 여기서 `<slingid>`은(는) 작업자 인스턴스의 Sling ID입니다.

예: `offloading_f5c8494a-4220-49b8-b079-360a72f71559`

**작성자 인스턴스에서 역방향 에이전트 이름 지정:**

`offloading_reverse_<slingid>`. 여기서 `<slingid>`은(는) 작업자 인스턴스의 Sling ID입니다.

예: `offloading_reverse_f5c8494a-4220-49b8-b079-360a72f71559`

**작업자 인스턴스에서 보낼 편지함 이름 지정:**

`offloading_outbox`

### 보내는 에이전트 만들기 {#creating-the-outgoing-agent}

1. 작성자에 대해 **복제 에이전트**&#x200B;을(를) 만듭니다. (복제 에이전트에 대한 [설명서](/help/sites-deploying/replication.md)를 참조하십시오.) **Title**&#x200B;을(를) 지정하십시오. **이름**&#x200B;은(는) 명명 규칙을 따라야 합니다.
1. 다음 속성을 사용하여 에이전트를 만듭니다.

   | 속성 | 값 |
   |---|---|
   | 설정 > 직렬화 유형 | 기본값 |
   | 전송 >전송 URI | https://*`<ip of target instance>`*:*`<port>`*`/bin/receive?sling:authRequestLogin=1` |
   | 전송 >전송 사용자 | 대상 인스턴스의 복제 사용자 |
   | 전송 >전송 암호 | 대상 인스턴스의 복제 사용자 암호 |
   | Extended > HTTP 메서드 | POST |
   | 트리거 > 기본값 무시 | 참 |

### 역방향 에이전트 만들기 {#creating-the-reverse-agent}

1. 작성자에 대해 **역방향 복제 에이전트**&#x200B;을(를) 만듭니다. (복제 에이전트에 대한 [설명서](/help/sites-deploying/replication.md)를 참조하세요.) **Title**&#x200B;을(를) 지정하십시오. **이름**&#x200B;은(는) 명명 규칙을 따라야 합니다.
1. 다음 속성을 사용하여 에이전트를 만듭니다.

   | 속성 | 값 |
   |---|---|
   | 설정 > 직렬화 유형 | 기본값 |
   | 전송 >전송 URI | https://*`<ip of target instance>`*:*`<port>`*`/bin/receive?sling:authRequestLogin=1` |
   | 전송 >전송 사용자 | 대상 인스턴스의 복제 사용자 |
   | 전송 >전송 암호 | 대상 인스턴스의 복제 사용자 암호 |
   | Extended > HTTP 메서드 | GET |

### 보낼 편지함 에이전트 만들기 {#creating-the-outbox-agent}

1. 작업자 인스턴스에 **복제 에이전트**&#x200B;을(를) 만듭니다. (복제 에이전트에 대한 [설명서](/help/sites-deploying/replication.md)를 참조하세요.) **Title**&#x200B;을(를) 지정하십시오. **이름**&#x200B;은(는) `offloading_outbox`이어야 합니다.
1. 다음 속성을 사용하여 에이전트를 만듭니다.

   | 속성 | 값 |
   |---|---|
   | 설정 > 직렬화 유형 | 기본값 |
   | 전송 >전송 URI | repo://var/replication/outbox |
   | 트리거 > 기본값 무시 | 참 |

### Sling ID 찾기 {#finding-the-sling-id}

다음 방법 중 하나를 사용하여 Experience Manager 인스턴스의 Sling ID를 얻습니다.

* 웹 콘솔을 열고 Sling 설정에서 Sling ID 속성의 값([http://localhost:4502/system/console/status-slingsettings](http://localhost:4502/system/console/status-slingsettings))을 찾습니다. 이 메서드는 인스턴스가 아직 토폴로지의 일부가 아닌 경우 유용합니다.
* 인스턴스가 이미 토폴로지의 일부인 경우 토폴로지 브라우저를 사용합니다.

<!--
## Offloading the Processing of DAM Assets {#offloading-the-processing-of-dam-assets}

Configure the instances of a topology so that specific instances perform the background processing of assets that are added or updated in DAM.

By default, Experience Manager executes the [!UICONTROL DAM Update Asset] workflow when a DAM asset changes or one is added to DAM. Change the default behavior so that Experience Manager instead executes the [!UICONTROL DAM Update Asset Offloader] workflow. This workflow generates a JobManager job that has a topic of `com/adobe/granite/workflow/offloading`. Then, configure the topology so that the job is offloaded to a dedicated worker.

>[!CAUTION]
>
>No workflow should be transient when used with workflow offloading. For example, the [!UICONTROL DAM Update Asset] workflow must not be transient when used for asset offloading. To set/unset the transient flag on a workflow, see [Transient Workflows](/help/assets/performance-tuning-guidelines.md#workflows).

The following procedure assumes the following characteristics for the offloading topology:

* One or more Experience Manager instance are authoring instances that users interact with for adding or updating DAM assets.
* Users to do not directly interact with one or more Experience Manager instances that process the DAM assets. These instances are dedicated to the background processing of DAM assets.

1. On each Experience Manager instance, configure the Discovery Service so that it points to the root Topography Connector. (See [Configuring Topology Membership](#title4).)
1. Configure the root Topography Connector so that the connecting instances are on the allow list.
1. Open Offloading Browser and disable the `com/adobe/granite/workflow/offloading` topic on the instances with which users interact to upload or change DAM assets.

   ![chlimage_1-116](assets/chlimage_1-116.png)

1. On each instance that users interact with to upload or change DAM assets, configure workflow launchers to use the [!UICONTROL DAM Update Asset Offloading] workflow:

    1. Open the Workflow console.
    1. Click the Launcher tab.
    1. Locate the two Launcher configurations that execute the [!UICONTROL DAM Update Asset] workflow. One launcher configuration event type is Node Created, and the other type is Node Modified.
    1. Change both event types so that they execute the [!UICONTROL DAM Update Asset Offloading] workflow. (For information about launcher configurations, see [Starting Workflows When Nodes Change](/help/sites-administering/workflows-starting.md).)

1. On the instances that perform the background processing of DAM assets, disable the workflow launchers that execute the [!UICONTROL DAM Update Asset] workflow.
-->

## 추가 참조 {#further-reading}

이 페이지에 제공된 세부 사항 외에 다음 사항도 읽을 수 있습니다.

* Java API를 사용하여 작업 및 작업 소비자를 만드는 방법에 대한 자세한 내용은 [오프로드용 작업 만들기 및 소비](/help/sites-developing/dev-offloading.md)를 참조하십시오.
