---
title: 컨텐츠 전달
seo-title: 컨텐츠 전달
description: 컨텐츠 전달
seo-description: 'null'
uuid: 1e7bea34-ca50-41ed-8295-fa182c27fa69
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
discoiquuid: 3d65cc6b-5721-472f-a805-588d50f3571b
exl-id: 85e73679-684e-402f-8186-8b56d8bd9372
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '971'
ht-degree: 1%

---

# 컨텐츠 전달{#content-delivery}

>[!NOTE]
>
>단일 페이지 애플리케이션 프레임워크 기반 클라이언트측 렌더링(예: React)이 필요한 프로젝트에 SPA 편집기를 사용하는 것이 좋습니다. [추가 정보](/help/sites-developing/spa-overview.md).

모바일 앱은 타깃팅된 앱 경험을 전달하는 데 필요한 경우 AEM의 모든 콘텐츠를 사용할 수 있어야 합니다.

여기에는 자산, 사이트 컨텐츠, CaaS 컨텐츠(공기 중) 및 자체 구조를 가질 수 있는 사용자 지정 컨텐츠 등이 포함됩니다.

>[!NOTE]
>
>**Over-the-Air** 콘텐츠는 ContentSync 핸들러를 통해 위의 모든 위치에서 가져올 수 있습니다. 이 플러그인은 업데이트 또는 패키지를 유지 관리할 뿐만 아니라 zips를 통해 패키지 및 전달을 일괄 처리하는 데 사용할 수 있습니다.

Content Services가 제공하는 자료는 다음과 같은 세 가지 주요 유형이 있습니다.

1. **에셋**
1. **패키지된 HTML 콘텐츠(HTML/CSS/JS)**
1. **채널 독립 컨텐츠**

![chlimage_1-154](assets/chlimage_1-154.png)

## 자산 {#assets}

자산 컬렉션은 다른 컬렉션에 대한 참조를 포함하는 AEM 구문입니다.

자산 수집은 Content Services를 통해 노출될 수 있습니다. 요청에서 자산 컬렉션을 호출하면 해당 URL을 포함하여 자산 목록인 개체가 반환됩니다. 자산은 URL을 통해 액세스합니다. URL은 개체에 제공됩니다. 예:

* 페이지 엔티티는 이미지 참조를 포함하는 JSON(페이지 개체)을 반환합니다. 이미지 참조는 이미지의 자산 바이너리를 가져오는 데 사용되는 URL입니다.
* 폴더의 자산 목록에 대한 요청은 해당 폴더의 모든 엔티티에 대한 세부 정보와 함께 JSON을 반환합니다. 이 목록은 개체입니다. JSON에는 해당 폴더의 각 자산에 대한 자산 바이너리를 가져오는 데 사용되는 URL 참조가 있습니다.

### 자산 최적화 {#asset-optimization}

컨텐츠 서비스의 주요 값은 장치에 최적화된 자산을 반환하는 기능입니다. 이렇게 하면 로컬 장치 스토리지 요구 사항이 줄어들고 앱 성능이 향상됩니다.

자산 최적화는 API 요청에 제공된 정보를 기반으로 하는 서버 측 함수가 됩니다. 가능한 경우, 유사한 요청에서 자산 표현물을 다시 생성할 필요가 없도록 자산 표현물을 캐시해야 합니다.

### 자산 워크플로우 {#assets-workflow}

자산 워크플로우는 다음과 같습니다.

1. AEM에서 사용할 수 있는 자산 참조
1. 해당 모델이 있는 자산 참조 엔티티 만들기
1. 엔티티 편집

   1. 자산 또는 자산 수집 선택
   1. JSON 렌더링 사용자 지정

다음 다이어그램은 **자산 참조 워크플로우**&#x200B;를 보여줍니다.

![chlimage_1-155](assets/chlimage_1-155.png)

### 자산 관리 {#managing-assets}

Content Services를 사용하면 다른 AEM 컨텐츠를 통해 참조되지 않을 수 있는 AEM 관리 자산에 액세스할 수 있습니다.

#### 기존 관리 자산 {#existing-managed-assets}

기존 AEM Sites 및 Assets 사용자는 AEM Assets을 사용하여 모든 채널에 대한 모든 디지털 자료를 관리하고 있습니다. 기본 모바일 앱을 개발 중이며 AEM Assets에서 관리하는 여러 자산을 사용해야 합니다. 로고, 배경 이미지, 단추 아이콘 등과 같은 작업을 수행할 수 있습니다.

현재 이것은 Assets 저장소 주위에 분산되어 있습니다. 앱에서 참조해야 하는 파일은 다음과 같습니다.

