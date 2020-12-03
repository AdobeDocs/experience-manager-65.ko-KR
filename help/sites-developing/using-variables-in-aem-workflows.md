---
title: AEM 워크플로우의 변수
seo-title: AEM 워크플로우의 변수
description: 변수를 만들고 변수에 값을 설정한 다음 OR 분할 및 이동 AEM 워크플로우 단계에서 사용합니다.
seo-description: 변수를 만들고 변수에 값을 설정한 다음 OR 분할 및 이동 AEM 워크플로우 단계에서 사용합니다.
uuid: cc62ff11-51d4-4db4-9c6d-5dc2caa1da52
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: bbb9936e-ecd2-44b3-b4ae-dd62a3160641
docset: aem65
translation-type: tm+mt
source-git-commit: 72a582b7ac19322b81fd1a92de8fce34e55b9db1
workflow-type: tm+mt
source-wordcount: '2081'
ht-degree: 0%

---


# AEM 워크플로우의 변수{#variables-in-aem-workflows}

워크플로우 모델의 변수는 데이터 유형을 기반으로 값을 저장하는 방법입니다. 그런 다음 워크플로우 단계에서 변수 이름을 사용하여 변수에 저장된 값을 검색할 수 있습니다. 또한 변수 이름을 사용하여 라우팅 결정을 위한 표현식을 정의할 수도 있습니다.

AEM 워크플로우 모델에서 다음을 수행할 수 있습니다.

