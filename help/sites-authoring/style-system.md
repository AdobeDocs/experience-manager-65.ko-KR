---
title: 스타일 시스템
description: 스타일 시스템을 사용하여 템플릿 작성자는 페이지에서 구성 요소를 편집할 때 콘텐츠 작성자가 선택할 수 있도록 구성 요소의 콘텐츠 정책에 스타일 클래스를 정의할 수 있습니다. 이러한 스타일은 보다 유연하게 사용할 수 있도록 구성 요소를 시각적으로 변형한 대체물일 수 있습니다.
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
exl-id: 1772368a-f5c9-440c-a92a-0f1d34cc4bf8
solution: Experience Manager, Experience Manager Sites
feature: Authoring
role: User,Admin,Architect,Developer
source-git-commit: 9a3008553b8091b66c72e0b6c317573b235eee24
workflow-type: tm+mt
source-wordcount: '1297'
ht-degree: 84%

---

# 스타일 시스템{#style-system}

스타일 시스템을 사용하여 템플릿 작성자는 페이지에서 구성 요소를 편집할 때 콘텐츠 작성자가 선택할 수 있도록 구성 요소의 콘텐츠 정책에 스타일 클래스를 정의할 수 있습니다. 이러한 스타일은 구성 요소를 보다 유연하게 사용할 수 있도록 구성 요소를 시각적으로 변형한 대체물일 수 있습니다.

따라서 각 스타일에 대해 사용자 정의 구성 요소를 개발하거나 이러한 스타일 기능을 사용하도록 구성 요소 대화 상자를 사용자 정의할 필요가 없습니다. 또한 AEM 백엔드 개발 없이 콘텐츠 작성자의 요구에 맞게 빠르고 쉽게 조정될 수 있는 재사용 가능한 구성 요소가 생성되게 됩니다.

## 사용 사례 {#use-case}

템플릿 작성자는 콘텐츠 작성자에 대해 구성 요소가 작동하는 방식을 구성해야 할 뿐만 아니라 구성 요소의 몇 가지 대체 시각적 변형을 구성해야 합니다.

마찬가지로 콘텐츠 작성자는 콘텐츠를 구성하고 배열해야 할 뿐만 아니라 시각적으로 표시되는 방법도 선택해야 합니다.

스타일 시스템은 템플릿 작성자 및 콘텐츠 작성자 요구 사항을 둘 다 충족할 수 있는 통합된 솔루션을 제공합니다.

* 템플릿 작성자는 구성 요소의 콘텐츠 정책에 스타일 클래스를 정의할 수 있습니다.
* 그런 다음 콘텐츠 작성자는 페이지에서 구성 요소를 편집하여 해당 스타일을 적용할 때 드롭다운에서 이러한 클래스를 선택할 수 있습니다.

그러면 해당 스타일 클래스가 구성 요소의 데코레이션 래퍼 요소에 삽입되므로 구성 요소 개발자는 CSS 규칙을 제공하는 것 이상의 스타일 처리를 수행할 필요가 없습니다.

## 개요 {#overview}

스타일 시스템을 사용할 경우 일반적으로 다음 양식이 사용됩니다.

1. 웹 디자이너는 구성 요소의 다른 시각적 변형을 만듭니다.

1. HTML 개발자에게는 구현을 위해 구성 요소의 HTML 출력과 원하는 시각적 변형이 제공됩니다.

1. HTML 개발자는 각 시각적 변형에 해당하며 구성 요소를 래핑하는 요소에 삽입해야 하는 CSS 클래스를 정의합니다.

1. HTML 개발자는 정의된 대로 표시되도록 각 시각적 변형에 해당하는 CSS 코드(및 선택적으로 JS 코드)를 구현합니다.

1. AEM 개발자는 제공된 CSS(및 선택적 JS)를 [클라이언트 라이브러리](/help/sites-developing/clientlibs.md)에 배치하고 배포합니다.

1. AEM 개발자 또는 템플릿 작성자는 페이지 템플릿을 구성하고, 스타일이 지정된 각 구성 요소의 정책을 편집하며, 정의된 CSS 클래스를 추가하고, 각 스타일에 대해 사용자에게 익숙한 이름을 지정하고, 결합할 수 있는 스타일을 지정합니다.

1. 그러면 AEM 페이지 작성자는 구성 요소 도구 모음의 스타일 메뉴를 통해 페이지 편집기에서 디자인된 스타일을 선택할 수 있습니다.

