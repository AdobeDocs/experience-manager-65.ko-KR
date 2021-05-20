---
title: 적응형 양식에서 Adobe Sign 사용
seo-title: 적응형 양식에서 Adobe Sign 사용
description: 적응형 양식의 전자 서명(Adobe Sign) 워크플로우를 통해 서명 워크플로우를 자동화하고 단일 및 다중 서명 프로세스를 간소화하고 모바일 장치에서 양식에 전자 서명할 수 있습니다.
seo-description: 적응형 양식의 전자 서명(Adobe Sign) 워크플로우를 통해 서명 워크플로우를 자동화하고 단일 및 다중 서명 프로세스를 간소화하고 모바일 장치에서 양식에 전자 서명할 수 있습니다.
uuid: cc3012ed-c318-4529-9adc-61aa5b5761a0
contentOwner: khsingh
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: f79828d8-2230-4477-8ffa-eeb6a0413acd
docset: aem65
feature: 응용 Forms, Adobe Sign
exl-id: a8decba9-229d-40a2-992a-3cc8ebefdd6d
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '3863'
ht-degree: 0%

---

# 적응형 양식{#using-adobe-sign-in-an-adaptive-form}에서 [!DNL Adobe Sign] 사용

[!DNL Adobe Sign] 적응형 양식을 위해 전자 서명 워크플로우를 활성화합니다. 전자 서명은 법률, 영업, 급여, 인적 자원 관리 등 다양한 분야에 대한 문서를 처리하기 위한 워크플로우를 개선합니다.

일반적인 [!DNL Adobe Sign] 및 적응형 양식 시나리오에서 사용자는 적응형 양식을 채워 서비스에 적용합니다. 예를 들어, 대출 및 신용 카드 신청은 모든 대출자와 공동 지원자의 법적 서명을 필요로 합니다. 유사한 시나리오에 대해 전자 서명 워크플로우를 활성화하려면 [!DNL Adobe Sign]을 AEM [!DNL Forms]과 통합할 수 있습니다. 예를 몇 가지 더 들면 [!DNL Adobe Sign]을 사용하여 다음을 수행할 수 있습니다.

* 완전히 자동화된 제안, 견적 및 계약 프로세스를 사용하여 모든 장치의 거래를 마감합니다.
* 인적 자원 프로세스를 보다 신속하게 완료하고 직원들에게 디지털 경험을 제공합니다.
* 계약 주기를 단축하고 공급업체 가입을 보다 신속하게 처리합니다.
* 공통 프로세스를 자동화하는 디지털 워크플로우를 구축할 수 있습니다.

[!DNL Adobe Sign] AEM과의 통합은 다음을  [!DNL Forms] 지원합니다.

* 단일 및 다중 사용자 서명 워크플로우
* 순차적 및 동시 서명 워크플로우
* 양식 및 양식 외 서명 경험
* 양식을 익명 또는 로그인 사용자로 서명
* 동적 서명 프로세스(AEM [!DNL Forms] 워크플로우와 통합)
* 기술 자료, 전화 및 소셜 프로필을 통한 인증

