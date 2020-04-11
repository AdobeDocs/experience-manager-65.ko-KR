---
title: '적응형 양식 스타일 지정 '
seo-title: '적응형 양식 스타일 지정 '
description: '사용자 정의 테마 만들기, 개별 구성 요소 스타일 지정, 테마에서 웹 글꼴 사용 방법 학습 '
seo-description: '사용자 정의 테마 만들기, 개별 구성 요소 스타일 지정, 테마에서 웹 글꼴 사용 방법 학습 '
page-status-flag: de-activated
uuid: ffb2cc22-baaf-4525-a2e3-29f39271c670
topic-tags: introduction
discoiquuid: 655303a4-99bb-4ba3-9d50-a178f5edcf85
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317

---


# 적응형 양식 스타일 지정 {#do-not-publish-style-your-adaptive-form}

사용자 정의 테마 만들기, 개별 구성 요소 스타일 지정, 테마에서 웹 글꼴 사용 방법 학습

![](do-not-localize/08-style_your_adaptiveformmain.png)

이 자습서는 첫 번째 적응형 [양식 만들기 시리즈의](https://helpx.adobe.com/experience-manager/6-3/forms/using/create-your-first-adaptive-form.html) 단계입니다. 전체 자습서 사용 사례를 이해하고, 실행하고, 시연하기 위해 시리즈를 시간 순서대로 따르는 것이 좋습니다.

## 자습서 정보 {#about-the-tutorial}

테마를 사용하여 적응형 양식에 고유한 모양과 스타일을 제공할 수 있습니다. 적응형 양식 편집기로 제공되는 테마를 즉시 적용하거나 자신만의 테마를 만들 수 있습니다. AEM Forms에서는 사용자 정의 테마를 만드는 [테마 편집기를](https://helpx.adobe.com/experience-manager/6-3/forms/using/themes.html) 제공합니다. 단일 테마는 모바일, 태블릿 또는 데스크탑에서 열린 동일한 적응형 양식에 서로 다른 모양을 제공할 수 있습니다. CSS 또는 LESS에 대한 사전 지식은 테마 편집기를 사용하는 데 필요하지 않지만 원하는 기능입니다.

튜토리얼이 종료되면 다음 방법을 배울 수 있습니다.

* 즉시 사용 가능한 양식에 테마 적용
* 테마 편집기를 사용하여 적응형 양식의 테마 만들기
* 개별 구성 요소 스타일 지정
* 보너스 섹션:사용자 정의 테마에서 웹 글꼴 사용

이 양식은 튜토리얼을 완료한 후 다음과 비슷합니다.

![사용자 정의 테마가 있는 양식](assets/styled-adaptive-form.png)

## Before you start {#before-you-start}

로컬 시스템에서 헤더 스타일 및 로고 이미지를 다운로드합니다. 적응형 양식의 머리글에는 머리글 스타일 및 로고 이미지가 사용됩니다. `shipping-address-add-update-form` 헤더 스타일 이미지가 헤더의 오른쪽에 나타납니다.

[파일 가져오기](assets/header-style.png)

[파일 가져오기](assets/logo-1.png)

## 1단계:적응형 양식에 테마 적용 {#step-apply-a-theme-to-your-adaptive-form}

적응형 양식 편집기는 즉시 사용 가능한 여러 테마를 제공합니다. 적응형 양식에 사용자 정의 스타일을 사용하지 않으려는 경우 즉시 사용 가능한 테마를 사용하여 적응형 양식을 게시할 수도 있습니다. 테마는 적응형 양식과 독립적입니다. 동일한 테마를 여러 적응형 양식에 적용할 수 있습니다. 적응형 양식에 테마를 적용하려면:

1. 편집할 적응형 양식을 엽니다.

   [http://localhost:4502/editor.html/content/forms/af/shipping-address-add-update-form.html](http://localhost:4502/editor.html/content/forms/af/shipping-address-add-update-form.html)

1. 적응형 양식 **컨테이너의**&#x200B;속성을 엽니다. 속성 브라우저에서 기본 > **적응형 양식** 테마로 **이동합니다**. 적응형 **양식 테마** 필드에는 모든 기본 테마와 사용자 정의 테마가 나열됩니다. 기본적으로 캔버스 테마가 적용됩니다.
1. 적응형 양식 테마 **필드에서 테마를** 선택합니다. 예를 들어 설문 조사 **테마를**&#x200B;참조하십시오. aem_ ![6_3_forms_save](assets/aem_6_3_forms_save.png) 를 눌러 선택한 테마를 적용합니다.

![기본 테마가 있는 적응형 양식](assets/default-adaptive-form.png)

**그림:** 기본 *테마가 있는 적응형 양식*

![설문 조사 테마를 사용한 적응형 양식](assets/adaptive-form-with-survey-theme.png)

**그림:** 설문 *조사 테마를 사용한 적응형 양식*

## 2단계:적응형 양식 업데이트 {#step-update-your-adaptive-form}

위에 표시된 디자인은 기존의 적응형 양식의 자리 표시자 텍스트 및 로고를 변경해야 합니다. 다음 단계를 수행하여 필요한 사항을 변경합니다.

1. 헤더의 기존 로고와 텍스트를 변경합니다. 로고를 제거하려면:

   1. 양식 편집기에서 양식을 엽니다.

      [http://localhost:4502/editor.html/content/forms/af/shipping-address-add-update-form.html](http://localhost:4502/editor.html/content/forms/af/shipping-address-add-update-form.html)

   1. 헤더 구성 요소에서 로고 이미지를 누르고 cmppr ![속성을](assets/cmppr.png) 누릅니다. 이미지 속성에서 X를 눌러 기존 로고 이미지를 제거합니다.
   1. 업로드를 누르고 logo.png를 선택한 다음 ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png) 를 눌러 변경 사항을 저장합니다. 이미지가 시작하기 [전에](/help/forms/using/style-your-adaptive-form.md#before-you-start) 다운로드되었습니다.
   1. 머리글 텍스트를 `We.Retail`누르고 ![aem_6_3_edit](assets/aem_6_3_edit.png) **편집을**&#x200B;누릅니다. 머리글 텍스트를 로 `we retail`변경합니다. 굵은체 서식을 `we`in에만 적용합니다 `we retail`.
   ![we-retail-logo-text](assets/we-retail-logo-text.png)

1. 제목을 제거하고 자리 표시자 텍스트를 추가합니다.

   1. 고객 ID 필드를 누르고 cmppr ![속성을](assets/cmppr.png) 누릅니다.
   1. 제목 필드의 내용을 **자리 표시자** 텍스트 **필드에 복사합니다** .
   1. 제목 필드의 내용을 **삭제하고** aem_6_ ![3_forms_save](assets/aem_6_3_forms_save.png)를 누릅니다.
   1. 양식의 모든 텍스트 상자, 숫자 상자 및 이메일 필드에 대해 이전 3단계를 반복합니다.
   ![updated-adaptive-form](assets/updated-adaptive-form.png)

## 3단계:적응형 양식의 사용자 정의 테마 만들기 {#step-create-a-custom-theme-for-your-adaptive-form}

테마 [편집기를](/help/forms/using/themes.md) 사용하여 사용자 정의 테마를 만들 수 있습니다. 테마 편집기는 강력한 WYSIWYG 편집기입니다. 적응형 양식의 다양한 구성 요소에 CSS를 적용하는 시각적 방법입니다. 응용 양식의 구성 요소와 패널에 스타일을 지정하는 미세한 컨트롤을 제공합니다.

테마는 적응형 양식과 같은 별도의 엔티티입니다. 응용 양식의 구성 요소와 패널에 대한 스타일(CSS)이 포함되어 있습니다. 스타일은 배경색, 상태 색상, 투명도, 정렬 및 크기와 같은 CSS 속성을 포함합니다. 테마를 적용하면 지정된 스타일이 적응형 양식의 해당 구성 요소에 적용됩니다.

이 자습서에서는 머리글과 바닥글, 텍스트 및 숫자 구성 요소, 첨부 구성 요소 및 단추의 스타일을 지정합니다. 먼저 테마를 만들어 보겠습니다.

### 테마 만들기 {#create-a-theme}

1. AEM 작성자 인스턴스에 로그인하고 Adobe Experience Manager > **양식** > 테마를 **탐색합니다******. 기본 URL은 http://localhost:4502/aem/forms.html/content/dam/formsanddocuments-themes [입니다](http://localhost:4502/aem/forms.html/content/dam/formsanddocuments-themes).
1. 만들기를 **[!UICONTROL 누르고]** 테마를 **[!UICONTROL 선택합니다]**. 테마를 만드는 데 필요한 필드가 있는 테마 만들기 페이지가 나타납니다. 제목 및 이름 필드는 필수입니다.

   * **제목:** 테마의 제목을 지정합니다. 예: 전역 **테마.** 제목은 테마 목록에서 테마를 식별하는 데 도움이 됩니다.
   * **이름:** 테마 이름을 지정합니다. 예: **전역 테마.** 지정된 이름의 노드가 저장소에 생성됩니다. 제목을 입력하기 시작하면 이름 필드의 값이 자동으로 생성됩니다. 제안된 값을 변경할 수 있습니다. 이름 필드에는 영숫자, 하이픈 및 밑줄만 사용할 수 있습니다. 잘못된 입력은 모두 하이픈으로 대체됩니다.

1. 만들기를 **누릅니다**. 테마가 생성되고 편집할 양식을 여는 대화 상자가 나타납니다. 열기를 **눌러** 새로 만든 테마를 새 탭에서 엽니다. 테마가 테마 편집기에서 열립니다. 스타일링을 위해 테마 편집기는 AEM Forms와 함께 제공된 즉시 사용 가능한 양식을 사용합니다.

   테마 편집기 UI 사용에 대한 자세한 내용은 [테마 편집기](/help/forms/using/themes.md#aboutthethemeeditor)정보를 참조하십시오.

1. 테마 **옵션** ![](assets/theme-options.png) 테마 옵션 **> 구성을**&#x200B;누릅니다. 양식 미리 보기 **필드에서** shipping-address-add-update-form **적응형 양식을** 선택하고 ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png)**를 누르고 저장을**&#x200B;누릅니다. 이제 테마 편집기가 기본 적응형 양식 대신 자신만의 적응형 양식을 사용하도록 구성됩니다. 취소를 **눌러** 테마 편집기로 돌아갑니다.

   ![맞춤형 테마](assets/custom-theme.png)

   **그림:** shipping-address-add-update-form 적응형 양식이 *포함된 테마 편집기*

   ![테마 만들기](assets/create-a-theme.png)

   **그림:** 기본 *양식이 있는 적응형 양식*

### 스타일 머리글 및 바닥글 {#style-header-and-footer}

머리글과 바닥글은 적응형 양식의 모양과 모양을 일관되게 제공합니다. 일반적으로 머리글에는 조직의 로고와 이름이 포함되어 있고, 바닥글에는 저작권 정보가 포함되어 있으며, 이러한 정보는 조직의 여러 양식에 걸쳐 동일하게 유지됩니다. shipping-address-add-update-form 적응형 양식의 머리글과 바닥글의 스타일을 지정하려면:

1. 선택기 패널에서 **머리글** > **텍스트** 옵션을 탐색합니다. 선택기 패널은 테마 편집기 왼쪽에 있습니다. 패널이 보이지 않으면 사이드 패널 전환을 ![](assets/toggle-side-panel.png) 누릅니다.

1. 텍스트 아코디언에서 다음 **속성을** 설정하고 ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png)를 누릅니다.

   | 속성 | 값 |
   |---|---|
   | 글꼴 모음 | Arial |
   | 글꼴 색상 | FFFFFF |
   | 글꼴 크기 | 54px |

1. 머리글 위젯을 누르고 헤더를 **누릅니다**. 머리글 위젯의 스타일을 지정하는 옵션이 왼쪽에 표시됩니다. [ **차원 및 위치** ] 아코디언을 확장하고 **[** 높이]를 `120px`설정한 ![다음](assets/aem_6_3_forms_save.png)aem_6_3_forms_save를 누릅니다.
1. 머리글 위젯의 배경 아코디언을 확장하고 배경색을 **다음으로** 설정합니다 `F6921E.`

   이미지 및 **그라디언트** > **+ 추가**, **이미지를**&#x200B;누릅니다. 다음 속성을 설정하고 ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png)를 누릅니다.

   | 속성 | 값 |
   |---|---|
   | 이미지 | header-style.png를 업로드합니다. 이미지가 시작하기 [전에](/help/forms/using/style-your-adaptive-form.md#before-you-start) 다운로드되었습니다. |
   | 위치 | 오른쪽 단추 |
   | 바둑판식으로 배열 | 반복 안 함 |

1. 테마 편집기에서 헤더의 로고를 누르고 머리글 로고를 **누릅니다**. 차원 및 위치 아코디언을 확장하고 다음 속성을 설정한 다음 ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png)를 누릅니다.

<table> 
 <tbody> 
  <tr> 
   <td>여백</td> 
   <td>값</td> 
  </tr> 
  <tr> 
   <td>여백</td> 
   <td> 
    <ul> 
     <li>위쪽:1.5렘</li> 
     <li>아래:-35px</li> 
     <li>왼쪽:1렘<strong><br /></strong></li> 
    </ul> <p><strong>팁:</strong> 각 필드에 다른 값을 제공하려면 <img src="assets/link.png"> 링크 아이콘을 누릅니다.<br /> </p> </td> 
  </tr> 
  <tr> 
   <td>높이</td> 
   <td>4.75rem</td> 
  </tr> 
 </tbody> 
</table>

1. 바닥글 위젯을 누르고 바닥글을 **누릅니다**. 배경 **아코디언을** 확장하고 **배경색을** 다음으로 설정한 `F6921E`다음 ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png)를 누릅니다.

### 데이터 캡처 구성 요소의 스타일을 지정하고 적응형 양식에 배경 적용 {#style-the-data-capture-component-and-apply-a-background-to-the-adaptive-form}

적응형 양식의 여러 구성 요소를 사용하여 데이터를 캡처할 수 있습니다. 예를 들어, 텍스트 상자 및 숫자 상자 모든 데이터 캡처 구성 요소에 동일한 스타일을 제공하거나 각 구성 요소에 대해 별도의 스타일을 제공할 수 있습니다. 이 자습서에서는 동일한 스타일이 숫자 상자(고객 ID, 우편 번호) 및 텍스트 상자(고객 ID, 이름, 배송 주소, 상태, 이메일)에 적용됩니다. 데이터 캡처 구성 요소의 스타일을 지정하려면

1. 고객 ID 필드를 누르고 필드 위젯 **옵션을** 누릅니다. 다음 속성을 설정하고 ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png)를 누릅니다.

<table> 
 <tbody> 
  <tr> 
   <td>어코디언</td> 
   <td>속성</td> 
   <td>값</td> 
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
     <li>위쪽:7px<br /> </li> 
     <li>오른쪽:7px<br /> </li> 
     <li>아래:7px<br /> </li> 
     <li>왼쪽:7px<br /> </li> 
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
   <td>차원 및 위치</td> 
   <td>너비</td> 
   <td>60%</td> 
  </tr> 
  <tr> 
   <td>차원 및 위치</td> 
   <td>여백</td> 
   <td> 
    <ul> 
     <li>왼쪽:10렘</li> 
    </ul> </td> 
  </tr> 
 </tbody> 
</table>

1. 고객 ID 필드 위의 빈 영역을 누르고 응답형 패널 **컨테이너를 누릅니다**. 배경 **> 배경색을** **F** 1F2F2로 설정합니다. aem_ ![6_3_forms_save](assets/aem_6_3_forms_save.png).

   ![](do-not-localize/responsive-panel-container.png)

### 단추 스타일 지정 {#style-the-buttons}

사용자 정의 테마를 사용하여 응용 양식 및 [인라인 스타일의](/help/forms/using/inline-style-adaptive-forms.md) 모든 단추에 동일한 스타일을 적용하여 특정 단추에 스타일을 적용할 수 있습니다. 단추 스타일을 지정하려면:

1. 제출 **단추를** 누르고 단추 **옵션을 누릅니다** . 다음 속성을 설정하고 ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png)를 누릅니다.

<table> 
 <tbody> 
  <tr> 
   <td>어코디언</td> 
   <td>속성</td> 
   <td>값</td> 
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
     <li>위쪽:7px<br /> </li> 
     <li>오른쪽:7px<br /> </li> 
     <li>아래:7px<br /> </li> 
     <li>왼쪽:7px</li> 
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

1. [사용자 정의 테마인](/help/forms/using/style-your-adaptive-form.md#step-apply-a-theme-to-your-adaptive-form)전역 테마를 응용 양식에 적용합니다. 스타일이 응용 양식에 반영되지 않으면 브라우저 캐시를 정리하고 다시 시도하십시오.

   ![style-data-capture-components](assets/style-data-capture-components.png)

## 4단계:개별 구성 요소 스타일 지정 {#step-style-individual-components}

일부 스타일은 특정 구성 요소에만 적용됩니다. 이러한 구성 요소는 적응형 양식 편집기에서 스타일이 지정됩니다.

1. 편집할 적응형 양식을 엽니다. [http://localhost:4502/editor.html/content/forms/af/shipping-address-add-update-form.html](http://localhost:4502/editor.html/content/forms/af/change-billing-shipping-address.html)
1. 상단 막대에서 스타일 **옵션을 선택합니다** .

   ![style-option](assets/style-option.png)

1. 첨부 **단추를** 누르고 ![aem_6_3_](assets/aem_6_3_edit.png)editicon을 누릅니다. [차원] 및 [위치] **아코디언에서 다음 속성을** 설정합니다.

   | 속성 | 값 |
   |---|---|
   | 부동 | 왼쪽 |
   | 너비 | 10% |

1. 정부 승인 **주소 증명** 옵션을 누르고 ![aem_6_3_](assets/aem_6_3_edit.png)editicon을 누릅니다. 다음 속성을 설정합니다.

<table> 
 <tbody> 
  <tr> 
   <td>어코디언</td> 
   <td>속성</td> 
   <td>값</td> 
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
     <li>왼쪽:10픽셀</li> 
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
     <li>오른쪽:2rem</li> 
     <li>왼쪽:10렘 </li> 
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
 </tbody> 
</table>

1. 제출 **단추를 누르고** aem_6_ ![3_edit](assets/aem_6_3_edit.png) 아이콘을 누릅니다. 다음 속성을 설정합니다.

<table> 
 <tbody> 
  <tr> 
   <td>어코디언</td> 
   <td>속성</td> 
   <td>값</td> 
  </tr> 
  <tr> 
   <td>차원 및 위치</td> 
   <td>부동</td> 
   <td>오른쪽</td> 
  </tr> 
  <tr> 
   <td>차원 및 위치</td> 
   <td>여백</td> 
   <td> 
    <ul> 
     <li>위쪽:5렘</li> 
     <li>오른쪽:14렘</li> 
     <li>아래:20px</li> 
     <li>왼쪽:20px<br /> </li> 
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

## 5단계:보너스 섹션:사용자 정의 테마에서 웹 글꼴 사용 {#step-bonus-section-using-web-fonts-in-a-custom-theme}

다양한 글꼴을 사용하여 적응형 양식을 디자인할 수 있습니다. 응용 양식을 보는 모든 장치에 응용 양식을 디자인하는 데 사용되는 글꼴이 없을 수 있습니다. 웹 글꼴 서비스를 사용하여 필요한 글꼴을 대상 장치에 제공할 수 있습니다.

Adobe Typekit은 웹 글꼴 서비스입니다. 적응형 양식과 함께 서비스를 구성하고 사용할 수 있습니다. 적응형 양식으로 Adobe Typekit를 사용하려면:

>[!NOTE]
>
>![typekit-to-adobe-fonts](assets/typekit-to-adobe-fonts.png) Typekit는 이제 Adobe Fonts라고 하며 Creative Cloud 및 기타 구독에 포함되어 있습니다. [추가 정보](https://fonts.adobe.com/).

1. Adobe [Typekit](https://typekit.com/) 계정을 만들고, 키트를 만들고, Myriad Pro 글꼴을 키트에 추가하고, 키트를 게시하고, 키트 ID를 얻습니다. 적응형 양식으로 Adobe Typekit 글꼴(웹 글꼴)을 사용해야 합니다.
1. AEM Forms 서버에서 ![adobe Experience Manager](assets/adobeexperiencemanager.png) **> Tools** **** ![](assets/hammer.png) Himmer > Deployment **Deployment** > Cloud Services로 이동합니다 ****. 클라우드 서비스 페이지에서 타사 서비스 > **Typekit으로** 이동한 **다음** Typekit **에서 지금** 구성을클릭합니다. 구성을 이미 사용할 수 있는 경우 + 단추를 클릭하여 새 인스턴스를 만듭니다.

   구성 만들기 대화 상자에서 구성에 **대한 제목을** 지정하고 만들기를 **클릭합니다**. 구성 페이지로 리디렉션됩니다. 표시되는 구성 요소 편집 대화 상자에서 키트 ID를 **제공하고** 확인을 **클릭합니다**.

1. TypeKit 구성을 사용하도록 테마를 구성합니다. 작성자 인스턴스의 테마 **편집기에서 전역** 테마를 엽니다. 테마 편집기에서 테마 옵션 ![테마 옵션](assets/theme-options.png) > 구성으로 이동합니다. Typekit **구성** 필드에서 키트를 선택하고 저장을 **클릭합니다**.

   Typekit에 추가된 글꼴은 모든 구성 요소의 텍스트 **아코디언에서** 선택할 수 있습니다.

