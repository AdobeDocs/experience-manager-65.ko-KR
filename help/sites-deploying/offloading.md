---
title: 작업 오프로딩
seo-title: 작업 오프로딩
description: 특정 유형의 처리를 수행하기 위해 토폴로지에서 AEM 인스턴스를 구성하고 사용하는 방법을 알아봅니다.
seo-description: 특정 유형의 처리를 수행하기 위해 토폴로지에서 AEM 인스턴스를 구성하고 사용하는 방법을 알아봅니다.
uuid: e971d403-dfd2-471f-b23d-a67e35f1ed88
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring
content-type: reference
discoiquuid: 370151df-3b8e-41aa-b586-5c21ecb55ffe
translation-type: tm+mt
source-git-commit: f24142064b15606a5706fe78bf56866f7f9a40ae

---


# 작업 오프로딩{#offloading-jobs}

## 소개 {#introduction}

오프로드는 토폴로지의 Experience Manager 인스턴스 중 처리 작업을 배포합니다. 오프로드를 사용하면 특정 유형의 처리를 수행하기 위해 특정 Experience Manager 인스턴스를 사용할 수 있습니다. 전문 처리를 통해 사용 가능한 서버 리소스의 사용을 최대화할 수 있습니다.

오프로드는 Apache Sling Discovery [및 Sling JobManager](https://sling.apache.org/documentation/bundles/discovery-api-and-impl.html) 기능을 기반으로 합니다. 오프로딩을 사용하려면 Experience Manager 클러스터를 토폴로지에 추가하고 클러스터가 처리하는 작업 항목을 식별합니다. 클러스터는 하나 이상의 Experience Manager 인스턴스로 구성되므로 단일 인스턴스가 클러스터로 간주됩니다.

토폴로지에 인스턴스 추가에 대한 자세한 내용은 토폴로지 [관리를 참조하십시오](/help/sites-deploying/offloading.md#administering-topologies).

### 작업 배포 {#job-distribution}

Sling JobManager 및 JobConsumer를 사용하면 토폴로지에서 처리되는 작업을 만들 수 있습니다.

* JobManager:특정 주제에 대한 작업을 만드는 서비스입니다.
* JobConsumer:하나 이상의 주제 작업을 실행하는 서비스입니다. 동일한 항목에 대해 여러 JobConsumer 서비스를 등록할 수 있습니다.

JobManager가 작업을 만들면 Offloading 프레임워크는 토폴로지에서 Experience Manager 클러스터를 선택하여 작업을 실행합니다.

* 클러스터에는 작업 항목에 대해 등록된 JobConsumer를 실행 중인 하나 이상의 인스턴스가 포함되어야 합니다.
* 클러스터의 인스턴스 중 적어도 하나에 대해 주제가 활성화되어 있어야 합니다.

작업 [분포를](/help/sites-deploying/offloading.md#configuring-topic-consumption) 조정하는 방법에 대한 자세한 내용은 주제 소비 구성을 참조하십시오.

![chlimage_1-109](assets/chlimage_1-109.png)

Offloading 프레임워크에서 작업을 실행할 클러스터를 선택하고 클러스터는 여러 인스턴스로 구성되어 있을 때 Sling Distribution에서 작업을 실행하는 클러스터의 인스턴스를 결정합니다.

### 작업 페이로드 {#job-payloads}

Offloading 프레임워크는 작업을 저장소의 리소스와 연결하는 작업 페이로드를 지원합니다. 작업 페이로드는 처리 리소스를 위해 작업을 만들고 작업을 다른 컴퓨터로 오버로드한 경우에 유용합니다.

작업을 만들면 페이로드가 작업을 만드는 인스턴스에만 위치할 수 있습니다. 작업을 오프로드할 때 복제 에이전트는 작업을 결국 사용하는 인스턴스에서 페이로드를 생성하는지 확인합니다. 작업 실행이 완료되면 역복제로 인해 페이로드가 작업을 만든 인스턴스로 다시 복사됩니다.

## 토폴로지 관리 {#administering-topologies}

토폴로지는 오프로드에 참여하는 느슨하게 연결된 Experience Manager 클러스터입니다. 클러스터는 하나 이상의 Experience Manager 서버 인스턴스로 구성됩니다(단일 인스턴스는 클러스터로 간주됨).

각 Experience Manager 인스턴스는 다음과 같은 오프로딩 관련 서비스를 실행합니다.

* 검색 서비스:토폴로지 커넥터로 요청을 전송하여 토폴로지에 가입합니다.
* 토폴로지 커넥터:참여 요청을 받고 각 요청을 수락하거나 거부합니다.

토폴로지 멤버의 모든 검색 서비스가 멤버 중 하나에서 토폴로지 커넥터를 가리킵니다. 다음 섹션에서 이 멤버를 루트 멤버라고 합니다.

![chlimage_1-110](assets/chlimage_1-110.png)

토폴로지의 각 클러스터에는 선두로 인식되는 인스턴스가 포함되어 있습니다. 클러스터 리더는 클러스터의 다른 구성원을 대신하여 토폴로지와 상호 작용합니다. 지시선이 클러스터를 떠나면 클러스터의 새 지시선이 자동으로 선택됩니다.

### 토폴로지 보기 {#viewing-the-topology}

토폴로지 브라우저를 사용하여 Experience Manager 인스턴스가 참여하는 토폴로지의 상태를 탐색합니다. 토폴로지 브라우저는 토폴로지의 클러스터 및 인스턴스를 표시합니다.

각 클러스터에 대해 각 구성원이 참여한 순서와 리더인 구성원을 나타내는 클러스터 멤버 목록이 표시됩니다. Current 속성은 현재 관리 중인 인스턴스를 나타냅니다.

클러스터의 각 인스턴스에 대해 몇 가지 토폴로지 관련 속성을 볼 수 있습니다.

* 인스턴스의 작업 소비자에 대한 주제 화이트 리스트.
* 토폴로지와 연결하기 위해 표시되는 끝점입니다.
* 인스턴스가 오프로드용으로 등록된 작업 주제입니다.
* 인스턴스가 처리하는 작업 주제입니다.

1. Touch UI를 사용하여 도구 탭을 클릭합니다. ([http://localhost:4502/tools.html](http://localhost:4502/tools.html))
1. [Granite Operations] 영역에서 [Offloading Browser]를 클릭합니다.
1. 탐색 패널에서 토폴로지 브라우저를 클릭합니다.

   토폴로지에 참여하는 클러스터가 나타납니다.

   ![chlimage_1-111](assets/chlimage_1-111.png)

1. 클러스터의 인스턴스 목록과 해당 ID, 현재 상태 및 리더 상태를 보려면 클러스터를 클릭합니다.
1. 자세한 속성을 보려면 인스턴스 ID를 클릭합니다.

웹 콘솔을 사용하여 토폴로지 정보를 볼 수도 있습니다. 콘솔은 토폴로지 클러스터에 대한 추가 정보를 제공합니다.

* 어느 인스턴스가 로컬 인스턴스입니다.
* 이 인스턴스가 토폴로지(발신)에 연결하는 데 사용하는 토폴로지 커넥터 서비스와 이 인스턴스에 연결하는 서비스(수신)입니다.
* 토폴로지 및 인스턴스 속성의 내역을 변경합니다.

다음 절차를 사용하여 웹 콘솔의 토폴로지 관리 페이지를 엽니다.

1. 브라우저에서 웹 콘솔을 엽니다. ([http://localhost:4502/system/console](http://localhost:4502/system/console))
1. 기본 > 토폴로지 관리를 클릭합니다.

   ![chlimage_1-112](assets/chlimage_1-112.png)

### 토폴로지 멤버십 구성 {#configuring-topology-membership}

Apache Sling 리소스 기반 검색 서비스는 각 인스턴스에서 실행되어 Experience Manager 인스턴스가 토폴로지와 상호 작용하는 방식을 제어합니다.

검색 서비스는 주기적으로 POST 요청(하트비트)을 토폴로지 커넥터 서비스로 전송하여 토폴로지와 연결을 설정하고 유지합니다. 토폴로지 커넥터 서비스는 토폴로지에 참여할 수 있는 IP 주소 또는 호스트 이름의 허용 목록을 유지합니다.

* 인스턴스를 토폴로지에 연결하려면 루트 멤버의 토폴로지 커넥터 서비스의 URL을 지정합니다.
* 인스턴스가 토폴로지에 가입하도록 하려면 루트 멤버의 토폴로지 커넥터 서비스의 허용 목록에 인스턴스를 추가합니다.

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
   <td>하트비트 시간 제한(초)</td>
   <td>heartbeatTimeout</td>
   <td>타깃팅된 인스턴스를 사용할 수 없는 것으로 간주되기 전에 하트비트 응답을 기다리는 시간(초)입니다. </td>
   <td>20</td>
  </tr>
  <tr>
   <td>하트비트 간격(초)</td>
   <td>heartbeatInterval</td>
   <td>하트비트 사이의 시간(초)입니다.</td>
   <td>15</td>
  </tr>
  <tr>
   <td>최소 이벤트 지연(초)</td>
   <td>minEventDelay</td>
   <td><p>토폴로지가 변경될 때 상태 변경을 TOPOLOGY_CHANGING에서 TOPOLOGY_CHANGING으로 연기하기 위한 시간입니다. 상태가 TOPOLOGY_CHANGING일 때 발생하는 각 변경 사항은 이 시간만큼 지연을 증가시킵니다.</p> <p>이러한 지연으로 인해 수신자에게 이벤트가 쇄도하지 않습니다. </p> <p>지연 없이 사용하려면 0 또는 음수를 지정합니다.</p> </td>
   <td>3</td>
  </tr>
  <tr>
   <td>토폴로지 커넥터 URL</td>
   <td>토폴로지 커넥터 URL</td>
   <td>하트비트 메시지를 보낼 토폴로지 커넥터 서비스의 URL.</td>
   <td>http://localhost:4502/libs/sling/topology/connector</td>
  </tr>
  <tr>
   <td>토폴로지 커넥터 화이트 리스트</td>
   <td>토폴로지 커넥터 화이트 리스트</td>
   <td>로컬 토폴로지 커넥터 서비스가 토폴로지에서 허용하는 IP 주소 또는 호스트 이름 목록입니다. </td>
   <td><p>localhost</p> <p>127.0.0.1</p> </td>
  </tr>
  <tr>
   <td>저장소 설명자 이름</td>
   <td>leaderElectionRepositoryDescriptor</td>
   <td> </td>
   <td>&lt;값 없음&gt;</td>
  </tr>
 </tbody>
</table>

다음 절차를 사용하여 CQ 인스턴스를 토폴로지의 루트 멤버에 연결합니다. 이 절차에서는 인스턴스를 루트 토폴로지 멤버의 토폴로지 커넥터 URL로 가리킵니다. 토폴로지의 모든 구성원에 대해 이 절차를 수행합니다.

1. 브라우저에서 웹 콘솔을 엽니다. ([http://localhost:4502/system/console](http://localhost:4502/system/console))
1. 기본 > 토폴로지 관리를 클릭합니다.
1. 검색 서비스 구성을 클릭합니다.
1. 토폴로지 커넥터 URL 속성에 항목을 추가하고 루트 토폴로지 멤버의 토폴로지 커넥터 서비스의 URL을 지정합니다. URL은 https://rootservername:4502/libs/sling/topology/connector 형식입니다.

토폴로지의 루트 멤버에 대해 다음 절차를 수행합니다. 이 절차에서는 다른 토폴로지 멤버의 이름을 검색 서비스 허용 목록에 추가합니다.

1. 브라우저에서 웹 콘솔을 엽니다. ([http://localhost:4502/system/console](http://localhost:4502/system/console))
1. 기본 > 토폴로지 관리를 클릭합니다.
1. 검색 서비스 구성을 클릭합니다.
1. 토폴로지의 각 멤버에 대해 토폴로지 커넥터 화이트 리스트 속성에 항목을 추가하고 토폴로지 멤버의 호스트 이름 또는 IP 주소를 지정합니다.

## 주제 소비 구성 {#configuring-topic-consumption}

Offloading Browser를 사용하여 토폴로지의 Experience Manager 인스턴스에 대한 항목 사용을 구성합니다. 각 인스턴스에 대해 필요한 항목을 지정할 수 있습니다. 예를 들어 하나의 인스턴스만 특정 유형의 주제를 사용하도록 토폴로지를 구성하려면 하나를 제외한 모든 인스턴스에서 토픽을 비활성화합니다.

작업은 라운드 로빈 로직을 사용하여 연관된 항목이 활성화된 인스턴스 간에 배포됩니다.

1. Touch UI를 사용하여 도구 탭을 클릭합니다. ([http://localhost:4502/tools.html](http://localhost:4502/tools.html))
1. [Granite Operations] 영역에서 [Offloading Browser]를 클릭합니다.
1. 탐색 패널에서 [브라우저 오프로딩]을 클릭합니다.

   항목을 사용할 수 있는 오프로딩 항목 및 서버 인스턴스가 나타납니다.

   ![chlimage_1-113](assets/chlimage_1-113.png)

1. 인스턴스에 대한 토픽의 소비를 비활성화하려면 해당 인스턴스 옆에 있는 토픽 이름 아래에 있는 비활성화를 클릭합니다.
1. 인스턴스에 대한 모든 토픽 소비를 구성하려면 항목 아래의 인스턴스 식별자를 클릭하십시오.

   ![chlimage_1-114](assets/chlimage_1-114.png)

1. 항목 옆에 있는 다음 단추 중 하나를 클릭하여 인스턴스에 대한 소비 동작을 구성한 다음 저장을 클릭합니다.

   * 활성화:이 인스턴스는 이 항목의 작업을 사용합니다.
   * 사용 안 함:이 인스턴스는 이 항목의 작업을 소비하지 않습니다.
   * 전용:이 인스턴스는 이 항목의 작업만 사용합니다.
   **참고:** 주제에 대해 [배타적]을 선택하면 다른 모든 항목이 자동으로 [비활성화]로 설정됩니다.

### 설치된 Job Consumers {#installed-job-consumers}

Adobe Experience Manager와 함께 여러 JobConsumer 구현이 설치됩니다. 이러한 JobConsumers가 등록된 항목은 Offloading Browser에 표시됩니다. 표시되는 추가 항목은 사용자 지정 JobConsumers가 등록한 항목입니다. 다음 표에서는 기본 JobConsumer에 대해 설명합니다.

| 작업 주제 | 서비스 PID | 설명 |
|---|---|---|
| / | org.apache.sling.event.impl.jobs.deprecated.EventAdminBridge | Apache Sling과 함께 설치되었습니다. 이전 버전과의 호환성을 위해 OSGi 이벤트 관리자가 생성하는 작업을 처리합니다. |
| com/day/cq/replication/job/&amp;ast; | com.day.cq.replication.impl.AgentManagerImpl | 작업 페이로드를 복제하는 복제 에이전트입니다. |
| com/adobe/granite/workflow/offloading | com.adobe.granite.workflow.core.offloading.WorkflowOffloadingJobConsumer | DAM 자산 [!UICONTROL 업데이트 오프로더 워크플로우가 생성하는 작업을] 처리합니다. |

### 인스턴스에 대한 항목 비활성화 및 활성화 {#disabling-and-enabling-topics-for-an-instance}

Apache Sling Job Consumer Manager 서비스는 주제 화이트 리스트 및 블랙 리스트 속성을 제공합니다. Experience Manager 인스턴스에서 특정 항목의 처리를 활성화하거나 비활성화하도록 이러한 속성을 구성합니다.

**참고:** 인스턴스가 토폴로지에 속한 경우 토폴로지의 모든 컴퓨터에서 브라우저 오프로드 기능을 사용하여 항목을 활성화하거나 비활성화할 수도 있습니다.

활성화된 항목 목록을 만드는 논리는 우선 화이트리스트에 있는 모든 항목을 허용한 다음 블랙리스트에 있는 항목을 제거합니다. 기본적으로 모든 항목이 활성화되어 있고(허용 목록 값이 `*`사용) 항목이 비활성화되어 있지 않습니다(블랙 리스트에는 값이 없음).

웹 콘솔 또는 `sling:OsgiConfig` 노드를 사용하여 다음 속성을 구성합니다. 노드의 경우 작업 소비자 관리자 서비스의 PID는 org.apache.sling.event.impl.jobs.JobConsumerManager입니다. `sling:OsgiConfig`

| 웹 콘솔의 속성 이름 | OSGi ID | 설명 |
|---|---|---|
| 주제 화이트 리스트 | job.consumermanager.whitelist | 로컬 JobManager 서비스가 처리하는 항목 목록입니다. &amp;ast;의 기본값모든 항목을 등록된 TopicConsumer 서비스로 보냅니다. |
| 주제 블랙 리스트 | job.consumermanager.blacklist | 로컬 JobManager 서비스가 처리하지 않는 항목 목록입니다. |

## 오프로드용 복제 에이전트 만들기 {#creating-replication-agents-for-offloading}

오프로딩 프레임워크는 복제를 사용하여 작성자와 작업자 간에 리소스를 전송합니다. 오프로딩 프레임워크는 인스턴스가 토폴로지에 가입하면 복제 에이전트를 자동으로 생성합니다. 에이전트는 기본값으로 생성됩니다. 에이전트가 인증에 사용하는 암호를 수동으로 변경해야 합니다.

>[!CAUTION]
>
>자동으로 생성된 복제 에이전트의 알려진 문제를 해결하려면 새 복제 에이전트를 수동으로 생성해야 합니다. 오프로드용 에이전트를 [만들기 전에 자동으로 생성된 복제 에이전트를](/help/sites-deploying/offloading.md#problems-using-the-automatically-generated-replication-agents) 사용하는 문제 의 절차를 따르십시오.

오프로드용 인스턴스 간에 작업 페이로드를 전송하는 복제 에이전트를 만듭니다. 다음 그림은 작성자에서 작업자 인스턴스로 오프로드하는 데 필요한 에이전트를 보여줍니다. 작성자는 Sling ID가 1이고 작업자 인스턴스는 Sling ID가 2입니다.

![chlimage_1-115](assets/chlimage_1-115.png)

이 설정을 사용하려면 다음 세 가지 에이전트가 필요합니다.

1. 작업자 인스턴스에 복제하는 작성자 인스턴스의 나가는 에이전트입니다.
1. 작업자 인스턴스의 보관함에서 가져오는 작성자 인스턴스의 역방향 에이전트입니다.
1. 작업자 인스턴스의 아웃박스 에이전트입니다.

이 복제 구성표는 작성자 및 게시 인스턴스 사이에 사용되는 구성표와 유사합니다. 그러나 오프로딩 상황의 경우 관련된 모든 인스턴스가 작성 인스턴스입니다.

>[!NOTE]
>
>Offloading 프레임워크는 토폴로지를 사용하여 오프로딩 인스턴스의 IP 주소를 가져옵니다. 그러면 프레임워크는 이러한 IP 주소를 기반으로 복제 에이전트를 자동으로 만듭니다. 나중에 오프로딩 인스턴스의 IP 주소가 변경되면 인스턴스가 다시 시작된 후 변경 내용이 토폴로지에 자동으로 표시됩니다. 그러나 오프로딩 프레임워크는 새 IP 주소를 반영하도록 복제 에이전트를 자동으로 업데이트하지 않습니다. 이러한 상황을 방지하려면 토폴로지의 모든 인스턴스에 대해 고정 IP 주소를 사용하십시오.

### 오프로드용 복제 에이전트 이름 지정 {#naming-the-replication-agents-for-offloading}

오프로딩 프레임워크에서 특정 작업자 ***인스턴스에 대해*** 올바른 에이전트를 자동으로 사용할 수 있도록 복제 에이전트의 이름 속성에 대한 특정 형식을 사용합니다.

**작성자 인스턴스에서 나가는 에이전트 이름 지정:**

`offloading_<slingid>`, where `<slingid>` is the Sling ID of the worker instance.

예: `offloading_f5c8494a-4220-49b8-b079-360a72f71559`

**작성자 인스턴스에서 역 에이전트 이름 지정:**

`offloading_reverse_<slingid>`, where `<slingid>` is the Sling ID of the worker instance.

예: `offloading_reverse_f5c8494a-4220-49b8-b079-360a72f71559`

**작업자 인스턴스에서 보낼 편지함의 이름 지정:**

`offloading_outbox`

### 나가는 에이전트 만들기 {#creating-the-outgoing-agent}

1. 작성자에 **복제 에이전트를** 만듭니다. (복제 에이전트 [문서](/help/sites-deploying/replication.md)참조). 제목을 **지정합니다**. 이름은 **이름** 지정 규칙을 따라야 합니다.
1. 다음 속성을 사용하여 에이전트를 만듭니다.

   | 속성 | 값 |
   |---|---|
   | 설정 > 직렬화 유형 | 기본값 |
   | 전송 > 전송 URI | https://*`<ip of target instance>`*:*`<port>`*`/bin/receive?sling:authRequestLogin=1` |
   | 전송 > 전송 사용자 | 타겟 인스턴스의 복제 사용자 |
   | 전송 > 전송 암호 | 대상 인스턴스의 복제 사용자 암호 |
   | Extended > HTTP 메서드 | POST |
   | 트리거 > 기본값 무시 | True |

### 역방향 에이전트 만들기 {#creating-the-reverse-agent}

1. 작성자에 **역방향 복제 에이전트를** 만듭니다. (복제 에이전트에 [대한 설명서를 참조하십시오](/help/sites-deploying/replication.md).) 제목을 **지정합니다**. 이름은 **이름** 지정 규칙을 따라야 합니다.
1. 다음 속성을 사용하여 에이전트를 만듭니다.

   | 속성 | 값 |
   |---|---|
   | 설정 > 직렬화 유형 | 기본값 |
   | 전송 > 전송 URI | https://*`<ip of target instance>`*:*`<port>`*`/bin/receive?sling:authRequestLogin=1` |
   | 전송 > 전송 사용자 | 타겟 인스턴스의 복제 사용자 |
   | 전송 > 전송 암호 | 대상 인스턴스의 복제 사용자 암호 |
   | Extended > HTTP 메서드 | GET |

### 보낼 편지함 에이전트 만들기 {#creating-the-outbox-agent}

1. 작업자 **인스턴스에** 복제 에이전트를 만듭니다. (복제 에이전트에 [대한 설명서를 참조하십시오](/help/sites-deploying/replication.md).) 제목을 **지정합니다**. 이름은 **반드시** 되어야 합니다 `offloading_outbox`.
1. 다음 속성을 사용하여 에이전트를 만듭니다.

   | 속성 | 값 |
   |---|---|
   | 설정 > 직렬화 유형 | 기본값 |
   | 전송 > 전송 URI | repo://var/replication/outbox |
   | 트리거 > 기본값 무시 | True |

### Sling ID 찾기 {#finding-the-sling-id}

다음 방법 중 하나를 사용하여 Experience Manager 인스턴스의 Sling ID를 얻습니다.

* 웹 콘솔을 열고 [Sling 설정]에서 Sling ID 속성(http://localhost:4502/system/console/status-slingsettings)의 값을[찾습니다](http://localhost:4502/system/console/status-slingsettings). 인스턴스가 아직 토폴로지의 일부가 아닌 경우 이 메서드를 사용할 수 있습니다.
* 인스턴스가 이미 토폴로지의 일부인 경우 토폴로지 브라우저를 사용합니다.

## DAM 자산 처리 취소 {#offloading-the-processing-of-dam-assets}

특정 인스턴스가 DAM에서 추가 또는 업데이트된 자산의 백그라운드 처리를 수행하도록 토폴로지 인스턴스를 구성합니다.

기본적으로 Adobe Experience Manager는 DAM [!UICONTROL 자산이 변경되거나] DAM에 자산이 추가되면 DAM 자산 업데이트 워크플로우를 실행합니다. Experience Manager가 대신 DAM 자산 [!UICONTROL 오프로더 업데이트 워크플로우를 실행하도록 기본 동작을] 변경합니다. 이 워크플로우는 주제가 있는 JobManager 작업을 생성합니다 `com/adobe/granite/workflow/offloading`. 그런 다음 전용 작업자에게 작업이 오프로드되도록 토폴로지를 구성합니다.

>[!CAUTION]
>
>워크플로우 오프로딩과 함께 사용하면 워크플로우가 일시적으로 중단되어서는 안 됩니다. 예를 들어 자산 [!UICONTROL 오프로딩에 DAM 자산] 업데이트 워크플로우가 일시적으로 사용되어서는 안 됩니다. 워크플로우에서 임시 플래그를 설정/해제하려면 임시 [워크플로우를 참조하십시오](/help/assets/performance-tuning-guidelines.md#workflows).

다음 절차에서는 오프로딩 토폴로지에 대해 다음 특성을 가정합니다.

* 하나 이상의 Adobe Experience Manager 인스턴스가 사용자가 DAM 자산을 추가하거나 업데이트하기 위해 상호 작용하는 작성 인스턴스입니다.
* 사용자는 DAM 자산을 처리하는 하나 이상의 Experience Manager 인스턴스와 직접 상호 작용하지 않습니다. 이러한 인스턴스는 DAM 자산의 백그라운드 처리에 사용됩니다.

1. 각 Experience Manager 인스턴스에서 루트 지형 커넥터를 가리키도록 검색 서비스를 구성합니다. 토폴로지 [구성원 구성을 참조하십시오](#title4).
1. 연결된 인스턴스가 화이트리스트에 있도록 루트 지형 커넥터를 구성합니다.
1. 오프로딩 브라우저를 열고 사용자가 DAM 자산을 업로드하거나 변경하기 위해 상호 작용하는 인스턴스에 대한 `com/adobe/granite/workflow/offloading` 항목을 비활성화합니다.

   ![chlimage_1-116](assets/chlimage_1-116.png)

1. 사용자가 DAM 자산을 업로드하거나 변경하기 위해 상호 작용하는 각 인스턴스에서 DAM 자산 [!UICONTROL 오프로딩 워크플로우를 사용하도록 워크플로우 런처를 구성합니다] .

   1. 워크플로우 콘솔을 엽니다.
   1. 실행 프로그램 탭을 클릭합니다.
   1. DAM 자산 업데이트 [!UICONTROL 워크플로우를 실행하는 두 개의 실행] 시작 구성을 찾습니다. 실행 관리자 구성 이벤트 유형 중 하나는 Node Created이고 다른 유형은 Node Modified입니다.
   1. 두 이벤트 유형을 모두 변경하여 DAM 자산 [!UICONTROL 오프로딩 워크플로우를 실행합니다] . 실행 프로그램 구성에 대한 자세한 내용은 노드 변경 [시 워크플로우 시작을 참조하십시오](/help/sites-administering/workflows-starting.md).

1. DAM 자산의 백그라운드 처리를 수행하는 인스턴스에서 DAM 자산 업데이트 [!UICONTROL 워크플로우를 실행하는 워크플로우 런처를] 비활성화합니다.

## 추가 읽기 {#further-reading}

이 페이지에 표시된 세부 사항 외에 다음을 읽을 수도 있습니다.

* Java API를 사용하여 작업 및 작업 소비자를 만드는 방법에 대한 자세한 내용은 오프로드를 [위한 작업 만들기 및 사용을 참조하십시오](/help/sites-developing/dev-offloading.md).
