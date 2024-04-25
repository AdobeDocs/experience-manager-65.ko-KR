---
title: Adobe Mobile Analytics로 앱 성능 추적
description: Adobe Mobile Services를 사용하면 모바일 앱에 대한 사용 현황, 앱 충돌, 장치 세부 정보 및 기타 많은 중요 지표를 추적하여 사용자가 모바일 앱을 어떻게 사용하고 있는지 파악할 수 있습니다. 자세한 내용은 이 페이지를 참조하십시오.
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
exl-id: 7e358660-bc2f-4d8f-8d74-6cdb6c1ea7b5
solution: Experience Manager
feature: Mobile
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '1054'
ht-degree: 1%

---

# Adobe Mobile Analytics로 앱 성능 추적{#track-app-performance-with-adobe-mobile-analytics}

>[!NOTE]
>
>Adobe 단일 페이지 애플리케이션 프레임워크 기반 클라이언트측 렌더링(예: React)이 필요한 프로젝트에는 SPA Editor를 사용하는 것이 좋습니다. [자세히 알아보기](/help/sites-developing/spa-overview.md).

더 높은 고객 전환율과 충성도를 원하게 됩니다.

고객에게 연관성 있고 매력적인 경험을 제공하려고 합니다.

AEM Mobile 앱이 마케팅 캠페인에 어떤 작업을 수행합니까?

모바일 애플리케이션을 미세 조정하여 사용자에게 최상의 경험을 제공하려면 어떻게 해야 합니까?

Adobe Mobile Services를 사용하면 모바일 앱에 대한 사용 현황, 앱 충돌, 장치 세부 정보 및 기타 많은 중요 지표를 추적하여 사용자가 모바일 앱을 어떻게 사용하고 있는지 파악할 수 있습니다.

