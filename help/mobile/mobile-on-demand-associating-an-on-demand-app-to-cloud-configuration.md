---
title: 클라우드 구성
description: 온디맨드 앱을 클라우드 구성에 연결하면 Adobe Experience Manager(AEM)가 양방향 링크를 설정하여 Mobile On-Demand 호스팅 프로젝트와 직접 통신할 수 있습니다. 자세한 내용은 이 페이지를 참조하십시오.
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: authoring-on-demand-services-app
exl-id: 37428543-c310-4712-a4ec-1f482579fb4b
solution: Experience Manager
feature: Mobile
role: User
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '412'
ht-degree: 5%

---

# 클라우드 구성{#cloud-configuration}

>[!NOTE]
>
>Adobe 단일 페이지 애플리케이션 프레임워크 기반 클라이언트측 렌더링(예: React)이 필요한 프로젝트에는 SPA Editor를 사용하는 것이 좋습니다. [자세히 알아보기](/help/sites-developing/spa-overview.md).

온디맨드 앱을 클라우드 구성에 연결하면 Adobe Experience Manager(AEM)가 양방향 링크를 설정하여 Mobile On-Demand 호스팅 프로젝트와 직접 통신할 수 있습니다. 앱을 Mobile On-Demand 프로젝트에 연결하면 AEM 내에서 문서, 배너 및 컬렉션과 같은 콘텐츠 작성을 수행할 수 있지만 해당 콘텐츠를 Mobile On-Demand에 제공할 수도 있습니다.

거기서부터 콘텐츠 게시, 미리보기, 관리 등이 가능해진다. 기존 Mobile On-Demand 콘텐츠를 AEM으로 가져오고 콘텐츠 편집을 수행할 수도 있습니다.

## 클라우드 구성 설정 {#setting-up-cloud-configuration}

>[!CAUTION]
>
>온디맨드 앱에 대한 클라우드 구성 구성을 시작하기 전에 AEM Mobile 프로비저닝 및 AEM Mobile On-demand Services 클라이언트 구성에 익숙해야 합니다.
>
>자세한 내용은 관리 섹션에서 [AEM Mobile On-demand Services 설정](/help/mobile/aem-mobile-setup.md)을 참조하십시오.

Mobile On-Demand Cloud Service을 구성하려면 앱 대시보드에서 **연결 관리** 타일의 오른쪽 상단 모서리에 있는 톱니바퀴를 클릭합니다.

앱 대시보드 및 사용 가능한 타일에 익숙해야 합니다. 자세한 내용은 [AEM Mobile 응용 프로그램 대시보드](/help/mobile/mobile-apps-ondemand-application-dashboard.md)를 참조하세요.

### 클라우드 구성에 대한 링크 설정 {#setting-up-link-to-cloud-configuration}

>[!CAUTION]
>
>기존 온디맨드 클라이언트 및 클라우드 구성이 있는지 확인합니다.
>
>자세한 내용은 관리 섹션에서 [AEM Mobile On-demand Services 설정](/help/mobile/aem-mobile-setup.md)을 참조하십시오.

다음 단계에서는 클라우드 구성 링크 설정에 대해 설명합니다.

1. **Mobile**&#x200B;에서 **앱**&#x200B;을 선택한 다음 카탈로그에서 Mobile On-Demand 앱을 선택하십시오.
1. **연결 관리** 타일에서 톱니바퀴 아이콘을 클릭합니다.

   ![chlimage_1-65](assets/chlimage_1-65.png)

1. 기존 구성을 입력하거나 **구성 제목**, **장치 ID** 및 **장치 토큰**&#x200B;을 입력하여 만드십시오.

   ![chlimage_1-66](assets/chlimage_1-66.png)

1. **장치 ID** 및 **장치 토큰**&#x200B;이 확인되면 목록에서 온디맨드 프로젝트를 선택하십시오.

   **제출**&#x200B;을 클릭합니다.

   ![chlimage_1-67](assets/chlimage_1-67.png)

   **연결 관리** 타일은 클라우드 구성을 보여 줍니다.

   ![chlimage_1-68](assets/chlimage_1-68.png)

   >[!CAUTION]
   >
   >대시보드에서 프로젝트를 전환하는 동안 이 앱과 연결된 프로젝트를 변경하려고 하면 아래 그림과 같이 컨텐츠 무결성 문제에 대한 경고가 표시됩니다.

   ![chlimage_1-69](assets/chlimage_1-69.png)

### 다음 단계 {#the-next-steps}

앱에 대한 클라우드 구성을 구성한 후에는 콘텐츠 관리를 위한 다음 리소스를 참조하십시오.

* [문서 관리](/help/mobile/mobile-on-demand-managing-articles.md)
* [배너 관리](/help/mobile/mobile-on-demand-managing-banners.md)
* [컬렉션 관리](/help/mobile/mobile-on-demand-managing-collections.md)
* [공유 리소스 업로드](/help/mobile/mobile-on-demand-shared-resources.md)
* [콘텐츠 게시/게시 취소](/help/mobile/mobile-on-demand-publishing-unpublishing.md)
* [Preflight로 미리 보기](/help/mobile/aem-mobile-manage-ondemand-services.md)
