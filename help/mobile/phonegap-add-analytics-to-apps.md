---
title: 모바일 애플리케이션에 Adobe Analytics 추가
description: 이 페이지를 따라 Mobile Services와 통합하여 Adobe Experience Manager Adobe 앱에서 Mobile App Analytics를 사용하는 방법에 대해 알아보십시오.
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
exl-id: 8d965e94-c368-481d-b000-6e22456c34db
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '932'
ht-degree: 0%

---

# 모바일 애플리케이션에 Adobe Analytics 추가{#add-adobe-analytics-to-your-mobile-application}

>[!NOTE]
>
>Adobe 단일 페이지 애플리케이션 프레임워크 기반 클라이언트측 렌더링(예: React)이 필요한 프로젝트에는 SPA Editor를 사용하는 것이 좋습니다. [자세히 알아보기](/help/sites-developing/spa-overview.md).

모바일 애플리케이션 사용자를 위한 매력적이고 적절한 경험을 구축하시겠습니까? Adobe Mobile Services SDK를 사용하여 애플리케이션 라이프사이클과 사용량을 모니터링하고 측정하지 않는 경우 의사 결정의 기준은 무엇입니까? 가장 단골 고객은 어디입니까? 관련성이 있고 전환을 최적화하고 있다고 어떻게 보증할 수 있습니까?

사용자가 모든 콘텐츠에 액세스하고 있습니까? 앱을 포기하는 것이며, 포기하는 경우 어디에 있습니까? 얼마나 자주 앱에 머무르며 앱을 사용하기 위해 다시 방문합니까? 어떤 변경 사항을 적용한 다음 이를 측정하여 보존을 늘릴 수 있습니까? 충돌 비율은 어떻습니까? 사용자들에게 앱이 충돌하고 있습니까?

