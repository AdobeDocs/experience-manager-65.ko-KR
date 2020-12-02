---
title: '"자습서:적응형 양식 만들기"'
seo-title: '"적응형 양식 만들기"'
description: 적응형 양식을 만들고, 레이아웃하고, 미리 보는 방법을 알아봅니다. 또한 제출 작업을 구성하는 방법을 알아봅니다.
seo-description: 적응형 양식을 만들고, 레이아웃하고, 미리 보는 방법을 알아봅니다. 또한 제출 작업을 구성하는 방법을 알아봅니다.
page-status-flag: de-activated
uuid: 0010d274-a683-499e-9fa6-ce355d7898a0
discoiquuid: 55c08940-8c25-4938-8e49-25bce20aaf22
translation-type: tm+mt
source-git-commit: 78768e6eab65f452421d8809384500c6eab6b97f
workflow-type: tm+mt
source-wordcount: '1395'
ht-degree: 3%

---


# 자습서:응용 양식 {#do-not-publish-tutorial-create-an-adaptive-form} 만들기

![02-create-adaptive-form-main-image](assets/02-create-adaptive-form-main-image.png)

이 자습서는 [첫 번째 적응형 양식 만들기](/help/forms/using/create-your-first-adaptive-form.md) 시리즈의 한 단계입니다. 전체 자습서 사용 사례를 이해하고, 실행하고, 시연하려면 연순의 순서로 시리즈를 따르는 것이 좋습니다.

## 자습서 {#about-the-tutorial} 정보

적응형 양식은 동적이고 응답 속도가 빠른 새로운 생성 양식입니다. 적응형 양식을 사용하여 개인화된 경험을 전달할 수 있습니다. 사용 통계 및 캠페인 관리를 위해 [!DNL Adobe Analytics]과(와) 적응형 양식을 통합할 수도 있습니다. [!DNL Adobe Campaign] 적응형 양식 기능에 대한 자세한 내용은 [적응형 양식 작성 소개](/help/forms/using/introduction-forms-authoring.md)를 참조하십시오.

적합한 프로세스를 진행할 때 양식을 손쉽게 만들고 관리할 수 있습니다. 이 문서에서는 다음 방법을 알아봅니다.