적응형 양식](https://medium.com/adobetech/using-adobe-sign-to-e-sign-an-adaptive-form-heres-the-best-way-to-do-it-dc3e15f9b684)에 Adobe Sign을 사용하는 모범 사례에 대해 배웁니다.[

## 전제 조건 {#prerequisites}

적응형 양식에서 [!DNL Adobe Sign] 사용 전:

* AEM [!DNL Forms] 클라우드 서비스가 [!DNL Adobe Sign]을 사용하도록 구성되어 있는지 확인합니다. 자세한 내용은 [Adobe Sign과 AEM Forms 통합](../../forms/using/adobe-sign-integration-adaptive-forms.md)을 참조하십시오.
* 서명자 목록을 준비하세요. 모든 서명자에 대해 이메일 주소가 최소 필요합니다.

## 적응형 양식 {#configure-adobe-sign-for-an-adaptive-form}에 대해 [!DNL Adobe Sign] 구성

적응형 양식에 대해 [!DNL Adobe Sign]을 구성하려면 다음 단계를 수행하십시오.

1. [Adobe 기호에 대한 적응형 양식 속성 편집](../../forms/using/working-with-adobe-sign.md#enableadobesign)
1. [적응형 양식에 Adobe Sign 필드 추가](../../forms/using/working-with-adobe-sign.md#addadobesignfieldstoanadaptiveform)
1. [적응형 양식에 Adobe Sign 활성화](../../forms/using/working-with-adobe-sign.md#enableadobsignforanadaptiveform)
1. [적응형 양식에 대한 Adobe Sign Cloud Service 선택](../../forms/using/working-with-adobe-sign.md#selectadobesigncloudserviceforanadaptiveform)

1. [적응형 양식에 Adobe Sign 서명자 추가](../../forms/using/working-with-adobe-sign.md#addsignerstoanadaptiveform)
1. [적응형 양식에 대한 제출 작업 선택](../../forms/using/working-with-adobe-sign.md#selectsubmitactionforanadaptiveform)

![서명자 세부 정보](assets/signer_details_new.png)

### [!DNL Adobe Sign]에 대한 적응형 양식 속성 편집 {#enableadobesign}

기존 또는 새 적응형 양식에 대해 [!DNL Adobe Sign]에 대한 적응형 양식 속성을 구성합니다.

[Adobe 서명을 위한 적응형 양식 만들기 ](../../forms/using/working-with-adobe-sign.md#create-an-adaptive-form-for-adobe-sign) 는 기본 적응형 양식을 만드는 단계를 설명합니다. 적응형 양식을 만드는 동안 사용할 수 있는 다른 옵션에 대해서는 [적응형 양식 만들기](../../forms/using/creating-adaptive-form.md)를 참조하십시오.

#### [!DNL Adobe Sign] {#create-an-adaptive-form-for-adobe-sign}에 대한 적응형 양식 만들기

서명 사용 적응형 양식을 만들려면 다음 단계를 수행하십시오.

1. **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms 및 문서]**&#x200B;로 이동합니다.
1. **[!UICONTROL 만들기]**&#x200B;를 누르고 **[!UICONTROL 적응형 양식]**&#x200B;을 선택합니다. 템플릿 목록이 나타납니다. 템플릿을 선택하고 **[!UICONTROL 다음]**&#x200B;을 누릅니다.
1. **[!UICONTROL 기본]** 탭에서 다음을 수행합니다.

   1. 적응형 양식의 **[!UICONTROL 이름]** 및 **[!UICONTROL 제목]**&#x200B;을 지정합니다.

   1. [!DNL Adobe Sign]을(를) AEM [!DNL Forms]으로 구성하는 동안 만들어진 [구성 컨테이너](../../forms/using/adobe-sign-integration-adaptive-forms.md#configure-adobe-sign-with-aem-forms)를 선택합니다.

      >[!NOTE]
      >
      >**[!UICONTROL Adobe Sign Cloud Service]** 드롭다운 목록에는 이 필드에서 선택하는 구성 컨테이너에 구성된 클라우드 서비스가 표시됩니다. **[!UICONTROL Adobe Sign Cloud Service]** 드롭다운 목록은 **[!UICONTROL Adobe Sign 활성화]** 옵션을 선택하면 적응형 양식 속성의 **[!UICONTROL 전자 서명]** 섹션에서 사용할 수 있습니다.

1. **[!UICONTROL 양식 모델]** 탭에서 다음 옵션 중 하나를 선택합니다.

   * **[!UICONTROL 양식 서식 파일을 레코드 문서 서식 파일로 연결]** 옵션을 선택하고 레코드 문서 서식 파일을 선택합니다. 적응형 양식 기반의 양식 템플릿을 사용하는 경우 서명을 위해 전송된 문서는 관련 양식 템플릿을 기반으로 하는 필드만 표시됩니다. 적용형 양식의 모든 필드가 표시되지 않습니다.

   * **[!UICONTROL 레코드 문서 생성]** 옵션을 선택합니다. [레코드 문서] 옵션을 활성화된 적응형 양식을 사용하는 경우 서명을 위해 전송된 문서에 적응형 양식의 모든 필드가 표시됩니다.

1. **[!UICONTROL 만들기 를 누릅니다.]** 서명 사용 적응형 양식이 만들어져서 필드를 추가하는 데 사용할 수  [!DNL Adobe Sign] 있습니다.

#### [!DNL Adobe Sign]에 대한 적응형 양식 편집 {#editafsign}

기존 적응형 양식에서 [!DNL Adobe Sign] 을 사용하려면 다음 단계를 수행하십시오.

1. **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms 및 문서]**&#x200B;로 이동합니다.
1. 적응형 양식을 선택하고 **[!UICONTROL 속성]**&#x200B;을 누릅니다.
1. **[!UICONTROL 기본]** 탭에서 AEM [!DNL Forms]로 [!DNL Adobe Sign]를 구성하는 동안 만든 [구성 컨테이너](../../forms/using/adobe-sign-integration-adaptive-forms.md#configure-adobe-sign-with-aem-forms)를 선택합니다.
1. **[!UICONTROL 양식 모델]** 탭에서 다음 옵션 중 하나를 선택합니다.

   * **[!UICONTROL 양식 서식 파일을 레코드 문서 서식 파일로 연결]** 옵션을 선택하고 레코드 문서 서식 파일을 선택합니다. 적응형 양식 기반의 양식 템플릿을 사용하는 경우 서명을 위해 전송된 문서는 관련 양식 템플릿을 기반으로 하는 필드만 표시됩니다. 적용형 양식의 모든 필드가 표시되지 않습니다.

   * **[!UICONTROL 레코드 문서 생성]** 옵션을 선택합니다. [레코드 문서] 옵션을 활성화된 적응형 양식을 사용하는 경우 서명을 위해 전송된 문서에 적응형 양식의 모든 필드가 표시됩니다.

1. **[!UICONTROL 저장 및 닫기]**&#x200B;를 누릅니다. 적응형 양식은 [!DNL Adobe Sign]에 대해 활성화되어 있습니다.

### 적응형 양식에 Adobe Sign 필드 추가 {#addadobesignfieldstoanadaptiveform}

[!DNL Adobe Sign] 에는 적응형 양식에 배치할 수 있는 다양한 필드가 있습니다. 이러한 필드는 서명, 이니셜, 회사 또는 제목과 같은 다양한 유형의 데이터를 허용하며 서명과 함께 서명 중에 추가 정보를 수집하는 데 도움이 됩니다. [!DNL Adobe Sign] 블록 구성 요소를 사용하여 적응형 양식의 다양한 위치에 [!DNL Adobe Sign] 필드를 배치할 수 있습니다.

적응형 양식에 필드를 추가하고 이러한 필드와 관련된 다양한 옵션을 사용자 지정하려면 다음 단계를 수행하십시오.

1. 구성 요소 브라우저에서 적응형 양식으로 **[!UICONTROL Adobe Sign Block]** 구성 요소를 드래그하여 놓습니다. [!DNL Adobe Sign] 블록 구성 요소에는 지원되는 모든 [!DNL Adobe Sign] 필드가 있습니다. 기본적으로 적응형 양식에 **서명** 필드가 추가됩니다.

   ![기호 블록](assets/sign_block_new.png)

   기본적으로 게시된 적응형 양식에는 [!DNL Adobe Sign] 블록이 표시되지 않습니다. 서명 문서에서만 볼 수 있습니다. [!DNL Adobe Sign] 블록 구성 요소의 속성에서 [!DNL Adobe Sign] 블록 가시성을 변경할 수 있습니다.

   >[!NOTE]
   >
   >    * 적응형 양식에서 [!DNL Adobe Sign] 블록을 사용해야 하는 것은 아닙니다. [!DNL Adobe Sign] [!DNL Adobe Sign] 블록을 사용하고 서명자를 위한 필드를 추가하지 않으면 서명 문서 하단에 기본 서명 필드가 표시됩니다.
   >    * 자동으로 레코드 문서를 생성하는 적응형 양식에 대해서만 [!DNL Adobe Sign] 블록을 사용합니다. 레코드 문서 또는 적응형 양식 기반의 양식 템플릿을 생성하는 사용자 지정 XDP를 사용하는 경우 [!DNL Adobe Sign] 블록이 지원되지 않습니다.


1. **[!UICONTROL Adobe Sign 블록]** 구성 요소를 선택하고 **편집** ![aem_6_3_edit](assets/aem_6_3_edit.png) 아이콘을 탭합니다. 필드의 필드와 형식 모양을 추가하는 옵션이 표시됩니다.

   ![adobe sign-block-select-fields](assets/adobe-sign-block-select-fields.png)

   **A.** 필드를 선택하고  [!DNL Adobe Sign] 추가합니다. **B.** 블록을  [!DNL Adobe Sign] 전체 화면 보기로 확장합니다.

1. **[!UICONTROL Adobe Sign] 필드** ![aem_6_3_adobesign](assets/aem_6_3_adobesign.png) 아이콘을 탭합니다. [!DNL Adobe Sign] 필드를 선택하고 추가하는 옵션이 표시됩니다.

   **[!UICONTROL 유형]** 드롭다운 필드를 확장하여 [!DNL Adobe Sign] 필드를 선택하고 완료 ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png) 아이콘을 탭하여 선택한 필드를 [!DNL Adobe Sign] 블록에 추가합니다. **[!UICONTROL 유형]** 드롭다운 필드에는 서명, 서명자 정보 및 데이터 필드 유형이 포함됩니다. [!DNL Adobe Sign] 유형 드롭다운  [!DNL Forms] 상자에 나열된 AEM   지원 필드와의 통합. [!DNL Adobe Sign] 필드에 대한 자세한 내용은 [Adobe Sign 설명서](https://helpx.adobe.com/sign/help/field-types.html)를 참조하십시오.

   ![adobe-sign-block-fields-options](assets/adobe-sign-block-fields-options.png)

   필드에 고유한 이름을 입력해야 합니다. 필수 필드를 선택하여 표시할 수도 있습니다. **[!UICONTROL 이름]** 및 **[!UICONTROL 필수]** 옵션 외에도 일부 [!DNL Adobe Sign] 필드에 더 많은 옵션이 있습니다. 예를 들어, 마스크 및 여러 줄. 또한 각 [!DNL Adobe Sign] 필드에 대해 필드가 동일하거나 다른 [!DNL Adobe Sign] 블록에 있는지 여부를 고유한 이름을 지정합니다.

   드롭다운 목록에서 **[!UICONTROL 디지털 서명]**&#x200B;을 선택하는 경우 적응형 양식에 디지털 서명을 적용할 수 있습니다.

   * 클라우드 서명을 사용하여 전자 메일 서비스 공급자가 호스팅하는 [디지털 ID](https://helpx.adobe.com/sign/kb/digital-certificate-providers.html)로 서명합니다.
   * 스마트 카드, USB 토큰 또는 파일 기반 디지털 ID를 사용하여 Adobe Acrobat 또는 Reader으로 문서를 로컬로 다운로드하십시오.

### 적응형 양식에 [!DNL Adobe Sign] 사용 {#enableadobsignforanadaptiveform}

기본적으로 적응형 양식에 대해 [!DNL Adobe Sign]이 활성화되지 않습니다. 다음 단계를 수행하여 활성화하십시오.

1. 컨텐츠 브라우저에서 **[!UICONTROL 양식 컨테이너]**&#x200B;를 탭하고 **[!UICONTROL 구성]** ![구성](assets/configure.png) 아이콘을 탭합니다. 속성 브라우저를 열고 적응형 양식 컨테이너 속성을 표시합니다.
1. 속성 브라우저에서 **[!UICONTROL 전자 서명]** 아코디언을 확장하고 **[!UICONTROL Adobe Sign 활성화]** 옵션을 선택합니다. 적응형 양식에 대해 [!DNL Adobe Sign]을 활성화합니다.

### [!DNL Adobe Sign] Cloud Service 및 서명 순서를 선택합니다 {#selectadobesigncloudserviceforanadaptiveform}

AEM [!DNL Forms] 인스턴스에 대해 여러 [!DNL Adobe Sign] 서비스를 구성할 수 있습니다. 각 기능(인사, 재무 등)에 대해 별도의 서비스 세트를 갖는 것이 좋습니다. 서명된 문서를 보다 쉽게 추적 및 보고할 수 있습니다. 예를 들어, 은행에는 여러 부서가 있습니다. 문서 추적을 더 잘 하기 위해 각 부서에 대해 별도의 구성을 지정할 수 있습니다.

한 문서에 여러 서명자가 있을 수도 있습니다. 예를 들어 신용 카드 지원에는 여러 명의 지원자가 있을 수 있습니다. 은행은 지원서를 처리하기 전에 모든 지원자의 서명을 받아야 한다. 여러 서명자 시나리오의 경우 문서를 순차적 또는 동시 순서로 서명하도록 선택할 수 있습니다.

클라우드 서비스와 서명 순서를 선택하려면 다음 단계를 수행하십시오.

![클라우드 서비스](assets/cloud-service.png)

1. 컨텐츠 브라우저에서 **[!UICONTROL 양식 컨테이너]**&#x200B;를 탭하고 **[!UICONTROL 구성]** ![구성](assets/configure.png) 아이콘을 탭합니다. 속성 브라우저를 열고 적응형 양식 컨테이너 속성을 표시합니다.
1. 속성 브라우저에서 **[!UICONTROL 전자 서명]** 아코디언을 확장하고 **[!UICONTROL Adobe Sign 활성화]** 옵션을 선택합니다. 적응형 양식에 대해 [!DNL Adobe Sign]을 활성화합니다.
1. 이미 구성된 [!DNL Adobe Sign] Cloud Services 목록에서 클라우드 서비스를 선택합니다.

   **[!UICONTROL Adobe Sign Cloud Service]** 목록이 비어 있는 경우 [AEM Forms으로 Adobe Sign 구성](../../forms/using/adobe-sign-integration-adaptive-forms.md) 문서에 따라 서비스를 구성하십시오.

   드롭다운에 도구 > **[!UICONTROL Cloud Services]** > **[!UICONTROL Adobe Sign]**&#x200B;의 `global` 폴더에 있는 클라우드 서비스가 나열됩니다. 또한 적응형 양식을 만들 때 **[!UICONTROL 구성 컨테이너]** 필드에서 선택하는 폴더에 존재하는 클라우드 서비스가 드롭다운에 나열됩니다.

1. **[!UICONTROL 서명자 수]** 대화 상자에서 서명 순서를 선택합니다. [!DNL Adobe Sign] 가수들은 적응형 양식 **[!UICONTROL 에 순차적으로]**  서명하거나,  **[!UICONTROL 동시에]**  원하는 순서로 서명할 수 있습니다.

   순차적으로, 한 서명자가 한 번에 서명 양식을 수신합니다. 서명자가 문서 서명을 완료하면 다음 서명자에게 양식이 전송됩니다.

   동시에 여러 서명자가 한 번에 양식에 서명할 수 있습니다.

1. [적응형 양식에 서명자](../../forms/using/working-with-adobe-sign.md#addsignerstoanadaptiveform) 를 추가하고 Done  ![aem_6_3_forms_](assets/aem_6_3_forms_save.png) saveicon을 탭하여 변경 사항을 저장합니다.


### 적응형 양식에 서명자 추가 {#addsignerstoanadaptiveform}

적응형 양식에 대해 서명자 또는 서명자가 여러 명만 가질 수 있습니다. 서명자를 추가할 때 서명자에 대한 인증 세부 사항을 구성할 수도 있습니다. 또한 양식 충전기와 가수가 같은 사람인지 선택할 수 있습니다. 서명자에 대한 다양한 세부 정보를 추가하고 제공하려면 다음 단계를 수행하십시오.

1. 컨텐츠 브라우저에서 **[!UICONTROL 양식 컨테이너]**&#x200B;를 탭하고 **[!UICONTROL 구성]** ![구성](assets/configure.png) 아이콘을 탭합니다. 응용 양식 컨테이너 속성이 있는 속성 브라우저를 엽니다.
1. 속성 브라우저에서 **[!UICONTROL 전자 서명]** 아코디언을 확장하고 **[!UICONTROL Adobe Sign 활성화]** 옵션을 선택합니다. 적응형 양식에 대해 [!DNL Adobe Sign]을 활성화합니다.
1. **[!UICONTROL 서명자 구성]**&#x200B;에서 **[!UICONTROL 서명자 추가]**&#x200B;를 누릅니다. 적응형 양식에 서명자가 추가됩니다. 적응형 양식에 [!DNL Adobe Sign] 서명자를 여러 개 추가할 수 있습니다.
   ![전화 세부 사항](assets/phone-details.png)

1. **편집** ![aem_6_3_edit](assets/aem_6_3_edit.png) 아이콘을 클릭하여 서명자에 대한 다음 정보를 지정합니다.

   * **[!UICONTROL 제목]:** 서명자를 고유하게 식별할 제목을 지정합니다.

   * **[!UICONTROL 서명자와 양식 작성자가 동일합니까?]:** 양식  **작성자와 첫 번째 서명자가 동일한 사람인 경우 [예]**&#x200B;를 선택합니다. 옵션이 **아니요,**&#x200B;로 설정되어 있으면 적응형 양식에서 서명 단계 구성 요소를 사용하지 마십시오. 양식에 서명 단계 구성 요소가 포함되어 있으면 필드가 자동으로 예로 설정됩니다.

   * **[!UICONTROL 서명자 이메일 주소]:** 서명자의 이메일 주소를 지정합니다. 서명자가 지정된 전자 메일 주소에서 서명된 문서/양식을 수신합니다. 양식 필드에 제공된 이메일 주소를 사용하거나, 로그인한 사용자의 AEM 사용자 프로필에서 이메일 주소를 사용하도록 선택하거나, 수동으로 이메일 주소를 입력할 수 있습니다. 이것은 필수 단계입니다. 첫 번째 서명자 또는 유일한 서명자의 이메일 주소가 AEM 클라우드 서비스를 구성하는 데 사용되는 [!DNL Adobe Sign] 계정과 동일하지 않은지 확인합니다.

   * **[!UICONTROL 서명자 인증 방법]:** 서명을 위한 양식을 열기 전에 사용자를 인증하는 방법을 지정합니다. 전화, 기술 자료 및 소셜 ID 기반 인증 중에서 선택할 수 있습니다.
   >[!NOTE]
   >
   >    * 기본적으로 소셜 ID 기반 인증은 Facebook, Google 및 LinkedIn을 사용하여 인증하는 옵션을 제공합니다. [!DNL Adobe Sign] 지원에 문의하여 다른 소셜 인증 공급자를 활성화할 수 있습니다.


   * **[!DNL Adobe Sign]채우거나 서명할 필드:** 서명자 [!DNL Adobe Sign] 의 필드를 선택합니다. 적응형 양식에는 여러 개의 [!DNL Adobe Sign] 필드가 있을 수 있습니다. 서명자에 대해 특정 필드를 활성화하도록 선택할 수 있습니다. 이 필드에는 사용 가능한 모든 [!DNL Adobe Sign] 블록이 표시됩니다. 블록을 선택하면 블록의 모든 필드가 선택됩니다. X 아이콘을 사용하여 필드를 선택 취소할 수 있습니다.

   ![서명자 세부 정보](assets/signer-details.png)

   위의 이미지에는 두 개의 [!DNL Adobe Sign] 블록 예제가 있습니다.개인 정보 및 Office 세부 정보

   완료 ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png) 아이콘을 탭합니다. 서명자가 추가되고 구성됩니다.

### 적응형 양식에 대한 제출 작업 선택 {#selectsubmitactionforanadaptiveform}

적응형 양식에 [!DNL Adobe Sign] 필드를 추가하고, 양식 컨테이너에서 [!DNL Adobe Sign] 을 활성화하고, [!DNL Adobe Sign] Cloud Service을 선택하고, [!DNL Adobe Sign] 서명자를 추가하고, 적응형 양식에 대해 적절한 제출 작업을 선택합니다. 적응형 양식 제출 작업에 대한 자세한 내용은 [제출 작업 구성](../../forms/using/configuring-submit-actions.md)을 참조하십시오.

또한 모든 서명자가 양식에 서명한 후에만 [!DNL Adobe Sign] 활성화된 적응형 양식이 제출됩니다. 양식 포털의 보류 중인 서명 섹션에서 부분적으로 서명된 양식을 찾을 수 있습니다. [!DNL Adobe Sign] Configuration Service는 서명  [!DNL Adobe Sign] 상태를 확인하기 위해  [일반 ](../../forms/using/adobe-sign-integration-adaptive-forms.md) 간격으로 폴링 서버를 유지합니다. 모든 서명자가 양식 서명을 완료하면 제출 작업 서비스가 시작되고 양식이 제출됩니다. 사용자 지정 제출 작업을 사용하는 양식이고 [!DNL Adobe Sign]을 사용하는 경우에는 사용자 지정 제출 작업을 업데이트하여 제출 작업 서비스를 사용하십시오.

<!-- Remove when forms portal goes live
>[!NOTE]
>
>Data of the adaptive form is stored temporarily on Forms Portal. It is recommended to use [custom storage for Forms Portal](/help/forms/using/configuring-draft-submission-storage.md). It ensures that the PII (personally identifiable information) data is not stored on AEM servers. 
-->

양식 서명 경험이 준비되었습니다. 양식을 미리 보고 서명 경험을 확인할 수 있습니다. 게시된 양식에서 서명자가 이메일을 통해 서명을 위한 양식을 수신하면 [!DNL Adobe Sign] 블록 필드가 표시됩니다. 이 경험을 양식 없는 서명 경험이라고도 합니다. 첫 번째 서명자에 대해 양식 서명 경험을 구성할 수도 있습니다. 자세한 단계는 [양식 서명 경험 만들기](../../forms/using/working-with-adobe-sign.md#create-in-form-signing-experience)를 참조하십시오.

## 적응형 양식 {#configure-cloud-signatures-for-an-adaptive-form}에 대한 클라우드 서명 구성

클라우드 기반 디지털 서명 또는 원격 서명은 데스크탑, 모바일 및 웹에서 작동하는 새로운 세대의 디지털 서명으로, 서명자 인증을 위한 최고 수준의 규정 준수 및 보증을 충족합니다. 클라우드 기반 디지털 서명을 사용하여 적응형 양식에 서명할 수 있습니다.

Adobe 기호](../../forms/using/working-with-adobe-sign.md#enableadobesign)에 대한 적응형 양식 속성을 편집한 후 다음 단계를 수행하여 클라우드 서명 필드를 적응형 양식에 추가합니다.[

1. 구성 요소 브라우저에서 적응형 양식으로 **[!UICONTROL Adobe Sign Block]** 구성 요소를 드래그하여 놓습니다. [!UICONTROL Adobe Sign 블록] 구성 요소에는 지원되는 모든 [!DNL Adobe Sign] 필드가 있습니다. 기본적으로 적응형 양식에 **[!UICONTROL 서명]** 필드가 추가됩니다.

   ![기호 블록](assets/sign-block-new.png)

1. **[!UICONTROL Adobe Sign 블록]** 구성 요소를 선택하고 **편집** ![aem_6_3_edit](assets/aem_6_3_edit.png) 아이콘을 탭합니다. 필드의 필드와 형식 모양을 추가하는 옵션이 표시됩니다.

   ![adobe sign-block-select-fields](assets/adobe-sign-block-select-fields.png)

   **A.** 필드를 선택하고  [!DNL Adobe Sign] 추가합니다. **B.** 블록을  [!DNL Adobe Sign] 전체 화면 보기로 확장합니다.

1. **[!UICONTROL Adobe Sign 필드]** ![aem_6_3_adobesign](assets/aem_6_3_adobesign.png) 아이콘을 탭합니다. [!DNL Adobe Sign] 필드를 선택하고 추가하는 옵션이 표시됩니다.

   **[!UICONTROL 유형]** 드롭다운 필드를 확장하여 **[!UICONTROL 디지털 서명]**&#x200B;을 선택하고 **완료** 아이콘을 탭하여 선택한 필드를 [!DNL Adobe Sign] 블록에 추가합니다.

   ![디지털 서명](assets/digital_signatures_new.png)

   필드에 고유한 이름을 입력해야 합니다.

   다음을 사용하여 적응형 양식에 디지털 서명을 적용합니다.

   * 클라우드 서명:트러스트 서비스 공급자가 호스팅하는 [디지털 ID](https://helpx.adobe.com/sign/kb/digital-certificate-providers.html)로 서명합니다.
   * Adobe Acrobat 또는 Reader:Adobe Acrobat 또는 Reader으로 문서를 다운로드하여 열어 스마트 카드, USB 토큰 또는 파일 기반 디지털 ID를 사용하여 서명합니다.

   적응형 양식에 클라우드 서명 필드를 추가한 후 다음 단계를 수행하여 구성 프로세스를 완료합니다.

   * [적응형 양식에 Adobe Sign 활성화](../../forms/using/working-with-adobe-sign.md#enableadobsignforanadaptiveform)
   * [적응형 양식에 대한 Adobe Sign Cloud Service 선택](../../forms/using/working-with-adobe-sign.md#selectadobesigncloudserviceforanadaptiveform)
   * [적응형 양식에 Adobe Sign 서명자 추가](../../forms/using/working-with-adobe-sign.md#addsignerstoanadaptiveform)
   * [적응형 양식에 대한 제출 작업 선택](../../forms/using/working-with-adobe-sign.md#selectsubmitactionforanadaptiveform)


## 양식 서명 경험 만들기 {#create-in-form-signing-experience}

사용자는 양식을 채우는 동안 적응형 양식에 서명할 수도 있습니다. 이 경험을 양식 서명 경험이라고도 합니다. 양식 서명 환경은 여러 서명자 환경에서 첫 번째 가수만 사용할 수 있습니다. 적응형 양식에 대해 양식 서명 경험을 만들려면 다음 단계를 수행하십시오.

1. [서명 단계 구성 요소를 추가 및 구성합니다](../../forms/using/working-with-adobe-sign.md#add-and-configure-the-signature-step-component).
1. [요약 단계 구성 요소를 추가합니다](../../forms/using/working-with-adobe-sign.md#configure-the-thank-you-page-or-summary-step-component).

![양식 서명 경험](assets/in_form_signing_experience_new.png)

### 서명 단계 구성 요소 {#add-and-configure-the-signature-step-component} 추가 및 구성

서명 단계 구성 요소를 사용하여 채워진 양식에 전자 서명할 영역을 제공합니다. 서명 단계 구성 요소가 포함된 섹션을 렌더링하면 채워진 양식의 서명 가능한 PDF 버전이 표시됩니다. 서명 단계 구성 요소는 양식에 사용할 수 있는 전체 너비를 높입니다. 서명 단계 구성 요소가 포함된 섹션에는 다른 구성 요소가 없는 것이 좋습니다.

다음 단계를 수행하여 서명 단계 구성 요소를 구성합니다.

1. 구성 요소 브라우저에서 **[!UICONTROL 서명 단계]** 구성 요소를 양식에 드래그하여 놓습니다.
1. 새로 추가된 서명 단계 구성 요소를 선택하고 **구성** ![구성](assets/configure.png) 아이콘을 탭합니다. 속성 브라우저를 열고 서명 단계 속성을 표시합니다. 다음 속성을 구성합니다.

   * **[!UICONTROL 이름]**:구성 요소의 이름을 지정합니다.

   * **[!UICONTROL 제목]:** 구성 요소의 고유한 제목을 지정합니다.
   * **[!UICONTROL 템플릿 메시지]:**  서명 PDF를 로드하는 동안 표시할 메시지를 지정합니다. [!DNL Adobe Sign] 서비스는 서명 PDF를 준비하고 로드하는 데 시간이 오래 걸립니다.
   * **[!UICONTROL 서명 서비스]:** 옵션을  **[!DNL Adobe Sign]** 선택합니다.

   * **[!UICONTROL 기존 E-sign 구성 요소 사용]**: [AEM Forms Workspace](../../forms/using/introduction-html-workspace.md), AEM  [!DNL Forms] 앱 또는 기본 적응형 양식에 기존 전자 서명 구성 요소가 있는 경우 기존 전자  **서명 구성 요소 사용 옵션을** 선택합니다.

   * **[!UICONTROL 구성]**:구성([!DNL Adobe Sign]  Cloud Service)을 선택합니다. 드롭다운 상자는 **기존 전자 서명 구성 요소 사용** 옵션이 활성화된 경우에만 사용할 수 있습니다.

   * **[!UICONTROL CSS 클래스]**:구성 요소의 CSS 클래스를 지정합니다.

   완료 ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png) 아이콘을 탭하여 변경 내용을 저장합니다.

   ![서명 단계](assets/signature_step_new.png)

   >[!NOTE]
   >
   > * **[!UICONTROL 서명 단계]** 구성 요소를 양식에 드래그하여 놓으면 **[!UICONTROL 서명자와 양식에 입력된 사람이 동일합니까?]** 옵션이 자동으로 예로  **설정됩니다**. 양식을 계속 작동시켜야 합니다.
      >
      > 
   * 최상의 경험을 위해 서명 단계 구성 요소 뒤에 요약 단계 구성 요소를 사용합니다. 요약 단계는 서명 단계 구성 요소에서 양식에 서명을 완료한 후 자동으로 즉시 양식을 제출합니다. 요약 단계를 사용하지 않는 경우 [Adobe Sign 구성 서비스](../../forms/using/adobe-sign-integration-adaptive-forms.md#configure-adobe-sign-scheduler-to-sync-the-signing-status)를 사용하여 설정된 간격 후에만 자동 제출이 트리거됩니다.
      > 몇 가지 우수 사례는 다음과 같습니다.
   > * 서명 단계를 포함하는 적응형 양식 패널은 항상 적응형 양식의 마지막 또는 두 번째 마지막 패널에 있습니다. 마지막 패널에 요약 단계가 포함된 경우에만 두 번째 마지막 패널이 될 수 있습니다.
   > * 서명 또는 요약 단계 구성 요소가 포함된 패널에는 다른 구성 요소가 포함될 수 없습니다.
   > * 서명 단계가 포함된 적응형 양식에는 전송 단추를 사용할 수 없습니다.
   > * 서명 단계가 포함된 적응형 양식에 대한 제출은 백그라운드 서비스 또는 요약 단계를 통해 처리됩니다. 양식을 채우는 구성된 서명자가 한 명 있는 경우 요약 단계를 사용하여 적응형 양식 제출을 처리하는 이점은 서명자가 양식에 서명했는지 즉시 평가하고 제출 작업을 호출하는 것입니다. 배경 서비스는 구성된 모든 서명자가 양식에 서명했는지 여부를 평가하고 적응형 양식 제출을 지연시키는 데 더 많은 시간이 소요됩니다.
   > * 사용자가 서명 또는 요약 단계가 포함된 패널에서 다시 탐색할 수 없도록 양식을 디자인합니다.



### 감사 인사 페이지 또는 요약 단계 구성 요소 {#configure-the-thank-you-page-or-summary-step-component} 구성

**요약 단계** 구성 요소는 자동으로 양식을 제출하고, 사용자 지정된 요약 페이지 내에 정보를 채우고, 제출된 양식의 요약을 표시합니다. 또한 반환 맵에서 필요한 정보를 가져옵니다. 요약 단계 구성 요소는 양식에 사용할 수 있는 전체 너비를 설정합니다. 요약 단계 구성 요소가 포함된 섹션에는 다른 구성 요소가 없는 것이 좋습니다.

이제 양식 서명 경험을 사용할 수 있습니다. 양식을 미리 보고 서명 경험을 확인할 수 있습니다.

## FAQ {#frequently-asked-questions}

**Q:** 다른 적응형 양식에 적응형 양식을 포함할 수 있습니다. 포함된 적응형 양식을 [!DNL Adobe Sign] 활성화할 수 있습니까?
**Ans:** 아니요, AEM [!DNL Forms] 는 서명을 위해 활성화된 적응형 양식을 포함하는 적응형  [!DNL Adobe Sign] 양식 사용을 지원하지 않습니다

**Q:** 고급 템플릿을 사용하여 적응형 양식을 만들고 편집을 위해 열면 &quot;전자 서명 또는 서명자가 올바르게 구성되지 않았습니다.&quot;라는 오류 메시지가 표시됩니다. 이 나타납니다. 오류 메시지를 해결하는 방법
**Ans:** 고급 템플릿을 사용하여 생성된 적응형 양식은 사용하도록 구성되어  [!DNL Adobe Sign]있습니다. 오류를 해결하려면 [!DNL Adobe Sign] 클라우드 구성을 만들고 선택하고 적응형 양식의 [!DNL Adobe Sign] 서명자를 구성합니다.

**Q:** 적응형 양식의 정적  [!DNL Adobe Sign] 텍스트 구성 요소에서 텍스트 태그를 사용할 수 있습니까?
**Ans:** 예. 텍스트 구성 요소에서 텍스트 태그를 사용하여  [!DNL Adobe Sign] 레코드  [문서](../../forms/using/generate-document-of-record-for-non-xfa-based-adaptive-forms.md) (레코드 자동 생성 옵션만 해당)가 활성화된 적응형 양식에 필드를 추가할 수 있습니다. 텍스트 태그를 만드는 절차 및 규칙에 대해 알아보려면 [Adobe Sign 설명서](https://helpx.adobe.com/sign/using/text-tag.html)를 참조하십시오. 또한 적응형 양식에는 텍스트 태그에 대한 지원이 제한됩니다. 텍스트 태그를 사용하여 [Adobe Sign Block](../../forms/using/working-with-adobe-sign.md#configure-cloud-signatures-for-an-adaptive-form)에서 지원하는 필드만 만들 수 있습니다.

**Q:** AEM [!DNL Forms] 에서는  [!UICONTROL Adobe Sign ] 블록과 서명 단계 구성 요소를 모두 제공합니다. 적응형 양식에서 동시에 사용할 수 있습니까?
**Ans:**  양식에서 두 구성 요소를 동시에 사용할 수 있습니다. 다음은 이러한 구성 요소를 사용하기 위한 몇 가지 권장 사항입니다.

**Adobe Sign 블록:**  [!UICONTROL Adobe Sign ] 블록을 사용하여 적응형 양식의  [!UICONTROL 어느 곳에서든 Adobe ] 서명 필드를 추가할 수 있습니다. 서명자에게 특정 필드를 할당하는 데에도 도움이 됩니다. 적응형 양식을 미리 보거나 게시한 경우 기본적으로 [!UICONTROL Adobe Sign] 블록이 표시되지 않습니다. 이러한 블록은 서명 문서에서만 사용할 수 있습니다. 서명 문서에서는 서명자에게 지정된 필드만 활성화됩니다. [!UICONTROL Adobe ] 서명 블록은 첫 번째 및 후속 서명자와 함께 사용할 수 있습니다.

**서명 단계 구성 요소:**  서명 단계 구성 요소를 사용하여 양식 서명 경험을 만들 수 있습니다. 양식을 채우는 동안 첫 번째 서명자만 서명할 수 있습니다. 서명 단계 구성 요소가 포함된 섹션을 렌더링하면 양식의 서명 가능한 PDF 버전이 표시됩니다. 일반적으로 양식의 마지막 섹션이나 최종 섹션 뒤에 요약 구성 요소가 옵니다.

## 문제 해결 {#troubleshoot}

### [!DNL Adobe Sign] 계약 실패  {#adobe-sign-agreement-failures}

****
문제 [!DNL Adobe Sign] 적응형 양식에 대해 서비스가 구성되어 있으면 서비스가 기본 적응형 양식에  [!DNL Adobe Sign] 대한 계약을 만들지 못합니다.

**해상도**

* 적응형 양식에 사용된 [Adobe Sign 클라우드 서비스](../../forms/using/adobe-sign-integration-adaptive-forms.md)의 구성을 확인합니다.
* [!DNL Adobe Sign] 클라우드 서비스를 구성하는 데 사용되는 [!DNL Adobe Sign] 서버의 API 애플리케이션에 필요한 권한이 있는지 확인합니다.
* 여러 [!DNL Adobe Sign] 클라우드 서비스를 사용하는 경우 모든 서비스의 **[!UICONTROL oAuth URL]**&#x200B;을 동일한 **[!UICONTROL Adobe Sign Shard]**&#x200B;로 가리킵니다.

* 별도의 이메일 주소를 사용하여 [!DNL Adobe Sign] 계정과 첫 번째 서명자와 단일 서명자에 대해 구성합니다. 첫 번째 서명자 또는 유일한 서명자의 이메일 주소(단일 서명자의 경우)는 AEM 클라우드 서비스를 구성하는 데 사용되는 [!DNL Adobe Sign] 계정과 동일할 수 없습니다.

### [!DNL Adobe Sign] 활성화된 적응형 양식에 대해 구성된 AEM [!DNL Forms] 워크플로가 {#adobe-sign-aem-form-workflow-failures}를 시작하지 않습니다

****
문제 [!DNL Adobe Sign] 가 적응형 양식에 대해 구성되면 워크플로우 호출 옵션 [!DNL Forms] 을 사용하여 구성된 워크플로우가 시작되지 않습니다.

**해상도**

* 서명 단계 없이 [!DNL Adobe Sign]을 사용하거나 양식에 여러 사람의 서명이 필요한 경우 AEM [!DNL Forms] 서버는 스케줄러가 모든 사람이 양식에 서명했는지 확인할 때까지 기다립니다. 스케줄러는 모든 사람이 서명을 완료하고 적응형 양식을 성공적으로 제출한 후에만 워크플로우가 시작되는 후에만 적응형 양식을 제출합니다. [스케줄러](adobe-sign-integration-adaptive-forms.md) 간격을 줄여 빠른 간격으로 양식 서명 상태를 확인하고 양식 제출을 강화할 수 있습니다.


## 관련 문서 {#related-articles}

* [Adobe Sign과 AEM Forms 통합](../../forms/using/adobe-sign-integration-adaptive-forms.md)
* [적응형 양식에서 Adobe Sign을 사용하는 우수 사례](https://medium.com/adobetech/using-adobe-sign-to-e-sign-an-adaptive-form-heres-the-best-way-to-do-it-dc3e15f9b684)
* [AEM Forms에서 Adobe Sign 사용(비디오)](https://helpx.adobe.com/experience-manager/kt/forms/using/adobe-sign-integration-feature-video.html)
