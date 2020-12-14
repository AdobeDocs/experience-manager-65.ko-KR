---
title: 새로운 Granite UI 필드 구성 요소 만들기
seo-title: 새로운 Granite UI 필드 구성 요소 만들기
description: Granite UI는 양식에서 사용할 수 있도록 설계된 다양한 구성 요소(필드)를 제공합니다.
seo-description: Granite UI는 양식에서 사용할 수 있도록 설계된 다양한 구성 요소(필드)를 제공합니다.
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

Granite UI는 양식에 사용할 수 있도록 디자인된 다양한 구성 요소를 제공합니다.이러한 필드를 Granite UI 어휘의 *fields*&#x200B;라고 합니다. 표준 Granite 양식 구성 요소는 다음 아래에서 사용할 수 있습니다.

`/libs/granite/ui/components/foundation/form/*`

>[!NOTE]
>
>이러한 [granite UI] 양식 필드는 [구성 요소 대화 상자](/help/sites-developing/developing-components.md)에 사용되므로 특히 유용합니다.

>[!NOTE]
>
>필드에 대한 자세한 내용은 [Granite UI 설명서](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html)를 참조하십시오.

Granite UI Foundation 프레임워크를 사용하여 Granite 구성 요소를 개발 및/또는 확장합니다. 여기에는 두 가지 요소가 있습니다.

* 서버측:

   * 기본 구성 요소 컬렉션

      * foundation - 모듈형, 합성, 레이아웃, 재사용 가능
      * 구성 요소 - Sling 구성 요소
   * 애플리케이션 개발에 도움이 되는 도움말


* client-side:

   * Hypermedia 기반 UI를 통해 일반적인 상호 작용 패턴을 얻기 위해 몇 가지 단어(즉, HTML 언어 확장)를 제공하는 clientlibs 컬렉션

일반 Granite UI 구성 요소 `field`은(는) 관심 있는 두 개의 파일로 구성됩니다.

* `init.jsp`:제네릭 처리를 처리합니다.필드를 렌더링할 때 필요한 양식 값을 레이블 지정, 설명 및 제공합니다.
* `render.jsp`:여기서 필드의 실제 렌더링이 수행되고 사용자 정의 필드에 대해 재정의해야 합니다.에 포함된 항목 `init.jsp`은

자세한 내용은 [Granite UI documentation - Field](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/components/foundation/form/field/index.html)를 참조하십시오.

예를 보려면 다음을 참조하십시오.

* `cqgems/customizingfield/components/colorpicker`

   * [코드 샘플](/help/sites-developing/developing-components-samples.md#code-sample-how-to-customize-dialog-fields)에서 제공

* `granite/ui/components/foundation/form`

>[!NOTE]
>
>이 메커니즘은 JSP, i18n 및 XSS를 사용하기 때문에 기본적으로 제공되지 않습니다. 이것은 Strings를 국제화하고 탈출해야 한다는 것을 의미합니다. 다음 디렉토리에는 표준 인스턴스의 일반 필드가 포함되어 있으며 이러한 필드를 참조로 사용할 수 있습니다.
>
>`/libs/granite/ui/components/foundation/form` directory

## 구성 요소 {#creating-the-server-side-script-for-the-component}에 대한 서버측 스크립트 만들기

사용자 지정된 필드는 구성 요소에 대한 마크업을 제공하는 `render.jsp` 스크립트만 재정의해야 합니다. JSP(렌더링 스크립트)를 마크업에 대한 래퍼로 간주할 수 있습니다.

1. `sling:resourceSuperType` 속성을 사용하여 상속할 새 구성 요소를 만듭니다.

   `/libs/granite/ui/components/foundation/form/field`

1. 스크립트 재정의:

   `render.jsp`

   이 스크립트에서 클라이언트가 생성된 요소와 상호 작용하는 방법을 알 수 있도록 하이퍼미디어 마크업(즉, 하이퍼미디어 비용이 포함된 강화 마크업)을 생성해야 합니다. 이렇게 하려면 Granite UI 서버측 코딩 스타일을 따라야 합니다.

   사용자 정의할 때 다음을 사용하여 요청에서 양식 값(`init.jsp`에서 초기화됨)을 읽기만 하면 *이(가)* 이행해야 하는 유일한 계약이 됩니다.

   ```
   // Delivers the value of the field (read from the content)
   ValueMap vm = (ValueMap) request.getAttribute(Field.class.getName());
   vm.get("value, String.class");
   ```

   자세한 내용은 기본 Granite UI 필드 구현을 참조하십시오.예: `/libs/granite/ui/components/foundation/form/textfield`

   >[!NOTE]
   >
   >현재, JSP는 HTL에서 쉽게 구현되지 않는 구성 요소 간에 정보를 전달하는 데 있어 선호하는 스크립팅 방법입니다. HTL에서는 JSP가 자주 사용됩니다.

## 구성 요소 {#creating-the-client-library-for-the-component}에 대한 클라이언트 라이브러리 만들기

구성 요소에 특정 클라이언트측 비헤이비어를 추가하려면:

1. `cq.authoring.dialog` 범주의 clientlib을 만듭니다.
1. `cq.authoring.dialog` 범주의 clientlib을 만들고 그 안에 `JS`/ `CSS`를 정의합니다.

   clientlib 내에서 `JS`/ `CSS` 정의

   >[!NOTE]
   >
   >현재 Granite UI는 JS 비헤이비어를 추가하는 데 직접 사용할 수 있는 즉시 사용 가능한 리스너나 후크를 제공하지 않습니다. 따라서 구성 요소에 JS 비헤이비어를 더 추가하려면 태그 생성 중에 구성 요소에 할당해야 하는 사용자 지정 클래스에 JS 후크를 구현해야 합니다.

