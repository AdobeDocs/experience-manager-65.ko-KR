---
title: Adobe Mobile Services Cloud Service 구성
seo-title: Adobe Mobile Services Cloud Service 구성
description: Adobe Mobile Services Cloud Service을 구성하려면 이 페이지를 따르십시오.
seo-description: Adobe Mobile Services Cloud Service을 구성하려면 이 페이지를 따르십시오.
uuid: 21fe5b24-dc4d-4ee4-9e7f-ed4783baf276
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: administering-adobe-phonegap-enterprise
discoiquuid: 962e9e98-a303-435b-a938-31319282e022
legacypath: /content/docs/en/aem/6-1/develop/mobile-apps/apps/managing-aem-mobile-apps/configure-your-adobe-phonegap-build-cloud-service1
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '468'
ht-degree: 1%

---


# Adobe Mobile Services Cloud Service {#configure-your-adobe-mobile-services-cloud-service} 구성

>[!NOTE]
>
>단일 페이지 애플리케이션 프레임워크 기반 클라이언트측 렌더링(예: 응답)이 필요한 프로젝트에는 SPA 편집기를 사용하는 것이 좋습니다. [추가 정보](/help/sites-developing/spa-overview.md).

명령 센터의 **모바일 지표 타일**&#x200B;은 모바일 응용 프로그램에 대한 실시간 분석을 제공합니다.

[Adobe 모바일 분석](https://www.adobe.com/ca/solutions/digital-analytics/mobile-web-apps-analytics.html) SDK는 PhoneGap 플러그인을 통해 사용할 수 있습니다. 지표가 수집 및 캐시되어 장치가 연결되어 보고 및 분석을 위해 데이터가 Adobe Mobile Services Cloud로 푸시될 때까지 장치에 캐시됩니다.

Adobe Mobile Analytics SDK는 다음을 제공합니다.

1. **모바일 채널을 위한 데이터 수집**  - 모든 주요 운영 체제에서 모바일 웹 사이트 및 앱에 대한 포괄적인 데이터를 수집할 수 있습니다.
1. **모바일 참여 분석**  - 모바일 앱, 웹 사이트 또는 비디오 내에서 소비자의 참여를 파악할 수 있습니다. 예를 들어 소비자의 채널 실행 빈도, 채널을 통한 구매 여부 등이 포함됩니다.
1. **모바일 앱 대시보드 및 보고서**  - 앱 및 앱스토어 지표에 대한 라이프사이클 지표가 포함된 사용 보고서를 가져옵니다. 사용자 동향, 실행 횟수, 평균 세션 길이, 유지 기간 및 충돌 횟수를 확인할 수 있습니다.
1. **모바일 캠페인 분석**  - SMS, 모바일 검색 광고, 모바일 디스플레이 광고, QR 코드 등 모바일별 캠페인의 효과를 수량화할 수 있습니다.
1. **지리적 위치 분석**  - GPS 위치 또는 관심 위치를 기반으로 앱 사용자가 모바일 경험을 실행하고 인터랙션하는 위치를 찾을 수 있습니다.
1. **경로 지정 분석**  - 사용자가 앱을 탐색하는 방법을 확인하여 사용자가 참여하고 있는 화면 및 UI 요소와 사용자가 떠나는 요인을 결정합니다.

>[!CAUTION]
>
>클라우드 서비스를 구성한 경우에만 **지표 분석** 타일이 대시보드에 표시됩니다.

![chlimage_1-22](assets/chlimage_1-22.png)

AEM 명령 센터 지표 타일

## Cloud Service {#configuring-the-cloud-service} 구성

Adobe Mobile Services Analytics를 활용하려면 Adobe Analytics 계정 정보로 AEM Mobile Analytics Cloud Service를 구성해야 합니다.

1. 오른쪽 상단의 아이콘을 클릭하여 앱 대시보드의 **Cloud Services 관리** 타일에서 Cloud Services을 추가하거나 편집합니다.

   ![chlimage_1-23](assets/chlimage_1-23.png)

1. **Cloud Services 추가 또는 편집** 화면이 표시됩니다. **Adobe Mobile Services**&#x200B;를 선택하고 **다음**&#x200B;을 클릭합니다.

   ![chlimage_1-24](assets/chlimage_1-24.png)

1. **Mobile Services**&#x200B;에서 기존 구성을 선택하거나 **구성 만들기**&#x200B;를 선택하여 새 구성을 만듭니다.

   새 구성에 대해 **Mobile Services 속성**&#x200B;을 입력하고 확인&#x200B;**을 클릭합니다.**

   ![chlimage_1-25](assets/chlimage_1-25.png)

   자격 증명이 확인되면 **확인** 단추가 **확인됨**&#x200B;으로 바뀝니다. **모바일 앱 서비스 선택**&#x200B;에서 모바일 서비스 앱을 선택할 수 있습니다.

   구성을 설정하려면 **제출**&#x200B;을 클릭합니다.

   ![chlimage_1-26](assets/chlimage_1-26.png)

1. 클라우드 구성을 설정하면 대시보드에서 동일한 항목을 볼 수 있습니다.

   ![chlimage_1-27](assets/chlimage_1-27.png)

   >[!NOTE]
   >
   >클라우드 구성을 설정하면 앱 대시보드에서 **지표 분석** 타일을 볼 수 있습니다.

   ![chlimage_1-28](assets/chlimage_1-28.png)

