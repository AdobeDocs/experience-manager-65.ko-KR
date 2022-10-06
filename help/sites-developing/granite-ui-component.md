---
title: 새로운 Granite UI 필드 구성 요소 만들기
seo-title: Creating a New Granite UI Field Component
description: Granite UI는 필드라고 하는 양식에 사용하도록 디자인된 다양한 구성 요소를 제공합니다
seo-description: Granite UI provides a range of components designed to be used in forms, called fields
uuid: cf26e057-4b0c-45f4-8975-2c658517f20e
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 94b9eeee-aae3-4b28-9d6f-1be0e4acd982
exl-id: e4820330-2ee6-4eca-83fd-462aa0b83647
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '539'
ht-degree: 2%

---

# 새로운 Granite UI 필드 구성 요소 만들기{#creating-a-new-granite-ui-field-component}

Granite UI는 양식에 사용하도록 디자인된 다양한 구성 요소를 제공합니다. 이러한 이름을 *필드* ( Granite UI 어휘에서)를 참조하십시오. 표준 Granite 양식 구성 요소는 다음과 같습니다.

`/libs/granite/ui/components/foundation/form/*`

>[!NOTE]
>
>이러한 Granite UI 양식 필드는 다음과 같은 용도로 사용되므로 특별히 관심이 있습니다 [구성 요소](/help/sites-developing/developing-components.md).

>[!NOTE]
>
>필드에 대한 자세한 내용은 [Granite UI 설명서](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html).

Granite UI Foundation 프레임워크를 사용하여 Granite 구성 요소를 개발 및/또는 확장합니다. 여기에는 두 가지 요소가 있습니다.

* 서버측:

   * 기초 구성 요소의 컬렉션

      * foundation - 모듈, 복합, 레이아웃, 재사용 가능
      * 구성 요소 - Sling 구성 요소
   * 애플리케이션 개발에 도움이 되는 도움말


* 클라이언트측:

   * 하이퍼미디어 기반 UI를 통해 일반적인 상호 작용 패턴을 구현할 수 있도록 일부 어휘를 제공하는 clientlibs 컬렉션입니다(HTML 언어 확장)

일반 Granite UI 구성 요소 `field` 는 다음과 같이 두 개의 관심 영역으로 구성됩니다.

* `init.jsp`: 일반 처리를 처리합니다. 필드를 렌더링할 때 필요한 양식 값을 레이블 지정, 설명 및 제공합니다.
* `render.jsp`: 여기에서 필드의 실제 렌더링이 수행되며 사용자 지정 필드에 대해 재정의해야 합니다. 에 포함되어 있습니다. `init.jsp`.

자세한 내용은 [Granite UI 설명서 - 필드](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/components/foundation/form/field/index.html) 더 자세히 알고 싶으시면

예를 보려면 다음을 참조하십시오.

* `cqgems/customizingfield/components/colorpicker`

   * 제공 [코드 샘플](/help/sites-developing/developing-components-samples.md#code-sample-how-to-customize-dialog-fields)

* `granite/ui/components/foundation/form`

>[!NOTE]
>
>이 메커니즘은 JSP, i18n 및 XSS를 사용하므로 즉시 사용할 수 없습니다. 즉, 문자열을 국제화하고 이스케이프 처리해야 합니다. 다음 디렉토리에는 표준 인스턴스의 일반 필드가 포함되어 있으므로 참조로 사용할 수 있습니다.
>
>`/libs/granite/ui/components/foundation/form` directory

## 구성 요소에 대한 서버측 스크립트 만들기 {#creating-the-server-side-script-for-the-component}

사용자 지정 필드는 `render.jsp` 스크립트. 구성 요소에 대한 마크업을 제공합니다. JSP(즉, 렌더링 스크립트)를 마크업의 래퍼로 간주할 수 있습니다.

1. 를 사용하는 새 구성 요소를 만듭니다 `sling:resourceSuperType` 상속할 속성:

   `/libs/granite/ui/components/foundation/form/field`

1. 스크립트 재정의:

   `render.jsp`

   이 스크립트에서는 클라이언트가 생성된 요소와 상호 작용하는 방법을 알 수 있도록 하이퍼미디어 마크업(즉, 하이퍼미디어 가격을 포함하는 보강된 마크업)을 생성해야 합니다. 이렇게 하려면 Granite UI 서버측 코딩 스타일을 따라야 합니다.

   사용자 지정할 때 *반드시* 이행은 양식 값( `init.jsp`)를 사용하십시오.

   ```
   // Delivers the value of the field (read from the content)
   ValueMap vm = (ValueMap) request.getAttribute(Field.class.getName());
   vm.get("value, String.class");
   ```

   자세한 내용은 기본 Granite UI 필드 구현 을 참조하십시오. 예 `/libs/granite/ui/components/foundation/form/textfield`.

   >[!NOTE]
   >
   >현재 JSP는 HTL에서 쉽게 수행할 수 없는 구성 요소 간에 정보를 전달하는 데 매우 빈번한 스크립팅 방법입니다.

## 구성 요소에 대한 클라이언트 라이브러리 만들기 {#creating-the-client-library-for-the-component}

특정 클라이언트측 동작을 구성 요소에 추가하려면:

1. 범주의 clientlib 만들기 `cq.authoring.dialog`.
1. 범주의 clientlib 만들기 `cq.authoring.dialog` 그리고 `JS`/ `CSS` 안에 있어요

   을(를) 정의합니다 `JS`/ `CSS` clientlib 내부

   >[!NOTE]
   >
   >현재 Granite UI는 JS 동작을 추가하는 데 직접 사용할 수 있는 기본 제공 청취자나 후크를 제공하지 않습니다. 따라서 구성 요소에 JS 동작을 더 추가하려면 마크업 생성 중에 구성 요소에 지정하는 사용자 지정 클래스에 JS 후크를 구현해야 합니다.
