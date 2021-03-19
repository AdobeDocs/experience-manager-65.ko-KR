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
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '971'
ht-degree: 1%

---


# 컨텐츠 배달{#content-delivery}

>[!NOTE]
>
>단일 페이지 애플리케이션 프레임워크 기반 클라이언트측 렌더링(예: 응답)이 필요한 프로젝트에는 SPA 편집기를 사용하는 것이 좋습니다. [추가 정보](/help/sites-developing/spa-overview.md).

모바일 앱은 필요에 따라 AEM의 모든 콘텐츠를 사용하여 타깃팅된 앱 경험을 제공할 수 있어야 합니다.

자산, 사이트 컨텐츠, CaaS 컨텐츠(무선 컨텐츠) 및 자체 구조를 갖는 사용자 지정 컨텐츠를 사용하는 것이 포함됩니다.

>[!NOTE]
>
>**Over-the-Air 컨텐츠** 는 ContentSync 핸들러를 통해 위의 모든 제품에서 가져올 수 있습니다. 이 플러그인을 사용하면 업데이트 또는 패키지를 유지 관리할 수 있을 뿐만 아니라 zips를 통해 패키징 및 전달할 수 있습니다.

컨텐츠 서비스가 제공하는 3가지 주요 유형의 자료는 다음과 같습니다.

1. **에셋**
1. **패키징된 HTML 컨텐츠(HTML/CSS/JS)**
1. **채널에 독립적인 컨텐츠**

![chlimage_1-154](assets/chlimage_1-154.png)

## 에셋 {#assets}

자산 컬렉션은 다른 컬렉션에 대한 참조를 포함하는 AEM 구조체입니다.

자산 컬렉션은 콘텐츠 서비스를 통해 노출될 수 있습니다. 요청에서 자산 컬렉션을 호출하면 해당 URL을 포함하여 자산의 목록인 개체가 반환됩니다. 자산은 URL을 통해 액세스합니다. URL이 개체에 제공됩니다. 예:

* 페이지 엔티티는 이미지 참조를 포함하는 JSON(페이지 개체)을 반환합니다. 이미지 참조는 이미지의 자산 이진 항목을 가져오는 데 사용되는 URL입니다.
* 폴더의 자산 목록에 대한 요청은 해당 폴더의 모든 개체에 대한 세부 정보가 포함된 JSON을 반환합니다. 이 목록은 하나의 객체입니다. JSON에는 해당 폴더의 각 에셋에 대한 에셋 바이너리를 가져오는 데 사용되는 URL 참조가 있습니다.

### 자산 최적화 {#asset-optimization}

콘텐츠 서비스의 주요 가치는 장치에 최적화된 자산을 반환하는 기능입니다. 이렇게 하면 로컬 장치 저장 공간이 줄어들고 앱 성능이 향상됩니다.

자산 최적화는 API 요청에 제공된 정보를 기반으로 서버측 함수가 됩니다. 가능한 경우 에셋 변환을 캐시해야 하므로 유사한 요청에는 에셋 표현물을 다시 생성할 필요가 없습니다.

### 자산 워크플로 {#assets-workflow}

자산 워크플로우는 다음과 같습니다.

1. 즉시 사용 가능한 AEM의 에셋 참조
1. 모델이 지정된 자산 참조 개체 만들기
1. 엔티티 편집

   1. 자산 또는 자산 수집 선택
   1. JSON 렌더링 사용자 정의

다음 다이어그램은 **자산 참조 워크플로**&#x200B;를 보여줍니다.

![chlimage_1-155](assets/chlimage_1-155.png)

### 자산 관리 {#managing-assets}

콘텐츠 서비스는 다른 AEM 콘텐츠를 통해 참조할 수 없는 AEM 관리 자산에 대한 액세스를 제공합니다.

#### 기존 관리 자산 {#existing-managed-assets}

기존 AEM Sites 및 자산 사용자는 AEM Assets을 사용하여 모든 채널의 디지털 자료를 모두 관리하고 있습니다. 이들은 기본 모바일 앱을 개발 중이며 AEM Assets에서 관리하는 여러 자산을 사용해야 합니다. 로고, 배경 이미지, 단추 아이콘 등의 작업을 할 수 있습니다.

현재 자산 저장소 주위에 분산되어 있습니다. 앱에서 참조해야 하는 파일은 다음과 같습니다.

* /content/dam/geometrixx-outdoors/brand/logo_light.png
* /content/dam/geometrixx-outdoors/brand/logo_dark.png
* /content/dam/geometrixx-outdoors/styles/backgrounds/gray_blue.jpg
* /content/dam/geometrixx-outdoors/brand/icons/app/cart.png
* /content/dam/geometrixx-outdoors/brand/icons/app/home.png

