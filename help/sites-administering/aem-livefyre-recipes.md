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
source-git-commit: 072898f18d418eac8e9d9e94453db34d62dd3ed9
workflow-type: tm+mt
source-wordcount: '1559'
ht-degree: 2%

---


# AEM Livefyre 레서피{#aem-livefyre-recipes}

Adobe Experience Manager Livefyre의 일반적인 사용 사례에 대한 단계별 지침

## 즉시 사용 가능한 Livefyre AEM 구성 요소를 사용하여 UGC를 선별하고 Livefyre 미디어 장벽 {#curate-ugc-using-the-out-of-the-box-livefyre-aem-components-and-display-using-livefyre-media-wall} 을 사용하여 표시

Media Wall은 소셜 및 기본 Livefyre 컨텐츠를 실시간 소셜 담벼락에 스트리밍합니다. 사용 사례와 요구 사항에 따라 AEM에서 미디어 월을 구현하는 방법에는 여러 가지가 있습니다.

AEM Livefyre 패키지는 기본적으로 구현되는 반면, 기존 통합은 사용자 정의 Livefyre AEM 구성 요소를 만드는 기능을 제공합니다.

### AEM 통합 {#aem-integration}

Livefyre Adobe Experience Manager 패키지는 AEM 6.1, 6.2SP1, 6.3, 6.4 및 6.4 SP1에서 사용할 수 있습니다. AEM 5.x 및 6.0은 지원되지 않습니다. 자세한 지침은 [Livefyre](https://helpx.adobe.com/kr/experience-manager/6-4/sites/administering/using/livefyre.html)와 통합을 참조하십시오.

지원되는 Livefyre 앱을 확인하려면 [AEM Support Matrix for Livefyre 앱](https://helpx.adobe.com/experience-manager/6-3/sites/administering/using/livefyre.html#AEMSupportMatrixforLivefyreApps)을 참조하십시오.

### 기존 구현(사용자 지정된 AEM 구성 요소의 경우) {#traditional-implementation-for-customized-aem-components}

Livefyre를 사용자 정의 AEM 구성 요소 또는 WordPress, Sitecore 또는 DemandWare와 같은 다른 CMS에 구현하는 3가지 방법이 있습니다. 기존의 Livefyre 통합은 CMS에 관계 없음

**방법 1:디자이너 앱 구현**

* **what:** Livefyre 앱을 가장 간단하고 신속하게 통합하는 방법 페이지에 미디어 담벼락 앱을 통합하기 위해 사용자 정의된 JavaScript 포함 코드를 디자인, 구성 및 생성할 수 있습니다.
* **방법:**  [미디어 담벼락 앱 만들기, 미리 보기, 게시 및 포함](https://docs.adobe.com/content/help/en/livefyre/using/apps/c-create-an-app.html)

* **예:** [https://codepen.io/dharafyre/pen/bvGrLo](https://codepen.io/dharafyre/pen/bvGrLo)

**방법 2:SDK 구현**

* **소개:** [Livefyre.](https://docs.adobe.com/content/help/en/livefyre/implementation/c-livefyre_js.html) jsis는 사이트에서 앱과 인증에 대해 보안을 설정하는 핵심 라이브러리입니다. 전역 *window.Livefyre* 개체와 단일 공개 메서드 *Livefyre.require*&#x200B;을 정의합니다. 이 메서드는 Livefyre 앱을 임베드하고 제3자 사용자 인증 플랫폼과 통합하는 데 도움이 되는 다른 Livefyre JavaScript 라이브러리를 로드하는 데 사용할 수 있습니다.

* **방법**: [Livefyre JavaScript SDK의 streamhub-wallpackage 사용](https://docs.adobe.com/content/help/en/livefyre/implementation/app-integrations/c-media-wall-integration.html)

* **예**: [https://codepen.io/dharafyre/pen/KZKBNv?editors=1010](https://codepen.io/dharafyre/pen/KZKBNv?editors=1010)

SDK를 사용하는 고급 사용자 정의는 [StreamHub SDK](https://github.com/Livefyre/streamhub-sdk)를 참조하십시오.

**방법 3:API 구현**

* 사용자 지정된 경험 및 데이터 시각화를 만들기 위해 [Bootstrap 및 스트림 API](https://docs.adobe.com/content/help/en/livefyre/implementation/advanced-topics/bootstrap-stream-api.html)를 사용하여 Livefyre 및 소셜 데이터를 사용함으로써 Livefyre 앱을 처음부터 만들 수 있습니다.

UGC용 UI를 작성할 때 [Twitter](https://developer.twitter.com/en/developer-terms/display-requirements.html), [Facebook](https://en.facebookbrand.com/guidelines/brand) 및 [Instagram](https://en.instagram-brand.com/) 표시 지침을 따라야 합니다.

### 미디어 담벼락 인증 통합 {#media-wall-authentication-integration}

인증이 필요한 미디어 벽 통합은 다음을 참조하십시오.

* [AEM Identity Management용 Single Sign ](https://helpx.adobe.com/experience-manager/6-4/sites/administering/using/livefyre.html#CustomizeSingleSignonIntegration) On Integration 사용자 정의
* [제3](https://docs.adobe.com/content/help/en/livefyre/implementation/identity-integration/t-about-identity-integration.html) 자 인증 플랫폼을 위한 ID 통합

### 사용 사례 개요 {#use-case-overview}

AEM 고객으로서 즉시 사용할 수 있는 Livefyre AEM 구성 요소를 사용하여 UGC를 선별하고 Livefyre Media Wall을 사용하여 표시하고자 합니다.

구현 단계:

1. [시작하기](https://helpx.adobe.com/experience-manager/6-3/sites/administering/using/livefyre.html)
1. [Livefyre를 사용하도록 AEM 구성](https://helpx.adobe.com/experience-manager/6-3/sites/administering/using/livefyre.html)
1. [AEM Media Wall 구성 요소를 페이지에 드래그하여 놓기](https://helpx.adobe.com/experience-manager/6-3/sites/administering/using/livefyre.html#UseLivefyrewithAEMSites)
1. [스트림 구성 및 규칙을 추가하여 UGC를 조정하고 미디어 담벼락 구성 요소에 표시](https://docs.adobe.com/content/help/en/livefyre/using/streams/c-streams.html)

스트리밍 UGC에 대한 교육 비디오는 Adobe Experience Manager Livefyre](https://helpx.adobe.com/experience-manager/tutorials.html)에서 [자동 콘텐츠 스트림 만들기 및 소셜 콘텐츠 검색을 참조하십시오.

### 고객 예 {#customer-examples}

* [CNN Media Wall](https://edition.cnn.com/specials/nepal-earthquake-media-wall)
* [PGA 투어 미디어 벽](https://www.pgatour.com/social-hub.html)

사용자 지정된 경험 및 데이터 시각화를 만들기 위해 [Bootstrap 및 스트림 API](https://docs.adobe.com/content/help/en/livefyre/implementation/advanced-topics/bootstrap-stream-api.html)를 사용하여 Livefyre 및 소셜 데이터를 사용함으로써 Livefyre 앱을 처음부터 만들 수 있습니다.

인증이 필요한 Livefyre 앱의 경우 제3자 인증 플랫폼의 경우 [ID 통합](https://docs.adobe.com/content/help/en/livefyre/implementation/identity-integration/t-about-identity-integration.html)을 참조하십시오.

* [PGA 투어 미디어 벽](https://www.pgatour.com/social-hub.html)
* [시간 초과](https://www.timeout.com/london/restaurants/forest-bar-kitchen#tab_panel_3)

## AEM 구성 요소 또는 기존의 Livefyre 통합을 사용하여 Livefyre 주석 통합 {#integrate-livefyre-comments-using-aem-components-or-traditional-livefyre-integration}

### AEM 통합 {#aem-integration-1}

Livefyre Adobe Experience Manager 패키지는 AEM 6.1, 6.2SP1, 6.3, 6.4 및 6.4 SP1에서 사용할 수 있습니다. AEM 5.x 및 6.0은 지원되지 않습니다. 자세한 지침은 [Livefyre](https://helpx.adobe.com/experience-manager/6-4/sites/administering/using/livefyre.html)와 통합을 참조하십시오.

### 기존 구현(사용자 지정된 AEM 구성 요소의 경우) {#traditional-implementation-for-customized-aem-components-1}

Livefyre 댓글 앱을 사용자 정의 AEM 구성 요소 또는 WordPress, Sitecore 또는 DemandWare와 같은 다른 CMS에 구현하는 3가지 방법이 있습니다. 기존의 Livefyre 통합은 CMS에 관계 없음

**방법 1:디자이너 앱 구현**

* **what:** Livefyre 앱을 가장 간단하고 신속하게 통합하는 방법 페이지에 미디어 담벼락 앱을 통합하기 위해 사용자 정의된 JavaScript 포함 코드를 디자인, 구성 및 생성할 수 있습니다.
* **방법:** [주석 앱 만들기, 미리 보기, 게시 및 포함](https://docs.adobe.com/content/help/en/livefyre/using/apps/c-create-an-app.html)

* **예:** [https://codepen.io/dharafyre/pen/oYoJdP](https://codepen.io/dharafyre/pen/oYoJdP)

**방법 2:SDK 구현**

* **소개:** [Livefyre.](https://docs.adobe.com/content/help/en/livefyre/implementation/c-livefyre_js.html) jsis는 사이트에서 앱과 인증에 대해 보안을 설정하는 핵심 라이브러리입니다. 전역 *window.Livefyre* 개체와 단일 공개 메서드 *Livefyre.require*&#x200B;을 정의합니다. 이 메서드는 Livefyre 앱을 임베드하고 제3자 사용자 인증 플랫폼과 통합하는 데 도움이 되는 다른 Livefyre JavaScript 라이브러리를 로드하는 데 사용할 수 있습니다.

* **방법:**

   * [CollectionMeta 토큰](https://docs.adobe.com/content/help/en/livefyre/implementation/getting-started/implementation-process/c-collectionmeta-tokent.html)을 사용하여 컬렉션/앱을 만듭니다.
   * Livefyre.js 포함 코드 구조를 사용하여 [댓글 앱](https://docs.adobe.com/content/help/en/livefyre/implementation/app-integrations/comments/c-comments-integration.html)을 사이트에 통합합니다.

* **예:**  [https://codepen.io/dharafyre/pen/oYoJdP](https://codepen.io/dharafyre/pen/oYoJdP)

SDK를 사용한 고급 사용자 정의는 [StreamHub SDK](https://github.com/Livefyre/streamhub-sdk)를 참조하십시오.

**방법 3:API 구현**

* 사용자 지정된 경험 및 데이터 시각화를 만들기 위해 [Bootstrap 및 스트림 API](https://docs.adobe.com/content/help/en/livefyre/implementation/advanced-topics/bootstrap-stream-api.html)를 사용하여 Livefyre 및 소셜 데이터를 사용함으로써 Livefyre 앱을 처음부터 만들 수 있습니다.

### 댓글 앱 인증 통합 {#comments-app-authentication-integration}

* [AEM Identity Management용 Single Sign ](https://helpx.adobe.com/experience-manager/6-4/sites/administering/using/livefyre.html#CustomizeSingleSignonIntegration) On Integration 사용자 정의
* [제3](https://docs.adobe.com/content/help/en/livefyre/implementation/identity-integration/t-about-identity-integration.html) 자 인증 플랫폼을 위한 ID 통합

### 고객 예 {#customer-examples-1}

* [보이즈(킴벌리 클라크)](https://www.poise.com/en-us/advice-and-support/blog-and-podcast/blog/5-holiday-party-tips-for-managing-lbl)

## Livefyre AEM Assets 통합을 사용하여 AEM Assets {#use-livefyre-aem-assets-integration-to-import-ugc-in-aem-assets}에서 UGC를 가져옵니다.

**Livefyre 설정(UGC 큐레이션 및 Rights Management용):**

1. [Livefyre 자산 라이브러리 폴더에 UGC를 조정하는 [스트림 구성] 및 [규칙 추가]를 선택합니다](https://docs.adobe.com/content/help/en/livefyre/using/streams/c-streams.html).

   1. 스트리밍 UGC에 대한 교육 비디오는 Adobe Experience Manager Livefyre](https://helpx.adobe.com/experience-manager/tutorials.html)에서 [자동 콘텐츠 스트림 만들기 및 소셜 콘텐츠 검색을 참조하십시오.

1. [Livefyre 에셋 라이브러리 폴더에 선별된 UGC를 수집, 구성 및 관리할 수 있습니다](https://docs.adobe.com/content/help/en/livefyre/using/library/assets/c-assets.html).

   1. Livefyre Studio 자산 라이브러리에서 폴더 만들기 및 관리에 대한 교육 비디오를 보려면 Adobe Experience Manager Livefyre](https://helpx.adobe.com/experience-manager/tutorials.html)에서 [자산 작업을 참조하십시오.

1. [Livefyre Studio를 사용하여 선별된 UGC에 대한 권한](https://docs.adobe.com/content/help/en/livefyre/using/rights-requests/c-how-requesting-rights-works.html) 요청

**AEM 설정(AEM Assets으로 UGC 가져오기):**

1. [시작하기](https://helpx.adobe.com/experience-manager/6-3/sites/administering/using/livefyre.html#GettingStarted)
1. [Livefyre를 사용하도록 AEM 구성](https://helpx.adobe.com/experience-manager/6-3/sites/administering/using/livefyre.html#ConfigureAEMtouseLivefyre)
1. [Livefyre에서 선별한 UGC를 AEM Assets으로 가져오기](https://helpx.adobe.com/experience-manager/6-3/sites/administering/using/livefyre.html#UseLivefyrewithAEMAssets)

* [Tourism Australia](https://www.australia.com/en-us)

## AEM 구성 요소 또는 기존의 Livefyre 통합을 사용하여 Livefyre 검토 통합 {#integrate-livefyre-reviews-using-aem-components-or-traditional-livefyre-integration}

### AEM 통합 {#aem-integration-2}

Livefyre Adobe Experience Manager 패키지는 AEM 6.1, 6.2SP1, 6.3, 6.4 및 6.4 SP1에서 사용할 수 있습니다. AEM 5.x 및 6.0은 지원되지 않습니다. 자세한 지침은 [Livefyre](https://helpx.adobe.com/experience-manager/6-4/sites/administering/using/livefyre.html)와 통합을 참조하십시오.

검토 구성 요소는 AEM 6.1에서 지원되는 구성 요소가 아닙니다. 모든 Livefyre 앱](https://helpx.adobe.com/experience-manager/6-3/sites/administering/using/livefyre.html#AEMSupportMatrixforLivefyreApps)에 대한 [AEM 지원 매트릭스를 확인하십시오.

### 기존 구현(사용자 지정된 AEM 구성 요소의 경우) {#traditional-implementation-for-customized-aem-components-2}

Livefyre 리뷰 앱을 사용자 정의 AEM 구성 요소나 WordPress, Sitecore 또는 DemandWare와 같은 다른 CMS에 구현하는 방법에는 두 가지가 있습니다. 기존의 Livefyre 통합은 CMS에 관계 없음

**방법 1:SDK 구현**

* **소개:** [Livefyre.](https://docs.adobe.com/content/help/en/livefyre/implementation/c-livefyre_js.html) jsis는 사이트에서 앱과 인증에 대해 보안을 설정하는 핵심 라이브러리입니다. 전역 *window.Livefyre* 개체와 단일 공개 메서드 *Livefyre.require*&#x200B;을 정의합니다. 이 메서드는 Livefyre 앱을 임베드하고 제3자 사용자 인증 플랫폼과 통합하는 데 도움이 되는 다른 Livefyre JavaScript 라이브러리를 로드하는 데 사용할 수 있습니다.

* **방법:**

   * 검토 컬렉션 내에 저장할 메타데이터를 지정하려면 [CollectionMeta 토큰](https://docs.adobe.com/content/help/en/livefyre/implementation/app-integrations/c-reviews-integration.html)을 만듭니다.
   * [리뷰 앱](https://docs.adobe.com/content/help/en/livefyre/implementation/app-integrations/c-reviews-integration.html)을 *Livefyre.js* 포함 코드 구조를 사용하여 사이트에 통합

* **예:**  [https://codepen.io/dharafyre/pen/GXgvvd](https://codepen.io/dharafyre/pen/GXgvvd)

SDK를 사용한 고급 사용자 정의는 [StreamHub SDK](https://github.com/Livefyre/streamhub-sdk)를 참조하십시오.

**방법 2:API 구현**

* 사용자 정의된 경험 및 데이터 시각화를 만들기 위해 Bootstrap 및 스트림 API를 사용하여 Livefyre 및 소셜 데이터를 사용함으로써 Livefyre 앱을 처음부터 만들 수 있습니다.

추가 등급 및 평가 API는 [여기](https://api.livefyre.com/docs/apis/by-category/ratings-and-reviews)에서 찾을 수 있습니다.

### 댓글 앱 인증 통합 {#comments-app-authentication-integration-1}

* [AEM Identity Management용 Single Sign ](https://helpx.adobe.com/experience-manager/6-4/sites/administering/using/livefyre.html#CustomizeSingleSignonIntegration) On Integration 사용자 정의
* [제3](https://docs.adobe.com/content/help/en/livefyre/implementation/identity-integration/t-about-identity-integration.html) 자 인증 플랫폼을 위한 ID 통합

### 고객 예 {#customer-examples-2}

* [시간 초과](https://www.timeout.com/london/restaurants/forest-bar-kitchen#tab_panel_3)
* [myrecipes](https://www.myrecipes.com/recipe/shrimp-florentine-pasta)

