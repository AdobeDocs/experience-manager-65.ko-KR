---
title: 복제 문제 해결
description: 이 문서에서는 복제 문제를 해결하는 방법에 대해 설명합니다.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: configuring
docset: aem65
feature: Configuring
exl-id: cfa822c8-f9a9-4122-9eac-0293d525f6b5
solution: Experience Manager, Experience Manager Sites
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '1224'
ht-degree: 0%

---

# 복제 문제 해결{#troubleshooting-replication}

이 페이지에서는 복제 문제를 해결하는 방법에 대해 설명합니다.

## 문제 {#problem}

어떤 이유로 복제(비역방향 복제)가 실패했습니다.

## 해결 방법 {#resolution}

복제가 실패하는 이유는 다양합니다. 이 문서에서는 이러한 문제를 분석할 때 취할 수 있는 접근 방식에 대해 설명합니다.

**활성화 단추를 클릭할 때 복제가 전혀 트리거되지 않습니까? 그렇지 않으면 다음을 수행하십시오.**

1. /crx/explorer로 이동한 다음 관리자로 로그인합니다.
1. &quot;Content Explorer&quot; 열기
1. /bin/replicate 또는 /bin/replicate.json 노드가 있는지 확인합니다. 노드가 있으면 삭제하고 저장합니다.

**복제가 복제 에이전트 큐에서 큐에 올라가고 있습니까?**

/etc/replication/agents.author.html로 이동한 다음 확인할 복제 에이전트를 클릭합니다.

**에이전트 큐 하나 또는 에이전트 큐 몇 개가 중단된 경우:**

1. 큐에 **차단됨** 상태가 표시됩니까? 그렇다면 게시 인스턴스가 실행되고 있지 않거나 응답하지 않습니까? 게시 인스턴스를 확인하여 무엇이 잘못되었는지 확인하십시오. 즉, 로그를 확인하여 OutOfMemory 오류 또는 기타 문제가 있는지 확인합니다. 속도가 느리면 스레드 덤프를 가져와 분석합니다.
1. 큐 상태가 **큐가 활성 상태입니까? # 보류 중**? 기본적으로 복제 작업이 게시 인스턴스 또는 Dispatcher의 응답을 기다리는 소켓 읽기에서 중단될 수 있습니다. 이는 게시 인스턴스 또는 Dispatcher이 높은 로드 중이거나 잠금에 있음을 의미할 수 있습니다. 작성자로부터 스레드 덤프를 가져와 이 경우 게시합니다.

   * 스레드 덤프 분석기에서 작성자의 스레드 덤프를 열고 복제 에이전트의 슬링 이벤트 작업이 socketRead에서 멈췄는지 확인합니다.
   * 스레드 덤프 분석기의 게시에서 스레드 덤프를 열고 게시 인스턴스가 응답하지 않는 원인이 무엇인지 분석합니다. 해당 이름에 작성자로부터 복제를 받는 스레드인 /bin/receive POST이 있는 스레드가 표시되어야 합니다.

**모든 에이전트 큐가 중단된 경우**

1. 저장소 손상 또는 기타 문제로 인해 특정 콘텐츠를 /var/replication/data로 serialize할 수 없습니다. logs/error.log에서 관련 오류를 확인합니다. 잘못된 복제 항목을 지우려면 다음을 수행합니다.

   1. https://&lt;host>:&lt;port>/crx/de로 이동하여 관리자로 로그인합니다.
   1. 상단 메뉴에서 &quot;도구&quot;를 클릭합니다.
   1. 돋보기 단추를 클릭합니다.
   1. 유형으로 &quot;XPath&quot;를 선택합니다.
   1. &quot;쿼리&quot; 상자에 이 쿼리 /jcr:root/var/eventing/jobs//element(&#42;,slingevent:Job) 순서를 @slingevent:created로 입력합니다
   1. &quot;검색&quot;을 클릭합니다.
   1. 결과에서 상위 항목은 최신 슬링 이벤트 작업입니다. 각 복제본을 클릭하고 대기열 맨 위에 표시되는 복제본과 일치하는 중단된 복제본을 찾습니다.

1. Sling 이벤트 프레임워크 작업 큐에 문제가 있을 수 있습니다. /system/console에서 org.apache.sling.event 번들을 다시 시작하십시오.
1. 작업 처리가 꺼져 있을 수 있습니다. Sling 이벤트 탭의 Felix 콘솔에서 확인할 수 있습니다. 표시 여부 확인 - Apache Sling 이벤트(작업 처리가 비활성화됨!)

   * 그렇다면 Felix 콘솔의 구성 탭에서 Apache Sling 작업 이벤트 핸들러 를 확인하십시오. &#39;작업 처리 사용&#39; 확인란이 선택 취소되었을 수 있습니다. 이 옵션이 선택되어 있고 여전히 &#39;작업 처리가 비활성화되어 있음&#39;이 표시되면, 작업 처리를 비활성화하는 /apps/system/config 아래에 오버레이가 있는지 확인합니다. 부울 값을 true로 설정하여 jobmanager.enabled에 대한 osgi:config 노드를 생성하고 활성화가 시작되었으며 큐에 작업이 더 이상 없는지 다시 확인해 보십시오.

