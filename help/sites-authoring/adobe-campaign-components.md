---
title: Adobe Campaign 구성 요소와 통합
description: Adobe Campaign과 통합하면 뉴스레터 및 양식으로 작업할 때 사용할 수 있는 구성 요소가 있습니다.
uuid: a858d5ca-aa6e-4bde-92db-a6dcd8b48ae6
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: personalization
discoiquuid: 9da34dab-7e89-4127-ab26-532687746b2a
docset: aem65
exl-id: d1132fcd-e6a0-44a2-8753-d250f68fbd78
source-git-commit: 50d29c967a675db92e077916fb4adef6d2d98a1a
workflow-type: tm+mt
source-wordcount: '2836'
ht-degree: 11%

---

# Adobe Campaign 구성 요소{#adobe-campaign-components}

Adobe Campaign과 통합하면 뉴스레터 및 양식으로 작업할 때 사용할 수 있는 구성 요소가 있습니다. 두 가지 모두 이 문서에 설명되어 있습니다.

>[!CAUTION]
>
>AEM 이메일 구성 요소는 더 이상 사용되지 않습니다. 콘텐츠와 스타일을 병합하는 이메일의 특성상 AEM에서 즉시 제공하는 이메일 구성 요소는 프로젝트에 필요한 모든 구성 요소로 사용자 정의 스타일을 구현해야 하므로 고객이 제한적으로 재사용할 수 있습니다.
>
>이메일 구성 요소는 프로젝트 수준에서 구현할 수 있으며, 더 이상 사용되지 않는 AEM 이메일 구성 요소는 이를 구현하는 방법을 보여 줍니다. 단, 이렇게 사용되지 않는 구성 요소는 프로젝트에서 사용할 수 없습니다.

## Adobe Campaign 뉴스레터 구성 요소 {#adobe-campaign-newsletter-components}

