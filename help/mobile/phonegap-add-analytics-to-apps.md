---
title: 모바일 애플리케이션에 Adobe Analytics 추가
seo-title: 모바일 애플리케이션에 Adobe Analytics 추가
description: Adobe Mobile Services와 통합하여 AEM 앱에서 모바일 앱 분석을 사용하는 방법에 대해 알려면 이 페이지를 따르십시오.
seo-description: Adobe Mobile Services와 통합하여 AEM 앱에서 모바일 앱 분석을 사용하는 방법에 대해 알려면 이 페이지를 따르십시오.
uuid: d3ff6f9b-0467-4abe-9a59-b3495a6af0f8
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
discoiquuid: cd9d2bea-48d8-4a17-8544-ea25dcad69f3
translation-type: tm+mt
source-git-commit: 8279cd590244a7f2d20cfaf1c7505a3ef57fae4a
workflow-type: tm+mt
source-wordcount: '971'
ht-degree: 0%

---


# 모바일 응용 프로그램에 Adobe Analytics 추가{#add-adobe-analytics-to-your-mobile-application}

>[!NOTE]
>
>단일 페이지 애플리케이션 프레임워크 기반 클라이언트측 렌더링(예: 응답)이 필요한 프로젝트에는 SPA 편집기를 사용하는 것이 좋습니다. [추가 정보](/help/sites-developing/spa-overview.md).

모바일 애플리케이션 사용자를 위해 매력적이고 연관성 있는 경험을 구축하고자 하십니까? Adobe Mobile Services SDK를 사용하여 애플리케이션 라이프사이클 및 사용량을 모니터링하고 측정하지 않는 경우 어떤 결정을 내리고 있습니까? 가장 충성스러운 고객은 어디에 있습니까? 고객의 관심사와 연관성 높은 전환율을 유지하고 전환을 최적화하는 데 어떻게 기여할 수 있습니까?

사용자가 모든 컨텐츠에 액세스하고 있습니까? 앱을 버리고 있다면 어디에 있습니까? 얼마나 자주 앱에서 유지되며 얼마나 자주 다시 돌아와 앱을 사용합니까? 어떤 변경 사항을 적용하고 유지율을 높일 수 있습니까? 충돌이 발생하는 경우는 어떻습니까? 사용자에게 앱이 작동하지 않는 이유는 무엇입니까?

