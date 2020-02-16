---
title: Adobe Campaign 구성 요소
seo-title: Adobe Campaign 구성 요소
description: Adobe Campaign과 통합하면 뉴스레터와 양식을 사용하여 작업할 때 사용할 수 있는 구성 요소가 있습니다.
seo-description: Adobe Campaign과 통합하면 뉴스레터와 양식을 사용하여 작업할 때 사용할 수 있는 구성 요소가 있습니다.
uuid: cc9417c9-4cc1-4554-858e-2ecd682dc92f
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: 5afe864d-5794-4ffa-99e7-a3233f982aff
docset: aem65
translation-type: tm+mt
source-git-commit: 016c705230dffec052c200b058a36cdbe0520fc4

---


# Adobe Campaign 구성 요소{#adobe-campaign-components}

Adobe Campaign과 통합하면 뉴스레터와 양식을 사용하여 작업할 때 사용할 수 있는 구성 요소가 있습니다. 모두 이 문서에 설명되어 있습니다.

>[!CAUTION]
>
>AEM 이메일 구성 요소는 더 이상 사용되지 않습니다. 콘텐츠와 스타일을 결합하는 이메일의 특성으로 인해 AEM에서 제공하는 이메일 구성 요소는 프로젝트에 필요한 구성 요소에 사용자 정의 스타일을 구현해야 하기 때문에 고객에게 제한된 재사용이 되었습니다.
>
>이메일 구성 요소는 프로젝트 수준에서 구현될 수 있으며, 더 이상 사용되지 않는 AEM 이메일 구성 요소는 이러한 기능을 구현하는 방법을 설명합니다. 그러나 이러한 사용되지 않는 구성 요소는 프로젝트에서 사용할 수 없습니다.

## Adobe Campaign 뉴스레터 구성 요소 {#adobe-campaign-newsletter-components}

