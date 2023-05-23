---
title: 적응형 양식 스타일 지정
seo-title: Style your adaptive form
description: 사용자 지정 테마를 만들고, 개별 구성 요소의 스타일을 지정하고, 테마에서 웹 글꼴을 사용하는 방법을 알아봅니다
seo-description: Learn to create a custom theme, style individual components, and use web fonts in a theme
page-status-flag: de-activated
uuid: ffb2cc22-baaf-4525-a2e3-29f39271c670
topic-tags: introduction
discoiquuid: 655303a4-99bb-4ba3-9d50-a178f5edcf85
feature: Adaptive Forms
exl-id: 7742c3ca-1755-44c5-b70f-61309f09d1b8
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '2037'
ht-degree: 8%

---

# 적응형 양식 스타일 지정 {#do-not-publish-style-your-adaptive-form}

사용자 지정 테마를 만들고, 개별 구성 요소의 스타일을 지정하고, 테마에서 웹 글꼴을 사용하는 방법을 알아봅니다

![](do-not-localize/08-style_your_adaptiveformmain.png)

이 튜토리얼의 단계는 다음과 같습니다. [첫 번째 적응형 양식 만들기](https://helpx.adobe.com/kr/experience-manager/6-3/forms/using/create-your-first-adaptive-form.html) 시리즈. 전체 자습서 사용 사례를 이해하고, 수행하고, 시연하려면 연대순으로 시리즈를 따르는 것이 좋습니다.

## 튜토리얼 기본 정보  {#about-the-tutorial}

테마를 사용하여 적응형 양식에 고유한 모양과 스타일을 제공할 수 있습니다. 적응형 양식 편집기와 함께 제공되는 즉시 테마를 적용하거나 자신만의 사용자 지정 테마를 만들 수 있습니다. AEM [!DNL Forms] 다음을 제공하십시오. [테마 편집기](https://helpx.adobe.com/experience-manager/6-3/forms/using/themes.html) 사용자 지정 테마를 만들 수 있습니다. 단일 테마는 모바일, 태블릿 또는 데스크탑에서 열린 동일한 적응형 양식에 다른 모양을 제공할 수 있습니다. 테마 편집기를 사용하려면 CSS 이하에 대한 사전 지식이 필요하지 않지만 필요합니다.

자습서를 마칠 때까지 다음 사항을 배울 수 있습니다.

* 적응형 양식에 즉시 사용 가능한 테마 적용
* 테마 편집기를 사용하여 적응형 양식에 대한 테마 만들기
* 개별 구성 요소 스타일 지정
* 보너스 섹션: 사용자 정의 테마에서 웹 글꼴 사용

자습서를 완료한 후 양식은 다음과 유사합니다.

![사용자 정의 테마가 있는 양식](assets/styled-adaptive-form.png)

## 시작하기 전 {#before-you-start}

로컬 컴퓨터에서 아래 제공된 헤더 스타일 및 로고 이미지를 다운로드합니다. 의 헤더 `shipping-address-add-update-form` 적응형 양식은 머리글 스타일 및 로고 이미지를 사용합니다. 헤더 스타일 이미지가 헤더의 오른쪽에 나타납니다.

[파일 가져오기](assets/header-style.png)

[파일 가져오기](assets/logo-1.png)

## 1단계: 적응형 양식에 테마 적용 {#step-apply-a-theme-to-your-adaptive-form}

적응형 양식 편집기는 다양한 기본 테마를 제공합니다. 적응형 양식에 사용자 지정 스타일을 사용하지 않을 계획이라면 기본 테마가 있는 적응형 양식을 게시할 수도 있습니다. 테마는 적응형 양식과 독립적입니다. 동일한 테마를 여러 적응형 양식에 적용할 수 있습니다. 적응형 양식에 테마를 적용하려면 다음을 수행합니다.

1. 편집할 적응형 양식을 엽니다.

   [http://localhost:4502/editor.html/content/forms/af/shipping-address-add-update-form.html](http://localhost:4502/editor.html/content/forms/af/shipping-address-add-update-form.html)

1. 다음의 속성 열기 **[!UICONTROL 적응형 양식 컨테이너]**. 속성 브라우저에서 다음 위치로 이동합니다 **[!UICONTROL 기본]** > **[!UICONTROL 적응형 양식 테마]**. 다음 **[!UICONTROL 적응형 양식 테마]** 필드에는 기본 제공 테마와 사용자 지정 테마가 모두 나열됩니다. 기본적으로 캔버스 테마가 적용됩니다.
1. 다음에서 테마 선택 **[!UICONTROL 적응형 양식 테마]** 필드. 예를 들어, **설문 조사 테마**. 누르기 ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png) 을 눌러 선택한 테마를 적용합니다.

   ![기본 테마를 사용한 적응형 양식](assets/default-adaptive-form.png)

   **그림:** *기본 테마를 사용한 적응형 양식*

   ![설문 조사 테마를 사용한 적응형 양식](assets/adaptive-form-with-survey-theme.png)

   **그림:** *설문 조사 테마를 사용한 적응형 양식*

## 2단계: 적응형 양식 업데이트 {#step-update-your-adaptive-form}

위에 표시된 디자인을 사용하려면 기존 적응형 양식의 자리 표시자 텍스트와 로고를 변경해야 합니다. 필요한 사항을 변경하려면 다음 단계를 수행하십시오.

1. 헤더의 기존 로고 및 텍스트를 변경합니다. 로고를 제거하려면:

   1. 양식 편집기에서 양식을 엽니다.

      [http://localhost:4502/editor.html/content/forms/af/shipping-address-add-update-form.html](http://localhost:4502/editor.html/content/forms/af/shipping-address-add-update-form.html)

   1. 에서 로고 이미지 탭하기 [!UICONTROL 머리글] 구성 요소 및 탭 ![cmppr](assets/cmppr.png) **[!UICONTROL 속성]**. 다음에서 [!UICONTROL 이미지] 속성을 사용하려면 X를 눌러 기존 로고 이미지를 제거합니다.
   1. 누르기 **[!UICONTROL 업로드]**, logo.png를 선택하고 을 누릅니다. ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png) 변경 내용을 저장합니다. 이미지는 다음에 다운로드되었습니다. [시작하기 전에](/help/forms/using/style-your-adaptive-form.md#before-you-start) 섹션.
   1. 머리글 텍스트, 탭 `We.Retail`, 및 탭 ![aem_6_3_edit](assets/aem_6_3_edit.png) **[!UICONTROL 편집]**. 헤더 텍스트를 다음으로 변경 `we retail`. 굵게 서식만 적용 `we`위치: `we retail`.

      ![we-retail-logo-text](assets/we-retail-logo-text.png)

1. 제목을 제거하고 자리 표시자 텍스트를 추가합니다.

   1. 고객 ID 필드를 탭하고 을 누릅니다. ![cmppr](assets/cmppr.png) 속성.
   1. 의 콘텐츠 복사 **[!UICONTROL 제목]** 필드 대상 **[!UICONTROL 자리 표시자 텍스트]** 필드.
   1. 의 콘텐츠 삭제 **[!UICONTROL 제목]** 필드 및 탭 ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png).
   1. 양식의 모든 텍스트 상자, 숫자 상자 및 전자 메일 필드에 대해 이전 세 단계를 반복합니다.

      ![업데이트된 적응형 양식](assets/updated-adaptive-form.png)

## 3단계: 적응형 양식에 대한 사용자 지정 테마 만들기 {#step-create-a-custom-theme-for-your-adaptive-form}

다음을 사용할 수 있습니다. [테마 편집기](/help/forms/using/themes.md) 사용자 지정 테마를 만들 수 있습니다. 테마 편집기는 강력한 WYSIWYG 편집기입니다. CSS를 적응형 양식의 다양한 구성 요소에 적용하는 시각적 방법입니다. 적응형 양식의 구성 요소 및 패널에 스타일을 지정할 수 있는 보다 세밀한 컨트롤을 제공합니다.

테마는 적응형 양식과 같은 별도의 엔티티입니다. 여기에는 적응형 양식의 구성 요소 및 패널에 대한 스타일(CSS)이 포함되어 있습니다. 스타일에는 배경색, 상태 색상, 투명도, 정렬 및 크기와 같은 CSS 속성이 포함됩니다. 테마를 적용하면 지정된 스타일이 적응형 양식의 해당 구성 요소에 적용됩니다.

이 자습서에서는 머리글 및 바닥글, 텍스트 및 숫자 구성 요소, 첨부 파일 구성 요소 및 단추에 스타일을 지정합니다. 테마 만들기부터 시작하겠습니다.

### 테마 만들기 {#create-a-theme}

1. AEM 작성자 인스턴스에 로그인하고 다음으로 이동합니다. **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL 테마]**. 기본 URL은 [http://localhost:4502/aem/forms.html/content/dam/formsanddocuments-themes](http://localhost:4502/aem/forms.html/content/dam/formsanddocuments-themes).
1. 누르기 **[!UICONTROL 만들기]** 및 선택 **[!UICONTROL 테마]**. 다음 [!UICONTROL 테마 만들기] 테마를 만드는 데 필요한 필드가 있는 페이지가 나타납니다. 다음 **[!UICONTROL 제목]** 및 **[!UICONTROL 이름]** 필드는 필수입니다.

   * **제목:** 테마의 제목을 지정합니다. 예를 들어, **글로벌 테마.** 제목을 사용하면 테마 목록에서 테마를 식별할 수 있습니다.
   * **이름:** 테마의 이름을 지정합니다. 예를 들어, **글로벌 테마.** 지정된 이름의 노드가 저장소에 생성됩니다. 제목 입력을 시작하면 이름 필드에 대한 값이 자동으로 생성됩니다. 제안 값을 변경할 수 있습니다. 이름 필드에는 영숫자, 하이픈 및 밑줄만 포함할 수 있습니다. 잘못된 모든 입력은 하이픈으로 대체됩니다.

1. 누르기 **[!UICONTROL 만들기]**. 테마가 만들어지고 편집할 양식을 여는 대화 상자가 나타납니다. 누르기 **[!UICONTROL 열기]** 새 탭에서 새로 만든 테마를 엽니다. 테마가 테마 편집기에서 열립니다. 스타일링을 위해 테마 편집기는 AEM과 함께 제공되는 즉시 사용 가능한 적응형 양식을 사용합니다 [!DNL Forms].

   테마 편집기 UI 사용에 대한 자세한 내용은 [테마 편집기 기본 정보](/help/forms/using/themes.md#aboutthethemeeditor).

1. 누르기 **[!UICONTROL 테마 옵션]** ![theme-options](assets/theme-options.png) > **[!UICONTROL 구성]**. 다음에서 **[!UICONTROL 양식 미리 보기]** 필드에서 **shipping-address-add-update-form** 적응형 양식, 탭 ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png), 탭 **[!UICONTROL 저장]**. 이제 테마 편집기는 기본 적응형 양식 대신 고유한 적응형 양식을 사용하도록 구성되었습니다. 누르기 **[!UICONTROL 취소]** 테마 편집기로 돌아갑니다.

   ![사용자 정의 테마](assets/custom-theme.png)

   **그림:** *배송 주소 추가 업데이트 양식 적응형 양식이 있는 테마 편집기*

   ![테마 만들기](assets/create-a-theme.png)

   **그림:** *기본 양식이 있는 적응형 양식*

### 스타일 머리글 및 바닥글 {#style-header-and-footer}

머리글과 바닥글은 적응형 양식에 일관되고 고유한 모양을 제공합니다. 일반적으로 머리글에는 로고 및 조직 이름이 포함되고, 바닥글에는 저작권 정보가 포함되며, 이러한 정보는 조직의 여러 양식에서 동일하게 유지됩니다. shipping-address-add-update-form 적응형 양식의 머리글과 바닥글에 스타일을 지정하려면 다음을 수행합니다.

1. 탐색 **[!UICONTROL 머리글]** > **[!UICONTROL 텍스트]** 선택 사항에서 선택할 수 있습니다. 선택기 패널은 테마 편집기의 왼쪽에 있습니다. 패널이 표시되지 않으면 을 누릅니다 ![토글 사이드 패널](assets/toggle-side-panel.png) 사이드 패널을 전환합니다.

1. 에서 다음 속성을 설정합니다. **[!UICONTROL 텍스트]** 아코디언 및 탭 ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png).

   | 속성 | 값 |
   |---|---|
   | 글꼴 모음 | Arial |
   | 글꼴 색상 | FFFFFF |
   | 글꼴 크기 | 54px |

1. 탭 [!UICONTROL 머리글] 위젯 및 탭 **[!UICONTROL 머리글]**. 헤더 위젯의 스타일을 지정하는 옵션이 왼쪽에 나타납니다. 확장 **[!UICONTROL Dimension 및 위치]** 아코디언, 설정 **[!UICONTROL 높이]** 끝 `120px`, 및 탭 ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png).
1. 확장 **[!UICONTROL 배경]** 헤더 위젯의 아코디언에서 **[!UICONTROL 배경색]** 끝 `F6921E.`

   마우스로 가리키기 **[!UICONTROL 이미지 및 그라데이션]** > **[!UICONTROL + 추가]**, 탭 **[!UICONTROL 이미지]**. 다음 속성을 설정하고 을 누릅니다 ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png).

   | 속성 | 값 |
   |---|---|
   | 이미지 | header-style.png를 업로드합니다. 이미지는 다음에 다운로드되었습니다. [시작하기 전에](/help/forms/using/style-your-adaptive-form.md#before-you-start) 섹션. |
   | 위치 | 오른쪽 단추 |
   | 바둑판식으로 배열 | 반복 안 함 |

1. 테마 편집기에서 헤더에서 로고를 탭한 다음 을 누릅니다 **[!UICONTROL 머리글 로고]**. Dimension 및 위치 아코디언을 확장하고 다음 속성을 설정한 다음 을 누릅니다 ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png).

   <table> 
    <tbody> 
     <tr> 
      <td><b>여백</b></td> 
      <td><b>값</b></td> 
     </tr> 
     <tr> 
      <td>여백</td> 
      <td> 
       <ul> 
        <li>위쪽: 1.5rem</li> 
        <li>하단: -35px</li> 
        <li>왼쪽: 1rem<strong><br /> </strong></li> 
       </ul> <p><strong>팁:</strong> 탭 <img src="assets/link.png"> 링크 아이콘 을 사용하여 각 필드에 다른 값을 제공할 수 있습니다.<br /> </p> </td> 
     </tr> 
     <tr> 
      <td>높이</td> 
      <td>4.75rem</td> 
     </tr> 
    </tbody> 
   </table>

