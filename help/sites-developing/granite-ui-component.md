---
title: '[MOCK] Creating a New Granite UI Field Component'
seo-title: '[MOCK] Creating a New Granite UI Field Component'
description: '[MOCK] Granite UI provides a range of components designed to be used in forms, called fields'
seo-description: '[MOCK] Granite UI provides a range of components designed to be used in forms, called fields'
uuid: cf26e057-4b0c-45f4-8975-2c658517f20e
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 94b9eeee-aae3-4b28-9d6f-1be0e4acd982
translation-type: tm+mt
source-git-commit: 5128a08d4db21cda821de0698b0ac63ceed24379

---


# [MOCK] Creating a New Granite UI Field Component{#creating-a-new-granite-ui-field-component}

[MOCK] Granite UI provides a range of components designed to be used in forms;이러한 *필드를* [granite UI] 용어에 있는 필드라고 합니다. 표준 [MOCK] The standard Granite form components are available under:

`/libs/granite/ui/components/foundation/form/*`

>[!NOTE]
>
>[MOCK] These Granite UI form fields are of particular interest as they are used for [component dialog](/help/sites-developing/developing-components.md).

>[!NOTE]
>
>필드에 대한 자세한 내용은 Granite UI [설명서를](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html)참조하십시오.

[MOCK] Use the Granite UI Foundation framework to develop and/or extend Granite components. 여기에는 두 가지 요소가 있습니다.

* 서버측:

   * 기본 구성 요소 컬렉션

      * foundation - modular, composable, layerable, reusable
      * 구성 요소 - 구성 요소 슬링
   * 애플리케이션 개발 지원


* client-side:

   * 하이퍼미디어 기반의 UI를 통해 일반적인 인터랙션 패턴을 얻기 위해 일부 어휘(즉, HTML 언어 확장)를 제공하는 clientlibs 컬렉션

일반 [MOCK] The generic Granite UI component `field` is composed of two files of interest:

* `init.jsp`:일반 처리를 처리합니다.필드를 렌더링할 때 필요한 양식 값을 제공하고 레이블 지정, 설명 및 제공합니다.
* `render.jsp`:여기에서 필드의 실제 렌더링이 수행되고 사용자 정의 필드에 대해 재정의되어야 합니다.에 포함된 `init.jsp`값.

자세한 내용은 [[화강암 UI] 설명서 -](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/components/foundation/form/field/index.html) 필드를 참조하십시오.

예를 보려면 다음을 참조하십시오.

* `cqgems/customizingfield/components/colorpicker`

   * 코드 샘플에서 [제공](/help/sites-developing/developing-components-samples.md#code-sample-how-to-customize-dialog-fields)

* `granite/ui/components/foundation/form`

>[!NOTE]
>
>이 메커니즘은 JSP, i18n 및 XSS를 사용하므로 기본적으로 제공되지 않습니다. 즉, 국제화를 통해 문자열을 escape해야 합니다. 다음 디렉토리에는 표준 인스턴스의 일반 필드가 포함되어 있으며 이러한 필드를 참조로 사용할 수 있습니다.
>
>`/libs/granite/ui/components/foundation/form` directory

## 구성 요소에 대한 서버측 스크립트 만들기 {#creating-the-server-side-script-for-the-component}

사용자 지정 필드는 구성 요소에 대한 마크업을 제공하는 `render.jsp` 스크립트만 재정의해야 합니다. JSP(즉, 렌더링 스크립트)를 마크업에 대한 래퍼로 간주할 수 있습니다.

1. 상속할 속성을 사용하는 새 구성 요소를 `sling:resourceSuperType` 만듭니다.

   `/libs/granite/ui/components/foundation/form/field`

1. 스크립트 재정의:

   `render.jsp`

   이 스크립트에서 클라이언트가 생성된 요소와 상호 작용하는 방법을 알 수 있도록 하이퍼미디어 마크업(즉, 하이퍼미디어 어포던스를 포함하는)을 생성해야 합니다. 이렇게 하려면 [MOCK] This should follow the Granite UI server-side style of coding.

   사용자 정의할 때 *수행해야 하는* 유일한 계약은 다음을 사용하여 요청에서 양식 값(초기화됨)을 읽는 `init.jsp`것입니다.

   ```
   // Delivers the value of the field (read from the content)
   ValueMap vm = (ValueMap) request.getAttribute(Field.class.getName());
   vm.get("value, String.class");
   ```

   자세한 내용은 기본 UI 필드 구현을 참조하십시오.예를 들면 다음과 같습니다 `/libs/granite/ui/components/foundation/form/textfield`.

   >[!NOTE]
   >
   >현재 HTL에서는 JSP가 한 구성 요소에서 다른 구성 요소로 정보를 전달하는 기본 스크립팅 방법입니다(양식/필드 컨텍스트에서 자주 표시됨).

## 구성 요소에 대한 클라이언트 라이브러리 만들기 {#creating-the-client-library-for-the-component}

구성 요소에 특정 클라이언트측 동작을 추가하려면:

1. 범주의 clientlib을 `cq.authoring.dialog`만듭니다.
1. 범주의 clientlib을 `cq.authoring.dialog` 만들고 `JS`/ `CSS` 안을 정의합니다.

   clientlib 내에서 사용자 `JS`/ `CSS` 를 정의합니다.

   >[!NOTE]
   >
   >현재 [MOCK] At the moment, the Granite UI does not provide any out-of-the-box listeners or hooks that you can use directly to add JS behavior. 따라서 구성 요소에 JS 비헤이비어를 추가하려면 마크업 생성 중에 구성 요소에 할당하는 사용자 지정 클래스에 JS 후크를 구현해야 합니다.