모든 Campaign 구성 요소는 [이메일 템플릿 우수 사례](/help/sites-administering/best-practices-for-email-templates.md)에 요약된 우수 사례를 따르며, Adobe 마크업 언어 [HTL](https://helpx.adobe.com/experience-manager/htl/using/overview.html)을 기반으로 합니다.

Adobe Campaign과 통합하도록 구성된 뉴스레터/이메일을 열면 **Adobe Campaign 뉴스레터** 섹션에 다음 구성 요소가 표시됩니다.

* 제목(캠페인)
* 이미지(캠페인)
* 링크(캠페인)
* Scene7 이미지 템플릿(캠페인)
* 타깃팅된 참조(캠페인)
* 텍스트 및 이미지(캠페인)
* 텍스트 및 개인화(캠페인)

이 구성 요소들에 대한 설명은 다음 섹션에 있습니다.

![chlimage_1-81](assets/chlimage_1-81.png)

### 제목(캠페인) {#heading-campaign}

제목 구성 요소의 기능은 다음과 같습니다.

* **제목** 필드를 비워 현재 페이지의 이름을 표시합니다.
* **제목** 필드에서 지정하는 텍스트를 표시합니다.

**제목(캠페인)** 구성 요소를 직접 편집합니다. 페이지 제목을 사용하려면 비워 둡니다.

![chlimage_1-82](assets/chlimage_1-82.png)

다음 내용을 구성할 수 있습니다.

* **제목**
페이지 제목 이외의 이름을 사용하려면 여기에 입력합니다.

* **제목 수준(1, 2, 3, 4)** HTML 제목 크기 1-4를 기반으로 하는 제목 수준입니다.

다음 예는 제목(캠페인) 구성 요소가 표시되는 것을 보여줍니다.

![chlimage_1-83](assets/chlimage_1-83.png)

### 이미지(캠페인) {#image-campaign}

이미지(캠페인) 구성 요소는 지정된 매개 변수에 따라 이미지와 추가 텍스트를 표시합니다.

이미지를 업로드한 다음 편집하고 조작(예: 자르기, 회전, 링크/제목/텍스트 추가)할 수 있습니다.

이미지를 업로드한 다음 편집하고 조작(예: 자르기, 회전, 링크/제목/텍스트 추가)할 수 있습니다. [컨텐츠 파인더](/help/sites-authoring/author-environment-tools.md#thecontentfinderclassicui)의 이미지를 구성 요소나 그 편집 대화 상자에 바로 끌어다 놓을 수 있습니다. 편집 대화 상자의 가운데 영역을 두 번 클릭하여 로컬 파일 시스템을 탐색하고 이미지를 업로드할 수도 있습니다. 편집 대화 상자의 두 탭은 이미지의 모든 정의 및 조작도 제어합니다.

![chlimage_1-84](assets/chlimage_1-84.png)

이미지가 로드되면 다음 항목을 구성할 수 있습니다.

* **맵**
이미지를 매핑하려면 맵을 선택합니다. 이미지 맵을 만들 방법(사각형, 다각형 등)과 영역이 가리킬 대상 위치를 지정할 수 있습니다.

* **자르기**
자르기를 선택하여 이미지를 자릅니다. 마우스를 사용하여 이미지를 자를 수 있습니다.

* **회전**
이미지를 회전하려면 [회전]을 선택합니다. 이미지가 원하는 방향으로 회전할 때까지 반복적으로 사용합니다.

* **지우기**
현재 이미지를 제거합니다.

* 확대/축소 막대(클래식만 해당)
이미지를 확대/축소하려면 이미지 아래에서 [확인] 및 [취소] 단추 위에 있는 슬라이드 막대를 사용합니다.
* **제목**
이미지의 제목입니다.

* **대체 텍스트**
액세스 가능한 컨텐츠를 만들 때 사용할 대체 텍스트입니다.

* **다음으로 링크**
웹 사이트 내의 자산 또는 다른 페이지로 이동하는 링크를 만듭니다.

* **설명**
이미지의 설명입니다.

* **크기**
이미지의 높이와 너비를 설정합니다.

>[!NOTE]
>
>**고급** 탭에서 **대체 텍스트** 필드에 정보를 입력해야 합니다. 그렇지 않으면, 이미지를 저장할 수 없으며 다음 오류 메시지가 표시됩니다.
>
>`Validation failed. Verify the values of the marked fields.`


다음 예는 이미지(캠페인) 구성 요소가 표시되는 것을 보여줍니다.

![chlimage_1-85](assets/chlimage_1-85.png)

### 링크(캠페인) {#link-campaign}

링크(캠페인) 구성 요소를 사용하면 뉴스레터에 링크를 추가할 수 있습니다. 이 구성 요소는 터치에 적합한 사용자 인터페이스에서 하나를 추가하고 호환성 모드에서 열 수도 있지만 클래식 사용자 인터페이스에서만 사용할 수 있습니다.

![chlimage_1-86](assets/chlimage_1-86.png)

**디스플레이**, **URL 정보** 또는 **고급** 탭에서 다음 내용을 구성할 수 있습니다.

* **링크 캡션** 링크용 캡션으로서, 사용자에게 표시되는 텍스트입니다.

* **링크 도구 설명** 링크 사용 방법에 대한 추가 정보를 추가합니다.

* **링크 유형** 드롭다운 목록에서 **사용자 지정 URL**&#x200B;과 **응용 문서** 중에 선택하십시오. 이 필드는 반드시 입력해야 합니다. [사용자 지정 URL]을 선택하는 경우 링크 URL을 제공할 수 있습니다. [응용 문서]를 선택하는 경우 문서 경로를 제공할 수 있습니다.

* **추가 URL 매개 변수** 추가적인 URL 매개 변수를 추가합니다. 여러 항목을 추가하려면 [항목 추가]를 클릭하십시오.

>[!NOTE]
>
>You must enter information in the **Link Type** field in the **URL Info** tab, or the component cannot save and you see the following error message:
>
>`Validation failed. Verify the values of the marked fields.`


다음 예는 링크(캠페인) 구성 요소가 표시되는 것을 보여줍니다.

![chlimage_1-87](assets/chlimage_1-87.png)

### 타깃팅된 참조(캠페인) {#targeted-reference-campaign}

타깃팅된 참조(캠페인) 구성 요소를 사용하면 타깃팅된 단락에 대한 참조를 만들 수 있습니다.

이 구성 요소에서 타깃팅된 단락으로 이동하여 선택합니다.

드롭다운 메뉴를 클릭하여 참조할 단락으로 이동합니다. 완료되면 **확인**&#x200B;을 클릭하십시오.

### 텍스트 및 이미지(캠페인) {#text-image-campaign}

텍스트 및 이미지(캠페인) 구성 요소는 텍스트 블록과 이미지를 추가합니다.

![chlimage_1-88](assets/chlimage_1-88.png)

텍스트 및 개인화(캠페인)와 이미지(캠페인) 구성 요소와 함께 다음 내용을 구성할 수 있습니다.

* **텍스트**
텍스트를 입력합니다. 도구 모음을 사용하여 서식을 수정하고, 목록을 만들고, 링크를 추가합니다.

* **이미지**
Content Finder에서 이미지를 드래그하거나 클릭하여 이미지를 찾습니다. 필요에 따라 자르거나 회전합니다.

* **이미지 속성**(**고급 이미지 속성**)
다음을 지정할 수 있습니다.

   * **제목**
블록의 제목으로서 마우스로 가리킬 때 표시됩니다.

   * **대체 텍스트**
이미지를 표시할 수 없을 때 표시할 대체 텍스트입니다.

   * **링크 대상** 웹 사이트 내의 자산 또는 다른 페이지로 이동하는 링크를 만듭니다.

   * **설명**
이미지의 설명입니다.

   * **크기**
이미지의 높이와 너비를 설정합니다.

>[!NOTE]
>
>**고급** 탭의 **대체 텍스트** 필드는 반드시 입력해야 합니다. 그렇지 않으면, 구성 요소를 저장할 수 없으며 다음 오류 메시지가 표시됩니다.
>
>`Validation failed. Verify the values of the marked fields.`


다음 예는 텍스트 및 이미지(캠페인) 구성 요소가 표시되는 것을 보여줍니다.

![chlimage_1-89](assets/chlimage_1-89.png)

### 텍스트 및 개인화(캠페인) {#text-personalization-campaign}

The Text &amp; Personalization (Campaign) component lets you enter a text block using a WYSIWYG editor, with functionality provided by the [Rich Text editor](/help/sites-authoring/rich-text-editor.md). 또한 이 구성 요소를 사용하면 Adobe Campaign에서 사용할 수 있는 컨텍스트 필드와 개인화 블록을 사용할 수 있습니다. [개인화 삽입](/help/sites-classic-ui-authoring/classic-personalization-ac-campaign.md#inserting-personalization)을 참조하십시오.

여러 가지 아이콘을 사용하여 글꼴 특성, 정렬, 링크, 목록 및 들여쓰기 등의 텍스트 서식을 지정할 수 있습니다.

일반적으로 리치 텍스트 편집기에서 하듯이 텍스트를 추가하십시오. Adobe Campaign 드롭다운을 선택하고 필드를 적절하게 선택하여 개인화를 추가합니다.

![chlimage_1-90](assets/chlimage_1-90.png)

컨텐츠를 작성하려면 텍스트 및 컨텍스트 필드 또는 개인화 블록을 추가합니다. 다음으로, Client Context를 선택하여 모습 프로필에서 데이터를 테스트하십시오. 모습을 선택하면 개인화 필드는 선택된 프로필의 데이터로 자동 교체됩니다.

>[!NOTE]
>
>**nms:seedMember** 스키마나 그 확장 중 하나에서 정의된 필드만 고려됩니다. `nms:seedMember`에 연결된 표의 특성은 사용할 수 없습니다.

## Adobe Campaign 양식 구성 요소 {#adobe-campaign-form-components}

Adobe Campaign 구성 요소를 사용하여 뉴스레터에 가입하거나, 뉴스레터 가입을 해지하거나, 사용자 프로필을 업데이트하기 위해 사용자가 채우는 양식을 만들 수 있습니다. 자세한 내용은 [Adobe Campaign 양식 만들기](/help/sites-classic-ui-authoring/classic-personalization-ac-forms.md)를 참조하십시오.

각 구성 요소 필드는 Adobe Campaign 데이터베이스 필드에 연결할 수 있습니다. 사용 가능한 필드는 [구성 요소 및 데이터 유형](#components-and-data-type) 섹션에 설명된 대로 필드가 포함하는 데이터의 유형에 따라 달라집니다. Adobe Campaign에서 수신자 스키마를 확장하는 경우에는, 데이터 유형이 일치하는 구성 요소에서 새 필드를 사용할 수 있습니다.

When you open a form that is configured to integrate with Adobe Campaign, you see the following components in the **Adobe Campaign** section:

* 확인란(캠페인)
* 날짜 필드(캠페인)와 날짜 필드/HTML5(캠페인)
* 암호화된 기본 키(캠페인)
* 표시 오류(캠페인)
* 숨겨진 조정 키(캠페인)
* 숫자 필드(캠페인)
* 옵션 필드(캠페인)
* 가입 확인 목록(캠페인)
* 텍스트 필드(캠페인)

이 섹션에서는 각 구성 요소에 대해 자세히 설명합니다.

### 구성 요소 및 데이터 유형 {#components-and-data-type}

다음 표에서는 Adobe Campaign 프로필 데이터를 표시하고 수정하는 데 사용할 수 있는 구성 요소에 대해 설명합니다. 각 구성 요소는 필드 값을 표시하고 양식이 제출되면 필드를 업데이트하도록 Adobe Campaign 프로필 필드에 매핑할 수 있습니다. 다른 구성 요소는 적절한 데이터 유형의 필드에만 대응시킬 수 있습니다.

<table>
 <tbody>
  <tr>
   <td><p><strong>구성 요소</strong></p> </td>
   <td><p><strong>Adobe Campaign 필드의 데이터 유형</strong></p> </td>
   <td><p><strong>예제 필드</strong></p> </td>
  </tr>
  <tr>
   <td><p>확인란(캠페인)</p> </td>
   <td><p>부울</p> </td>
   <td><p>더 이상 연락하지 않음(모든 채널에서)</p> </td>
  </tr>
  <tr>
   <td><p>날짜 필드(캠페인)</p> <p>날짜 필드/HTML 5(캠페인)</p> </td>
   <td><p>날짜</p> </td>
   <td><p>생년월일</p> </td>
  </tr>
  <tr>
   <td><p>숫자 필드(캠페인)</p> </td>
   <td><p>숫자(바이트, short, long, double)</p> </td>
   <td><p>연령</p> </td>
  </tr>
  <tr>
   <td><p>옵션 필드(캠페인)</p> </td>
   <td><p>연결된 값이 있는 바이트</p> </td>
   <td><p>성별</p> </td>
  </tr>
  <tr>
   <td><p>텍스트 필드(캠페인)</p> </td>
   <td><p>문자열</p> </td>
   <td><p>이메일</p> </td>
  </tr>
 </tbody>
</table>

### 대부분의 구성 요소에 공통인 설정 {#settings-common-to-most-components}

Adobe Campaign 구성 요소에는 모든 구성 요소(암호화된 기본 키와 숨겨진 조정 키 구성 요소 제외)에서 공통인 설정이 있습니다.

대부분의 구성 요소에서 다음 내용을 구성할 수 있습니다.

#### 제목 및 텍스트 {#title-and-text}

* **제목** 요소 이름 이외의 이름을 사용하려면 여기에 입력하십시오.

* **제목 숨기기** 제목을 표시하지 않으려면 이 확인란을 선택하십시오.

* **설명** 설명을 필드에 추가하여 사용자에 대한 자세한 정보를 제공하십시오.

* **값만 표시** 값이 있을 경우 값만 보여줍니다.

#### Adobe Campaign {#adobe-campaign}

다음 내용을 구성할 수 있습니다.

* **매핑** 적절한 경우 Adobe Campaign 개인화 필드를 선택하십시오.

* **조정 키** 이 필드가 조정 키의 일부인 경우 이 확인란을 선택하십시오.

#### 제한 {#constraints}

* **필수** - 이 구성 요소를 필수 구성 요소로 만들려면 이 확인란을 선택합니다.즉, 사용자가 값을 입력해야 합니다.
* **필수 메시지** - 필드를 필수 항목이라는 메시지를 추가합니다(선택 사항).

#### 스타일링 {#styling}

* **CSS** 이 구성 요소에 사용할 CSS 클래스를 입력하십시오.

### 확인란(캠페인) {#checkbox-campaign}

확인란(캠페인) 구성 요소를 사용하면 사용자가 부울 데이터 유형의 Adobe Campaign 프로필 필드를 수정할 수 있습니다. 예를 들어, 수신자가 채널을 통해 연락을 받지 않도록 지정할 수 있게 해주는 확인란(캠페인) 구성 요소가 있을 수 있습니다.

확인란(캠페인) 구성 요소에서 [대부분의 Adobe Campaign 구성 요소에 공통인 설정을 구성](#settings-common-to-most-components)할 수 있습니다.

다음 예는 확인란(캠페인) 구성 요소가 표시되는 것을 보여줍니다.

![chlimage_1-91](assets/chlimage_1-91.png)

### 날짜 필드(캠페인)와 날짜 필드/HTML 5(캠페인) {#date-field-campaign-and-date-field-html-campaign}

수신자가 날짜를 지정할 수 있도록 하려면 날짜 필드를 사용하십시오. 예를 들어, 수신자가 생년월일을 지정하도록 할 수 있습니다. 날짜 형식은 Adobe Campaign 인스턴스에 사용된 형식과 일치합니다.

[대부분의 Adobe Campaign 구성 요소에 공통인 설정](#settings-common-to-most-components) 외에 다음 내용을 구성할 수 있습니다.

* **제한 - 제한** - 없음 **또는 날짜를** 선택하여 **날짜 제한을 추가하거나 제한을 추가하지 않을 수 있습니다** . 날짜를 선택하는 경우, 사용자가 필드에 입력하는 응답의 형식은 날짜 형식이어야 합니다.

* **제한 메시지** - 또한 사용자가 응답의 형식을 제대로 지정하는 방법을 알 수 있도록 제한 메시지를 추가할 수 있습니다.
* **스타일 - 너비** - **+** 및 **아이콘을 클릭하거나 탭하거나 숫자를 입력하여 필드의 너비를 조정합니다** .

다음 예는 날짜 필드(캠페인) 구성 요소가 조정된 너비로 표시되는 것을 보여줍니다.

![chlimage_1-92](assets/chlimage_1-92.png)

### 암호화된 기본 키(캠페인) {#encrypted-primary-key-campaign}

이 구성 요소는 Adobe Campaign 프로필의 ID를 포함할 URL 매개 변수의 이름을 정의합니다(각각 Adobe Campaign Standard와 6.1의 **기본 리소스 ID** 또는 **암호화된 기본 키**).

Adobe Campaign 프로필 데이터를 표시 및 수정하는 각 양식은 암호화된 기본 키 구성 요소를 포함&#x200B;**해야** 합니다.

암호화된 기본 키(캠페인) 구성 요소에서는 다음 내용을 구성할 수 있습니다.

* **제목 및 텍스트 - 요소 이름** - 기본값은 encryptedPK입니다. 양식에서 다른 요소의 이름과 충돌할 때에만 요소 이름을 변경해야 합니다. 두 양식 필드에는 동일한 요소 이름이 있을 수 없습니다.
* **Adobe Campaign - URL 매개 변수** - EPK에 대한 URL 매개 변수를 추가합니다. 예를 들어 값 **epk**&#x200B;를 사용할 수 있습니다.

다음 예는 암호화된 기본 키(캠페인) 구성 요소가 표시되는 것을 보여줍니다.

![chlimage_1-93](assets/chlimage_1-93.png)

### 표시 오류(캠페인) {#error-display-campaign}

이 구성 요소를 사용하면 백엔드 오류를 표시할 수 있습니다. 구성 요소가 제대로 작동하도록 하려면 양식의 오류 처리를 [앞으로]로 설정해야 합니다.

다음 예는 오류 표시(캠페인) 구성 요소가 표시되는 것을 보여줍니다.

![chlimage_1-94](assets/chlimage_1-94.png)

### 숨겨진 조정 키(캠페인) {#hidden-reconciliation-key-campaign}

숨겨진 조정 키(캠페인) 구성 요소를 사용하면 숨겨진 필드를 조정 키의 일부로 양식에 추가할 수 있습니다.

숨겨진 조정 키(캠페인) 구성 요소에서는 다음 내용을 구성할 수 있습니다.

* **제목 및 텍스트 - 요소 이름** - 기본값은 reconcilKey입니다. 양식에서 다른 요소의 이름과 충돌할 때에만 요소 이름을 변경해야 합니다. 두 양식 필드에는 동일한 요소 이름이 있을 수 없습니다.
* **Adobe Campaign - 매핑** - Adobe Campaign 개인화 필드에 매핑합니다.

다음 예는 숨겨진 조정 키(캠페인) 구성 요소가 표시되는 것을 보여줍니다.

![chlimage_1-95](assets/chlimage_1-95.png)

### 숫자 필드(캠페인) {#numeric-field-campaign}

수신자가 나이와 같은 숫자를 입력할 수 있도록 하려면 숫자 필드를 사용하십시오.

[대부분의 Adobe Campaign 구성 요소에 공통인 설정](#settings-common-to-most-components) 외에 다음 내용을 구성할 수 있습니다.

* **제한 - 제한** 드롭다운없음 **또는 숫자** 중 하나를 선택하여 숫자 또는 **제한을** 추가할 수 있습니다. 숫자를 선택하는 경우, 사용자가 필드에 입력하는 응답의 형식은 숫자여야 합니다.

* **제한 메시지** - 또한 사용자가 응답의 형식을 제대로 지정하는 방법을 알 수 있도록 제한 메시지를 추가할 수 있습니다.
* **스타일 - 너비** - **+** 및 **아이콘을 클릭하거나 탭하거나 숫자를 입력하여 필드의 너비를 조정합니다** .

다음 예는 숫자 필드(캠페인) 구성 요소가 구성된 너비로 표시되는 것을 보여줍니다.

![chlimage_1-96](assets/chlimage_1-96.png)

### 옵션 필드(캠페인) {#option-field-campaign}

이 드롭다운 목록에서는 수신자의 성별이나 상태와 같은 선택 사항을 선택할 수 있습니다.

옵션 필드(캠페인) 구성 요소에서 [대부분의 Adobe Campaign 구성 요소에 공통인 설정을 구성](#settings-common-to-most-components)할 수 있습니다. 드롭다운 목록을 채우려면 Adobe Campaign 기호를 클릭하거나 탭하고 적절한 필드로 이동하여 Adobe Campaign 개인화 필드에서 해당 필드를 선택하십시오.

다음 예는 옵션 필드(캠페인) 구성 요소가 표시되는 것을 보여줍니다.

![chlimage_1-97](assets/chlimage_1-97.png)

### 가입 확인 목록(캠페인) {#subscriptions-checklist-campaign}

Adobe Campaign 프로필과 연결된 가입을 수정하려면 **가입 확인 목록(캠페인)** 구성 요소를 사용하십시오.

이 구성 요소를 양식에 추가하면 모든 사용 가능한 가입이 확인란으로 표시되고 사용자가 원하는 가입을 선택할 수 있습니다. When users submit the form, this component subscribes the user to or unsubscribes the user from the selected services depending on the form action type (**Adobe Campaign: Subscribe to Services** or **Adobe Campaign: Unsubscribe from Services**).

>[!NOTE]
>
>이 구성 요소는 사용자가 이미 가입했거나 가입을 해지한 서비스를 확인하지는 않습니다.

가입 확인 목록(캠페인) 구성 요소에서 [대부분의 Adobe Campaign 구성 요소에 공통인 설정을 구성](#settings-common-to-most-components)할 수 있습니다. (이 구성 요소에 사용할 수 있는 Adobe Campaign 구성이 없습니다.)

다음 예는 가입 확인 목록(캠페인) 구성 요소가 표시되는 것을 보여줍니다.

![chlimage_1-98](assets/chlimage_1-98.png)

### 텍스트 필드(캠페인) {#text-field-campaign}

텍스트 필드(캠페인) 구성 요소에서는 문자열 유형 데이터(예: 이름, 성, 주소, 이메일 주소 등)를 입력할 수 있습니다.

[대부분의 Adobe Campaign 구성 요소에 공통인 설정](#settings-common-to-most-components) 외에 다음 내용을 구성할 수 있습니다.

* **제한 - 제한** - 드롭다운 - 없음, **이메일**, 이름 **(모음**&#x200B;없음)을 선택하여 이메일 주소, 이름 또는 제한 조건 없음을 **** 추가할 수 있습니다. 이메일을 선택하는 경우, 사용자가 필드에 입력하는 응답의 형식은 이메일 주소여야 합니다. 이름을 선택하는 경우 이름이어야 합니다(모음 기호는 허용되지 않음).

* **제한 메시지** - 또한 사용자가 응답의 형식을 제대로 지정하는 방법을 알 수 있도록 제한 메시지를 추가할 수 있습니다.
* **스타일 - 너비** - **+** 및 **아이콘을 클릭하거나 탭하거나 숫자를 입력하여 필드의 너비를 조정합니다** .

다음 예는 텍스트 필드(캠페인) 구성 요소가 표시되는 것을 보여줍니다.

![chlimage_1-99](assets/chlimage_1-99.png)
