---
title: 페이지 생성 및 구성
description: AEM으로 페이지를 생성 및 관리하는 방법
translation-type: tm+mt
source-git-commit: 90364cdf6044616d43c1851b3def9b1f063449ca
workflow-type: tm+mt
source-wordcount: '2523'
ht-degree: 97%

---


# 페이지 생성 및 구성 {#creating-and-organizing-pages}

이 섹션에서는 해당 페이지에 [컨텐츠를 만들 수](/help/sites-authoring/editing-content.md) 있도록 AEM(Adobe Experience Manager)으로 페이지를 만들고 관리하는 방법을 설명합니다.

>[!NOTE]
>
>생성, 복사, 이동, 편집, 삭제와 같은 작업을 페이지에서 수행하기 위해서는 계정에 [적절한 액세스 권한](/help/sites-administering/security.md)과 [사용 권한](/help/sites-administering/security.md#permissions)이 있어야 합니다. 
>
>문제가 발생하면 시스템 관리자에게 문의하십시오.

>[!NOTE]
>
>페이지를 보다 효율적으로 구성할 수 있도록 해주고 웹 사이트 콘솔에서 사용할 수 있는 다양한 [키보드 단축키](/help/sites-authoring/keyboard-shortcuts.md)가 있습니다.

## 웹 사이트 구성 {#organizing-your-website}

작성자는 AEM 내에서 웹 사이트를 구성해야 합니다. 이 작업에는 컨텐츠 페이지 생성이 포함되며 이 페이지에 대한 이름 지정 작업도 포함되어 있어서

* 작성자가 작성 환경에서 페이지를 쉽게 찾을 수 있습니다.
* 사이트 방문자가 게시 환경에서 페이지를 쉽게 찾을 수 있습니다.

컨텐츠 구성에 도움이 되도록 [폴더](#creating-a-new-folder)를 사용할 수도 있습니다.

웹 사이트의 구조는 컨텐츠 페이지를 담는 트리 구조로 생각할 수 있습니다. 이 컨텐츠 페이지의 이름은 URL을 구성하는 데 사용됩니다. 반면에 제목은 페이지 컨텐츠가 표시될 때 표시됩니다.

다음은 하이킹 요약 페이지(`desert-sky-shorts`)가 액세스되는 We.Retail 사이트의 예제를 보여줍니다.

* 작성자 환경
   `https://localhost:4502/editor.html/content/we-retail/us/en/products/equipment/hiking/desert-sky-shorts.html`

* 게시 환경
   `https://localhost:4503/content/we-retail/us/en/products/equipment/hiking/desert-sky-shorts.html`

인스턴스의 구성에 따라서는 게시 환경에서 `/content`의 사용은 선택 사항일 수 있습니다.

```xml
 /content
 /we-retail
  /us
   /en
    /products
     /equipment
      /hiking
       /desert-sky-shorts
       /hiking-poles
       /...
      /running...
      /surfing...
      /...
     /seasonal...
     /...
    /about-us
    /experience
    /...
   /es...
  /de...
  /fr...
  /...
 /...
```

이 구조가 표시되는 **사이트** 콘솔에서는 [웹 사이트의 페이지를 모두 탐색](/help/sites-authoring/basic-handling.md#navigating)하고 페이지에서 작업을 수행할 수 있습니다. 새 사이트와 [새 페이지](#creating-a-new-page)를 만들 수도 있습니다.

어떤 지점에서든, 헤더 막대의 탐색 표시를 통해 위쪽 분기를 볼 수 있습니다.

![caop-01](assets/caop-01.png)

### 페이지 이름 지정 규칙 {#page-naming-conventions}

새 페이지를 만드는 경우 다음과 같은 두 개의 주요 필드가 있습니다.

* **[제목](#title)**:

   * 콘솔에서 사용자에게 표시되고, 편집할 때 페이지 컨텐츠 상단에 표시됩니다.
   * 이 필드는 선택 사항입니다.

* **[이름](#name)**:

   * URI를 생성하는 데 사용됩니다.
   * 이 필드에 대한 사용자 입력은 선택 사항입니다. 지정하지 않을 경우 이름이 제목에서 파생됩니다. 자세한 내용은 [페이지 이름 제한 및 우수 사례](/help/sites-authoring/managing-pages.md#page-name-restrictions-and-best-practices) 섹션을 참조하십시오.

#### 페이지 이름 제한 및 우수 사례 {#page-name-restrictions-and-best-practices}

페이지 **제목** 및 **이름**&#x200B;은 별도로 작성할 수 있지만 관련되어 있습니다.

* 페이지를 생성할 때 **제목** 필드만 필요합니다. 페이지 생성 시 **이름**&#x200B;을 제공하지 않으면 AEM은 제목의 처음 64자에서 이름을 생성합니다(아래에 작성된 유효성 검사 관찰). 짧은 페이지 이름에 대한 우수 사례를 지원하기 위해 처음 64자만 사용됩니다.

* 작성자가 페이지 이름을 수동으로 지정하는 경우 64자 제한이 적용되지 않지만, 페이지 이름 길이에 대한 다른 기술 제한 사항은 적용될 수 있습니다.

>[!NOTE]
>
>페이지 이름을 정의할 때 되도록이면 간단하게 지정하되, 함축적이며 기억하기 쉽게 지정하여 독자가 쉽게 이해할 수 있도록 하는 것이 좋습니다. 자세한 내용은 `title` 요소에 대한 [W3C 스타일 가이드](https://www.w3.org/Provider/Style/TITLE.html)를 참조하십시오.
>
>일부 브라우저(예: 이전 버전의 IE)는 특정 길이까지만 URL을 허용하므로 기술적인 이유로 페이지 이름을 짧게 유지하는 경우도 있습니다.

새 페이지를 만들 때 AEM은 AEM 및 JCR에서 지정한 규칙](/help/sites-developing/naming-conventions.md)에 따라 페이지 이름을 확인합니다.[

허용되는 최소 문자는 다음과 같습니다.

* &#39;a&#39; - &#39;z&#39;
* &#39;A&#39; - &#39;Z&#39;
* &#39;0&#39; - &#39;9&#39;
* `_`(밑줄)
* `-`(하이픈/빼기)

허용되는 모든 문자에 대한 전체 상세 정보는 [이름 지정 규칙](/help/sites-developing/naming-conventions.md)에서 찾을 수 있습니다.

>[!NOTE]
>
>AEM이 [MongoMK 지속성 관리자 배포](/help/sites-deploying/recommended-deploys.md)에서 실행 중인 경우, 페이지 이름은 150자로 제한됩니다.

#### 제목 {#title}

새 페이지를 만들 때 페이지 **제목**&#x200B;만 제공하면 AEM은 이 문자열에서 페이지 **이름**[을 파생하고 AEM 및 JCR에서 지정한 규칙에 따라 이름을 확인합니다. ](/help/sites-developing/naming-conventions.md) **제목** 필드에는 잘못된 문자가 포함될 수 있지만, 파생되는 이름에서는 잘못된 문자가 대체됩니다. 예:

| 제목 | 파생되는 이름 |
|---|---|
| Schön | schoen.html |
| SC%&amp;*ç+ | sc---c-.html |

#### 이름 {#name}

새 페이지를 만들 때 페이지 **이름**&#x200B;을 제공하면 AEM이 AEM 및 JCR에서 지정한 규칙에 따라 이름을 확인합니다. [](/help/sites-developing/naming-conventions.md) **이름** 필드에 잘못된 문자를 제출할 수 없습니다. AEM에서 유효하지 않은 문자를 발견하면 필드가 설명 메시지와 함께 강조 표시됩니다.

![caop-02](assets/caop-02.png)

>[!NOTE]
>
>언어 루트가 아닌 경우 ISO-639-1에 따라 페이지 이름으로 정의된 두 문자 코드를 사용할 수 없습니다.
>
>자세한 내용은 [컨텐츠 번역 준비](/help/sites-administering/tc-prep.md)를 참조하십시오.

### 템플릿 {#templates}

AEM에서 템플릿은 페이지의 전문 유형을 지정합니다. 템플릿은 만들어지는 새 페이지의 기초로 사용됩니다.

템플릿은 썸네일 이미지 및 기타 속성을 비롯한 페이지 구조를 정의합니다. 예를 들어 제품 페이지, 사이트 맵 및 연락처 정보에 서로 다른 템플릿을 사용할 수 있습니다. 템플릿은 여러 [구성 요소](#components)로 이루어집니다.

AEM에는 특별히 제공되는 몇 개의 템플릿이 있습니다. 사용 가능한 템플릿은 개별 웹 사이트에 따라 다릅니다. 주요 필드는 다음과 같습니다.

* **제목**
결과 웹 페이지에 표시되는 제목입니다.

* **이름**
페이지 이름을 지정할 때 사용됩니다.

* **템플릿**
새 페이지를 생성하는 데 사용할 수 있는 템플릿 목록입니다.

>[!NOTE]
>
>인스턴스에서 구성한 경우 [템플릿 작성자가 템플릿 편집기를 사용하여 템플릿을 만들 수 있습니다](/help/sites-authoring/templates.md).

### 구성 요소 {#components}

구성 요소는 특정 유형의 컨텐츠를 추가할 수 있도록 AEM에서 제공하는 요소입니다. AEM에는 다음과 같이 광범위한 기능을 제공하는 다양하고 [특별한 구성 요소](/help/sites-authoring/default-components-console.md)가 포함되어 있습니다.

* 텍스트
* 이미지
* Slideshow
* 비디오
* 기타

페이지를 생성하여 열면 [구성 요소 브라우저](/help/sites-authoring/editing-content.md#insertinganewparagraph)의 [구성 요소를 사용하여 컨텐츠를 추가](/help/sites-authoring/author-environment-tools.md#componentbrowser)할 수 있습니다.

>[!NOTE]
>
>[구성 요소 콘솔](/help/sites-authoring/default-components-console.md)은 인스턴스에 대한 구성 요소 개요를 제공합니다.

## 페이지 관리 {#managing-pages}

### 새 페이지 만들기 {#creating-a-new-page}

모든 페이지가 미리 만들어져 있지 않다면 컨텐츠를 만들기 전에 우선 페이지를 만들어야 합니다.

1. 사이트 콘솔을 엽니다(예: [https://localhost:4502/sites.html/content](https://localhost:4502/sites.html/content)).
1. 새 페이지를 만들 위치로 이동합니다.
1. 도구 모음에서 **만들기**&#x200B;를 사용하여 드롭다운 선택기를 연 다음, 목록에서 **페이지**&#x200B;를 선택합니다.

   ![caop-03](assets/caop-03.png)

1. 마법사의 첫 번째 단계에서 다음 중 하나를 수행할 수 있습니다.

   * 새 페이지를 만드는 데 사용할 템플릿을 선택한 후, **다음**&#x200B;을 클릭/탭하여 계속 진행합니다.

   * 프로세스를 중단하려면 **취소**&#x200B;를 클릭/탭합니다.

   ![caop-04](assets/caop-04.png)

1. 마법사의 마지막 단계에서 다음 중 하나를 수행할 수 있습니다.

   * 세 탭을 사용하여 새 페이지에 지정할 [페이지 속성](/help/sites-authoring/editing-page-properties.md)을 입력한 다음, 실제로 페이지를 만들려면 **만들기**&#x200B;를 클릭/탭합니다.

   * 선택한 템플릿으로 돌아가려면 **뒤로**&#x200B;를 사용하십시오.

   주요 필드는 다음과 같습니다.

   * **제목**:

      * 사용자에게 표시되며 필수입니다.
   * **이름**:

      * URI를 생성하는 데 사용됩니다. 지정하지 않을 경우 이름이 제목에서 파생됩니다.
      * 새 페이지를 만들 때 페이지 **이름**[을 제공하면 AEM이 AEM 및 JCR에서 지정한 규칙에 따라 이름을 확인합니다.](/help/sites-developing/naming-conventions.md)

      * **이름** 필드에 **잘못된 문자를 제출**&#x200B;할 수 없습니다. AEM에서 잘못된 문자를 감지하면 필드가 강조 표시되고 제거/교체가 필요한 문자를 나타내는 설명 메시지가 표시됩니다.
   >[!NOTE]
   >
   >[페이지 이름 지정 규칙](#page-naming-conventions)을 참조하십시오.

   새 페이지를 만드는 데 필요한 최소 정보는 **제목**&#x200B;입니다.

   ![caop-05](assets/caop-05.png)

1. **만들기**&#x200B;를 클릭하여 프로세스를 완료하고 새 페이지를 만듭니다. 확인 대화 상자에 페이지를 즉시 **열지** 또는 콘솔로 돌아갈지(**완료**) 여부를 묻는 메시지가 표시됩니다.

   ![chlimage_1-118](assets/chlimage_1-118.png)

   >[!NOTE]
   >
   >해당 위치에 이미 존재하는 이름을 사용하여 페이지를 만들 경우, 번호가 추가되어 변형된 이름이 자동으로 생성됩니다. 예를 들어 `winter`가 이미 존재하는 경우 새 페이지는 `winter0`이 됩니다.

1. 콘솔로 돌아오면 새 페이지가 보입니다.

   ![caop-06](assets/caop-06.png)

>[!CAUTION]
>
>페이지가 만들어지면 해당 템플릿을 변경할 수 없습니다. 대신 [새 템플릿으로 launch를 만들 수는 있지만 ](/help/sites-authoring/launches-creating.md#create-launch-with-new-template)그렇게 되면 이미 존재하는 컨텐츠는 모두 잃게 됩니다.

### 편집할 페이지 열기 {#opening-a-page-for-editing}

페이지를 만들거나 기존 페이지로 이동한 후(콘솔에서), 열어서 편집할 수 있습니다.

1. **사이트** 콘솔을 엽니다.
1. 편집할 페이지가 표시될 때까지 탐색합니다.
1. 다음 중 하나를 사용하여 페이지를 선택합니다.

   * [빠른 작업](/help/sites-authoring/basic-handling.md#quick-actions)
   * [선택 모드](/help/sites-authoring/basic-handling.md#navigatingandselectionmode) 및 도구 모음

   그런 다음 **편집** 아이콘을 선택하십시오.

   ![screen_shot_2018-03-22at105355](assets/screen_shot_2018-03-22at105355.png)

1. 페이지가 열리고, 원하는 대로 [페이지를 편집](/help/sites-authoring/editing-content.md#touchoptimizedui)할 수 있습니다.

>[!NOTE]
>
>링크가 편집 모드에서 활성 상태가 아니므로 페이지 편집기에서 다른 페이지로 이동하는 것은 미리 보기 모드에서만 가능합니다.

### 페이지 복사 및 붙여넣기 {#copying-and-pasting-a-page}

페이지 및 모든 하위 페이지를 새 위치에 복사할 수 있습니다.

1. **사이트** 콘솔에서 복사할 페이지가 표시될 때까지 탐색합니다.
1. 다음 중 하나를 사용하여 페이지를 선택합니다.

   * [빠른 작업](/help/sites-authoring/basic-handling.md#quick-actions)
   * [선택 모드](/help/sites-authoring/basic-handling.md#navigatingandselectionmode) 및 도구 모음

   그런 다음 페이지 **복사** 아이콘을 선택합니다.

   ![screen_shot_2018-03-22at105425](assets/screen_shot_2018-03-22at105425.png)

   >[!NOTE]
   >
   >선택 모드에 있을 경우, 페이지가 복사되자마자 이 모드가 종료됩니다.

1. 페이지의 새 복사본을 위한 위치로 이동합니다.
1. **붙여넣기** 아이콘은 오른쪽 드롭다운 화살표로 사용할 수 있습니다.

   ![붙여넣기](assets/paste-without-children.png)

   다음을 수행할 수 있습니다.
   * **붙여넣기** 아이콘 자체를 선택합니다. 원본 페이지와 모든 하위 페이지의 복사본이 이 위치에 만들어집니다.
   * 드롭다운 화살표를 선택하여 **하위 항목 없이 붙여넣기** 옵션을 표시합니다. 이 위치에 원본 페이지의 복사본이 만들어집니다. 하위 페이지는 복사되지 않습니다.

   >[!NOTE]
   >
   >페이지를 원본과 동일한 이름의 페이지가 이미 있는 위치에 복사하는 경우 숫자가 추가되어 변형된 이름이 자동으로 생성됩니다. 예를 들어 `winter`가 이미 존재하는 경우 `winter`는 `winter1`이 됩니다.

### 페이지 이동 또는 이름 바꾸기 {#moving-or-renaming-a-page}

>[!NOTE]
>
>페이지 이름 바꾸기는 새 페이지 이름을 지정할 때의 [페이지 이름 지정 규칙](#page-naming-conventions)을 따릅니다.

>[!NOTE]
>
>페이지는 페이지가 기반으로 하는 템플릿이 허용되는 위치로만 이동할 수 있습니다. 자세한 내용은 [템플릿 가용성](/help/sites-developing/templates.md#template-availability)을 참조하십시오.

페이지를 이동하는 절차와 페이지 이름을 변경하는 절차는 기본적으로 동일하며 같은 마법사로 처리됩니다. 이 마법사를 사용하여 다음을 수행할 수 있습니다.

* 페이지를 이동하지 않고 이름을 변경합니다.
* 이름을 변경하지 않고 페이지를 이동합니다.
* 동시에 이동하여 이름을 변경합니다.

AEM에서는 이름을 바꾸거나 이동하는 페이지를 참조하는 모든 내부 링크를 업데이트하는 기능을 제공합니다. 페이지별로 다른 기준을 적용할 수 있으므로 완벽한 유연성이 발휘됩니다.

1. 이동할 페이지가 표시될 때까지 탐색합니다.
1. 다음 중 하나를 사용하여 페이지를 선택합니다.

   * [빠른 작업](/help/sites-authoring/basic-handling.md#quick-actions)
   * [선택 모드](/help/sites-authoring/basic-handling.md#navigatingandselectionmode) 및 도구 모음

   그런 다음 페이지 **이동** 아이콘을 선택합니다.

   ![screen_shot_2018-03-22at105534](assets/screen_shot_2018-03-22at105534.png)

   이렇게 하면 페이지 이동 마법사가 열립니다.

1. 마법사의 **이름 변경** 단계에서 다음 중 하나를 수행할 수 있습니다.

   * 페이지가 이동되면 사용할 페이지의 이름을 지정한 후 **다음**&#x200B;을 클릭/탭하여 다음 단계로 진행합니다.

   * 프로세스를 중단하려면 **취소**&#x200B;를 클릭/탭합니다.

   ![caop-07](assets/caop-07.png)

   페이지를 이동하는 경우에만 페이지 이름이 동일하게 유지될 수 있습니다.

   >[!NOTE]
   >
   >페이지를 동일한 이름의 페이지가 이미 있는 위치로 이동하는 경우 숫자가 추가되어 변형된 이름이 자동으로 생성됩니다. 예를 들어 `winter`가 이미 존재하는 경우 `winter`는 `winter1`이 됩니다.

1. 마법사의 **대상 선택** 단계에서 다음 중 하나를 수행할 수 있습니다.

   * [열 보기](/help/sites-authoring/basic-handling.md#column-view)를 사용하여 페이지의 새 위치를 탐색할 수 있습니다.

      * 대상의 썸네일을 클릭하여 대상을 선택합니다.
      * 계속하려면 **다음**&#x200B;을 클릭하십시오.
   * **뒤로**&#x200B;를 사용하여 페이지 이름 지정으로 돌아갑니다.

   >[!NOTE]
   >
   >기본적으로 이동/이름을 바꾼 페이지의 상위 페이지는 대상으로 선택됩니다.

   ![caop-08](assets/caop-08.png)

   >[!NOTE]
   >
   >페이지를 동일한 이름의 페이지가 이미 있는 위치로 이동하는 경우 숫자가 추가되어 변형된 이름이 자동으로 생성됩니다. 예를 들어 `winter`가 이미 존재하는 경우 `winter`는 `winter1`이 됩니다.

1. 페이지가 연결되거나 참조된 경우 또는 게시된 경우 세부 사항이 **조정/다시 게시** 단계에서 나열됩니다.

   조정 및/또는 다시 게시해야 하는 사항을 적절히 표시할 수 있습니다.

   >[!NOTE]
   >
   >페이지가 연결 또는 참조되지 않은 경우 이 단계를 사용할 수 없습니다.

   ![caop-09](assets/caop-09.png)

1. **이동**&#x200B;을 선택하면 프로세스가 완료되고 페이지가 적절하게 이동되거나 페이지 이름이 변경됩니다.

>[!NOTE]
>
>페이지가 이미 게시된 경우 페이지를 이동하면 자동으로 게시 취소됩니다. 기본적으로 이동이 완료되면 다시 게시되지만 **조정/다시 게시** 창에서 페이지의 **다시 게시** 필드를 선택 취소하여 변경할 수 있습니다.

>[!NOTE]
>
>페이지가 어떤 식으로든 참조되지 않는 경우, **조정/다시 게시** 단계는 무시됩니다.

#### 비동기 작업 {#asynchronous-actions}

일반적으로 페이지 이동 또는 이름 변경 작업은 즉시 수행됩니다. 이 작업은 동기 처리로 간주되며 작업이 완료될 때까지 UI의 추가 작업이 차단됩니다.

그러나 영향을 받은 페이지 수가 정의된 제한을 초과하는 경우 작업은 비동기적으로 처리되므로 페이지 이동 또는 이름 변경 작업에 의해 방해받지 않고 사용자가 UI에서 계속 작성할 수 있습니다.

* 위의 마지막 단계에서 **이동**&#x200B;을 클릭하면 AEM이 구성된 제한을 확인합니다.
* 영향을 받는 페이지 수가 제한보다 적은 경우 동기 작업을 수행합니다.
* 영향을 받는 페이지 수가 제한보다 많은 경우 비동기 작업을 수행합니다.
   * 사용자는 비동기 작업을 수행할 시점을 정의해야 합니다
      * **이제** 비동기 작업의 실행을 즉시 시작합니다.
      * **나중에** 사용자는 비동기 작업이 시작될 시기를 정의할 수 있습니다.

         ![비동기 페이지 이동](assets/asynchronous-page-move.png)

비동기 작업의 상태는 **전역 탐색** -> **도구** -> **작업** -> **작업**&#x200B;의 [**비동기 작업 상태** 대시보드](/help/sites-administering/asynchronous-jobs.md#monitor-the-status-of-asynchronous-operations)에서 확인할 수 있습니다.

>[!NOTE]
>
>비동기 작업 처리와 페이지 이동/이름 바꾸기 작업에 대한 제한을 구성하는 방법에 대한 자세한 내용은 관리 사용자 안내서의 [비동기 작업](/help/sites-administering/asynchronous-jobs.md) 문서를 참조하십시오.

>[!NOTE]
>
>비동기 페이지 이동 처리를 위해서는 AEM 6.5.3.0 이상이 필요합니다.

### 페이지 삭제 {#deleting-a-page}

1. 삭제할 페이지가 표시될 때까지 탐색합니다.
1. [선택 모드](/help/sites-authoring/basic-handling.md#viewing-and-selecting-resources)를 사용하여 필요한 페이지를 선택한 다음, 도구 모음에서&#x200B;**삭제**&#x200B;를 사용합니다.

   ![screen_shot_2018-03-22at105622](assets/screen_shot_2018-03-22at105622.png)

   >[!NOTE]
   >
   >보안 규정에 따라, **삭제** 페이지 아이콘은 빠른 작업으로 사용할 수 없습니다.

1. 확인을 묻는 대화 상자가 나타나면:

   * **취소**&#x200B;를 사용하여 작업을 중단하거나,
   * **삭제**&#x200B;를 사용하여 작업을 확인합니다.

      * 페이지에 참조가 없으면, 페이지가 삭제됩니다.
      * 페이지에 참조가 있으면, 메시지 상자에 **하나 이상의 페이지가 참조되었다**&#x200B;고 표시됩니다. **강제 삭제**&#x200B;나 **취소**&#x200B;를 선택할 수 있습니다.

>[!NOTE]
>
>페이지가 이미 게시되어 있으면 삭제하기 전에 자동으로 게시 취소됩니다.

### 페이지 잠금 {#locking-a-page}

콘솔에서 또는 개별 페이지를 편집할 때 [페이지 잠금/잠금 해제](/help/sites-authoring/editing-content.md#locking-a-page)할 수 있습니다. 페이지가 잠겨 있는지 여부도 두 위치 모두에 표시됩니다.

![screen_shot_2018-03-22at105713](assets/screen_shot_2018-03-22at105713.png) ![screen_shot_2018-03-22at105720](assets/screen_shot_2018-03-22at105720.png)

### 새 폴더 만들기 {#creating-a-new-folder}

파일 및 페이지 구성에 도움이 되도록 폴더를 만들 수 있습니다.

>[!NOTE]
>
>폴더도 새 폴더 이름을 지정할 때 [페이지 이름 지정 규칙](#page-naming-conventions)을 따릅니다.

>[!CAUTION]
>
>* 폴더는 **사이트**&#x200B;나 다른 폴더 아래에서만 직접 만들 수 있습니다. 페이지 아래에서는 만들 수 없습니다.
>* 표준 작업인 이동, 복사, 붙여넣기, 삭제, 게시, 게시 취소 및 보기/편집 속성은 폴더에서 수행할 수 있습니다.
>* live copy 내에서는 폴더를 선택할 수 없습니다.

>



1. **사이트** 콘솔을 열고 필요한 위치로 이동합니다.
1. 옵션 목록을 열려면 도구 모음에서 **만들기**&#x200B;를 선택합니다.
1. 폴더 대화 상자를 열려면 **폴더**&#x200B;를 선택합니다. 여기에서 **이름** 및 **제목**&#x200B;을 입력할 수 있습니다.

   ![chlimage_1-119](assets/chlimage_1-119.png)

1. 폴더를 만들려면 **만들기**&#x200B;를 선택합니다.