모든 캠페인 구성 요소는 다음에 요약된 모범 사례를 따릅니다. [이메일 템플릿에 대한 우수 사례](/help/sites-administering/best-practices-for-email-templates.md) 및 는 Adobe 마크업 언어를 기반으로 합니다 [HTL](https://helpx.adobe.com/kr/experience-manager/htl/using/overview.html).

Adobe Campaign과 통합하도록 구성된 뉴스레터/이메일을 열면 **Adobe Campaign 뉴스레터** 섹션:

* 제목(캠페인)
* 이미지(캠페인)
* 링크(캠페인)
* Scene7 이미지 템플릿(캠페인)
* 타깃팅된 참조(캠페인)
* 텍스트 및 이미지(캠페인)
* 텍스트 및 개인화(캠페인)

이러한 구성 요소에 대한 설명은 다음 섹션에 있습니다.

구성 요소는 다음과 같이 표시됩니다.

![chlimage_1-43](assets/chlimage_1-43.png)

### 제목(캠페인) {#heading-campaign}

제목 구성 요소는 다음 중 하나를 수행할 수 있습니다.

* 에서 나가면 현재 페이지의 이름을 표시합니다. **제목** 필드가 비어 있습니다.
* 에 지정하는 텍스트 표시 **제목** 필드.

다음을 편집했습니다. **제목(캠페인)** 구성 요소를 바로 사용할 수 있습니다. 페이지 제목을 사용하려면 비워 둡니다.

![chlimage_1-44](assets/chlimage_1-44.png)

다음을 구성할 수 있습니다.

* **제목**
페이지 제목 이외의 이름을 사용하려면 여기에 입력합니다.

* **제목 수준(1, 2, 3, 4)**
HTML 제목 크기 1-4를 기반으로 하는 제목 수준입니다.

다음 예는 표시 중인 제목 (캠페인) 구성 요소를 보여 줍니다.

![chlimage_1-45](assets/chlimage_1-45.png)

### 이미지(캠페인) {#image-campaign}

이미지(캠페인) 구성 요소는 지정된 매개 변수에 따라 이미지와 추가 텍스트를 표시합니다.

이미지를 업로드한 다음 편집하고 조작할 수 있습니다(예: 자르기, 회전, 링크/제목/텍스트 추가).

에서 이미지를 드래그하여 놓을 수 있습니다. [자산 브라우저](/help/sites-authoring/author-environment-tools.md#assetsbrowsertouchoptimizedui) 구성 요소 또는 구성 요소에 직접 연결 [구성 대화 상자](/help/sites-authoring/editing-content.md#editconfigurecopycutdeletepastetouchoptimizedui). 구성 대화 상자에서 이미지를 업로드할 수도 있습니다. 이 대화 상자는 이미지의 모든 정의와 조작을 제어합니다.

![chlimage_1-46](assets/chlimage_1-46.png)

>[!NOTE]
>
>다음에 정보를 입력해야 합니다. **대체 텍스트** 필드 또는 이미지를 저장할 수 없습니다.

이미지가 업로드된 후(그 전은 아님) 다음을 사용할 수 있습니다. [즉석 편집](/help/sites-authoring/editing-content.md#editcontenttouchoptimizedui) 필요에 따라 이미지를 자르기/회전하려면 다음을 수행하십시오.

![즉석 편집 도구 모음](do-not-localize/chlimage_1-10.png)

>[!NOTE]
>
>즉석 편집기에서는 편집할 때 이미지의 원래 크기와 종횡비를 사용합니다. 높이 및 너비 속성을 지정할 수도 있습니다. 속성에 정의된 모든 크기와 종횡비는 편집 변경 사항을 저장할 때 적용됩니다.
>
>사용자 인스턴스에 따라 최소 및 최대 제한 사항은 [페이지의 디자인](/help/sites-developing/designer.md)에 의해 적용될 수도 있습니다. 이러한 제한 사항은 프로젝트 구현 중 개발됩니다.

맵 및 확대/축소와 같은 몇 가지 추가 옵션은 전체 화면 편집 모드에서 사용할 수 있습니다.

![전체 화면 편집 모드](do-not-localize/chlimage_1-11.png)

이미지가 로드되면 다음 항목을 구성할 수 있습니다.

* **맵**
이미지를 매핑하려면 맵을 선택합니다. 이미지 맵을 만들 방법(사각형, 다각형 등)과 영역이 가리킬 대상 위치를 지정할 수 있습니다.

* **자르기**
자르기를 선택하여 이미지를 자릅니다. 마우스를 사용하여 이미지를 자를 수 있습니다.

* **회전**
이미지를 회전하려면 회전을 선택합니다. 이미지가 원하는 방향으로 회전할 때까지 반복적으로 사용합니다.

* **지우기**
현재 이미지를 제거합니다.

* 확대/축소 막대(기본만 해당) 이미지를 확대/축소하려면 이미지 아래에서 확인 및 취소 단추 위에 있는 슬라이드 막대를 사용합니다.
* **제목**
이미지의 제목입니다.

* **대체 텍스트**
액세스 가능한 컨텐츠를 만들 때 사용할 대체 텍스트입니다.

* **링크 대상**
웹 사이트 내의 자산 또는 기타 페이지에 대한 링크를 만듭니다.

* **설명**
이미지에 대한 설명.

* **크기**
이미지의 높이와 너비를 설정합니다.

>[!NOTE]
>
>다음에 정보를 입력해야 합니다. **대체 텍스트** 의 필드 **고급** 탭하거나 이미지를 저장할 수 없고 다음과 같은 오류 메시지가 표시됩니다.
>
>`Validation failed. Verify the values of the marked fields.`
>

다음 예는 표시되는 이미지(캠페인) 구성 요소를 보여 줍니다.

![chlimage_1-47](assets/chlimage_1-47.png)

### 링크(캠페인) {#link-campaign}

링크 (캠페인) 구성 요소를 사용하여 뉴스레터에 링크를 추가할 수 있습니다.

다음에서 다음을 구성할 수 있습니다. **표시**, **URL 정보**, 또는 **고급** 탭:

* **링크 캡션**
링크의 캡션입니다. 사용자가 볼 수 있는 텍스트입니다.

* **링크 툴팁**
링크 사용 방법에 대한 추가 정보를 추가합니다.

* **링크 유형**
드롭다운 목록에서 다음 중 하나를 선택합니다 **사용자 정의 URL** 및 **적응형 문서**. 이 필드는 필수입니다. 사용자 지정 URL을 선택하는 경우 링크 URL을 제공할 수 있습니다. 적응형 문서를 선택하면 문서 경로를 제공할 수 있습니다.

* **추가 URL 매개 변수**
추가 URL 매개 변수를 추가합니다. 항목 추가 를 클릭하여 여러 항목을 추가합니다.

>[!NOTE]
>
>다음에 정보를 입력해야 합니다. **링크 유형** 의 필드 **URL 정보** 탭하거나, 구성 요소를 저장할 수 없고 다음과 같은 오류 메시지가 표시됩니다.
>
>`Validation failed. Verify the values of the marked fields.`
>

다음 예는 표시되는 링크 (캠페인) 구성 요소를 보여 줍니다.

![chlimage_1-48](assets/chlimage_1-48.png)

### Dynamic Media Classic(Scene7) 이미지 템플릿(캠페인) {#scene-image-template-campaign}

Dynamic Media Classic(Scene7) 이미지 템플릿은 계층화된 이미지 파일로, 여기서 가변성을 위해 콘텐츠와 속성을 매개 변수화할 수 있습니다. 다음 **[!UICONTROL 이미지 템플릿]** 구성 요소를 사용하여 뉴스레터 내에서 Scene7 템플릿을 사용하고 템플릿 매개 변수의 값을 변경할 수 있습니다. 또한 매개 변수 내에서 Adobe Campaign 메타데이터 변수를 사용할 수 있으므로 각 사용자는 개인화된 방식으로 이미지를 경험하게 됩니다.

![chlimage_1-49](assets/chlimage_1-49.png)

**편집**&#x200B;을 클릭하여 구성 요소를 구성합니다. 이 섹션에서 설명하는 설정을 구성할 수 있습니다. 이 Scene7 이미지 템플릿은에 자세히 설명되어 있습니다. [Scene7 이미지 템플릿 구성 요소](/help/assets/scene7.md#image-template).

또한 Scene7의 템플릿에 대해 정의된 모든 템플릿 매개 변수가 매개 변수 패널에 나열됩니다. 이러한 각 매개 변수에 대해 값을 조정하거나, 변수를 삽입하거나, 기본값으로 재설정할 수 있습니다.

![chlimage_1-50](assets/chlimage_1-50.png)

### 타깃팅된 참조(캠페인) {#targeted-reference-campaign}

타겟팅된 참조(캠페인) 구성 요소를 사용하면 타겟팅된 단락에 대한 참조를 생성할 수 있습니다.

이 구성 요소에서는 타겟팅된 단락으로 이동하여 선택합니다.

폴더 아이콘을 클릭하여 참조할 단락으로 이동합니다. 완료되면 확인 표시를 클릭합니다.

### 텍스트 및 이미지(캠페인) {#text-image-campaign}

텍스트 및 이미지(캠페인) 구성 요소는 텍스트 블록과 이미지를 추가합니다.

을 클릭하여 구성 요소를 구성할 때 텍스트 또는 이미지 를 선택합니다.

![chlimage_1-51](assets/chlimage_1-51.png)

선택 **텍스트** 인라인 편집기를 표시합니다.

![텍스트 도구 모음](do-not-localize/chlimage_1-12.png)

선택 **이미지** 이미지의 즉석 편집기를 표시합니다.

![이미지 도구 모음](do-not-localize/chlimage_1-13.png)

다음을 참조하십시오 [이미지(캠페인) 구성 요소](#image-campaign) 이미지 작업에 대한 자세한 정보입니다. 다음을 참조하십시오 [텍스트 및 개인화(캠페인) 구성 요소](#text-personalization-campaign) 를 참조하십시오.

텍스트 및 개인화(캠페인) 및 이미지(캠페인) 구성 요소와 마찬가지로 다음을 구성할 수 있습니다.

* **텍스트**
텍스트를 입력합니다. 도구 모음을 사용하여 서식을 수정하고, 목록을 만들고, 링크를 추가합니다.

* **이미지**
컨텐츠 파인더에서 이미지를 끌어 놓거나 클릭하여 이미지를 찾습니다. 필요에 따라 자르거나 회전합니다.

* **이미지 속성** (**고급 이미지 속성**) 다음을 지정할 수 있습니다.

   * **제목**
블록의 제목입니다. 마우스를 올려 놓으면 표시됩니다.

   * **대체 텍스트**
이미지를 표시할 수 없는 경우 표시할 대체 텍스트입니다.

   * **링크 대상**
웹 사이트 내의 자산 또는 기타 페이지에 대한 링크를 만듭니다.

   * **설명**
이미지에 대한 설명.

   * **크기**
이미지의 높이와 너비를 설정합니다.

>[!NOTE]
>
>다음 **대체 텍스트** 의 필드 **고급** 탭이 필요하거나 구성 요소를 저장할 수 없으며 다음 오류 메시지가 표시됩니다.
>
>`Validation failed. Verify the values of the marked fields.`
>

다음 예는 표시되는 텍스트 및 이미지(캠페인) 구성 요소를 보여 줍니다.

![chlimage_1-52](assets/chlimage_1-52.png)

### 텍스트 및 개인화(캠페인) {#text-personalization-campaign}

텍스트 및 개인화(캠페인) 구성 요소를 사용하면 WYSIWYG 편집기를 사용하여 텍스트 블록을 입력할 수 있습니다. [리치 텍스트 편집기](/help/sites-authoring/rich-text-editor.md). 또한 이 구성 요소를 사용하여 Adobe Campaign에서 사용할 수 있는 컨텍스트 필드 및 개인화 블록을 사용할 수 있습니다. 다음을 참조하십시오. [개인화 삽입](/help/sites-authoring/campaign.md#inserting-personalization).

아이콘을 선택하면 글꼴 특성, 정렬, 링크, 목록, 들여쓰기 등 텍스트 서식을 지정할 수 있습니다. 기능은에서 기본적으로 동일합니다 [두 UI](/help/sites-authoring/editing-content.md)와 같은 다양한 모양과 느낌은 서로 다릅니다.

![chlimage_1-53](assets/chlimage_1-53.png)

즉석 편집기에서 텍스트를 추가하고, 양쪽 맞춤을 변경하고, 링크를 추가 및 제거하고, 컨텍스트 필드 또는 개인화 블록을 추가하고, 전체 화면 모드로 전환할 수 있습니다. 텍스트/개인화 추가가 완료되면 확인 표시를 선택하여 변경 사항을 저장합니다(또는 x를 선택하여 취소). 다음을 참조하십시오 [즉석 편집](/help/sites-authoring/editing-content.md#editcontenttouchoptimizedui) 추가 정보.

>[!NOTE]
>
>* 사용 가능한 개인화 필드는 뉴스레터가 연결되는 Adobe Campaign 템플릿에 따라 다릅니다.
>* ContextHub에서 담당자를 선택하면 개인화 필드가 선택한 프로필의 데이터로 자동으로 대체됩니다.
>
>다음을 참조하십시오 [개인화 삽입](/help/sites-authoring/campaign.md#inserting-personalization).

![chlimage_1-54](assets/chlimage_1-54.png)

>[!NOTE]
>
>에 정의된 필드만 **nms:seedMember** 스키마 또는 해당 확장 중 하나가 고려됩니다. 연결된 테이블의 속성 **nms:seedMember** 을(를) 사용할 수 없습니다.

## Adobe Campaign 양식 구성 요소 {#adobe-campaign-form-components}

Adobe Campaign 구성 요소를 사용하여 사용자가 뉴스레터를 구독하거나 뉴스레터 구독을 취소하거나 사용자 프로필을 업데이트하는 양식을 만듭니다. 다음을 참조하십시오 [Adobe Campaign Forms 만들기](/help/sites-authoring/adobe-campaign-forms.md) 추가 정보.

각 구성 요소 필드는 Adobe Campaign 데이터베이스 필드에 연결할 수 있습니다. 사용 가능한 필드는 섹션에 설명된 대로 포함된 데이터 유형에 따라 다릅니다 [구성 요소 및 데이터 유형](#components-and-data-type). Adobe Campaign에서 수신자 스키마를 확장하는 경우 데이터 유형이 일치하는 구성 요소에서 새 필드를 사용할 수 있습니다.

Adobe Campaign과 통합되도록 구성된 양식을 열면 **Adobe Campaign** 섹션:

* 확인란(캠페인)
* 날짜 필드(캠페인) 및 날짜 필드/HTML5(캠페인)
* 암호화된 기본 키(캠페인)
* 표시 오류(캠페인)
* 숨겨진 조정 키(캠페인)
* 숫자 필드(캠페인)
* 옵션 필드(캠페인)
* 가입 확인 목록(캠페인)
* 텍스트 필드(캠페인)

구성 요소는 다음과 같이 표시됩니다.

![chlimage_1-55](assets/chlimage_1-55.png)

이 섹션에서는 각 구성 요소에 대해 자세히 설명합니다.

### 구성 요소 및 데이터 유형 {#components-and-data-type}

다음 표에서는 Adobe Campaign 프로필 데이터를 표시하고 수정하는 데 사용할 수 있는 구성 요소에 대해 설명합니다. 각 구성 요소를 Adobe Campaign 프로필 필드에 매핑하여 해당 값을 표시하고 양식 제출 시 필드를 업데이트할 수 있습니다. 다른 구성 요소는 적절한 데이터 유형의 필드에만 일치시킬 수 있습니다.

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
   <td><p>아니요 긴 연락처(모든 채널에서)</p> </td>
  </tr>
  <tr>
   <td><p>날짜 필드(캠페인)</p> <p>날짜 필드/HTML 5(캠페인)</p> </td>
   <td><p>날짜</p> </td>
   <td><p>생일</p> </td>
  </tr>
  <tr>
   <td><p>숫자 필드(캠페인)</p> </td>
   <td><p>숫자(바이트, 짧음, 긴, 더블)</p> </td>
   <td><p>나이</p> </td>
  </tr>
  <tr>
   <td><p>옵션 필드(캠페인)</p> </td>
   <td><p>바이트(관련 값 포함)</p> </td>
   <td><p>성별</p> </td>
  </tr>
  <tr>
   <td><p>텍스트 필드(캠페인)</p> </td>
   <td><p>문자열</p> </td>
   <td><p>이메일</p> </td>
  </tr>
 </tbody>
</table>

### 대부분의 구성 요소에 공통되는 설정 {#settings-common-to-most-components}

Adobe Campaign 구성 요소에는 모든 구성 요소에서 공통되는 설정이 있습니다(암호화된 기본 키 및 숨겨진 조정 키 구성 요소 제외).

대부분의 구성 요소에서 다음을 구성할 수 있습니다.

#### 제목 및 텍스트 {#title-and-text}

![chlimage_1-56](assets/chlimage_1-56.png)

* **제목**
요소 이름 이외의 이름을 사용하려면 여기에 입력합니다.

* **제목 숨기기**
제목을 표시하지 않으려면 이 확인란을 선택합니다.

* **설명**
필드에 설명을 추가하여 사용자에게 자세한 정보를 제공합니다.

* **값만 표시**
값이 있는 경우에만 표시합니다.

#### Adobe Campaign {#adobe-campaign}

다음을 구성할 수 있습니다.

* **매핑**
해당되는 경우 Adobe Campaign 개인화 필드를 선택합니다.

* **조정 키**
이 필드가 조정 키의 일부인 경우 이 확인란을 선택합니다.

![chlimage_1-57](assets/chlimage_1-57.png)

#### 제한 {#constraints}

* **필수** 이 구성 요소를 필수로 만들려면(즉, 사용자가 값을 입력해야 함) 이 확인란을 선택합니다.
* **필수 메시지** 선택적으로 필드가 필수임을 나타내는 메시지를 추가합니다.

![chlimage_1-58](assets/chlimage_1-58.png)

#### 스타일링 {#styling}

* **CSS**
이 구성 요소에 사용할 CSS 클래스를 입력합니다.

![chlimage_1-59](assets/chlimage_1-59.png)

### 확인란(캠페인) {#checkbox-campaign}

확인란(캠페인) 구성 요소를 사용하면 부울 데이터 유형의 Adobe Campaign 프로필 필드를 수정할 수 있습니다. 예를 들어 수신자가 어떤 채널을 통해서도 연락을 받지 않도록 지정할 수 있는 확인란(캠페인) 구성 요소가 있을 수 있습니다.

다음을 수행할 수 있습니다. [대부분의 Adobe Campaign 구성 요소에 공통되는 설정 구성](#settings-common-to-most-components) 확인란(캠페인) 구성 요소

다음 예는 표시되는 확인란(캠페인) 구성 요소를 보여 줍니다.

![chlimage_1-60](assets/chlimage_1-60.png)

### 날짜 필드(캠페인) 및 날짜 필드/HTML 5(캠페인) {#date-field-campaign-and-date-field-html-campaign}

날짜 필드를 사용하여 수신자의 날짜를 허용할 수 있습니다. 예를 들어 수신자가 생년월일을 지정하도록 할 수 있습니다. 날짜 형식은 Adobe Campaign 인스턴스에 사용된 형식과 일치합니다.

에 더하여 [대부분의 Adobe Campaign 구성 요소에 공통되는 설정](#settings-common-to-most-components), 다음을 구성할 수 있습니다.

* **제한 - 제한** 드롭다운 다음을 선택할 수 있습니다. **없음** 또는 **날짜 -** 날짜 제한을 추가하거나 제한을 해제하십시오. 날짜를 선택하는 경우 필드에 입력하는 응답 사용자는 날짜 형식이어야 합니다.

* **제한 메시지** 또한 제한 메시지를 추가하여 사용자가 답변의 서식을 올바르게 지정하는 방법을 알 수 있습니다.
* **스타일링 - 폭** 필드를 클릭하거나 탭하여 너비를 조정합니다. **+** 및 **-** 아이콘 또는 숫자 입력.

다음 예는 너비가 조정된 날짜 필드(캠페인) 구성 요소가 표시되는 것을 보여 줍니다.

![chlimage_1-61](assets/chlimage_1-61.png)

### 암호화된 기본 키(캠페인) {#encrypted-primary-key-campaign}

이 구성 요소는 Adobe Campaign 프로필의 식별자를 포함할 URL 매개 변수의 이름(**기본 리소스 식별자** 또는 **암호화된 기본 키** Adobe Campaign Standard 및 6.1에서 각각).

Adobe Campaign 프로필 데이터를 표시하고 수정하는 각 양식 **필수** 암호화된 기본 키 구성 요소를 포함합니다.

암호화된 기본 키(캠페인) 구성 요소에서 다음을 구성할 수 있습니다.

* **제목 및 텍스트 - 요소 이름** 기본값은 encryptedPK입니다. 양식에 있는 다른 요소의 이름과 충돌하는 경우에만 요소 이름을 변경하면 됩니다. 두 개의 양식 필드에 동일한 요소 이름을 사용할 수 없습니다.
* **Adobe Campaign - URL 매개 변수** EPK에 대한 URL 매개 변수를 추가합니다. 예를 들어 값을 사용할 수 있습니다 **epk**.

다음 예제에서는 암호화된 기본 키(캠페인) 구성 요소가 표시되는 것을 보여 줍니다.

![chlimage_1-62](assets/chlimage_1-62.png)

### 표시 오류(캠페인) {#error-display-campaign}

이 구성 요소를 사용하여 백엔드 오류를 표시할 수 있습니다. 구성 요소가 제대로 작동하려면 양식의 오류 처리를 앞으로 로 설정해야 합니다.

다음 예에서는 표시되는 오류 표시(캠페인) 구성 요소를 보여 줍니다.

![chlimage_1-63](assets/chlimage_1-63.png)

### 숨겨진 조정 키(캠페인) {#hidden-reconciliation-key-campaign}

숨겨진 조정 키(캠페인) 구성 요소를 사용하여 숨겨진 필드를 양식에 조정 키의 일부로 추가할 수 있습니다.

숨겨진 조정 키(캠페인) 구성 요소에서 다음을 구성할 수 있습니다.

* **제목 및 텍스트 - 요소 이름** 기본값은 reconcilKey입니다. 양식에 있는 다른 요소의 이름과 충돌하는 경우에만 요소 이름을 변경하면 됩니다. 두 개의 양식 필드에 동일한 요소 이름을 사용할 수 없습니다.
* **Adobe Campaign - 매핑** Adobe Campaign 개인화 필드에 매핑합니다.

다음 예제에서는 숨겨진 조정 키(캠페인) 구성 요소가 표시되는 것을 보여 줍니다.

![chlimage_1-64](assets/chlimage_1-64.png)

### 숫자 필드(캠페인) {#numeric-field-campaign}

수신자가 나이 등의 숫자를 입력할 수 있도록 하려면 숫자 필드를 사용하십시오.

에 더하여 [대부분의 Adobe Campaign 구성 요소에 공통되는 설정](#settings-common-to-most-components), 다음을 구성할 수 있습니다.

* **제한 - 제한** 드롭다운 다음을 선택할 수 있습니다. **없음** 또는 **숫자 -** 숫자 또는 제한 없음의 제한을 추가합니다. 숫자를 선택하는 경우 필드에 입력하는 응답 사용자는 숫자여야 합니다.

* **제한 메시지** 또한 제한 메시지를 추가하여 사용자가 답변의 서식을 올바르게 지정하는 방법을 알 수 있습니다.
* **스타일링 - 폭** 필드를 클릭하거나 탭하여 너비를 조정합니다. **+** 및 **-** 아이콘 또는 숫자 입력.

다음 예는 구성된 너비의 숫자 필드(캠페인) 구성 요소가 표시되는 것을 보여 줍니다.

![chlimage_1-65](assets/chlimage_1-65.png)

### 옵션 필드(캠페인) {#option-field-campaign}

이 드롭다운 목록에서 옵션을 선택할 수 있습니다(예: 수신자의 성별 또는 상태).

다음을 수행할 수 있습니다. [대부분의 Adobe Campaign 구성 요소에 공통되는 설정 구성](#settings-common-to-most-components) 옵션 필드(캠페인) 구성 요소 드롭다운 목록을 채우려면 Adobe Campaign 기호를 클릭하거나 탭하고 필드로 이동하여 Adobe Campaign 개인화 필드의 해당 필드를 선택합니다.

![chlimage_1-66](assets/chlimage_1-66.png)

다음 예는 표시되는 옵션 필드(캠페인) 구성 요소를 보여 줍니다.

![chlimage_1-67](assets/chlimage_1-67.png)

### 가입 확인 목록(캠페인) {#subscriptions-checklist-campaign}

사용 **구독 체크리스트(캠페인)** Adobe Campaign 프로필과 연결된 구독을 수정할 구성 요소입니다.

양식에 추가되면 이 구성 요소는 사용 가능한 모든 구독을 확인란으로 표시하고 사용자가 원하는 구독을 선택할 수 있도록 합니다. 사용자가 양식을 제출할 때 이 구성 요소는 양식 작업 유형에 따라 사용자를 선택한 서비스에 가입시키거나 가입을 취소합니다(**Adobe Campaign: 서비스에 가입** 또는 **Adobe Campaign: 서비스에서 구독 취소**).

>[!NOTE]
>
>구성 요소는 사용자가 이미 구독/구독 취소한 서비스를 확인하지 않습니다.

다음을 수행할 수 있습니다. [대부분의 Adobe Campaign 구성 요소에 공통되는 설정 구성](#settings-common-to-most-components) ( 구독 체크리스트 (캠페인) 구성 요소 참조). (이 구성 요소에 사용할 수 있는 Adobe Campaign 구성이 없습니다.)

다음 예에서는 표시되는 구독 체크리스트(캠페인) 구성 요소를 보여 줍니다.

![chlimage_1-68](assets/chlimage_1-68.png)

### 텍스트 필드(캠페인) {#text-field-campaign}

텍스트 필드(캠페인) 구성 요소를 사용하여 이름, 성, 주소, 이메일 주소 등과 같은 문자열 유형 데이터를 입력할 수 있습니다.

에 더하여 [대부분의 Adobe Campaign 구성 요소에 공통되는 설정](#settings-common-to-most-components), 다음을 구성할 수 있습니다.

* **제한 - 제한** 드롭다운 다음을 선택할 수 있습니다. **없음,** **이메일**, 또는 **이름** (모음 기호 없음) - 이메일 주소, 이름 또는 제한 없음의 제한을 추가합니다. 이메일을 선택하는 경우 필드에 입력하는 응답 사용자는 이메일 주소여야 합니다. 이름을 선택하는 경우 이름이 되어야 합니다(모음 기호 는 허용되지 않음).

* **제한 메시지** 또한 제한 메시지를 추가하여 사용자가 답변의 서식을 올바르게 지정하는 방법을 알 수 있습니다.
* **스타일링 - 폭** 필드를 클릭하거나 탭하여 너비를 조정합니다. **+** 및 **-** 아이콘 또는 숫자 입력.

다음 예제에서는 표시되는 텍스트 필드(캠페인) 구성 요소를 보여 줍니다.

![chlimage_1-69](assets/chlimage_1-69.png)
