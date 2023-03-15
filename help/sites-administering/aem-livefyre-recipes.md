---
title: AEM Livefyre Recipes
seo-title: AEM Livefyre Recipes
description: Adobe Experience Manager Livefyre의 공통 사용 사례에 대한 단계별 지침입니다.
seo-description: Step-by-step instructions on common use cases for Adobe Experience Manager Livefyre.
uuid: 78695a63-fca6-4990-9755-0aeaae4a7f64
contentOwner: alba
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: fdea5ede-d44f-463e-af8a-111ee7469ede
exl-id: 7ccd67a7-9945-48c1-9986-f4eaf0f2b961
source-git-commit: 63f066013c34a5994e2c6a534d88db0c464cc905
workflow-type: tm+mt
source-wordcount: '1503'
ht-degree: 4%

---

# AEM Livefyre Recipes{#aem-livefyre-recipes}

Adobe Experience Manager Livefyre의 공통 사용 사례에 대한 단계별 지침입니다.

## 즉시 사용 가능한 Livefyre AEM 구성 요소를 사용하여 UGC를 큐레이션하고 Livefyre Media Wall을 사용하여 표시합니다. {#curate-ugc-using-the-out-of-the-box-livefyre-aem-components-and-display-using-livefyre-media-wall}

Media Wall은 소셜 및 기본 Livefyre 콘텐츠를 실시간 소셜 월로 스트리밍합니다. 사용 사례 및 요구 사항에 따라 AEM에서 Media Wall을 구현하는 방법은 여러 가지가 있습니다.

AEM Livefyre 패키지는 즉시 사용 가능한 구현을 제공하는 반면, 기존 통합은 사용자 지정 Livefyre AEM 구성 요소를 만드는 기능을 제공합니다.

### AEM 통합 {#aem-integration}

