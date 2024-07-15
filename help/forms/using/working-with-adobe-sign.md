---
title: 적응형 양식에서 Adobe Sign 사용
description: 적응형 양식용 전자 서명(Adobe Sign) 워크플로우를 사용하여 서명 워크플로우를 자동화하고, 단일 및 다중 서명 프로세스를 간소화하며, 모바일 장치에서 양식에 전자적으로 서명할 수 있습니다.
contentOwner: khsingh
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
feature: Adaptive Forms,Foundation Components,Acrobat Sign
discoiquuid: f79828d8-2230-4477-8ffa-eeb6a0413acd
docset: aem65
exl-id: a8decba9-229d-40a2-992a-3cc8ebefdd6d
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '3875'
ht-degree: 1%

---

# 적응형 양식에서 [!DNL Adobe Sign] 사용{#using-adobe-sign-in-an-adaptive-form}

<span class="preview"> [새 적응형 양식 만들기](/help/forms/using/create-an-adaptive-form-core-components.md) 또는 [AEM Sites 페이지에 적응형 양식 추가](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md) 작업을 할 때 현대적이고 확장 가능한 데이터 캡처 [핵심 구성 요소](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html)를 사용하는 것이 좋습니다. 이러한 구성 요소는 적응형 양식 만들기 작업이 대폭 개선되어 우수한 사용자 경험을 보장할 수 있게 되었음을 나타냅니다. 이 문서에서는 기초 구성 요소를 사용하여 적응형 양식을 작성하는 이전 접근법에 대해 설명합니다. </span>

| 버전 | 문서 링크 |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [여기 클릭](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/use-adobe-sign/working-with-adobe-sign.html) |
| AEM 6.5 | 이 문서 |


[!DNL Adobe Sign]은(는) 적응형 양식용 전자 서명 워크플로를 사용합니다. 전자 서명은 법무, 판매, 급여, 인사 관리 등의 분야에서 문서를 처리하는 워크플로를 개선합니다.

일반적인 [!DNL Adobe Sign] 및 적응형 양식 시나리오에서 사용자는 서비스에 적용할 적응형 양식에 정보를 입력합니다. 예를 들어, 모기지 및 신용 카드 신청에는 모든 차입자 및 공동 신청자의 법적 서명이 필요합니다. 유사한 시나리오에 전자 서명 워크플로를 사용하려면 [!DNL Adobe Sign]을(를) AEM [!DNL Forms]과(와) 통합할 수 있습니다. 몇 가지 예가 더 있습니다. [!DNL Adobe Sign]을(를) 사용하여 다음을 수행할 수 있습니다.

* 제안, 견적 및 계약 프로세스가 완전히 자동화된 모든 장치에서 거래를 성사시킵니다.
* 인적 자원 프로세스를 보다 빠르게 완료하고 직원에게 디지털 환경을 제공하십시오.
* 계약 주기 시간을 단축하고 공급업체를 더 빨리 온보딩하십시오.
* 일반적인 프로세스를 자동화하는 디지털 워크플로를 만듭니다.

AEM [!DNL Forms]과(와) [!DNL Adobe Sign] 통합은 다음을 지원합니다.

* 단일 및 다중 사용자 서명 워크플로
* 순차 및 동시 서명 워크플로
* 양식 내 및 양식 외 서명 경험
* 양식을 익명 또는 로그인한 사용자로 서명
* 동적 서명 프로세스(AEM [!DNL Forms] 워크플로우와 통합)
* 기술 자료, 전화 및 소셜 프로필을 통한 인증

