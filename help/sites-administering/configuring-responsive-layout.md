---
title: 레이아웃 컨테이너 및 레이아웃 모드 구성
seo-title: 레이아웃 컨테이너 및 레이아웃 모드 구성
description: 레이아웃 컨테이너 및 레이아웃 모드를 구성하는 방법을 알아봅니다.
seo-description: 레이아웃 컨테이너 및 레이아웃 모드를 구성하는 방법을 알아봅니다.
uuid: 952b7c86-76ab-4699-8530-8638e46bb50f
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: 10940000-808a-48ae-8e46-61eccef71eab
legacypath: /content/docs/en/aem/6-2/administer/operations/page-authoring/configuring-responsive-layouting
translation-type: tm+mt
source-git-commit: ebf3f34af7da6b1a659ac8d8843152b97f30b652
workflow-type: tm+mt
source-wordcount: '1324'
ht-degree: 9%

---


# 레이아웃 컨테이너 및 레이아웃 모드 구성{#configuring-layout-container-and-layout-mode}

[반응형 레이아웃](/help/sites-authoring/responsive-layout.md) 은 [반응형 웹 디자인을 구현하기 위한 메커니즘입니다](https://en.wikipedia.org/wiki/Responsive_web_design). 사용자는 사용자가 사용하는 장치에 따라 레이아웃과 차원이 다른 웹 페이지를 만들 수 있습니다.

>[!NOTE]
>
>응용 웹 디자인을 사용하는 [모바일 웹](/help/sites-developing/mobile-web.md) 메커니즘과 비교할 수 있습니다(주로 클래식 UI용).

AEM에서는 메커니즘을 조합하여 페이지에 대한 응답형 레이아웃을 실현합니다.

* [**레이아웃 컨테이너&#x200B;**](/help/sites-authoring/responsive-layout.md#adding-a-layout-container-and-its-content-edit-mode)구성 요소

   이 구성 요소는 응답형 격자 내에 구성 요소를 추가 및 배치할 수 있도록 해주는 격자 단락 시스템을 제공합니다. 페이지의 기본 parsys로 사용하거나 구성 요소 브라우저에서 작성자가 사용할 수 있도록 만들 수 있습니다.

   * 기본 **레이아웃 컨테이너** 구성 요소는 다음과 같이 정의됩니다.

      /libs/wcm/foundation/components/responsivegrid

   * 레이아웃 컨테이너를 정의할 수 있습니다.

      * 사용자가 페이지에 추가할 수 있는 구성 요소입니다.
      * 페이지의 기본 parsys입니다.
      * 모두.

         레이아웃 컨테이너를 페이지의 표준으로 지정할 수 있지만 사용자가 이 내에 추가 레이아웃 컨테이너를 추가할 수 있습니다. 예를 들어 열 컨트롤을 만들려면

* **[레이아웃 모드](/help/sites-authoring/responsive-layout.md#defining-layouts-layout-mode)**레이아웃 컨테이너를 페이지에 배치하면&#x200B;**레이아웃**모드를 사용하여 컨텐츠를 응답형 격자 내에 배치할 수 있습니다.
[**에뮬레이터&#x200B;**](/help/sites-authoring/responsive-layout.md#selecting-a-device-to-emulate)에뮬레이터를 사용하면 구성 요소의 크기를 대화 방식으로 변경하여 장치/창 크기에 따라 레이아웃을 다시 정렬하는 응답형 웹 사이트를 만들고 편집할 수 있습니다. 사용자는 컨텐츠가 에뮬레이터를 사용하여 어떻게 렌더링될지 알 수 있습니다.**

* [!CAUTION]**](/help/sites-authoring/responsive-layout.md#selecting-a-device-to-emulate)

>Although the **Layout Container** component is available in the classic UI, its full functionality is only available in the touch-enabled UI.
>
>이러한 응답형 격자 메커니즘을 사용하여 다음을 수행할 수 있습니다.****

중단점(장치 그룹화를 나타내는)을 사용하여 장치 레이아웃을 기반으로 달라지는 컨텐츠 동작을 정의할 수 있습니다.

* 장치 그룹을 기반으로 구성 요소를 숨깁니다(구성 요소가 숨겨지는 중단점을 정의함).
* 수평 격자에 맞춤 기능을 사용할 수 있습니다(구성 요소를 격자에 배치하고, 필요에 따라 크기를 변경하고, 언제 구성 요소가 나란히 또는 위/아래에 있도록 축소되거나 리플로우되어야 하는지 지정).
* 열 컨트롤을 구현할 수 있습니다.
* [!NOTE]

>즉시 설치할 수 있도록 응답형 레이아웃이 We.Retail 참조 사이트 [에 맞게 구성되었습니다](/help/sites-developing/we-retail.md). 다른 페이지에 대해 [레이아웃 컨테이너] 구성 요소를 [활성화해야](#enable-the-layout-container-component-for-page) 합니다.
>
>응답형 에뮬레이터 구성 {#configuring-the-responsive-emulator}](/help/sites-developing/we-retail.md)[](#enable-the-layout-container-component-for-page)

## 이 작업을 통해 사이트에서 응답형 **에뮬레이터를** 볼 수 있습니다.

에뮬레이션 페이지 구성 요소 등록 {#register-your-page-components-for-emulation}**

### 에뮬레이터를 사용하여 페이지를 지원하려면 페이지 구성 요소를 등록해야 합니다. 시뮬레이션을 [위해 페이지 구성 요소 등록을 참조하십시오](/help/sites-developing/responsive.md#registering-page-components-for-simulation).

장치 그룹 지정 {#specify-the-device-groups}](/help/sites-developing/responsive.md#registering-page-components-for-simulation)

### 에뮬레이터의 장치 목록에 나타나는 장치 그룹을 지정하려면 장치 그룹 [지정을 참조하십시오](/help/sites-developing/responsive.md#specifying-the-device-groups).

사이트를 지정된 장치 그룹에 연결 {#link-your-site-to-the-specified-device-groups}](/help/sites-developing/responsive.md#specifying-the-device-groups)

### 장치를 포함하려면 사이트를 장치 그룹에 연결해야 합니다. 장치 [목록](/help/sites-developing/responsive.md#adding-the-devices-list) 추가(클래식 및 터치에 적합한 UI 모두에 대해)를 참조하십시오.

사이트에 대한 레이아웃 모드 활성화 {#activate-layout-mode-for-your-site}](/help/sites-developing/responsive.md#adding-the-devices-list)

## 이러한 절차는 사이트에서 **레이아웃** 모드를 활성화하는 데 사용됩니다.

중단점 구성 {#configure-the-breakpoints}**

### [중단점](/help/sites-authoring/responsive-layout.md#selecting-a-device-to-emulate):

[반응형 디자인에 사용됩니다.](/help/sites-authoring/responsive-layout.md#selecting-a-device-to-emulate)

* 다음을 정의할 수 있습니다.
* 페이지 템플릿에서, 여기서 설정은 해당 템플릿으로 만든 모든 페이지에 복사됩니다.

   * 페이지 노드에서 설정이 하위 페이지에서 상속됩니다.
   * 제목과 너비를 정의합니다.

* 제목은 필요한 경우 방향을 포함한 일반 장치 그룹화에 대해 설명합니다. 예: phone, tablet, tablet landscape.

   * 너비는 해당 일반 장치 그룹의 최대 너비(픽셀 단위)를 정의합니다. 예를 들어 중단점 휴대폰의 너비가 768인 경우 휴대폰 장치에 사용되는 레이아웃의 최대 너비가 됩니다.
   * 에뮬레이터를 사용할 때 페이지 편집기 상단에 마커로 표시됩니다.

* 상위 노드 계층으로부터 상속되며 임의로 재정의할 수 있습니다.
* 마지막으로 구성된 중단점 위에 있는 모든 항목을 포함하는 기본( *즉시 사용 가능한* 중단점)이 있습니다.
* CRXDE Lite 또는 XML을 사용하여 정의할 수 있습니다.**

[!NOTE]

>[!NOTE]새 프로젝트를 설정하는 경우:
>
>템플릿에 중단점을 추가해야 합니다.
>
>* 기존 프로젝트(기존 컨텐츠 포함)를 마이그레이션하는 경우 다음을 수행해야 합니다.
>
>
템플릿에 중단점 추가
>
>* 기존 페이지에 동일한 중단점 추가
>* 상속이 작동 중이기 때문에 콘텐츠의 루트 페이지로 제한할 수 있습니다.

>
>  
CRXDE Lite를 사용하여 중단점 구성 {#configuring-breakpoints-using-crxde-lite}

#### CRXDE Lite(또는 동급)를 사용하여 다음 중 하나로 이동합니다.{#configuring-breakpoints-using-crxde-lite}

1. 템플릿 정의

   * 페이지의 `jcr:content` 노드입니다.
   * Under create the node: `jcr:content`

1. 이름: `cq:responsive`

   * 유형: `nt:unstructured`
   * Under this create the node:`nt:unstructured`

1. 이름: `breakpoints`

   * 유형: `nt:unstructured`
   * 중단점 노드 아래에서 원하는 수의 중단점을 만들 수 있습니다. 각 정의는 다음과 같은 속성을 가진 단일 노드입니다.`nt:unstructured`

1. 이름: `<descriptive name>`

   * 유형: `nt:unstructured`
   * 제목: `String` * `<descriptive title seen in Emulator>`*
   * 너비: `Decimal` * `<value of breakpoint>`*
   * XML을 사용하여 중단점 구성 {#configuring-breakpoints-using-xml}`<value of breakpoint>`

#### 중단점은 해당 템플릿(또는 컨텐트) 폴더 `<jcr:content>` `.context.html` 아래의 섹션 내에 있습니다.

예제 정의:`<jcr:content>``.context.html`

응답형 정보 공급자 추가 {#add-a-responsive-information-provider}

```xml
<cq:responsive jcr:primaryType="nt:unstructured">
  <breakpoints jcr:primaryType="nt:unstructured">
    <phone jcr:primaryType="nt:unstructured" title="{String}Phone" width="{Decimal}768"/>
    <tablet jcr:primaryType="nt:unstructured" title="{String}Tablet" width="{Decimal}1200"/>
  </breakpoints>
</cq:responsive>
```

### [!NOTE]

>[!NOTE]페이지 구성 요소가 기초 페이지 구성 요소를 기반으로 하지 않는 경우에만 필요합니다.
>
>다음 노드 구조를 상위 페이지 구성 요소에 `cq:infoProviders` 복사합니다.

`/libs/foundation/components/page/cq:infoProviders/responsive`

페이지에 대한 구성 요소 크기 조정 활성화 {#enable-component-resizing-for-the-page}

## 이러한 절차는 레이아웃 **모드에서 구성 요소의 크기를 조정할 수 있도록** 필요합니다.

레이아웃 컨테이너를 기본 Parsys로 설정 {#set-layout-container-as-main-parsys}**

### 페이지의 기본 parsys를 레이아웃 컨테이너로 설정하려면 parsys를 다음과 같이 정의해야 합니다.{#set-layout-container-as-main-parsys}

`wcm/foundation/components/responsivegrid`

`wcm/foundation/components/responsivegrid`다음 중 하나에서

페이지 구성 요소

* 페이지 템플릿(나중에 사용하기 위해)
* 다음 두 예는 정의를 보여 줍니다.

**HTL:**

* **JSP:**

   ```xml
   <sly data-sly-resource="${'par' @ resourceType='wcm/foundation/components/responsivegrid'}/>
   ```

* 반응형 CSS 포함 {#include-the-responsive-css}**

   ```
   <cq:include path="par" resourceType="wcm/foundation/components/responsivegrid" />
   ```

### LESS를 사용한 중단점에 대한 CSS {#css-for-breakpoints-using-less}

#### AEM에서는 LESS를 사용하여 필요한 CSS의 일부를 생성하므로 프로젝트에 포함시켜야 합니다.{#css-for-breakpoints-using-less}

또한 추가 구성 및 함수 호출을 제공하려면 [클라이언트 라이브러리를[#$tu99] 만들어야 합니다. 다음 LESS 추출은 프로젝트에 추가해야 하는 최소값의 예입니다.



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

`/libs/wcm/foundation/clientlibs/grid/grid_base.less`

스타일 지정 고려 사항 {#styling-considerations}

#### 응답형 컨테이너 내에 있는 구성 요소는 응답형 격자 크기에 따라 크기가 조정됩니다(해당 HTML DOM 요소와 함께). 따라서 이러한 상황에서는 고정 폭(포함된) DOM 요소의 정의를 피하거나 업데이트하는 것이 좋습니다.{#styling-considerations}

예:

이전:

* `width=100px`

   * `width=100px`이후:

* `max-width=100px`

   * 크기 조정 및 적응형 이미지 준수 {#resizing-and-adaptive-image-compliance}

#### 격자 내의 구성 요소 크기를 조정하면 다음 리스너가 적절하게 트리거됩니다.{#resizing-and-adaptive-image-compliance}

`beforeedit`

* `beforechildedit`
* `afteredit`
* `afterchildedit`

* 응답형 그리드에 포함된 응용 이미지의 컨텐츠 크기를 적절하게 조정하고 업데이트하려면 리스너로 설정된 `afterEdit` 세트를 포함된 모든 구성 `REFRESH_PAGE` `EditConfig` 요소의 파일에 추가해야 합니다.

예:`afterEdit``REFRESH_PAGE``EditConfig`

`<cq:listeners jcr:primaryType="cq:EditListenersConfig" afteredit="REFRESH_PAGE" />`

`<cq:listeners jcr:primaryType="cq:EditListenersConfig" afteredit="REFRESH_PAGE" />`적응형 이미지 메커니즘은 현재 창 크기에 대해 올바른 이미지 선택을 제어하는 스크립트를 통해 사용할 수 있습니다. DOM이 준비되거나 전용 이벤트를 수신할 때 활성화됩니다. 현재 사용자의 작업 결과를 제대로 반영하려면 페이지를 새로 고쳐야 합니다.

[!CAUTION]

>[!CAUTION]Custom stylesheet clientlibs는 작성자와 게시 시 제대로 작동되도록 헤더의 일부로 로드되어야 합니다.
>
>페이지에 대한 레이아웃 컨테이너 구성 요소 활성화 {#enable-the-layout-container-component-for-page}

## 이러한 작업을 통해 작성자는 레이아웃 컨테이너 구성 요소의 **인스턴스를** 페이지로 드래그할 수 있습니다.

페이지 편집을 위해 레이아웃 컨테이너 구성 요소 활성화 {#enable-the-layout-container-component-for-page-editing}**

### 작성자가 컨텐츠 페이지에 응답형 그리드를 추가할 수 있도록 하려면 페이지의 레이아웃 컨테이너 구성 요소를 활성화해야 합니다. 다음 중 하나를 사용하여 수행할 수 있습니다.{#enable-the-layout-container-component-for-page-editing}

**작성 환경**

* 디자인 [모드](/help/sites-authoring/default-components-designmode.md) 를 사용하여 페이지의 **레이어 컨테이너** 구성 요소를 활성화합니다.

   **구성 요소 정의******

* 구성 요소 `allowedComponent` 를 정의할 때 또는 정적 포함을 사용합니다.**

   레이아웃 컨테이너의 격자 구성 {#configure-the-grid-of-the-layout-container}

### 레이아웃 컨테이너의 각 특정 인스턴스에 사용할 수 있는 열 수를 구성할 수 있습니다.{#configure-the-grid-of-the-layout-container}

**작성 환경**

1. **레이아웃 컨테이너의 각 특정 인스턴스에 사용할 수 있는 열 수를 구성할 수 있습니다.**

   이렇게 하려면 [디자인 모드를](/help/sites-authoring/default-components-designmode.md)사용한 다음 필요한 컨테이너에 대한 디자인 대화 상자를 엽니다. 배치 및 크기 조정을 위해 사용할 수 있는 열 수를 지정할 수 있습니다. 기본값은 12입니다.

   **XML**

1. **응답형 격자에 대한 정의는 다음과 같이 지정됩니다.**

   `etc/design/<*your-project-name*>/.content.xml`

   `etc/design/<*your-project-name*>/.content.xml`다음 매개 변수를 정의할 수 있습니다.

   사용 가능한 열 수:

   * `columns="{String}8"`

      * `columns="{String}8"`현재 구성 요소에 추가할 수 있는 구성 요소:
   * `components="[/libs/wcm/foundation/components/responsivegrid, ...`

      * `components="[/libs/wcm/foundation/components/responsivegrid, ...`


