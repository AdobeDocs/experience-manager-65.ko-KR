---
title: 응용 프로그램 만들기 및 구성 작업
seo-title: 응용 프로그램 만들기 및 구성 작업
description: AEM Mobile 온디맨드 콘텐츠를 만들고 관리하는 첫 번째 단계는 종종 앱을 만드는 것입니다. 자세한 내용은 이 페이지를 참조하십시오.
seo-description: AEM Mobile 온디맨드 콘텐츠를 만들고 관리하는 첫 번째 단계는 종종 앱을 만드는 것입니다. 자세한 내용은 이 페이지를 참조하십시오.
uuid: f6b41d9a-d896-479e-9f6c-e91a88f3e74d
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: authoring-on-demand-services-app
discoiquuid: ccafd49a-5c8a-44eb-9b0c-37070560bb52
exl-id: dbe81ead-dfaa-4af0-9b66-a14917a1bcc7
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '469'
ht-degree: 1%

---

# 응용 프로그램 만들기 및 구성 작업{#application-create-and-configuration-actions}

>[!NOTE]
>
>단일 페이지 애플리케이션 프레임워크 기반 클라이언트측 렌더링(예: React)이 필요한 프로젝트에 SPA 편집기를 사용하는 것이 좋습니다. [추가 정보](/help/sites-developing/spa-overview.md).

## 주문형 응용 프로그램 만들기 {#creating-an-on-demand-application}

앱을 만드는 것은 종종 AEM Mobile On-Demand 컨텐츠를 만들고 관리하는 첫 번째 단계이며, AEM 관리자 수준에서 수행되는 경우가 많습니다. 문서, 이미지, 컬렉션 등과 같이 작성자가 만든 컨텐츠를 표시할 준비가 된 모바일 장치에서 볼 수 있는 컨텐츠 셸을 나타냅니다.

앱의 세부 사항은 대시보드 또는 AEM Mobile 컨트롤 센터에서 확인할 수 있습니다.

>[!NOTE]
>
>대시보드는 앱의 컨텐츠, 메타데이터 및 AEM Mobile 온디맨드 연결 상태에 대한 개요를 제공하는 유용한 타일의 시리즈입니다.
>
>자세한 내용은 [AEM Mobile Application Dashboard](/help/mobile/mobile-apps-ondemand-application-dashboard.md)를 참조하십시오.

**온디맨드 앱을 만들려면:**

1. 사이드 레일에서 **모바일**&#x200B;을 선택합니다.
1. 탐색에서 **앱**&#x200B;을 선택합니다.
1. **만들기**&#x200B;를 클릭하고 드롭다운에서 **App**&#x200B;을 선택합니다.
1. 모바일 앱 템플릿을 선택하고 **다음**&#x200B;을 클릭합니다.
1. **제목**, **이름**, **설명**&#x200B;과 같은 앱 속성을 입력합니다.
1. **다음**&#x200B;을 클릭합니다.
1. 알려진 경우 클라우드 구성 세부 사항을 입력하고, 그렇지 않은 경우 **만들기**&#x200B;를 클릭합니다.
1. 카탈로그에서 새 AEM Mobile 앱을 보려면 **완료**&#x200B;를 클릭하십시오.

![chlimage_1](assets/chlimage_1.gif)

>[!NOTE]
>
>이 프로세스를 사용하면 AEM에서 앱 인스턴스를 만들 수 있습니다.

## 앱 템플릿 사용 {#using-app-templates}

앱 템플릿을 사용하면 AEM 내에서 새로운 앱을 만드는 데 사용되는 개발자가 만든 기존 디자인을 쉽게 활용할 수 있습니다.

앱 템플릿이란 무엇입니까? 앱의 기준선 또는 기반을 나타내는 페이지 템플릿 및 구성 요소의 컬렉션으로 간주하십시오.
다른 앱의 템플릿을 기반으로 새 앱을 만들 때 앱이 만들어진 시작점을 나타내는 앱이 표시됩니다.

이 기능을 사용하려면 기존 모바일 앱 템플릿(또는 앱 템플릿이 있는 앱)이 설치되어 있어야 합니다.

### 다음 단계 {#the-next-step}

애플리케이션 대시보드에서 온디맨드 앱을 만들면 다음 단계는 앱을 클라우드 구성에 연결하는 것입니다.

자세한 내용은 [앱을 클라우드 구성에 연결](/help/mobile/mobile-on-demand-associating-an-on-demand-app-to-cloud-configuration.md)을 참조하십시오.

### 미리 보기 {#getting-ahead}

온디맨드 응용 프로그램을 만들어 이 앱을 클라우드 구성에 연결하는 것을 잘 알고 있으면 [컨텐츠 관리 작업](/help/mobile/mobile-apps-ondemand-manage-content-ondemand.md)을 참조하십시오.

**컨텐츠 관리** 작업에서는 다음 컨텐츠를 만들고 관리합니다.

* [문서 관리](/help/mobile/mobile-on-demand-managing-articles.md)
* [배너 관리](/help/mobile/mobile-on-demand-managing-banners.md)
* [컬렉션 관리](/help/mobile/mobile-on-demand-managing-collections.md)
* [공유 리소스 업로드](/help/mobile/mobile-on-demand-shared-resources.md)
* [게시 취소 컨텐츠](/help/mobile/mobile-on-demand-publishing-unpublishing.md)

관리자 및 개발자의 역할과 책임에 대해 알아보려면 아래 리소스를 참조하십시오.

* [AEM Mobile On-demand Services용 AEM 컨텐츠 개발](/help/mobile/aem-mobile-on-demand.md)
* [AEM Mobile On-demand Services을 사용할 컨텐츠 관리](/help/mobile/aem-mobile.md)
