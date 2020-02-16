---
title: AEM Mobile On-Demand
seo-title: AEM Mobile On-Demand
description: 새 AEM Mobile 앱 환경을 시작하려면 콘텐츠 편집을 위해 역할을 결합해야 합니다. AEM Mobile 온디맨드 서비스를 시작하려면 이 페이지를 따르십시오.
seo-description: 새 AEM Mobile 앱 환경을 시작하려면 콘텐츠 편집을 위해 역할을 결합해야 합니다. AEM Mobile 온디맨드 서비스를 시작하려면 이 페이지를 따르십시오.
uuid: 175c609d-3cb8-4a1b-bfea-278df272e500
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: introduction
content-type: reference
discoiquuid: dc6891cd-19cc-4dff-8bda-a41ed8af8bfb
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# AEM Mobile On-Demand{#aem-mobile-on-demand}

>[!NOTE]
>
>단일 페이지 애플리케이션 프레임워크 기반 클라이언트측 렌더링(예: 응답)이 필요한 프로젝트에 SPA 편집기를 사용하는 것이 좋습니다. [추가 정보](/help/sites-developing/spa-overview.md).

>[!NOTE]
>
>AEM을 콘텐츠 관리 소스로 사용하지 않는 경우 AEM Mobile 온디맨드 [서비스 도움말을 참조하십시오](https://helpx.adobe.com/digital-publishing-solution/topics.html).

AEM 파섹

다음 다이어그램은 AEM Mobile 및 On-Demand Services의 다양한 구성 요소가 모바일 앱에 콘텐츠를 전달하는 데 어떻게 적합한지 보여줍니다.

AEM Preflight 앱은 게시 전에 앱 및 콘텐츠를 미리 보기 위한 테스트 환경으로 간주할 수 있습니다.반면에 AEM Mobile 앱은 배포를 위해 빌드된 최종 앱입니다.

>[!NOTE]
>
>Preflight 앱에 대한 자세한 내용은 AEM [Mobile 온디맨드 서비스 도움말의 AEM Preflight 앱](https://helpx.adobe.com/digital-publishing-solution/help/preflight-app.html) 사용을 참조하십시오.

![chlimage_1-171](assets/chlimage_1-171.png)

>[!NOTE]
>
>위의 다이어그램에서 AEM Mobile 온디맨드 서비스에 대한 일반적인 배포 시나리오에 대해서는 AEM 게시 인스턴스가 필요하지 않습니다.

## 새 모바일 앱 시작 {#starting-a-new-mobile-app}

AEM Mobile은 전체 AEM 플랫폼을 구성하는 한 기둥에 불과합니다.

새 AEM Mobile 앱 환경을 시작하려면 콘텐츠 편집을 위해 역할을 결합해야 합니다. 다음 역할은 새 AEM Mobile 응용 프로그램을 만들기 위한 시작점을 제공합니다.

* **관리자**
* **개발자**
* **작성**

>[!NOTE]
>
>AEM Mobile을 사용하여 작업하고 이 시작 안내서의 단계를 따르기 전에 AEM에 익숙해야 합니다. Learn the basics of AEM [here](/help/sites-deploying/deploy.md).

### AEM Mobile 애플리케이션 대시보드 이해 {#understanding-the-aem-mobile-application-dashboard}

역할 및 책임을 이해하기 전에 사용자는 AEM Mobile Control Center **또는 애플리케이션 대시보드에** 대한 충분한 지식이 **있어야 합니다**. 자세한 내용을 살펴보려면 [여기를](/help/mobile/mobile-apps-ondemand-application-dashboard.md) 클릭하십시오.

### AEM 관리자 {#aem-administrator}

AEM ***관리자는*** 만들기 마법사를 사용하여 새 앱을 만들거나 기존 애플리케이션을 가져와 AEM Mobile 카탈로그에 새 애플리케이션을 추가할 책임이 있습니다. AEM Mobile의 *제작 마법사를* 사용하여 새 앱을 만드는 AEM 관리자는 일반적으로 기본 참조 샘플 또는 AEM 개발자가 만든 사용자 정의 앱 템플릿 중 하나를 *선택합니다.*

AEM 관리자는 AEM Mobile 온디맨드 서비스를 사용하여 앱을 제작하는 동안 다음 작업을 담당합니다.

* [AEM Mobile 설정](/help/mobile/aem-mobile-setup.md)
* [사용자 및 사용자 그룹 구성](/help/mobile/aem-mobile-configure-users.md)
* [Preflight를 사용한 미리 보기](/help/mobile/aem-mobile-manage-ondemand-services.md)
* [컨텐츠 서비스 관리](/help/mobile/developing-content-services.md)

관리자의 역할과 책임을 시작하려면 AEM Mobile 온디맨드 서비스 [사용을 위한 콘텐츠 관리를 참조하십시오](/help/mobile/aem-mobile.md).

## AEM 개발자 {#aem-developer}

AEM **개발자는** 사용자 정의 웹 템플릿과 구성 요소를 확장 및 생성하여 *AEM 작성자 *를 사용하여 매력적이고 멋진 모바일 경험을 제작할 수 있습니다. 이러한 템플릿 및 구성 요소는 모바일 앱 환경에만 최적화되어 있지 않습니다.그러나 장치 및 AEM 서버(모든 원격 서버)와 전체 채널 서비스 종단점에 모두 통신합니다. AEM의 내장 컨텐츠 편집기는 *AEM* 작성자가 나머지 Adobe Marketing Cloud와의 통합을 포함하여 앱 내에서 풍부하고 연관성 있는 경험을 제작하는 데 사용됩니다.

AEM 개발자는 AEM Mobile 온디맨드 서비스를 사용하여 앱을 제작하는 동안 다음 작업을 수행합니다.

* [앱 템플릿 및 구성 요소](/help/mobile/app-templates-and-components1.md)
* [Mobile with Content Sync](/help/mobile/mobile-ondemand-contentsync.md)
* [컨텐츠 속성 및 컨텐츠 내보내기](/help/mobile/on-demand-content-properties-exporting.md)
* [AEM Mobile 콘텐츠 서비스 개발](//help/mobile/developing-content-services.md)

개발자의 역할과 책임을 시작하려면 AEM Mobile 온디맨드 [서비스용 AEM 콘텐츠 개발을 참조하십시오](/help/mobile/aem-mobile-on-demand.md).

>[!NOTE]
>
>AEM *개발자의* 역할은 템플릿 및 구성 요소 개발에서 시작되고 종료되지 않습니다. AEM *개발자는* 즉시 사용 가능한 참조 구현 샘플만 확장하지 않고 완전히 새로운 앱을 만들 수 있습니다.

## AEM Author {#aem-author}

AEM ***작성자&#x200B;*(또는*마케터&#x200B;*)는&#x200B;**사용자 정의 템플릿과 구성 요소를 사용하여 페이지를 추가 및 편집하고, 구성 요소를 드래그 앤 드롭하고, DAM에서 이미지, 비디오 및 텍스트 조각(컨텐츠 조각)을 비롯한 모든 유형의 미디어를 추가합니다. 그런 다음 AEM의 내장된 컨텐츠 편집기는*AEM *작성자가 나머지 Adobe Marketing Cloud와의 통합을 포함하여 앱 내에서 풍부하고 연관성 있는 경험을 제작하는 데 사용됩니다.

AEM 작성자는 AEM Mobile 온디맨드 서비스를 사용하여 앱을 제작하는 동안 다음 항목을 이해해야 합니다.

* [AEM Mobile 애플리케이션 대시보드](/help/mobile/mobile-apps-ondemand-application-dashboard.md)
* [애플리케이션 만들기 및 구성 작업](/help/mobile/mobile-apps-ondemand-application-create-configure-action.md)
* [클라우드 구성](/help/mobile/mobile-on-demand-associating-an-on-demand-app-to-cloud-configuration.md)
* [컨텐츠 관리](/help/mobile/mobile-apps-ondemand-manage-content-ondemand.md)
* [콘텐츠 서비스 개요](/help/mobile/develop-content-as-a-service.md)

작성자의 역할 및 책임을 시작하려면 AEM Mobile 온디맨드 [서비스 앱용 AEM 콘텐츠 제작을 참조하십시오](/help/mobile/mobile-apps-ondemand.md).

>[!NOTE]
>
>또한 AEM 작성자는 권한 부여 설정, 카드 및 레이아웃 만들기, 푸시 알림 발송을 담당합니다. 또한 컨텐츠 작성 방법에 대한 자세한 내용을 살펴보십시오.아티클 및 컬렉션 관리aem Mobile에서 배너, 카드 및 레이아웃을 만드는 경우 [AEM Mobile 온디맨드 포털을 참조하십시오](https://helpx.adobe.com/digital-publishing-solution/topics.html#dynamicpod_reference_2).

