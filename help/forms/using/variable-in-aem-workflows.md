---
title: AEM Forms 워크플로우의 변수
seo-title: Variables in AEM Forms Workflows
description: 변수를 만들고 변수에 대한 값을 설정한 다음 AEM Forms 워크플로우 단계에서 사용합니다.
seo-description: Create a variable, set a value for the variable, and use it in AEM Forms workflow steps.
uuid: 634a75c4-4899-478f-9e5d-a870f5efa583
contentOwner: khsingh
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
discoiquuid: cbf4e35a-7905-44ab-ab68-fb443443f02d
docset: aem65
exl-id: beb2b83e-e8db-40bb-915f-cb6ba3140947
source-git-commit: 936b636819eaef595fcdf9f1f3446d4ac0c28b2f
workflow-type: tm+mt
source-wordcount: '2208'
ht-degree: 0%

---

# AEM Forms 워크플로우의 변수{#variables-in-aem-forms-workflows}

워크플로우 모델의 변수는 데이터 유형을 기반으로 값을 저장하는 방법입니다. 그런 다음 워크플로우 단계에서 변수 이름을 사용하여 변수에 저장된 값을 검색할 수 있습니다. 변수 이름을 사용하여 라우팅 결정을 수행할 표현식을 정의할 수도 있습니다.

AEM 워크플로우 모델에서 다음을 수행할 수 있습니다.