* [저장할 정보 유형을 기반으로 ](/help/sites-developing/using-variables-in-aem-workflows.md#create-a-variable) 다양한 데이터 유형을 만듭니다.
* [변수 설정 워크플로우 단계를 ](/help/sites-developing/using-variables-in-aem-workflows.md#set-a-variable) 사용하여 변수에 대한 값을 설정합니다.
* [OR 분할 및 이동 AEM 워크플로우 단계의 ](/help/sites-developing/using-variables-in-aem-workflows.md#use-a-variable) 변수를 사용하여 라우팅 결정을 내릴 표현식을 정의합니다. 모든 AEM Forms 워크플로우 단계에서 변수를 사용할 수도 있습니다.

다음 비디오에서는 AEM 워크플로우 모델에서 변수를 만들고 설정 및 사용하는 방법을 보여 줍니다.

>[!VIDEO](https://helpx.adobe.com/content/dam/help/en/experience-manager/6-5/forms/using/usevariables_example.mp4)

변수는 [MetaDataMap](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/metadata/MetaDataMap.html) 인터페이스의 확장입니다. ECMAScript에서 [MetaDataMap](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/metadata/MetaDataMap.html)을 사용하여 변수를 사용하여 저장된 메타데이터에 액세스할 수 있습니다.

## 변수 {#create-a-variable} 만들기

워크플로우 모델의 사이드 킥에서 사용할 수 있는 변수 섹션을 사용하여 변수를 만듭니다. AEM 워크플로우 변수는 다음 데이터 유형을 지원합니다.

* **기본 데이터 유형**:Long, Double, Boolean, Date 및 String
* **복잡한 데이터 유형**: [XML ](https://docs.oracle.com/javase/8/docs/api/org/w3c/dom/Document.html) 및  [JSON](https://static.javadoc.io/com.google.code.gson/gson/2.3/com/google/gson/JsonObject.html)

>[!NOTE]
>
>워크플로우는 날짜 유형 변수에 대해서만 ISO8601 형식을 지원합니다.

AEM Forms 워크플로우에서 사용할 수 있는 추가적인 복잡한 데이터 유형은 AEM Forms 워크플로우의 변수[를 참조하십시오.  ](/help/forms/using/variable-in-aem-workflows.md)  ArrayList 데이터 유형을 사용하여 변수 컬렉션을 만듭니다. 모든 기본 및 복잡한 데이터 유형에 대해 ArrayList 변수를 만들 수 있습니다. 예를 들어 ArrayList 변수를 만들고 변수를 사용하여 여러 문자열 값을 저장하려면 하위 유형으로 String을 선택합니다.

다음 단계를 실행하여 변수를 만듭니다.

1. AEM 인스턴스에서 도구 > 워크플로우 > 모델로 이동합니다.
1. **[!UICONTROL 만들기]**&#x200B;를 누르고 워크플로우 모델의 제목과 선택적 이름을 지정합니다. 모델을 선택하고 **[!UICONTROL 편집]**&#x200B;을 누릅니다.
1. 워크플로우 모델의 사이드 킥에서 사용할 수 있는 변수 아이콘을 누르고 **[!UICONTROL 변수 추가]**&#x200B;를 누릅니다.

   ![변수 추가](assets/variables_add_variable_new.png)

1. 변수 추가 대화 상자에서 이름을 지정하고 변수 유형을 선택합니다.
1. **[!UICONTROL 유형]** 드롭다운 목록에서 데이터 유형을 선택하고 다음 값을 지정합니다.

   * 기본 데이터 유형 - 변수에 대한 선택적 기본값을 지정합니다.
   * JSON 또는 XML - 선택적 JSON 또는 XML 스키마 경로를 지정합니다. 시스템에서는 이 스키마에서 사용 가능한 속성을 다른 변수에 매핑하고 저장하는 동안 스키마 경로를 검증합니다.
   * 양식 데이터 모델 - 양식 데이터 모델 경로를 지정합니다.
   * ArrayList - 컬렉션의 하위 유형을 지정합니다.

1. 변수에 대한 선택적 설명을 지정하고 ![](https://helpx.adobe.com/content/dam/help/en/experience-manager/6-4/forms/using/chart-component/Done_Icon.png)을 눌러 변경 내용을 저장합니다. 이 변수는 왼쪽 창에서 사용할 수 있는 목록에 표시됩니다.

변수를 만들 때는 다음 방법을 고려하십시오.

* 워크플로우에 필요한 만큼 많은 변수를 만들 수 있습니다. 그러나 데이터베이스 리소스를 보존하려면 필요한 최소 변수 수를 사용하고 가능한 경우 변수를 재사용하십시오.
* 변수는 대소문자를 구분합니다. 워크플로우에서 동일한 케이스를 사용하여 변수를 참조하는지 확인하십시오.
* 변수 이름에 특수 문자를 사용하지 마십시오.

## 변수 {#set-a-variable} 설정

변수 설정 단계를 사용하여 변수 값을 설정하고 값이 설정되는 순서를 정의할 수 있습니다. 이 변수는 변수 매핑이 세트 변수 단계에 나열된 순서대로 설정됩니다.

변수 값의 변경 사항은 변경이 발생하는 프로세스 인스턴스에만 영향을 줍니다. 예를 들어 워크플로우가 시작되고 데이터 변수가 변경되면 워크플로우의 해당 인스턴스에만 변경 사항이 적용됩니다. 변경 사항은 이전에 시작되었거나 이후에 시작된 워크플로우의 다른 인스턴스에는 영향을 주지 않습니다.

변수의 데이터 유형에 따라 다음 옵션을 사용하여 변수의 값을 설정할 수 있습니다.

* **리터럴:** 지정할 정확한 값을 알고 있을 때 옵션을 사용합니다.
* **표현식:** 사용할 값이 표현식에 따라 계산될 때 이 옵션을 사용합니다. 표현식은 제공된 표현식 편집기에서 만들어집니다.
* **JSON 점 표기법:** 이 옵션을 사용하여 JSON 또는 FDM 유형 변수에서 값을 검색합니다.
* **XPATH:** XML 유형 변수에서 값을 검색하려면 이 옵션을 사용합니다.
* **페이로드 상대:** 변수에 저장할 값을 페이로드를 기준으로 하는 경로에서 사용할 수 있을 때 옵션을 사용합니다.
* **절대 경로:** 변수에 저장할 값을 절대 경로에서 사용할 수 있을 때 옵션을 사용합니다.

JSON DOT 표기법 또는 XPATH 표기법을 사용하여 JSON 또는 XML 유형 변수의 특정 요소를 업데이트할 수도 있습니다.

### 변수 {#add-mapping-between-variables} 사이에 매핑 추가

다음 단계를 실행하여 변수 간 매핑을 추가합니다.

1. 워크플로우 편집 페이지에서 워크플로우 모델의 사이드 킥에 있는 단계 아이콘을 누릅니다.
1. **변수 설정** 단계를 워크플로 편집기로 드래그하여 놓고 단계를 누르고 ![](https://helpx.adobe.com/content/dam/help/en/experience-manager/6-4/forms/using/configure_icon.png) (구성)을 선택합니다.
1. 변수 설정 대화 상자에서 **[!UICONTROL 매핑]** > **[!UICONTROL 매핑 추가]**&#x200B;를 선택합니다.
1. **변수 매핑** 섹션에서 데이터를 저장할 변수를 선택하고 매핑 모드를 선택한 다음 변수에 저장할 값을 지정합니다. 매핑 모드는 변수 유형에 따라 다릅니다.
1. 의미 있는 표현을 만들 변수를 더 매핑합니다. ![](https://helpx.adobe.com/content/dam/help/en/experience-manager/6-4/forms/using/chart-component/Done_Icon.png)을 눌러 변경 내용을 저장합니다.

### 예 1:XML 변수를 쿼리하여 문자열 변수 {#example-query-an-xml-variable-to-set-value-for-a-string-variable} 값을 설정합니다.

XML 파일을 저장하려면 XML 유형의 변수를 선택합니다. XML 파일에서 사용할 수 있는 속성의 문자열 변수 값을 설정하려면 XML 변수를 쿼리합니다. XML 변수&#x200B;**필드에 대한** XPATH를 지정하여 문자열 변수에 저장할 속성을 정의합니다.

이 예에서 **formdata** XML 변수를 선택하여 **cc-app.xml** 파일을 저장합니다. **formdata** 변수를 쿼리하여 **emailaddress** 문자열 변수의 값을 설정하여 **cc-app.xml** 파일에서 사용할 수 있는 **emailAddress** 속성의 값을 저장합니다.

>[!VIDEO](https://helpx.adobe.com/content/dam/help/en/experience-manager/6-5/forms/using/set_variable_example1.mp4 "변수의 값 설정")

### 예 2:표현식을 사용하여 다른 변수 {#example2}에 따라 값을 저장

표현식을 사용하여 변수의 합계를 계산하고 결과를 변수에 저장합니다.

이 예에서 표현식 편집기를 사용하여 **assetscost** 및 **balanceamount** 변수의 합계를 계산하는 표현식을 정의하고 결과를 **totalvalue** 변수에 저장합니다.

>[!VIDEO](https://helpx.adobe.com/content/dam/help/en/experience-manager/6-5/forms/using/variables_expression.mp4)

## 표현식 편집기 {#use-expression-editor} 사용

또한 표현식을 사용하여 런타임에서 변수의 값을 계산합니다. 변수는 표현식을 정의하는 표현식 편집기를 제공합니다.

표현식 편집기를 사용하여 다음을 수행할 수 있습니다.

* 다른 워크플로우 변수, 숫자 또는 수학 표현식을 사용하여 변수의 값을 설정합니다.
* 수학 표현식 내에서 워크플로우 변수, 문자열, 숫자 또는 표현식을 사용합니다
* 조건을 추가하여 변수 값을 설정합니다.
* 조건 사이에 연산자를 추가합니다.

![표현식 편집기](assets/variables_expression_editor_new.png)

적응형 양식 규칙 편집기를 기반으로 다음 변경 사항을 적용합니다. 변수의 규칙 편집기:

* 기능을 지원하지 않습니다.
* 규칙 요약을 볼 수 있는 UI를 제공하지 않음
* 코드 편집기가 없습니다.
* 개체의 값 활성화 및 비활성화는 지원하지 않습니다.
* 개체의 속성 설정을 지원하지 않습니다.
* 웹 서비스 호출을 지원하지 않습니다.

자세한 내용은 [적응형 양식 규칙 편집기](/help/forms/using/rule-editor.md)를 참조하십시오.

## 변수 {#use-a-variable} 사용

변수를 사용하여 입력 및 출력을 검색하거나 단계 결과를 저장할 수 있습니다. 워크플로우 편집기에서는 다음 두 가지 유형의 워크플로우 단계를 제공합니다.

* 변수에 대한 지원이 포함된 워크플로우 단계
* 변수에 대한 지원이 없는 워크플로우 단계

### {#workflow-steps-with-support-for-variables} 변수를 지원하는 워크플로우 단계

이동 단계, OR 분할 단계 및 모든 AEM Forms 워크플로우 단계는 변수를 지원합니다.

#### OR 분할 단계 {#or-split-step}

OR 분할은 워크플로우에서 분할을 생성하며 그 뒤에는 하나의 분기만 활성화됩니다. 이 단계에서는 조건부 처리 경로를 워크플로에 도입할 수 있습니다. 필요에 따라 각 분기에 워크플로우 단계를 추가합니다.

규칙 정의, ECMA 스크립트 또는 외부 스크립트를 사용하여 분기에 대한 라우팅 표현식을 정의할 수 있습니다.

변수를 사용하여 표현식 편집기를 사용하여 라우팅 표현식을 정의할 수 있습니다. OR 분할 단계의 라우팅 표현식 사용에 대한 자세한 내용은 [OR 분할 단계](/help/sites-developing/workflows-step-ref.md#or-split)를 참조하십시오.

이 예에서 라우팅 표현식을 정의하기 전에 [example 2](/help/sites-developing/using-variables-in-aem-workflows.md#example2)을 사용하여 **totalvalue** 변수의 값을 설정합니다. 분기 1은 **totalvalue** 변수의 값이 50000보다 큰 경우 활성화됩니다. 마찬가지로, **totalvalue** 변수의 값이 50000보다 작으면 분기 2를 활성화하도록 규칙을 정의할 수 있습니다.

>[!VIDEO](https://helpx.adobe.com/content/dam/help/en/experience-manager/6-5/forms/using/variables_orsplit_example.mp4)

마찬가지로, 외부 스크립트 경로를 선택하거나 활성 분기를 평가할 라우팅 표현식에 대한 ECMA 스크립트를 지정합니다. **[!UICONTROL 분기 이름 바꾸기]**&#x200B;를 눌러 분기의 대체 이름을 지정합니다.

자세한 예는 [워크플로우 모델 만들기](/help/forms/using/aem-forms-workflow.md#create-a-workflow-model)를 참조하십시오.

#### 이동 단계 {#go-to-step}

**이동 단계**&#x200B;에서는 라우팅 표현식 결과에 따라 실행할 워크플로우 모델의 다음 단계를 지정할 수 있습니다.

OR 분할 단계와 유사하게, 규칙 정의, ECMA 스크립트 또는 외부 스크립트를 사용하여 이동 단계에 대한 라우팅 표현식을 정의할 수 있습니다.

변수를 사용하여 표현식 편집기를 사용하여 라우팅 표현식을 정의할 수 있습니다. 이동 단계의 라우팅 표현식 사용에 대한 자세한 내용은 [이동 단계](/help/sites-developing/workflows-step-ref.md#goto-step)를 참조하십시오.

![이동 규칙](assets/variables_goto_rule1_new.png)

이 예에서 이동 단계에서는 **actiontaken** 변수의 값이 **추가 정보 필요**&#x200B;와 같은 경우 신용 카드 검토 응용 프로그램을 다음 단계로 지정합니다.

이동 단계에서 규칙 정의를 사용하는 방법에 대한 자세한 예는 [Simulating a For loop](/help/sites-developing/workflows-step-ref.md#simulateforloop)을 참조하십시오.

#### Forms 워크플로우 중심의 워크플로우 단계 {#forms-workflow-centric-workflow-steps}

모든 AEM Forms 워크플로우 단계는 변수를 지원합니다. 자세한 내용은 OSGi[의 Forms 중심 워크플로우를 참조하십시오.](/help/forms/using/aem-forms-workflow-step-reference.md)

### {#workflow-steps-without-support-for-variables} 변수가 지원되지 않는 워크플로우 단계

[MetaDataMap](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/metadata/MetaDataMap.html) 인터페이스를 사용하여 변수를 지원하지 않는 워크플로우 단계의 변수에 액세스할 수 있습니다.

#### 변수 값 {#retrieve-the-variable-value} 검색

ECMA 스크립트의 다음 API를 사용하여 데이터 유형에 따라 기존 변수의 값을 검색합니다.

| 변수 데이터 유형 | API |
|---|---|
| 기본(Long, Double, Boolean, Date 및 String) | workItem.getWorkflowData().getMetaDataMap().get(variableName, type) |
| XML | Packages.org.w3c.dom.Document xmlObject = workItem.getWorkflowData().getMetaDataMap().get(variableName, Packages.org.w3c.dom.Document.class); |
| JSON | Packages.com.google.gson.JsonObject jsonObject = workItem.getWorkflowData().getMetaDataMap().get(variableName, Packages.com.google.gson.JsonObject.class); |

AEM Forms 워크플로우에서 사용할 수 있는 추가적인 복잡한 변수 데이터 유형에 대한 API에 대한 자세한 내용은 AEM Forms 워크플로우의 변수[를 참조하십시오.](/help/forms/using/variable-in-aem-workflows.md)

**예**

다음 API를 사용하여 문자열 데이터 형식의 값을 검색합니다.

```
workItem.getWorkflowData().getMetaDataMap().get(accname, Packages.java.lang.String)
```

#### 변수 값 {#update-the-variable-value} 업데이트

ECMA 스크립트의 다음 API를 사용하여 변수 값을 업데이트합니다.

```
workItem.getWorkflowData().getMetaDataMap().put(variableName, value)
```

**예**

```
workItem.getWorkflowData().getMetaDataMap().put(salary, 50000)
```

**salary** 변수의 값을 50000으로 업데이트합니다.

### 변수를 설정하여 워크플로 {#apiinvokeworkflow} 호출

API를 사용하여 변수를 설정하고 이를 전달하여 워크플로우 인스턴스를 호출할 수 있습니다.

[workflowSession.](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/WorkflowSession.html#startWorkflow-com.adobe.granite.workflow.model.WorkflowModel-com.adobe.granite.workflow.exec.WorkflowData-java.util.Map-) startWorkflow에서는 모델, wfData 및 metaData를 인수로 사용합니다. MetaDataMap을 사용하여 변수 값을 설정합니다.

이 API에서 **variableName** 변수는 metaData.put(variableName, value)을 사용하여 **value**&#x200B;으로 설정됩니다.

```java
import com.adobe.granite.workflow.model.WorkflowModel;
import com.adobe.granite.workflow.metadata.MetaDataMap;
import com.adobe.aemfd.docmanager.Document;

/*Assume that you already have a workflowSession and modelId along with the payloadType and payload*/
WorkflowData wfData = workflowSession.newWorkflowData(payloadType, payload);
MetaDataMap metaData = wfData.getMetaDataMap();
metaData.put(variableName, value); //Create a variable "variableName" in your workflow model
WorkflowModel model = workflowSession.getModel(modelId);
workflowSession.startWorkflow(model, wfData, metaData);
```

## 변수 {#edit-a-variable} 편집

1. 편집 워크플로우 페이지에서 워크플로우 모델의 사이드 킥에 있는 변수 아이콘을 누릅니다. 왼쪽 창의 변수 섹션에는 모든 기존 변수가 표시됩니다.
1. 편집할 변수 이름 옆에 있는 ![](https://helpx.adobe.com/content/dam/help/images/en/edit.png)(편집) 아이콘을 누릅니다.
1. 변수 정보를 편집하고 ![](https://helpx.adobe.com/content/dam/help/en/experience-manager/6-4/forms/using/chart-component/Done_Icon.png)을 눌러 변경 사항을 저장합니다. 변수의 **[!UICONTROL 이름]** 및 **[!UICONTROL 유형]** 필드는 편집할 수 없습니다.

## 변수 {#delete-a-variable} 삭제

변수를 삭제하기 전에 워크플로우에서 변수의 모든 참조를 제거합니다. 워크플로우에서 변수가 사용되지 않는지 확인합니다.

다음 단계를 실행하여 변수를 삭제합니다.

1. 편집 워크플로우 페이지에서 워크플로우 모델의 사이드 킥에 있는 변수 아이콘을 누릅니다. 왼쪽 창의 변수 섹션에는 모든 기존 변수가 표시됩니다.
1. 삭제할 변수 이름 옆에 있는 삭제 아이콘을 누릅니다.
1. ![](https://helpx.adobe.com/content/dam/help/en/experience-manager/6-4/forms/using/chart-component/Done_Icon.png)을 눌러 변수를 확인하고 삭제합니다.