AEM에서는 마지막 세 단계만 실제로 수행됩니다. 즉, 필요한 CSS 및 JavaScript의 모든 개발을 AEM 없이도 수행할 수 있습니다.

실제로 스타일을 구현할 때는 AEM에서 배포를 수행하고 원하는 템플릿의 구성 요소 내에서 선택하기만 하면 됩니다.

다음 다이어그램은 스타일 시스템의 아키텍처를 보여 줍니다.

![aem-style-system](assets/aem-style-system.png)

## 사용 {#use}

이 기능을 보여 주기 위해 핵심 구성 요소의 [제목 구성 요소](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-wknd-tutorial-develop/overview.html?lang=ko)에 대한 [WKND](https://www.adobe.com/go/aem_cmp_title_v2_kr)의 구현을 예로 사용할 것입니다.

다음 섹션 [콘텐츠 작성자](#as-a-content-author) 및 [템플릿 작성자](#as-a-template-author)에서는 WKND의 스타일 시스템을 사용하여 스타일 시스템의 기능을 테스트하는 방법을 설명합니다.

사용자 고유의 구성 요소에 대해 스타일 시스템을 사용하려면 다음 작업을 수행하십시오.

1. [개요](#overview) 섹션에서 설명한 대로 CSS를 클라이언트 라이브러리로 설치합니다.
1. [템플릿 작성자](#as-a-template-author) 섹션에 설명된 대로 콘텐츠 작성자가 사용할 수 있도록 하려는 CSS 클래스를 구성합니다.
1. 그러면 콘텐츠 작성자는 [콘텐츠 작성자](#as-a-content-author) 섹션에 설명된 대로 스타일을 사용할 수 있습니다.

### 콘텐츠 작성자 {#as-a-content-author}

1. WKND 프로젝트를 설치한 후 `http://<host>:<port>/sites.html/content/wknd/language-masters/en`에서 WKND의 영어 마스터 홈 페이지로 이동하여 페이지를 편집합니다.
1. 페이지 아래쪽에서 **제목** 구성 요소 선택

   ![작성자를 위한 스타일 시스템](assets/style-system-author.png)

1. **List** 구성 요소의 도구 모음에서 **스타일** 단추를 클릭하여 스타일 메뉴를 열고 구성 요소의 모양을 변경합니다.

   ![스타일 선택](assets/style-system-author2.png)

   >[!NOTE]
   >
   >이 예에서 **색상** 스타일(**검은색**, **흰색** 및 **회색**)은 상호 배타적이지만 **스타일** 옵션(**밑줄**, **오른쪽 정렬** 및 **미니 공간**)은 조합할 수 있습니다. 이는 [템플릿에서 템플릿 작성자로 구성](#as-a-template-author)할 수 있습니다.

### 템플릿 작성자 {#as-a-template-author}

1. `http://<host>:<port>/sites.html/content/wknd/language-masters/en`에서 WKND의 영어 마스터 홈 페이지를 편집하는 동안 **페이지 정보 > 템플릿 편집**&#x200B;을 통해 페이지의 템플릿을 편집하십시오.

   ![템플릿 편집](assets/style-system-edit-template.png)

1. 구성 요소의 **정책** 버튼을 탭하거나 클릭하여 **제목** 구성 요소의 정책을 편집합니다.

   ![정책 편집](assets/style-system-edit-policy.png)

1. 속성의 스타일 탭에서 스타일이 구성된 방식을 확인할 수 있습니다.

   ![속성 편집](assets/style-system-properties.png)

   * **그룹 이름:** 구성 요소의 스타일을 구성할 때 콘텐츠 작성자에게 표시될 스타일을 스타일 메뉴에서 함께 그룹화할 수 있습니다.
   * **스타일을 결합할 수 있음:** 해당 그룹 내의 여러 스타일을 은 한꺼번에 선택할 수 있습니다.
   * **스타일 이름:** 구성 요소의 스타일을 구성할 때 콘텐츠 작성자에게 표시할 스타일에 대한 설명입니다.
   * **CSS 클래스:** 스타일과 연관된 CSS 클래스의 실제 이름입니다.

   끌기 핸들을 사용하여 그룹의 순서와 그룹 내의 스타일을 정렬합니다. 추가 또는 삭제 아이콘을 사용하여 그룹 내에서 그룹 또는 스타일을 추가하거나 제거합니다.

>[!CAUTION]
>
>구성 요소 정책의 스타일 속성으로 구성된 CSS 클래스(및 필요한 JavaScript)는 [클라이언트 라이브러리](/help/sites-developing/clientlibs.md)(으)로 배포해야 작동합니다.

## 설정 {#setup}

핵심 구성 요소 버전 2 이상은 스타일 시스템을 활용할 수 있도록 전체적으로 활성화되며 추가 구성이 필요 없습니다.

다음 단계는 사용자 정의 구성 요소에 대해 스타일 시스템을 활성화하거나 [편집 대화 상자에서 옵션 스타일 탭을 활성화](#enable-styles-tab-edit)하기만 하면 됩니다.

### 디자인 대화 상자에서 스타일 탭 활성화 {#enable-styles-tab-design}

구성 요소가 AEM의 스타일 시스템을 사용하고 디자인 대화 상자에 스타일 탭을 표시하도록 하려면 구성 요소 개발자가 다음 설정이 있는 스타일 탭을 구성 요소에 포함해야 합니다.

* `path = "/mnt/overlay/cq/gui/components/authoring/dialog/style/tab_design/styletab"`
* `sling:resourceType = "granite/ui/components/coral/foundation/include"`

구성 요소를 구성하면 페이지 작성자가 구성한 스타일이 AEM에서 편집 가능한 모든 구성 요소를 자동으로 감싸는 데코레이션 요소에 AEM에서 자동으로 삽입됩니다. 구성 요소 자체는 이 작업을 수행하기 위해 다른 작업을 수행할 필요가 없습니다.

### 편집 대화 상자에서 스타일 탭 활성화 {#enable-styles-tab-edit}

이제 AEM 버전 6.5.3.0부터 편집 대화 상자의 선택 사항 스타일 탭을 사용할 수 있습니다. 디자인 대화 상자 탭과 달리 편집 대화 상자의 탭은 스타일 시스템이 작동하는 데 꼭 필요한 것은 아니지만 콘텐츠 작성자가 스타일을 설정할 수 있는 선택 가능한 대체 인터페이스입니다.

편집 대화 상자 탭은 디자인 대화 상자 탭과 유사한 방식으로 포함될 수 있습니다.

* `path = "/mnt/overlay/cq/gui/components/authoring/dialog/style/tab_edit/styletab"`
* `sling:resourceType = "granite/ui/components/coral/foundation/include"`

>[!NOTE]
>
>편집 대화 상자의 스타일 탭은 기본적으로 활성화되어 있지 않습니다.

### 요소 이름을 갖는 스타일 {#styles-with-element-names}

개발자는 `cq:styleElements` 문자열 배열 속성을 사용하여 구성 요소의 스타일에 대해 허용되는 요소 이름 목록을 구성할 수도 있습니다. 그러면 템플릿 작성자는 디자인 대화 상자의 정책 스타일 탭에서 각 스타일에 대해 설정할 요소 이름을 선택할 수도 있습니다. 다음은 래퍼 요소의 요소 이름을 설정합니다.

이 속성은 `cq:Component` 노드에서 설정됩니다. 예:

* `/apps/<yoursite>/components/content/list@cq:styleElements=[div,section,span]`

>[!CAUTION]
>
>결합할 수 있는 스타일에 대해서는 요소 이름을 정의하지 마십시오. 여러 요소 이름이 정의된 경우 우선 순위 순서는 다음과 같습니다.
>
>1. HTL이 모든 것에 우선합니다. `data-sly-resource="${'path/to/resource' @ decorationTagName='span'}`
>1. 그런 다음 여러 활성 스타일 중에서 구성 요소의 정책에 구성된 스타일 목록의 첫 번째 스타일이 적용됩니다.
>1. 마지막으로 구성 요소의 `cq:htmlTag`/ `cq:tagName`은 폴백 값으로 간주됩니다.
>

스타일 이름을 정의하는 기능은 레이아웃 컨테이너 또는 콘텐츠 조각 구성 요소와 같은 매우 일반적인 구성 요소에 추가적인 의미를 제공하는 데 유용합니다.

예를 들어 레이아웃 컨테이너에 `<main>`, `<aside>`, `<nav>` 등의 의미 체계를 부여할 수 있습니다.
