---
title: 레이아웃 컨테이너 및 레이아웃 모드 구성
seo-title: Configuring Layout Container and Layout Mode
description: 레이아웃 컨테이너 및 레이아웃 모드를 구성하는 방법을 알아봅니다.
seo-description: Learn how to configure Layout Container and Layout Mode.
uuid: 952b7c86-76ab-4699-8530-8638e46bb50f
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: 10940000-808a-48ae-8e46-61eccef71eab
legacypath: /content/docs/en/aem/6-2/administer/operations/page-authoring/configuring-responsive-layouting
exl-id: 61152b2d-4c0b-4cfd-9669-cf03d32cb7c7
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1309'
ht-degree: 9%

---

# 레이아웃 컨테이너 및 레이아웃 모드 구성{#configuring-layout-container-and-layout-mode}

[응답형 레이아웃](/help/sites-authoring/responsive-layout.md) 이는 [반응형 웹 디자인](https://en.wikipedia.org/wiki/Responsive_web_design). 이를 통해 사용자는 사용자가 사용하는 장치에 따라 레이아웃과 차원이 있는 웹 페이지를 만들 수 있습니다.

>[!NOTE]
>
>이는 와 비교할 수 있습니다 [모바일 웹](/help/sites-developing/mobile-web.md) 응용 웹 디자인을 사용하는 메커니즘(주로 클래식 UI용).

AEM에서는 메커니즘을 조합하여 페이지에 대한 응답형 레이아웃을 실현합니다.

* [**레이아웃 컨테이너**](/help/sites-authoring/responsive-layout.md#adding-a-layout-container-and-its-content-edit-mode) 구성 요소

   이 구성 요소는 응답형 격자 내에 구성 요소를 추가 및 배치할 수 있도록 해주는 격자 단락 시스템을 제공합니다. 이 매개 변수는 페이지의 기본 parsys로 사용하거나 구성 요소 브라우저의 작성자가 사용할 수 있도록 만들 수 있습니다.

   * 기본값 **레이아웃 컨테이너** 구성 요소는 다음과 같이 정의됩니다.

      /libs/wcm/foundation/components/responsivegrid

   * 레이아웃 컨테이너를 정의할 수 있습니다.

      * 사용자가 페이지에 추가할 수 있는 구성 요소입니다.
      * 페이지의 기본 parsys입니다.
      * 모두.

         사용자가 이 페이지 내에 추가 레이아웃 컨테이너를 추가할 수 있도록 하면서 레이아웃 컨테이너를 페이지의 표준으로 지정할 수 있습니다. 예를 들어, 열 컨트롤을 구현할 수 있습니다.

* **[레이아웃 모드](/help/sites-authoring/responsive-layout.md#defining-layouts-layout-mode)**
레이아웃 컨테이너를 페이지에 배치하면 
**레이아웃** 응답형 그리드 내에 컨텐츠를 배치하기 위한 모드.

* [**에뮬레이터**](/help/sites-authoring/responsive-layout.md#selecting-a-device-to-emulate)
에뮬레이터를 사용하면 구성 요소의 크기를 대화 방식으로 변경하여 장치/창 크기에 따라 레이아웃을 다시 정렬하는 응답형 웹 사이트를 만들고 편집할 수 있습니다. 사용자는 컨텐츠가 에뮬레이터를 사용하여 어떻게 렌더링될지 알 수 있습니다.

>[!CAUTION]
>
>하지만 **레이아웃 컨테이너** 구성 요소는 클래식 UI에서 사용할 수 있으며, 전체 기능은 터치 지원 UI에서만 사용할 수 있습니다.

이러한 응답형 격자 메커니즘을 사용하여 다음과 같은 작업을 수행할 수 있습니다.

* 중단점(장치 그룹을 나타내는)을 사용하여 장치 레이아웃에 따라 달라지는 컨텐츠 동작을 정의합니다.
* 장치 그룹을 기반으로 구성 요소를 숨깁니다(구성 요소가 숨겨질 중단점을 정의합니다.).
* 수평 격자에 맞춤 기능을 사용할 수 있습니다(구성 요소를 격자에 배치하고, 필요에 따라 크기를 변경하고, 언제 구성 요소가 나란히 또는 위/아래에 있도록 축소되거나 리플로우되어야 하는지 지정).
* 열 컨트롤을 구현할 수 있습니다.

>[!NOTE]
>
>기본 설치에서 응답형 레이아웃이 [We.Retail 참조 사이트](/help/sites-developing/we-retail.md). 당신은 여전히 [레이아웃 컨테이너 구성 요소 활성화](#enable-the-layout-container-component-for-page) 추가 정보.

## 응답형 에뮬레이터 구성 {#configuring-the-responsive-emulator}

이 작업을 사용하면 응답형 사용자를 볼 수 있습니다 **에뮬레이터** 구현합니다.

### 에뮬레이션용 페이지 구성 요소 등록 {#register-your-page-components-for-emulation}

에뮬레이터에서 페이지를 지원하도록 하려면 페이지 구성 요소를 등록해야 합니다. 자세한 내용은 [시뮬레이션에 페이지 구성 요소 등록](/help/sites-developing/responsive.md#registering-page-components-for-simulation).

### 장치 그룹 지정 {#specify-the-device-groups}

에뮬레이터의 장치 목록에 나타나는 장치 그룹을 지정하려면 다음을 참조하십시오 [장치 그룹 지정](/help/sites-developing/responsive.md#specifying-the-device-groups).

### 지정된 장치 그룹에 사이트 연결 {#link-your-site-to-the-specified-device-groups}

장치를 포함하려면 사이트를 장치 그룹에 연결해야 합니다. 자세한 내용은 [장치 목록 추가](/help/sites-developing/responsive.md#adding-the-devices-list) (클래식 및 터치에 적합한 UI 모두에 대해)

## 사이트에 대한 레이아웃 모드 활성화 {#activate-layout-mode-for-your-site}

이러한 절차는 **레이아웃** 모드로 전환합니다.

### 중단점 구성 {#configure-the-breakpoints}

[중단점](/help/sites-authoring/responsive-layout.md#selecting-a-device-to-emulate):

* 반응형 디자인에 사용됩니다.
* 다음을 정의할 수 있습니다.

   * 페이지 템플릿에서 설정을 해당 템플릿으로 만든 페이지에 복사할 수 있습니다.
   * 페이지 노드에서 설정이 하위 페이지에서 상속됩니다.

* 제목과 너비를 정의합니다.

   * 제목은 필요한 경우 방향을 사용하여 일반 장치 그룹을 설명합니다. 예를 들어 phone, tablet, tablet 가로 등이 있습니다.
   * 너비는 해당 일반 장치 그룹의 최대 너비(픽셀 단위)를 정의합니다. 예를 들어 중단점 전화기의 너비가 768이라면 휴대폰 장치에 사용되는 레이아웃의 최대 너비입니다.

* 에뮬레이터를 사용할 때 페이지 편집기 맨 위에 마커로 표시됩니다.
* 상위 노드 계층에서 상속되며 임의로 대체할 수 있습니다.
* 마지막 부분 위에 있는 모든 것을 포함하는 기본(즉시 사용 가능한) 중단점이 있습니다 *구성* 중단점.

CRXDE Lite 또는 XML을 사용하여 정의할 수 있습니다.

>[!NOTE]
>
>새 프로젝트를 설정하는 경우:
>
>* 템플릿에 중단점을 추가해야 합니다.
>
>기존 프로젝트(기존 컨텐츠 포함)를 마이그레이션하는 경우 다음을 수행해야 합니다.
>
>* 템플릿에 중단점 추가
>* 기존 페이지에 동일한 중단점 추가
>
>  상속이 작동 중이기 때문에 컨텐츠의 루트 페이지로 제한할 수 있습니다.

#### CRXDE Lite을 사용하여 중단점 구성 {#configuring-breakpoints-using-crxde-lite}

1. CRXDE Lite(또는 그에 상응하는 항목)를 사용하여 다음 중 하나로 이동합니다.

   * 템플릿 정의.
   * 다음 `jcr:content` 노드 아래에 있어야 합니다.

1. 아래 `jcr:content` 노드 만들기:

   * 이름: `cq:responsive`
   * 유형: `nt:unstructured`

1. 여기서 노드를 만듭니다.

   * 이름: `breakpoints`
   * 유형: `nt:unstructured`

1. 중단점 노드 아래에서 원하는 수만큼 중단점을 만들 수 있습니다. 각 정의는 다음 속성을 갖는 단일 노드입니다.

   * 이름: `<descriptive name>`
   * 유형: `nt:unstructured`
   * 제목: `String` * `<descriptive title seen in Emulator>`*
   * 너비: `Decimal` * `<value of breakpoint>`*

#### XML을 사용하여 중단점 구성 {#configuring-breakpoints-using-xml}

중단점은 `<jcr:content>` 섹션 `.context.html` 적절한 템플릿(또는 컨텐츠) 폴더 아래에 표시됩니다.

예제 정의:

```xml
<cq:responsive jcr:primaryType="nt:unstructured">
  <breakpoints jcr:primaryType="nt:unstructured">
    <phone jcr:primaryType="nt:unstructured" title="{String}Phone" width="{Decimal}768"/>
    <tablet jcr:primaryType="nt:unstructured" title="{String}Tablet" width="{Decimal}1200"/>
  </breakpoints>
</cq:responsive>
```

### 응답형 정보 공급자 추가 {#add-a-responsive-information-provider}

>[!NOTE]
>
>페이지 구성 요소가 기초 페이지 구성 요소를 기반으로 하지 않는 경우에만 필요합니다.

다음을 복사합니다. `cq:infoProviders` 노드 구조를 상위 페이지 구성 요소로 만들기:

`/libs/foundation/components/page/cq:infoProviders/responsive`

## 페이지에 대한 구성 요소 크기 조정 활성화 {#enable-component-resizing-for-the-page}

다음 절차에서는 **레이아웃** 모드.

### 레이아웃 컨테이너를 기본 Parsys로 설정 {#set-layout-container-as-main-parsys}

페이지의 기본 parsys를 레이아웃 컨테이너로 설정하려면 parsys를 다음과 같이 정의해야 합니다.

`wcm/foundation/components/responsivegrid`

다음 중 하나에서 다음을 수행합니다.

* 페이지 구성 요소
* 페이지 템플릿(나중에 사용하기 위해)

다음 두 예는 정의를 보여줍니다.

* **HTL:**

   ```xml
   <sly data-sly-resource="${'par' @ resourceType='wcm/foundation/components/responsivegrid'}/>
   ```

* **JSP:**

   ```
   <cq:include path="par" resourceType="wcm/foundation/components/responsivegrid" />
   ```

### 응답형 CSS 포함 {#include-the-responsive-css}

#### LESS를 사용하여 중단점에 대한 CSS {#css-for-breakpoints-using-less}

AEM에서는 LESS를 사용하여 필요한 CSS의 일부를 생성하므로 프로젝트에 포함되어야 합니다.

또한 [클라이언트 라이브러리](https://docs.adobe.com/content/docs/en/aem/6-0/develop/the-basics/clientlibs.html) 추가 구성 및 함수 호출을 제공합니다. 다음 LESS 추출은 프로젝트에 추가해야 하는 최소값의 예입니다.

```java
@import (once) "/libs/wcm/foundation/clientlibs/grid/grid_base.less";

/* maximum amount of grid cells to be provided */
@max_col: 12;

/* default breakpoint */
.aem-Grid {
  .generate-grid(default, @max_col);
}

/* phone breakpoint */
@media (max-width: 768px) {
  .aem-Grid {
    .generate-grid(phone, @max_col);
  }
}

/* tablet breakpoint */
@media (min-width: 769px) and (max-width: 1200px) {
  .aem-Grid {
    .generate-grid(tablet, @max_col);
  }
}
```

기본 그리드 정의는 다음 위치에서 찾을 수 있습니다.

`/libs/wcm/foundation/clientlibs/grid/grid_base.less`

#### 스타일 지정 고려 사항 {#styling-considerations}

응답형 컨테이너 내에 있는 구성 요소는 응답형 그리드 크기에 따라 해당 HTML DOM 요소와 함께 크기가 조정됩니다. 따라서 이러한 경우에는 고정 너비(포함) DOM 요소를 정의하지 않거나 업데이트하는 것이 좋습니다.

예:

* 이전:

   * `width=100px`

* 이후:

   * `max-width=100px`

#### 크기 조정 및 응용 이미지 준수 {#resizing-and-adaptive-image-compliance}

그리드 내에서 구성 요소를 변경하면 다음 리스너가 적절히 트리거됩니다.

* `beforeedit`
* `beforechildedit`
* `afteredit`

* `afterchildedit`

응답형 그리드에 포함된 응용 이미지의 콘텐츠를 적절하게 크기를 조정하고 업데이트하려면 `afterEdit` 설정 `REFRESH_PAGE` 수신기로 `EditConfig` 포함된 모든 구성 요소의 파일입니다.

예:

`<cq:listeners jcr:primaryType="cq:EditListenersConfig" afteredit="REFRESH_PAGE" />`

응용 이미지 메커니즘은 현재 창의 크기에 대해 올바른 이미지의 선택을 제어하는 스크립트를 통해 사용할 수 있습니다. DOM이 준비되거나 전용 이벤트를 받을 때 활성화됩니다. 현재 사용자의 작업 결과를 제대로 반영하려면 페이지를 새로 고쳐야 합니다.

>[!CAUTION]
>
>사용자 정의 스타일시트 clientlibs를 헤더의 일부로 로드하여 작성자와 게시 시 제대로 작동해야 합니다.

## 페이지에 대한 레이아웃 컨테이너 구성 요소 활성화 {#enable-the-layout-container-component-for-page}

이러한 작업을 통해 작성자는 **레이아웃 컨테이너** 구성 요소를 페이지에 추가합니다.

### 페이지 편집을 위한 레이아웃 컨테이너 구성 요소 활성화 {#enable-the-layout-container-component-for-page-editing}

작성자가 컨텐츠 페이지에 추가 응답형 그리드를 추가할 수 있도록 하려면 페이지의 레이아웃 컨테이너 구성 요소를 활성화해야 합니다. 다음 중 하나를 사용하여 이 작업을 수행할 수 있습니다.

* **작성 환경**

   사용 [디자인 모드](/help/sites-authoring/default-components-designmode.md) 를 활성화하려면 **레이어 컨테이너** 구성 요소 를 포함합니다.

* **구성 요소 정의**

   사용 `allowedComponent` 또는 구성 요소를 정의할 때 정적 포함이 포함됩니다.

### 레이아웃 컨테이너의 그리드 구성 {#configure-the-grid-of-the-layout-container}

레이아웃 컨테이너의 각 특정 인스턴스에 대해 사용할 수 있는 열 수를 구성할 수 있습니다.

1. **작성 환경**

   레이아웃 컨테이너의 각 특정 인스턴스에 사용할 수 있는 열 수를 구성할 수 있습니다.

   이렇게 하려면 [디자인 모드](/help/sites-authoring/default-components-designmode.md)그런 다음 필요한 컨테이너에 대한 디자인 대화 상자를 엽니다. 여기에서 위치 지정 및 크기 조정을 위해 사용할 수 있는 열 수를 지정할 수 있습니다. 기본값은 12입니다.

1. **XML**

   응답형 그리드에 대한 정의는 다음과 같이 지정됩니다.

   `etc/design/<*your-project-name*>/.content.xml`

   다음 매개 변수를 정의할 수 있습니다.

   * 사용 가능한 열 수:

      * `columns="{String}8"`
   * 현재 구성 요소에 추가할 수 있는 구성 요소:

      * `components="[/libs/wcm/foundation/components/responsivegrid, ...`
