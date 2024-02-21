---
title: 응용 프로그램 만들기 및 구성 작업
description: 앱을 만드는 것은 종종 AEM Mobile 온디맨드 콘텐츠를 만들고 관리하는 첫 단계입니다. 자세한 내용은 이 페이지를 참조하십시오.
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: authoring-on-demand-services-app
exl-id: dbe81ead-dfaa-4af0-9b66-a14917a1bcc7
source-git-commit: 80e85ed78a26d784f4aa8e36c7de413cf9c03fa2
workflow-type: tm+mt
source-wordcount: '440'
ht-degree: 0%

---

# 응용 프로그램 만들기 및 구성 작업{#application-create-and-configuration-actions}

>[!NOTE]
>
>Adobe 단일 페이지 애플리케이션 프레임워크 기반 클라이언트측 렌더링(예: React)이 필요한 프로젝트에는 SPA Editor를 사용하는 것이 좋습니다. [자세히 알아보기](/help/sites-developing/spa-overview.md).

## 온디맨드 애플리케이션 생성 {#creating-an-on-demand-application}

앱을 만드는 것은 AEM Mobile 온디맨드 콘텐츠를 만들고 관리하기 위한 첫 번째 단계이며 AEM 관리자 수준에서 수행되는 경우가 많습니다. 문서, 이미지 및 컬렉션과 같이 작성자가 만든 콘텐츠를 표시할 준비가 된 모바일 디바이스에서 볼 수 있는 콘텐츠 셸을 나타냅니다.

앱의 세부 정보는 대시보드 또는 AEM Mobile 제어 센터에서 볼 수 있습니다.

>[!NOTE]
>
>대시보드 는 앱의 콘텐츠, 메타데이터 및 AEM Mobile 온디맨드 연결 상태에 대한 개요를 제공하는 유용한 타일 시리즈입니다.
>
>다음을 참조하십시오 [AEM Mobile 애플리케이션 대시보드](/help/mobile/mobile-apps-ondemand-application-dashboard.md) 을 참조하십시오.

**온디맨드 앱을 만들려면:**

1. 선택 **모바일** 사이드 레일에서.
1. 선택 **앱** 탐색에서.
1. 클릭 **만들기** 및 선택 **앱** 드롭다운에서 을 클릭합니다.
1. 모바일 앱 템플릿을 선택하고 **다음**.
1. 다음과 같은 앱 속성 입력 **제목**, **이름**, **설명**.
1. **다음**&#x200B;을 클릭합니다.
1. 알려진 경우 클라우드 구성 세부 정보를 입력하고 그렇지 않은 경우 을 클릭합니다. **만들기**.
1. 클릭 **완료** 카탈로그에서 새 AEM Mobile 앱을 봅니다.

![chlimage_1](assets/chlimage_1.gif)

>[!NOTE]
>
>이 프로세스를 사용하면 AEM에서 앱 인스턴스를 만들 수 있습니다.

## 앱 템플릿 사용 {#using-app-templates}

앱 템플릿은 개발자가 만든 기존 디자인을 AEM 내에서 새 앱을 만드는 데 사용하는 간편한 방법을 제공합니다.

앱 템플릿이란 무엇입니까? 앱의 기준선이나 기반을 나타내는 페이지 템플릿과 구성 요소의 컬렉션으로 생각하십시오.
다른 앱의 템플릿을 기반으로 앱을 만들 때 앱이 만들어진 원본 앱을 나타내는 시작점이 있는 앱이 제공됩니다.

이 기능을 사용하려면 기존 모바일 앱 템플릿(또는 앱 템플릿이 설치된 앱)이 있어야 합니다.

### 다음 단계 {#the-next-step}

애플리케이션 대시보드에서 온디맨드 앱을 만들면 다음 단계는 앱을 클라우드 구성에 연결하는 것입니다.

다음을 참조하십시오 [앱을 클라우드 구성에 연결](/help/mobile/mobile-on-demand-associating-an-on-demand-app-to-cloud-configuration.md) 을 참조하십시오.

### 시작하기 {#getting-ahead}

온디맨드 애플리케이션을 만들어 해당 앱을 클라우드 구성에 연결하는 방법에 익숙해지면 다음을 참조하십시오. [컨텐츠 관리 작업](/help/mobile/mobile-apps-ondemand-manage-content-ondemand.md).

**컨텐츠 관리 작업** 에는 다음 컨텐츠 생성 및 관리 작업이 포함됩니다.

* [문서 관리](/help/mobile/mobile-on-demand-managing-articles.md)
* [배너 관리](/help/mobile/mobile-on-demand-managing-banners.md)
* [컬렉션 관리](/help/mobile/mobile-on-demand-managing-collections.md)
* [공유 리소스 업로드](/help/mobile/mobile-on-demand-shared-resources.md)
* [게시 취소 컨텐츠](/help/mobile/mobile-on-demand-publishing-unpublishing.md)

관리자 및 개발자의 역할과 책임에 대해 알아보려면 아래 리소스를 참조하십시오.

* [AEM Mobile On-demand Services용 AEM 컨텐츠 개발](/help/mobile/aem-mobile-on-demand.md)
* [AEM Mobile On-demand Services을 사용할 컨텐츠 관리](/help/mobile/aem-mobile.md)