Adobe Experience Manager Mobile에서는 AEM Mobile 애플리케이션 대시보드에서 바로 모바일 분석에 대한 세부 정보를 볼 수 있습니다. 다음 **모바일 지표 타일** 대시보드에서 모바일 애플리케이션용 Real-Time Analytics을 제공하므로 개발자, 작성자 및 관리자가 모바일 앱의 상태를 한 눈에 볼 수 있습니다. 표지 아래에서 분석을 강화하는 것은 [Adobe 모바일 분석](https://business.adobe.com/products/analytics/mobile-marketing.html) SDK. Adobe Mobile Analytics SDK는 기본적으로 또는 웹 보기용 PhoneGap Bridge 플러그인을 통해 애플리케이션에 연결할 수 있습니다. 지표는 장치가 연결될 때까지 장치에서 수집 및 캐시되며, 이때 보고 및 분석을 위해 데이터가 Adobe Mobile Services 클라우드로 푸시됩니다.

Adobe Mobile Analytics SDK는 다음을 제공합니다.

1. **모바일 채널을 위한 데이터 수집** - 모든 주요 운영 체제에서 모바일 웹 사이트 및 앱에 대한 포괄적인 데이터를 수집합니다.
1. **모바일 참여 분석** - 소비자가 채널을 실행하는 빈도, 채널을 구매하는지 여부 등을 포함하여 모바일 앱, 웹 사이트 또는 비디오 내의 사용자 참여를 이해합니다.
1. **모바일 앱 대시보드 및 보고서** - 앱에 대한 라이프사이클 지표 및 앱스토어 지표가 포함된 사용량 보고서를 가져옵니다. 사용자, 시작, 평균 세션 길이, 보존 길이 및 충돌에 대한 트렌드를 참조하십시오.
1. **모바일 캠페인 분석** - SMS, 모바일 검색 광고, 모바일 디스플레이 광고 및 QR 코드와 같은 모바일 특정 캠페인의 효과를 수량화합니다.
1. **지리적 위치 분석** - 앱 사용자가 GPS 위치 또는 관심 영역을 통해 모바일 경험을 시작하고 상호 작용하는 위치를 찾습니다.
1. **경로 지정 분석** - 사용자가 앱을 탐색하여 어떤 화면과 UI 요소가 사용자의 관심을 끌고 사용자가 중단되는지 확인하는 방법을 알아봅니다.

이 섹션에서는 다음 방법에 대해 설명합니다 [AEM 개발자](#developers) 그런 다음 analytics 추적을 사용하여 AEM Mobile 앱을 계측하는 방법을 배울 수 있습니다.

마지막으로, [AEM 관리자](#administrators) 학습 내용:

* 클라우드 서비스를 만들어 Mobile Services Adobe
* 모바일 서비스 구성 만들기 및 보고서 세트 연결
* 모바일 서비스 구성을 모바일 앱에 연결
* AEM 앱 명령 센터를 통해 지표 보기
* 모바일 앱에 AMS SDK 구성 할당

## 개발자용 - 앱에 Analytics 통합 {#for-developers-integrate-analytics-into-your-app}

**전제 조건:** AEM 관리자는 Adobe Mobile Services 클라우드 구성을 구성해야 합니다. [아래에서 논의되는 바와 같이](#amscloudserviceconfig).

개발자는 다음의 책임을 집니다. [AEM Mobile 앱에 analytics 추가](/help/mobile/phonegap-add-analytics-to-apps.md) 필요한 경우 사용자가 모바일 앱 컨텐츠에 어떻게 참여하는지를 추적, 보고 및 파악하고, 시작, 인앱 시간 및 충돌률과 같은 주요 라이프사이클 지표를 측정합니다.

## 관리자용 - Mobile Services Adobe Cloud Service 구성 {#for-administrators-configure-the-adobe-mobile-services-cloud-service}

Adobe Mobile Services를 활용하려면 Adobe Analytics 계정 정보로 AEM Adobe Mobile Services Cloud Service을 구성해야 합니다. Apps Command Center에서는 **지표 분석** 타일을 사용하여 클라우드 서비스를 만들고 모바일 앱과 연결할 수 있습니다.

모바일 앱에 대한 클라우드 서비스 구성은 지표 분석 타일에서 톱니바퀴 아이콘을 클릭하여 시작합니다.

![chlimage_1-125](assets/chlimage_1-125.png)

지표 분석 타일에서 톱니바퀴 아이콘을 클릭하면 &#39;Mobile Services Analytics 구성&#39; 모달 대화 상자가 열립니다. &#39;모바일 서비스 구성 선택&#39; 드롭다운에서 구성을 선택합니다. 구성을 만들어야 하는 경우 렌치 버튼을 클릭합니다.

Adobe Mobile Service 클라우드 서비스를 만들려면 서비스에 연결하는 단계와 구성에 할당할 보고 세트를 선택하는 단계가 있습니다.

시작하려면 대시보드의 Cloud Service 관리 타일에서 &#39;+&#39; 버튼을 클릭하십시오.

![chlimage_1-126](assets/chlimage_1-126.png)

를 클릭한 후&#x200B;**+**&#39; 버튼, **Cloud Service 추가** 마법사가 표시됩니다.

![chlimage_1-127](assets/chlimage_1-127.png)

아래 표시된 대로 필수 필드를 채워 모바일 서비스 구성을 선택하거나 만듭니다. AEM 관리자가 Adobe Mobile Services에 대한 연결을 만들려면 이 정보가 필요합니다.

![chlimage_1-128](assets/chlimage_1-128.png)

Mobile Services 계정 설정을 완료하면 앱을 선택하라는 메시지가 표시됩니다. 이렇게 하면 Adobe Mobile Service 분석 보고가 해당 애플리케이션에 연결됩니다.

원하는 모바일 서비스를 선택하고 &#39;업데이트&#39;를 클릭하여 모바일 서비스 구성을 지정하고 대화 상자를 닫습니다.

모바일 서비스 구성을 AEM Mobile 앱에 연결했으므로 타일은 지표 데이터를 가져오고 보고를 시작합니다.

![chlimage_1-129](assets/chlimage_1-129.png)

### Adobe Mobile Services SDK 구성 파일 {#adobe-mobile-services-sdk-config-file}

이 시점에서 모바일 애플리케이션은 클라우드 서비스와 연결되지만 모바일 애플리케이션은 아직 수집된 모바일 지표를 Adobe Analytics에 다시 전달하는 방법을 알지 못합니다. 모바일 앱을 Adobe Analytics에 연결하려면 Adobe Mobile Services SDK 구성 파일을 Adobe Experience Manager에 추가해야 합니다.

지표 분석 타일에서 화살표 아이콘을 클릭하여 AMS SDK 구성 다운로드/업로드 메뉴 항목을 표시합니다.

![chlimage_1-130](assets/chlimage_1-130.png)

첫 번째 단계는 Adobe Mobile Services에서 SDK 구성을 가져오는 것입니다. 구성 파일을 다운로드할 수 있는 Adobe Mobile Services 웹 사이트로 리디렉션하려면 &#39;AMS SDK 구성 다운로드&#39;를 클릭하십시오. ADBMobileConfig.json 파일을 가져온 후 &quot;AMS SDK 구성 업로드&quot;를 클릭하여 구성 파일을 AEM에 업로드합니다.

![chlimage_1-131](assets/chlimage_1-131.png)

&#39;Adobe Mobile Services 애플리케이션 구성 업로드&#39; 버튼을 클릭하고 ADBMobileConfig.json 파일을 찾은 다음 &#39;업로드&#39;를 클릭합니다.

이제 모바일 앱에서 ADBMobileConfig.json 파일에 액세스할 수 있으므로 Adobe Analytics에 다시 통신하고 앱 성공을 이끄는 데 도움이 되는 중요한 지표 값에 대한 보고를 시작하는 방법에 대한 지식을 보유하고 있습니다.

## 다음은 무엇입니까? {#what-s-next}

1. [내 AEM Mobile 앱 경험 시작](/help/mobile/starting-aem-phonegap-app.md)
1. [내 앱 콘텐츠 관리](/help/mobile/phonegap-manage-app-content.md)
1. [내 애플리케이션 빌드](/help/mobile/building-app-mobile-phonegap.md)
1. [Adobe Mobile Analytics로 앱 성능 추적](/help/mobile/phonegap-intro-to-app-analytics.md)
1. [Adobe Target을 통해 개인화된 앱 경험 제공](/help/mobile/phonegap-aem-mobile-content-personalization.md)
1. [내 사용자에게 중요한 메시지 보내기](/help/mobile/phonegap-push-notifications.md)
