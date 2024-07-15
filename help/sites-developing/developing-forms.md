---
title: Forms 개발(클래식 UI)
description: Adobe Experience Manager의 클래식 UI에 대한 양식을 개발하는 방법 알아보기
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: components
content-type: reference
docset: aem65
exl-id: f43e9491-aa8f-40af-9800-123695142559
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '1930'
ht-degree: 1%

---

# Forms 개발(클래식 UI){#developing-forms-classic-ui}

양식의 기본 구조는 다음과 같습니다.

* 양식 시작
* 양식 요소
* 양식 끝

표준 AEM 설치에서 사용할 수 있는 일련의 기본 [양식 구성 요소](/help/sites-authoring/default-components.md#form)를 통해 이러한 모든 기능을 사용할 수 있습니다.

[새 구성 요소를 개발](/help/sites-developing/developing-components-samples.md)하여 양식에서 사용할 수 있습니다. 또한 다음을 수행할 수 있습니다.

* [값을 사용하여 양식 미리 로드](#preloading-form-values)
* [여러 값이 있는 (특정) 필드 미리 로드](#preloading-form-fields-with-multiple-values)
* [새로운 액션 개발](#developing-your-own-form-actions)
* [새로운 제한 사항 개발](#developing-your-own-form-constraints)
* [특정 양식 필드 표시 또는 숨기기](#showing-and-hiding-form-components)

필요한 경우 [스크립트를 사용하여](#developing-scripts-for-use-with-forms) 기능을 확장합니다.

>[!NOTE]
>
>이 문서는 클래식 UI에서 [기초 구성 요소](/help/sites-authoring/default-components-foundation.md)를 사용한 양식 개발에 중점을 둡니다. Adobe 터치 사용 UI에서 양식 개발을 위해 새 [핵심 구성 요소](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=ko-KR) 및 [조건 숨기기](/help/sites-developing/hide-conditions.md)를 사용하는 것이 좋습니다.

## 양식 값 미리 로드 {#preloading-form-values}

양식 시작 구성 요소는 저장소의 노드를 가리키는 선택적 경로인 **로드 경로**&#x200B;에 대한 필드를 제공합니다.

로드 경로는 미리 정의된 값을 양식의 여러 필드에 로드하는 데 사용되는 노드 속성에 대한 경로입니다.

저장소의 노드에 대한 경로를 지정하는 선택적 필드입니다. 이 노드에 필드 이름과 일치하는 속성이 있으면 양식의 해당 필드에 해당 속성 값이 미리 로드됩니다. 일치하는 항목이 없으면 필드에 기본값이 포함됩니다.

>[!NOTE]
>
>[양식 작업](#developing-your-own-form-actions)에서도 초기 값을 로드할 리소스를 설정할 수 있습니다. 이 작업은 `init.jsp` 내의 `FormsHelper#setFormLoadResource`을(를) 사용하여 수행됩니다.
>
>설정되지 않은 경우에만 작성자가 양식 시작 구성 요소에 설정한 경로에서 양식이 채워집니다.

### 여러 값이 있는 양식 필드 미리 로드 {#preloading-form-fields-with-multiple-values}

또한 다양한 양식 필드에 저장소의 노드를 가리키는 선택적 경로인 **항목 로드 경로**&#x200B;가 있습니다.

**항목 로드 경로**&#x200B;은(는) 양식의 특정 필드에 미리 정의된 값을 로드하는 데 사용되는 노드 속성의 경로입니다(예: [드롭다운 목록](/help/sites-authoring/default-components-foundation.md#dropdown-list), [확인란 그룹](/help/sites-authoring/default-components-foundation.md#checkbox-group) 또는 [라디오 그룹](/help/sites-authoring/default-components-foundation.md#radio-group)).

#### 예 - 여러 값이 있는 드롭다운 목록 미리 로드 {#example-preloading-a-dropdown-list-with-multiple-values}

선택할 값 범위로 드롭다운 목록을 구성할 수 있습니다.

**항목 로드 경로**&#x200B;을(를) 사용하여 저장소의 폴더에서 목록에 액세스하고 이러한 항목을 필드에 미리 로드할 수 있습니다.

1. 슬링 폴더(`sling:Folder`) 만들기
예: `/etc/designs/<myDesign>/formlistvalues`

1. 다중 값 문자열(`String[]`) 유형의 새 속성(예: `myList`)을 추가하여 드롭다운 항목 목록을 포함합니다. JSP 스크립트나 셸 스크립트의 cURL과 같이 스크립트를 사용하여 컨텐츠를 가져올 수도 있습니다.

1. **항목 로드 경로** 필드의 전체 경로 사용:
예: `/etc/designs/geometrixx/formlistvalues/myList`

`String[]`의 값이 다음과 같은 형식의 경우:

* `AL=Alabama`
* `AK=Alaska`

이렇게 하면 AEM이 다음과 같이 목록을 생성합니다.

* `<option value="AL">Alabama</option>`
* `<option value="AK">Alaska</option>`

예를 들어 이 기능은 다국어 설정에서 유용하게 사용할 수 있습니다.

### 고유한 양식 작업 개발 {#developing-your-own-form-actions}

양식에는 작업이 필요합니다. 작업은 사용자 데이터로 양식을 제출할 때 실행되는 작업을 정의합니다.

표준 AEM 설치에서는 다양한 작업이 제공되며, 이러한 작업은 다음에서 볼 수 있습니다.

`/libs/foundation/components/form/actions`

**Form** 구성 요소의 **Action Type** 목록:

![chlimage_1-8](assets/chlimage_1-8.png)

이 섹션에서는 이 목록에 포함할 고유한 양식 작업을 개발하는 방법을 다룹니다.

다음과 같이 `/apps`에서 자신의 작업을 추가할 수 있습니다.

1. `sling:Folder` 유형의 노드를 만듭니다. 구현할 작업을 반영하는 이름을 지정합니다.

   예:

   `/apps/myProject/components/customFormAction`

1. 이 노드에서 다음 속성을 정의한 다음 **모두 저장**&#x200B;을 클릭하여 변경 내용을 유지합니다.

   * `sling:resourceType` - `foundation/components/form/action`(으)로 설정

   * `componentGroup` - `.hidden`(으)로 정의

   * 선택적으로:

      * `jcr:title` - 선택한 제목을 지정합니다. 드롭다운 선택 목록에 표시됩니다. 설정하지 않으면 노드 이름이 표시됩니다

      * `jcr:description` - 선택한 설명을 입력하십시오.

1. 폴더에서 대화 상자 노드를 만듭니다.

   1. 작업을 선택한 후 작성자가 양식 대화 상자를 편집할 수 있도록 필드를 추가합니다.

1. 폴더에서 다음 중 하나를 만듭니다.

   1. 게시물 스크립트.
스크립트 이름은 `post.POST.<extension>`입니다. 예: `post.POST.jsp`
양식을 처리하기 위해 양식을 제출할 때 `POST` 양식에서 도착하는 데이터를 처리하는 코드가 포함되어 있는 POST 스크립트가 호출됩니다.

   1. 양식 제출 시 호출되는 전달 스크립트를 추가합니다.
스크립트 이름은 `forward.<extension`>입니다(예: `forward.jsp`).
이 스크립트는 경로를 정의할 수 있습니다. 그런 다음 현재 요청이 지정된 경로로 전달됩니다.

   필요한 호출은 `FormsHelper#setForwardPath`(variant 2개)입니다. 일반적인 사례는 유효성 검사 또는 논리를 수행하여 대상 경로를 찾은 다음 해당 경로로 전달하여 기본 Sling POST 서블릿이 JCR에서 실제 저장소를 수행하도록 하는 것입니다.

   폼 작업과 `forward.jsp`이(가) &quot;접착제&quot; 코드로만 작동하는 경우 실제 처리를 수행하는 다른 서블릿도 있을 수 있습니다. 예를 들어 `/libs/foundation/components/form/actions/mail`의 메일 작업이 있습니다. 메일 서블릿이 있는 `<currentpath>.mail.html`에 세부 정보를 전달합니다.

   그래서:

   * `post.POST.jsp`은(는) 작업 자체로 완전히 수행되는 작은 작업에 유용합니다.
   * `forward.jsp`은(는) 위임만 필요한 경우에 유용합니다.

   스크립트 실행 순서는 다음과 같습니다.

   * 양식을 렌더링할 때(`GET`):

      1. `init.jsp`
      1. 모든 필드의 제약 조건: `clientvalidation.jsp`
      1. 양식의 validationRT: `clientvalidation.jsp`
      1. 설정된 경우 로드 리소스를 통해 양식이 로드됨
      1. `<form></form>` 렌더링 내에서 `addfields.jsp`

   * `POST` 양식을 처리할 때:

      1. `init.jsp`
      1. 모든 필드의 제약 조건: `servervalidation.jsp`
      1. 양식의 validationRT: `servervalidation.jsp`
      1. `forward.jsp`
      1. 전달 경로가 설정된 경우(`FormsHelper.setForwardPath`) 요청을 전달한 다음 `cleanup.jsp`을(를) 호출합니다.

      1. 정방향 경로가 설정되지 않은 경우 `post.POST.jsp`을(를) 호출합니다(여기서 종료되고 `cleanup.jsp`이(가) 호출되지 않음).

1. 폴더에서 다시 다음을 선택적으로 추가합니다.

   1. 필드를 추가하기 위한 스크립트.
스크립트 이름은 `addfields.<extension>`입니다. 예: `addfields.jsp`
양식 시작에 대한 HTML이 작성된 직후에 `addfields` 스크립트가 호출됩니다. 이렇게 하면 작업에서 사용자 지정 입력 필드 또는 양식 내에 다른 HTML을 추가할 수 있습니다.

   1. 초기화 스크립트.
스크립트 이름은 `init.<extension>`입니다. 예: `init.jsp`
이 스크립트는 양식이 렌더링될 때 호출됩니다. 작업 세부 사항을 초기화하는 데 사용할 수 있습니다.

   1. 정리 스크립트.
스크립트 이름은 `cleanup.<extension>`입니다. 예: `cleanup.jsp`
이 스크립트를 사용하여 정리를 수행할 수 있습니다.

1. parsys에서 **Forms** 구성 요소를 사용하십시오. 이제 **작업 유형** 드롭다운에 새 작업이 포함됩니다.

   >[!NOTE]
   >
   >제품에 포함된 기본 작업을 보려면 다음과 같이 하십시오.
   >
   >
   >`/libs/foundation/components/form/actions`

### 고유한 양식 제한 개발 {#developing-your-own-form-constraints}

다음 두 가지 수준에서 제한을 적용할 수 있습니다.

* [개별 필드(다음 절차 참조)의 경우](#constraints-for-individual-fields)
* [폼-전역 유효성 검사](#form-global-constraints)(으)로

#### 개별 필드에 대한 제한 {#constraints-for-individual-fields}

개별 필드(`/apps` 아래)에 대한 자체 제약 조건을 다음과 같이 추가할 수 있습니다.

1. `sling:Folder` 유형의 노드를 만듭니다. 구현할 제약 조건을 반영하는 이름을 지정합니다.

   예:

   `/apps/myProject/components/customFormConstraint`

1. 이 노드에서 다음 속성을 정의한 다음 **모두 저장**&#x200B;을 클릭하여 변경 내용을 유지합니다.

   * `sling:resourceType` - `foundation/components/form/constraint`(으)로 설정

   * `constraintMessage` - 양식을 제출할 때 제한 사항에 따라 필드가 유효하지 않은 경우 표시되는 사용자 지정된 메시지

   * 선택적으로:

      * `jcr:title` - 선택한 제목을 지정합니다. 선택 목록에 표시됩니다. 설정하지 않으면 노드 이름이 표시됩니다
      * `hint` - 필드 사용 방법에 대한 사용자의 추가 정보

1. 이 폴더 내에서는 다음 스크립트가 필요할 수 있습니다.

   * 클라이언트 유효성 검사 스크립트:
스크립트 이름은 `clientvalidation.<extension>`입니다. 예: `clientvalidation.jsp`
양식 필드가 렌더링될 때 호출됩니다. 클라이언트의 필드를 확인하기 위해 클라이언트 Javascript를 만드는 데 사용할 수 있습니다.

   * 서버 유효성 검사 스크립트:
스크립트 이름은 `servervalidation.<extension>`입니다. 예: `servervalidation.jsp`
양식 제출 시 호출됩니다. 제출 후 서버에서 필드를 검증하는 데 사용할 수 있습니다.

>[!NOTE]
>
>샘플 제약조건은 다음에서 볼 수 있습니다.
>
>`/libs/foundation/components/form/constraints`

#### 양식-전역 제한 {#form-global-constraints}

양식 시작 구성 요소(`validationRT`)에서 리소스 유형을 구성하여 양식 전역 유효성 검사를 지정합니다. 예:

`apps/myProject/components/form/validation`

그런 다음 다음을 정의할 수 있습니다.

* 필드의 클라이언트 유효성 검사 스크립트 뒤에 삽입된 `clientvalidation.jsp`
* 및 `servervalidation.jsp` - `POST`에서 개별 필드 서버 유효성 검사 후에 호출됩니다.

### 양식 구성 요소 표시 및 숨기기 {#showing-and-hiding-form-components}

양식의 다른 필드 값에 따라 양식 구성 요소를 표시하거나 숨기도록 양식을 구성할 수 있습니다.

양식 필드의 가시성을 변경하는 것은 특정 조건에서만 필드가 필요한 경우에 유용합니다. 예를 들어 피드백 양식에서 고객에게 이메일로 제품 정보를 보낼 것인지 묻는 질문을 합니다. 예를 선택하면 고객이 이메일 주소를 입력할 수 있는 텍스트 필드가 나타납니다.

**규칙 표시/숨기기 편집** 대화 상자를 사용하여 양식 구성 요소를 표시하거나 숨기는 조건을 지정합니다.

![showhideeditor](assets/showhideeditor.png)

대화 상자 맨 위에 있는 필드를 사용하여 다음 정보를 지정합니다.

* 구성 요소를 숨기거나 표시하기 위한 조건을 지정하는지 여부.
* 구성 요소를 표시하거나 숨기기 위해 조건이 true여야 하는지 여부.

하나 이상의 조건이 이 필드 아래에 나타납니다. 조건은 (동일한 양식의) 다른 양식 구성 요소의 값을 값과 비교합니다. 필드의 실제 값이 조건을 충족하면 조건이 true로 평가됩니다. 조건에는 다음 정보가 포함됩니다.

* 테스트되는 양식 필드의 제목
* 연산자.
* 필드 값에 대한 값이 비교됩니다.

예를 들어 제목이 `Receive email notifications?`**인 라디오 그룹 구성 요소에는 `Yes` 및 `No` 라디오 단추가 있습니다. 제목이 `Email Address`인 텍스트 필드 구성 요소는 `Yes`을(를) 선택하면 표시되도록 다음 조건을 사용합니다.

![showhitedecondition](assets/showhidecondition.png)

JavaScript에서 조건은 필드를 참조하기 위해 요소 이름 속성의 값을 사용합니다. 앞의 예제에서 라디오 그룹 구성 요소의 Element Name 속성은 `contact`입니다. 다음 코드는 이 예제에 대한 동등한 JavaScript 코드입니다.

`((contact == "Yes"))`

**양식 구성 요소를 표시하거나 숨기려면:**

1. 특정 양식 구성 요소를 편집합니다.

1. **표시/숨기기**&#x200B;를 선택하여 **표시/숨기기 규칙 편집** 대화 상자를 엽니다.

   * 첫 번째 드롭다운 목록에서 **표시** 또는 **숨기기**&#x200B;를 선택하여 조건에 따라 구성 요소를 표시할지 또는 숨길지 여부를 지정합니다.

   * 맨 위 줄의 끝에 있는 드롭다운 목록에서 다음을 선택합니다.

      * **모두** - 구성 요소를 표시하거나 숨기려면 모든 조건이 true여야 하는 경우
      * **모두** - 구성 요소를 표시하거나 숨기려면 하나 이상의 조건만 true여야 하는 경우

   * 조건 줄(하나가 기본값으로 표시됨)에서 구성 요소, 연산자를 선택한 다음 값을 지정합니다.
   * 필요한 경우 **조건 추가**&#x200B;를 클릭하여 조건을 더 추가합니다.

   예:

   ![chlimage_1-9](assets/chlimage_1-9.png)

1. **확인**&#x200B;을 클릭하여 정의를 저장합니다.

1. 정의를 저장한 후 양식 구성 요소 속성에서 **표시/숨기기** 옵션 옆에 **규칙 편집** 링크가 나타납니다. 변경하려면 이 링크를 클릭하여 **규칙 표시/숨기기 편집** 대화 상자를 엽니다.

   모든 변경 내용을 저장하려면 **확인**&#x200B;을 클릭하세요.

   ![chlimage_1-10](assets/chlimage_1-10.png)

   >[!CAUTION]
   >
   >[표시/숨기기] 정의의 효과를 보고 테스트할 수 있습니다.
   >
   >* 작성자 환경의 **미리 보기** 모드에서(처음 미리 보기로 전환할 때 페이지를 다시 로드해야 함)
   >
   >* 게시 환경에서

#### 끊어진 컴포넌트 참조 처리 {#handling-broken-component-references}

조건 표시/숨기기에서는 Element Name 속성의 값을 사용하여 폼의 다른 구성 요소를 참조합니다. 조건이 삭제되거나 요소 이름 속성이 변경된 구성 요소를 참조하는 경우 표시/숨기기 구성이 잘못되었습니다. 이러한 상황이 발생하면 조건을 수동으로 업데이트해야 하거나 양식이 로드될 때 오류가 발생합니다.

표시/숨기기 구성이 잘못된 경우 구성은 JavaScript 코드로만 제공됩니다. 문제를 해결하려면 코드를 편집합니다.코드는 구성 요소를 참조하는 데 원래 사용한 요소 이름 속성을 사용합니다.

### Forms에 사용할 스크립트 개발 {#developing-scripts-for-use-with-forms}

스크립트를 작성할 때 사용할 수 있는 API 요소에 대한 자세한 내용은 [양식 관련 javadocs](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/foundation/forms/package-summary.html)을 참조하십시오.

양식을 제출하기 전에 서비스를 호출하고 실패한 경우 서비스를 취소하는 등의 작업에 이 옵션을 사용할 수 있습니다.

* 유효성 검사 리소스 유형 정의
* 유효성 검사를 위한 스크립트 포함:

   * JSP에서 웹 서비스를 호출하고 오류 메시지가 포함된 `com.day.cq.wcm.foundation.forms.ValidationInfo` 개체를 만듭니다. 오류가 있으면 양식 데이터가 게시되지 않습니다.
