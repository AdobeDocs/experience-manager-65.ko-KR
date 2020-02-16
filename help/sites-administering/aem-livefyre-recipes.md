---
title: AEM Livefyre 레서피
seo-title: AEM Livefyre 레서피
description: Adobe Experience Manager Livefyre의 일반적인 사용 사례에 대한 단계별 지침
seo-description: Adobe Experience Manager Livefyre의 일반적인 사용 사례에 대한 단계별 지침
uuid: 78695a63-fca6-4990-9755-0aeaae4a7f64
contentOwner: alba
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: fdea5ede-d44f-463e-af8a-111ee7469ede
translation-type: tm+mt
source-git-commit: 5128a08d4db21cda821de0698b0ac63ceed24379

---


# AEM Livefyre 레서피{#aem-livefyre-recipes}

Adobe Experience Manager Livefyre의 일반적인 사용 사례에 대한 단계별 지침

## 기본 Livefyre AEM 구성 요소를 사용하여 UGC를 조정하고 Livefyre 미디어 벽을 사용하여 표시 {#curate-ugc-using-the-out-of-the-box-livefyre-aem-components-and-display-using-livefyre-media-wall}

Media Wall은 소셜 및 기본 Livefyre 컨텐츠를 실시간 소셜 담벼락에 스트리밍합니다. 사용 사례와 요구 사항에 따라 AEM에서 미디어 장벽을 구현하는 방법은 여러 가지가 있습니다.

AEM Livefyre 패키지는 기본적으로 구현되는 반면 기존 통합은 사용자 정의 Livefyre AEM 구성 요소를 만드는 기능을 제공합니다.

### AEM 통합 {#aem-integration}