활용 [모바일 앱 분석](https://business.adobe.com/products/analytics/mobile-marketing.html) 를 사용하여 Adobe Experience Manager(AEM) 앱에서 [Adobe Mobile Services](https://business.adobe.com/products/campaign/mobile-marketing.html).

AEM 앱을 활용하여 사용자가 모바일 앱 및 콘텐츠에 어떻게 참여하는지를 추적, 보고 및 파악하고, 시작, 앱 내 시간 및 충돌률과 같은 주요 라이프사이클 지표를 측정합니다.

이 섹션에서는 AEM에 대해 설명합니다 *개발자* 다음을 수행할 수 있습니다.

* 모바일 애플리케이션에 Mobile Analytics 통합
* Bloodhound를 사용하여 분석 추적 테스트

## 사전 요구 사항 {#prerequisties}

AEM Mobile에서는 앱에서 추적 데이터를 수집하고 보고하려면 Adobe Analytics 계정이 필요합니다. 구성의 일부로 AEM *관리자* 다음을 먼저 수행해야 합니다.

* Mobile Services에서 Adobe Analytics 계정을 설정하고 애플리케이션에 대한 보고서 세트를 만듭니다.
* AEM(Adobe Experience Manager)에서 AMS Cloud Service을 구성합니다.

## 개발자용 - Mobile Analytics를 앱에 통합 {#for-developers-integrate-mobile-analytics-into-your-app}

### 구성 파일을 가져오도록 ContentSync 구성 {#configure-contentsync-to-pull-in-configuration-file}

Analytics 계정이 설정되면 콘텐츠 동기화 구성을 만들어 콘텐츠를 모바일 애플리케이션으로 가져옵니다.

자세한 내용은 콘텐츠 동기화 콘텐츠 구성 을 참조하십시오. ADBMobileConfig를 /www 디렉터리에 넣으려면 Content Sync에 지시해야 합니다. 예를 들어 Geometrixx Outdoors 앱에서 컨텐츠 동기화 구성은 다음 위치에 있습니다. */content/phonegap/geometrixx-outdoors/shell/jcr:content/pge-app/app-config/ams-ADBMobileConfig*. 개발에 대한 구성도 있지만, Geometrixx Outdoors의 경우 비개발 구성과 동일합니다.

모바일 애플리케이션 AEM 앱 대시보드에서 ADBMobileConfig를 다운로드하는 방법에 대한 자세한 내용은 Analytics - Mobile Services - Adobe Mobile Services SDK 구성 파일을 참조하십시오.

```xml
<jcr:root xmlns:jcr="https://www.jcp.org/jcr/1.0" xmlns:nt="https://www.jcp.org/jcr/nt/1.0"
    jcr:primaryType="nt:unstructured"
    extension="json"
    path="../../../.."
    selector="ADBMobileConfig"
    targetRootDirectory="www"
    type="mobileADBMobileConfigJSON"/>
```

각 플랫폼에서는 ADBMobileConfig를 특정 위치에 복사해야 합니다.

PhoneGap CLI를 사용하여 빌드하는 경우 cordova 빌드 후크 스크립트를 사용하여 이 작업을 수행할 수 있습니다. 이 기능은 Geometrixx Outdoors 앱의 다음 위치에서 볼 수 있습니다.*content/phonegap/geometrixx-outdoors/shell/_jcr_content/pge-app/app-content/phonegap/scripts/restore_plugins.js입니다.*

iOS의 경우 파일을 XCode 프로젝트의 **리소스** 디렉터리(예: &quot;platforms/ios/Geometrixx/Resources/ADBMobileConfig.json&quot;). 앱이 Android™용으로 타깃팅된 경우 복사할 경로는 &quot;platforms/android/assets/ADBMobileConfig.json&quot;입니다. PhoneGap CLI 빌드 중에 후크를 사용하는 방법에 대한 자세한 내용은 [Cordova/PhoneGap 프로젝트에 필요한 3개의 후크](https://gist.github.com/jlcarvalho/22402d013bc72f795d45a01836ce735c).

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

### 앱에 AMS 플러그인 추가 {#add-the-ams-plugin-in-the-app}

앱이 데이터를 수집하려면 Adobe Mobile Services(AMS) 플러그인을 앱의 일부로 포함해야 합니다. 플러그인을 앱의 config.xml에 기능으로 포함시키면 PhoneGap Build 프로세스 중에 다른 Cordova 후크를 사용하여 플러그인을 자동으로 추가할 수 있습니다.

```xml
<feature name="ADBMobile">
    <param name="id" value="https://github.com/Adobe-Marketing-Cloud/mobile-services#0482f9cedf90c98a8d4b07219ece1933b2e46a60"/>
</feature>
```

Geometrixx Outdoors 앱 config.xml은에 있습니다. */content/phonegap/geometrixx-outdoors/shell/jcr:content/pge-app/app-content/phonegap/www/config.xml*. 위의 예에서는 플러그인 URL 뒤에 &#39;#&#39;를 추가한 다음 태그 값을 추가하여 사용할 플러그인의 특정 버전을 요청합니다. 빌드 중에 테스트되지 않은 플러그인이 추가되어 예상치 못한 문제가 발생하지 않도록 하기 위해 따라야 할 좋은 방법입니다.

이 단계를 수행하면 앱에서 Adobe Analytics이 제공하는 모든 라이프사이클 지표를 보고할 수 있습니다. 여기에는 실행, 충돌 및 설치와 같은 데이터가 포함됩니다. 중요한 데이터가 그것뿐이라면 완료됩니다. 사용자 지정 데이터를 수집하려면 코드를 계측해야 합니다.

### 전체 앱 추적을 위해 코드 계측 {#instrument-your-code-for-full-app-tracking}

에는 몇 가지 추적 API가 제공됩니다. [AMS Phonegap 플러그인 API.](https://github.com/Adobe-Marketing-Cloud/mobile-services/blob/master/docs/ios/phonegap/phonegap-methods.md)

이를 통해 사용자가 앱에서 탐색하는 페이지, 즉 가장 많이 사용되는 컨트롤과 같은 상태 및 작업을 추적할 수 있습니다. 앱을 추적하기 위해 계측하는 가장 쉬운 방법은 AMS 플러그인이 제공하는 Analytics API를 사용하는 것입니다.

* ADB.trackState()
* ADB.trackAction()

참조용으로 Geometrixx Outdoors 앱의 코드를 참조하십시오. Geometrixx Outdoors 앱에서 모든 페이지 탐색은 ADB.trackState() 메서드를 사용하여 추적됩니다. 자세한 내용은 /libs/mobileapps/components/angular/ng-page/clientlibs/app-navigation.js의 소스 코드를 참조하십시오.

이 메서드 호출을 사용하여 소스 코드를 계측하면 애플리케이션에 대한 전체 지표를 수집할 수 있습니다.

#### AMS에 연결하기 위한 속성 {#properties-for-connecting-to-ams}

*com.adobe.cq.mobile.mobileservices.impl.service.MobileServicesHttpClientImp* l은 AMS에 연결하기 위해 다음 속성을 노출합니다.

| **레이블** | **설명** | **기본값** |
|---|---|---|
| API 엔드포인트 | Adobe Mobile Services HTTP API의 기본 URL | https://api.omniture.com |
| 구성 엔드포인트 | 지정된 보고서 세트 ID에 대한 ADB 모바일 구성을 검색하는 데 사용되는 URL | /ams/1.0/app/config/ |
| 모바일 서비스 앱 | 사용자 회사 내 앱 목록 가져오기 | /ams/1.0/apps |