* [고객이 배송 주소를 추가할 수 있는 적응형 양식 만들기](/help/forms/using/create-adaptive-form.md#step-create-the-adaptive-form)

* [고객의 정보를 표시하고 수락하는 응용 양식의 레이아웃 필드](/help/forms/using/create-adaptive-form.md#step-add-header-and-footer)

* [양식 컨텐츠가 포함된 이메일을 전송하는 제출 작업 만들기](/help/forms/using/create-adaptive-form.md#step-add-components-to-capture-and-display-information)
* [적응형 양식 미리 보기 및 제출](/help/forms/using/create-adaptive-form.md)

문서의 끝 부분에 다음과 유사한 양식이 있습니다.\
[![](do-not-localize/form-preview-mobile.gif)](do-not-localize/form-preview-mobile.gif)

## 1단계:응용 양식 {#step-create-the-adaptive-form} 만들기

1. AEM 작성자 인스턴스에 로그인하고 **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms 및 문서]**&#x200B;로 이동합니다. 기본 URL은 [http://localhost:4502/aem/forms.html/content/dam/formsanddocuments](http://localhost:4502/aem/forms.html/content/dam/formsanddocuments)입니다.
1. **[!UICONTROL 만들기]**&#x200B;를 누르고 **[!UICONTROL 응용 양식]**&#x200B;을 선택합니다. 템플릿을 선택하는 옵션이 나타납니다. **[!UICONTROL Blank]** 템플릿을 눌러 선택하고 **[!UICONTROL Next]**&#x200B;를 누릅니다.

1. **[!UICONTROL 속성 추가]**&#x200B;에 대한 옵션이 나타납니다. **[!UICONTROL 제목]** 및 **[!UICONTROL 이름]** 필드는 필수입니다.

   * **제목:** 제목 필드 `Add new or update shipping address` 에  **** 지정합니다. 제목 필드는 양식의 표시 이름을 지정합니다. 제목은 AEM [!DNL Forms] 사용자 인터페이스에서 양식을 식별하는 데 도움이 됩니다.
   * **이름:** 이름 필드 `shipping-address-add-update-form` 에서  **** 지정합니다. 이름 필드는 양식의 이름을 지정합니다. 지정한 이름의 노드가 저장소에 생성됩니다. 제목을 입력하기 시작하면 이름 필드에 대한 값이 자동으로 생성됩니다. 제안된 값을 변경할 수 있습니다. 이름 필드에는 영숫자, 하이픈 및 밑줄만 포함할 수 있습니다. 잘못된 입력은 모두 하이픈으로 대체됩니다.

1. **[!UICONTROL 만들기]**&#x200B;를 누릅니다. 응용 양식이 만들어지고 편집할 양식을 여는 대화 상자가 나타납니다. **[!UICONTROL 열기]**&#x200B;를 눌러 새로 만든 양식을 새 탭에서 엽니다. 편집할 양식이 열립니다. 필요에 따라 새로 만든 양식을 사용자 정의하는 사이드바를 표시합니다.

   적응형 양식 작성 인터페이스 및 사용 가능한 구성 요소에 대한 자세한 내용은 [적응형 양식 작성 소개](/help/forms/using/creating-adaptive-form.md)를 참조하십시오.

   ![새롭게 생성된 적응형](assets/newly-created-adaptive-form.png)

## 2단계:머리글 및 바닥글 {#step-add-header-and-footer} 추가

AEM [!DNL Forms]에서는 응용 양식에 대한 정보를 표시하는 여러 구성 요소를 제공합니다. 머리글 및 바닥글 구성 요소를 사용하면 양식의 모양과 느낌을 일관되게 제공할 수 있습니다. 헤더에는 일반적으로 기업의 로고, 양식의 제목 및 요약이 포함됩니다. 바닥글에는 일반적으로 저작권 정보와 다른 페이지에 대한 링크가 포함됩니다.

1. ![toggle-side-panel](assets/toggle-side-panel.png) > ![treeexpandall](assets/treeexpandall.png)을 누릅니다. 구성 요소 브라우저가 열립니다. 구성 요소 브라우저의 **[!UICONTROL 헤더]** 구성 요소를 응용 양식으로 드래그합니다.
1. **[!UICONTROL 로고]**&#x200B;를 누릅니다. 도구 모음이 나타납니다. 도구 모음에서 ![aem_6_3_edit](assets/aem_6_3_edit.png)을 탭하고 **We.Retail**&#x200B;을 입력하고 ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png)를 탭합니다.

1. 이미지를 누릅니다. 도구 모음이 나타납니다. ![cmppr](assets/cmppr.png)을 누릅니다. 화면 왼쪽에 속성 브라우저가 열립니다. **[!UICONTROL 로고]** 이미지를 찾아 업로드합니다. ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png)를 누릅니다. 이미지가 헤더에 나타납니다.

   파일 가져오기를 눌러 이 아티클에 사용된 로고를 다운로드할 수 있습니다.

   [파일 가져오기](assets/logo.png)

1. ![treeexpandall](assets/treeexpandall.png)의 **[!UICONTROL 바닥글]** 구성 요소를 응용 양식으로 드래그합니다. 이 단계에서 양식은 다음과 같습니다.

   ![adaptive-form-with-headers-and-footers](assets/adaptive-form-with-headers-and-footers.png)

## 3단계:구성 요소를 추가하여 캡처 및 표시 정보 {#step-add-components-to-capture-and-display-information}

구성 요소는 적응형 양식의 기본 요소를 만듭니다. AEM [!DNL Forms]은 적응형 형식으로 정보를 캡처하고 표시하는 많은 구성 요소를 제공합니다. 구성 요소를 ![treeexpandall](assets/treeexpandall.png)에서 양식으로 드래그할 수 있습니다. 사용 가능한 구성 요소 및 해당 기능에 대한 자세한 내용은 [적응형 양식 작성 소개](/help/forms/using/introduction-forms-authoring.md)를 참조하십시오.

1. **[!UICONTROL 숫자 상자 구성 요소]**&#x200B;를 응용 양식으로 드래그합니다. 바닥글 구성 요소 앞에 놓습니다. 구성 요소의 속성을 열고, 구성 요소의 **[!UICONTROL 제목]**&#x200B;을 **`Customer ID`**&#x200B;으로 변경하고, **[!UICONTROL 요소 이름]**&#x200B;을 **`customer_ID`**&#x200B;로 변경하고, **[!UICONTROL 필수 필드]** 옵션을 활성화하고 **[!UICONTROL HTML5 번호 입력 유형 사용]** 옵션을 활성화하고 &lt;a &lt;a> 10/>aem_6_3_forms_save](assets/aem_6_3_forms_save.png).![
1. 세 개의 텍스트 상자 구성 요소를 응용 양식으로 드래그합니다. 바닥글 구성 요소 앞에 놓습니다. 이러한 텍스트 상자에 대해 다음 속성을 설정합니다.:

   <table> 
    <tbody> 
     <tr> 
      <td><b>속성</b></td> 
      <td><b>텍스트 상자 1<br/></b></td> 
      <td><b>텍스트 상자 2<br/></b></td> 
      <td><b>텍스트 상자 3</b></td> 
     </tr> 
     <tr> 
      <td>제목</td> 
      <td>이름<br /> </td> 
      <td>배송 주소</td> 
      <td>상태</td> 
     </tr> 
     <tr> 
      <td>요소 이름</td> 
      <td>customer_Name<br /> </td> 
      <td>customer_Shipping_Address</td> 
      <td>customer_State</td> 
     </tr> 
     <tr> 
      <td>필수 필드</td> 
      <td>활성화됨</td> 
      <td>활성화됨</td> 
      <td>활성화됨</td> 
     </tr> 
     <tr> 
      <td>여러 줄 허용<br /> </td> 
      <td>비활성화</td> 
      <td>활성화됨</td> 
      <td>비활성화</td> 
     </tr> 
    </tbody> 
   </table>

1. 바닥글 구성 요소 앞에 **[!UICONTROL 숫자 상자]** 구성 요소를 드래그합니다. 구성 요소의 속성을 열고 아래 표에 나열된 값을 설정합니다. ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png)를 누릅니다.

   | 속성 | 값 |
   |---|---|
   | 제목 | 우편 번호 |
   | 요소 이름 | customer_ZIPCode |
   | 최대 자릿수 | 6 |
   | 필수 필드 | 활성화됨 |
   | 패턴 유형 표시 | 패턴 없음 |

