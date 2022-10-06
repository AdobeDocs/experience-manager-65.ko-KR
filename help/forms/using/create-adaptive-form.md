---
title: '자습서: 적응형 양식 만들기'
seo-title: Create an adaptive form
description: 적응형 양식을 만들고, 레이아웃하고, 미리 보는 방법을 알아봅니다. 또한 제출 작업을 구성하는 방법도 알아봅니다.
seo-description: Learn to create, layout, and preview an adaptive form. Also, learn to configure submit actions.
page-status-flag: de-activated
uuid: 0010d274-a683-499e-9fa6-ce355d7898a0
discoiquuid: 55c08940-8c25-4938-8e49-25bce20aaf22
feature: Adaptive Forms
exl-id: c0a2adcd-528a-41af-99b5-d8b423cd6605
source-git-commit: ed11891c27910154df1bfec6225aecd8a9245bff
workflow-type: tm+mt
source-wordcount: '1376'
ht-degree: 3%

---

# 자습서: 적응형 양식 만들기 {#do-not-publish-tutorial-create-an-adaptive-form}

![02-create-adaptive-form-main-image](assets/02-create-adaptive-form-main-image.png)

이 자습서는 [첫 번째 적응형 양식 만들기](/help/forms/using/create-your-first-adaptive-form.md) 시리즈. 전체 자습서 사용 사례를 이해하고, 수행하고, 시연하기 위해 시리즈를 시간 순서대로 따르는 것이 좋습니다.

## 자습서 정보 {#about-the-tutorial}

적응형 양식은 동적이고 반응형 양식입니다. 적응형 양식을 사용하여 개인화된 경험을 제공할 수 있습니다. 적응형 양식을 [!DNL Adobe Analytics] 사용 통계 및 [!DNL Adobe Campaign] campaign 관리를 위해 적응형 양식 기능에 대한 자세한 내용은 [적응형 양식 작성 소개](/help/forms/using/introduction-forms-authoring.md).

적절한 프로세스를 수행하면 양식을 더 쉽게 만들고 관리할 수 있습니다. 이 문서에서는 다음 방법을 알아봅니다.

