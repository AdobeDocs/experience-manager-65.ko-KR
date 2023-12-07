---
title: 템플릿
description: 템플릿은 새 페이지의 기반으로 사용되는 페이지를 만들 때 사용됩니다.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
legacypath: /content/docs/en/aem/6-1/develop/the-basics/templates
exl-id: 59f01bb1-4ff1-42b6-afc9-56d448b1f803
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '924'
ht-degree: 0%

---

# 템플릿{#templates}

템플릿은 AEM의 다양한 지점에서 사용됩니다.

* [페이지를 만들 때 템플릿을 선택합니다](#templates-pages). 이 템플릿은 새 페이지의 기반으로 사용됩니다. 템플릿은 페이지 구조, 초기 콘텐츠 및 [구성 요소](/help/sites-authoring/default-components.md) 사용할 수 있습니다(디자인 속성).

* [콘텐츠 조각을 만들 때 템플릿도 선택합니다](#templates-content-fragments). 이 템플릿은 구조, 초기 요소 및 변형을 정의합니다.

다음 템플릿에 대해 자세히 설명합니다.

* [페이지 템플릿 - 편집 가능](/help/sites-developing/page-templates-editable.md)
* [페이지 템플릿 - 정적](/help/sites-developing/page-templates-static.md)
* [콘텐츠 조각 템플릿](/help/sites-developing/content-fragment-templates.md)
* [적응형 템플릿 렌더링](/help/sites-developing/templates-adaptive-rendering.md)

## 템플릿 - 페이지 {#templates-pages}

이제 AEM에서는 페이지를 만들기 위한 두 가지 기본 템플릿 유형을 제공합니다.

>[!NOTE]
>
>템플릿 사용 시 [페이지 만들기](/help/sites-authoring/managing-pages.md#creating-a-new-page), 페이지 작성자에게는 가시적인 차이가 없으며 사용 중인 템플릿 유형이 표시되지 않습니다.

### 편집 가능한 템플릿 {#editable-templates}

이제 편집 가능한 템플릿은 AEM을 사용하여 개발하는 우수 사례로 간주됩니다.

편집 가능한 템플릿의 장점:

* 다음과 같을 수 있습니다. [생성됨](/help/sites-authoring/templates.md#creating-a-new-template-template-author) 및 [편집됨](/help/sites-authoring/templates.md#editing-a-template-structure-template-author) 작성자에 의해 제어됩니다.

* 템플릿으로 만든 페이지에 대해 다음 사항을 정의할 수 있도록 도입되었습니다.

   * 구조
   * 초기 콘텐츠
   * 콘텐츠 정책

* 새 페이지가 만들어지면 페이지와 템플릿 간에 동적 연결이 유지됩니다. 이 연결은 템플릿 구조의 변경 사항이 해당 템플릿으로 만든 페이지에 반영됨을 의미합니다. 초기 콘텐츠에 대한 변경 사항은 반영되지 않습니다.
* 콘텐츠 정책(템플릿 편집기에서 편집됨)을 사용하여 디자인 속성을 유지합니다(페이지 편집기 내에서 디자인 모드를 사용하지 않음).
* 아래에 저장됩니다. `/conf`
* 다음을 참조하십시오 [편집 가능한 템플릿](/help/sites-developing/page-templates-editable.md) 추가 정보.

>[!NOTE]
>
>다음을 참조하십시오 [편집 가능한 페이지 템플릿을 사용하여 Experience Manager 사이트 개발](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/page-authoring/template-editor-feature-video-use.html?lang=en).

### 정적 템플릿 {#static-templates}

정적 템플릿:

* 개발자가 정의 및 구성해야 합니다.
* 여러 버전에서 사용할 수 있었던 AEM의 원래 템플릿 시스템입니다.
* 정적 템플릿은 만들 페이지와 구조가 동일하지만 실제 컨텐츠는 없는 노드의 계층입니다.
* 복사되어 페이지를 만듭니다. 이후에 동적 연결이 존재하지 않습니다.
* 사용 [디자인 모드](/help/sites-authoring/default-components-designmode.md) 디자인 속성을 유지합니다.
* 아래에 저장됩니다. `/apps`
* 다음을 참조하십시오 [정적 템플릿](/help/sites-developing/page-templates-static.md) 추가 정보.

>[!NOTE]
>
>AEM 6.5부터는 정적 템플릿을 사용하는 것이 우수 사례로 간주되지 않습니다. 대신 편집 가능한 템플릿을 사용하십시오.
>
>[AEM 현대화](modernization-tools.md) 도구를 사용하면 정적 템플릿에서 편집 가능한 템플릿으로 마이그레이션할 수 있습니다.

### 템플릿 가용성 {#template-availability}

>[!CAUTION]
>
>AEM에서는 허용되는 템플릿을 제어할 여러 속성을 제공합니다. **사이트**. 하지만 이를 결합하면 추적 및 관리가 어려운 복잡한 규칙이 발생할 수 있다.
>
>따라서 Adobe은 다음을 정의하여 단순하게 시작하는 것을 권장합니다.
>
>* 만 `cq:allowedTemplates` 속성
>
>* 사이트 루트에서만
>
>예를 들어 We.Retail: `/content/we-retail/jcr:content`
>
>속성 `allowedPaths`, `allowedParents`, 및 `allowedChildren` 템플릿에 배치하여 더 정교한 규칙을 정의할 수도 있습니다. 그러나 가능한 경우 다음과 같습니다. *많이* 간단히 추가 정의 `cq:allowedTemplates` 허용된 템플릿을 추가로 제한할 필요가 있는 경우 사이트의 하위 섹션에 있는 속성.
>
>추가적인 이점은 `cq:allowedTemplates` 의 작성자는 속성을 업데이트할 수 있습니다. **고급** 의 탭 **페이지 속성**. 다른 템플릿 속성은 (표준) UI를 사용하여 업데이트할 수 없으므로 개발자는 모든 변경 사항에 대한 규칙 및 코드 배포를 유지 관리해야 합니다.

사이트 관리 인터페이스에서 페이지를 만들 때 사용 가능한 템플릿 목록은 새 페이지의 위치와 각 템플릿에 지정된 배치 제한에 따라 다릅니다.

다음 속성은 템플릿 여부를 결정합니다 `T` 는 새 페이지를 페이지의 하위 페이지로 배치하는 데 사용됩니다 `P`. 이러한 각 속성은 경로와의 일치에 사용되는 0개 이상의 정규 표현식을 포함하는 다중 값 문자열입니다.

* 다음 `cq:allowedTemplates` 의 속성 `jcr:content` 의 하위 노드 `P` 또는 의 상위 항목 `P`.

* 다음 `allowedPaths` 다음의 속성 `T`.

* 다음 `allowedParents` 다음의 속성 `T`.

* 다음 `allowedChildren` 템플릿 속성 `P`.

평가는 다음과 같이 작동합니다.

* 비어 있지 않은 첫 번째 `cq:allowedTemplates` 다음으로 시작하는 페이지 계층 구조를 오름차순으로 계산하는 동안 속성을 찾았습니다. `P` 다음 경로에 대해 일치함: `T`. 일치하는 값이 없으면 `T` 거부되었습니다.

* If `T` 이(가) 비어 있지 않습니다. `allowedPaths` 속성이지만 다음 경로와 일치하는 값은 없습니다. `P`, `T` 거부되었습니다.

* 위의 두 속성이 모두 비어 있거나 존재하지 않는 경우 `T` 와 동일한 애플리케이션에 속해 있지 않으면 거부됩니다. `P`. `T` 은(는) 과 동일한 애플리케이션에 속합니다. `P` 경로의 두 번째 수준 이름인 경우 및 `T` 은 경로의 두 번째 수준 이름과 동일합니다. `P`. (예: 템플릿) `/apps/geometrixx/templates/foo` 은(는) 페이지와 동일한 애플리케이션에 속합니다 `/content/geometrixx`.

* If `T` 이(가) 비어 있지 않습니다. `allowedParents` 속성이지만 다음 경로와 일치하는 값은 없습니다. `P`, `T` 거부되었습니다.

* 다음의 템플릿인 경우 `P` 이(가) 비어 있지 않습니다. `allowedChildren` 속성이지만 다음 경로와 일치하는 값은 없습니다. `T`, `T` 거부되었습니다.

* 다른 모든 경우에는 `T` 허용됩니다.

다음 다이어그램은 템플리트 평가 프로세스를 보여 줍니다.

![chlimage_1-176](assets/chlimage_1-176.png)

#### 하위 페이지에 사용되는 템플릿 제한 {#limiting-templates-used-in-child-pages}

주어진 페이지에서 하위 페이지를 만드는 데 사용할 수 있는 템플릿을 제한하려면 `cq:allowedTemplates` 다음의 속성 `jcr:content` 하위 페이지로 허용할 템플릿 목록을 지정할 페이지의 노드입니다. 목록의 각 값은 허용된 하위 페이지에 대한 템플릿의 절대 경로여야 합니다(예: ). `/apps/geometrixx/templates/contentpage`.

다음을 사용할 수 있습니다. `cq:allowedTemplates` 템플릿의 속성  `jcr:content` 이 템플릿을 사용하는 새로 만든 모든 페이지에 이 구성을 적용할 노드

예를 들어 템플릿 계층에 대해 제한을 더 추가하려면 `allowedParents/allowedChildren` 템플릿에 있는 속성입니다. 그런 다음 템플릿 T에서 만든 페이지가 템플릿 T에서 만든 페이지의 상위/하위 페이지가 되도록 명시적으로 지정할 수 있습니다.

## 템플릿 - 콘텐츠 조각 {#templates-content-fragments}

다음을 참조하십시오 [콘텐츠 조각 템플릿](/help/sites-developing/content-fragment-templates.md).