* [변수 만들기](../../forms/using/variable-in-aem-workflows.md#create-a-variable) 저장할 정보 유형을 기반으로 한 데이터 유형입니다.
* [변수에 대한 값 설정](../../forms/using/variable-in-aem-workflows.md#set-a-variable) 변수 설정 워크플로우 단계를 사용합니다.
* [변수 사용](../../forms/using/variable-in-aem-workflows.md#use-a-variable) 모든 AEM Forms 워크플로우 단계에서 저장된 값을 검색하고 OR 분할 및 이동 단계에서 라우팅 표현식을 정의합니다.

다음 비디오에서는 AEM 워크플로우 모델에서 변수를 만들고, 설정하고, 사용하는 방법을 보여 줍니다.

<!-- FUTURE ERROR: YouTube and mp4 videos are not supported -->

>[!VIDEO](https://helpx.adobe.com/content/dam/help/en/experience-manager/6-5/forms/using/variables_introduction_1_1.mp4)

변수는 기존 변수의 확장입니다 [MetaDataMap](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/metadata/MetaDataMap.html) 인터페이스. 다음을 사용할 수 있습니다 [MetaDataMap](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/metadata/MetaDataMap.html) 변수를 사용하여 저장된 메타데이터에 액세스할 수 있습니다.

## 변수 만들기 {#create-a-variable}

워크플로우 모델의 사이드 킥에서 사용할 수 있는 변수 섹션을 사용하여 변수를 만듭니다. AEM 워크플로우 변수는 다음 데이터 유형을 지원합니다.

* **기본 데이터 유형**: Long, Double, Boolean, Date 및 String
* **복잡한 데이터 유형**: [문서](https://helpx.adobe.com/experience-manager/6-5/forms/javadocs/com/adobe/aemfd/docmanager/Document.html), [XML](https://docs.oracle.com/javase/8/docs/api/org/w3c/dom/Document.html), [JSON](https://static.javadoc.io/com.google.code.gson/gson/2.3/com/google/gson/JsonObject.html), 및 양식 데이터 모델 인스턴스.

>[!NOTE]
>
>워크플로우는 날짜 유형 변수에 대해서만 ISO8601 형식만 지원합니다.

필요한 경우 [AEM Forms 추가 기능 패키지](https://helpx.adobe.com/kr/aem-forms/kb/aem-forms-releases.html) 문서 및 양식 데이터 모델 데이터 유형용.  ArrayList 데이터 유형을 사용하여 변수 컬렉션을 만듭니다. 모든 기본 데이터 유형과 복잡한 데이터 유형에 대해 ArrayList 변수를 만들 수 있습니다. 예를 들어 ArrayList 변수를 만들고 String을 하위 형식으로 선택하여 변수를 사용하여 여러 문자열 값을 저장합니다.

다음 단계를 실행하여 변수를 만듭니다.

1. AEM 인스턴스에서 도구로 이동합니다 ![](/help/forms/using/assets/hammer.png) > 워크플로우 > 모델.
1. 탭 **[!UICONTROL 만들기]** 워크플로우 모델의 제목과 선택적 이름을 지정합니다. 모델을 선택하고 탭합니다 **[!UICONTROL 편집]**.
1. 워크플로우 모델의 사이드 킥에서 사용할 수 있는 변수 아이콘을 탭하고 탭합니다 **[!UICONTROL 변수 추가]**.

   ![변수 추가](assets/variables_add_variable_new.png)

1. 변수 추가 대화 상자에서 이름을 지정하고, 변수 유형을 선택합니다.
1. 에서 데이터 유형을 선택합니다 **[!UICONTROL 유형]** 드롭다운 목록을 표시하고 다음 값을 지정합니다.

   * 기본 데이터 유형 - 변수에 대한 선택적 기본값을 지정합니다.
   * JSON 또는 XML - 선택적 JSON 또는 XML 스키마 경로를 지정합니다. 시스템은 이 스키마에서 사용할 수 있는 속성을 다른 변수에 매핑하고 저장하는 동안 스키마 경로를 검증합니다.
   * 양식 데이터 모델 - 양식 데이터 모델 경로를 지정합니다.
   * ArrayList - 컬렉션의 하위 유형을 지정합니다.

1. 변수에 대한 선택적 설명을 지정하고 을(를) 누릅니다 ![done_icon](assets/done_icon.png) 변경 사항을 저장하려면 을 클릭합니다. 변수는 왼쪽 창에서 사용할 수 있는 목록에 표시됩니다.

변수를 만들 때 다음 방법을 고려하십시오.

* 워크플로우에 필요한 만큼 변수를 만듭니다. 그러나 데이터베이스 리소스를 보존하려면 필요한 최소 변수 수를 사용하고 가능한 경우 변수를 다시 사용하십시오.
* 변수는 대/소문자를 구분합니다. 워크플로우에서 동일한 사례를 사용하여 변수를 참조하는지 확인합니다.
* 변수 이름에 특수 문자를 사용하지 마십시오

## 변수 설정 {#set-a-variable}

변수 설정 단계를 사용하여 변수의 값을 설정하고 값이 설정되는 순서를 정의할 수 있습니다. 변수는 변수 매핑이 변수 설정 단계에서 나열된 순서로 설정됩니다.

변수 값에 대한 변경 사항은 변경 사항이 발생하는 프로세스의 인스턴스에만 영향을 줍니다. 예를 들어 워크플로우가 시작되고 변수 데이터가 변경되면 변경 사항은 워크플로우의 해당 인스턴스에만 영향을 줍니다. 변경 사항은 이전에 시작되었거나 이후에 시작된 워크플로우의 다른 인스턴스는 영향을 주지 않습니다.

변수의 데이터 유형에 따라 다음 옵션을 사용하여 변수의 값을 설정할 수 있습니다.

* **리터럴:** 지정할 정확한 값을 알고 있는 경우 옵션을 사용합니다.

* **표현식:** 표현식을 기반으로 사용할 값이 계산되는 경우 옵션을 사용합니다. 표현식은 제공된 표현식 편집기에서 만들어집니다.

* **JSON 점 표기법:** JSON 또는 FDM 유형 변수에서 값을 검색하려면 옵션을 사용합니다.
* **XPATH:** XML 유형 변수에서 값을 검색하려면 옵션을 사용합니다.

* **페이로드에 대해:** 페이로드를 기준으로 하는 경로에서 변수에 저장할 값을 사용할 수 있는 경우 옵션을 사용합니다.

* **절대 경로:** 절대 경로에서 변수에 저장할 값을 사용할 수 있는 경우 옵션을 사용합니다.

JSON 점 표기법 또는 XPATH 표기법을 사용하여 JSON 또는 XML 유형 변수의 특정 요소를 업데이트할 수도 있습니다.

### 변수 간에 매핑 추가 {#add-mapping-between-variables}

다음 단계를 실행하여 변수 간에 매핑을 추가합니다.

1. 워크플로우 편집 페이지에서 워크플로우 모델의 사이드 킥에서 사용할 수 있는 단계 아이콘을 탭합니다.
1. 드래그 앤 드롭 **변수 설정** 워크플로우 편집기 단계로 이동하여 단계를 탭하고 을(를) 선택합니다 ![configure_icon](assets/configure_icon.png) (구성).
1. 변수 설정 대화 상자에서 를 선택합니다. **[!UICONTROL 매핑]** > **[!UICONTROL 매핑 추가]**.
1. 에서 **맵 변수** 섹션에서 데이터를 저장할 변수를 선택하고 매핑 모드를 선택한 다음 변수에 저장할 값을 지정합니다. 매핑 모드는 변수 유형에 따라 달라집니다.
1. 의미 있는 표현식을 만들기 위해 더 많은 변수를 매핑합니다. 탭 ![done_icon](assets/done_icon.png) 변경 사항을 저장하려면 을 클릭합니다.

### 예제 1: 문자열 변수의 값을 설정할 XML 변수를 질의합니다 {#example-query-an-xml-variable-to-set-value-for-a-string-variable}

XML 파일을 저장할 XML 유형의 변수를 선택합니다. XML 변수를 쿼리하여 XML 파일에서 사용할 수 있는 속성의 문자열 변수 값을 설정합니다. 사용 **XML 변수에 대한 XPATH 지정** 문자열 변수에 저장할 속성을 정의하는 필드입니다.

이 예에서 **양식 데이터** 저장할 XML 변수 **cc-app.xml** 파일. 쿼리 **양식 데이터** 변수에 대한 값을 설정할 수 있습니다. **emailaddress** 값을 저장할 문자열 변수 **emailAddress** 에서 사용할 수 있는 속성 **cc-app.xml** 파일.

>[!VIDEO](https://helpx.adobe.com/content/dam/help/en/experience-manager/6-5/forms/using/set_variable_example1.mp4 "변수의 값 설정")

### 예제 2: 표현식을 사용하여 다른 변수를 기반으로 값을 저장합니다 {#example2}

표현식을 사용하여 변수의 합계를 계산하고 결과를 변수에 저장합니다.

이 예에서 표현식 편집기를 사용하여 표현식을 정의하여 **assetscost** 및 **잔액** 변수와 결과를 **totalvalue** 변수를 채우는 방법을 설명합니다.

<!-- FUTURE ERROR: YouTube and mp4 videos are not supported -->

>[!VIDEO](https://helpx.adobe.com/content/dam/help/en/experience-manager/6-5/forms/using/variables_expression.mp4)

## 표현식 편집기 사용 {#use-expression-editor}

또한 표현식을 사용하여 런타임 시 변수의 값을 계산합니다. 변수는 표현식을 정의하는 표현식 편집기를 제공합니다.

표현식 편집기를 사용하여 다음을 수행합니다.

* 다른 워크플로우 변수, 숫자 또는 수학 표현식을 사용하여 변수의 값을 설정합니다.
* 수식 내에서 워크플로우 변수, 문자열, 숫자 또는 표현식을 사용합니다
* 변수 값을 설정하려면 조건을 추가하십시오.
* 조건 사이에 연산자를 추가합니다.

![표현식 편집기](assets/variables_expression_editor_new.png)

이 편집기는 다음과 같은 변경 사항이 있는 적응형 양식 규칙 편집기를 기반으로 합니다. 변수의 규칙 편집기:

* 함수가 지원되지 않습니다.
* 규칙 요약을 볼 UI를 제공하지 않음
* 코드 편집기가 없습니다.
* 개체의 값 활성화 및 비활성화를 지원하지 않습니다.
* 개체의 속성 설정을 지원하지 않습니다.
* 웹 서비스 호출을 지원하지 않습니다.

자세한 내용은 [적응형 양식 규칙 편집기](../../forms/using/rule-editor.md).

## 변수 사용 {#use-a-variable}

변수를 사용하여 입력 및 출력을 검색하거나 단계 결과를 저장할 수 있습니다. 워크플로우 편집기에서는 두 가지 유형의 워크플로우 단계를 제공합니다.

* 변수를 지원하는 워크플로우 단계
* 변수를 지원하지 않는 워크플로우 단계

### 변수를 지원하는 워크플로우 단계 {#workflow-steps-with-support-for-variables}

이동 단계, 또는 분할 단계 및 모든 AEM Forms 워크플로우 단계는 변수를 지원합니다.

#### 또는 분할 단계 {#or-split-step}

OR 분할은 워크플로우에서 분할을 만들며, 그 뒤에는 하나의 분기만 활성화됩니다. 이 단계를 통해 워크플로우에 조건부 처리 경로를 도입할 수 있습니다. 필요에 따라 각 분기에 워크플로우 단계를 추가합니다.

규칙 정의, ECMA 스크립트 또는 외부 스크립트를 사용하여 분기에 대한 라우팅 표현식을 정의할 수 있습니다.

변수를 사용하여 표현식 편집기를 사용하여 라우팅 표현식을 정의할 수 있습니다. OR 분할 단계의 라우팅 표현식 사용에 대한 자세한 내용은 [또는 분할 단계](/help/sites-developing/workflows-step-ref.md#or-split).

이 예에서 라우팅 표현식을 정의하기 전에 [예제 2](../../forms/using/variable-in-aem-workflows.md#example2) 에 대한 값을 설정하려면 **totalvalue** 변수를 채우는 방법을 설명합니다. 분기 1은 **totalvalue** 변수가 50000보다 큼. 마찬가지로, **totalvalue** 변수가 50000 보다 작습니다.

<!-- FUTURE ERROR: YouTube and mp4 videos are not supported -->

>[!VIDEO](https://helpx.adobe.com/content/dam/help/en/experience-manager/6-5/forms/using/variables_orsplit_example.mp4)

마찬가지로, 외부 스크립트 경로를 선택하거나 라우팅 표현식에 대한 ECMA 스크립트를 지정하여 활성 분기를 평가합니다. 탭 **[!UICONTROL 분기 이름 바꾸기]** 분기의 대체 이름을 지정합니다.

자세한 내용은 [워크플로우 모델 만들기](../../forms/using/aem-forms-workflow.md#create-a-workflow-model).

#### 단계로 이동 {#go-to-step}

다음 **이동 단계** 라우팅 표현식 결과에 따라 실행할 워크플로우 모델의 다음 단계를 지정할 수 있습니다.

OR 분할(OR Split) 단계와 마찬가지로 규칙 정의, ECMA 스크립트 또는 외부 스크립트를 사용하여 이동 단계에 대한 라우팅 표현식을 정의할 수 있습니다.

변수를 사용하여 표현식 편집기를 사용하여 라우팅 표현식을 정의할 수 있습니다. 이동 단계의 라우팅 표현식 사용에 대한 자세한 내용은 [이동 단계](/help/sites-developing/workflows-step-ref.md#goto-step).

![이동 규칙](assets/variables_goto_rule1_new.png)

이 예에서 이동 단계는 **실행** 변수가 다음과 같음 **추가 정보 필요**.

이동 단계에서 규칙 정의를 사용하는 방법에 대한 자세한 내용은 [For 루프 시뮬레이션](/help/sites-developing/workflows-step-ref.md#simulateforloop).

#### Forms 워크플로우 중심의 워크플로우 단계 {#forms-workflow-centric-workflow-steps}

모든 AEM Forms 워크플로우 단계는 변수를 지원합니다. 자세한 내용은 [OSGi의 Forms 중심 워크플로우](../../forms/using/aem-forms-workflow-step-reference.md).

### 변수를 지원하지 않는 워크플로우 단계 {#workflow-steps-without-support-for-variables}

다음을 사용할 수 있습니다 [MetaDataMap](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/metadata/MetaDataMap.html) 변수를 지원하지 않는 워크플로우 단계의 변수에 액세스할 수 있는 인터페이스.

#### 변수 값을 검색합니다 {#retrieve-the-variable-value}

ECMA Script에서 다음 API를 사용하여 데이터 유형을 기반으로 기존 변수의 값을 검색합니다.

| 변수 데이터 유형 | API |
|---|---|
| 기본(Long, Double, Boolean, Date 및 String) | workItem.getWorkflowData().getMetaDataMap().get(variableName, type) |
| 문서 | Packages.com.adobe.aemfd.docmanager.Document doc = workItem.getWorkflowData().getMetaDataMap().get(&quot;docVar&quot;, Packages.com.adobe.aemfd.docmanager.Document.class); |
| XML | Packages.w3c.dom.Document xmlObject = workItem.getWorkflowData().getMetaDataMap().get(variableName, Packages.org.w3c.dom.Document.class); |
| 양식 데이터 모델 | Packages.com.adobe.aem.dermis.api.FormDataModelInstance fdmObject = workItem.getWorkflowData().getMetaDataMap().get(variableName, Packages.com.adobe.aem.dermis.api.FormDataModelInstance.class); |
| JSON | Packages.com.google.gson.JsonObject jsonObject = workItem.getWorkflowData().getMetaDataMap().get(variableName, Packages.com.google.gson.JsonObject.class); |

필요한 경우 [AEM Forms 추가 기능 패키지](https://helpx.adobe.com/kr/aem-forms/kb/aem-forms-releases.html) 문서 및 양식 데이터 모델 변수 데이터 유형에 사용할 수 있습니다.

**예**

다음 API를 사용하여 문자열 데이터 유형의 값을 검색합니다.

```javascript
workItem.getWorkflowData().getMetaDataMap().get(accname, Packages.java.lang.String)
```

#### 변수 값 업데이트 {#update-the-variable-value}

ECMA Script에서 다음 API를 사용하여 변수 값을 업데이트합니다.

```javascript
workItem.getWorkflowData().getMetaDataMap().put(variableName, value)
```

**예**

```javascript
workItem.getWorkflowData().getMetaDataMap().put(salary, 50000)
```

는 다음 항목의 값을 업데이트합니다. **임금** 변수를 50000.

### 워크플로우를 호출하는 변수 설정 {#apiinvokeworkflow}

API를 사용하여 변수를 설정하고 이를 전달하여 워크플로우 인스턴스를 호출할 수 있습니다.

[workflowSession.startWorkflow](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/WorkflowSession.html#startWorkflow-com.adobe.granite.workflow.model.WorkflowModel-com.adobe.granite.workflow.exec.WorkflowData-java.util.Map-) 는 모델, wfData 및 metaData를 인수로 사용합니다. MetaDataMap을 사용하여 변수에 대한 값을 설정합니다.

이 API에서는 **variableName** 변수를으로 설정합니다. **value** metaData.put(variableName, value) 사용;

```javascript
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

**예**

초기화 **doc** 문서 객체를 경로(&quot;a/b/c&quot;)로 설정하고 **docVar** 변수에 채울 수 있습니다.

```javascript
import com.adobe.granite.workflow.WorkflowSession;
import com.adobe.granite.workflow.exec.WorkflowData;
import com.adobe.granite.workflow.model.WorkflowModel;
import com.adobe.granite.workflow.metadata.MetaDataMap;
import com.adobe.aemfd.docmanager.Document;

/*This example assumes that you already have a workflowSession and modelId along with the payloadType and payload */
WorkflowData wfData = workflowSession.newWorkflowData(payloadType, payload);
MetaDataMap metaData = wfData.getMetaDataMap();
Document doc = new Document("/a/b/c");// initialize a document object
metaData.put("docVar",doc); //Assuming that you have created a variable "docVar" of type Document in your workflow model
WorkflowModel model = workflowSession.getModel(modelId);
workflowSession.startWorkflow(model, wfData, metaData);
```

### 워크플로우 변수를 사용하여 JCR 외부에 중요한 사용자 데이터 저장 {#jcr-independent-persistance}

Forms Workflow을 사용하여 처리된 데이터에는 개인 식별 정보 및 중요 개인 정보와 같은 중요한 사용자 데이터가 포함될 수 있습니다. 기업은 다양한 워크플로우 단계에 의해 처리되고 워크플로우 변수를 사용하여 전달된 데이터를 JCR 스토리지 내에서 해당 데이터가 소유하고 관리하는 외부 데이터 저장소에 저장하도록 선택할 수 있습니다. 외부 저장소에서 워크플로우 데이터 유지에 대한 자세한 내용은 [고객이 소유한 데이터 저장소에 대한 워크플로우 변수 사용](/help/sites-administering/workflows-administering.md#using-workflow-variables-customer-datastore).
[!DNL Adobe Experience Manager] 워크플로우 API 제공 [UserMetaDataPersistenceProvider](https://github.com/adobe/workflow-variable-externalizer) 워크플로우 변수를 외부 Azure blob 저장소에 저장. API 사용에 대한 자세한 내용은 [워크플로우 변수를 사용하여 중요한 데이터를 매개 변수화하고 외부 데이터 저장소에 저장](/help/forms/using/aem-forms-workflow.md#externalize-wf-variables).

## 변수 편집 {#edit-a-variable}

1. 워크플로우 편집 페이지에서 워크플로우 모델의 사이드 킥에서 사용할 수 있는 변수 아이콘을 탭합니다. 왼쪽 창의 변수 섹션에는 모든 기존 변수가 표시됩니다.
1. 탭하기 ![편집](assets/edit.png) (편집) 아이콘을 클릭합니다.
1. 변수 정보를 편집하고 탭합니다. ![done_icon](assets/done_icon.png) 변경 사항을 저장하려면 을 클릭합니다. 는 편집할 수 없습니다 **[!UICONTROL 이름]** 및 **[!UICONTROL 유형]** 변수에 대한 필드입니다.

## 변수 삭제 {#delete-a-variable}

변수를 삭제하기 전에 워크플로우에서 변수의 모든 참조를 제거합니다. 변수가 워크플로우에서 사용되지 않는지 확인합니다.

다음 단계를 실행하여 변수를 삭제합니다.

1. 워크플로우 편집 페이지에서 워크플로우 모델의 사이드 킥에서 사용할 수 있는 변수 아이콘을 탭합니다. 왼쪽 창의 변수 섹션에는 모든 기존 변수가 표시됩니다.
1. 삭제할 변수 이름 옆에 있는 삭제 아이콘을 탭합니다.
1. 탭 ![done_icon](assets/done_icon.png) 변수를 확인하고 삭제합니다.

## 참조 {#references}

AEM Forms 워크플로우 단계에서 변수를 사용하는 방법에 대한 자세한 내용은 [AEM 워크플로우의 변수](https://helpx.adobe.com/experience-manager/kt/forms/using/authoring_variables_in_aem_forms-workflow1.html).