[Adobe Mobile Services](https://www.adobe.com/marketing-cloud/mobile-marketing.html)와 통합하여 AEM 앱에서 [모바일 앱 분석](https://www.adobe.com/ca/solutions/digital-analytics/mobile-web-apps-analytics.html)을 활용할 수 있습니다.

AEM Apps를 사용하면 모바일 앱 및 컨텐츠에 대한 사용자의 참여 방법을 추적, 보고 및 파악할 수 있고 실행 횟수, 앱 내 시간, 충돌 속도 등 주요 라이프사이클 측정 지표를 측정할 수 있습니다.

이 섹션에서는 AEM *개발자*&#x200B;가 다음을 수행할 수 있는 방법에 대해 설명합니다.

* 모바일 분석에 모바일 애플리케이션 통합
* Bloodhound를 사용하여 분석 추적 테스트

## 사전 요구 사항 {#prerequisties}

AEM Mobile은 앱에서 추적 데이터를 수집하고 보고하려면 Adobe Analytics 계정이 필요합니다. 구성의 일부로 AEM *Administrator*&#x200B;는 먼저 다음을 수행해야 합니다.

* Adobe Analytics 계정을 설정하고 Mobile Services에서 애플리케이션에 대한 보고서 세트를 만듭니다.
* AEM(Adobe Experience Manager)에서 AMS Cloud Service을 구성합니다.

## 개발자용 - 모바일 분석을 앱 {#for-developers-integrate-mobile-analytics-into-your-app}에 통합

### 구성 파일 {#configure-contentsync-to-pull-in-configuration-file}을(를) 가져오도록 ContentSync 구성

Analytics 계정이 설정되면 콘텐츠를 모바일 응용 프로그램으로 가져오려면 콘텐츠 동기화 구성을 만들어야 합니다.

자세한 내용은 콘텐츠 동기화 콘텐츠 구성을 참조하십시오. 구성은 컨텐트 동기화를 통해 ADBMobileConfig를 /www 디렉토리에 배치하도록 지시해야 합니다. 예를 들어 Geometrixx Outdoors 앱에서 콘텐츠 동기화 구성은 다음 위치에 있습니다.*/content/phonegap/geometrixx-outdoors/shell/jcr:content/page-app/app-config/ams-ADBMobileConfig*. 개발을 위한 구성도 있습니다.그러나 Geometrixx Outdoors의 경우 개발이 아닌 구성과 동일합니다.

모바일 응용 프로그램 AEM Apps 대시보드에서 ADBMobileConfig를 다운로드하는 방법에 대한 자세한 내용은 Analytics - Mobile Services - Adobe Mobile Services SDK 구성 파일을 참조하십시오.

```xml
<jcr:root xmlns:jcr="https://www.jcp.org/jcr/1.0" xmlns:nt="https://www.jcp.org/jcr/nt/1.0"
    jcr:primaryType="nt:unstructured"
    extension="json"
    path="../../../.."
    selector="ADBMobileConfig"
    targetRootDirectory="www"
    type="mobileADBMobileConfigJSON"/>
```

각 플랫폼을 사용하려면 ADBMobileConfig를 특정 위치에 복사해야 합니다.

PhoneGap CLI를 사용하여 구축하는 경우 cordova 빌드 후크 스크립트로 수행할 수 있습니다. Geometrixx Outdoors 앱에서 볼 수 있는 위치:*content/phonegap/geometrixx-outdoors/shell/_jcr_content/pge-app/app-content/phonegap/scripts/restore_plugins.js.*

iOS의 경우 파일을 XCode 프로젝트의 **Resources** 디렉토리(예: &quot;platforms/ios/Geometrixx/Resources/ADBMobileConfig.json&quot;). 앱이 Android를 대상으로 하는 경우 복사할 경로는 &quot;platforms/android/assets/ADBMobileConfig.json&quot;입니다. PhoneGap CLI 빌드 중 후크를 사용하는 방법에 대한 자세한 내용은 [Cordova/PhoneGap 프로젝트에 필요한 ](https://devgirl.org/2013/11/12/three-hooks-your-cordovaphonegap-project-needs/)을 참조하십시오.

```xml
///////////////////////////
//          iOS
///////////////////////////
    ios : [
        {
            "www/ADBMobileConfig.json": "platforms/ios/<YOUR_APP_NAME>/Resources/ADBMobileConfig.json"
        }
    ],
///////////////////////////
//          ANDROID
///////////////////////////
    android: [
        {
            "www/ADBMobileConfig.json": "platforms/android/assets/ADBMobileConfig.json"
        }
    ]
```

### 앱 {#add-the-ams-plugin-in-the-app}에 AMS 플러그인을 추가합니다.

앱이 데이터를 수집하려면 AMS(Adobe Mobile Services) 플러그인을 앱의 일부로 포함해야 합니다. 플러그인을 앱의 config.xml에 기능으로 포함함으로써 PhoneGap 빌드 프로세스 동안 플러그인을 자동으로 추가하는 데 다른 Cordova 후크를 사용할 수 있습니다.

```xml
<feature name="ADBMobile">
    <param name="id" value="https://github.com/Adobe-Marketing-Cloud/mobile-services#0482f9cedf90c98a8d4b07219ece1933b2e46a60"/>
</feature>
```

Geometrixx Outdoors 앱 config.xml은 */content/phonegap/geometrixx-outdoors/shell/jcr:content/pge-app/app-content/phonegap/www/config.xml*&#x200B;에 있습니다. 위의 예에서는 플러그인 URL 뒤에 &#39;#&#39;를 추가한 다음 태그 값을 추가하여 사용할 특정 버전의 플러그인을 요청합니다. 이는 빌드 중에 테스트되지 않은 플러그인이 추가되었기 때문에 예상치 못한 문제가 발생하지 않도록 하기 위해 수행하는 좋은 방법입니다.

이 단계를 수행하면 앱이 Adobe Analytics에서 제공하는 모든 라이프사이클 지표를 보고할 수 있게 됩니다. 여기에는 시작, 충돌 및 설치와 같은 데이터가 포함됩니다. 만약 그것이 당신이 관심을 가지는 유일한 데이터라면 당신은 끝납니다. 사용자 지정 데이터를 수집하려면 코드를 작성해야 합니다.

### 전체 앱 추적 {#instrument-your-code-for-full-app-tracking}에 대한 코드 계기

[AMS Phonegap Plugin API에 제공된 추적 API가 여러 개 있습니다.](https://docs.adobe.com/content/help/en/mobile-services/ios/phonegap-ios/phonegap-methods.html)

사용자가 앱에서 탐색하는 페이지 위치, 가장 많이 사용되는 컨트롤 등과 같은 상태 및 작업을 추적할 수 있습니다. 추적을 위해 앱을 계측하는 가장 쉬운 방법은 AMS 플러그인에서 제공하는 Analytics API를 사용하는 것입니다.

* ADB.trackState()
* ADB.trackAction()

Geometrixx Outdoors 앱의 코드를 참조하십시오. Geometrixx Outdoors 앱에서 모든 페이지 탐색은 ADB.trackState() 메서드를 사용하여 추적됩니다. 자세한 내용은 /libs/mobileapps/components/angular/ng-page/clientlibs/app-navigation.js의 소스 코드를 참조하십시오.

이러한 메서드 호출을 사용하여 소스 코드를 구현함으로써 애플리케이션에 대해 전체 지표를 수집할 수 있습니다.

#### AMS에 연결하기 위한 속성 {#properties-for-connecting-to-ams}

*com.adobe.cq.mobile.mobileservices.impl.service.* MobileServicesHttpClientImpl은 AMS에 연결하기 위한 다음 속성을 표시합니다.

| **레이블** | **설명** | **기본값** |
|---|---|---|
| API 끝점 | Adobe Mobile Services HTTP API의 기본 URL | https://api.omniture.com |
| 구성 끝점 | 지정된 보고서 세트 ID에 대한 ADB 모바일 구성을 검색하는 데 사용되는 URL | /ams/1.0/app/config/ |
| 모바일 서비스 앱 | 사용자 회사 내의 앱 목록 가져오기 | /ams/1.0/apps |

