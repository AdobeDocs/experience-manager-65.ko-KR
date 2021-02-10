---
title: 적응형 양식을 만드는 방법
description: ' [!DNL Experience Manager Forms]을(를) 사용하여 적응형 양식을 만드는 방법을 알아봅니다. 적응형 양식은 정보 수집 및 처리를 간소화하는 반응형 HTML5 양식입니다. 양식 데이터 모델, XFA 양식 템플릿, XML 또는 JSON 스키마를 기반으로 적응형 양식을 만드는 방법에 대해 자세히 살펴봅니다. '
feature: Adaptive Forms
role: Business Practitioner, Developers
level: Beginner
translation-type: tm+mt
source-git-commit: 52fedc234b3edf581393bb42325902d2da3ab46e
workflow-type: tm+mt
source-wordcount: '1856'
ht-degree: 0%

---


# 응용 양식 만들기 {#creating-an-adaptive-form}

## <strong>적응형 양식 만들기</strong> {#strong-create-an-adaptive-form-strong}

적응형 양식을 만들려면 다음 단계를 수행합니다.

1. `https://'[server]:[port]'/<custom-context-if-any>.`의 작성자 인스턴스에 액세스[!DNL Experience Manager Forms]

1. Experience Manager 로그인 페이지에 자격 증명을 입력합니다.

   로그인한 후 왼쪽 위 모서리에서 **[!UICONTROL Adobe Experience Manager]** > **[!UICONTROL Forms]** > **[!UICONTROL Forms &amp; 문서]**&#x200B;를 탭합니다.

   >[!NOTE]
   >
   >기본 설치의 경우 로그인은 `admin`이고 암호는 `admin`입니다.

