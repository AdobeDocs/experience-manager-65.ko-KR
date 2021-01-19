---
title: AEM Mobile On-Demand
seo-title: AEM Mobile On-Demand
description: 새로운 AEM Mobile 앱 환경을 시작하려면 콘텐츠 편집을 위해 역할을 통합해야 합니다. AEM 모바일 온디맨드 서비스를 시작하려면 이 페이지를 따르십시오.
seo-description: 새로운 AEM Mobile 앱 환경을 시작하려면 콘텐츠 편집을 위해 역할을 통합해야 합니다. AEM 모바일 온디맨드 서비스를 시작하려면 이 페이지를 따르십시오.
uuid: 175c609d-3cb8-4a1b-bfea-278df272e500
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: introduction
content-type: reference
discoiquuid: dc6891cd-19cc-4dff-8bda-a41ed8af8bfb
translation-type: tm+mt
source-git-commit: a876a1a8d4aeb9e9a94c93a16742a4058307b0a8
workflow-type: tm+mt
source-wordcount: '804'
ht-degree: 1%

---


# AEM Mobile On-Demand{#aem-mobile-on-demand}

>[!NOTE]
>
>단일 페이지 애플리케이션 프레임워크 기반 클라이언트측 렌더링(예: 응답)이 필요한 프로젝트에는 SPA 편집기를 사용하는 것이 좋습니다. [추가 정보](/help/sites-developing/spa-overview.md).

