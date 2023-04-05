---
title: 템플릿
description: 템플릿은 새 페이지의 기초로 사용되는 페이지를 만들 때 사용됩니다.
uuid: 6fa3dafc-dfa1-42d8-b296-d4be57449411
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 7c723773-7c23-43d7-85dc-53e54556b648
legacypath: /content/docs/en/aem/6-1/develop/the-basics/templates
exl-id: 59f01bb1-4ff1-42b6-afc9-56d448b1f803
source-git-commit: 95638b6dd9527c567b38d8cd9da14633bd4142b5
workflow-type: tm+mt
source-wordcount: '931'
ht-degree: 2%

---

# 템플릿{#templates}

템플릿은 AEM의 다양한 지점에서 사용됩니다.

* [페이지를 만들 때 템플릿을 선택합니다](#templates-pages). 이 템플릿은 새 페이지의 기초로 사용됩니다. 템플릿은 페이지의 구조, 초기 컨텐츠 및 [구성 요소](/help/sites-authoring/default-components.md) 사용할 수 있습니다(디자인 속성).

* [컨텐츠 조각을 만들 때 템플릿도 선택합니다](#templates-content-fragments). 이 템플릿은 구조, 초기 요소 및 변형을 정의합니다.

다음 템플릿은 자세히 다룹니다.

* [페이지 템플릿 - 편집 가능](/help/sites-developing/page-templates-editable.md)
* [페이지 템플릿 - 정적](/help/sites-developing/page-templates-static.md)
* [컨텐츠 조각 템플릿](/help/sites-developing/content-fragment-templates.md)
* [적응형 템플릿 렌더링](/help/sites-developing/templates-adaptive-rendering.md)

## 템플릿 - 페이지 {#templates-pages}

이제 AEM에서는 페이지를 작성하는 두 가지 기본 유형의 템플릿을 제공합니다.

>[!NOTE]
>
>템플릿을 사용할 때 [페이지 만들기](/help/sites-authoring/managing-pages.md#creating-a-new-page)으로 설정되어 있는 경우, (페이지 작성자에 대한) 표시와 사용 중인 템플릿 유형이 표시되지 않습니다.

### 편집 가능한 템플릿 {#editable-templates}

이제 편집 가능한 템플릿은 AEM을 사용하여 개발하는 우수 사례로 간주됩니다.

편집 가능한 템플릿의 이점:

* 다음을 수행할 수 있습니다. [생성됨](/help/sites-authoring/templates.md#creating-a-new-template-template-author) 및 [편집됨](/help/sites-authoring/templates.md#editing-a-template-structure-template-author) 작성자

* 템플릿으로 만든 페이지에 대해 다음 사항을 정의할 수 있도록 이 도입되었습니다.

   * 구조
   * 초기 컨텐츠
   * 콘텐츠 정책

* 새 페이지가 만들어지면 페이지와 템플릿 간에 동적 연결이 유지됩니다. 이 연결은 템플릿 구조에 대한 변경 사항이 해당 템플릿으로 만든 페이지에 반영됨을 의미합니다. 초기 컨텐츠에 대한 변경 사항은 반영되지 않습니다.
* 컨텐츠 정책(템플릿 편집기에서 편집됨)을 사용하여 디자인 속성을 유지합니다(페이지 편집기 내에서 디자인 모드를 사용하지 않음).
* 아래에 저장됩니다. `/conf`
* 자세한 내용은 [편집 가능한 템플릿](/help/sites-developing/page-templates-editable.md) 추가 정보.

>[!NOTE]
>
>자세한 내용은 [편집 가능한 페이지 템플릿을 사용하여 Experience Manager 사이트 개발](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/page-authoring/template-editor-feature-video-use.html?lang=en).

### 정적 템플릿 {#static-templates}

정적 템플릿:

* 개발자가 정의하고 구성해야 합니다.
* 많은 버전에서 사용할 수 있었던 AEM의 원래 템플릿 시스템입니다.
* 정적 템플릿은 만들 페이지와 구조가 동일하지만 실제 컨텐츠가 없는 노드 계층 구조입니다.
* 페이지를 만들기 위해 복사되며, 이후에 동적 연결이 존재하지 않습니다.
* 사용 [디자인 모드](/help/sites-authoring/default-components-designmode.md) 디자인 속성을 유지합니다.
* 아래에 저장됩니다. `/apps`
* 자세한 내용은 [정적 템플릿](/help/sites-developing/page-templates-static.md) 추가 정보.

>[!NOTE]
>
>AEM 6.5부터는 정적 템플릿 사용이 권장되지 않습니다. 대신 편집 가능한 템플릿을 사용하십시오.
>
>[AEM 현대화](modernization-tools.md) 도구를 사용하면 정적 템플릿에서 편집 가능한 템플릿으로 마이그레이션할 수 있습니다.

### 템플릿 가용성 {#template-availability}

>[!CAUTION]
>
>AEM에서는 다음에 허용되는 템플릿을 제어하는 여러 속성을 제공합니다. **Sites**. 그러나 이러한 규칙을 결합하면 추적 및 관리가 어려운 복잡한 규칙이 만들어질 수 있습니다.
>
>따라서 다음을 정의하여 간단하게 시작할 것을 Adobe에서 권장합니다.
>
>* 유일한 `cq:allowedTemplates` 속성
>
>* 사이트 루트에서만
>
>예를 보려면 We.Retail 을 참조하십시오. `/content/we-retail/jcr:content`
>
>속성 `allowedPaths`, `allowedParents`, 및 `allowedChildren` 템플릿에 배치하여 보다 복잡한 규칙을 정의할 수도 있습니다. 그러나, 가능한 경우, *많이* 더 간단하게 `cq:allowedTemplates` 허용된 템플릿을 추가로 제한해야 하는 경우 사이트의 하위 섹션에 있는 속성입니다.
>
>또 다른 이점은 `cq:allowedTemplates` 속성은 작성자가 **고급** 의 탭 **페이지 속성**. 다른 템플릿 속성은 (표준) UI를 사용하여 업데이트할 수 없으므로 변경 때마다 개발자가 규칙과 코드 배포를 유지해야 합니다.

사이트 관리자 인터페이스에서 페이지를 만들 때 사용 가능한 템플릿 목록은 새 페이지의 위치와 각 템플릿에 지정된 배치 제한에 따라 다릅니다.

다음 속성은 템플릿 여부를 결정합니다 `T` 새 페이지를 페이지의 하위 페이지로 배치하기 위해 사용됩니다 `P`. 이러한 각 속성은 경로와의 일치에 사용되는 0개 이상의 정규 표현식을 포함하는 다중 값 문자열입니다.

* 다음 `cq:allowedTemplates` 속성 `jcr:content` 하위 노드 `P` 또는 의 상위 `P`.

* 다음 `allowedPaths` 속성 `T`.

* 다음 `allowedParents` 속성 `T`.

* 다음 `allowedChildren` 템플릿의 속성입니다. `P`.

평가는 다음과 같이 작동합니다.

* 비어 있지 않은 첫 번째 `cq:allowedTemplates` 다음으로 시작하는 페이지 계층 구조를 오름차순으로 하는 동안 속성이 발견되었습니다. `P` 의 경로와 일치합니다 `T`. 값이 일치하지 않으면 `T` 이 거부됩니다.

* If `T` 에는 비어 있지 않은 가 있습니다. `allowedPaths` 속성이지만 값이 의 경로와 일치하지 않습니다 `P`, `T` 이 거부됩니다.

* 위의 두 속성 모두 비어 있거나 존재하지 않는 경우 `T` 와 동일한 애플리케이션에 속하지 않는 한 거부됨 `P`. `T` 는 와 동일한 애플리케이션에 속합니다. `P` 및 가 있어야 합니다. `T` 은 경로 의 두 번째 수준 이름과 동일합니다 `P`. 예를 들어, 템플릿 `/apps/geometrixx/templates/foo` 는 페이지와 동일한 애플리케이션에 속합니다 `/content/geometrixx`.

* If `T` 에는 비어 있지 않은 가 있습니다. `allowedParents` 속성이지만 값이 의 경로와 일치하지 않습니다 `P`, `T` 이 거부됩니다.

* 템플릿의 `P` 에는 비어 있지 않은 가 있습니다. `allowedChildren` 속성이지만 값이 의 경로와 일치하지 않습니다 `T`, `T` 이 거부됩니다.

* 다른 경우에는 `T` 가 허용됩니다.

다음 다이어그램은 템플릿 평가 프로세스를 나타냅니다.

![chlimage_1-176](assets/chlimage_1-176.png)

#### 하위 페이지에 사용된 템플릿 제한 {#limiting-templates-used-in-child-pages}

특정 페이지에서 하위 페이지를 만드는 데 사용할 수 있는 템플릿을 제한하려면 `cq:allowedTemplates` 속성 `jcr:content` 노드 아래에 있는 노드 아래에 있는 템플릿 목록을 하위 페이지로 지정할 수 있습니다. 예를 들어, 목록의 각 값은 허용된 하위 페이지에 대한 템플릿의 절대 경로여야 합니다 `/apps/geometrixx/templates/contentpage`.

를 사용할 수 있습니다 `cq:allowedTemplates` 템플릿의 속성에 대한  `jcr:content` 이 구성을 이 템플릿을 사용하는 새로 만든 모든 페이지에 적용할 노드입니다.

예를 들어 템플릿 계층에 대한 제약 조건을 추가하려는 경우 다음을 사용할 수 있습니다 `allowedParents/allowedChildren` 템플릿의 속성입니다. 그런 다음 템플릿에서 만든 페이지를 T 템플릿에서 만든 페이지의 상위/1차 하위 구성요소로 명시적으로 지정할 수 있습니다.

## 템플릿 - 컨텐츠 조각 {#templates-content-fragments}

자세한 내용은 [컨텐츠 조각 템플릿](/help/sites-developing/content-fragment-templates.md).