Livefyre Adobe Experience Manager 패키지는 AEM 6.1, 6.2SP1, 6.3, 6.4 및 6.4 SP1에서 사용할 수 있습니다. AEM 5.x 및 6.0은 지원되지 않습니다. 자세한 지침은 Livefyre와 [통합을 참조하십시오](https://helpx.adobe.com/experience-manager/6-4/sites/administering/using/livefyre.html).

지원되는 Livefyre 앱을 확인하려면 Livefyre 앱용 [AEM Support Matrix를 참조하십시오](https://helpx.adobe.com/experience-manager/6-3/sites/administering/using/livefyre.html#AEMSupportMatrixforLivefyreApps).

### 기존 구현(사용자 정의된 AEM 구성 요소의 경우) {#traditional-implementation-for-customized-aem-components}

Livefyre를 사용자 정의 AEM 구성 요소나 WordPress, Sitecore 또는 DemandWare와 같은 다른 CMS에 구현하는 방법에는 세 가지가 있습니다. 기존의 Livefyre 통합은 CMS에 상관없이 가능합니다.

**방법 1:디자이너 앱 구현**

* **** 소개:Livefyre 앱을 가장 간단하고 신속하게 통합하는 방법 사용자 정의된 JavaScript 포함 코드를 디자인, 구성 및 생성하여 페이지에 Media Wall App을 몇 분 내에 통합할 수 있습니다.
* **** 방법: Media [Wall 앱 만들기, 미리 보기, 게시 및 포함](https://marketing.adobe.com/resources/help/en_US/livefyre/c_create_an_app.html)

* **** 예: [https://codepen.io/dharafyre/pen/bvGrLo](https://codepen.io/dharafyre/pen/bvGrLo)

**방법 2:SDK 구현**

* **** 소개:Livefyre.js [는](https://marketing.adobe.com/resources/help/en_US/livefyre/c_livefyre.js.html) 사이트에서 Apps 및 Auth를 지원하는 핵심 라이브러리입니다. 전역 *창을 정의합니다.Livefyre* 개체와 단일 공개 방법인 *Livefyre.require를*&#x200B;사용하여 Livefyre 앱 임베드 및 타사 사용자 인증 플랫폼과의 통합에 도움이 되는 다른 Livefyre JavaScript 라이브러리를 로드하는 데 사용할 수 있습니다.

* **방법**:Livefyre [JavaScript SDK의 streamhub-walpackage 사용](https://marketing.adobe.com/resources/help/en_US/livefyre/?f=c_media_wall_app&s=c_media_wall_integration)

* **예**: [https://codepen.io/dharafyre/pen/KZKBNv?editors=1010](https://codepen.io/dharafyre/pen/KZKBNv?editors=1010)

SDK를 사용한 고급 사용자 정의는 StreamHub SDK를 [참조하십시오](https://github.com/Livefyre/streamhub-sdk).

**방법 3:API 구현**

* 사용자 정의된 경험과 데이터 시각화를 만들기 위해 Bootstrap 및 스트림 API를 사용하여 Livefyre 및 소셜 데이터를 사용하여 Livefyre 앱을 처음부터 만들 [수 있습니다](https://marketing.adobe.com/resources/help/en_US/livefyre/bootstrap-stream-api.html).

UGC용 UI [를](https://developer.twitter.com/en/developer-terms/display-requirements.html)만들 때 Twitter [,](https://en.facebookbrand.com/guidelines/brand)Facebook [및 Instagram](https://en.instagram-brand.com/) 표시 지침을 따라야 합니다.

### Media Wall 인증 통합 {#media-wall-authentication-integration}

인증이 필요한 Media Wall 통합은 다음을 참조하십시오.

* [AEM Identity Management에 대한](https://helpx.adobe.com/experience-manager/6-4/sites/administering/using/livefyre.html#CustomizeSingleSignonIntegration) Single Sign On 통합 사용자 정의
* [타사 인증](https://marketing.adobe.com/resources/help/en_US/livefyre/t_about_identity_integration.html) 플랫폼을 위한 ID 통합

### 사용 사례 개요 {#use-case-overview}

AEM 고객인 경우 즉시 사용 가능한 Livefyre AEM 구성 요소를 사용하여 UGC를 조정하고 Livefyre Media Wall을 사용하여 표시하고자 합니다.

구현 단계:

1. [시작하기](https://helpx.adobe.com/experience-manager/6-3/sites/administering/using/livefyre.html)
1. [Livefyre를 사용하도록 AEM 구성](https://helpx.adobe.com/experience-manager/6-3/sites/administering/using/livefyre.html)
1. [AEM Media Wall 구성 요소를 페이지에 드래그하여 놓기](https://helpx.adobe.com/experience-manager/6-3/sites/administering/using/livefyre.html#UseLivefyrewithAEMSites)
1. [스트림 구성 및 규칙을 추가하여 UGC를 조정하고 Media Wall 구성 요소에 표시](https://marketing.adobe.com/resources/help/en_US/livefyre/c_streams.html)

스트리밍 UGC에 대한 교육 비디오는 Adobe Experience [Manager Livefyre에서 자동 콘텐츠 스트림 만들기 및 소셜 콘텐츠 검색을 참조하십시오](https://helpx.adobe.com/experience-manager/tutorials.html).

### 고객 사례 {#customer-examples}

* [CNN Media Wall](https://edition.cnn.com/specials/nepal-earthquake-media-wall)
* [PGA Tour Media Wall](https://www.pgatour.com/social-hub.html)

사용자 정의된 경험과 데이터 시각화를 만들기 위해 Bootstrap 및 스트림 API를 사용하여 Livefyre 및 소셜 데이터를 사용하여 Livefyre 앱을 처음부터 만들 [수 있습니다](https://marketing.adobe.com/resources/help/en_US/livefyre/bootstrap-stream-api.html).

인증이 필요한 Livefyre 앱의 경우 타사 인증 [플랫폼용](https://marketing.adobe.com/resources/help/en_US/livefyre/t_about_identity_integration.html) ID 통합을 참조하십시오.

* [PGA Tour Media Wall](https://www.pgatour.com/social-hub.html)
* [시간 초과](https://www.timeout.com/london/restaurants/forest-bar-kitchen#tab_panel_3)

## AEM 구성 요소 또는 기존 Livefyre 통합을 사용하여 Livefyre 주석 통합 {#integrate-livefyre-comments-using-aem-components-or-traditional-livefyre-integration}

### AEM 통합 {#aem-integration-1}

Livefyre Adobe Experience Manager 패키지는 AEM 6.1, 6.2SP1, 6.3, 6.4 및 6.4 SP1에서 사용할 수 있습니다. AEM 5.x 및 6.0은 지원되지 않습니다. 자세한 지침은 Livefyre와 [통합을 참조하십시오](https://helpx.adobe.com/experience-manager/6-4/sites/administering/using/livefyre.html).

### 기존 구현(사용자 정의된 AEM 구성 요소의 경우) {#traditional-implementation-for-customized-aem-components-1}

Livefyre 댓글 앱을 사용자 지정 AEM 구성 요소나 WordPress, Sitecore 또는 DemandWare와 같은 다른 CMS에 구현하는 방법에는 세 가지가 있습니다. 기존의 Livefyre 통합은 CMS에 상관없이 가능합니다.

**방법 1:디자이너 앱 구현**

* **** 소개:Livefyre 앱을 가장 간단하고 신속하게 통합하는 방법 사용자 정의된 JavaScript 포함 코드를 디자인, 구성 및 생성하여 페이지에 Media Wall App을 몇 분 내에 통합할 수 있습니다.
* **** 방법:주석 [앱 만들기, 미리 보기, 게시 및 포함](https://marketing.adobe.com/resources/help/en_US/livefyre/c_create_an_app.html)

* **** 예: [https://codepen.io/dharafyre/pen/oYoJdP](https://codepen.io/dharafyre/pen/oYoJdP)

**방법 2:SDK 구현**

* **** 소개:Livefyre.js [는](https://marketing.adobe.com/resources/help/en_US/livefyre/c_livefyre.js.html) 사이트에서 Apps 및 Auth를 지원하는 핵심 라이브러리입니다. 전역 *창을 정의합니다.Livefyre* 개체와 단일 공개 방법인 *Livefyre.require를*&#x200B;사용하여 Livefyre 앱 임베드 및 타사 사용자 인증 플랫폼과의 통합에 도움이 되는 다른 Livefyre JavaScript 라이브러리를 로드하는 데 사용할 수 있습니다.

* **방법:**

   * CollectionMeta 토큰을 사용하여 컬렉션/ [앱을 만듭니다](https://marketing.adobe.com/resources/help/en_US/livefyre/t_create_a_collectionmeta_token.html).
   * Livefyre [](https://marketing.adobe.com/resources/help/en_US/livefyre/c_comments_integration.html) .js 임베드 코드 구조를 사용하여 사이트에 주석 앱을 통합합니다.

* **** 예: [https://codepen.io/dharafyre/pen/oYoJdP](https://codepen.io/dharafyre/pen/oYoJdP)

SDK를 사용한 고급 사용자 지정에 대해서는 StreamHub [SDK를 참조하십시오](https://github.com/Livefyre/streamhub-sdk).

**방법 3:API 구현**

* 사용자 정의된 경험과 데이터 시각화를 만들기 위해 Bootstrap 및 스트림 API를 사용하여 Livefyre 및 소셜 데이터를 사용하여 Livefyre 앱을 처음부터 만들 [수 있습니다](https://marketing.adobe.com/resources/help/en_US/livefyre/bootstrap-stream-api.html).

### 댓글 앱 인증 통합 {#comments-app-authentication-integration}

* [AEM Identity Management에 대한](https://helpx.adobe.com/experience-manager/6-4/sites/administering/using/livefyre.html#CustomizeSingleSignonIntegration) Single Sign On 통합 사용자 정의
* [타사 인증](https://marketing.adobe.com/resources/help/en_US/livefyre/t_about_identity_integration.html) 플랫폼을 위한 ID 통합

### 고객 사례 {#customer-examples-1}

* [푸아즈(킴벌리 클라크)](https://www.poise.com/en-us/advice-and-support/blog-and-podcast/blog/5-holiday-party-tips-for-managing-lbl)

## Livefyre AEM Assets 통합을 사용하여 AEM Assets에서 UGC를 가져옵니다. {#use-livefyre-aem-assets-integration-to-import-ugc-in-aem-assets}

**Livefyre 설정(UGC 조정 및 권한 관리용):**

1. [Livefyre 자산 라이브러리 폴더에 UGC를 조정하기 위한 [스트림 구성] 및 [규칙 추가]](https://marketing.adobe.com/resources/help/en_US/livefyre/c_streams.html).

   1. 스트리밍 UGC에 대한 교육 비디오는 Adobe Experience [Manager Livefyre에서 자동 콘텐츠 스트림 만들기 및 소셜 콘텐츠 검색을 참조하십시오](https://helpx.adobe.com/experience-manager/tutorials.html).

1. [Livefyre 자산 라이브러리 폴더에서](https://marketing.adobe.com/resources/help/en_US/livefyre/c_assets.html)선별된 UGC를 수집, 구성 및 관리합니다.

   1. Livefyre Studio 에셋 라이브러리에서 폴더 만들기 및 관리에 대한 교육 비디오는 Adobe Experience Manager Livefyre [에서 에셋을 사용한 작업을 참조하십시오](https://helpx.adobe.com/experience-manager/tutorials.html).

1. [Livefyre Studio를 사용하여 선별된 UGC에 대한 권한 요청](https://marketing.adobe.com/resources/help/en_US/livefyre/c_how_requesting_rights_works.html).

**AEM 설정(AEM 자산에 UGC를 가져오는 경우):**

1. [시작하기](https://helpx.adobe.com/experience-manager/6-3/sites/administering/using/livefyre.html#GettingStarted)
1. [Livefyre를 사용하도록 AEM 구성](https://helpx.adobe.com/experience-manager/6-3/sites/administering/using/livefyre.html#ConfigureAEMtouseLivefyre)
1. [AEM 자산에 Livefyre로 조정된 UGC 가져오기](https://helpx.adobe.com/experience-manager/6-3/sites/administering/using/livefyre.html#UseLivefyrewithAEMAssets)

* [Tourism Australia](https://www.australia.com/en-us)

## AEM 구성 요소 또는 기존 Livefyre 통합을 사용하여 Livefyre 검토 통합 {#integrate-livefyre-reviews-using-aem-components-or-traditional-livefyre-integration}

### AEM 통합 {#aem-integration-2}

Livefyre Adobe Experience Manager 패키지는 AEM 6.1, 6.2SP1, 6.3, 6.4 및 6.4 SP1에서 사용할 수 있습니다. AEM 5.x 및 6.0은 지원되지 않습니다. 자세한 지침은 Livefyre와 [통합을 참조하십시오](https://helpx.adobe.com/experience-manager/6-4/sites/administering/using/livefyre.html).

검토 구성 요소는 AEM 6.1에서 지원되지 않습니다.모든 Livefyre 앱에 [대한 AEM 지원 매트릭스를 확인하십시오](https://helpx.adobe.com/experience-manager/6-3/sites/administering/using/livefyre.html#AEMSupportMatrixforLivefyreApps).

### 기존 구현(사용자 정의된 AEM 구성 요소의 경우) {#traditional-implementation-for-customized-aem-components-2}

Livefyre 평가 앱을 사용자 지정 AEM 구성 요소나 WordPress, Sitecore 또는 DemandWare와 같은 다른 CMS에 구현하는 방법에는 두 가지가 있습니다. 기존의 Livefyre 통합은 CMS에 상관없이 가능합니다.

**방법 1:SDK 구현**

* **** 소개:Livefyre.js [는](https://marketing.adobe.com/resources/help/en_US/livefyre/c_livefyre.js.html) 사이트에서 Apps 및 Auth를 지원하는 핵심 라이브러리입니다. 전역 *창을 정의합니다.Livefyre* 개체와 단일 공개 방법인 *Livefyre.require를*&#x200B;사용하여 Livefyre 앱 임베드 및 타사 사용자 인증 플랫폼과의 통합에 도움이 되는 다른 Livefyre JavaScript 라이브러리를 로드하는 데 사용할 수 있습니다.

* **방법:**

   * Reviews CollectionMeta [토큰을](https://marketing.adobe.com/resources/help/en_US/livefyre/c_reviews_integration.html) 만들어 검토 컬렉션 내에 저장할 메타데이터를 지정합니다.
   * Livefyre [.js 임베드 코드 구조를 사용하여](https://marketing.adobe.com/resources/help/en_US/livefyre/c_reviews_integration.html) 검토 앱을 ** 사이트에 통합

* **** 예: [https://codepen.io/dharafyre/pen/GXgvvd](https://codepen.io/dharafyre/pen/GXgvvd)

SDK를 사용한 고급 사용자 지정에 대해서는 StreamHub [SDK를 참조하십시오](https://github.com/Livefyre/streamhub-sdk).

**방법 2:API 구현**

* 사용자 정의된 경험과 데이터 시각화를 만들기 위해 Bootstrap 및 스트림 API를 사용하여 Livefyre 및 소셜 데이터를 사용함으로써 Livefyre 앱을 처음부터 만들 수 있습니다.

추가 등급 및 평가 API는 [여기에서](https://api.livefyre.com/docs/apis/by-category/ratings-and-reviews)찾을 수 있습니다.

### 댓글 앱 인증 통합 {#comments-app-authentication-integration-1}

* [AEM Identity Management에 대한](https://helpx.adobe.com/experience-manager/6-4/sites/administering/using/livefyre.html#CustomizeSingleSignonIntegration) Single Sign On 통합 사용자 정의
* [타사 인증](https://marketing.adobe.com/resources/help/en_US/livefyre/t_about_identity_integration.html) 플랫폼을 위한 ID 통합

### 고객 사례 {#customer-examples-2}

* [시간 초과](https://www.timeout.com/london/restaurants/forest-bar-kitchen#tab_panel_3)
* [myrecipes](https://www.myrecipes.com/recipe/shrimp-florentine-pasta)

