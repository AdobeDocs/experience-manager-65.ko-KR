---
title: 적응형 양식에서 Adobe Sign 사용
seo-title: 적응형 양식에서 Adobe Sign 사용
description: 적응형 양식의 전자 서명(Adobe Sign) 워크플로우를 통해 서명 워크플로우를 자동화하고, 단일 및 다중 서명 프로세스를 단순화하며, 모바일 디바이스에서 양식에 전자 서명할 수 있습니다.
seo-description: 적응형 양식의 전자 서명(Adobe Sign) 워크플로우를 통해 서명 워크플로우를 자동화하고, 단일 및 다중 서명 프로세스를 단순화하며, 모바일 디바이스에서 양식에 전자 서명할 수 있습니다.
uuid: cc3012ed-c318-4529-9adc-61aa5b5761a0
contentOwner: khsingh
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: f79828d8-2230-4477-8ffa-eeb6a0413acd
docset: aem65
translation-type: tm+mt
source-git-commit: 70052a5a8cba16dd2d73179e6e1d617347d716bc
workflow-type: tm+mt
source-wordcount: '3679'
ht-degree: 0%

---


# 적응형 양식에서 Adobe Sign 사용{#using-adobe-sign-in-an-adaptive-form}

Adobe Sign을 사용하면 적응형 양식에 전자 서명 워크플로우를 적용할 수 있습니다. 전자 서명을 사용하면 법률, 영업, 급여, 인사 관리 등 다양한 영역에 맞는 문서를 처리할 수 있는 워크플로우를 향상시킬 수 있습니다.

일반적인 Adobe Sign 및 적응형 양식 시나리오에서 사용자는 적응형 양식을 채워 서비스에 적용합니다. 예를 들어, 대출 및 신용 카드 신청에는 모든 대출자와 공동 지원자의 법적 서명이 필요합니다. 유사한 시나리오에 전자 서명 워크플로우를 사용하려면 Adobe Sign을 AEM Forms과 통합할 수 있습니다. 몇 가지 예는 Adobe Sign을 사용하여 다음을 수행할 수 있습니다.

* 자동화된 제안, 견적 및 계약 프로세스를 통해 모든 디바이스에서 거래를 성사시킬 수 있습니다.
* 인사 관리 프로세스를 보다 신속하게 완료하여 직원에게 디지털 경험을 제공할 수 있습니다.
* 계약 주기 시간을 단축하고 벤더를 보다 신속하게 확보할 수 있습니다.
* 일반적인 프로세스를 자동화하는 디지털 워크플로우 구축

AEM Forms과 Adobe Sign의 통합 기능:

* 단일 및 여러 사용자 서명 워크플로우
* 순차적 및 동시 서명 워크플로우
* 양식 및 양식 외 서명 경험
* 익명 또는 로그인 사용자로 양식 서명
* 동적 서명 프로세스(AEM Forms 워크플로우와 통합)
* 기술 자료, 전화 및 소셜 프로필을 통한 인증

## 전제 조건 {#prerequisites}

적응형 양식으로 Adobe Sign 사용 전:

* AEM Forms 클라우드 서비스가 Adobe Sign을 사용하도록 구성되어 있는지 확인합니다. 자세한 내용은 AEM Forms과 [Adobe Sign 통합을 참조하십시오](../../forms/using/adobe-sign-integration-adaptive-forms.md).
* 서명자 목록 준비 모든 서명자의 이메일 주소를 필요로 합니다.

## 적응형 양식의 Adobe Sign 구성 {#configure-adobe-sign-for-an-adaptive-form}

적응형 양식에 대해 Adobe Sign을 구성하려면 다음 단계를 수행하십시오.

