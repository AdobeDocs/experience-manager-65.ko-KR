---
title: 컨텐츠 전달
seo-title: 컨텐츠 전달
description: 'null'
seo-description: 'null'
uuid: 1e7bea34-ca50-41ed-8295-fa182c27fa69
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
discoiquuid: 3d65cc6b-5721-472f-a805-588d50f3571b
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 컨텐츠 전달{#content-delivery}

>[!NOTE]
>
>단일 페이지 애플리케이션 프레임워크 기반 클라이언트측 렌더링(예: 응답)이 필요한 프로젝트에 SPA 편집기를 사용하는 것이 좋습니다. [추가 정보](/help/sites-developing/spa-overview.md).

모바일 앱은 필요에 따라 AEM의 모든 콘텐츠를 사용하여 타깃팅된 앱 경험을 제공할 수 있어야 합니다.

여기에는 자산, 사이트 컨텐츠, CaaS 컨텐츠(OOO-AIR) 및 자체 구조를 갖는 사용자 정의 컨텐츠 사용이 포함됩니다.

>[!NOTE]
>
>**Over-the-Air** 컨텐츠는 ContentSync 핸들러를 통해 위의 모든 제품에서 가져올 수 있습니다. 이 플러그인은 업데이트나 패키지를 유지 관리할 수 있을 뿐만 아니라 zips를 통해 패키징 및 전달하는 데 사용할 수 있습니다.

컨텐츠 서비스가 제공하는 자료의 주요 유형은 다음과 같습니다.

1. **자산**
1. **패키지화된 HTML 컨텐츠(HTML/CSS/JS)**
1. **채널 독립적인 컨텐츠**

![chlimage_1-154](assets/chlimage_1-154.png)

## 자산 {#assets}

자산 컬렉션은 다른 컬렉션에 대한 참조를 포함하는 AEM 구조체입니다.

자산 컬렉션은 콘텐츠 서비스를 통해 노출될 수 있습니다. 요청에서 자산 컬렉션을 호출하면 해당 URL을 포함하여 자산의 목록인 개체가 반환됩니다. 자산은 URL을 통해 액세스합니다. 개체에 URL이 제공됩니다. 예:

* 페이지 엔티티는 이미지 참조를 포함하는 JSON(페이지 개체)을 반환합니다. 이미지 참조는 이미지의 자산 바이너리를 가져오는 데 사용되는 URL입니다.
* 폴더의 자산 목록 요청은 해당 폴더의 모든 개체에 대한 세부 정보가 포함된 JSON을 반환합니다. 그 목록은 하나의 개체입니다. JSON에는 해당 폴더의 각 자산에 대한 자산 바이너리를 가져오는 데 사용되는 URL 참조가 있습니다.

### 자산 최적화 {#asset-optimization}

Content Services의 주요 가치는 장치에 맞게 최적화된 자산을 반환하는 기능입니다. 이렇게 하면 로컬 디바이스 스토리지 요구 사항이 줄어들고 앱 성능이 향상됩니다.

자산 최적화는 API 요청에 제공된 정보를 기반으로 서버측 함수가 됩니다. 가능한 경우 에셋 표현물을 캐시하여 유사한 요청도 에셋 표현물을 다시 생성할 필요가 없습니다.

### 자산 워크플로우 {#assets-workflow}

자산 워크플로우는 다음과 같습니다.

1. AEM에서 바로 사용 가능한 자산 참조
1. 모델이 지정된 자산 참조 개체 만들기
1. 엔터티 편집

   1. 자산 또는 자산 컬렉션 선택
   1. JSON 렌더링 사용자 정의

다음 다이어그램은 자산 **참조 워크플로우를 보여줍니다**.

![chlimage_1-155](assets/chlimage_1-155.png)

### 자산 관리 {#managing-assets}

콘텐츠 서비스는 다른 AEM 콘텐츠를 통해 참조할 수 없는 AEM 관리 자산에 대한 액세스를 제공합니다.

#### 기존 관리 자산 {#existing-managed-assets}

기존 AEM Sites 및 Assets 사용자는 AEM Assets를 사용하여 모든 채널에 대한 모든 디지털 자료를 관리하고 있습니다. 기본 모바일 앱을 개발 중이며 AEM 자산에서 관리하는 여러 자산을 사용해야 합니다. 로고, 배경 이미지, 단추 아이콘 등

현재 자산 저장소 주위로 분산되어 있습니다. 앱에서 참조해야 하는 파일은 다음과 같습니다.

* /content/dam/geometrixx-outdoors/brand/logo_light.png
* /content/dam/geometrixx-outdoors/brand/logo_dark.png
* /content/dam/geometrixx-outdoors/styles/backgrounds/gray_blue.jpg
* /content/dam/geometrixx-outdoors/brand/icons/app/cart.png
* /content/dam/geometrixx-outdoors/brand/icons/app/home.png

#### CS Asset Entities 액세스 {#accessing-cs-asset-entities}

이제 API를 통해 페이지를 사용할 수 있는 방법에 대한 단계를 잠시 중단하고 AEM UI 설명에 따라 처리했다고 가정합니다. 자산 엔터티가 생성되어 &quot;appImages&quot; 공간에 추가되었습니다. 조직 용도로 공간 아래에 추가 폴더가 생성되었습니다. 따라서 자산 엔티티는 다음과 같이 AEM JCR에 저장됩니다.

* /content/entities/appImages/logos/logo_light
* /content/entities/appImages/logos/logo_dark
* /content/entities/appImages/bkgnd/gray_blue
* /content/entities/appImages/icons/cart
* /content/entities/appImages/icons/home

#### 사용 가능한 자산 엔티티 목록 가져오기 {#getting-a-list-of-available-asset-entities}

앱 개발자는 에셋 엔티티를 검색하여 사용 가능한 에셋 목록을 가져올 수 있습니다. 콘텐츠 서비스 공간 끝점은 웹 서비스 API SDK를 통해 해당 정보를 제공할 수 있습니다.

결과는 &quot;icons&quot; 폴더의 자산 목록을 제공하는 JSON 형식의 개체가 됩니다.

![chlimage_1-156](assets/chlimage_1-156.png)

#### 이미지 가져오기 {#getting-an-image}

JSON은 컨텐츠 서비스에서 이미지에 생성한 각 이미지에 대한 URL을 제공합니다.

&quot;장바구니&quot; 이미지의 바이너리를 가져오기 위해 클라이언트 라이브러리가 다시 사용됩니다.

## 패키지화된 HTML 컨텐츠 {#packaged-html-content}

HTML 컨텐츠는 컨텐츠 레이아웃을 유지해야 하는 고객에게 필요합니다. 이는 Cordova 웹뷰와 같은 웹 컨테이너를 사용하는 기본 응용 프로그램에서 컨텐츠를 표시하는 데 유용합니다.

AEM Content Services는 API를 통해 모바일 앱에 HTML 콘텐츠를 제공할 수 있습니다. AEM 컨텐츠를 HTML로 노출하려는 고객은 AEM 컨텐츠 소스를 가리키는 HTML 페이지 엔티티를 만듭니다.

다음 옵션이 고려됩니다.

* **** Zip 파일:장치에서 제대로 표시할 수 있는 최상의 기회를 얻기 위해 페이지의 모든 참조 자료(css, JavaScript, 에셋 등)를 표시합니다. - 는 응답과 함께 하나의 압축 파일에 포함됩니다. HTML 페이지의 참조는 이러한 파일의 상대 경로를 사용하도록 조정됩니다.
* **** 스트리밍:AEM에서 필요한 파일의 매니페스트 가져오기를 참조하십시오. 그런 다음 이 매니페스트를 사용하여 모든 파일(HTML, CSS, JS 등)을 요청합니다. 후속 요청에서 사용할 수 있습니다.

![chlimage_1-157](assets/chlimage_1-157.png)

## 채널 독립 컨텐츠 {#channel-independent-content}

채널 독립적인 컨텐츠는 레이아웃, 구성 요소 또는 기타 채널별 정보에 대한 걱정 없이 페이지와 같은 AEM 컨텐츠 구문을 노출하는 방법입니다.

이러한 콘텐츠 엔티티는 콘텐츠 모델을 사용하여 생성되어 AEM 구조를 JSON 형식으로 변환합니다. 결과 JSON 데이터에는 AEM 저장소에서 분리된 컨텐츠 데이터에 대한 정보가 포함되어 있습니다. 여기에는 메타데이터와 자산에 대한 AEM 참조 링크 반환과 콘텐츠 구조 간의 관계(엔티티 계층 구조 포함)가 포함됩니다.

### 채널 독립 컨텐츠 관리 {#managing-channel-independent-content}

콘텐츠는 다양한 방법으로 앱에 액세스할 수 있습니다.

1. AEM Over-the-Air를 통해 컨텐츠 ZIPS 다운로드

   * 컨텐츠 동기화 핸들러는 zip 패키지를 직접 업데이트하거나 기존 컨텐츠 렌더러를 호출하여 업데이트할 수 있습니다

      * 플랫폼 처리기
      * AEMM 처리기
      * 사용자 지정 처리기

1. 컨텐츠 렌더러를 통해 직접 컨텐츠 가져오기

   * 기본 슬링 렌더러
   * AEM Mobile/Content Services 컨텐츠 렌더링
   * 사용자 정의 렌더링