1. 바닥글 구성 요소 앞에 **[!UICONTROL 이메일]** 구성 요소를 드래그합니다. 구성 요소의 속성을 열고 아래 표에 나열된 값을 설정한 다음 ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png)를 누릅니다.

   | 속성 | 값 |
   |---|---|
   | 제목 | 이메일 |
   | 요소 이름 | customer_Email |
   | 필수 필드 | 활성화됨 |

1. 바닥글 구성 요소 앞에 **[!UICONTROL 파일 첨부]** 구성 요소를 드래그합니다. 구성 요소의 속성을 열고 아래 표에 나열된 값을 설정한 다음 ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png)를 누릅니다.

   <table> 
    <tbody> 
     <tr> 
      <td><b>속성</b></td> 
      <td><b>값</b></td> 
     </tr> 
     <tr> 
      <td>제목</td> 
      <td>정부 승인 주소 증명<br /> </td> 
     </tr> 
     <tr> 
      <td>요소 이름</td> 
      <td>customer_Address_Proof</td> 
     </tr> 
     <tr> 
      <td>필수 필드</td> 
      <td>활성화됨</td> 
     </tr> 
    </tbody> 
   </table>

1. **[!UICONTROL 제출 단추]** 구성 요소를 응용 양식으로 드래그합니다. 바닥글 구성 요소 앞에 놓습니다. 구성 요소의 속성을 열고 요소 이름을 `address_addition_update_submit`으로 변경하고 ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png)를 누릅니다. 양식의 레이아웃이 완료되었으며 양식은 다음과 같습니다.

   ![adaptive-form-with-all-the-components](assets/adaptive-form-with-all-the-components.png)

## 4단계:응용 양식 {#step-configure-submit-action-for-the-adaptive-form}에 대한 제출 작업 구성

사용자가 적응형 양식의 제출 단추를 누를 때 제출 작업이 트리거됩니다. 전송 작업을 사용하여 양식 데이터를 로컬 저장소에 저장하고, 양식 데이터를 REST 종단점에 보내고, 양식 데이터를 이메일로 보내는 등의 작업을 수행할 수 있습니다. 적응형 양식에서는 즉시 사용 가능한 몇 가지 더 많은 전송 작업을 제공합니다. 자세한 내용은 [제출 작업 ](/help/forms/using/configuring-submit-actions.md) 구성을 참조하십시오.

