---
title: 복제 문제 해결
seo-title: 복제 문제 해결
description: 이 문서에서는 복제 문제를 해결하는 방법에 대한 정보를 제공합니다.
seo-description: 이 문서에서는 복제 문제를 해결하는 방법에 대한 정보를 제공합니다.
uuid: 1662bf60-b000-4eb2-8834-c6da607128fe
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: configuring
discoiquuid: 0d055be7-7189-4587-8c7c-2ce34e22a6ad
docset: aem65
translation-type: tm+mt
source-git-commit: 38ef8fc8d80009c8ca79aca9e45cf10bd70e1f1e

---


# 복제 문제 해결{#troubleshooting-replication}

이 페이지에서는 복제 문제를 해결하는 방법에 대한 정보를 제공합니다.

## 문제 {#problem}

일부 이유로 복제(역복제 아님)가 실패합니다.

## 해상도 {#resolution}

복제에 실패하는 이유는 다양합니다. 이 문서에서는 이러한 문제를 분석할 때 발생할 수 있는 접근 방식을 설명합니다.

**활성화 버튼을 클릭하면 복제가 트리거됩니까? 그렇지 않은 경우 다음을 수행합니다.**

1. /crx/explorer로 이동하여 관리자로 로그인합니다.
1. &quot;콘텐츠 탐색기&quot; 열기
1. /bin/replicate 또는 /bin/replicate.json 노드가 있는지 확인하십시오. 노드가 있으면 노드를 삭제하고 저장합니다.

**복제 에이전트 큐에서 복제가 큐에 올라가 있습니까?**

/etc/replication/agents.author.html로 이동한 다음 복제 에이전트를 클릭하여 확인합니다.

**하나의 에이전트 큐 또는 몇 개의 에이전트 큐가 중지되는 경우:**

1. 대기열에 **차단된** 상태가 표시됩니까? 그렇다면 게시 인스턴스가 실행 중이 아니거나 완전히 응답하지 않습니까? 게시 인스턴스를 확인하여 문제가 있는지 확인합니다(예: 로그 확인, OutOfMemory 오류 또는 기타 문제가 있는지 확인). 그러면 보통 속도가 느린 경우 스레드 덤프를 사용하여 분석합니다.
1. 큐 상태에 **큐가 활성 상태임 - # 보류**&#x200B;중? 기본적으로 게시 인스턴스 또는 디스패처가 응답할 때까지 기다리는 소켓 읽기에 복제 작업이 중단될 수 있습니다. 이는 게시 인스턴스 또는 디스패처가 로드가 높거나 잠금 상태에 있음을 의미합니다. 이 경우 작성자의 스레드 덤프를 가져와 게시할 수 있습니다.

   * 스레드 덤프 분석기에서 작성자의 스레드 덤프를 열고 복제 에이전트의 sling 이벤트 작업이 socketRead에 고정되어 있는지 확인합니다.
   * 스레드 덤프 분석기의 게시에서 스레드 덤프를 열고 게시 인스턴스가 응답하지 않는 원인을 분석합니다. 작성자로부터 복제를 받는 스레드인 POST /bin/receive가 있는 스레드가 해당 이름으로 표시됩니다.

**모든 에이전트 큐가 중지되는 경우**

1. 저장소 손상 또는 일부 다른 문제로 인해 /var/replication/data 아래에서 특정 컨텐츠를 직렬화할 수 없을 수 있습니다. logs/error.log에서 관련 오류를 확인하십시오. 잘못된 복제 항목을 지우려면 다음을 수행합니다.

   1. https://&lt;host>:&lt;port>/crx/de로 이동하여 관리자 사용자로 로그인합니다.
   1. 상단 메뉴에서 &quot;도구&quot;를 클릭합니다.
   1. 돋보기 단추를 클릭합니다.
   1. &quot;XPath&quot;를 Type으로 선택합니다.
   1. &quot;쿼리&quot; 상자에 @slingevent:created의 이 쿼리 /jcr:root/var/events/jobs//element(*,slingevent:Job) 순서를 입력합니다.
   1. &quot;검색&quot;을 클릭합니다.
   1. 그 결과, 맨 위 항목은 최신 스프라이팅 작업입니다. 각 복제본을 클릭하고 대기열 맨 위에 표시되는 내용과 일치하는 중단된 복제본을 찾습니다.

1. 이벤트 프레임워크 작업 큐의 sling에 문제가 있을 수 있습니다. /system/console에서 org.apache.sling.event 번들을 다시 시작하십시오.
1. 작업 처리가 완전히 꺼져 있을 수 있습니다. [Sling Eventing] 탭의 [Felix 콘솔] 아래에서 확인할 수 있습니다. Apache Sling 이벤트(작업 처리가 비활성화됨!)가 표시되는지 확인

   * 이 경우 Felix Console의 구성 탭에서 Apache Sling 작업 이벤트 핸들러를 선택합니다. &#39;작업 처리 사용&#39; 확인란의 선택이 취소되어 있을 수 있습니다. 이 확인란을 선택했는데도 여전히 &#39;작업 처리가 비활성화됨&#39;으로 표시되면 /apps/system/config 아래에 작업 처리를 비활성화하는 오버레이가 있는지 확인하십시오. boolean 값을 true로 설정하여 jobmanager.enabled에 대한 osgi:config 노드를 만들고 활성화가 시작되었고 대기열에 더 이상 작업이 없는지 다시 확인하십시오.