* [고객이 배송 주소를 추가할 수 있도록 하는 적응형 양식을 만듭니다](/help/forms/using/create-adaptive-form.md#step-create-the-adaptive-form)

* [고객의 정보를 표시하고 수락하는 적응형 양식의 레이아웃 필드](/help/forms/using/create-adaptive-form.md#step-add-header-and-footer)

* [양식 컨텐츠가 포함된 이메일을 전송하기 위한 제출 작업 만들기](/help/forms/using/create-adaptive-form.md#step-add-components-to-capture-and-display-information)
* [적응형 양식 미리 보기 및 제출](/help/forms/using/create-adaptive-form.md)

문서의 끝 부분에 다음과 유사한 양식이 있습니다.\
[![](do-not-localize/form-preview-mobile.gif)](do-not-localize/form-preview-mobile.gif)

## 1단계: 적응형 양식 만들기 {#step-create-the-adaptive-form}

1. AEM 작성자 인스턴스에 로그인하고 다음 위치로 이동합니다. **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms 및 문서]**. 기본 URL은 [http://localhost:4502/aem/forms.html/content/dam/formsanddocuments](http://localhost:4502/aem/forms.html/content/dam/formsanddocuments).
1. 탭 **[!UICONTROL 만들기]** 을(를) 선택합니다. **[!UICONTROL 적응형 양식]**. 템플릿을 선택하는 옵션이 나타납니다. 탭하기 **[!UICONTROL 비어 있음]** 템플릿을 선택하고 탭합니다. **[!UICONTROL 다음]**.

1. 다음 옵션 **[!UICONTROL 속성 추가]** 이 나타납니다. 다음 **[!UICONTROL 제목]** 및 **[!UICONTROL 이름]** 필드는 필수입니다.

   * **제목:** 지정 `Add new or update shipping address` 에서 **[!UICONTROL 제목]** 필드. 제목 필드는 양식의 표시 이름을 지정합니다. 제목은 AEM에서 양식을 식별하는 데 도움이 됩니다 [!DNL Forms] 사용자 인터페이스.
   * **이름:** 지정 `shipping-address-add-update-form` 에서 **[!UICONTROL 이름]** 필드. 이름 필드는 양식 이름을 지정합니다. 지정된 이름의 노드가 저장소에 생성됩니다. 제목을 입력을 시작하면 이름 필드의 값이 자동으로 생성됩니다. 제안된 값을 변경할 수 있습니다. 이름 필드에는 영숫자, 하이픈 및 밑줄만 포함할 수 있습니다. 잘못된 입력은 모두 하이픈으로 대체됩니다.

1. 탭 **[!UICONTROL 만들기]**. 적응형 양식이 만들어지고 편집할 양식을 여는 대화 상자가 나타납니다. 탭 **[!UICONTROL 열기]** 새 탭에서 새로 만든 양식을 열려면 다음을 수행하십시오. 편집할 양식이 열립니다. 또한 필요에 따라 새로 만든 양식을 사용자 지정하는 사이드바가 표시됩니다.

   적응형 양식 작성 인터페이스 및 사용 가능한 구성 요소에 대한 자세한 내용은 [적응형 양식 작성 소개](/help/forms/using/creating-adaptive-form.md).

   ![새로 만든 적응형 양식](assets/newly-created-adaptive-form.png)

## 2단계: 머리글 및 바닥글 추가 {#step-add-header-and-footer}

AEM [!DNL Forms] 적응형 양식에 대한 정보를 표시하는 많은 구성 요소를 제공합니다. 머리글 및 바닥글 구성 요소를 사용하면 양식의 모양과 느낌을 일관되게 제공할 수 있습니다. 헤더는 일반적으로 법인의 로고, 양식의 제목 및 요약을 포함합니다. 바닥글은 일반적으로 저작권 정보와 다른 페이지에 대한 링크를 포함합니다.

1. 탭 ![토글 사이드 패널](assets/toggle-side-panel.png) > ![treeexpandall](assets/treeexpandall.png). 구성 요소 브라우저가 열립니다. 을(를) 드래그합니다. **[!UICONTROL Header]** 구성 요소를 구성 요소 브라우저에서 적응형 양식으로 전환
1. 탭 **[!UICONTROL 로고]**. 도구 모음이 나타납니다. 탭 ![aem_6_3_edit](assets/aem_6_3_edit.png) 도구 모음에서 **We.Retail**, 탭 ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png).

1. 이미지 를 누릅니다. 도구 모음이 나타납니다. 탭 ![cmppr](assets/cmppr.png). 속성 브라우저가 화면 왼쪽에 열립니다. **[!UICONTROL 찾아보기]** 로고 이미지를 업로드합니다. 탭 ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png). 헤더에 이미지가 나타납니다.

   파일 가져오기 를 탭하여 이 문서에 사용된 로고를 다운로드할 수 있습니다.

[파일 가져오기](assets/logo.png)

1. 을(를) 드래그합니다. **[!UICONTROL 바닥글]** 구성 요소 ![treeexpandall](assets/treeexpandall.png) 적응형 양식으로 전환 이 단계에서는 양식이 다음과 같습니다.

   ![적응형 양식-with-headers-and-footers](assets/adaptive-form-with-headers-and-footers.png)

## 3단계: 정보를 캡처하고 표시할 구성 요소 추가 {#step-add-components-to-capture-and-display-information}

구성 요소는 적응형 양식의 빌딩 블록입니다. AEM [!DNL Forms] 에서는 적응형 양식으로 정보를 캡처하고 표시할 여러 구성 요소를 제공합니다. 구성 요소를 ![treeexpandall](assets/treeexpandall.png) 추가 정보. 사용 가능한 구성 요소 및 해당 기능에 대해 알아보려면 [적응형 양식 작성 소개](/help/forms/using/introduction-forms-authoring.md).

1. 을(를) 드래그합니다. **[!UICONTROL 숫자 상자 구성 요소]** 적응형 양식으로 전환 바닥글 구성 요소 앞에 배치합니다. 구성 요소의 속성을 열고 변경합니다. **[!UICONTROL 제목]** 구성 요소의 **`Customer ID`**, 변경 **[!UICONTROL 요소 이름]** to **`customer_ID`**&#x200B;를 활성화하십시오. **[!UICONTROL 필수 필드]** 선택 사항을 활성화하십시오. **[!UICONTROL HTML5 숫자 입력 유형 사용]** 옵션 및 탭 ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png).
1. 3개의 텍스트 상자 구성 요소를 적응형 양식으로 드래그합니다. 바닥글 구성 요소 앞에 배치합니다. 이러한 텍스트 상자에 대해 다음 속성을 설정합니다.:

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

1. 드래그 **[!UICONTROL 숫자 상자]** 구성 요소를 바닥글 구성 요소 앞에 추가합니다. 구성 요소의 속성을 열고 아래 표에 나열된 값을 설정합니다. 탭합니다. ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png).

   | 속성 | 값 |
   |---|---|
   | 제목 | 우편 번호 |
   | 요소 이름 | customer_ZIPode |
   | 최대 자릿수 | 6 |
   | 필수 필드 | 활성화됨 |
   | 표시 패턴 유형 | 패턴 없음 |

1. 끌어서 놓기 **[!UICONTROL 이메일]** 구성 요소를 바닥글 구성 요소 앞에 추가합니다. 구성 요소의 속성을 열고 아래 표에 나열된 값을 설정한 다음 탭합니다 ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png).

   | 속성 | 값 |
   |---|---|
   | 제목 | 이메일 |
   | 요소 이름 | customer_Email |
   | 필수 필드 | 활성화됨 |

1. 끌어서 놓기 **[!UICONTROL 파일 첨부]** 구성 요소를 바닥글 구성 요소 앞에 추가합니다. 구성 요소의 속성을 열고 아래 표에 나열된 값을 설정한 다음 탭합니다 ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png).

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