#### CS Asset 엔티티 액세스 {#accessing-cs-asset-entities}

이제 API를 통해 페이지를 사용할 수 있게 되는 방법에 대한 단계를 제쳐두고(AEM UI 설명에 의해 설명됨) 작업이 완료되었다고 가정합니다. 자산 엔터티가 만들어지고 &quot;appImages&quot; 공간에 추가되었습니다. 조직 목적으로 스페이스에서 추가 폴더가 생성되었습니다. 따라서 자산 엔티티는 AEM JCR에 다음과 같이 저장됩니다.

* /content/entities/appImages/logos/logo_light
* /content/entities/appImages/logos/logo_dark
* /content/entities/appImages/bkgnd/gray_blue
* /content/entities/appImages/icons/cart
* /content/entities/appImages/icons/home

#### 사용 가능한 자산 엔티티 목록 {#getting-a-list-of-available-asset-entities} 가져오기

앱 개발자는 에셋 엔티티를 검색함으로써 사용 가능한 에셋 목록을 가져올 수 있습니다. 콘텐츠 서비스 공간 끝점은 웹 서비스 API SDK를 통해 해당 정보를 제공할 수 있습니다.

그 결과는 &quot;아이콘&quot; 폴더의 에셋 목록을 제공하는 JSON 형식의 개체가 됩니다.

![chlimage_1-156](assets/chlimage_1-156.png)

#### 이미지 {#getting-an-image} 가져오기

JSON은 컨텐츠 서비스에서 이미지에 생성된 각 이미지에 대한 URL을 제공합니다.

&quot;장바구니&quot; 이미지의 바이너리를 가져오기 위해 클라이언트 라이브러리가 다시 사용됩니다.

## 패키지화된 HTML 컨텐츠 {#packaged-html-content}

HTML 컨텐츠는 컨텐츠 레이아웃을 유지 관리해야 하는 고객에게 필요합니다. 이는 Cordova 웹뷰와 같은 웹 컨테이너를 사용하는 기본 응용 프로그램에서 컨텐트를 표시하는 데 유용합니다.

AEM Content Services는 API를 통해 모바일 앱에 HTML 콘텐츠를 제공할 수 있습니다. AEM 컨텐츠를 HTML로 노출하려는 고객은 AEM 컨텐츠 소스를 가리키는 HTML 페이지 엔티티를 만듭니다.

다음 옵션이 고려됩니다.

* **Zip 파일:** 장치에서 제대로 표시할 수 있는 최상의 기회를 얻으려면 페이지의 모든 참조 자료(css, JavaScript, 자산 등)를 - 응답이 있는 단일 압축 파일에 포함됩니다. HTML 페이지의 참조는 이러한 파일의 상대 경로를 사용하도록 조정됩니다.
* **스트리밍:** AEM에서 필요한 파일의 매니페스트를 가져옵니다. 그런 다음 해당 매니페스트를 사용하여 모든 파일(HTML, CSS, JS 등)을 요청합니다. 후속 요청과 함께.

![chlimage_1-157](assets/chlimage_1-157.png)

## 채널 독립 콘텐츠 {#channel-independent-content}

채널 독립적인 컨텐츠는 레이아웃, 구성 요소 또는 기타 채널 특정 정보에 대한 걱정 없이 페이지와 같은 AEM 컨텐츠 구문을 보여주는 방법입니다.

이러한 콘텐츠 개체는 AEM 구조를 JSON 형식으로 변환하는 콘텐츠 모델을 사용하여 생성됩니다. 결과 JSON 데이터에는 AEM 저장소에서 분리되는 컨텐츠 데이터에 대한 정보가 포함되어 있습니다. 여기에는 메타데이터와 AEM 참조 링크를 자산에 반환하고 콘텐츠 구조 간 관계(엔티티 계층 구조 포함)가 포함됩니다.

### 채널 독립 컨텐츠 관리 {#managing-channel-independent-content}

콘텐츠는 다양한 방법으로 앱에 가져올 수 있습니다.

1. AEM Over-the-Air를 통한 GET 컨텐츠 ZIPS

   * 컨텐츠 동기화 핸들러는 zip 패키지를 직접 업데이트하거나 기존 컨텐츠 렌더러를 호출하여 업데이트할 수 있습니다

      * 플랫폼 핸들러
      * AEMM 핸들러
      * 사용자 정의 핸들러

1. 컨텐츠 렌더러를 통해 직접 컨텐츠 GET

   * 기본 스링 렌더러
   * AEM Mobile/Content Services 컨텐츠 렌더링 프로그램
   * 사용자 지정 렌더링