1. 바닥글 위젯을 탭하고 을 누릅니다 **[!UICONTROL 바닥글]**. 확장 **[!UICONTROL 배경]** 아코디언, 설정 **[!UICONTROL 배경색]** 끝 `F6921E`, 및 탭 ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png).

### 데이터 캡처 구성 요소의 스타일을 지정하고 적응형 양식에 배경을 적용합니다 {#style-the-data-capture-component-and-apply-a-background-to-the-adaptive-form}

적응형 양식에서 여러 구성 요소를 사용하여 데이터를 캡처할 수 있습니다. 예를 들어 텍스트 상자와 숫자 상자가 있습니다. 모든 데이터 캡처 구성 요소에 동일한 스타일을 제공하거나 각 구성 요소에 대해 별도의 스타일을 제공할 수 있습니다. 이 자습서에서는 숫자 상자(고객 ID, 우편 번호)와 텍스트 상자(고객 ID, 이름, 배송 주소, 상태, 이메일)에 동일한 스타일이 적용됩니다. 데이터 캡처 구성 요소의 스타일을 지정하려면 다음을 수행하십시오.

1. 탭 **[!UICONTROL 고객 ID]** 필드 및 탭 **[!UICONTROL 필드 위젯]** 옵션을 선택합니다. 다음 속성을 설정하고 을 누릅니다 ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png).

   <table> 
    <tbody> 
     <tr> 
      <td><b>아코디언</b></td> 
      <td><b>속성</b></td> 
      <td><b>값</b></td> 
     </tr> 
     <tr> 
      <td>테두리</td> 
      <td>테두리 색상</td> 
      <td>A7A9AC</td> 
     </tr> 
     <tr> 
      <td>테두리</td> 
      <td>테두리 반지름 </td> 
      <td> 
       <ul> 
        <li>위쪽: 7px<br /> </li> 
        <li>오른쪽: 7px<br /> </li> 
        <li>하단: 7px<br /> </li> 
        <li>왼쪽: 7px<br /> </li> 
       </ul> </td> 
     </tr> 
     <tr> 
      <td>텍스트</td> 
      <td>글꼴 모음</td> 
      <td>Arial</td> 
     </tr> 
     <tr> 
      <td>텍스트</td> 
      <td>글꼴 색상</td> 
      <td>939598<br /> </td> 
     </tr> 
     <tr> 
      <td>텍스트</td> 
      <td>글꼴 크기</td> 
      <td>18px</td> 
     </tr> 
     <tr> 
      <td>Dimension 및 위치</td> 
      <td>너비</td> 
      <td>60%</td> 
     </tr> 
     <tr> 
      <td>Dimension 및 위치</td> 
      <td>여백</td> 
      <td> 
       <ul> 
        <li>왼쪽: 10rem</li> 
       </ul> </td> 
     </tr> 
    </tbody> 
    </table>