1. 또한 DefaultJobManager 구성이 일관성 없는 상태가 될 수 있습니다. 이 문제는 누군가가 OSGiconsole을 통해 &#39;Apache Sling 작업 이벤트 핸들러&#39; 구성을 수동으로 수정할 때(예: &#39;작업 처리 활성화됨&#39; 속성을 비활성화했다가 다시 활성화하고 구성을 저장) 발생할 수 있습니다.

   * 이 시점에서 crx-quickstart/launchpad/config/org/apache/sling/event/impl/jobs/DefaultJobManager.config에 저장된 DefaultJobManager 구성이 일관되지 않은 상태가 됩니다. 그리고 &#39;Apache Sling Job Event Handler&#39; 속성에 &#39;Job Processing Enabled&#39;가 확인 상태로 표시되지만, Sling Eventing 탭으로 이동하면 JOB PROCESSING IS DISABLED이고 복제가 작동하지 않는다는 메시지가 표시됩니다.
   * 이 문제를 해결하려면 OSGi 콘솔의 구성 페이지로 이동하여 &#39;Apache Sling 작업 이벤트 핸들러&#39; 구성을 삭제합니다. 그런 다음 클러스터의 기본 노드를 재시작하여 구성을 일관된 상태로 다시 전환합니다. 이렇게 하면 문제가 해결되고 복제가 다시 시작됩니다.

**replication.log 만들기**

경우에 따라 모든 복제 로깅을 디버그 수준의 별도 로그 파일에 추가하도록 설정하는 것이 유용합니다. 이를 위해 진행되는 작업:

1. https://host:port/system/console/configMgr으로 이동한 다음 관리자로 로그인합니다.
1. Apache Sling Logging Logger 팩터리를 찾고 팩터리 구성 오른쪽의 **+** 단추를 클릭하여 인스턴스를 만듭니다. 이렇게 하면 새 로깅 로거가 만들어집니다.
1. 다음과 같이 구성을 설정합니다.

   * 로그 수준: 디버그
   * 로그 파일 경로: logs/replication.log
   * 카테고리: com.day.cq.replication

1. 어떤 식으로든 이 문제가 슬링 이벤트/작업과 관련이 있다고 의심되는 경우 이 Java™ 패키지를 다음 범주에 추가할 수도 있습니다.org.apache.sling.event

## 복제 에이전트 큐 일시 중지  {#pausing-replication-agent-queue}

복제 큐를 일시 중지하여 작성자 시스템의 로드를 줄이는 것이 적합할 수 있습니다. 현재는 일시적으로 유효하지 않은 포트를 구성하는 해킹을 통해서만 가능하다. 5.4 이상에서는 복제 에이전트 대기열에 일시 중지 버튼이 표시되며 몇 가지 제한이 있습니다

1. 상태가 지속되지 않습니다. 즉, 서버를 다시 시작하거나 복제 번들이 재활용되면 실행 상태로 돌아갑니다.
1. 일시 중지는 짧은 기간(다른 스레드에서 복제한 활동이 없는 후 OOB 1시간) 동안 유휴 상태이며 더 긴 시간 동안 유휴 상태가 아닙니다. sling에는 유휴 스레드를 방지하는 기능이 있으므로 기본적으로 작업 큐 스레드가 더 오랫동안 사용되지 않았는지 확인하며, 사용되지 않은 경우 정리 주기를 시작합니다. 정리 사이클로 인해 스레드가 중지되므로 일시 중지된 설정이 손실됩니다. 작업은 유지되므로 새 스레드를 시작하여 일시 중지된 구성에 대한 세부 정보가 없는 대기열을 처리합니다. 이 대기열로 인해 실행 상태가 됩니다.

## 사용자 활성화 시 페이지 권한이 복제되지 않음 {#page-permissions-are-not-replicated-on-user-activation}

페이지 권한은 사용자가 아닌 액세스가 허용되는 노드 아래에 저장되므로 복제되지 않습니다.

일반적으로 페이지 권한은 작성자에서 게시로 복제되지 않아야 하며 기본적으로 복제되지 않습니다. 이러한 두 환경에서는 액세스 권한이 달라야 하기 때문입니다. 따라서 Adobe은 작성자와 별도로 게시 시 ACL을 구성할 것을 권장합니다.

## 작성자에서 Publish으로 네임스페이스 정보를 복제할 때 복제 큐가 차단됨 {#replication-queue-blocked-when-replicating-namespace-information-from-author-to-publish}

작성자 인스턴스에서 게시 인스턴스로 네임스페이스 정보를 복제하려고 할 때 복제 큐가 차단되는 경우가 있습니다. 이 문제는 복제 사용자에게 `jcr:namespaceManagement` 권한이 없기 때문에 발생합니다. 이 문제를 방지하려면 다음을 확인하십시오.

* [전송](/help/sites-deploying/replication.md#replication-agents-configuration-parameters) 탭>사용자 아래에 구성된 복제 사용자도 Publish 인스턴스에 있습니다.
* 사용자는 콘텐츠가 설치된 경로에서 읽기 및 쓰기 권한을 갖습니다.
* 사용자가 저장소 수준에서 `jcr:namespaceManagement` 권한을 가지고 있습니다. 다음과 같은 권한을 부여할 수 있습니다.

1. 관리자로 CRX/DE(`https://localhost:4502/crx/de/index.jsp`)에 로그인합니다.
1. **액세스 제어** 탭을 클릭합니다.
1. **저장소**&#x200B;를 선택하십시오.
1. **항목 추가**(더하기 아이콘)를 클릭합니다.
1. 사용자의 이름을 입력합니다.
1. 권한 목록에서 `jcr:namespaceManagement`을(를) 선택합니다.
1. **확인**&#x200B;을 클릭합니다.