1. DefaultJobManager 구성이 일관성이 없는 상태로 되는 경우도 있습니다. 이 문제는 OSGiconsole을 통해 수동으로 &#39;Apache Sling 작업 이벤트 핸들러&#39; 구성을 수정할 때 발생할 수 있습니다(예: &#39;작업 처리 활성화&#39; 속성을 비활성화하고 다시 활성화하고 구성 저장).

   * 이 시점에서 crx-quickstart/launchpad/config/org/apache/sling/event/impl/jobs/DefaultJobManager.config에 저장된 DefaultJobManager 구성이 일관성이 없는 상태로 전환됩니다. &#39;Apache Sling 작업 이벤트 핸들러&#39; 속성이 &#39;작업 처리 활성화&#39;를 체크 상태로 표시해도 [Sling 이벤트] 탭으로 이동하면 &#39;작업 처리 사용 안 함&#39;이라는 메시지가 표시되고 복제가 작동하지 않습니다.
   * 이 문제를 해결하려면 OSGi 콘솔의 구성 페이지로 이동하여 &#39;Apache Sling 작업 이벤트 처리기&#39; 구성을 삭제해야 합니다. 그런 다음 클러스터의 마스터 노드를 다시 시작하여 구성을 다시 일관된 상태로 만듭니다. 이 경우 문제가 해결되고 복제가 다시 시작됩니다.

**replication.log 만들기**

경우에 따라 모든 복제 로깅을 DEBUG 수준에서 별도의 로그 파일에 추가하도록 설정하는 것이 매우 유용합니다. 이를 위해 진행되는 작업:

1. https://host:port/system/console/configMgr으로 이동하여 관리자로 로그인합니다.
1. Apache Sling Logging Logger 팩토리를 찾아 공장 구성 오른쪽에 있는 **+** 버튼을 클릭하여 인스턴스를 만듭니다. 그러면 새로운 로깅 로거가 만들어집니다.
1. 다음과 같이 구성을 설정합니다.

   * 로그 수준:디버그
   * 로그 파일 경로:logs/replication.log
   * 카테고리:com.day.cq.re응용 프로그램

1. 이벤트/작업과 관련된 문제가 의심되는 경우 categories:org.apache.sling.event 아래에 이 java 패키지를 추가할 수도 있습니다

## 복제 에이전트 큐 일시 중지 {#pausing-replication-agent-queue}

때로 복제 큐를 일시 중지하여 비활성화하지 않고 작성자 시스템의 로드를 줄이는 것이 적절할 수 있습니다. 현재 이것은 잘못된 포트를 임시로 구성하는 경우에만 가능합니다. 5.4 이상 버전에서는 복제 에이전트 큐에 일시 중지 버튼이 표시될 수 있으며 몇 가지 제한이 있습니다.

1. 상태가 지속되지 않으므로 서버를 다시 시작하거나 복제 번들을 다시 사용하는 경우 다시 실행 상태로 돌아갑니다.
1. 일시 중지는 더 짧은 기간(다른 스레드의 복제 작업이 없는 후 OOB 1시간) 동안 유휴 상태이며 더 이상 사용되지 않습니다. Because There is a feature in sling which avoid idle threads. 기본적으로 작업 큐 스레드가 더 오랜 시간 동안 사용되지 않았는지 확인하고, 이렇게 되면 정리 주기가 시작됩니다. 정리 주기 때문에 스레드가 중단되고 일시 중지된 설정이 손실됩니다. 작업이 지속되므로 새 스레드를 시작하여 일시 중지된 구성에 대한 세부 정보가 없는 큐를 처리합니다. 이 큐가 실행 상태로 전환됩니다.

## 사용자 활성화 시 페이지 권한이 복제되지 않음 {#page-permissions-are-not-replicated-on-user-activation}

페이지 권한은 사용자가 아닌 액세스 권한이 부여된 노드 아래에 저장되므로 복제되지 않습니다.

일반적으로 페이지 권한은 작성자로부터 게시로 복제되어서는 안 되며 기본적으로 복제되지 않습니다. 액세스 권한은 두 환경에서 달라야 하기 때문입니다. 따라서 작성자와 별도로 게시 시 ACL을 구성하는 것이 좋습니다.

## 작성자에서 게시로 네임스페이스 정보를 복제할 때 복제 큐가 차단됨 {#replication-queue-blocked-when-replicating-namespace-information-from-author-to-publish}

경우에 따라 작성 인스턴스에서 게시 인스턴스로 네임스페이스 정보를 복제할 때 복제 큐가 차단되는 경우도 있습니다. 이 문제는 복제 사용자에게 `jcr:namespaceManagement` 권한이 없기 때문에 발생합니다. 이 문제를 방지하려면 다음을 확인하십시오.

* 전송 탭>사용자 아래에 구성된 [복제](/help/sites-deploying/replication.md#replication-agents-configuration-parameters) 사용자는 게시 인스턴스에도 있습니다.
* 사용자는 컨텐츠가 설치된 경로에서 읽기 및 쓰기 권한을 가집니다.
* 사용자는 저장소 수준에서 `jcr:namespaceManagement` 권한이 있습니다. 다음과 같이 권한을 부여할 수 있습니다.

1. CRX/DE( `https://localhost:4502/crx/de/index.jsp`)에 관리자로 로그인합니다.
1. 액세스 제어 **탭을** 클릭합니다.
1. 저장소를 **선택합니다**.
1. 항목 **추가** (더하기 아이콘)를 클릭합니다.
1. 사용자 이름을 입력합니다.
1. 권한 `jcr:namespaceManagement` 목록에서 선택합니다.
1. 확인을 클릭합니다.

