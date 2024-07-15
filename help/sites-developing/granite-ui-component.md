---
title: 새 Granite UI 필드 구성 요소 만들기
description: Granite UI는 필드라고 하는 양식에서 사용하도록 설계된 다양한 구성 요소를 제공합니다
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
exl-id: e4820330-2ee6-4eca-83fd-462aa0b83647
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '498'
ht-degree: 0%

---

# 새 Granite UI 필드 구성 요소 만들기{#creating-a-new-granite-ui-field-component}

Granite UI는 양식에서 사용할 수 있도록 디자인된 다양한 구성 요소를 제공합니다. 이러한 구성 요소는 Granite UI 어휘에서 *필드*&#x200B;라고 합니다. 표준 Granite 양식 구성 요소는 다음에서 사용할 수 있습니다.

`/libs/granite/ui/components/foundation/form/*`

>[!NOTE]
>
>이러한 Granite UI 양식 필드는 [구성 요소 대화 상자](/help/sites-developing/developing-components.md)에 사용되므로 특히 유용합니다.

>[!NOTE]
>
>필드에 대한 자세한 내용은 [Granite UI 설명서](https://developer.adobe.com/experience-manager/reference-materials/6-5/granite-ui/api/jcr_root/libs/granite/ui/index.html)를 참조하십시오.

Granite UI Foundation 프레임워크를 사용하여 Granite 구성 요소를 개발 및/또는 확장합니다. 여기에는 두 가지 요소가 있습니다.

* 서버측:

   * 기초 구성 요소 컬렉션

      * 기초 - 모듈식, 구성 가능, 레이어 가능, 재사용 가능
      * 구성 요소 - Sling 구성 요소

   * 애플리케이션 개발 지원 도우미

* 클라이언트측:

   * 하이퍼미디어 기반 사용자 인터페이스를 통해 일반적인 상호 작용 패턴을 달성하기 위해 일부 어휘(즉, HTML 언어의 확장)를 제공하는 clientlibs의 컬렉션입니다.

일반 Granite UI 구성 요소 `field`은(는) 두 개의 관심 파일로 구성됩니다.

* `init.jsp`: 일반 처리, 레이블 지정, 설명을 처리하고 필드를 렌더링할 때 필요한 양식 값을 제공합니다.
* `render.jsp`: 필드의 실제 렌더링이 수행되며 사용자 지정 필드에 대해 재정의해야 합니다. `init.jsp`에 포함됩니다.

자세한 내용은 [Granite UI 설명서 - 필드](https://developer.adobe.com/experience-manager/reference-materials/6-5/granite-ui/api/jcr_root/libs/granite/ui/components/foundation/form/field/index.html)를 참조하십시오.

예를 보려면 다음을 참조하십시오.

* `cqgems/customizingfield/components/colorpicker`

   * [코드 샘플](/help/sites-developing/developing-components-samples.md#code-sample-how-to-customize-dialog-fields)에서 제공

* `granite/ui/components/foundation/form`

>[!NOTE]
>
>이 메커니즘은 JSP를 사용하므로 i18n 및 XSS는 즉시 사용할 수 없습니다. 즉, 문자열을 인터내셔널리제이션하고 이스케이프 처리해야 합니다. 다음 디렉토리에는 표준 인스턴스의 일반 필드가 포함되어 있으므로 이를 참조로 사용할 수 있습니다.
>
>`/libs/granite/ui/components/foundation/form` 디렉터리

## 구성 요소에 대한 서버측 스크립트 만들기 {#creating-the-server-side-script-for-the-component}

사용자 지정된 필드는 구성 요소에 태그를 제공하는 `render.jsp` 스크립트만 재정의해야 합니다. JSP(즉, 렌더링 스크립트)는 마크업에 대한 래퍼로 간주할 수 있습니다.

1. `sling:resourceSuperType` 속성을 사용하여 다음 항목에서 상속할 구성 요소를 만듭니다.

   `/libs/granite/ui/components/foundation/form/field`

1. 스크립트 재정의:

   `render.jsp`

   이 스크립트에서는 클라이언트가 생성된 요소와 상호 작용하는 방법을 알 수 있도록 하이퍼미디어 마크업(즉, 하이퍼미디어 어포던스가 포함된 강화된 마크업)을 생성합니다. 이는 Granite UI 서버측 코딩 스타일을 따라야 합니다.

   사용자 지정할 때 *반드시*&#x200B;이 이행해야 하는 유일한 계약은 다음을 사용하여 요청에서 양식 값(`init.jsp`에서 초기화됨)을 읽는 것입니다.

   ```
   // Delivers the value of the field (read from the content)
   ValueMap vm = (ValueMap) request.getAttribute(Field.class.getName());
   vm.get("value, String.class");
   ```

   자세한 내용은 기본 Granite UI 필드(예: `/libs/granite/ui/components/foundation/form/textfield`)의 구현을 참조하십시오.

   >[!NOTE]
   >
   >현재 JSP가 기본 스크립팅 방법인데, 이는 HTL에서 한 구성 요소에서 다른 구성 요소로 정보를 전달하는 것(양식/필드의 컨텍스트에서 자주 사용됨)이 쉽지 않기 때문입니다.

## 구성 요소에 대한 클라이언트 라이브러리 만들기 {#creating-the-client-library-for-the-component}

구성 요소에 특정 클라이언트측 비헤이비어를 추가하려면 다음을 수행하십시오.

1. `cq.authoring.dialog` 범주의 clientlib을 만듭니다.
1. `cq.authoring.dialog` 범주의 clientlib을 만들고 그 안에 `JS`/ `CSS`을(를) 정의합니다.

   clientlib 내에서 `JS`/ `CSS`을(를) 정의합니다.

   >[!NOTE]
   >
   >현재 Granite UI는 JS 비헤이비어를 추가하는 데 직접 사용할 수 있는 기본 리스너 또는 후크를 제공하지 않습니다. 따라서 구성 요소에 JS 비헤이비어를 추가하려면 마크업을 생성하는 동안 구성 요소에 지정할 사용자 지정 클래스에 JS 후크를 구현해야 합니다.