>[!NOTE]
>
>AEM을 컨텐츠 관리 소스로 사용하지 않는 경우 [AEM Mobile On-demand Services 도움말](https://helpx.adobe.com/digital-publishing-solution/topics.html)을 참조하십시오.

AEM은 모바일 애플리케이션에 컨텐츠를 통합할 수 있는 다양한 툴을 제공합니다.

다음 다이어그램은 AEM Mobile 및 On-Demand Services의 다양한 구성 요소가 모바일 앱에 컨텐츠를 전달하는 데 어떻게 연동되는지 보여줍니다.

AEM Preflight 앱은 게시 전에 앱 및 콘텐츠를 미리 보기 위한 테스트 환경으로 간주할 수 있습니다.반면 AEM Mobile 앱은 배포를 위해 빌드된 최종 앱입니다.

>[!NOTE]
>
>Preflight 앱에 대한 자세한 내용은 AEM Mobile On-demand Services 도움말의 [AEM Preflight 앱 사용](https://helpx.adobe.com/digital-publishing-solution/help/preflight-app.html)을 참조하십시오.

![chlimage_1-171](assets/chlimage_1-171.png)

>[!NOTE]
>
>위의 다이어그램에서 AEM 게시 인스턴스는 AEM Mobile On-demand Services의 일반적인 배포 시나리오에 필요하지 않습니다.

## 새 모바일 앱 시작 {#starting-a-new-mobile-app}

AEM Mobile은 완벽한 AEM 플랫폼을 구성하는 한 기둥에 불과합니다.

새로운 AEM Mobile 앱 환경을 시작하려면 콘텐츠 편집을 위해 역할을 통합해야 합니다. 다음 역할은 새 AEM Mobile 응용 프로그램을 만들기 위한 시작 지점을 제공합니다.

* **관리자**
* **개발자**
* **작성**

>[!NOTE]
>
>AEM Mobile을 사용하여 작업하고 이 시작하기 안내서의 단계를 따르기 전에 사용자는 AEM에 익숙해야 합니다. AEM [여기](/help/sites-deploying/deploy.md)에 대한 기본 사항을 알아봅니다.

### AEM Mobile 응용 프로그램 대시보드 {#understanding-the-aem-mobile-application-dashboard} 이해

역할 및 책임을 이해하기 전에 사용자는 **AEM Mobile Control Center** 또는 **Application Dashboard**&#x200B;에 대한 충분한 지식이 있어야 합니다. 자세한 내용을 보려면 [여기](/help/mobile/mobile-apps-ondemand-application-dashboard.md)를 클릭하십시오.

### AEM 관리자 {#aem-administrator}

***AEM 관리자***&#x200B;는 만들기 마법사를 사용하여 새 앱을 만들거나 기존 응용 프로그램을 가져와 AEM Mobile 카탈로그에 새 응용 프로그램을 추가할 책임이 있습니다. AEM MOBILE의 *만들기 마법사*&#x200B;를 사용하여 새 앱을 제작하는 AEM 관리자는 일반적으로 기본 참조 샘플 또는 *AEM 개발자가 만든 사용자 정의 앱 템플릿(대부분의 경우) 중 하나를 선택합니다.*

AEM 관리자는 AEM Mobile On-demand Services을 사용하여 앱을 만들 때 다음 작업을 수행합니다.

* [AEM Mobile 설정](/help/mobile/aem-mobile-setup.md)
* [사용자 및 사용자 그룹 구성](/help/mobile/aem-mobile-configure-users.md)
* [프리플라이트를 사용하여 미리 보기](/help/mobile/aem-mobile-manage-ondemand-services.md)
* [컨텐츠 서비스 관리](/help/mobile/developing-content-services.md)

관리자의 역할 및 책임을 시작하려면 [AEM Mobile On-demand Services을 사용하도록 컨텐츠 관리](/help/mobile/aem-mobile.md)를 참조하십시오.

## AEM 개발자 {#aem-developer}

**AEM 개발자**&#x200B;는 사용자 정의 웹 템플릿 및 구성 요소를 확장 및 생성하여 *AEM 작성자 *가 매력적이고 멋진 모바일 경험을 제작할 수 있도록 지원합니다. 이러한 템플릿 및 구성 요소는 모바일 앱 월드에만 최적화되어 있을 뿐만 아니라그러나 디바이스와 AEM 서버(모든 원격 서버)를 옴니채널 서비스 종단점으로 모두 통신합니다. AEM 내장 컨텐츠 편집기는 *AEM 작성자*&#x200B;에서 나머지 Adobe Marketing Cloud와의 통합을 포함하여 앱 내에서 풍부하고 연관성 있는 경험을 만드는 데 사용됩니다.

AEM 개발자는 AEM Mobile On-demand Services을 사용하여 앱을 제작하는 동안 다음 작업을 수행합니다.

* [앱 템플릿 및 구성 요소](/help/mobile/app-templates-and-components1.md)
* [컨텐츠 동기화를 통한 모바일](/help/mobile/mobile-ondemand-contentsync.md)
* [컨텐츠 속성 및 컨텐츠 내보내기](/help/mobile/on-demand-content-properties-exporting.md)
* [AEM Mobile 컨텐츠 서비스 개발](/help/mobile/developing-content-services.md)

개발자의 역할 및 책임을 시작하려면 [AEM Mobile On-demand Services용 AEM 컨텐츠 개발](/help/mobile/aem-mobile-on-demand.md)을 참조하십시오.

>[!NOTE]
>
>*AEM 개발자의* 역할은 템플릿 및 구성 요소 개발을 시작하고 종료하지 않습니다. *AEM 개발자*&#x200B;는 즉시 사용 가능한 참조 구현 샘플을 확장하는 대신 완전히 새로운 앱을 만들 수 있습니다.

## AEM Author {#aem-author}

***AEM 작성자*(또는 *마케터*)**는 사용자가 직접 개발한 템플릿과 구성 요소를 사용하여 페이지를 추가 및 편집하고, 구성 요소를 드래그 앤 드롭하고 DAM에서 이미지, 비디오 및 텍스트 조각(컨텐츠 조각)을 비롯한 모든 유형의 미디어를 추가합니다. 그런 다음 AEM 내장 컨텐츠 편집기를 *AEM 작성자*에서 나머지 Adobe Marketing Cloud와의 통합을 포함하여 앱 내에서 풍부하고 연관성 있는 경험을 만듭니다.

AEM 작성자는 AEM Mobile On-demand Services을 사용하여 앱을 제작하는 동안 다음 주제를 이해해야 합니다.

* [AEM Mobile 애플리케이션 대시보드](/help/mobile/mobile-apps-ondemand-application-dashboard.md)
* [응용 프로그램 만들기 및 구성 작업](/help/mobile/mobile-apps-ondemand-application-create-configure-action.md)
* [클라우드 구성](/help/mobile/mobile-on-demand-associating-an-on-demand-app-to-cloud-configuration.md)
* [컨텐츠 관리](/help/mobile/mobile-apps-ondemand-manage-content-ondemand.md)
* [콘텐츠 서비스 개요](/help/mobile/develop-content-as-a-service.md)

작성자의 역할 및 책임을 시작하려면 [AEM Mobile On-demand Services 앱용 AEM 콘텐츠 제작](/help/mobile/mobile-apps-ondemand.md)을 참조하십시오.

>[!NOTE]
>
>또한 AEM 작성자는 권한 부여 설정, 카드 및 레이아웃 만들기, 푸시 알림 전송에 대한 책임을 집니다. 또한 컨텐츠 작성 방법에 대한 자세한 내용을 살펴보려면아티클 및 컬렉션 관리aem mobile에서 배너, 카드 및 레이아웃을 만드는 경우 [AEM Mobile 온디맨드 포털](https://helpx.adobe.com/digital-publishing-solution/topics.html#dynamicpod_reference_2)을 참조하십시오.

