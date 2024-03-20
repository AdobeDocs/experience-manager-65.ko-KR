---
title: Adobe Target과 통합
description: Adobe Experience Manager을 Adobe Target과 통합하는 방법을 알아봅니다.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
exl-id: 2b17d8cd-a43c-4d54-b990-a6f0cb1db22b
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '567'
ht-degree: 65%

---

# Adobe Target과 통합{#integrating-with-adobe-target}

Adobe Marketing Cloud의 일부인 [Adobe Target](https://www.adobe.com/ro/solutions/testing-targeting/testandtarget.html)을 사용하여 모든 채널에 걸친 타겟팅 및 측정을 통해 콘텐츠 관련성을 높일 수 있습니다. 마케터는 Adobe Target을 사용하여 온라인 테스트를 디자인 및 실행하고, 즉석으로 대상자 세그먼트를 만들고(행동 기반), 콘텐츠 및 온라인 경험의 타겟팅을 자동화합니다. AEM은 Adobe Target Standard에서 사용되는 타겟팅 워크플로우를 채택했습니다. Target을 사용하는 경우 AEM의 타깃팅 편집 환경에 익숙할 것입니다.

AEM 사이트와 Adobe Target을 통합함으로써 페이지의 콘텐츠를 개인화하여 다음과 같은 작업을 수행할 수 있습니다.

* 콘텐츠 타겟팅 구현
* Target 대상자를 사용하여 개인화된 경험 만들기
* 방문자가 페이지와 상호 작용할 때 컨텍스트 데이터를 Target에 제출
* 전환율 추적

Target과 통합하려면 다음과 같은 작업을 수행해야 합니다.

1. [사전 요구 사항 작업 수행](/help/sites-administering/target-requirements.md): Adobe Target으로 등록하여 AEM 작성자 인스턴스의 특정 측면을 구성합니다. Adobe Target 계정에는 최소한 **승인자 **수준 권한이 있어야 합니다. 또한 사용자가 액세스할 수 없도록 게시 노드의 활동 설정을 보호해야 합니다.

1. 다음 중 하나를 선택합니다.

   1. [Adobe Target에 옵트인](/help/sites-administering/opt-in.md): 옵트인 마법사는 Target 계정 정보를 가져와 Adobe Target 클라우드 구성 및 Target 프레임워크를 만듭니다. 또한 이 마법사는 사이트를 Target 프레임워크와 연결합니다. 마법사가 대상에 연결할 수 없는 경우 [연결 문제 해결](/help/sites-administering/target-configuring.md#troubleshooting-target-connection-problems) 섹션. 그런 다음 [기본 클라우드 구성 수정](/help/sites-administering/target-configuring.md#modifying-the-opt-in-wizard-configurations): 필요한 경우 옵트인 마법사가 만든 클라우드 구성 및 프레임워크를 수정합니다. 예를 들어 추가적인 컨텍스트 데이터를 Target에 보내도록 프레임워크를 수정합니다. Adobe Analytics을 Adobe Target에 대한 보고 소스로 사용하려면 A4T 구성을 가리키도록 클라우드 구성을 수정해야 합니다.
   1. [Adobe Target과 수동으로 통합](/help/sites-administering/target-configuring.md#manually-integrating-with-adobe-target).

1. [활동 구성](/help/sites-authoring/activitylib.md): 활동을 Target 클라우드 구성과 연결합니다.

>[!NOTE]
>
>참조: [DTM을 사용하여 AEM과 Adobe Target 및 Adobe Analytics 통합](https://helpx.adobe.com/experience-manager/using/integrate-digital-marketing-solutions.html).

>[!NOTE]
>
>사용자 정의 프록시 구성을 통해 Target을 사용 중인 경우, AEM의 일부 기능은 3.x API를 사용하고 다른 일부 기능은 4.x API를 사용하므로 HTTP 클라이언트 프록시 구성을 모두 구성해야 합니다.
>
>* 3.x은(는) [http://localhost:4502/system/console/configMgr/com.day.commons.httpclient](http://localhost:4502/system/console/configMgr/com.day.commons.httpclient)로 구성됩니다.
>* 4.x은(는) [http://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator](http://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator)로 구성됩니다.
>

>[!CAUTION]
>
>일반 사용자가 액세스할 수 없도록 게시 인스턴스에서 활동 설정 노드 **cq:ActivitySettings**&#x200B;를 보호합니다. 활동 설정 노드는 Adobe Target에 대한 활동 동기화를 처리하는 서비스에만 액세스할 수 있어야 합니다.
>
>자세한 내용은 [Adobe Target과 통합하기 위한 전제 조건](/help/sites-administering/target-requirements.md#securing-the-activity-settings-node)을 참조하십시오.

통합이 완료되면 Adobe Target에 방문자 데이터를 전송하는 [타겟팅된 콘텐츠를 작성](/help/sites-authoring/content-targeting-touch.md)할 수 있습니다. 콘텐츠 타겟팅을 활성화하려면 페이지 구성 요소에 특정 코드가 필요합니다. (참조: [타깃팅된 컨텐츠를 위한 개발](/help/sites-developing/target.md).)

>[!NOTE]
>
>AEM 작성자의 구성 요소를 타겟팅하면 해당 구성 요소는 Adobe Target에 대한 일련의 서버측 호출을 만들어 캠페인을 등록하고, 오퍼를 설정하고, Adobe Target 세그먼트를 검색합니다(구성된 경우). AEM 게시에서 Adobe Target으로는 서버측 호출을 만들 수 없습니다.

## 배경 정보 소스 {#background-information-sources}

AEM을 Adobe Target과 통합하려면 Adobe Target, AEM 활동 관리 및 AEM 대상 관리에 대한 지식이 필요합니다. 다음과 같은 정보를 숙지해야 합니다.

* Adobe Target ([Adobe Target 설명서](https://experienceleague.adobe.com/docs/target/using/target-home.html) 참조)
* AEM 활동 콘솔([활동 관리](/help/sites-authoring/activitylib.md) 참조)
* AEM 대상자([대상자 관리](/help/sites-authoring/managing-audiences.md) 참조)

>[!NOTE]
>
>Adobe Target을 사용하여 작업 시 캠페인 내에서 허용되는 최대 아티팩트의 수는 다음과 같습니다.
>
>* 50개 위치
>* 2,000개 경험
>* 50개 지표
>* 50개 보고 세그먼트
>
