---
title: Adobe Target과 통합
seo-title: Adobe Target과 통합
description: Adobe Target과 AEM 통합에 대해 자세히 알아보십시오.
seo-description: Adobe Target과 AEM 통합에 대해 자세히 알아보십시오.
uuid: b90346e8-9757-4272-a870-bbe5e647303f
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: 454854f8-6053-406c-888d-f427777bf570
translation-type: tm+mt
source-git-commit: 70b18dbe351901abb333d491dd06a6c1c1c569d6
workflow-type: tm+mt
source-wordcount: '611'
ht-degree: 10%

---


# Adobe Target과 통합{#integrating-with-adobe-target}

Adobe Marketing Cloud의 일부로, [Adobe Target](http://www.adobe.com/ro/solutions/testing-targeting/testandtarget.html)을 사용하면 모든 채널에서 타깃팅과 측정을 통해 컨텐츠 관련성을 높일 수 있습니다. Adobe Target은 마케터가 온라인 테스트를 디자인 및 실행하고, 행동에 따라 고객 세그먼트를 만들고, 컨텐츠 및 온라인 경험 타깃팅을 자동화하는 데 사용됩니다. AEM에서 Adobe Target Standard에 사용되는 타깃팅 워크플로우를 채택했습니다. Target을 사용하는 경우 AEM의 타깃팅 편집 환경에 익숙할 것입니다.

AEM 사이트를 Adobe Target과 통합하여 컨텐츠를 페이지에 개인화합니다.

* 컨텐츠 타깃팅을 구현합니다.
* Target 고객을 사용하여 개인화된 경험 제작
* 방문자가 페이지와 상호 작용할 때 컨텍스트 데이터를 Target에 제출합니다.
* 전환율을 추적할 수 있습니다.

Target과 통합하려면 다음 작업을 수행합니다.

1. [사전 요구 작업](/help/sites-administering/target-requirements.md) 수행:Adobe Target에 등록하고 AEM 작성자 인스턴스의 특정 측면을 구성합니다. Adobe Target 계정에는 최소 **승인자 **수준 권한이 있어야 합니다. 또한 사용자가 액세스할 수 없도록 게시 노드에서 활동 설정을 보호해야 합니다.

1. 다음 중 하나를 선택합니다.

   1. [Adobe Target](/help/sites-administering/opt-in.md) 동의:옵트인 마법사는 Target 계정 정보를 가져와서 Adobe Target 클라우드 구성 및 Target 프레임워크을 만듭니다. 또한 마법사는 사이트를 Target 프레임워크과 연결합니다. 마법사가 대상에 연결할 수 없는 경우 [연결 문제 촬영](/help/sites-administering/target-configuring.md#troubleshooting-target-connection-problems) 섹션을 참조하십시오. 그런 다음 [기본 클라우드 구성을 수정할 수 있습니다](/help/sites-administering/target-configuring.md#modifying-the-opt-in-wizard-configurations).필요한 경우 옵트인 마법사가 만든 클라우드 구성 및 프레임워크를 수정합니다. 예를 들어 추가 컨텍스트 데이터를 Target으로 전송하도록 프레임워크를 수정합니다. Adobe Target의 보고 소스로 Adobe Analytics을 사용하려면 A4T 구성을 가리키도록 클라우드 구성을 수정해야 합니다.
   1. [Adobe Target과 수동 통합](/help/sites-administering/target-configuring.md#manually-integrating-with-adobe-target).

1. [활동 구성](/help/sites-authoring/activitylib.md):활동을 Target 클라우드 구성과 연결합니다.

>[!NOTE]
>
>DTM[을 사용하여 AEM과 Adobe Target 및 Adobe Analytics 통합을 참조하십시오.](https://helpx.adobe.com/experience-manager/using/integrate-digital-marketing-solutions.html)

>[!NOTE]
>
>사용자 지정 프록시 구성과 함께 Target을 사용하는 경우, HTTP 클라이언트 프록시 구성을 모두 AEM의 일부 기능에서 3.x API를 사용하고 4.x API를 사용하는 다른 기능으로서 구성해야 합니다.
>
>* 3.x는 [http://localhost:4502/system/console/configMgr/com.day.commons.httpclient](http://localhost:4502/system/console/configMgr/com.day.commons.httpclient)로 구성됩니다.
>* 4.x는 [http://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator](http://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator)로 구성됩니다.

>



>[!CAUTION]
>
>일반 사용자가 액세스할 수 없도록 게시 인스턴스에서 활동 설정 노드 **cq:ActivitySettings**&#x200B;를 보호해야 합니다. 활동 설정 노드는 Adobe Target에 대한 활동 동기화를 처리하는 서비스만 액세스할 수 있어야 합니다.
>
>자세한 내용은 [Adobe Target과 통합하기 위한 전제 조건](/help/sites-administering/target-requirements.md#securing-the-activity-settings-node)을 참조하십시오.

통합이 완료되면 방문자 데이터를 Adobe Target으로 보내는 [타깃팅된 컨텐츠](/help/sites-authoring/content-targeting-touch.md)를 작성할 수 있습니다. 페이지 구성 요소에는 컨텐츠 타깃팅을 활성화하려면 특정 코드가 필요합니다. ([타깃팅된 컨텐츠 개발](/help/sites-developing/target.md)을 참조하십시오.)

>[!NOTE]
>
>AEM 작성자의 구성 요소를 타깃팅하면 구성 요소는 Adobe Target에 일련의 서버측 호출을 수행하여 캠페인을 등록하고, 오퍼를 설정하고, Adobe Target 세그먼트를 검색합니다(구성된 경우). AEM 게시에서 Adobe Target으로 수행된 서버측 호출은 없습니다.

## 배경 정보 소스 {#background-information-sources}

AEM과 Adobe Target을 통합하려면 Adobe Target, AEM 활동 관리 및 AEM 대상 관리에 대한 지식이 필요합니다. 다음 정보에 익숙해야 합니다.

* Adobe Target([Adobe Target 설명서](https://docs.adobe.com/content/help/en/target/using/target-home.html) 참조).
* AEM 활동 콘솔([활동 관리](/help/sites-authoring/activitylib.md) 참조).
* AEM 대상([대상자 관리](/help/sites-authoring/managing-audiences.md) 참조).

>[!NOTE]
>
>Adobe Target 작업 시 캠페인 내에서 허용되는 최대 객체 수는 다음과 같습니다.
>
>* 50개 위치
>* 2,000개 경험
>* 50개 지표
>* 세그먼트 50개 보고

>