1. **[!UICONTROL 만들기]**&#x200B;를 누르고 **[!UICONTROL 적응형 양식]**&#x200B;을 선택합니다.
1. 템플릿을 선택하는 옵션이 나타납니다. 템플릿에 대한 자세한 내용은 [적응형 양식 템플릿](creating-adaptive-form.md#p-adaptive-form-templates-p)을 참조하십시오. 템플릿을 눌러 선택하고 다음을 누릅니다.
1. &#39;속성 추가&#39; 옵션이 나타납니다. 다음 속성 필드에 대한 값을 지정합니다. 제목 및 이름 필드는 필수입니다.

   * **[!UICONTROL 제목:]** 양식의 표시 이름을 지정합니다. 제목은 [!DNL Experience Manager Forms] 사용자 인터페이스에서 양식을 식별하는 데 도움이 됩니다.
   * **[!UICONTROL 이름:]** 양식의 이름을 지정합니다. 지정된 이름의 노드가 저장소에 생성됩니다. 제목을 입력하기 시작하면 이름 필드에 대한 값이 자동으로 생성됩니다. 제안된 값을 변경할 수 있습니다. 이름 필드에는 영숫자, 하이픈 및 밑줄만 포함할 수 있습니다. 잘못된 입력은 모두 하이픈으로 바뀝니다.
   * **[!UICONTROL 설명:]** 양식에 대한 자세한 정보를 지정합니다.
   * **[!UICONTROL 태그:]** 적응형 양식을 고유하게 식별하는 태그를 지정합니다. 태그는 양식을 검색하는 데 도움이 됩니다. 태그를 만들려면 **[!UICONTROL 태그]** 상자에 새 태그 이름을 입력합니다.

1. 다음 양식 모델 중 하나를 기반으로 적응형 양식을 만들 수 있습니다.

   * [양식 데이터 모델](#fdm)
   * [XFA 양식 템플릿](#create-an-adaptive-form-based-on-an-xfa-form-template)
   * [XML 또는 JSON 스키마](#create-an-adaptive-form-based-on-xml-or-json-schema)
   * 양식 모델 없음 또는 없음

   **[!UICONTROL 속성 추가]** 페이지의 **[!UICONTROL 양식 모델]** 탭에서 구성할 수 있습니다. 기본적으로 선택한 양식 모델은 **[!UICONTROL None]**&#x200B;입니다.

1. **[!UICONTROL 만들기]**&#x200B;를 누릅니다. 적응형 양식이 만들어지고 편집할 양식을 여는 대화 상자가 나타납니다.

   모든 속성 지정이 완료되면 **[!UICONTROL 만들기]**&#x200B;를 클릭합니다. 적응형 양식이 만들어지고 편집할 양식을 여는 대화 상자가 나타납니다.

   모든 속성 지정이 완료되면 **[!UICONTROL 만들기]**&#x200B;를 클릭합니다. 적응형 양식이 만들어지고 편집할 양식을 여는 대화 상자가 나타납니다.

1. **[!UICONTROL 열기]**&#x200B;를 눌러 새로 만든 양식을 새 탭에서 엽니다. 편집할 양식이 열리고 템플릿에 사용할 수 있는 컨텐츠가 표시됩니다. 또한 필요에 따라 새로 만든 양식을 사용자 정의하는 사이드바를 표시합니다.

   적응형 양식 유형에 따라 연결된 XFA 양식 템플릿, XML 스키마 또는 JSON 스키마에 있는 양식 요소가 사이드바의 **[!UICONTROL 컨텐츠 브라우저]**&#x200B;의 **[!UICONTROL 데이터 모델 객체]** 탭에 표시됩니다. 이러한 요소를 드래그하여 응용 양식을 만들 수도 있습니다.

   적응형 양식 작성 인터페이스 및 사용 가능한 구성 요소에 대한 자세한 내용은 [적응형 양식 작성 소개](introduction-forms-authoring.md)를 참조하십시오.

   >[!NOTE]
   >
   >브라우저의 팝업 창에서 새로 만든 양식을 새 탭에서 열 수 있습니다.

## 양식 데이터 모델 {#fdm}을 기반으로 적응형 양식 만들기

[[!DNL Experience Manager Forms] 데이터 ](data-integration.md) 통합을 통해 여러 데이터 소스를 통합하고 해당 개체 및 서비스를 함께 가져와 양식 데이터 모델을 만들 수 있습니다. JSON 스키마 확장입니다. 양식 데이터 모델을 사용하여 적응형 양식을 만들 수 있습니다. 양식 데이터 모델에 구성된 엔터티 또는 데이터 모델 개체는 양식 작성을 위한 데이터 모델 개체로 사용할 수 있습니다. 각 데이터 소스에 바인딩되고 양식을 미리 작성하고 제출된 데이터를 각 데이터 소스에 다시 쓰는 데 사용됩니다. 적응형 양식 규칙을 사용하여 양식 데이터 모델에서 구성된 서비스를 호출할 수도 있습니다.

적응형 양식을 만들기 위해 양식 데이터 모델을 사용하려면:

1. [속성 추가] 화면의 [양식 모델] 탭에서 ****&#x200B;에서 선택 드롭다운 목록에서 **[!UICONTROL 양식 데이터 모델]**&#x200B;을 선택합니다.

   ![create-af-1-1](assets/create-af-1-1.png)

1. 을 눌러 **[!UICONTROL 양식 데이터 모델 선택]**&#x200B;을 확장합니다. 사용 가능한 모든 양식 데이터 모델이 나열됩니다.

   데이터 모델에서 하나를 선택합니다.

   ![create-af-2-1](assets/create-af-2-1.png)

>[!NOTE]
>
>적응형 양식의 양식 데이터 모델을 변경할 수도 있습니다. 자세한 내용은 응용 양식](#edit-form-model)의 양식 모델 속성 편집을 참조하십시오.[

## XFA 양식 템플릿 {#create-an-adaptive-form-based-on-an-xfa-form-template}을(를) 기반으로 적응형 양식 만들기

XFA 양식 템플릿을 재사용하여 적응형 양식을 만들 수 있습니다. 용도를 변경하려면 XFA 양식 템플릿을 업로드하고 적응형 양식과 연결합니다. 양식 템플릿(XFA 양식)의 요소는 적응형 양식 작성 시 컨텐츠 파인더에서 사용할 수 있습니다. 컨텐츠 파인더에서 양식 템플릿 요소를 양식에 드래그하여 놓을 수 있습니다.

<!-- >>[!NOTE]
>
>[Upload the XFA Form Template](get-xdp-pdf-documents-aem.md) to AEM Forms before you start creating an adaptive form based on the form template.

Do the following to use an XFA form template as form model for your adaptive form:

1. On the **[!UICONTROL Add Properties]** page, open the **[!UICONTROL Form Model]** tab.
1. In the Form Model tab, from the drop-down list, select **[!UICONTROL Form Templates]**. All the form templates that are uploaded to the repository via AEM Forms UI are listed for selection. Select a template from the list.

   ![Associate XFA Form Template with an Adaptive Form](assets/form_model_xfa_associate.png)
**Figure:** *Selecting a form template*

   >[!NOTE]
   >
   >You can also change the form template for an adaptive form. For detailed steps, see [Edit Form Model properties of an adaptive form](#edit-form-model). -->

## XML 또는 JSON 스키마를 기반으로 하는 적응형 양식 만들기 {#create-an-adaptive-form-based-on-xml-or-json-schema}

XML 및 JSON 스키마는 조직의 백엔드 시스템에서 데이터를 생성하거나 사용하는 구조를 나타냅니다. 스키마를 적응형 양식에 연결하고 해당 요소를 사용하여 적응형 양식에 동적 내용을 추가할 수 있습니다. 스키마 요소는 적응형 양식을 작성하기 위해 내용 브라우저의 [데이터 모델 개체] 탭에서 사용할 수 있습니다. 스키마 요소를 끌어 놓아서 양식을 작성할 수 있습니다.

적응형 양식 작성을 위해 XML 또는 JSON 스키마를 디자인하는 방법을 이해하려면 다음 문서를 참조하십시오.

* [XML 스키마를 사용하여 적응형 양식 만들기](adaptive-form-xml-schema-form-model.md)
* [JSON 스키마를 사용하여 적응형 양식 만들기](adaptive-form-json-schema-form-model.md)

적응형 양식의 양식 모델로 XML 또는 JSON 스키마를 사용하려면 다음을 수행합니다.

1. 응용 양식 작성 페이지의 **[!UICONTROL 속성 추가]** 단계에서 **[!UICONTROL 양식 모델]** 탭을 누릅니다.
1. 양식 모델 탭의 **[!UICONTROL 다음에서]**&#x200B;에서 스키마&#x200B;]**을 선택합니다.**[!UICONTROL 

1. **[!UICONTROL 스키마 선택]**&#x200B;을 탭하고 다음 중 하나를 수행합니다.

   * **[!UICONTROL 디스크에서]**  업로드 - 이 옵션을 선택하고 스키마 정의 업로드를 눌러 파일 시스템에서 XML 스키마 또는 JSON 스키마를 검색하고 업로드합니다. 업로드된 스키마 파일은 양식과 함께 있으며 다른 적응형 양식에 액세스할 수 없습니다.
   * **[!UICONTROL 저장소에서 검색]**  - 저장소에서 사용 가능한 스키마 정의 파일 목록에서 선택하려면 이 옵션을 선택합니다. XML 또는 JSON 스키마 파일을 양식 모델로 선택합니다. 선택한 스키마는 참조별로 양식과 연결되어 있으며 다른 적응형 양식에 사용할 수 있습니다.

   >[!CAUTION]
   >
   >JSON 스키마 파일 이름이 **.schema.json**&#x200B;으로 끝나야 합니다. 예:mySchema.schema.json

   ![XML 또는 JSON 스키마 선택](assets/upload-schema.png)
   **그림:** *XML 또는 JSON 스키마 선택*

1. (XML 스키마의 경우) XML 스키마를 선택하거나 업로드한 후 선택한 XSD 파일의 루트 요소를 지정하여 적응형 양식에 매핑합니다.

   ![XSD 루트 요소 선택](assets/xsd-root-element.png)
   **그림:** *XSD 루트 요소 선택*

>[!NOTE]
>
>적응형 양식의 스키마를 변경할 수도 있습니다. 자세한 내용은 응용 양식](#edit-form-model)의 양식 모델 속성 편집을 참조하십시오.[

## 적응형 양식 템플릿 {#adaptive-form-templates}

템플릿은 기본 구조를 제공하고 응용 양식의 모양(레이아웃 및 스타일)을 정의합니다. 특정 속성 및 컨텐츠 구조를 포함하는 미리 서식이 지정된 구성 요소가 있습니다.<!-- Out of the box, AEM Forms provides some adaptive form templates. To get the complete template package including advanced templates, you need to install the AEM Forms add-on package. For more information, see [Installing AEM Forms add-on package](installing-configuring-aem-forms-osgi.md).-->

또한 템플릿 편집기를 사용하여 자신만의 템플릿을 만들 수 있습니다. 템플릿 작업에 대한 자세한 내용은 [적응형 양식 템플릿](template-editor.md)을 참조하십시오.

>[!NOTE]
>
>편집을 위해 고급 템플릿을 사용하여 만든 응용 양식을 열면 오류 메시지가 표시됩니다. 고급 템플릿에는 서명 단계 구성 요소가 있으며 Adobe Sign은 기본적으로 활성화되어 있습니다. [Adobe Sign 클라우드 구성](adobe-sign-integration-adaptive-forms.md) 및 [서명자](working-with-adobe-sign.md#addsignerstoanadaptiveform)를 만들어 선택하여 오류를 해결하십시오.

## 응용 양식 {#edit-form-model} 양식의 양식 모델 속성 편집

적응형 양식은 양식 모델 없이(양식 모델에 대해 없음 옵션 사용) 또는 양식 템플릿, XML 스키마 또는 JSON 스키마 또는 양식 데이터 모델과 같은 양식 모델을 사용하여 생성됩니다. 적응형 양식의 양식 모델을 없음에서 다른 양식 모델로 변경할 수 있습니다. 양식 모델을 기반으로 하는 적응형 양식의 경우 동일한 양식 모델에 대해 다른 양식 템플릿, XML 스키마, JSON 스키마 또는 양식 데이터 모델을 선택할 수 있습니다. 그러나 한 양식 모델에서 다른 양식 모델로 변경할 수는 없습니다.

1. 적응형 양식을 선택하고 **속성** 아이콘을 누릅니다.
1. **[!UICONTROL 양식 모델]** 탭을 열고 다음 중 하나를 수행합니다.

   * 적응형 양식이 양식 모델이 없는 경우 다른 양식 모델을 선택하여 양식 템플릿, XML 또는 JSON 스키마 또는 양식 데이터 모델을 선택할 수 있습니다.
   * 적응형 양식이 양식 모델을 기반으로 하는 경우 동일한 양식 모델에 대해 다른 양식 템플릿, XML 또는 JSON 스키마 또는 양식 데이터 모델을 선택할 수 있습니다.

1. **[!UICONTROL 저장]**&#x200B;을 눌러 속성을 저장합니다.

## 적응형 양식 {#auto-save-an-adaptive-form} 자동 저장

기본적으로 응용 양식의 내용은 저장 단추 누르기와 같은 사용자 작업에 저장됩니다. 이벤트 또는 시간 간격에 따라 자동으로 컨텐츠 저장을 시작하도록 적응형 양식을 구성할 수도 있습니다. 자동 저장 옵션은 다음과 같은 경우에 유용합니다.

* 익명 사용자와 로그인한 사용자를 위해 컨텐츠를 자동으로 저장
* 사용자 개입 없이 또는 최소한의 사용자 개입 없이 양식 컨텐츠 저장
* 사용자 이벤트를 기반으로 양식의 내용 저장 시작
* 지정된 시간 간격 후에 양식 내용을 반복해서 저장

### 응용 양식 {#enable-auto-save-for-an-adaptive-form}에 대해 자동 저장 사용

기본적으로 자동 저장 옵션은 활성화되지 않습니다. 적응형 양식의 자동 저장 탭에서 자동 저장 옵션을 활성화할 수 있습니다. 자동 저장 탭에서는 여러 가지 다른 구성 옵션도 제공합니다. 적응형 양식에 대해 자동 저장 옵션을 활성화하고 구성하려면 다음 단계를 수행하십시오.

1. 속성의 자동 저장 섹션에 액세스하려면 구성 요소를 선택한 다음 ![필드 수준](assets/field-level.png) > **[!UICONTROL 적응형 양식 컨테이너]**&#x200B;를 누른 다음 ![cmppr](assets/cmppr.png)을 탭합니다.
1. **[!UICONTROL 자동 저장]** 섹션에서 **[!UICONTROL 자동 저장 옵션]**&#x200B;을 활성화합니다.
1. **[!UICONTROL 적응형 양식 이벤트]** 상자에서 1이나 TRUE를 지정하여 양식을 브라우저에 로드할 때 자동으로 양식 저장을 시작합니다. 이벤트에 대한 조건부 표현식을 지정할 수도 있습니다. 이 식을 트리거하고 true를 반환하면 양식 내용을 저장하기 시작합니다.
1. 트리거를 지정합니다. 자동 저장은 구성에 따라 트리거됩니다. 옵션은 다음과 같습니다.

   * **[!UICONTROL 시간 기준:]** 특정 시간 간격에 따라 컨텐츠 저장을 시작하는 옵션을 선택합니다.
   * **[!UICONTROL 이벤트 기반:]** 이벤트가 트리거될 때 컨텐츠 저장을 시작하는 옵션을 선택합니다.

   트리거를 선택하면 전략 구성 상자가 활성화됩니다. 전략 구성 상자를 사용하여 다음을 수행할 수 있습니다.

   * **[!UICONTROL 시간 기반]** 트리거를 선택하는 경우 시간 간격을 지정합니다.
   * **[!UICONTROL 이벤트 기반]** 트리거를 선택하는 경우 이벤트 이름을 지정합니다.

   <!-- You can also create and add your own custom strategy to the list. For details, see [Implement a custom strategy to autosave the forms](auto-save-an-adaptive-form.md#p-implement-a-custom-strategy-to-enable-autosave-for-adaptive-forms-p). -->

1. (시간 기반 자동 저장만 해당) 다음 단계를 수행하여 시간 기반 자동 저장에 대한 옵션을 구성합니다.

   1. **[!UICONTROL 이 간격에 자동 저장]** 상자에서 시간 간격(초)을 지정합니다. 간격 상자에 지정된 시간(초)이 경과되면 양식이 반복해서 저장됩니다.

1. (이벤트 기반 자동 저장만 해당) 다음 단계를 수행하여 이벤트 기반 자동 저장에 대한 옵션을 구성합니다.

   1. **[!UICONTROL 이 이벤트]** 뒤에 자동 저장 상자에서 [GuideBridge](https://helpx.adobe.com/aem-forms/6/javascript-api/GuideBridge.html) 이벤트를 지정합니다. 표현식이 TRUE로 평가될 때마다 양식이 저장됩니다.

1. (선택 사항) 익명 사용자를 위해 컨텐츠를 자동으로 저장하려면 **[!UICONTROL 익명 사용자를 위해 자동 저장 활성화]** 옵션을 선택하고 **[!UICONTROL 확인]**&#x200B;을 클릭합니다.

   >[!NOTE]
   >
   >자동 저장 옵션이 익명의 사용자에게 작동하려면 모든 사용자가 양식을 미리 보고, 확인하고, 서명할 수 있도록 Forms Common Configuration Service를 구성해야 합니다.
   >
   >서비스를 구성하려면 `https://'[server]:[port]'system/console/configMgr`의 Adobe Experience Manager 웹 콘솔 구성으로 이동한 후 **[!UICONTROL Forms 공통 구성 서비스]**&#x200B;를 편집하여 **[!UICONTROL 허용]** 필드에서 **[!UICONTROL 모든 사용자]** 옵션을 선택하고 구성을 저장합니다.