1. [Adobe 서명을 위한 적응형 양식 속성 편집](../../forms/using/working-with-adobe-sign.md#enableadobesign)
1. [적응형 양식에 Adobe Sign 필드 추가](../../forms/using/working-with-adobe-sign.md#addadobesignfieldstoanadaptiveform)
1. [적응형 양식에 Adobe Sign 사용](../../forms/using/working-with-adobe-sign.md#enableadobsignforanadaptiveform)
1. [적응형 양식의 Adobe Sign Cloud Service 선택](../../forms/using/working-with-adobe-sign.md#selectadobesigncloudserviceforanadaptiveform)

1. [적응형 양식에 Adobe Sign 서명자 추가](../../forms/using/working-with-adobe-sign.md#addsignerstoanadaptiveform)
1. [적응형 양식의 작업 제출 선택](../../forms/using/working-with-adobe-sign.md#selectsubmitactionforanadaptiveform)

![서명자 세부 정보](assets/signer_details_new.png)

### Adobe Sign의 적응형 양식 속성 편집 {#enableadobesign}

기존 또는 새 적응형 양식에 대해 Adobe Sign에 대한 적응형 양식 속성을 구성합니다.

[Adobe Sign용 응용 양식](../../forms/using/working-with-adobe-sign.md#create-an-adaptive-form-for-adobe-sign) 만들기에서 기본 적응형 양식을 만드는 단계에 대해 설명합니다. 응용 [양식을 만드는 동안 사용할 수 있는 다른 옵션에 대한 응용 양식](../../forms/using/creating-adaptive-form.md) 만들기를 참조하십시오.

#### Adobe Sign용 적응형 양식 만들기 {#create-an-adaptive-form-for-adobe-sign}

서명 사용 응용 양식을 만들려면 다음 단계를 수행하십시오.

1. Adobe Experience Manager **[!UICONTROL >]** Forms **[!UICONTROL >]** Forms 및 문서로 이동합니다 ****.
1. 만들기 **[!UICONTROL 를]** 누르고 **[!UICONTROL 적응형 양식을 선택합니다]**. 템플릿 목록이 나타납니다. 템플릿을 선택하고 다음을 **[!UICONTROL 누릅니다]**.
1. 기본 **[!UICONTROL 탭에서 다음을]** 수행합니다.

   1. 적응형 양식의 **이름** 및 **제목을** 지정합니다.

   1. AEM Forms으로 Adobe Sign을 구성하는 동안 만들어진 [구성 컨테이너를](../../forms/using/adobe-sign-integration-adaptive-forms.md#configure-adobe-sign-with-aem-forms) 선택합니다.

1. 양식 **[!UICONTROL 모델]** 탭에서 다음 옵션 중 하나를 선택합니다.

   * 양식 **[!UICONTROL 템플릿을 기록 문서로 연결 템플릿]** 옵션을 선택하고 기록 문서 템플릿을 선택합니다. 양식 템플릿을 적응형 양식으로 사용하는 경우 서명을 위해 전송된 문서는 관련 양식 템플릿을 기반으로 하는 필드만 표시합니다. 응용 양식의 모든 필드는 표시되지 않습니다.

   * 기록 문서 **[!UICONTROL 생성 옵션을]** 선택합니다. 문서 기록 옵션 사용 응용 양식을 사용하는 경우 서명을 위해 보낸 문서에 응용 양식의 모든 필드가 표시됩니다.

1. 만들기를 **[!UICONTROL 누릅니다.]** Adobe Sign 필드를 추가하는 데 사용할 수 있는 서명 사용 응용 양식이 만들어집니다.

#### Adobe Sign용 응용 양식 편집 {#editafsign}

기존 적응형 양식에서 Adobe Sign을 사용하려면 다음 단계를 수행하십시오.

1. Adobe Experience Manager **[!UICONTROL >]** Forms **[!UICONTROL >]** Forms 및 문서로 이동합니다 ****.
1. 적응형 양식을 선택하고 속성을 **[!UICONTROL 누릅니다]**.
1. [ **[!UICONTROL 기본]** ] 탭에서 AEM Forms으로 Adobe Sign을 구성하는 동안 만들어진 [구성 컨테이너를](../../forms/using/adobe-sign-integration-adaptive-forms.md#configure-adobe-sign-with-aem-forms) 선택합니다.
1. 양식 **[!UICONTROL 모드]** 탭에서 다음 옵션 중 하나를 선택합니다.

   * 양식 **[!UICONTROL 템플릿을 기록 문서로 연결 템플릿]** 옵션을 선택하고 기록 문서 템플릿을 선택합니다. 양식 템플릿을 적응형 양식으로 사용하는 경우 서명을 위해 전송된 문서는 관련 양식 템플릿을 기반으로 하는 필드만 표시합니다. 응용 양식의 모든 필드는 표시되지 않습니다.

   * 기록 문서 **[!UICONTROL 생성 옵션을]** 선택합니다. 문서 기록 옵션 사용 응용 양식을 사용하는 경우 서명을 위해 보낸 문서에 응용 양식의 모든 필드가 표시됩니다.

1. 저장 **[!UICONTROL 및 닫기를 누릅니다]**. 적응형 양식이 Adobe Sign에 대해 활성화됩니다.

### 적응형 양식에 Adobe Sign 필드 추가 {#addadobesignfieldstoanadaptiveform}

Adobe Sign에는 적응형 형태로 배치할 수 있는 다양한 필드가 있습니다. 이러한 필드에는 서명, 이니셜, 회사 또는 제목과 같은 다양한 유형의 데이터가 적용되며 서명 과정에서 추가 정보를 수집할 수 있습니다. Adobe Sign 블록 구성 요소를 사용하여 Adobe Sign 필드를 적응형 양식의 다양한 위치에 배치할 수 있습니다.

적응형 양식에 필드를 추가하고 이러한 필드와 관련된 다양한 옵션을 사용자 정의하려면 다음 단계를 수행하십시오.

1. 구성 요소 브라우저의 **Adobe Sign 블록** 구성 요소를 응용 양식으로 드래그하여 놓습니다. Adobe Sign 블록 구성 요소에는 지원되는 모든 Adobe Sign 필드가 있습니다. 기본적으로 응용 양식에 **서명** 필드를 추가합니다.

   ![Sign 블록](assets/sign_block_new.png)

   기본적으로, Adobe Sign 블록은 게시된 적응형 양식에 표시되지 않습니다. 서명 문서에서만 볼 수 있습니다. Adobe Sign 블록 구성 요소의 속성에서 Adobe Sign 블록의 가시성을 변경할 수 있습니다.

   >[!NOTE]
   >
   >    * Adobe Sign 블록을 사용하는 것은 적응형 형식으로 Adobe Sign을 사용하는 것이 필수는 아닙니다. Adobe Sign 블록을 사용하고 서명자의 필드를 추가하지 않는 경우 서명 문서 하단에 기본 서명 필드가 표시됩니다.
   >    * 기록 문서를 자동으로 생성하는 이러한 고급 양식에 대해서만 Adobe Sign 블록을 사용하십시오. 사용자 지정 XDP를 사용하여 기록 문서 또는 적응형 양식을 생성하는 경우 Adobe Sign 블록이 필요하지 않습니다.


1. Adobe Sign **블록** 구성 요소를 선택하고 **aem_6_** 3_edit ![아이콘을](assets/aem_6_3_edit.png) 누릅니다. 필드의 필드 및 형식 모양을 추가하는 옵션이 표시됩니다.

   ![adobe-sign-block-select-fields](assets/adobe-sign-block-select-fields.png)

   **A.** Adobe Sign 필드를 선택하고 추가합니다. **B.** Adobe Sign 블록을 전체 화면 보기로 확장

1. **Adobe Sign 필드** aem_6_ ![3_adobesign](assets/aem_6_3_adobesign.png) 아이콘을 누릅니다. Adobe Sign 필드를 선택하고 추가하는 옵션이 표시됩니다.

   유형 **드롭다운** 필드를 확장하여 Adobe Sign 필드를 선택하고 완료 ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png) 아이콘을 눌러 선택한 필드를 Adobe Sign 블록에 추가합니다. 유형 **** 드롭다운 필드에는 서명, 서명자 정보 및 데이터 필드 유형이 포함되어 있습니다. 유형 드롭다운 상자에 나열된 AEM Forms 지원 필드와 Adobe Sign 통합 Adobe Sign 필드에 대한 자세한 내용은 [Adobe Sign 설명서를 참조하십시오](https://helpx.adobe.com/sign/help/field-types.html).

   ![adobe-sign-block-fields-options](assets/adobe-sign-block-fields-options.png)

   필드에 고유한 이름을 입력해야 합니다. 필수 옵션을 선택하여 필드를 필수로 표시할 수도 있습니다. [ **이름** ] 및 [필수] 옵션 ****&#x200B;외에도 일부 Adobe Sign 필드에 더 많은 옵션이 있습니다. 예를 들어, 마스크 및 여러 줄로 된 파일을 저장할 수 있습니다. 또한 필드가 동일한 Adobe Sign 블록에 있는지 또는 다른 블록에 있는지 여부에 따라 각 Adobe Sign 필드에 고유한 이름을 지정합니다.

   드롭다운 목록에서 **디지털 서명** 을 선택하는 경우 적응형 양식에 디지털 서명을 적용할 수 있습니다.

   * 클라우드 서명을 사용하여 TSP(Trust Service Provider)에서 호스팅하는 [디지털 ID로](https://helpx.adobe.com/sign/kb/digital-certificate-providers.html) 서명할 수 있습니다.
   * 스마트 카드, USB 토큰 또는 파일 기반 디지털 ID를 사용하여 Adobe Acrobat 또는 Reader으로 문서를 로컬로 다운로드하여 문서를 다운로드합니다.

### 적응형 양식에 Adobe Sign 사용 {#enableadobsignforanadaptiveform}

기본적으로 Adobe Sign은 적응형 양식에 사용할 수 없습니다. 다음 단계를 수행하여 활성화합니다.

1. 컨텐츠 브라우저에서 **양식 컨테이너**&#x200B;를 누르고 구성 **** 구성 ![](assets/configure.png) 아이콘을누릅니다. 속성 브라우저를 열고 응용 양식 컨테이너 속성을 표시합니다.
1. 속성 브라우저에서 **전자 서명** 아코디언을 확장하고 [Adobe Sign **사용** ] 옵션을 선택합니다. Adobe Sign의 적응형 양식을 활용할 수 있습니다.

### Adobe Sign Cloud Service 및 서명 주문 선택 {#selectadobesigncloudserviceforanadaptiveform}

AEM Forms 인스턴스에 대해 여러 Adobe Sign 서비스를 구성할 수 있습니다. 각 기능(Human Resource, Finance 등)에 대해 별도의 서비스 세트가 있어야 합니다. 서명된 문서의 추적 및 보고 작업이 수월해집니다. 예를 들어 은행에 여러 부서가 있습니다. 문서를 더 잘 추적하기 위해 각 부서에 대해 별도의 구성을 가질 수 있습니다.

한 문서에 여러 서명자를 포함시킬 수도 있습니다. 예를 들어 신용카드 지원서에는 여러 명의 지원자가 포함될 수 있습니다. 은행에서는 신청서를 처리하기 전에 모든 지원자의 서명을 요구한다. 여러 서명자 시나리오의 경우 문서를 순차적 또는 동시에 서명하도록 선택할 수 있습니다.

클라우드 서비스와 서명 순서를 선택하려면 다음 단계를 수행하십시오.

![클라우드 서비스](assets/cloud-service.png)

1. 컨텐츠 브라우저에서 **양식 컨테이너**&#x200B;를 누르고 구성 **** 구성 ![](assets/configure.png) 아이콘을누릅니다. 속성 브라우저를 열고 응용 양식 컨테이너 속성을 표시합니다.
1. 속성 브라우저에서 **전자 서명** 아코디언을 확장하고 [Adobe Sign **사용** ] 옵션을 선택합니다. Adobe Sign의 적응형 양식을 활용할 수 있습니다.
1. 이미 구성된 Adobe Sign Cloud Service 목록에서 클라우드 서비스를 선택합니다.

   Adobe Sign **Cloud Service** 목록이 비어 있는 경우 AEM Forms과 함께 [Adobe Sign](../../forms/using/adobe-sign-integration-adaptive-forms.md) 구성 아티클에 따라 서비스를 구성합니다.

1. 서명자가 서명할 수 있음 **대화 상자에서 서명** 순서를 선택합니다. Adobe Sign 가수들은 임의의 순서대로 **적응형** 양식에 서명할 수 있습니다. 즉, 다른 서명자의 다음 또 **는 동시에** 서명할 수 있습니다.

   한 서명자가 서명을 위한 양식을 한 번에 차례로 수신하게 됩니다. 서명자가 문서에 서명하면 양식이 다음 서명자에게 보내는 등의 작업을 수행합니다.

   동시에 여러 서명자가 한 번에 양식에 서명할 수 있습니다.

1. [적응형 양식에](../../forms/using/working-with-adobe-sign.md#addsignerstoanadaptiveform) 서명자를 추가하고 [aem_6_3_forms_save](assets/aem_6_3_forms_save.png) 아이콘을 눌러 변경 사항을 저장합니다.


### 적응형 양식에 서명자 추가 {#addsignerstoanadaptiveform}

적응형 양식의 서명자는 한 명 또는 여러 명으로 할 수 있습니다. 서명자를 추가할 때 서명자에 대한 인증 세부 사항을 구성할 수도 있습니다. 또한 양식 채우기 및 가수가 같은 사람인지 선택할 수 있습니다. 서명자에 대한 다양한 세부 정보를 추가하고 제공하려면 다음 단계를 수행하십시오.

1. 컨텐츠 브라우저에서 **양식 컨테이너**&#x200B;를 누르고 구성 **** 구성 ![](assets/configure.png) 아이콘을누릅니다. 응용 양식 컨테이너 속성이 있는 속성 브라우저를 엽니다.
1. 속성 브라우저에서 **전자 서명** 아코디언을 확장하고 [Adobe Sign **사용** ] 옵션을 선택합니다. Adobe Sign의 적응형 양식을 활용할 수 있습니다.
1. 서명자 **구성** 아래의 서명자 **추가를 누릅니다**. 적응형 양식에 서명자가 추가됩니다. 적응형 양식에 여러 Adobe Sign 서명자를 추가할 수 있습니다.
1. ![전화 정보](assets/phone-details.png)

   aem_ **6** _ ![3_edit](assets/aem_6_3_edit.png) 아이콘을 클릭하여 서명자에 대한 다음 정보를 지정합니다.

   * **제목:** 서명자를 고유하게 식별하는 제목을 지정합니다.

   * **서명자와 양식 작성자는 동일합니까?** 양식 작성자 **와**&#x200B;첫 번째 서명자가 동일한 경우 예를 선택합니다. 이 옵션이 **아니요로 설정된** 경우 적응형 양식의 서명 단계 구성 요소를 사용하지 마십시오. 양식에 서명 단계 구성 요소가 포함되어 있으면 해당 필드는 자동으로 예로 설정됩니다.

   * **서명자 이메일 주소:** 서명자의 이메일 주소를 지정합니다. 서명자는 지정된 이메일 주소로 문서/양식에 서명하도록 수신됩니다. 양식 필드에 제공된 이메일 주소를 사용하거나, 로그인한 사용자의 AEM 사용자 프로필에 사용하거나, 이메일 주소를 수동으로 입력할 수 있습니다. It is a mandatory step. Ensure that the email address of the first signer or the only signer (in case of single signer) is not identical to Adobe Sign account used to configure AEM cloud services.

   * **Signer Authentication Method:** Specify the method to authenticate a user before opening a form for signing. You can choose between phone, knowledge base, and social identity-based authentication.
   >[!NOTE]
   >
   >    * By default, the social identity-based authentication provides an option to authenticate using Facebook, Google, and LinkedIn. 다른 소셜 인증 공급자를 활성화하려면 Adobe Sign 지원에 문의할 수 있습니다.


   * **Adobe Sign fields to fill or sign:** Select Adobe Sign fields for the signer. 적응형 양식에는 여러 개의 Adobe Sign 필드가 있을 수 있습니다. You can choose to enable specific fields for a signer. 이 필드는 사용 가능한 모든 Adobe Sign 블록을 표시합니다. When you select a block, all the fields of the block are selected. You can use the X icon to deselect a field.

   ![signer-details](assets/signer-details.png)

   The above image has two example Adobe Sign Blocks: Personal-Information and Office-details

   Tap the Done ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png) icon. 서명자가 추가되고 구성됩니다.

### 적응형 양식의 작업 제출 선택 {#selectsubmitactionforanadaptiveform}

이후 적응형 양식에 Adobe Sign 필드를 추가하고, 양식 컨테이너에서 Adobe Sign을 활성화하고, Adobe Sign Cloud Service을 선택하고, Adobe Sign 서명자를 추가하고, 적응형 양식에 적합한 제출 작업을 선택합니다. 적응형 양식 제출 작업에 대한 자세한 내용은 제출 작업 [구성을 참조하십시오](../../forms/using/configuring-submit-actions.md).

또한 Adobe Sign 지원 적응형 양식은 모든 서명자가 양식에 서명한 후에만 제출됩니다. 양식 포털의 Pending Sign 섹션에서 부분적으로 서명된 양식을 찾을 수 있습니다. Adobe Sign 구성 서비스는 [정기적으로](../../forms/using/adobe-sign-integration-adaptive-forms.md) Adobe Sign 서버를 폴링하여 서명 상태를 확인합니다. 모든 서명자가 양식 서명을 완료하면 제출 작업 서비스가 시작되고 양식이 제출됩니다. 사용자 지정 제출 작업을 사용하고 양식에 Adobe Sign이 사용된 경우 사용자 지정 제출 작업을 업데이트하여 제출 작업 서비스를 사용하십시오.

>[!NOTE]
>
>적응형 양식의 데이터는 Forms 포털에 일시적으로 저장됩니다. Forms 포털에는 [맞춤형 스토리지를 사용하는 것이 좋습니다](/help/forms/using/configuring-draft-submission-storage.md). PII(개인 식별 정보) 데이터가 AEM 서버에 저장되지 않도록 합니다.

양식 서명 환경을 경험해 보십시오. 양식을 미리 보고 서명 환경을 확인할 수 있습니다. On the published form, Adobe Sign Block fields are displayed when a signer receives the form for signing through an email. This experience is also known as out-of-form signing experience. 첫 번째 서명자에 대해 양식 서명 환경을 구성할 수도 있습니다. 자세한 내용은 양식 서명 경험 [만들기를 참조하십시오](../../forms/using/working-with-adobe-sign.md#create-in-form-signing-experience).

## 적응형 양식에 대한 클라우드 서명 구성 {#configure-cloud-signatures-for-an-adaptive-form}

Cloud-based digital signatures or remote signatures are a new generation of digital signatures that work across desktop, mobile, and the web — and meet the highest levels of compliance and assurance for signer authentication. 클라우드 기반의 디지털 서명을 사용하여 적응형 양식에 서명할 수 있습니다.

Adobe 서명에 [대한 적응형 양식 속성을](../../forms/using/working-with-adobe-sign.md#enableadobesign)편집한 후 다음 단계를 수행하여 적응형 양식에 클라우드 서명 필드를 추가합니다.

1. 구성 요소 브라우저의 **Adobe Sign 블록** 구성 요소를 응용 양식으로 드래그하여 놓습니다. Adobe Sign 블록 구성 요소에는 지원되는 모든 Adobe Sign 필드가 있습니다. 기본적으로 응용 양식에 **서명** 필드를 추가합니다.

   ![Sign 블록](assets/sign-block-new.png)

1. Adobe Sign **블록** 구성 요소를 선택하고 **aem_6_** 3_edit ![아이콘을](assets/aem_6_3_edit.png) 누릅니다. 필드의 필드 및 형식 모양을 추가하는 옵션이 표시됩니다.

   ![adobe-sign-block-select-fields](assets/adobe-sign-block-select-fields.png)

   **A.** Adobe Sign 필드를 선택하고 추가합니다. **B.** Adobe Sign 블록을 전체 화면 보기로 확장

1. **Adobe Sign 필드** aem_6_ ![3_adobesign](assets/aem_6_3_adobesign.png) 아이콘을 누릅니다. Adobe Sign 필드를 선택하고 추가하는 옵션이 표시됩니다.

   유형 **드롭다운** 필드를 확장하여 **디지털 서명을** 선택하고 완료 아이콘을 눌러 선택한 필드를 Adobe Sign 블록에 추가합니다.

   ![디지털 서명](assets/digital_signatures_new.png)

   필드에 고유한 이름을 입력해야 합니다.

   다음을 사용하여 적응형 양식에 디지털 서명 적용

   * 클라우드 서명: 트러스트 서비스 제공업체에서 호스팅하는 [디지털 ID로](https://helpx.adobe.com/sign/kb/digital-certificate-providers.html) 서명합니다.
   * Adobe Acrobat 또는 Reader: 스마트 카드, USB 토큰 또는 파일 기반 디지털 ID를 사용하여 문서를 다운로드하여 Adobe Acrobat 또는 Reader에서 엽니다.

   적응형 양식에 클라우드 서명 필드를 추가한 후 다음 단계를 수행하여 구성 프로세스를 완료합니다.

   * [적응형 양식에 Adobe Sign 사용](../../forms/using/working-with-adobe-sign.md#enableadobsignforanadaptiveform)
   * [적응형 양식의 Adobe Sign Cloud Service 선택](../../forms/using/working-with-adobe-sign.md#selectadobesigncloudserviceforanadaptiveform)
   * [적응형 양식에 Adobe Sign 서명자 추가](../../forms/using/working-with-adobe-sign.md#addsignerstoanadaptiveform)
   * [적응형 양식의 작업 제출 선택](../../forms/using/working-with-adobe-sign.md#selectsubmitactionforanadaptiveform)


## 양식 서명 경험 만들기 {#create-in-form-signing-experience}

사용자는 양식을 채우는 동안 적응형 양식에 서명할 수도 있습니다. 이 경험은 양식 서명 경험이라고도 합니다. 양식 서명 환경은 여러 서명자 환경에서 첫 번째 서명자만 사용할 수 있습니다. 적응형 양식의 양식 서명 환경을 만들려면 다음 단계를 수행하십시오.

1. [서명 단계 구성 요소를 추가하고 구성합니다](../../forms/using/working-with-adobe-sign.md#add-and-configure-the-signature-step-component).
1. [요약 단계 구성 요소를 추가합니다](../../forms/using/working-with-adobe-sign.md#configure-the-thank-you-page-or-summary-step-component).

![양식 서명 경험](assets/in_form_signing_experience_new.png)

### 서명 단계 구성 요소 추가 및 구성 {#add-and-configure-the-signature-step-component}

서명 단계 구성 요소를 사용하여 채워진 양식에 전자 서명할 영역을 제공하십시오. 서명 단계 구성 요소를 포함하는 섹션이 렌더링되면 채워진 양식의 서명 가능한 PDF 버전이 표시됩니다. 서명 단계 구성 요소는 양식에 사용할 수 있는 전체 너비를 차지합니다. 서명 단계 구성 요소를 포함하는 섹션에는 다른 구성 요소가 없는 것이 좋습니다.

서명 단계 구성 요소를 구성하려면 다음 단계를 수행하십시오.

1. 구성 요소 브라우저에서 **서명 단계** 구성 요소를 양식으로 드래그하여 놓습니다.
1. 새로 추가된 서명 단계 구성 요소를 선택하고 구성 **아이콘을** ![누릅니다](assets/configure.png) . 속성 브라우저를 열고 서명 단계 속성을 표시합니다. 다음 속성을 구성합니다.

   * **요소 이름**: 구성 요소의 이름을 지정합니다.

   * **제목:** 구성 요소의 고유한 제목을 지정합니다.
   * **템플릿 메시지:** 서명 PDF를 로드하는 동안 표시할 메시지를 지정합니다. Adobe Sign 서비스는 서명 PDF를 준비하고 로드하는 데 시간이 다소 소요됩니다.
   * **서명 서비스:** Adobe Sign **옵션을** 선택합니다.

   * **기존 전자 서명 구성 요소**&#x200B;사용: AEM Forms 작업 공간 [, AEM Forms 앱 또는 기본 응용 양식에 기존 전자 서명 구성 요소가 있는 경우 기존 전자 서명 구성 요소](../../forms/using/introduction-html-workspace.md)사용 옵션을 선택합니다 **** .

   * **구성**: 구성(Adobe Sign Cloud Service)을 선택합니다. 드롭다운 상자는 이전 전자 서명 구성 요소 **사용** 옵션이 활성화된 경우에만 사용할 수 있습니다.

   변경 사항을 저장하려면 ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png) 완료 아이콘을 누릅니다.

   ![서명 단계](assets/signature_step_new.png)

   >[!NOTE]
   >
   > * 서명 **[!UICONTROL 단계]** 구성 요소를 양식에 드래그하여 놓으면 **[!UICONTROL 서명자와 양식을 채우는 사람이 동일합니까?]** 옵션이 자동으로 **예로 설정됩니다**. 양식을 계속 작동시켜야 합니다.
      >
      > 
   * 최상의 경험을 위해 서명 단계 구성 요소 다음의 요약 단계 구성 요소를 사용하십시오. [요약] 단계는 서명 단계 구성 요소에서 양식 서명을 완료한 후 즉시 양식을 자동으로 제출합니다. 요약 단계를 사용하지 않는 경우 자동 제출은 [Adobe Sign 구성 서비스를 사용하는 간격 설정 후에만 트리거됩니다](../../forms/using/adobe-sign-integration-adaptive-forms.md#configure-adobe-sign-scheduler-to-sync-the-signing-status).
   > * 몇 가지 우수 사례는 다음과 같습니다.
   > * 서명 단계가 포함된 응용 양식 패널은 항상 응용 양식의 마지막 패널이나 두 번째 패널에 있습니다. 마지막 패널에 [요약] 단계가 포함된 경우에만 두 번째 마지막 패널이 될 수 있습니다.
   > * 서명 또는 요약 단계 구성 요소가 포함된 패널에는 다른 구성 요소가 포함될 수 없습니다.
   > * 서명 단계가 포함된 응용 양식에는 전송 단추를 사용할 수 없습니다. 제출은 백그라운드 서비스 또는 요약 단계를 통해 처리됩니다.
   > * 사용자가 서명 또는 요약 단계가 포함된 패널에서 다시 이동할 수 없도록 양식을 디자인합니다.



### 감사 페이지 또는 요약 단계 구성 요소 구성 {#configure-the-thank-you-page-or-summary-step-component}

요약 **단계** 구성 요소는 자동으로 양식을 제출하고 사용자 지정된 요약 페이지 내에 정보를 채우고 제출된 양식의 요약을 표시합니다. 반품 맵에서 필요한 정보도 얻을 수 있습니다. 요약 단계 구성 요소는 양식에 사용할 수 있는 전체 너비를 차지합니다. 요약 단계 구성 요소를 포함하는 섹션에는 다른 구성 요소가 없는 것이 좋습니다.

이제 양식 서명 환경을 경험해 보십시오. 양식을 미리 보고 서명 환경을 확인할 수 있습니다.

## FAQ {#frequently-asked-questions}

**Ans:** 아니요. AEM Forms은 Adobe Sign이 활성화된 적응형 양식을 서명을 위해 포함하는 적응형 양식 사용을 지원하지 않습니다.

**Ans:** 고급 템플릿을 사용하여 만든 응용 양식이 Adobe Sign을 사용하도록 구성되었습니다. 오류를 해결하려면 Adobe Sign 클라우드 구성을 만들고 선택하고 적응형 양식의 Adobe Sign 서명자를 구성합니다.

**Ans:** 예. 텍스트 구성 요소의 텍스트 태그를 사용하여 활성화된 적응형 양식의 기록 [문서](../../forms/using/generate-document-of-record-for-non-xfa-based-adaptive-forms.md) (자동 생성 문서 옵션만 해당)에 Adobe Sign 필드를 추가할 수 있습니다. 텍스트 태그를 만드는 절차와 규칙에 대해 자세히 알아보려면 [Adobe Sign 설명서를 참조하십시오](https://helpx.adobe.com/sign/help/text-tags.html). 또한 적응형 양식에는 텍스트 태그에 대한 지원이 제한됩니다. 텍스트 태그를 사용하여 [Adobe Sign 블록에서 지원하는 필드만 만들 수](../../forms/using/working-with-adobe-sign.md#configure-cloud-signatures-for-an-adaptive-form) 있습니다.

**Ans:** 양식에서 두 구성 요소를 동시에 사용할 수 있습니다. 다음은 이러한 구성 요소를 사용하기 위한 몇 가지 권장 사항입니다.

**Adobe Sign 블록:** Adobe Sign 블록을 사용하여 적응형 양식의 아무 곳에나 Adobe Sign 필드를 추가할 수 있습니다. 서명자에게 특정 필드를 할당하는 데에도 도움이 됩니다. 응용 양식을 미리 보거나 게시한 Adobe Sign 블록이 표시되지 않는 경우 기본적으로 표시됩니다. 이러한 블록은 서명 문서에서만 활성화됩니다. 서명 문서에서는 서명자에게 할당된 필드만 활성화됩니다. Adobe Sign 블록을 첫 번째 및 다음 서명자와 함께 사용할 수 있습니다.

**서명 단계 구성 요소:** 서명 단계 구성 요소를 사용하여 양식 서명 환경을 만들 수 있습니다. 양식을 작성하는 동안 첫 번째 서명자만 서명할 수 있습니다. 서명 단계 구성 요소가 포함된 섹션이 렌더링되면 서명 가능한 양식의 PDF 버전이 표시됩니다. 일반적으로 양식의 마지막 섹션 또는 끝에서 요약 구성 요소입니다.

## 문제 해결 {#troubleshoot}

### Adobe Sign 합의 실패 {#adobe-sign-agreement-failures}

**문제**&#x200B;적응형 양식에 대해 Adobe Sign 서비스가 구성된 경우 서비스가 기본 적응형 양식에 대한 Adobe Sign 계약을 만들지 못합니다.

**해상도**

* 적응형 양식에 사용된 Adobe Sign 클라우드 서비스 [](../../forms/using/adobe-sign-integration-adaptive-forms.md) 구성을 확인합니다.
* Adobe Sign 클라우드 서비스를 구성하는 데 사용된 Adobe Sign 서버의 API 응용 프로그램에 필요한 권한이 있는지 확인하십시오.
* 여러 Adobe Sign 클라우드 서비스를 사용하는 경우 모든 서비스의 **[!UICONTROL oAuth URL]** 을 동일한 **[!UICONTROL Adobe Sign 샤드]**&#x200B;로 가리킵니다.

* 별도의 이메일 주소를 사용하여 Adobe Sign 계정, 첫 번째 서명자 및 단일 서명자에 대해 구성합니다. 첫 번째 서명자의 이메일 주소 또는 유일한 서명자(단일 서명자의 경우)는 AEM cloud services 구성에 사용되는 Adobe Sign 계정과 동일하지 않습니다.

## 관련 문서 {#related-articles}

* [Adobe Sign과 AEM Forms 통합](../../forms/using/adobe-sign-integration-adaptive-forms.md)
* [적응형 양식에서 Adobe Sign 사용](../../forms/using/working-with-adobe-sign.md)

* [AEM Forms과 Adobe Sign 사용(비디오)
   ](https://helpx.adobe.com/experience-manager/kt/forms/using/adobe-sign-integration-feature-video.html)
