---
title: 새로운 Granite UI 필드 구성 요소 만들기
seo-title: 새로운 Granite UI 필드 구성 요소 만들기
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
workflow-type: tm+mt
source-wordcount: '561'
ht-degree: 3%

---


# 새로운 Granite UI 필드 구성 요소 만들기{#creating-a-new-granite-ui-field-component}

[MOCK] Granite UI provides a range of components designed to be used in forms;[MOCK] These are called *fields* in the Granite UI vocabulary. [MOCK] The standard Granite form components are available under:

`/libs/granite/ui/components/foundation/form/*`

>[!NOTE]
>
>[MOCK] These Granite UI form fields are of particular interest as they are used for [component dialogs](/help/sites-developing/developing-components.md).

>[!NOTE]
>
>필드에 대한 자세한 내용은 [Granite UI documentation](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html)을 참조하십시오.

[MOCK] Use the Granite UI Foundation framework to develop and/or extend Granite components. 여기에는 두 가지 요소가 있습니다.

* server-side:

   * 기본 구성 요소 컬렉션

      * foundation - modular, composable, layerable, reusable
      * 구성 요소 - 구성 요소 슬링
   * 애플리케이션 개발을 돕는 도우미


* client-side:

   * Hypermedia 기반 UI를 통해 일반적인 인터랙션 패턴을 구현할 수 있도록 일부 단어(즉, HTML 언어 확장)를 제공하는 clientlibs 컬렉션

[MOCK] The generic Granite UI component `field` is composed of two files of interest:

* `init.jsp`:일반 처리를 처리합니다.필드를 렌더링할 때 필요한 양식 값을 지정하고, 설명을 추가하고, 제공합니다.
* `render.jsp`:여기서 필드의 실제 렌더링이 수행되며 사용자 지정 필드에 대해 무시해야 합니다.에 포함된 값 `init.jsp`.

자세한 내용은 [Granite UI documentation - Field](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/components/foundation/form/field/index.html)를 참조하십시오.

예를 보려면 다음을 참조하십시오.

* `cqgems/customizingfield/components/colorpicker`

   * [코드 샘플](/help/sites-developing/developing-components-samples.md#code-sample-how-to-customize-dialog-fields)에서 제공

* `granite/ui/components/foundation/form`

>[!NOTE]
>
>이 메커니즘이 JSP, i18n 및 XSS를 사용하므로 기본적으로 제공되지 않습니다. 이는 Strings를 국제화하고 탈출해야 함을 의미합니다. 다음 디렉토리에는 표준 인스턴스의 일반 필드가 포함되어 있으며 이러한 필드를 참조로 사용할 수 있습니다.
>
>`/libs/granite/ui/components/foundation/form` directory

## 구성 요소 {#creating-the-server-side-script-for-the-component}에 대한 서버측 스크립트 만들기

사용자 지정된 필드는 구성 요소에 대한 마크업을 제공하는 `render.jsp` 스크립트만 재정의해야 합니다. JSP(렌더링 스크립트)를 마크업에 대한 래퍼로 간주할 수 있습니다.

1. 상속할 `sling:resourceSuperType` 속성을 사용하는 새 구성 요소를 만듭니다.

   `/libs/granite/ui/components/foundation/form/field`

1. 스크립트 재정의:

   `render.jsp`

   이 스크립트에서 클라이언트가 생성된 요소와 상호 작용하는 방법을 알 수 있도록 하이퍼미디어 마크업(즉, 하이퍼미디어 어포던스를 포함하는 풍부해진 마크업)을 생성해야 합니다. [MOCK] This should follow the Granite UI server-side style of coding.

   사용자 정의할 때 다음을 사용하여 요청에서 양식 값(`init.jsp`에서 초기화됨)을 읽는 것은 *이(가)* 이행해야 하는 유일한 계약입니다.

   ```
   // Delivers the value of the field (read from the content)
   ValueMap vm = (ValueMap) request.getAttribute(Field.class.getName());
   vm.get("value, String.class");
   ```

   자세한 내용은 [MOCK] For more details, please refer to the implementation of out-ot-the-box Granite UI fields;예: `/libs/granite/ui/components/foundation/form/textfield`

   >[!NOTE]
   >
   >현재, JSP는 HTL에서 쉽게 달성되지 않는 한 구성 요소에서 다른 구성 요소로 정보를 전달하는 기본 스크립팅 방법입니다. HTL에서는 이러한 정보를 쉽게 전달하지 않습니다.

## 구성 요소 {#creating-the-client-library-for-the-component}에 대한 클라이언트 라이브러리 만들기

구성 요소에 특정 클라이언트측 동작을 추가하려면:

1. `cq.authoring.dialog` 범주의 clientlib을 만듭니다.
1. `cq.authoring.dialog` 범주의 clientlib을 만들고 그 안에 `JS`/ `CSS`를 정의합니다.

   clientlib 내에서 `JS`/ `CSS` 정의

   >[!NOTE]
   >
   >현재 [MOCK] At the moment, the Granite UI does not provide any out-of-the-box listeners or hook that you can use directly to add JS behavior. 따라서 구성 요소에 JS 비헤이비어를 추가하려면 태그 생성 중에 구성 요소에 할당하는 사용자 지정 클래스에 JS 후크를 구현해야 합니다.