1. 위의 빈 영역을 탭합니다. **[!UICONTROL 고객 ID]** 필드 및 탭 **[!UICONTROL 반응형 패널 컨테이너]**. 설정 **[!UICONTROL 배경]** > **[!UICONTROL 배경색]** F1F2F2로 이동합니다. 누르기 ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png).

   ![](do-not-localize/responsive-panel-container.png)

### 단추 스타일 지정 {#style-the-buttons}

사용자 지정 테마를 사용하여 적응형 양식의 모든 버튼에 동일한 스타일을 적용하고 [인라인 스타일 지정](/help/forms/using/inline-style-adaptive-forms.md) 특정 단추에 스타일을 적용합니다. 단추 스타일을 지정하려면 다음을 수행합니다.

1. 탭 **[!UICONTROL 제출]** 버튼을 클릭하고 탭 **[!UICONTROL 단추]** 옵션을 선택합니다. 다음 속성을 설정하고 을 누릅니다 ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png).

   <table> 
    <tbody> 
     <tr> 
      <td><b>아코디언</b></td> 
      <td><b>속성</b></td> 
      <td><b>값</b></td> 
     </tr> 
     <tr> 
      <td>배경</td> 
      <td>배경색</td> 
      <td>F6921E</td> 
     </tr> 
     <tr> 
      <td>테두리<br /> </td> 
      <td>테두리 색상</td> 
      <td>F6921E</td> 
     </tr> 
     <tr> 
      <td>테두리</td> 
      <td>테두리 반지름 </td> 
      <td> 
       <ul> 
        <li>위쪽: 7px<br /> </li> 
        <li>오른쪽: 7px<br /> </li> 
        <li>하단: 7px<br /> </li> 
        <li>왼쪽: 7px</li> 
       </ul> </td> 
     </tr> 
     <tr> 
      <td>텍스트<br /> </td> 
      <td>글꼴 모음</td> 
      <td>Arial</td> 
     </tr> 
     <tr> 
      <td>텍스트</td> 
      <td>글꼴 색상</td> 
      <td>FFFFFF</td> 
     </tr> 
     <tr> 
      <td>텍스트</td> 
      <td>글꼴 크기</td> 
      <td>18px</td> 
     </tr> 
    </tbody> 
   </table>