1. 드래그 **[!UICONTROL 전송 단추]** 구성 요소를 적응형 양식에 추가합니다. 바닥글 구성 요소 앞에 배치합니다. 구성 요소의 속성을 열고 요소 이름을 로 변경합니다. `address_addition_update_submit`, 탭 ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png). 양식의 레이아웃이 완료되고 양식은 다음과 같습니다.

   ![응용 양식-with-all-the-components](assets/adaptive-form-with-all-the-components.png)

## 4단계: 적응형 양식에 대한 제출 작업 구성 {#step-configure-submit-action-for-the-adaptive-form}

사용자가 적응형 양식에서 제출 단추를 누르면 제출 작업이 트리거됩니다. 제출 작업을 사용하여 양식 데이터를 로컬 리포지토리에 저장하고, 양식 데이터를 REST 엔드포인트로 보내고, 양식 데이터를 이메일로 보내는 등의 작업을 수행할 수 있습니다. 적응형 양식은 몇 가지 추가 기본 제출 작업을 제공합니다. 자세한 내용은 [제출 작업 구성](/help/forms/using/configuring-submit-actions.md).

다음 단계를 사용하여 전자 메일 제출 작업 및 양식의 데모 제출 작업을 구성할 수 있습니다.

1. 이메일 서버를 구성합니다. 자세한 내용은 [전자 메일 알림 구성](/help/sites-administering/notification.md).


1. 탭 **[!UICONTROL 양식 컨테이너]** 컨텐츠 브라우저에서 ![cmppr](assets/cmppr.png). 속성 브라우저가 왼쪽에서 열립니다.
1. 이동 **[!UICONTROL 제출]** >  **[!UICONTROL 작업 제출]**. 선택 **[!UICONTROL 이메일 보내기]**. 다음 값을 지정하고 탭합니다 ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png).

   | 속성 | 값 |
   |--- |--- |
   | 시작 | `donotreply@weretail.com` |
   | 끝 | `${customer_Email}` |
   | 제목 | 확인: We.Retail 웹 사이트에 배송 주소를 추가했습니다. |
   | 이메일 템플릿 | 안녕 `${customer_Name}`, 계정의 배송 주소로 다음 주소가 추가됩니다. <br>`${customer_Name}`, `${customer_Shipping_Address}`, `${customer_State}`, `${customer_ZIPCode}`<br> 감사합니다, We.Retail |
   | 첨부 파일 포함 | 활성화됨 |

   양식을 준비했습니다. 이제 양식을 미리 보고 기능을 테스트할 수 있습니다. 자습서에 언급된 이름을 사용하고 AEM을 실행하는 시스템에서 양식에 액세스한 경우 [!DNL Forms] server에서 양식을 사용할 수 있습니다. [http://localhost:4502/editor.html/content/forms/af/shipping-address-add-update-form.html](http://localhost:4502/editor.html/content/forms/af/shipping-address-add-update-form.html).

## 5단계: 적응형 양식 미리 보기 및 제출 {#step-preview-and-submit-the-adaptive-form}

를 사용할 수 있습니다 **[!UICONTROL 미리 보기 옵션]** 폼의 모양과 동작을 평가하기 위해 미리 보기 모드에서 양식을 제출하고 양식에 적용된 유효성 검사를 확인할 수도 있습니다. 예를 들어 필수 필드를 비워 두면 오류가 표시됩니다.

적응형 양식은 다양한 장치의 양식 경험을 에뮬레이션하는 옵션도 제공합니다. 예를 들어 iPhone, iPad 및 Desktop이 있습니다. 두 가지 모두를 사용할 수 있습니다 **[!UICONTROL 미리 보기]** 및 **[!UICONTROL 에뮬레이터]** ![눈금자](assets/ruler.png) 다른 화면 크기의 장치를 위한 양식을 미리 보기 위한 옵션 .

1. 탭하기 **[!UICONTROL 미리 보기]** 옵션 을 클릭합니다. 양식이 미리 보기 모드에서 열립니다. 자습서에 언급된 이름을 사용한 경우 양식의 미리 보기 URL은 [http://localhost:4502/content/dam/formsanddocuments/shipping-address-add-update-form/jcr:content?wcmmode=disabled](http://localhost:4502/content/dam/formsanddocuments/shipping-address-addition-updation-form/jcr:content?wcmmode=disabled)
1. 사용 ![눈금자](assets/ruler.png) 다양한 장치에서 양식이 어떻게 보이는지 보기 위해.
1. 양식의 필드를 작성하고 탭합니다. **[!UICONTROL 제출]**. 양식이 제출되면 기본값으로 리디렉션됩니다 **감사합니다** 페이지. 사용자 지정 감사 인사 페이지를 지정할 수도 있습니다. 자세한 내용은 [리디렉션 페이지 구성](/help/forms/using/configuring-redirect-page.md).

주소를 추가할 적응형 양식이 준비되었습니다. 자습서에서 언급된 이름을 사용하고 AEM Forms 서버를 실행하는 시스템에서 양식에 액세스한 경우 다음 위치에서 양식을 사용할 수 있습니다. [http://localhost:4502/editor.html/content/forms/af/shipping-address-add-update-form.html](http://localhost:4502/editor.html/content/forms/af/shipping-address-add-update-form.html).
