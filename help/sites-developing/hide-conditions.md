---
title: 조건 숨기기 사용
description: 구성 요소 리소스의 렌더링 여부를 판별하기 위해 숨기기 조건을 사용할 수 있습니다.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: components
content-type: reference
exl-id: 65f5d5e1-ac11-4a3c-8a51-ce06a741c264
source-git-commit: 69346a710708ee659ee97e9fdc193c8ea2658fe6
workflow-type: tm+mt
source-wordcount: '633'
ht-degree: 2%

---

# 조건 숨기기 사용 {#using-hide-conditions}

구성 요소 리소스의 렌더링 여부를 판별하기 위해 숨기기 조건을 사용할 수 있습니다. 템플릿 작성자가 핵심 구성 요소를 구성하는 경우가 이에 대한 예입니다 [목록 구성 요소](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/list.html?lang=en) 다음에서 [템플릿 편집기](/help/sites-authoring/templates.md) 및 은 하위 페이지를 기반으로 목록을 작성하는 옵션을 비활성화하기로 결정합니다. 디자인 대화 상자에서 이 옵션을 비활성화하면 목록 구성 요소가 렌더링될 때 숨기기 조건이 평가되고 하위 페이지 표시 옵션이 표시되지 않도록 속성이 설정됩니다.

## 개요 {#overview}

대화 상자는 사용자가 원하는 옵션의 일부만 사용할 수 있는 다양한 옵션으로 복잡해질 수 있습니다. 이로 인해 사용자에게 압도적인 사용자 인터페이스 경험이 제공될 수 있습니다.

관리자, 개발자 및 수퍼 유저는 숨기기 조건을 사용하여 규칙 세트에 따라 리소스를 숨길 수 있습니다. 이 기능을 사용하면 작성자가 콘텐츠를 편집할 때 표시할 리소스를 결정할 수 있습니다.

>[!NOTE]
>
>표현식을 기반으로 리소스를 숨기더라도 ACL 권한은 대체되지 않습니다. 컨텐츠는 편집 가능 상태로 유지되지만 표시되지 않습니다.

## 구현 및 사용 세부 정보 {#implementation-and-usage-details}

`com.adobe.granite.ui.components.FilteringResourceWrapper` 은(는) 의 존재 및 값을 기반으로 리소스를 필터링합니다. `granite:hide` 속성, 필터링할 필드에 위치합니다. 구현 `/libs/cq/gui/components/authoring/dialog/dialog.jsp` 의 인스턴스를 포함합니다. `FilteringResourceWrapper.`

이 구현은 Granite를 사용합니다 [ELResolver API](https://developer.adobe.com/experience-manager/reference-materials/6-5/granite-ui/api/jcr_root/libs/granite/ui/docs/server/el.html) 및 추가 `cqDesign` ExpressionCustomizer를 통한 사용자 지정 변수입니다.

다음은 다음 중 하나에 있는 디자인 노드에서 숨기기 조건의 몇 가지 예입니다. `etc/design` 또는 을 콘텐츠 정책으로 사용하십시오.

```
${cqDesign.myProperty}
${!cqDesign.myProperty}
${cqDesign.myProperty == 'someText'}
${cqDesign.myProperty != 'someText'}
${cqDesign.myProperty == true}
${cqDesign.myProperty == true}
${cqDesign.property1 == 'someText' && cqDesign.property2 || cqDesign.property3 != 1 || header.myHeader}
```

숨기기 표현식을 정의할 때는 다음 사항에 유의하십시오.

* 속성이 유효하려면 속성이 발견되는 범위를 표현해야 합니다(예: `cqDesign.myProperty`).
* 값은 읽기 전용입니다.
* 함수(필요한 경우)는 서비스에서 제공하는 지정된 세트로 제한해야 합니다.

## 예 {#example}

숨기기 조건의 예는 AEM 및 [핵심 구성 요소](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html) 특히. 예를 들어 [목록 핵심 구성 요소](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/list.html?lang=en).

[템플릿 편집기 사용](/help/sites-authoring/templates.md)템플릿 작성자는 디자인 대화 상자에서 페이지 작성자가 사용할 수 있는 목록 구성 요소의 옵션을 정의할 수 있습니다. 정적 목록, 하위 페이지 목록, 태그가 지정된 페이지 목록 등을 허용할지 여부와 같은 옵션을 활성화하거나 비활성화할 수 있습니다.

템플릿 작성자가 하위 페이지 옵션을 비활성화하도록 선택하면 디자인 속성이 설정되고 숨기기 조건이 평가되어 페이지 작성자에 대해 옵션이 렌더링되지 않습니다.

1. 기본적으로 페이지 작성자는 옵션을 선택하여 목록 핵심 구성 요소를 사용하여 하위 페이지를 사용하는 목록을 빌드할 수 있습니다 **하위 페이지**.

   ![chlimage_1-218](assets/chlimage_1-218.png)

1. 목록 핵심 구성 요소의 디자인 대화 상자에서 템플릿 작성자는 옵션을 선택할 수 있습니다 **하위 항목 비활성화** 하위 페이지를 기반으로 목록을 생성하는 옵션이 페이지 작성자에게 표시되지 않도록 하기 위해

   ![chlimage_1-219](assets/chlimage_1-219.png)

1. 정책 노드는 `/conf/we-retail/settings/wcm/policies/weretail/components/content/list` 속성 포함 `disableChildren` 을 로 설정 `true`.
1. 숨기기 조건은 의 값으로 정의됩니다. `granite:hide` 대화 상자 속성 노드의 속성 `/conf/we-retail/settings/wcm/policies/weretail/components/content/list`

   ![chlimage_1-220](assets/chlimage_1-220.png)

1. 값: `disableChildren` 디자인 구성 및 표현식에서 가져옵니다. `${cqDesign.disableChildren}` 다음으로 평가: `false`즉, 옵션이 구성 요소의 일부로 렌더링되지 않습니다.

   숨기기 표현식을 의 값으로 볼 수 있습니다. `granite:hide` 속성 [GitHub의 여기](https://github.com/adobe/aem-core-wcm-components/blob/main/content/src/content/jcr_root/apps/core/wcm/components/list/v1/list/_cq_dialog/.content.xml#L40).

1. 옵션 **하위 페이지** 목록 구성 요소를 사용할 때 가 더 이상 페이지 작성자에 대해 렌더링되지 않습니다.

   ![chlimage_1-221](assets/chlimage_1-221.png)