1. [사용자 정의 테마 적용](/help/forms/using/style-your-adaptive-form.md#step-apply-a-theme-to-your-adaptive-form), 전역 테마 를 적응형 양식에 추가합니다. 스타일이 적응형 양식에 반영되지 않으면 브라우저 캐시를 지우고 다시 시도하십시오.

   ![style-data-capture-components](assets/style-data-capture-components.png)

## 4단계: 개별 구성 요소 스타일 지정 {#step-style-individual-components}

일부 스타일은 특정 구성 요소에만 적용됩니다. 이러한 구성 요소는 적응형 양식 편집기에서 스타일을 지정합니다.

1. 편집할 적응형 양식을 엽니다. [http://localhost:4502/editor.html/content/forms/af/shipping-address-add-update-form.html](http://localhost:4502/editor.html/content/forms/af/change-billing-shipping-address.html)
1. 상단 막대에서 **[!UICONTROL 스타일]** 옵션을 선택합니다.

   ![style-option](assets/style-option.png)

1. 탭 **[!UICONTROL 첨부]** 버튼을 클릭하고 탭 ![aem_6_3_edit](assets/aem_6_3_edit.png)아이콘. 에서 다음 속성을 설정합니다. **[!UICONTROL Dimension 및 위치]** 아코디언:

   | 속성 | 값 |
   |---|---|
   | 부동 | 왼쪽 |
   | 너비 | 10% |

1. 탭 **[!UICONTROL 정부 승인 주소 증명]** 옵션 및 탭 ![aem_6_3_edit](assets/aem_6_3_edit.png)아이콘. 다음 속성을 설정합니다.

   <table> 
    <tbody> 
     <tr> 
      <td><b>아코디언</b></td> 
      <td><b>속성</b></td> 
      <td><b>값</b></td> 
     </tr> 
     <tr> 
      <td>치수 및 위치</td> 
      <td>부동</td> 
      <td>왼쪽</td> 
     </tr> 
     <tr> 
      <td>치수 및 위치</td> 
      <td>너비</td> 
      <td>73%</td> 
     </tr> 
     <tr> 
      <td>치수 및 위치</td> 
      <td>사진 간격</td> 
      <td> 
       <ul> 
        <li>왼쪽: 10px</li> 
       </ul> </td> 
     </tr> 
     <tr> 
      <td>치수 및 위치</td> 
      <td>높이</td> 
      <td>40px</td> 
     </tr> 
     <tr> 
      <td>치수 및 위치<br /> </td> 
      <td>여백</td> 
      <td><br /> 
       <ul> 
        <li>오른쪽: 2rem</li> 
        <li>왼쪽: 10rem </li> 
       </ul> </td> 
     </tr> 
     <tr> 
      <td>배경</td> 
      <td>배경색</td> 
      <td>FFFFFF</td> 
     </tr> 
     <tr> 
      <td>테두리</td> 
      <td>테두리 너비</td> 
      <td>1px</td> 
     </tr> 
     <tr> 
      <td>테두리</td> 
      <td>테두리 스타일</td> 
      <td>단색</td> 
     </tr> 
     <tr> 
      <td>테두리</td> 
      <td>테두리 색상</td> 
      <td>A7A9AC</td> 
     </tr> 
     <tr> 
      <td>테두리</td> 
      <td>테두리 반지름</td> 
      <td>7px</td> 
     </tr> 
     <tr> 
      <td>텍스트</td> 
      <td>글꼴 모음</td> 
      <td>Arial</td> 
     </tr> 
     <tr> 
      <td>텍스트</td> 
      <td>글꼴 색상</td> 
      <td>BCBEC0</td> 
     </tr> 
     <tr> 
      <td>텍스트</td> 
      <td>글꼴 크기</td> 
      <td>18px</td> 
     </tr> 
     <tr> 
      <td>텍스트</td> 
      <td>선 높이</td> 
      <td>2</td> 
     </tr> 
     </tr> 
    </tbody> 
   </table>

1. 탭 **[!UICONTROL 제출]** 버튼을 클릭하고 탭 ![aem_6_3_edit](assets/aem_6_3_edit.png) 아이콘. 다음 속성을 설정합니다.

   <table> 
    <tbody> 
     <tr> 
      <td><b>아코디언</b></td> 
      <td><b>속성</b></td> 
      <td><b>값</b></td> 
     </tr> 
     <tr> 
      <td>Dimension 및 위치</td> 
      <td>부동</td> 
      <td>오른쪽</td> 
     </tr> 
     <tr> 
      <td>Dimension 및 위치</td> 
      <td>여백</td> 
      <td> 
       <ul> 
        <li>위쪽: 5rem</li> 
        <li>오른쪽: 14rem</li> 
        <li>하단: 20px</li> 
        <li>왼쪽: 20px<br /> </li> 
       </ul> </td> 
     </tr> 
     <tr> 
      <td>배경</td> 
      <td>배경색</td> 
      <td>F6921E</td> 
     </tr> 
     <tr> 
      <td>테두리</td> 
      <td>테두리 색상</td> 
      <td>F6921E</td> 
     </tr> 
    </tbody> 
   </table>

   ![styled-adaptive-form-1](assets/styled-adaptive-form-1.png)

## 5단계: 보너스 섹션: 사용자 정의 테마에서 웹 글꼴 사용 {#step-bonus-section-using-web-fonts-in-a-custom-theme}

다양한 글꼴을 사용하여 적응형 양식을 디자인할 수 있습니다. 적응형 양식을 보는 모든 장치에는 적응형 양식을 디자인하는 데 사용되는 글꼴이 없을 수 있습니다. 웹 글꼴 서비스를 사용하여 필요한 글꼴을 대상 장치에 전달할 수 있습니다.

[!DNL Adobe Fonts] 는 웹 글꼴 서비스입니다. 적응형 양식에서 서비스를 구성하고 사용할 수 있습니다. 사용 [!DNL Adobe Fonts] 적응형 양식에서:

>[!NOTE]
>
>![typekit-to-adobe-fonts](assets/typekit-to-adobe-fonts.png) [!DNL Typekit] 는 이제 Adobe Fonts라고 하며 Creative Cloud 및 기타 구독에 포함됩니다. [자세히 알아보기](https://fonts.adobe.com/).

1. 만들기 [Adobe Fonts](https://typekit.com/) 계정, 키트를 만들고, Myriad Pro 글꼴을 키트에 추가하고, 키트를 게시하고 키트 ID를 가져옵니다. 다음을 사용해야 합니다. [!DNL Adobe Fonts] (Web fonts) 를 입력합니다.
1. AEM [!DNL Forms] 서버, 다음으로 이동 ![adobeexperiencemanger](assets/adobeexperiencemanager.png) **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL 도구]** ![망치](assets/hammer.png) > **[!UICONTROL Adobe Fonts]**. 이제 구성 폴더를 엽니다. 구성을 이미 사용할 수 있는 경우 **[!UICONTROL 만들기]** 단추를 클릭하여 새 인스턴스를 만듭니다.

   구성 만들기 대화 상자에서 **제목** 을 누르고 을 누릅니다. **[!UICONTROL 만들기]**. 구성 페이지로 리디렉션됩니다. 다음에서 [!UICONTROL 구성 요소 편집] 표시되는 대화 상자에서 **키트 ID** 및 클릭 **[!UICONTROL 확인]**.

1. 테마를 구성하여 사용 [!DNL Adobe Fonts] 구성. 작성자 인스턴스에서 을 엽니다. **[!UICONTROL 글로벌 테마]** 를 입력합니다. 테마 편집기에서 다음으로 이동 **[!UICONTROL 테마 옵션]** ![theme-options](assets/theme-options.png) > **[!UICONTROL 구성]**. 위치 **[!UICONTROL Adobe Fonts 구성]** 필드에서 키트를 선택하고 **[!UICONTROL 저장]**.

   에 추가된 글꼴 **[!UICONTROL Adobe Fonts]** 에서 선택할 수 있습니다. **[!UICONTROL 텍스트]** 모든 구성 요소의 아코디언
