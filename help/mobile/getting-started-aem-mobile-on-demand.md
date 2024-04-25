---
title: Adobe Experience Manager Mobile 온디맨드
description: 새로운 Adobe Experience Manager(AEM) 모바일 앱 경험을 시작하려면 콘텐츠를 편집할 준비가 되기 전에 역할 통합이 필요합니다. AEM Mobile On-Demand Services를 시작하려면 이 페이지를 따르십시오.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: introduction
content-type: reference
exl-id: 4be199d8-963d-4807-b9bb-e23fa577c5f2
solution: Experience Manager
feature: Mobile
role: User
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '761'
ht-degree: 1%

---

# AEM Mobile 온디맨드{#aem-mobile-on-demand}

>[!NOTE]
>
>Adobe 단일 페이지 애플리케이션 프레임워크 기반 클라이언트측 렌더링(예: React)이 필요한 프로젝트에는 SPA Editor를 사용하는 것이 좋습니다. [자세히 알아보기](/help/sites-developing/spa-overview.md).

>[!NOTE]
>
>Adobe Experience Manager(AEM)를 컨텐츠 관리 소스로 사용하지 않는 경우 다음을 참조하십시오. [AEM Mobile On-demand Services 도움말](https://helpx.adobe.com/digital-publishing-solution/topics.html).

AEM은 콘텐츠를 모바일 애플리케이션에 통합할 수 있는 몇 가지 도구를 제공합니다.

다음 다이어그램은 AEM Mobile과 온디맨드 서비스의 다양한 구성 요소가 어떻게 서로 결합하여 콘텐츠를 모바일 앱에 전달하는지를 보여 줍니다.

AEM Preflight 앱은 게시하기 전에 앱과 콘텐츠를 미리 보는 테스트 환경으로 간주될 수 있습니다. 반면에 AEM Mobile 앱은 배포를 위해 빌드된 최종 앱입니다.

>[!NOTE]
>
>Preflight 앱에 대해 자세히 알아보려면 [AEM Preflight 앱 사용](https://helpx.adobe.com/digital-publishing-solution/help/preflight-app.html) AEM Mobile On-demand Services 도움말에서 참조할 수 있습니다.

![chlimage_1-171](assets/chlimage_1-171.png)

>[!NOTE]
>
>위의 다이어그램에서 AEM Publish 인스턴스는 AEM Mobile On-demand Services에 대한 일반적인 배포 시나리오에 필요하지 않습니다.

## 새 모바일 앱 시작 {#starting-a-new-mobile-app}

AEM Mobile은 완전한 AEM 플랫폼을 구성하는 하나의 기둥에 불과합니다.

새로운 AEM Mobile 앱 경험을 시작하려면 콘텐츠를 편집할 준비가 되기 전에 역할을 통합해야 합니다. 다음 역할은 AEM Mobile 애플리케이션을 만드는 시작점을 제공합니다.

* **관리자**
* **개발자**
* **작성자**

>[!NOTE]
>
>AEM Mobile으로 작업하고 이 시작 안내서의 단계를 따르려면 먼저 사용자가 AEM에 익숙해야 합니다. AEM 기본 사항 알아보기 [여기](/help/sites-deploying/deploy.md).

### AEM Mobile 애플리케이션 대시보드 이해 {#understanding-the-aem-mobile-application-dashboard}

역할과 책임을 이해하기 전에 사용자는 **AEM Mobile 컨트롤 센터** 또는 **응용 프로그램 대시보드**. 클릭 [여기](/help/mobile/mobile-apps-ondemand-application-dashboard.md) 을 참조하십시오.

### AEM 관리자 {#aem-administrator}

An ***AEM 관리자*** 는 생성 마법사를 사용하여 앱을 생성하거나 기존 애플리케이션을 가져와서 AEM Mobile 카탈로그에 애플리케이션을 추가하는 역할을 합니다. AEM Mobile을 사용하여 앱을 생성하는 AEM 관리자 *만들기 마법사* 일반적으로 Adobe의 기본 참조 샘플 또는 (일반적으로) 다음 사용자가 만든 사용자 지정 앱 템플릿에서 원하는 앱 템플릿 중 하나를 선택합니다. *AEM 개발자.*

AEM 관리자는 AEM Mobile On-demand Services을 사용하여 앱을 만드는 동안 다음 작업을 담당합니다.

* [AEM Mobile 설정](/help/mobile/aem-mobile-setup.md)
* [사용자 및 사용자 그룹 구성](/help/mobile/aem-mobile-configure-users.md)
* [Preflight로 미리 보기](/help/mobile/aem-mobile-manage-ondemand-services.md)
* [Content Services 관리](/help/mobile/developing-content-services.md)

관리자의 역할과 책임을 시작하려면 다음을 참조하십시오. [AEM Mobile On-demand Services을 사용할 컨텐츠 관리](/help/mobile/aem-mobile.md).

## AEM 개발자 {#aem-developer}

An **AEM 개발자** *AEM 작성자 *가 아름답고 매력적인 모바일 경험을 만들 수 있도록 맞춤형 웹 템플릿과 구성 요소를 확장하고 만듭니다. 이러한 템플릿과 구성 요소는 모바일 앱 환경에 최적화될 뿐만 아니라, 옴니채널 서비스 엔드포인트에 대해 디바이스와 AEM 서버(임의 원격 서버) 모두에 통신합니다. AEM 기본 제공 콘텐츠 편집기는 *AEM 작성자* Adobe Experience Cloud의 나머지 부분과의 통합을 포함하여 앱 내에서 풍부하고 관련 있는 경험을 만들 수 있습니다.

AEM 개발자는 AEM Mobile On-demand Services을 사용하여 앱을 만드는 동안 다음 작업을 담당합니다.

* [앱 템플릿 및 구성 요소](/help/mobile/app-templates-and-components1.md)
* [콘텐츠 동기화가 있는 모바일](/help/mobile/mobile-ondemand-contentsync.md)
* [컨텐츠 속성 및 컨텐츠 내보내기](/help/mobile/on-demand-content-properties-exporting.md)
* [AEM Mobile 컨텐츠 서비스 개발](/help/mobile/developing-content-services.md)

개발자의 역할과 책임을 시작하려면 다음을 참조하십시오. [AEM Mobile On-demand Services용 AEM 컨텐츠 개발](/help/mobile/aem-mobile-on-demand.md).

>[!NOTE]
>
>An *AEM 개발자* 역할은 템플릿 및 구성 요소 개발로 시작되거나 종료되지 않습니다. An *AEM 개발자* 는 기본 참조 구현 샘플을 단순히 확장하는 대신 완전히 새로운 앱을 만들 수 있습니다.

## AEM Author {#aem-author}

An ***AEM 작성자* (또는 *마케터*)**는 사용자 정의 개발 또는 즉시 사용 가능한 템플릿과 구성 요소를 사용하여 페이지를 추가 및 편집하고 구성 요소를 드래그 앤 드롭하며 이미지, 비디오 및 텍스트 조각(콘텐츠 조각)을 포함한 DAM의 모든 유형의 미디어를 추가합니다. 그런 다음 AEM 기본 제공 콘텐츠 편집기를 *AEM 작성자* Adobe Experience Cloud의 나머지 부분과의 통합을 포함하여 앱 내에서 풍부하고 관련 있는 경험을 만들 수 있습니다.

AEM 작성자는 AEM Mobile On-demand Services을 사용하여 앱을 만들 때 다음 주제를 이해해야 합니다.

* [AEM Mobile 애플리케이션 대시보드](/help/mobile/mobile-apps-ondemand-application-dashboard.md)
* [응용 프로그램 만들기 및 구성 작업](/help/mobile/mobile-apps-ondemand-application-create-configure-action.md)
* [클라우드 구성](/help/mobile/mobile-on-demand-associating-an-on-demand-app-to-cloud-configuration.md)
* [컨텐츠 관리](/help/mobile/mobile-apps-ondemand-manage-content-ondemand.md)
* [Content Services 개요](/help/mobile/develop-content-as-a-service.md)

작성자의 역할과 책임을 시작하려면 다음을 참조하십시오. [AEM Mobile On-demand Services 앱용 AEM 컨텐츠 작성](/help/mobile/mobile-apps-ondemand.md).

>[!NOTE]
>
>AEM 작성자는 권한 설정, 카드 및 레이아웃 만들기, 푸시 알림 전송도 담당합니다. 또한 AEM Mobile에서 컨텐츠 작성, 문서 및 컬렉션 관리, 배너, 카드 및 레이아웃 만들기 방법에 대한 자세한 내용은 다음을 참조하십시오. [AEM Mobile 온디맨드 포털](https://helpx.adobe.com/digital-publishing-solution/topics.html#dynamicpod_reference_2).
