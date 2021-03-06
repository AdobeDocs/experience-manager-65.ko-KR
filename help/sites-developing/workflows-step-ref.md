---
title: 워크플로우 단계 참조
seo-title: 워크플로우 단계 참조
description: 워크플로우 단계 참조
seo-description: 'null'
uuid: 88bf6997-73a1-4639-82aa-5dff08d3ef86
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: e3afffd0-d90c-4bd0-b814-f7aeac6ceb6d
docset: aem65
exl-id: 8de78bde-2fcb-4221-873e-59e347ff2d74
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '3288'
ht-degree: 2%

---

# 워크플로우 단계 참조 {#workflow-step-reference}

워크플로우 모델은 다양한 유형의 일련의 단계로 구성됩니다. 유형에 따라 필요한 기능과 제어를 제공하기 위해 매개 변수와 스크립트를 사용하여 이러한 단계를 구성하고 확장할 수 있습니다.

>[!NOTE]
>
>이 섹션에서는 표준 워크플로우 단계를 다룹니다.
>
>모듈별 단계에 대해서는 다음을 참조하십시오.
>
>* [AEM Forms 워크플로우 단계 참조](/help/forms/using/aem-forms-workflow-step-reference.md)
* [Processing Assets Using Media Handlers and Workflows](/help/assets/media-handlers.md)



## 단계 속성 {#step-properties}

각 단계 구성 요소에는 필요한 속성을 정의하고 편집할 수 있는 **단계 속성** 대화 상자가 있습니다.

### 단계 속성 - 일반 탭 {#step-properties-common-tab}

속성 대화 상자의 **공통** 탭에서 대부분의 워크플로우 단계 구성 요소에 다음 속성의 조합을 사용할 수 있습니다.

* ****
제목 단계의 제목입니다.

* ****
설명 단계에 대한 설명입니다.