다음 단계를 사용하여 양식의 이메일 제출 작업 및 데모 제출 작업을 구성할 수 있습니다.

1. 이메일 서버를 구성합니다. 자세한 내용은 [이메일 알림 구성](/help/sites-administering/notification.md)을 참조하십시오.


1. 콘텐트 브라우저에서 **[!UICONTROL 양식 컨테이너]**&#x200B;를 누르고 ![cmppr](assets/cmppr.png)을 누릅니다. 속성 브라우저가 왼쪽에 열립니다.
1. **[!UICONTROL 제출]** > **[!UICONTROL 제출 작업]**&#x200B;으로 이동합니다. **[!UICONTROL 이메일 보내기]**&#x200B;를 선택합니다. 다음 값을 지정하고 ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png)를 누릅니다.

   | 속성 | 값 |
   |--- |--- |
   | 시작 | `donotreply@weretail.com` |
   | 끝 | `${customer_Email}` |
   | 제목 | 확인:We.Retail 웹 사이트에 배송 주소를 추가했습니다. |
   | 이메일 템플릿 | `${customer_Name}`님, 다음 주소가 귀하의 계정의 배송 주소로 추가됩니다.<br>`${customer_Name}`, `${customer_Shipping_Address}`, `${customer_State}`, `${customer_ZIPCode}`<br> 안부, We.Retail |
   | 첨부 파일 포함 | 활성화됨 |

   양식 준비가 되었습니다. 이제 양식을 미리 보고 기능을 테스트할 수 있습니다. 자습서에 언급된 이름을 사용하고 AEM [!DNL Forms] 서버를 실행하는 시스템에서 양식에 액세스한 경우 이 양식은 [http://localhost:4502/editor.html/content/forms/af/shipping-address-add-update-form.html](http://localhost:4502/editor.html/content/forms/af/shipping-address-add-update-form.html)에서 사용할 수 있습니다.

## 5단계:응용 양식 {#step-preview-and-submit-the-adaptive-form} 미리 보기 및 제출

**[!UICONTROL 미리 보기 옵션]**&#x200B;을 사용하여 양식의 모양과 동작을 평가할 수 있습니다. 미리 보기 모드에서 양식을 제출하고 양식에 적용된 유효성 검사를 확인할 수도 있습니다. 예를 들어 필수 필드를 비워 둘 때 오류가 표시되는 경우

응용 양식에서는 다양한 장치에 대한 양식의 경험을 에뮬레이션하는 옵션도 제공합니다. 예: iPhone, iPad 및 Desktop. **[!UICONTROL 미리 보기]** 및 **[!UICONTROL 에뮬레이터]** ![눈금자](assets/ruler.png) 옵션을 모두 함께 사용하여 서로 다른 화면 크기의 장치에 대한 양식을 미리 볼 수 있습니다.

1. 양식 편집기 오른쪽의 **[!UICONTROL 미리 보기]** 옵션을 누릅니다. 양식이 미리 보기 모드로 열립니다. 자습서에 언급된 이름을 사용한 경우 양식의 미리 보기 URL은 [http://localhost:4502/content/dam/formsanddocuments/shipping-address-add-update-form/jcr:content?wcmmode=disabled](http://localhost:4502/content/dam/formsanddocuments/shipping-address-addition-updation-form/jcr:content?wcmmode=disabled)입니다.
1. 다양한 장치에서 양식이 어떻게 보이는지 보려면 ![눈금자](assets/ruler.png)를 사용하십시오.
1. 양식의 필드를 채우고 **[!UICONTROL 제출]**&#x200B;을 누릅니다. 양식이 제출되고 기본 **감사 인사** 페이지로 리디렉션됩니다. 사용자 지정 감사 페이지를 지정할 수도 있습니다. 자세한 내용은 [리디렉션 페이지 구성](/help/forms/using/configuring-redirect-page.md)을 참조하십시오.

주소를 추가하는 적응형 양식이 준비되었습니다. 자습서에 언급된 이름을 사용하고 AEM Forms 서버를 실행하는 시스템에서 양식에 액세스한 경우 이 양식은 [http://localhost:4502/editor.html/content/forms/af/shipping-address-add-update-form.html](http://localhost:4502/editor.html/content/forms/af/shipping-address-add-update-form.html)에서 사용할 수 있습니다.