[적응형 양식과 Adobe Sign을 사용하는 모범 사례](https://medium.com/adobetech/using-adobe-sign-to-e-sign-an-adaptive-form-heres-the-best-way-to-do-it-dc3e15f9b684)를 학습하여 더 나은 서명 경험을 만드십시오.

## 사전 요구 사항 {#prerequisites}

적응형 양식에서 [!DNL Adobe Sign]을(를) 사용하기 전에:

* AEM [!DNL Forms] 클라우드 서비스가 [!DNL Adobe Sign]을(를) 사용하도록 구성되어 있는지 확인하십시오. 자세한 내용은 [Adobe Sign과 AEM Forms 통합](../../forms/using/adobe-sign-integration-adaptive-forms.md)을 참조하십시오.
* 서명자 목록을 준비하십시오. 서명자마다 최소한 이메일 주소가 필요합니다.

## 적응형 양식에 대해 [!DNL Adobe Sign] 구성 {#configure-adobe-sign-for-an-adaptive-form}

적응형 양식에 대해 [!DNL Adobe Sign]을(를) 구성하려면 다음 단계를 수행하십시오.

1. [Adobe 기호에 대한 적응형 양식 속성 편집](../../forms/using/working-with-adobe-sign.md#enableadobesign)
1. [적응형 양식에 Adobe Sign 필드 추가](../../forms/using/working-with-adobe-sign.md#addadobesignfieldstoanadaptiveform)
1. [적응형 양식에 Adobe Sign 활성화](../../forms/using/working-with-adobe-sign.md#enableadobsignforanadaptiveform)
1. [적응형 양식에 대한 Adobe Sign Cloud Service 선택](../../forms/using/working-with-adobe-sign.md#selectadobesigncloudserviceforanadaptiveform)

1. [적응형 양식에 Adobe Sign 서명자 추가](../../forms/using/working-with-adobe-sign.md#addsignerstoanadaptiveform)
1. [적응형 양식에 대한 제출 액션 선택](../../forms/using/working-with-adobe-sign.md#selectsubmitactionforanadaptiveform)

![서명자 세부 정보](assets/signer_details_new.png)

### [!DNL Adobe Sign]에 대한 적응형 양식 속성 편집 {#enableadobesign}

기존 또는 새 적응형 양식에 대해 [!DNL Adobe Sign]에 대한 적응형 양식 속성을 구성하십시오.

[Adobe Sign용 적응형 양식을 만들기](../../forms/using/working-with-adobe-sign.md#create-an-adaptive-form-for-adobe-sign)에서는 기본 적응형 양식을 만드는 단계를 설명합니다. 적응형 양식을 만드는 동안 사용할 수 있는 기타 옵션은 [적응형 양식 만들기](../../forms/using/creating-adaptive-form.md)를 참조하십시오.

#### [!DNL Adobe Sign]에 대한 적응형 양식 만들기 {#create-an-adaptive-form-for-adobe-sign}

서명 사용 적응형 양식을 만들려면 다음 단계를 수행하십시오.

1. **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms 및 문서]**&#x200B;로 이동합니다.
1. **[!UICONTROL 만들기]**&#x200B;를 선택하고 **[!UICONTROL 적응형 양식]**&#x200B;을 선택하세요. 템플릿 목록이 나타납니다. 템플릿을 선택하고 **[!UICONTROL 다음]**&#x200B;을(를) 선택합니다.
1. **[!UICONTROL 기본]** 탭에서:

   1. 적응형 양식에 대해 **[!UICONTROL 이름]** 및 **[!UICONTROL 제목]**&#x200B;을 지정하십시오.

   1. AEM [!DNL Forms]을(를) 사용하여 [!DNL Adobe Sign]을(를) 구성하는 동안 만든 [구성 컨테이너](../../forms/using/adobe-sign-integration-adaptive-forms.md#configure-adobe-sign-with-aem-forms)을(를) 선택하십시오.

      >[!NOTE]
      >
      >**[!UICONTROL Adobe Sign Cloud Service]** 드롭다운 목록에는 이 필드에서 선택한 구성 컨테이너에 구성된 클라우드 서비스가 표시됩니다. **[!UICONTROL Adobe Sign Cloud Service 사용]** 옵션을 선택하면 적응형 양식 속성의 **[!UICONTROL 전자 서명]** 섹션에서 **[!UICONTROL Adobe Sign]** 드롭다운 목록을 사용할 수 있습니다.

1. **[!UICONTROL 양식 모델]** 탭에서 다음 옵션 중 하나를 선택합니다.

   * **[!UICONTROL 양식 서식 파일을 기록 문서 서식 파일로 연결]** 옵션을 선택하고 기록 문서 서식 파일을 선택하십시오. 양식 템플릿 기반 적응형 양식을 사용하는 경우 서명을 위해 전송된 문서에 관련 양식 템플릿을 기반으로 하는 필드만 표시됩니다. 적응형 양식의 모든 필드가 표시되지는 않습니다.

   * **[!UICONTROL 기록 문서 생성]** 옵션을 선택하십시오. 기록 문서 옵션 사용 적응형 양식을 사용하는 경우 서명을 위해 전송된 문서에 적응형 양식의 모든 필드가 표시됩니다.

1. **[!UICONTROL 만들기를 선택합니다.]** 기호 사용 적응형 양식이 만들어져 [!DNL Adobe Sign] 필드를 추가하는 데 사용할 수 있습니다.

#### [!DNL Adobe Sign]에 대한 적응형 양식 편집 {#editafsign}

기존 적응형 양식에서 [!DNL Adobe Sign]을(를) 사용하려면 다음 단계를 수행하십시오.

1. **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms 및 문서]**&#x200B;로 이동합니다.
1. 적응형 양식을 선택하고 **[!UICONTROL 속성]**&#x200B;을 선택합니다.
1. **[!UICONTROL 기본]** 탭에서 AEM [!DNL Forms]을(를) 사용하여 [!DNL Adobe Sign]을(를) 구성하는 동안 만든 [구성 컨테이너](../../forms/using/adobe-sign-integration-adaptive-forms.md#configure-adobe-sign-with-aem-forms)을(를) 선택합니다.
1. **[!UICONTROL 양식 모델]** 탭에서 다음 옵션 중 하나를 선택합니다.

   * **[!UICONTROL 양식 서식 파일을 기록 문서 서식 파일로 연결]** 옵션을 선택하고 기록 문서 서식 파일을 선택하십시오. 양식 템플릿 기반 적응형 양식을 사용하는 경우 서명을 위해 전송된 문서에 관련 양식 템플릿을 기반으로 하는 필드만 표시됩니다. 적응형 양식의 모든 필드가 표시되지는 않습니다.

   * **[!UICONTROL 기록 문서 생성]** 옵션을 선택하십시오. 기록 문서 옵션 사용 적응형 양식을 사용하는 경우 서명을 위해 전송된 문서에 적응형 양식의 모든 필드가 표시됩니다.

1. **[!UICONTROL 저장 및 닫기]**&#x200B;를 선택합니다. [!DNL Adobe Sign]에 대해 적응형 양식을 사용할 수 있습니다.

### 적응형 양식에 Adobe Sign 필드 추가 {#addadobesignfieldstoanadaptiveform}

[!DNL Adobe Sign]에는 적응형 양식에 배치할 수 있는 다양한 필드가 있습니다. 이러한 필드에는 서명, 이니셜, 회사 또는 제목과 같은 다양한 유형의 데이터가 허용되며 서명과 함께 서명 중에 추가 정보를 수집하는 데 도움이 됩니다. [!DNL Adobe Sign] 블록 구성 요소를 사용하여 적응형 양식의 다양한 위치에 [!DNL Adobe Sign] 필드를 배치할 수 있습니다.

다음 단계를 수행하여 적응형 양식에 필드를 추가하고 이러한 필드와 관련된 다양한 옵션을 사용자 지정합니다.

1. 구성 요소 브라우저에서 **[!UICONTROL Adobe Sign 블록]** 구성 요소를 적응형 양식으로 드래그 앤 드롭하십시오. [!DNL Adobe Sign] 블록 구성 요소에 지원되는 모든 [!DNL Adobe Sign] 필드가 있습니다. 기본적으로 적응형 양식에 **서명** 필드를 추가합니다.

   ![블록 서명](assets/sign_block_new.png)

   기본적으로 [!DNL Adobe Sign] 블록은 게시된 적응형 양식에 표시되지 않습니다. 서명 문서에만 표시됩니다. [!DNL Adobe Sign] 블록 구성 요소의 속성에서 [!DNL Adobe Sign] 블록의 가시성을 변경할 수 있습니다.

   >[!NOTE]
   >
   >    * 적응형 양식에서 [!DNL Adobe Sign]을(를) 사용하려면 [!DNL Adobe Sign] 블록을 사용해야 하는 것은 아닙니다. [!DNL Adobe Sign] 블록을 사용하지 않고 서명자를 위한 필드를 추가하는 경우 서명 문서 하단에 기본 서명 필드가 표시됩니다.
   >    * 기록 문서를 자동으로 생성하는 적응형 양식에만 [!DNL Adobe Sign] 블록을 사용하십시오. 기록 문서 또는 양식 템플릿 기반 적응형 양식을 생성하는 데 사용자 지정 XDP를 사용하는 경우 [!DNL Adobe Sign] 블록이 지원되지 않습니다.
   >
   >

1. **[!UICONTROL Adobe Sign 블록]** 구성 요소를 선택하고 **편집** ![aem_6_3_edit](assets/aem_6_3_edit.png) 아이콘을 선택합니다. 필드를 추가하고 필드의 형식 지정을 지정하는 옵션을 표시합니다.

   ![adobe-sign-block-select-fields](assets/adobe-sign-block-select-fields.png)

   **A.** [!DNL Adobe Sign] 필드를 선택하고 추가하십시오. **B.** [!DNL Adobe Sign] 블록을 전체 화면 보기로 확장합니다.

1. **[!UICONTROL Adobe Sign] 필드** ![aem_6_3_adobesign](assets/aem_6_3_adobesign.png) 아이콘을 선택합니다. [!DNL Adobe Sign] 필드를 선택하고 추가하는 옵션이 표시됩니다.

   **[!UICONTROL Type]** 드롭다운 필드를 확장하여 [!DNL Adobe Sign] 필드를 선택하고 완료 ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png) 아이콘을 선택하여 [!DNL Adobe Sign] 블록에 선택한 필드를 추가합니다. **[!UICONTROL Type]** 드롭다운 필드에는 서명, 서명자 정보 및 데이터 필드 형식이 포함됩니다. [!UICONTROL Type] 드롭다운 상자에만 나열된 AEM [!DNL Forms] 지원 필드와 [!DNL Adobe Sign] 통합 [!DNL Adobe Sign] 필드에 대한 자세한 내용은 [Adobe Sign 설명서](https://helpx.adobe.com/sign/help/field-types.html)를 참조하세요.

   ![adobe-sign-block-fields-options](assets/adobe-sign-block-fields-options.png)

   필드에 고유한 이름을 입력해야 합니다. 필수 옵션을 선택하여 필드를 필수 항목으로 표시할 수도 있습니다. **[!UICONTROL 이름]** 및 **[!UICONTROL 필수]** 옵션 외에 일부 [!DNL Adobe Sign] 필드에 더 많은 옵션이 있습니다. 예: 마스크 및 여러 줄. 또한 필드가 같은 [!DNL Adobe Sign] 블록에 있는지 아니면 다른  블록에 있는지 여부에 관계없이 각 [!DNL Adobe Sign] 필드에 고유한 이름을 지정하십시오.

   드롭다운 목록에서 **[!UICONTROL 디지털 서명]**&#x200B;을(를) 선택하면 적응형 양식에 디지털 서명을 적용할 수 있습니다.

   * 클라우드 서명을 사용하여 트러스트 서비스 공급자가 호스팅하는 [디지털 ID](https://helpx.adobe.com/sign/kb/digital-certificate-providers.html)(으)로 서명하는 온라인
   * 스마트 카드, USB 토큰 또는 파일 기반 디지털 ID를 사용하여 Adobe Acrobat 또는 Reader으로 문서를 로컬로 다운로드합니다.

### 적응형 양식에 [!DNL Adobe Sign] 사용 {#enableadobsignforanadaptiveform}

기본적으로 [!DNL Adobe Sign]은(는) 적응형 양식에 사용할 수 없습니다. 활성화하려면 다음 단계를 수행하십시오.

1. 콘텐츠 브라우저에서 **[!UICONTROL 양식 컨테이너]**&#x200B;를 선택하고 **[!UICONTROL 구성]** ![구성](assets/configure.png) 아이콘을 선택합니다. 속성 브라우저를 열고 적응형 양식 컨테이너 속성을 표시합니다.
1. 속성 브라우저에서 **[!UICONTROL 전자 서명]** 아코디언을 확장하고 **[!UICONTROL Adobe Sign 사용]** 옵션을 선택합니다. 적응형 양식에 대해 [!DNL Adobe Sign]을(를) 사용합니다.

### [!DNL Adobe Sign] Cloud Service 및 서명 순서 선택 {#selectadobesigncloudserviceforanadaptiveform}

AEM [!DNL Forms]의 인스턴스에 대해 여러 [!DNL Adobe Sign] 서비스를 구성할 수 있습니다. 각 기능(인적 자원, 금융 등)별로 별도의 서비스 세트를 두는 것이 바람직하다. 서명된 문서의 추적 및 보고를 더 쉽게 만듭니다. 예를 들어, A은행에는 여러 부서가 있습니다. 문서 추적을 향상시키기 위해 각 부서에 대해 별도의 구성을 가질 수 있습니다.

한 문서에 여러 서명자가 있을 수도 있습니다. 예를 들어 신용 카드 신청서에는 여러 명의 신청자가 있을 수 있습니다. 은행은 신청서 처리를 시작하기 전에 모든 신청자의 서명을 필요로 한다. 여러 서명자 시나리오의 경우 문서를 순차적 또는 동시 순서로 서명하도록 선택할 수 있습니다.

클라우드 서비스 및 서명 순서를 선택하려면 다음 단계를 수행하십시오.

![클라우드 서비스](assets/cloud-service.png)

1. 콘텐츠 브라우저에서 **[!UICONTROL 양식 컨테이너]**&#x200B;를 선택하고 **[!UICONTROL 구성]** ![구성](assets/configure.png) 아이콘을 선택합니다. 속성 브라우저를 열고 적응형 양식 컨테이너 속성을 표시합니다.
1. 속성 브라우저에서 **[!UICONTROL 전자 서명]** 아코디언을 확장하고 **[!UICONTROL Adobe Sign 사용]** 옵션을 선택합니다. 적응형 양식에 대해 [!DNL Adobe Sign]을(를) 사용합니다.
1. 이미 구성된 [!DNL Adobe Sign] Cloud Service 목록에서 클라우드 서비스를 선택하십시오.

   **[!UICONTROL Adobe Sign Cloud Service]** 목록이 비어 있으면 [AEM Forms으로 Adobe Sign 구성](../../forms/using/adobe-sign-integration-adaptive-forms.md) 문서에 따라 서비스를 구성하십시오.

   도구 > **[!UICONTROL Cloud Service]** > **[!UICONTROL Adobe Sign]**&#x200B;의 `global` 폴더에 있는 클라우드 서비스가 드롭다운에 나열됩니다. 또한 적응형 양식을 만들 때 **[!UICONTROL 구성 컨테이너]** 필드에서 선택한 폴더에 있는 클라우드 서비스도 드롭다운에 나열됩니다.

1. **[!UICONTROL 서명자가 서명할 수 있음]** 대화 상자에서 서명 순서를 선택하십시오. [!DNL Adobe Sign]명의 가수가 순서대로 **[!UICONTROL 순차적으로]**(다른 서명자 다음으로) 또는 **[!UICONTROL 동시에]**(으)로 적응형 양식에 서명할 수 있습니다.

   서명자 한 사람이 서명할 양식을 한 번에 하나씩 순차적으로 받습니다. 서명자가 문서 서명을 완료한 후 양식이 다음 서명자에게 전송되는 방식입니다.

   동시에 여러 서명자가 한 번에 양식에 서명할 수 있습니다.

1. [적응형 양식에 서명자 추가](../../forms/using/working-with-adobe-sign.md#addsignerstoanadaptiveform) 및 완료 ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png) 아이콘을 선택하여 변경 내용을 저장합니다.


### 적응형 양식에 서명자 추가 {#addsignerstoanadaptiveform}

적응형 양식에 서명자가 한 명만 있거나 여러 명이 있을 수 있습니다. 서명자를 추가할 때 서명자에 대한 인증 세부 사항을 구성할 수도 있습니다. 폼 필러와 가수가 동일인지도 선택할 수 있다. 서명자에 대한 다양한 세부 정보를 추가하고 제공하려면 다음 단계를 수행하십시오.

1. 콘텐츠 브라우저에서 **[!UICONTROL 양식 컨테이너]**&#x200B;를 선택하고 **[!UICONTROL 구성]** ![구성](assets/configure.png) 아이콘을 선택합니다. 적응형 양식 컨테이너 속성이 있는 속성 브라우저를 엽니다.
1. 속성 브라우저에서 **[!UICONTROL 전자 서명]** 아코디언을 확장하고 **[!UICONTROL Adobe Sign 사용]** 옵션을 선택합니다. 적응형 양식에 대해 [!DNL Adobe Sign]을(를) 사용합니다.
1. **[!UICONTROL 서명자 구성]**&#x200B;에서 **[!UICONTROL 서명자 추가]**&#x200B;를 선택합니다. 적응형 양식에 서명자를 추가합니다. 적응형 양식에 여러 [!DNL Adobe Sign]명의 서명자를 추가할 수 있습니다.
   ![전화 정보](assets/phone-details.png)

1. 서명자에 대해 다음 정보를 지정하려면 **편집** ![aem_6_3_편집](assets/aem_6_3_edit.png) 아이콘을 클릭하십시오.

   * **[!UICONTROL 제목]:** 서명자를 고유하게 식별하는 제목을 지정합니다.

   * **[!UICONTROL 서명자와 양식 작성자가 동일합니까?]:** 양식 작성자와 첫 번째 서명자가 같은 사람인 경우 **예**&#x200B;를 선택합니다. 옵션이 **아니요,**(으)로 설정된 경우 적응형 양식에서 서명 단계 구성 요소를 사용하지 마십시오. 양식에 서명 단계 구성 요소가 포함되어 있으면 필드가 자동으로 예로 설정됩니다.

   * **[!UICONTROL 서명자 전자 메일 주소]:** 서명자의 전자 메일 주소를 지정합니다. 서명자는 지정된 이메일 주소에 서명된 문서/양식을 수신합니다. 양식 필드, 로그인한 사용자의 AEM 사용자 프로필에 제공된 이메일 주소를 사용하도록 선택하거나 이메일 주소를 수동으로 입력할 수 있습니다. 필수 단계입니다. 첫 번째 서명자 또는 유일한 서명자(단일 서명자가 있는 경우)의 전자 메일 주소가 AEM Cloud Services 구성에 사용된 [!DNL Adobe Sign] 계정과 동일하지 않은지 확인하십시오.

   * **[!UICONTROL 서명자 인증 방법]:** 서명할 양식을 열기 전에 사용자를 인증할 방법을 지정하십시오. 전화, 기술 자료 및 소셜 ID 기반 인증 중에서 선택할 수 있습니다. Adobe Acrobat Sign Solutions for Government의 경우 전화 및 지식 기반 인증 옵션만 사용할 수 있습니다.

   >[!NOTE]
   >
   >    * 기본적으로 소셜 ID 기반 인증은 Facebook, Google 및 LinkedIn을 사용하여 인증할 수 있는 옵션을 제공합니다. [!DNL Adobe Sign] 지원팀에 연락하여 다른 소셜 인증 공급자를 사용하도록 설정할 수 있습니다.
   >
   >

   * 입력하거나 서명할 필드 **[!DNL Adobe Sign]개:** 서명자의 필드 [!DNL Adobe Sign]개를 선택하십시오. 적응형 양식에는 여러 [!DNL Adobe Sign]개의 필드가 있을 수 있습니다. 서명자에 대해 특정 필드를 활성화하도록 선택할 수 있습니다. 필드에 사용 가능한 모든 [!DNL Adobe Sign] 블록이 표시됩니다. 블록을 선택하면 블록의 모든 필드가 선택됩니다. X 아이콘을 사용하여 필드를 선택 취소할 수 있습니다.

   ![서명자-세부 정보](assets/signer-details.png)

   위의 이미지에는 [!DNL Adobe Sign] 블록의 두 가지 예가 있습니다. 개인 정보 및 Office 세부 정보

   완료 ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png) 아이콘을 선택합니다. 서명자가 추가되고 구성됩니다.

### 적응형 양식에 대한 제출 액션 선택 {#selectsubmitactionforanadaptiveform}

적응형 양식에 [!DNL Adobe Sign] 필드를 추가하고, 양식 컨테이너에서 [!DNL Adobe Sign]을(를) 활성화하고, [!DNL Adobe Sign] Cloud Service을 선택하고, [!DNL Adobe Sign] 서명자를 추가한 후 적응형 양식에 적절한 제출 액션을 선택하십시오. 적응형 양식 제출 액션에 대한 자세한 내용은 [제출 액션 구성](../../forms/using/configuring-submit-actions.md)을 참조하세요.

또한 [!DNL Adobe Sign] 사용 적응형 양식은 모든 서명자가 양식에 서명한 후에만 제출됩니다. 양식 포털의 대기 중 서명 섹션에서 부분적으로 서명된 양식을 찾을 수 있습니다. [!DNL Adobe Sign] 구성 서비스에서 [!DNL Adobe Sign] 서버를 [일정 간격](../../forms/using/adobe-sign-integration-adaptive-forms.md)으로 폴링하여 서명 상태를 확인합니다. 모든 서명자가 양식 서명을 완료하면 제출 액션 서비스가 시작되고 양식이 제출된다. 사용자 지정 제출 액션을 사용 중이며 양식에서 [!DNL Adobe Sign]을(를) 사용하는 경우 사용자 지정 제출 액션을 업데이트하여 제출 액션 서비스를 사용하십시오.

<!-- Remove when forms portal goes live
>[!NOTE]
>
>Data of the adaptive form is stored temporarily on Forms Portal. Use [custom storage for Forms Portal](/help/forms/using/configuring-draft-submission-storage.md). It ensures that the PII (personally identifiable information) data is not stored on AEM servers. 
-->

양식 서명 경험이 준비되었습니다. 양식을 미리 보고 서명 환경을 확인할 수 있습니다. 서명자가 전자 메일을 통해 서명할 양식을 받을 때 게시된 양식에 [!DNL Adobe Sign] 블록 필드가 표시됩니다. 이 경험을 양식 외 서명 경험이라고도 합니다. 첫 번째 서명자의 양식 내 서명 환경을 구성할 수도 있습니다. 자세한 단계는 [양식 내 서명 환경 만들기](../../forms/using/working-with-adobe-sign.md#create-in-form-signing-experience)를 참조하십시오.

## 적응형 양식에 대한 클라우드 서명 구성 {#configure-cloud-signatures-for-an-adaptive-form}

클라우드 기반 디지털 서명 또는 원격 서명은 데스크탑, 모바일 및 웹에서 작동하는 새로운 세대의 디지털 서명으로, 서명자 인증을 위한 최고 수준의 규정 준수 및 보증을 충족합니다. 클라우드 기반 디지털 서명을 사용하여 적응형 양식에 서명할 수 있습니다.

[Adobe 서명에 대한 적응형 양식 속성을 편집](../../forms/using/working-with-adobe-sign.md#enableadobesign)한 후 다음 단계를 수행하여 적응형 양식에 클라우드 서명 필드를 추가하십시오.

1. 구성 요소 브라우저에서 **[!UICONTROL Adobe Sign 블록]** 구성 요소를 적응형 양식으로 드래그 앤 드롭하십시오. [!UICONTROL Adobe Sign 블록] 구성 요소에 지원되는 모든 [!DNL Adobe Sign] 필드가 있습니다. 기본적으로 적응형 양식에 **[!UICONTROL 서명]** 필드를 추가합니다.

   ![블록 서명](assets/sign-block-new.png)

1. **[!UICONTROL Adobe Sign 블록]** 구성 요소를 선택하고 **편집** ![aem_6_3_edit](assets/aem_6_3_edit.png) 아이콘을 선택합니다. 필드를 추가하고 필드의 형식 지정을 지정하는 옵션을 표시합니다.

   ![adobe-sign-block-select-fields](assets/adobe-sign-block-select-fields.png)

   **A.** [!DNL Adobe Sign] 필드를 선택하고 추가하십시오. **B.** [!DNL Adobe Sign] 블록을 전체 화면 보기로 확장합니다.

1. **[!UICONTROL Adobe Sign 필드]** ![aem_6_3_adobesign](assets/aem_6_3_adobesign.png) 아이콘을 선택합니다. [!DNL Adobe Sign] 필드를 선택하고 추가하는 옵션이 표시됩니다.

   **[!UICONTROL 유형]** 드롭다운 필드를 확장하여 **[!UICONTROL 디지털 서명]**&#x200B;을(를) 선택하고 **완료** 아이콘을 선택하여 [!DNL Adobe Sign] 블록에 선택한 필드를 추가합니다.

   ![디지털 서명](assets/digital_signatures_new.png)

   필드에 고유한 이름을 입력해야 합니다.

   다음을 사용하여 적응형 양식에 디지털 서명 적용:

   * 클라우드 서명: 트러스트 서비스 공급자가 호스팅하는 [디지털 ID](https://helpx.adobe.com/sign/kb/digital-certificate-providers.html)로 서명합니다. Adobe Acrobat Sign Solutions for Government에서는 클라우드 서명 옵션을 사용할 수 없습니다.

   * Adobe Acrobat 또는 Reader: Adobe Acrobat 또는 Reader으로 문서를 다운로드하여 열고 스마트 카드, USB 토큰 또는 파일 기반 디지털 ID를 사용하여 서명합니다.

   클라우드 서명 필드를 적응형 양식에 추가한 후 다음 단계를 수행하여 구성 프로세스를 완료합니다.

   * [적응형 양식에 Adobe Sign 활성화](../../forms/using/working-with-adobe-sign.md#enableadobsignforanadaptiveform)
   * [적응형 양식에 대한 Adobe Sign Cloud Service 선택](../../forms/using/working-with-adobe-sign.md#selectadobesigncloudserviceforanadaptiveform)
   * [적응형 양식에 Adobe Sign 서명자 추가](../../forms/using/working-with-adobe-sign.md#addsignerstoanadaptiveform)
   * [적응형 양식에 대한 제출 액션 선택](../../forms/using/working-with-adobe-sign.md#selectsubmitactionforanadaptiveform)

## 양식 내 서명 경험 만들기 {#create-in-form-signing-experience}

사용자는 양식을 작성하는 동안 적응형 양식에 서명할 수도 있습니다. 이 경험을 양식 내 서명 경험이라고도 합니다. 인폼 서명 경험은 다중 서명자 환경의 첫 번째 가수에게만 가능하다. 적응형 양식에 대한 양식 내 서명 경험을 만들려면 다음 단계를 수행하십시오.

1. [서명 단계 구성 요소를 추가하고 구성합니다](../../forms/using/working-with-adobe-sign.md#add-and-configure-the-signature-step-component).
1. [요약 단계 구성 요소를 추가](../../forms/using/working-with-adobe-sign.md#configure-the-thank-you-page-or-summary-step-component)합니다.

![양식 내 서명 환경](assets/in_form_signing_experience_new.png)

### 서명 단계 구성 요소 추가 및 구성 {#add-and-configure-the-signature-step-component}

서명 단계 구성 요소를 사용하여 채워진 양식에 전자적으로 서명할 영역을 제공합니다. 서명 단계 구성 요소가 포함된 섹션이 렌더링되면 작성된 양식의 서명 가능한 PDF 버전을 표시합니다. 서명 단계 구성 요소는 양식에 사용할 수 있는 전체 너비를 차지합니다. 서명 단계 구성 요소가 포함된 섹션에는 다른 구성 요소가 없는 것이 좋습니다.

서명 단계 구성 요소를 구성하려면 다음 단계를 수행하십시오.

1. 구성 요소 브라우저에서 **[!UICONTROL 서명 단계]** 구성 요소를 양식으로 드래그 앤 드롭합니다.
1. 새로 추가된 서명 단계 구성 요소를 선택하고 **구성** ![구성](assets/configure.png) 아이콘을 선택합니다. 속성 브라우저를 열고 서명 단계 속성을 표시합니다. 다음 속성을 구성합니다.

   * **[!UICONTROL 이름]**: 구성 요소의 이름을 지정하십시오.

   * **[!UICONTROL 제목]:** 구성 요소의 고유한 제목을 지정합니다.
   * **[!UICONTROL 템플릿 메시지]:** 서명 PDF을 로드하는 동안 표시할 메시지를 지정합니다. [!DNL Adobe Sign]개의 서비스에서 서명 PDF을 준비하고 로드하는 데 시간이 좀 걸립니다.
   * **[!UICONTROL 서명 서비스]:** **[!DNL Adobe Sign]** 옵션을 선택하십시오.

   * **[!UICONTROL 기존 전자 서명 구성 요소 사용]**: [AEM Forms Workspace](../../forms/using/introduction-html-workspace.md), AEM [!DNL Forms] 앱에서 각 적응형 양식을 사용하거나 기본 적응형 양식에 기존 전자 서명 구성 요소가 있는 경우 **기존 전자 서명 구성 요소 사용** 옵션을 선택하십시오.

   * **[!UICONTROL 구성]**: 구성([!DNL Adobe Sign] Cloud Service)을 선택하십시오. 드롭다운 상자는 **기존 전자 서명 구성 요소 사용** 옵션이 활성화된 경우에만 사용할 수 있습니다.

   * **[!UICONTROL CSS 클래스]**: 구성 요소의 CSS 클래스를 지정합니다.

   완료 ![aem_6_3_forms_save](assets/aem_6_3_forms_save.png) 아이콘을 선택하여 변경 사항을 저장합니다.

   ![서명 단계](assets/signature_step_new.png)

   >[!NOTE]
   >
   >* **[!UICONTROL 서명 단계]** 구성 요소를 양식으로 드래그 앤 드롭하면 **[!UICONTROL 서명자와 양식을 작성하는 사람이 동일합니까?]** 옵션이 자동으로 **예**(으)로 설정됩니다. 양식 작동을 유지하는 것이 필요합니다.
   >* 최상의 경험을 위해 서명 단계 구성 요소 뒤에 요약 단계 구성 요소를 사용하십시오. 요약 단계는 서명 단계 구성 요소에서 양식 서명을 완료한 후 자동으로 즉시 양식을 제출합니다. 요약 단계를 사용하지 않으면 [Adobe Sign 구성 서비스](../../forms/using/adobe-sign-integration-adaptive-forms.md#configure-adobe-sign-scheduler-to-sync-the-signing-status)를 사용하여 설정된 간격 이후에만 자동 제출이 트리거됩니다.
   >
   >몇 가지 모범 사례는 다음과 같습니다.
   >
   >* 서명 단계가 포함된 적응형 양식 패널은 항상 적응형 양식의 마지막 또는 마지막 두 번째 패널에 있습니다. 마지막 패널에 요약 단계가 포함된 경우에만 두 번째 마지막 패널일 수 있습니다.
   >* 서명 또는 요약 단계 구성 요소가 포함된 패널에는 다른 구성 요소를 포함할 수 없습니다.
   >* 서명 단계가 포함된 적응형 양식에는 제출 단추를 사용할 수 없습니다.
   >* 서명 단계를 포함하는 적응형 양식에 대한 제출은 백그라운드 서비스 또는 요약 단계를 통해 처리됩니다. 양식을 작성하는 구성된 서명자가 한 명 있는 경우 요약 단계를 사용하여 적응형 양식 제출을 처리할 때 서명자가 양식에 서명했음을 즉시 평가하고 제출 작업을 호출한다는 이점이 있습니다. 백그라운드 서비스는 구성된 모든 서명자가 양식에 서명했는지 여부를 평가하는 데 더 많은 시간이 소요되고 적응형 양식의 제출을 지연시킵니다.
   >* 사용자가 서명 또는 요약 단계가 포함된 패널에서 다시 탐색할 수 없도록 양식을 디자인합니다.


### 감사 페이지 또는 요약 단계 구성 요소 구성 {#configure-the-thank-you-page-or-summary-step-component}

**요약 단계** 구성 요소는 자동으로 양식을 제출하고 사용자 지정된 요약 페이지 내에 정보를 입력한 다음 제출된 양식의 요약을 표시합니다. 또한 반환 맵에 필요한 정보를 가져옵니다. 요약 단계 구성 요소는 양식에 사용할 수 있는 전체 폭을 차지합니다. 요약 단계 구성 요소가 포함된 섹션에는 다른 구성 요소가 없는 것이 좋습니다.

이제 양식 서명 경험의 가 준비되었습니다. 양식을 미리 보고 서명 환경을 확인할 수 있습니다.

## 자주 묻는 질문 {#frequently-asked-questions}

**Q:** 적응형 양식을 다른 적응형 양식에 포함할 수 있습니다. 임베드된 적응형 양식을 [!DNL Adobe Sign] 활성화할 수 있습니까?
**Ans:** 아니요, AEM [!DNL Forms]에서는 서명을 위해 [!DNL Adobe Sign]이(가) 활성화된 적응형 양식을 임베드하는 적응형 양식 사용을 지원하지 않습니다.

**Q:** 고급 템플릿을 사용하여 적응형 양식을 만들고 편집하기 위해 열면 &quot;전자 서명 또는 서명자가 올바르게 구성되지 않았습니다.&quot;라는 오류 메시지가 표시됩니다. 가 표시됩니다. 오류 메시지를 해결하는 방법
고급 템플릿을 사용하여 만든 **Ans:** 적응형 양식이 [!DNL Adobe Sign]을(를) 사용하도록 구성되어 있습니다. 오류를 해결하려면 [!DNL Adobe Sign] 클라우드 구성을 만들고 선택한 다음 적응형 양식에 대해 [!DNL Adobe Sign] 서명자를 구성하십시오.

**Q:** 적응형 양식의 정적 텍스트 구성 요소에서 [!DNL Adobe Sign] 텍스트 태그를 사용할 수 있습니까?
**Ans:** 예, 텍스트 구성 요소의 텍스트 태그를 사용하여 [!DNL Adobe Sign] 필드를 [기록 문서](../../forms/using/generate-document-of-record-for-non-xfa-based-adaptive-forms.md)(자동 생성된 기록 문서 옵션만 해당) 사용 적응형 양식에 추가할 수 있습니다. 텍스트 태그를 만드는 절차 및 규칙에 대해 알아보려면 [Adobe Sign 설명서](https://helpx.adobe.com/sign/using/text-tag.html)를 참조하세요. 또한 적응형 양식에는 텍스트 태그에 대한 지원이 제한되어 있습니다. 텍스트 태그를 사용하여 [Adobe Sign 블록](../../forms/using/working-with-adobe-sign.md#configure-cloud-signatures-for-an-adaptive-form)에서 지원하는 필드만 만들 수 있습니다.

**Q:** AEM [!DNL Forms]은(는) [!UICONTROL Adobe Sign 블록] 및 서명 단계 구성 요소를 모두 제공합니다. 적응형 양식에서 이러한 코드를 동시에 사용할 수 있습니까?
**Ans:** 양식에서 두 구성 요소를 동시에 사용할 수 있습니다. 다음은 이러한 구성 요소 사용에 대한 몇 가지 권장 사항입니다.

**Adobe Sign 블록:** [!UICONTROL Adobe Sign 블록]을(를) 사용하여 적응형 양식의 어디에나 [!UICONTROL Adobe Sign] 필드를 추가할 수 있습니다. 서명자에게 특정 필드를 할당하는 데도 도움이 됩니다. 적응형 양식을 미리 보거나 게시할 때 기본적으로 [!UICONTROL Adobe Sign] 블록이 표시되지 않습니다. 이러한 블록은 서명 문서에서만 활성화됩니다. 서명 문서에서는 서명자에게 지정된 필드만 활성화됩니다. [!UICONTROL Adobe Sign] 블록은 첫 번째 및 후속 서명자와 함께 사용할 수 있습니다.

**서명 단계 구성 요소:** 서명 단계 구성 요소를 사용하여 양식 내 서명 환경을 만들 수 있습니다. 양식을 작성하는 동안 첫 번째 서명자만 서명할 수 있습니다. 서명 단계 구성 요소가 포함된 섹션이 렌더링되면 서명 가능한 양식 PDF 버전이 표시됩니다. 일반적으로 양식의 요약 구성 요소 다음에 오는 마지막 또는 마지막 섹션입니다.

## 문제 해결 {#troubleshoot}

### [!DNL Adobe Sign]개 계약 실패 {#adobe-sign-agreement-failures}

**문제**
[!DNL Adobe Sign] 서비스가 적응형 양식에 대해 구성된 경우, 기본 적응형 양식에 대해 [!DNL Adobe Sign] 계약을 만들지 못했습니다.

**해결**

* 적응형 양식에 사용된 [Adobe Sign 클라우드 서비스 구성](../../forms/using/adobe-sign-integration-adaptive-forms.md)을 확인하십시오.
* [!DNL Adobe Sign] 클라우드 서비스를 구성하는 데 사용되는 [!DNL Adobe Sign] 서버의 API 응용 프로그램에 필요한 권한이 있는지 확인하십시오.
* 여러 [!DNL Adobe Sign] 클라우드 서비스를 사용하는 경우 모든 서비스의 **[!UICONTROL oAuth URL]**&#x200B;을(를) 동일한 **[!UICONTROL Adobe Sign Shard]**(으)로 지정합니다.

* [!DNL Adobe Sign] 계정 및 첫 번째 서명자 및 단일 서명자에 대해 별도의 전자 메일 주소를 사용하여 구성하십시오. 첫 번째 서명자 또는 유일한 서명자(단일 서명자가 있는 경우)의 전자 메일 주소는 AEM Cloud Services 구성에 사용된 [!DNL Adobe Sign] 계정과 같을 수 없습니다.

### [!DNL Adobe Sign] 사용 적응형 양식에 대해 구성된 AEM [!DNL Forms] 워크플로가 시작되지 않습니다 {#adobe-sign-aem-form-workflow-failures}

**문제**
[!DNL Adobe Sign]이(가) 적응형 양식에 대해 구성된 경우 [!DNL Forms] 워크플로 호출 옵션을 사용하여 구성된 워크플로가 시작되지 않습니다.

**해결**

* 서명 단계 없이 [!DNL Adobe Sign]을(를) 사용하거나 양식에 여러 사람의 서명이 필요한 경우, AEM [!DNL Forms] 서버는 스케줄러가 모든 사람이 양식에 서명했는지 확인할 때까지 기다립니다. 모든 사람이 서명을 완료한 후에만 스케줄러가 적응형 양식을 제출하고 적응형 양식을 성공적으로 제출한 후에만 워크플로가 시작됩니다. [스케줄러](adobe-sign-integration-adaptive-forms.md)의 간격을 짧게 설정하여 빠른 간격으로 양식 서명 상태를 확인하고 양식 제출을 고정할 수 있습니다.


## 관련 문서 {#related-articles}

* [Adobe Sign과 AEM Forms 통합](../../forms/using/adobe-sign-integration-adaptive-forms.md)
* [적응형 양식과 Adobe Sign 사용에 대한 모범 사례](https://medium.com/adobetech/using-adobe-sign-to-e-sign-an-adaptive-form-heres-the-best-way-to-do-it-dc3e15f9b684)
* [AEM Forms에서 Adobe Sign 사용(비디오)](https://helpx.adobe.com/experience-manager/kt/forms/using/adobe-sign-integration-feature-video.html)