* **워크플로우 단계**

   [Stage](/help/sites-developing/workflows.md#workflow-stages)를 단계에 적용하는 드롭다운 선택기입니다.

* **시간 초과**

   단계가 &quot;시간 초과&quot;될 이후 기간입니다.
다음 중 하나를 선택할 수 있습니다.**해제**, **즉시**, **1h**, **6h**, **12h**, **24h**.

* **시간 초과 핸들러**

   단계가 시간 초과될 때 워크플로우를 제어하는 핸들러예:
   `Auto Advancer`

* **핸들러 진행**

   실행 후 워크플로우를 다음 단계로 자동으로 이동하려면 이 옵션을 선택합니다. 선택하지 않으면 구현 스크립트가 워크플로우 선진화를 처리해야 합니다.

### 단계 속성 - 사용자/그룹 탭 {#step-properties-user-group-tab}

많은 워크플로우 단계 구성 요소에 대해 속성 대화 상자의 **사용자/그룹** 탭에서 다음 속성을 사용할 수 있습니다.

* **사용자에게 이메일로 알립니다**

   * 워크플로우가 단계에 도달하면 참가자에게 이메일을 보내어 참가자에게 알릴 수 있습니다.
   * 활성화된 경우 **User/Group** 속성으로 정의된 사용자에게 이메일을 보내거나, 그룹이 정의된 경우 그룹의 각 구성원에게 이메일을 보냅니다.

* **사용자/그룹**

   * 드롭다운 선택 상자를 사용하여 사용자 또는 그룹을 탐색하고 선택할 수 있습니다.
   * 특정 사용자에게 단계를 지정하는 경우 이 사용자만 단계에서 작업을 수행할 수 있습니다.
   * 단계를 전체 그룹에 지정하는 경우, 워크플로우가 이 단계에 도달하면 이 그룹의 모든 사용자가 **Workflow 받은 편지함**&#x200B;에 작업을 수행합니다.
   * 자세한 내용은 [워크플로우에 참여](/help/sites-authoring/workflows-participating.md)를 참조하십시오.

## AND 분할 {#and-split}

**AND Split**&#x200B;은(는) 워크플로우에서 분할을 만들며, 그 뒤에는 두 분기가 모두 활성 상태가 됩니다. 필요에 따라 각 분기에 워크플로우 단계를 추가합니다. 이 단계를 통해 워크플로우에 여러 처리 경로를 도입할 수 있습니다. 예를 들어 특정 검토 단계를 동시에 수행하도록 허용하여 시간을 절약할 수 있습니다.

![wf-26](assets/wf-26.png)

### AND 분할 - 구성 {#and-split-configuration}

분할을 구성하려면

* **AND 분할 속성**&#x200B;을 편집합니다.

   * **분할 이름**:설명을 위해 이름을 지정하십시오
   * 필요한 분기 수를 선택합니다.2, 3, 4 또는 5.

* 필요에 따라 분기에 워크플로우 단계를 추가합니다.

   ![wf-27](assets/wf-27.png)

## 컨테이너 단계 {#container-step}

컨테이너 단계는 하위 워크플로우로 실행되는 다른 워크플로우 모델을 시작합니다.

이 컨테이너를 사용하면 워크플로우 모델을 재사용하여 단계의 일반적인 시퀀스를 구현할 수 있습니다. 예를 들어 번역 워크플로우 모델은 여러 편집 워크플로우에서 사용할 수 있습니다.

![wf-28](assets/wf-28.png)

### 컨테이너 단계 - 구성 {#container-step-configuration}

단계를 구성하려면 다음 탭을 편집하고 사용합니다.

* [일반](#step-properties-common-tab)
* **컨테이너**

   * **하위 워크플로우**:시작할 워크플로우를 선택합니다.

## 이동 단계 {#goto-step}

**이동 단계**&#x200B;를 사용하면 워크플로우 모델에서 실행할 다음 단계를 지정할 수 있습니다. 규칙 정의, 외부 스크립트 또는 ECMA 스크립트를 라우팅 표현식으로 지정하여 워크플로우 모델의 다음 단계를 평가할 수 있습니다.

* 지정하는 조건이 true인 경우 **이동 단계**&#x200B;가 완료되고 워크플로우 엔진이 지정된 단계를 실행합니다.
* 지정하는 조건이 true를 갖지 않으면 **이동 단계**&#x200B;가 완료되고 일반 라우팅 로직이 실행할 다음 단계를 결정합니다.

**이동 단계**&#x200B;를 사용하면 워크플로우 모델에서 고급 라우팅 구조를 구현할 수 있습니다. 예를 들어 루프를 구현하기 위해 루프 조건을 평가하는 라우팅 표현식을 사용하여 워크플로우에서 이전 단계를 실행하도록 **이동 단계**&#x200B;를 정의할 수 있습니다.

### 이동 단계 - 구성 {#goto-step-configuration}

단계를 구성하려면 다음 탭을 편집하고 사용합니다.

* [일반](#step-properties-common-tab)
* **프로세스**

   * **Target 단계**:라우팅 표현식의 조건을 평가한 후 실행할 단계를 선택합니다.
   * **라우팅 표현식**:규칙 정의, 외부 스크립트 또는  **Target 단계** 실행 여부를 결정하는 ECMA 스크립트를 선택합니다.

      * **규칙 정의:** 표현식  [편집기를 ](/help/forms/using/variable-in-aem-workflows.md#use-expression-editor) 사용하여 규칙을 정의합니다.
      * **외부 스크립트:**  외부 스크립트의 경로입니다.
      * **ECMA 스크립트**:이동 단계를 실행할지 여부를 결정하는  **스크립트입니다**.

#### 루프({#simulating-a-for-loop})에 대한 시뮬레이션

for 루프를 시뮬레이션하려면 발생한 루프 반복 횟수 개수를 유지해야 합니다.

* 개수는 일반적으로 워크플로우에서 작동하는 항목의 인덱스를 나타냅니다.
* 개수는 루프의 종료 기준으로 평가됩니다.

예를 들어 여러 JCR 노드에서 작업을 수행하는 워크플로우를 구현하려면 루프 카운터를 노드의 인덱스로 사용할 수 있습니다. 카운트를 유지하려면 워크플로우 인스턴스의 데이터 맵에 `integer` 값을 저장합니다. **이동 단계**&#x200B;의 스크립트를 사용하여 카운트를 증가시키고 카운트를 종료 기준과 비교하십시오.

```
function check(){
   var count=0;
   var keyname="loopcount"
   try{
      if (workflowData.getMetaDataMap().containsKey(keyname)){
        log.info("goto script: found loopcount key");
        count= parseInt(workflowData.getMetaDataMap().get(keyname))+1;
      }

     workflowData.getMetaDataMap().put(keyname,count);

     }catch(err) {
         log.info(err.message);
         return false;
    }
   if (parseInt(count) <7){
       return true;
   } else {
      return false;
   }
}
```

### 규칙 정의를 사용하여 for 루프 시뮬레이션 {#simulateforloop}

규칙 정의 를 라우팅 표현식으로 사용하여 for 루프를 시뮬레이션할 수도 있습니다. [Long  **** ](/help/forms/using/variable-in-aem-workflows.md#create-a-variable) 데이터 유형의 Countvariables를 만듭니다. **변수 설정](/help/sites-developing/using-variables-in-aem-workflows.md#set-a-variable)** 단계에서 **표현식**&#x200B;을 매핑 모드로 사용하여 **count** 변수의 값을 **수 + 1** 단계의 각 실행에 대해 **[로 설정합니다.**

![for 루프 시뮬레이션](assets/variable_use_case_count_new.png)

**이동 단계**&#x200B;에서 **변수 설정**&#x200B;을 **Target 단계** 로 사용하고, **개수 &lt; 5**&#x200B;를 라우팅 식으로 사용합니다.

![for 루프 시뮬레이션 조건](assets/variable_use_case_count1_new.png)

**변수 설정** 단계는 값이 5에 도달할 때까지 각 실행에서 **count** 변수의 값을 1씩 반복적으로 증가시킵니다.

## OR 분할 {#or-split}

**OR 분할**&#x200B;은 워크플로우에서 분할을 만들며, 그 뒤에는 하나의 분기만 활성화됩니다. 이 단계를 통해 워크플로우에 조건부 처리 경로를 도입할 수 있습니다. 필요에 따라 각 분기에 워크플로우 단계를 추가합니다.

>[!NOTE]
OR 분할 생성에 대한 자세한 내용은 다음을 참조하십시오.[https://helpx.adobe.com/experience-manager/using/aem64_workflow_servlet.html](https://helpx.adobe.com/experience-manager/using/aem64_workflow_servlet.html)

![OR 분할을 사용하여 분기](assets/variables_orsplit_new.png)

### OR 분할 - 구성 {#or-split-configuration}

분할을 구성하려면

* **OR 분할 속성**&#x200B;을 편집합니다.

   * **일반**

      * 분할 이름을 지정합니다.
   * **분기(*x)***

      * **분기 추가:**  단계에 분기를 더 추가합니다.
      * **라우팅 표현식** 선택:활성 분기를 평가할 라우팅 표현식을 선택합니다. 가능한 값은 다음과 같습니다.규칙 정의, 외부 스크립트 및 ECMA 스크립트.
      * **표현식 추가를 클릭합니다**.라우팅 표현식으로 규칙 정의를  **선택하면 활성 분기** 를 평가할 표현식을 추가합니다.
      * **스크립트 경로**:라우팅 표현식에서 외부 스크립트( **External Scripts)를 선택하는 경우 활성 분기를 평가하는 스크립트가** 포함된 파일의 경로입니다.
      * **스크립트**:ECMA 스크립트(ECMA Scripts)를 라우팅 표현식 **으로 선택하는 경우 활성 분기** 를 평가할 스크립트를 상자에 추가합니다.
      * **기본 경로**:여러 분기의 경우 기본 분기 뒤에 옵니다. 하나의 분기만 기본값으로 지정할 수 있습니다.

   >[!NOTE]
   * 공정순서 표현식을 기준으로 한 번에 하나의 분기가 평가됩니다.
   * 분기는 위에서 아래로 평가된다.
   * true로 평가되는 첫 번째 스크립트가 실행됩니다.
   * 분기가 true로 평가되지 않으면 워크플로우가 진행되지 않습니다.


   >[!NOTE]
   [OR Split](/help/sites-developing/workflows-models.md#defineruleecmascript)에 대한 규칙 정의 를 참조하십시오.

* 필요에 따라 분기에 워크플로우 단계를 추가합니다.

## 참가자 단계 및 선택기 {#participant-steps-and-choosers}

### 참가자 단계 {#participant-step}

**참가자 단계**&#x200B;를 사용하면 특정 작업에 대한 소유권을 할당할 수 있습니다. 워크플로우는 사용자가 단계를 수동으로 인식하는 경우에만 진행됩니다. 다른 사람이 워크플로우에서 작업을 수행하도록 할 때 사용됩니다.예를 들어, 검토 단계입니다.

직접 관련되지는 않지만 작업을 지정할 때 사용자 인증을 고려해야 합니다.사용자는 워크플로우 페이로드인 페이지에 액세스할 수 있어야 합니다.

#### 참가자 단계 - 구성 {#participant-step-configuration}

단계를 구성하려면 다음 탭을 편집하고 사용합니다.

* [일반](#step-properties-common-tab)
* [사용자/그룹](#step-properties-user-group-tab)

>[!NOTE]
다음과 같은 경우 워크플로우 이니시에이터에 항상 알림을 보냅니다.
* 워크플로우가 완료됨(완료됨).
* 워크플로우가 중단되었습니다(종료됨).



>[!NOTE]
이메일 알림을 활성화하려면 일부 속성을 구성해야 합니다. 이메일 템플릿을 사용자 정의하거나 새 언어의 이메일 템플릿을 추가할 수도 있습니다. AEM에서 이메일 알림을 구성하려면 [이메일 알림 구성](/help/sites-administering/notification.md#configuringemailnotification)을 참조하십시오.

### 대화 상자 참가자 단계 {#dialog-participant-step}

작업 항목이 지정된 사용자로부터 정보를 수집하려면 **대화 상자 참가자 단계**&#x200B;를 사용하십시오. 이 단계는 나중에 워크플로우에서 사용되는 소량의 데이터를 수집하는 데 유용합니다.

단계를 완료하면 **작업 항목 완료** 대화 상자에 대화 상자에서 정의한 필드가 포함됩니다. 필드에 수집된 데이터는 워크플로우 페이로드의 노드에 저장됩니다. 그런 다음 후속 워크플로우 단계에서 저장소에서 값을 읽을 수 있습니다.

단계를 구성하려면 작업 항목을 지정할 그룹 또는 사용자를 지정하고 대화 상자의 경로를 지정합니다.

#### 대화 상자 참가자 단계 - 구성 {#dialog-participant-step-configuration}

단계를 구성하려면 다음 탭을 편집하고 사용합니다.

* [일반](#step-properties-common-tab)
* [사용자/그룹](#step-properties-user-group-tab)
* **대화 상자**

   * **대화 상자 경로**:작성하는 대화 상자의 대화 상자  [노드에 대한 경로입니다](#dialog-participant-step-creating-a-dialog).

#### 대화 상자 참가자 단계 - 대화 상자 {#dialog-participant-step-creating-a-dialog} 만들기

대화 상자를 만들려면 대화 상자를 만들어야 합니다.

* 결과 데이터가 페이로드](#dialog-participant-step-storing-data-in-the-payload)에 저장되는 위치를 결정합니다.[
* [대화 상자를 정의합니다.여기에는 데이터를 수집(및 저장하는 데 사용되는 필드를 정의하는 작업이 포함됩니다](#dialog-participant-step-dialog-definition).

#### 대화 상자 참가자 단계 - 페이로드에 데이터 저장 {#dialog-participant-step-storing-data-in-the-payload}

위젯 데이터를 워크플로우 페이로드 또는 작업 항목 메타데이터에 저장할 수 있습니다. 위젯 노드의 `name` 속성 형식은 데이터가 저장되는 위치를 결정합니다.

* **페이로드를 사용하여 데이터 저장**

   * 위젯 데이터를 워크플로우 페이로드의 속성으로 저장하려면 위젯 노드의 이름 속성 값에 다음 형식을 사용하십시오.
      `./jcr:content/nodename`

   * 데이터는 페이로드 노드의 `nodename` 속성에 저장됩니다. 노드에 해당 속성이 없으면 속성이 만들어집니다.
   * 페이로드로 저장할 때 동일한 페이로드로 대화 상자를 계속 사용하면 속성 값을 덮어씁니다.

* **작업 항목으로 데이터 저장**

   * 위젯 데이터를 작업 항목 메타데이터의 속성으로 저장하려면 이름 속성 값에 다음 형식을 사용하십시오.
      `nodename`

   * 데이터는 작업 항목 `metadata`의 `nodename` 속성에 저장됩니다. 나중에 동일한 페이로드와 함께 대화 상자가 사용되는 경우 데이터가 유지됩니다.

#### 대화 상자 참가자 단계 - 대화 상자 정의 {#dialog-participant-step-dialog-definition}

1. **대화 상자 구조**

   대화 상자 참가자 단계에 대한 대화 상자는 구성 요소 작성을 위해 만드는 대화 상자와 유사합니다. 이러한 파일은 다음 위치에 저장됩니다.

   `/apps/myapp/workflow/dialogs`

   표준 터치 지원 UI에 대한 대화 상자의 노드 구조는 다음과 같습니다.

   ```xml
   newComponent (cq:Component)
     |- cq:dialog (nt:unstructured)
       |- content
         |- layout
           |- items
             |- column
               |- items
                 |- component0
                 |- component1
                 |- ...
   ```

   >[!NOTE]
   자세한 내용은 [대화 상자 만들기 및 구성](/help/sites-developing/developing-components.md#creating-and-configuring-a-dialog)을 참조하십시오.

1. **대화 상자 경로 속성**

   **대화 상자 참가자 단계**&#x200B;에는 **대화 상자 경로** 속성([참가자 단계](#participant-step)의 속성과 함께)이 있습니다. **대화 상자 경로** 속성 값은 대화 상자의 `dialog` 노드에 대한 경로입니다.

   예를 들어, 대화 상자는 노드에 저장된 `EmailWatch` 구성 요소에 들어 있습니다.

   `/apps/myapp/workflows/dialogs`

   터치 지원 UI의 경우 **대화 상자 경로** 속성에 다음 값이 사용됩니다.

   `/apps/myapp/workflow/dialogs/EmailWatch/cq:dialog`

   ![wf-30](assets/wf-30.png)

1. **예제 대화 상자 정의**

   다음 XML 코드 조각은 페이로드 컨텐츠의 `watchEmail` 노드에 `String` 값을 저장하는 대화 상자를 나타냅니다. 제목 노드는 [TextField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/components/coral/foundation/form/textfield/index.html) 구성 요소를 나타냅니다.

   ```xml
   jcr:primaryType="nt:unstructured"
       jcr:title="Watcher Email Address Dialog"
       sling:resourceType="cq/gui/components/authoring/dialog">
       <content jcr:primaryType="nt:unstructured"
           sling:resourceType="granite/ui/components/foundation/container">
           <layout jcr:primaryType="nt:unstructured"
               margin="false"
               sling:resourceType="granite/ui/components/foundation/layouts/fixedcolumns"
           />
           <items jcr:primaryType="nt:unstructured">
               <column jcr:primaryType="nt:unstructured"
                   sling:resourceType="granite/ui/components/foundation/container">
                   <items jcr:primaryType="nt:unstructured">
                       <title jcr:primaryType="nt:unstructured"
                           fieldLabel="Notification Email Address"
                           name="./jcr:content/watchEmails"
                           sling:resourceType="granite/ui/components/foundation/form/textfield"
                       />
                   </items>
               </column>
           </items>
       </content>
   </cq:dialog>
   ```

   이 예는 터치 지원 UI의 경우 다음과 같은 대화 상자가 표시됩니다.

   ![chlimage_1-70](assets/chlimage_1-70.png)

### 동적 참가자 단계 {#dynamic-participant-step}

**동적 참가자 단계** 구성 요소는 **[참가자 단계](#participant-step)**&#x200B;와 유사하며, 런타임에 참가자가 자동으로 선택된다는 차이점이 있습니다.

단계를 구성하려면 작업 항목을 지정할 참여자를 식별하는 **참가자 선택기**&#x200B;를 대화 상자와 함께 선택합니다.

#### 동적 참가자 단계 - 구성 {#dynamic-participant-step-configuration}

단계를 구성하려면 다음 탭을 편집하고 사용합니다.

* [일반](#step-properties-common-tab)
* **참가자 선택기**

   * **참가자 선택기**:생성하는  [참가자 선택기의 이름입니다](#developingtheparticipantchooser).
   * **인수**:필요한 인수
   * **이메일**:사용자에게 이메일 알림을 전송해야 하는지 여부.

* **대화 상자**

   * **대화 상자 경로**:대화 상자 참가자  [단계 **와 같이 사용자가 만드는 대화 상자의**&#x200B;대화 상자 노드에 대한 경로입니다.](#dialog-participant-step-creating-a-dialog)

#### 동적 참가자 단계 - 참가자 선택기 개발 {#dynamic-participant-step-developing-the-participant-chooser}

참가자 선택기를 생성합니다. 따라서 선택 로직이나 기준을 사용할 수 있습니다. 예를 들어, 참가자 선택자는 가장 적은 작업 항목이 있는 사용자(그룹 내)를 선택할 수 있습니다. 워크플로우 모델에서 **동적 참가자 단계** 구성 요소의 다른 인스턴스에 사용할 참가자 선택기를 원하는 수만큼 만들 수 있습니다.

작업 항목을 지정할 사용자를 선택하는 OSGi 서비스 또는 ECMAScript를 만듭니다.

* **ECMAscript**

   스크립트에는 사용자 ID를 `String` 값으로 반환하는 getParticipant라는 함수가 포함되어야 합니다. 사용자 지정 스크립트를 `/apps/myapp/workflow/scripts` 폴더 또는 하위 폴더 등에 저장합니다.

   샘플 스크립트는 표준 AEM 인스턴스에 포함됩니다.

   `/libs/workflow/scripts/initiator-participant-chooser.ecma`

   >[!CAUTION]
   ***은 `/libs` 경로에서 아무 것도 변경하지 않아야 합니다.***
   이는 다음 번에 인스턴스를 업그레이드할 때 `/libs` 컨텐츠를 덮어쓰게 되기 때문입니다(핫픽스 또는 기능 팩을 적용할 때 덮어쓸 수 있음).

   이 스크립트는 워크플로우 개시자를 참가자로 선택합니다.

   ```
   function getParticipant() {
       return workItem.getWorkflow().getInitiator();
   }
   ```

   >[!NOTE]
   **워크플로우 개시자 참가자 선택기** 구성 요소는 **동적 참가자 단계**&#x200B;를 확장하고 이 스크립트를 단계 구현으로 사용합니다.

* **OSGi 서비스**

   서비스는 [com.day.cq.workflow.exec.ParticipantStepSelector](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/workflow/exec/ParticipantStepChooser.html) 인터페이스를 구현해야 합니다. 인터페이스는 다음 멤버를 정의합니다.

   * `SERVICE_PROPERTY_LABEL` 필드:이 필드를 사용하여 참가자 선택기의 이름을 지정합니다. 이 이름은 **동적 참가자 단계** 속성의 사용 가능한 참가자 선택기 목록에 나타납니다.

   * `getParticipant` 메서드:동적으로 확인된 주체 ID를 값으로  `String` 반환합니다.
   >[!CAUTION]
   `getParticipant` 메서드는 동적으로 확인된 주체 ID를 반환합니다. 그룹 ID 또는 사용자 ID일 수 있습니다.
   그러나 참가자 목록이 반환될 때 그룹 ID는 **참가자 단계**&#x200B;에만 사용할 수 있습니다. **동적 참가자 단계**&#x200B;에 대해 빈 목록이 반환되며 위임에 사용할 수 없습니다.

   **동적 참가자 단계** 구성 요소에서 구현을 사용할 수 있도록 하려면 Java 클래스를 서비스를 내보내는 OSGi 번들에 추가하고 번들을 AEM 서버에 배포합니다.

   >[!NOTE]
   **임의 참가자 임의** 사용자(  `com.day.cq.workflow.impl.process.RandomParticipantChooser`)를 선택하는 샘플 서비스를 선택합니다. **임의의 참가자 선택**&#x200B;단계 구성 요소 샘플은 **동적 참가자 단계**&#x200B;를 확장하고 이 서비스를 단계 구현으로 사용합니다.

#### 동적 참가자 단계 - 예제 참가자 선택기 서비스 {#dynamic-participant-step-example-participant-chooser-service}

다음 Java 클래스는 `ParticipantStepChooser` 인터페이스를 구현합니다. 클래스는 워크플로우를 시작한 참가자의 이름을 반환합니다. 코드는 샘플 스크립트(`initiator-participant-chooser.ecma`)에서 사용하는 것과 동일한 논리를 사용합니다.

`@Property` 주석은 `SERVICE_PROPERTY_LABEL` 필드의 값을 `Workflow Initiator Participant Chooser`로 설정합니다.

```java
package com.adobe.example;

import org.apache.felix.scr.annotations.Component;
import org.apache.felix.scr.annotations.Properties;
import org.apache.felix.scr.annotations.Property;
import org.apache.felix.scr.annotations.Service;
import org.osgi.framework.Constants;
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;

import com.adobe.granite.workflow.WorkflowException;
import com.adobe.granite.workflow.WorkflowSession;
import com.adobe.granite.workflow.exec.ParticipantStepChooser;
import com.adobe.granite.workflow.exec.WorkItem;
import com.adobe.granite.workflow.metadata.MetaDataMap;

@Component
@Service
@Properties({
        @Property(name = Constants.SERVICE_DESCRIPTION, value = "An example implementation of a dynamic participant chooser."),
        @Property(name = ParticipantStepChooser.SERVICE_PROPERTY_LABEL, value = "Workflow Initiator Participant Chooser (service)") })
public class InitiatorParticipantChooser implements ParticipantStepChooser {

 private Logger logger = LoggerFactory.getLogger(this.getClass());

 public String getParticipant(WorkItem arg0, WorkflowSession arg1,
   MetaDataMap arg2) throws WorkflowException {

  String initiator = arg0.getWorkflow().getInitiator();
  logger.info("Assigning Dynamic Participant Step work item to {}",initiator);

  return initiator;
 }
}
```

**동적 참가자 단계** 속성 대화 상자에서 **참가자 선택기** 목록에는 이 서비스를 나타내는 `Workflow Initiator Participant Chooser (script)` 항목이 포함되어 있습니다.

워크플로우 모델이 시작되면, 로그는 워크플로우를 시작한 사용자의 ID와 작업 항목이 지정된 사용자를 나타냅니다. 이 예에서는 `admin` 사용자가 워크플로우를 시작했습니다.

`13.09.2015 15:48:53.037 *INFO* [10.176.129.223 [1347565733037] POST /etc/workflow/instances HTTP/1.1] com.adobe.example.InitiatorParticipantChooser Assigning Dynamic Participant Step work item to admin`

### 양식 참가자 단계 {#form-participant-step}

**양식 참가자 단계**&#x200B;는 작업 항목을 열 때 양식을 표시합니다. 사용자가 양식을 작성하고 제출하면 필드 데이터가 워크플로우 페이로드의 노드에 저장됩니다.

단계를 구성하려면 작업 항목을 지정할 그룹 또는 사용자를 지정하고 양식의 경로를 지정합니다.

>[!CAUTION]
이 섹션에서는 페이지 작성을 위한 기초 구성 요소의 [Forms 섹션에 대해 설명합니다](/help/sites-authoring/default-components-foundation.md#form).

#### 양식 참가자 단계 - 구성 {#form-participant-step-configuration}

단계를 구성하려면 다음 탭을 편집하고 사용합니다.

* [일반](#step-properties-common-tab)
* [사용자/그룹](#step-properties-user-group-tab)
* **양식**

   * **양식 경로**:사용자가 만드는  [양식의 경로입니다](#form-participant-step-creating-the-form).

#### 양식 참가자 단계 - {#form-participant-step-creating-the-form} 양식 만들기

**양식 참가자 단계**&#x200B;와 함께 사용할 양식을 만듭니다. 그러나 양식 참가자 단계의 양식에는 다음 구성이 있어야 합니다.

* **양식 시작** 구성 요소에는 **작업 유형** 속성이 `Edit Workflow Controlled Resource(s)`로 설정되어 있어야 합니다.
* **Start of Form** 구성 요소에는 `Form Identifier` 속성에 대한 값이 있어야 합니다.
* 양식 구성 요소에는 필드 데이터가 저장되는 노드의 경로로 설정된 **요소 이름** 속성이 있어야 합니다. 경로는 워크플로우 페이로드 컨텐츠에서 노드를 찾아야 합니다. 값은 다음 형식을 사용합니다.

   `./jcr:content/path_to_node`

* 양식에는 **워크플로우 제출 단추** 구성 요소가 포함되어야 합니다. 구성 요소의 속성은 구성하지 않습니다.

워크플로우의 요구 사항은 필드 데이터를 저장할 위치를 결정합니다. 예를 들어 필드 데이터를 사용하여 페이지 컨텐츠의 속성을 구성할 수 있습니다. **요소 이름** 속성의 다음 값은 필드 데이터를 `jcr:content` 노드의 `redirectTarget` 속성 값으로 저장합니다.

`./jcr:content/redirectTarget`

다음 예에서 필드 데이터는 페이로드 페이지에서 **Text** 구성 요소의 컨텐츠로 사용됩니다.

`./jcr:content/par/text_3/text`

첫 번째 예는 `cq:Page` 구성 요소가 렌더링하는 모든 페이지에 사용할 수 있습니다. 두 번째 예제는 페이로드 페이지에 ID가 `text_3`인 **Text** 구성 요소가 포함된 경우에만 사용할 수 있습니다.

양식은 저장소의 어느 곳에서든 찾을 수 있지만 워크플로 사용자는 양식을 읽을 수 있는 권한을 부여받아야 합니다.

### 임의 참가자 선택기 {#random-participant-chooser}

**임의 참가자 선택기** 단계는 생성된 작업 항목을 목록에서 임의로 선택한 사용자에게 지정하는 참가자 선택기입니다.

![wf-31](assets/wf-31.png)

#### 임의 참가자 선택기 - 구성 {#random-participant-chooser-configuration}

단계를 구성하려면 다음 탭을 편집하고 사용합니다.

* [일반](#step-properties-common-tab)
* **인수**

   * **참가자**:선택할 수 있는 사용자 목록을 지정합니다. 사용자를 목록에 추가하려면 **항목 추가**&#x200B;를 클릭하고 사용자 노드나 사용자 ID의 홈 경로를 입력합니다. 사용자 순서는 작업 항목이 할당될 가능성에 영향을 주지 않습니다.

### 워크플로우 개시자 참가자 선택기 {#workflow-initiator-participant-chooser}

**워크플로우 개시자 참가자 선택기** 단계는 생성된 작업 항목을 워크플로우를 시작한 사용자에게 지정하는 참가자 선택기입니다. **Common** 속성 외에 구성할 속성이 없습니다.

#### 워크플로우 개시자 참가자 선택기 - 구성 {#workflow-initiator-participant-chooser-configuration}

단계를 구성하려면 다음 탭을 사용하여 편집합니다.

* [일반](#step-properties-common-tab)

## 프로세스 단계 {#process-step}

**프로세스 단계**&#x200B;는 ECMAScript를 실행하거나 OSGi 서비스를 호출하여 자동 처리를 수행합니다.

![wf-32](assets/wf-32.png)

### 프로세스 단계 - 구성 {#process-step-configuration}

단계를 구성하려면 다음 탭을 편집하고 사용합니다.

* [일반](#step-properties-common-tab)
* **프로세스**

   * **프로세스**:실행할 프로세스 구현입니다. 드롭다운 메뉴를 사용하여 ECMAScript 또는 OSGi 서비스를 선택합니다. 다음에 대한:

      * 표준 ECMASripts 및 OSGi 서비스는 [프로세스 단계에 대한 내장 프로세스](/help/sites-developing/workflows-process-ref.md)를 참조하십시오.
      * 프로세스 단계에 대한 ECMAScript 만들기를 참조하십시오. [ECMAScript](/help/sites-developing/workflows-customizing-extending.md#using-ecmascript)로 프로세스 단계 구현 을 참조하십시오.
      * 프로세스 단계에 대한 OSGi 서비스 만들기를 참조하십시오. [Java 클래스를 사용하는 프로세스 단계 구현](/help/sites-developing/workflows-customizing-extending.md#implementing-a-process-step-with-a-java-class)을 참조하십시오.
   * **핸들러 고급**:실행 후 워크플로우를 다음 단계로 자동으로 이동하려면 이 옵션을 선택합니다. 선택하지 않으면 구현 스크립트가 워크플로우 선진화를 처리해야 합니다.
   * **인수**:프로세스에 전달할 인수.


## 변수 설정 {#set-variable}

변수 설정 단계를 사용하면 변수의 값을 설정하고 값이 설정되는 순서를 정의할 수 있습니다. 변수는 변수 매핑이 변수 설정 단계에서 나열된 순서로 설정됩니다.

![매핑을 추가하여 변수 설정](assets/set_variable_addmappingnew.png)

### 변수 설정 - 구성 {#setvariable}

단계를 구성하려면 다음 탭을 편집하고 사용합니다.

* [일반](/help/sites-developing/workflows-step-ref.md#step-properties-common-tab)
* **매핑**

   * **변수 선택:**  이 옵션을 사용하여 값을 설정할 변수를 선택합니다.
   * **매핑 모드 선택:**  매핑 모드를 선택하여 변수에 대한 값을 설정합니다. 변수의 데이터 유형에 따라 다음 옵션을 사용하여 변수의 값을 설정할 수 있습니다.

      * **리터럴:**  지정할 정확한 값을 알고 있는 경우 옵션을 사용합니다.
      * **표현식:** 사용할 값이 표현식을 기반으로 계산되면 옵션을 사용합니다. 표현식은 제공된 표현식 편집기에서 만들어집니다.
      * **JSON 점 표기법:**  옵션을 사용하여 JSON 또는 FDM 유형 변수에서 값을 검색합니다.
      * **XPATH:** XML 유형 변수에서 값을 검색하려면 옵션을 사용합니다.
      * **페이로드에 상대:** 페이로드를 기준으로 하는 경로에서 변수에 저장할 값을 사용할 수 있는 경우 옵션을 사용합니다.
      * **절대 경로:** 절대 경로에서 변수에 저장할 값을 사용할 수 있는 경우 옵션을 사용합니다.
   * **값 지정:**  변수에 매핑할 값을 지정합니다. 이 필드에서 지정하는 값은 매핑 모드에 따라 다릅니다.
   * **매핑 추가:**  이 옵션을 사용하여 변수에 대한 값을 설정할 매핑을 더 추가합니다.