Livefyre Adobe Experience Manager 패키지는 AEM 6.1, 6.2 SP1, 6.3, 6.4 및 6.4 SP1에 사용할 수 있습니다. AEM 5.x 및 6.0은 지원되지 않습니다. 자세한 지침은 [Livefyre와 통합 사용](https://helpx.adobe.com/kr/experience-manager/6-4/sites/administering/using/livefyre.html).

지원되는 Livefyre 앱을 보려면 [Livefyre 앱용 AEM Support Matrix](https://helpx.adobe.com/experience-manager/6-3/sites/administering/using/livefyre.html#AEMSupportMatrixforLivefyreApps).

### 기존 구현(사용자 지정된 AEM 구성 요소의 경우) {#traditional-implementation-for-customized-aem-components}

Livefyre를 사용자 지정 AEM 구성 요소 또는 WordPress, Sitecore 또는 DemandWare와 같은 기타 CMS에 구현하는 방법에는 세 가지가 있습니다. 기존 Livefyre 통합은 CMS에 영향을 주지 않습니다.

**방법 1: Designer 앱 구현**

* **내용:** Livefyre 앱을 통합하는 가장 간단하고 빠른 방법입니다. 사용자 지정된 JavaScript 포함 코드를 디자인, 구성 및 생성하여 페이지에 Media Wall 앱을 몇 분 만에 통합할 수 있습니다.
* **방법:**  [Media Wall 앱 만들기, 미리보기, 게시 및 포함](https://experienceleague.adobe.com/docs/livefyre/using/apps/c-create-an-app.html)

* **예:** [https://codepen.io/dharafyre/pen/bvGrLo](https://codepen.io/dharafyre/pen/bvGrLo)

**방법 2: SDK 구현**

* **내용:** [Livefyre.js](https://experienceleague.adobe.com/docs/livefyre/implementation/c-livefyre_js.html) 는 사이트에서 앱 및 인증을 활성화하는 핵심 라이브러리입니다. 이는 전세계를 정의합니다 *window.Livefyre* 개체와 단일 공용 메서드, *Livefyre.require*: Livefyre 앱 임베드 및 타사 사용자 인증 플랫폼과의 통합을 지원하는 다른 Livefyre JavaScript 라이브러리를 로드하는 데 사용할 수 있습니다.

* **방법**: [Livefyre JavaScript SDK의 streamhub-wallpackage 사용](https://experienceleague.adobe.com/docs/livefyre/implementation/app-integrations/c-media-wall-integration.html)

* **예**: [https://codepen.io/dharafyre/pen/KZKBNv?editors=1010](https://codepen.io/dharafyre/pen/KZKBNv?editors=1010)

SDK를 사용한 고급 사용자 지정에 대해서는 다음을 참조하십시오. [StreamHub SDK](https://github.com/Livefyre/streamhub-sdk).

**방법 3: API 구현**

* 사용자 지정된 경험과 데이터 시각화를 만들기 위해 Livefyre 앱은 다음을 사용하여 Livefyre 및 소셜 데이터를 소모함으로써 처음부터 만들 수 있습니다. [Bootstrap 및 스트림 API](https://experienceleague.adobe.com/docs/livefyre/implementation/advanced-topics/bootstrap-stream-api.html).

다음을 따르세요 [Twitter](https://developer.twitter.com/en/developer-terms/display-requirements.html), [Facebook](https://en.facebookbrand.com/guidelines/brand), 및 [Instagram](https://en.instagram-brand.com/) ugc에 대한 UI를 작성할 때 지침을 표시합니다.

### Media Wall 인증 통합 {#media-wall-authentication-integration}

인증이 필요한 Media Wall 통합의 경우 다음을 참조하십시오.

* [단일 사인온 통합 사용자 지정](https://helpx.adobe.com/experience-manager/6-4/sites/administering/using/livefyre.html#CustomizeSingleSignonIntegration) AEM Identity Management용
* [ID 통합](https://experienceleague.adobe.com/docs/livefyre/implementation/identity-integration/t-about-identity-integration.html) 타사 인증 플랫폼용

### 사용 사례 개요 {#use-case-overview}

AEM 고객인 경우 기본 제공 Livefyre AEM 구성 요소를 사용하여 UGC를 큐레이션하고 Livefyre Media Wall을 사용하여 표시하려고 합니다.

구현 단계:

1. [시작하기](https://helpx.adobe.com/kr/experience-manager/6-3/sites/administering/using/livefyre.html)
1. [Livefyre를 사용하도록 AEM 구성](https://helpx.adobe.com/kr/experience-manager/6-3/sites/administering/using/livefyre.html)
1. [AEM Media Wall 구성 요소를 페이지로 끌어다 놓기](https://helpx.adobe.com/experience-manager/6-3/sites/administering/using/livefyre.html#UseLivefyrewithAEMSites)
1. [스트림을 구성하고 규칙을 추가하여 UGC를 조정하고 미디어 월 구성 요소에 표시합니다](https://experienceleague.adobe.com/docs/livefyre/using/streams/c-streams.html)

스트리밍 UGC에 대한 교육 비디오는 다음을 참조하십시오. [Adobe Experience Manager Livefyre에서 자동 컨텐츠 스트림 만들기 및 소셜 컨텐츠 검색](https://helpx.adobe.com/experience-manager/tutorials.html).

### 고객 예 {#customer-examples}

* [미디어 월](https://edition.cnn.com/specials/nepal-earthquake-media-wall)
* [투어 미디어 월](https://www.pgatour.com/social-hub.html)

사용자 지정된 경험과 데이터 시각화를 만들기 위해 Livefyre 앱은 다음을 사용하여 Livefyre 및 소셜 데이터를 소모함으로써 처음부터 만들 수 있습니다. [Bootstrap 및 스트림 API](https://experienceleague.adobe.com/docs/livefyre/implementation/advanced-topics/bootstrap-stream-api.html).

인증이 필요한 Livefyre 앱의 경우 다음을 참조하십시오. [ID 통합](https://experienceleague.adobe.com/docs/livefyre/implementation/identity-integration/t-about-identity-integration.html) 타사 인증 플랫폼용.

* [투어 미디어 월](https://www.pgatour.com/social-hub.html)
* [시간 초과](https://www.timeout.com/london/restaurants/forest-bar-kitchen#tab_panel_3)

## AEM 구성 요소 또는 기존 Livefyre 통합을 사용하여 Livefyre 주석 통합 {#integrate-livefyre-comments-using-aem-components-or-traditional-livefyre-integration}

### AEM 통합 {#aem-integration-1}

Livefyre Adobe Experience Manager 패키지는 AEM 6.1, 6.2 SP1, 6.3, 6.4 및 6.4 SP1에 사용할 수 있습니다. AEM 5.x 및 6.0은 지원되지 않습니다. 자세한 지침은 [Livefyre와 통합 사용](https://helpx.adobe.com/kr/experience-manager/6-4/sites/administering/using/livefyre.html).

### 기존 구현(사용자 지정된 AEM 구성 요소의 경우) {#traditional-implementation-for-customized-aem-components-1}

Livefyre 댓글 앱을 사용자 지정 AEM 구성 요소 또는 WordPress, Sitecore 또는 DemandWare와 같은 기타 CMS에 구현하는 방법에는 세 가지가 있습니다. 기존 Livefyre 통합은 CMS에 영향을 주지 않습니다.

**방법 1: Designer 앱 구현**

* **내용:** Livefyre 앱을 통합하는 가장 간단하고 빠른 방법입니다. 사용자 지정된 JavaScript 포함 코드를 디자인, 구성 및 생성하여 페이지에 Media Wall 앱을 몇 분 만에 통합할 수 있습니다.
* **방법:** [주석 앱 만들기, 미리 보기, 게시 및 포함](https://experienceleague.adobe.com/docs/livefyre/using/apps/c-create-an-app.html)

* **예:** [https://codepen.io/dharafyre/pen/oYoJdP](https://codepen.io/dharafyre/pen/oYoJdP)

**방법 2: SDK 구현**

* **내용:** [Livefyre.js](https://experienceleague.adobe.com/docs/livefyre/implementation/c-livefyre_js.html) 는 사이트에서 앱 및 인증을 활성화하는 핵심 라이브러리입니다. 이는 전세계를 정의합니다 *window.Livefyre* 개체와 단일 공용 메서드, *Livefyre.require*: Livefyre 앱 임베드 및 타사 사용자 인증 플랫폼과의 통합을 지원하는 다른 Livefyre JavaScript 라이브러리를 로드하는 데 사용할 수 있습니다.

* **방법:**

   * 다음을 사용하여 컬렉션/앱 만들기 [CollectionMeta 토큰](https://experienceleague.adobe.com/docs/livefyre/implementation/getting-started/implementation-process/c-collectionmeta-tokent.html).
   * 통합 [댓글 앱](https://experienceleague.adobe.com/docs/livefyre/implementation/app-integrations/comments/c-comments-integration.html) livefyre.js 포함 코드 구조를 사용하는 사이트에 로그인합니다.

* **예:**  [https://codepen.io/dharafyre/pen/oYoJdP](https://codepen.io/dharafyre/pen/oYoJdP)

SDK를 사용한 고급 사용자 지정에 대해서는 다음을 참조하십시오. [StreamHub SDK](https://github.com/Livefyre/streamhub-sdk).

**방법 3: API 구현**

* 사용자 지정된 경험과 데이터 시각화를 만들기 위해 Livefyre 앱은 다음을 사용하여 Livefyre 및 소셜 데이터를 소모함으로써 처음부터 만들 수 있습니다. [Bootstrap 및 스트림 API](https://experienceleague.adobe.com/docs/livefyre/implementation/advanced-topics/bootstrap-stream-api.html).

### 댓글 앱 인증 통합 {#comments-app-authentication-integration}

* [단일 사인온 통합 사용자 지정](https://helpx.adobe.com/experience-manager/6-4/sites/administering/using/livefyre.html#CustomizeSingleSignonIntegration) AEM Identity Management용
* [ID 통합](https://experienceleague.adobe.com/docs/livefyre/implementation/identity-integration/t-about-identity-integration.html) 타사 인증 플랫폼용

### 고객 예 {#customer-examples-1}

* [푸아즈(킴벌리 클라크)](https://www.poise.com/en-us/advice-and-support/blog-and-podcast/blog/5-holiday-party-tips-for-managing-lbl)

## Livefyre AEM Assets 통합을 사용하여 AEM Assets에서 UGC를 가져옵니다 {#use-livefyre-aem-assets-integration-to-import-ugc-in-aem-assets}

**Livefyre 설정(UGC 큐레이션 및 Rights Management):**

1. [Livefyre 자산 라이브러리 폴더에 UGC를 조정하기 위해 스트림 구성 및 규칙 추가](https://experienceleague.adobe.com/docs/livefyre/using/streams/c-streams.html).

   1. 스트리밍 UGC에 대한 교육 비디오는 다음을 참조하십시오. [Adobe Experience Manager Livefyre에서 자동 컨텐츠 스트림 만들기 및 소셜 컨텐츠 검색](https://helpx.adobe.com/experience-manager/tutorials.html).

1. [Livefyre 자산 라이브러리 폴더에서 엄선된 UGC를 수집, 구성 및 관리합니다.](https://experienceleague.adobe.com/docs/livefyre/using/library/assets/c-assets.html).

   1. Livefyre Studio 자산 라이브러리에서 폴더를 만들고 관리하는 방법에 대한 교육 비디오는 를 참조하십시오. [Adobe Experience Manager Livefyre에서 에셋으로 작업](https://helpx.adobe.com/experience-manager/tutorials.html).

1. [Livefyre Studio를 사용하여 조정된 UGC에 대한 권한 요청](https://experienceleague.adobe.com/docs/livefyre/using/rights-requests/c-how-requesting-rights-works.html).

**AEM 설정(UGC를 AEM Assets으로 가져오는 경우):**

1. [시작하기](https://helpx.adobe.com/experience-manager/6-3/sites/administering/using/livefyre.html#GettingStarted)
1. [Livefyre를 사용하도록 AEM 구성](https://helpx.adobe.com/experience-manager/6-3/sites/administering/using/livefyre.html#ConfigureAEMtouseLivefyre)
1. [Livefyre에서 큐레이션한 UGC를 AEM Assets으로 가져오기](https://helpx.adobe.com/experience-manager/6-3/sites/administering/using/livefyre.html#UseLivefyrewithAEMAssets)

* [호주정부관광청](https://www.australia.com/en-us)

## AEM 구성 요소 또는 기존 Livefyre 통합을 사용하여 Livefyre 리뷰 통합 {#integrate-livefyre-reviews-using-aem-components-or-traditional-livefyre-integration}

### AEM 통합 {#aem-integration-2}

Livefyre Adobe Experience Manager 패키지는 AEM 6.1, 6.2 SP1, 6.3, 6.4 및 6.4 SP1에 사용할 수 있습니다. AEM 5.x 및 6.0은 지원되지 않습니다. 자세한 지침은 [Livefyre와 통합 사용](https://helpx.adobe.com/kr/experience-manager/6-4/sites/administering/using/livefyre.html).

리뷰 구성 요소는 AEM 6.1에서 지원되는 구성 요소가 아닙니다. 다음을 확인하십시오. [모든 Livefyre 앱에 대한 AEM 지원 매트릭스](https://helpx.adobe.com/experience-manager/6-3/sites/administering/using/livefyre.html#AEMSupportMatrixforLivefyreApps).

### 기존 구현(사용자 지정된 AEM 구성 요소의 경우) {#traditional-implementation-for-customized-aem-components-2}

두 가지 방법으로 Livefyre 리뷰 앱을 사용자 지정 AEM 구성 요소나 WordPress, Sitecore 또는 DemandWare와 같은 기타 CMS에 구현할 수 있습니다. 기존 Livefyre 통합은 CMS에 영향을 주지 않습니다.

**방법 1: SDK 구현**

* **내용:** [Livefyre.js](https://experienceleague.adobe.com/docs/livefyre/implementation/c-livefyre_js.html) 는 사이트에서 앱 및 인증을 활성화하는 핵심 라이브러리입니다. 이는 전세계를 정의합니다 *window.Livefyre* 개체와 단일 공용 메서드, *Livefyre.require*: Livefyre 앱 임베드 및 타사 사용자 인증 플랫폼과의 통합을 지원하는 다른 Livefyre JavaScript 라이브러리를 로드하는 데 사용할 수 있습니다.

* **방법:**

   * 리뷰 만들기 [CollectionMeta 토큰](https://experienceleague.adobe.com/docs/livefyre/implementation/app-integrations/c-reviews-integration.html) 리뷰 컬렉션 내에 저장할 메타데이터를 지정합니다.
   * 통합 [리뷰 앱](https://experienceleague.adobe.com/docs/livefyre/implementation/app-integrations/c-reviews-integration.html) 를 사용하여 사이트에 *Livefyre.js* 포함 코드 구조

* **예:**  [https://codepen.io/dharafyre/pen/GXgvvd](https://codepen.io/dharafyre/pen/GXgvvd)

SDK를 사용한 고급 사용자 지정에 대해서는 다음을 참조하십시오. [StreamHub SDK](https://github.com/Livefyre/streamhub-sdk).

**방법 2: API 구현**

* 사용자 지정된 경험과 데이터 시각화를 만들기 위해 Livefyre 앱은 Bootstrap 및 스트림 API를 사용하여 Livefyre 및 소셜 데이터를 소모함으로써 처음부터 만들 수 있습니다.

추가 평점 및 리뷰 API를 찾을 수 있습니다. [여기](https://api.livefyre.com/docs/apis/by-category/ratings-and-reviews).

### 댓글 앱 인증 통합 {#comments-app-authentication-integration-1}

* [단일 사인온 통합 사용자 지정](https://helpx.adobe.com/experience-manager/6-4/sites/administering/using/livefyre.html#CustomizeSingleSignonIntegration) AEM Identity Management용
* [ID 통합](https://experienceleague.adobe.com/docs/livefyre/implementation/identity-integration/t-about-identity-integration.html) 타사 인증 플랫폼용

### 고객 예 {#customer-examples-2}

* [시간 초과](https://www.timeout.com/london/restaurants/forest-bar-kitchen#tab_panel_3)
* [내 레시피](https://www.myrecipes.com/recipe/shrimp-florentine-pasta)