* /content/dam/geometrixx-outdoors/brand/logo_light.png
* /content/dam/geometrixx-outdoors/brand/logo_dark.png
* /content/dam/geometrixx-outdoors/styles/backgrounds/gray_blue.jpg
* /content/dam/geometrixx-outdoors/brand/icons/app/cart.png
* /content/dam/geometrixx-outdoors/brand/icons/app/home.png

#### CS 자산 엔티티 액세스 {#accessing-cs-asset-entities}

페이지를 API를 통해 사용할 수 있도록 하는 방법을 당분간 (AEM UI 설명에 포함됨)에 한 단계 뒤로 제쳐두고 작업이 수행되었다고 가정해 보겠습니다. 자산 엔티티가 만들어져서 &quot;appImages&quot; 공간에 추가되었습니다. 추가적인 폴더는 조직을 위한 공간 아래에 만들어졌습니다. 따라서 자산 엔티티는 AEM JCR에 다음과 같이 저장됩니다.

* /content/entities/appImages/logos/logo_light
* /content/entities/appImages/logos/logo_dark
* /content/entities/appImages/bkgnd/gray_blue
* /content/entities/appImages/icons/cart
* /content/entities/appImages/icons/home

#### 사용 가능한 자산 엔티티 목록 가져오기 {#getting-a-list-of-available-asset-entities}

앱 개발자는 자산 엔티티를 검색하여 사용 가능한 자산 목록을 가져올 수 있습니다. Content Services 공간 엔드포인트는 웹 서비스 API SDK를 통해 해당 정보를 제공할 수 있습니다.

그 결과는 &quot;아이콘&quot; 폴더에 있는 자산 목록을 제공하는 JSON 형식의 개체가 됩니다.

![chlimage_1-156](assets/chlimage_1-156.png)

#### 이미지 가져오기 {#getting-an-image}

JSON은 Content Services에서 이미지에 생성한 각 이미지의 URL을 제공합니다.

&quot;장바구니&quot; 이미지에 대한 바이너리를 가져오려면 클라이언트 라이브러리가 다시 사용됩니다.

## 패키지된 HTML 콘텐츠 {#packaged-html-content}

콘텐츠 레이아웃을 유지해야 하는 고객을 위해 HTML 콘텐츠가 필요합니다. Cordova 웹뷰와 같은 웹 컨테이너를 사용하여 컨텐츠를 표시하는 기본 애플리케이션에 유용합니다.

AEM Content Services는 API를 통해 모바일 앱에 HTML 콘텐츠를 제공할 수 있습니다. AEM 컨텐츠를 HTML로 노출하려는 고객은 AEM 컨텐츠 소스를 가리키는 HTML 페이지 엔티티를 만듭니다.

다음 옵션이 고려됩니다.

* **Zip 파일:** 장치에서 올바르게 표시할 수 있는 최상의 기회를 얻기 위해 페이지의 모든 참조 자료(css, JavaScript, 자산 등)가 여기에 해당합니다. - 응답이 있는 단일 압축 파일에 포함됩니다. HTML 페이지의 참조는 이러한 파일의 상대 경로를 사용하도록 조정됩니다.
* **스트리밍:** AEM에서 필요한 파일의 매니페스트를 가져옵니다. 그런 다음 해당 매니페스트를 사용하여 모든 파일(HTML, CSS, JS 등)을 요청하고 후속 요청 사용.

![chlimage_1-157](assets/chlimage_1-157.png)

## 채널 독립 컨텐츠 {#channel-independent-content}

채널 독립 콘텐츠는 레이아웃, 구성 요소 또는 기타 채널별 정보에 대한 걱정 없이 페이지와 같은 AEM 컨텐츠 구문을 노출하는 방법입니다.

이러한 컨텐츠 엔티티는 컨텐츠 모델을 사용하여 AEM 구조를 JSON 형식으로 변환하는 것입니다. 결과 JSON 데이터에는 AEM 리포지토리에서 분리되는 컨텐츠의 데이터에 대한 정보가 포함되어 있습니다. 여기에는 메타데이터 및 자산에 대한 AEM 참조 링크 반환과 컨텐츠 구조 간 관계(엔티티 계층 포함)가 포함됩니다.

### 채널 독립 컨텐츠 관리 {#managing-channel-independent-content}

콘텐츠는 여러 가지 방법으로 앱에 액세스할 수 있습니다.

1. AEM Over-the-Air를 통한 GET 컨텐츠 ZIPS

   * 컨텐츠 동기화 처리기는 zip 패키지를 직접 업데이트하거나 기존 컨텐츠 렌더러를 호출하여 업데이트할 수 있습니다

      * 플랫폼 핸들러
      * AEM 핸들러
      * 사용자 지정 핸들러

1. 콘텐츠 렌더러를 통해 직접 콘텐츠 GET

   * 기본 Sling 렌더러
   * AEM Mobile/Content Services 컨텐츠 렌더러
   * 사용자 지정 렌더링
