---
title: 워크플로 단계 참조
description: Adobe Experience Manager의 워크플로에 대해서는 이 단계 참조 를 참조하십시오.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
docset: aem65
exl-id: 8de78bde-2fcb-4221-873e-59e347ff2d74
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '3227'
ht-degree: 2%

---

# 워크플로 단계 참조 {#workflow-step-reference}

워크플로우 모델은 다양한 유형의 일련의 단계로 구성됩니다. 유형에 따라 이러한 단계를 매개 변수와 스크립트를 사용하여 구성하고 확장하여 필요한 기능과 컨트롤을 제공할 수 있습니다.

>[!NOTE]
>
>이 섹션에서는 표준 워크플로우 단계를 다룹니다.
>
>모듈별 단계는 다음을 참조하십시오.
>
>* [AEM Forms 워크플로 단계 참조](/help/forms/using/aem-forms-workflow-step-reference.md)
>* [미디어 처리기 및 워크플로를 사용하여 Assets 처리](/help/assets/media-handlers.md)
>

## 단계 속성 {#step-properties}

각 단계 구성 요소에는 필요한 속성을 정의하고 편집할 수 있는 **단계 속성** 대화 상자가 있습니다.

### 단계 속성 - 공통 탭 {#step-properties-common-tab}

속성 대화 상자의 **공통** 탭에서 대부분의 워크플로 단계 구성 요소에 대해 다음 속성을 조합하여 사용할 수 있습니다.

* **제목**
단계의 제목입니다.

* **설명**
단계에 대한 설명입니다.

* **워크플로 단계**

  단계에 [단계](/help/sites-developing/workflows.md#workflow-stages)을(를) 적용하는 드롭다운 선택기입니다.

* **시간 초과**

  이후 단계가 &quot;시간 초과&quot;되는 기간입니다.
다음 중 하나를 선택할 수 있습니다. **해제**, **즉시**, **1h**, **6h**, **12h**, **24h**.

* **시간 제한 처리기**

  단계 제한 시간이 초과되면 워크플로우를 제어하는 핸들러입니다. 예, `Auto Advancer`

* **핸들러 진행**

  실행 후 워크플로우를 자동으로 다음 단계로 이동하려면 이 옵션을 선택합니다. 선택하지 않은 경우 구현 스크립트는 워크플로우 개선을 처리해야 합니다.

### 단계 속성 - 사용자/그룹 탭 {#step-properties-user-group-tab}

다음 속성은 속성 대화 상자의 **사용자/그룹** 탭에서 여러 워크플로 단계 구성 요소에 사용할 수 있습니다.

* **전자 메일로 사용자에게 알림**

   * 워크플로우가 단계에 도달하면 이메일을 보내어 참가자에게 알립니다.
   * 활성화된 경우 **사용자/그룹** 속성으로 정의된 사용자에게 전자 메일이 전송되거나 그룹이 정의된 경우 그룹의 각 구성원에게 전자 메일이 전송됩니다.

* **사용자/그룹**

   * 드롭다운 선택 상자를 사용하여 사용자 또는 그룹으로 이동하여 선택할 수 있습니다.
   * 특정 사용자에게 단계를 할당하면 이 사용자만 단계에서 작업을 수행할 수 있습니다.
   * 단계를 전체 그룹에 할당한 경우 워크플로가 이 단계에 도달하면 이 그룹의 모든 사용자는 **워크플로 받은 편지함**&#x200B;에서 작업을 수행할 수 있습니다.
   * 자세한 내용은 [워크플로에 참여](/help/sites-authoring/workflows-participating.md)를 참조하십시오.

## AND 분할 {#and-split}

**AND Split**&#x200B;은(는) 워크플로우에서 분할을 만들고 그 후 두 분기가 활성화됩니다. 필요에 따라 각 분기에 워크플로 단계를 추가합니다. 이 단계를 통해 워크플로우에 여러 처리 경로를 도입할 수 있습니다. 예를 들어 특정 검토 단계를 동시에 수행하도록 하여 시간을 절약할 수 있습니다.

![wf-26](assets/wf-26.png)

### AND 분할 - 구성 {#and-split-configuration}

분할을 구성하려면 다음을 수행합니다.

* **AND 분할 속성**&#x200B;을(를) 편집합니다.

   * **분할 이름**: 설명을 위해 이름을 지정하십시오.
   * 필요한 분기 수를 선택합니다(2, 3, 4 또는 5).

* 필요에 따라 분기에 워크플로우 단계를 추가합니다.

  ![wf-27](assets/wf-27.png)

## 컨테이너 단계 {#container-step}

컨테이너 단계는 하위 워크플로우로 실행되는 다른 워크플로우 모델을 시작합니다.

이 컨테이너를 사용하면 워크플로우 모델을 재사용하여 일반적인 단계 시퀀스를 구현할 수 있습니다. 예를 들어 번역 워크플로 모델은 여러 편집 워크플로에서 사용할 수 있습니다.

![wf-28](assets/wf-28.png)

### 컨테이너 단계 - 구성 {#container-step-configuration}

단계를 구성하려면 다음 탭을 편집하고 사용합니다.

* [일반](#step-properties-common-tab)
* **컨테이너**

   * **하위 워크플로**: 시작할 워크플로를 선택하십시오.

## 이동 단계 {#goto-step}

**이동 단계**&#x200B;를 사용하면 워크플로우 모델에서 실행할 다음 단계를 지정할 수 있습니다. 규칙 정의, 외부 스크립트 또는 ECMA 스크립트를 라우팅 표현식으로 지정하여 워크플로우 모델의 다음 단계를 평가할 수 있습니다.

* 지정한 조건이 true이면 **이동 단계**&#x200B;가 완료되고 워크플로 엔진이 지정된 단계를 실행합니다.
* 지정한 조건이 true가 아니면 **이동 단계**&#x200B;가 완료되고 일반 라우팅 로직이 실행할 다음 단계를 결정합니다.

**이동 단계**&#x200B;를 사용하면 워크플로우 모델에서 고급 라우팅 구조를 구현할 수 있습니다. 예를 들어, 루프를 구현하기 위해 **이동 단계**&#x200B;를 정의하여 워크플로우에서 이전 단계를 실행할 수 있습니다. 이때 라우팅 식은 루프 조건을 평가합니다.

### 이동 단계 - 구성 {#goto-step-configuration}

단계를 구성하려면 다음 탭을 편집하고 사용합니다.

* [일반](#step-properties-common-tab)
* **프로세스**

   * **대상 단계**: 라우팅 식의 조건을 평가한 후 실행할 단계를 선택합니다.
   * **라우팅 식**: **대상 단계**&#x200B;를 실행할지 여부를 결정하는 규칙 정의, 외부 스크립트 또는 ECMA 스크립트를 선택하십시오.

      * **규칙 정의:** [표현식 편집기](/help/forms/using/variable-in-aem-workflows.md#use-expression-editor)를 사용하여 규칙을 정의합니다.
      * **외부 스크립트:** 외부 스크립트의 경로입니다.
      * **ECMA 스크립트**: **이동 단계**&#x200B;를 실행할지 여부를 결정하는 스크립트.

#### for 루프 시뮬레이션 {#simulating-a-for-loop}

&quot;for 루프&quot;를 시뮬레이트하려면 발생한 루프 반복 횟수 카운트를 유지 관리해야 합니다.

* 카운트는 일반적으로 워크플로우에서 수행되는 항목의 인덱스를 나타냅니다.
* 카운트는 루프의 종료 기준으로 평가됩니다.

예를 들어 여러 JCR 노드에서 작업을 수행하는 워크플로우를 구현하려면 루프 카운터를 노드의 인덱스로 사용할 수 있습니다. 카운트를 유지하려면 워크플로 인스턴스의 데이터 맵에 `integer` 값을 저장하십시오. 카운트를 증가시키고 카운트를 종료 기준과 비교하려면 **이동 단계**&#x200B;의 스크립트를 사용하십시오.

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

규칙 정의(Rule Definition)를 라우팅 표현식으로 사용하여 for 루프를 시뮬레이션할 수도 있습니다. [Long 데이터 형식의 **count** 변수를 만듭니다](/help/forms/using/variable-in-aem-workflows.md#create-a-variable). **[변수 설정](/help/sites-developing/using-variables-in-aem-workflows.md#set-a-variable)** 단계에서 **식**&#x200B;을(를) 매핑 모드로 사용하여 **변수 설정** 단계의 각 실행 시 **count** 변수의 값을 **count + 1**(으)로 설정합니다.

![for 루프 시뮬레이션](assets/variable_use_case_count_new.png)

**이동 단계**&#x200B;에서 **변수 설정**&#x200B;을 **대상 단계**(으)로 사용하고 **개수 &lt; 5**&#x200B;을(를) 라우팅 식으로 사용합니다.

![for 루프를 시뮬레이션하는 조건](assets/variable_use_case_count1_new.png)

**변수 설정** 단계는 반복적으로 실행되며, 값이 5에 도달할 때까지 각 실행에서 **count** 변수 값을 1씩 증가시킵니다.

## OR 분할 {#or-split}

**OR 분할**&#x200B;은(는) 워크플로우에서 분할을 만들고 그 후 하나의 분기만 활성화됩니다. 이 단계를 통해 조건부 처리 경로를 워크플로우에 도입할 수 있습니다. 필요에 따라 각 분기에 워크플로 단계를 추가합니다.

>[!NOTE]
>
>[또는 분할 단계](https://experienceleague.adobe.com/docs/experience-manager-65/developing/extending-aem/extending-workflows/using-variables-in-aem-workflows.html?lang=ko#use-a-variable)를 참조하십시오.

![OR 분할을 사용하여 분기](assets/variables_orsplit_new.png)

### OR 분할 - 구성 {#or-split-configuration}

분할을 구성하려면 다음을 수행합니다.

* **OR 분할 속성**&#x200B;을(를) 편집합니다.

   * **공통**

      * 분할 이름을 지정합니다.

   * **분기(*x)***

      * **분기 추가:** 단계에 분기를 더 추가합니다.
      * **라우팅 식 선택**: 활성 분기를 계산하려면 라우팅 식을 선택하십시오. 가능한 값은 규칙 정의, 외부 스크립트 및 ECMA 스크립트입니다.
      * **식을 추가하려면 클릭하세요**: 라우팅 식으로 **규칙 정의**&#x200B;를 선택한 경우 활성 분기를 평가할 식을 추가합니다.
      * **스크립트 경로**: 라우팅 식으로 **외부 스크립트**&#x200B;를 선택하는 경우 활성 분기를 평가하는 스크립트가 포함된 파일의 경로입니다.
      * **스크립트**: 라우팅 식으로 **ECMA 스크립트**&#x200B;를 선택하는 경우 활성 분기를 평가하도록 상자에 스크립트를 추가합니다.
      * **기본 경로**: 여러 분기가 있는 경우 기본 분기가 적용됩니다. 하나의 분기만 기본값으로 지정할 수 있습니다.

  >[!NOTE]
  >
  >    * 라우팅 표현식을 기반으로 한 번에 하나의 분기가 평가됩니다.
  >    * 분기는 위쪽에서 아래쪽으로 평가됩니다.
  >    * true로 평가되는 첫 번째 스크립트가 실행됩니다.
  >    * 참으로 평가되는 분기가 없으면 워크플로우가 진행되지 않습니다.
  >
  >

  >[!NOTE]
  >
  >[OR 분할에 대한 규칙 정의](/help/sites-developing/workflows-models.md#defineruleecmascript)를 참조하십시오.

* 필요에 따라 분기에 워크플로우 단계를 추가합니다.

## 참가자 단계 및 선택기 {#participant-steps-and-choosers}

### 참가자 단계 {#participant-step}

**참가자 단계**&#x200B;를 사용하면 특정 작업에 대한 소유권을 할당할 수 있습니다. 사용자가 단계를 수동으로 승인한 경우에만 워크플로우가 진행됩니다. 이 워크플로는 누군가가 워크플로를 수행하도록 할 때 사용됩니다. 예를 들어 검토 단계입니다.

직접 관련되지는 않지만 작업을 할당할 때 사용자 인증을 고려해야 합니다. 사용자는 워크플로우 페이로드인 페이지에 액세스할 수 있어야 합니다.

#### 참가자 단계 - 구성 {#participant-step-configuration}

단계를 구성하려면 다음 탭을 편집하고 사용합니다.

* [일반](#step-properties-common-tab)
* [사용자/그룹](#step-properties-user-group-tab)

>[!NOTE]
>
>워크플로 개시자는 다음과 같은 경우에 항상 알림을 받습니다.
>
>* 워크플로우가 완료(완료)되었습니다.
>* 워크플로우가 중단(종료)됩니다.
>

>[!NOTE]
>
>이메일 알림을 활성화하려면 일부 속성을 구성해야 합니다. 전자 메일 템플릿을 사용자 지정하거나 새 언어의 전자 메일 템플릿을 추가할 수도 있습니다. AEM에서 전자 메일 알림을 구성하려면 [전자 메일 알림 구성](/help/sites-administering/notification.md#configuringemailnotification)을 참조하십시오.

### 대화 상자 참가자 단계 {#dialog-participant-step}

**대화 참가자 단계**&#x200B;를 사용하여 작업 항목이 할당된 사용자로부터 정보를 수집합니다. 이 단계는 나중에 워크플로우에서 사용되는 소량의 데이터를 수집하는 데 유용합니다.

단계를 완료하면 **작업 항목 완료** 대화 상자에 대화 상자에서 정의한 필드가 포함됩니다. 필드에 수집된 데이터는 워크플로우 페이로드의 노드에 저장됩니다. 그런 다음 후속 워크플로우 단계에서 저장소에서 값을 읽을 수 있습니다.

단계를 구성하려면 작업 항목을 지정할 그룹이나 사용자를 지정하고 대화 상자에 대한 경로를 지정합니다.

#### 대화 상자 참가자 단계 - 구성 {#dialog-participant-step-configuration}

단계를 구성하려면 다음 탭을 편집하고 사용합니다.

* [일반](#step-properties-common-tab)
* [사용자/그룹](#step-properties-user-group-tab)
* **대화 상자**

   * **대화 상자 경로**: 사용자가 만든 [대화 상자](#dialog-participant-step-creating-a-dialog)의 대화 상자 노드 경로

#### 대화 상자 참가자 단계 - 대화 상자 만들기 {#dialog-participant-step-creating-a-dialog}

대화 상자를 만들려면 대화 상자를 만들어야 합니다.

* 결과 데이터가 [페이로드에 저장되어 있는 위치](#dialog-participant-step-storing-data-in-the-payload)를 결정합니다.
* [대화 상자를 정의합니다. 데이터를 수집하고 저장하는 데 사용되는 필드를 정의하는 것을 포함합니다](#dialog-participant-step-dialog-definition).

#### 대화 상자 참가자 단계 - 페이로드에 데이터 저장 {#dialog-participant-step-storing-data-in-the-payload}

워크플로 페이로드 또는 작업 항목 메타데이터에 위젯 데이터를 저장할 수 있습니다. 위젯 노드의 `name` 속성 형식에 따라 데이터가 저장되는 위치가 결정됩니다.

* **페이로드로 데이터 저장**

   * 위젯 데이터를 워크플로 페이로드의 속성으로 저장하려면 위젯 노드의 이름 속성 값에 다음 형식을 사용합니다.

     `./jcr:content/nodename`

   * 데이터는 페이로드 노드의 `nodename` 속성에 저장됩니다. 노드에 해당 속성이 없으면 속성이 만들어집니다.
   * 페이로드와 함께 저장되는 경우 동일한 페이로드를 사용하는 대화 상자의 후속 사용은 속성 값을 덮어씁니다.

* **작업 항목으로 데이터 저장**

   * 위젯 데이터를 작업 항목 메타데이터의 속성으로 저장하려면 이름 속성 값에 다음 형식을 사용합니다.

     `nodename`

   * 데이터가 작업 항목 `metadata`의 `nodename` 속성에 저장됩니다. 대화 상자가 나중에 동일한 페이로드와 함께 사용되는 경우 데이터가 유지됩니다.

#### 대화 상자 참가자 단계 - 대화 상자 정의 {#dialog-participant-step-dialog-definition}

1. **대화 상자 구조**

   대화 상자 참가자 단계의 대화 상자는 구성 요소 작성을 위해 만든 대화 상자와 유사합니다. 이러한 파일은 다음 위치에 저장됩니다.

   `/apps/myapp/workflow/dialogs`

   터치 사용이 가능한 표준 UI에 대한 대화 상자는 다음과 같은 노드 구조를 갖습니다.

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
   >
   >[대화 상자 만들기 및 구성](/help/sites-developing/developing-components.md#creating-and-configuring-a-dialog)을 참조하세요.

1. **대화 상자 경로 속성**

   **대화 참가자 단계**&#x200B;에 **대화 경로** 속성([참가자 단계](#participant-step) 속성과 함께)이 있습니다. **Dialog Path** 속성의 값은 대화 상자의 `dialog` 노드에 대한 경로입니다.

   예를 들어 대화 상자는 노드에 저장된 `EmailWatch` 구성 요소에 포함되어 있습니다.

   `/apps/myapp/workflows/dialogs`

   터치 사용 UI의 경우 **대화 상자 경로** 속성에 다음 값이 사용됩니다.

   `/apps/myapp/workflow/dialogs/EmailWatch/cq:dialog`

   ![wf-30](assets/wf-30.png)

1. **예제 대화 상자 정의**

   다음 XML 코드 조각은 페이로드 콘텐츠의 `watchEmail` 노드에 `String` 값을 저장하는 대화 상자를 나타냅니다. 제목 노드는 [TextField](https://developer.adobe.com/experience-manager/reference-materials/6-5/granite-ui/api/jcr_root/libs/granite/ui/components/coral/foundation/form/textfield/index.html) 구성 요소를 나타냅니다.

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

   터치 사용 UI에서 이 예제는 다음과 같은 대화 상자를 생성합니다.

   ![chlimage_1-70](assets/chlimage_1-70.png)

### 동적 참가자 단계 {#dynamic-participant-step}

**동적 참가자 단계** 구성 요소는 **[참가자 단계](#participant-step)**&#x200B;와 비슷하지만 런타임에 참가자가 자동으로 선택됩니다.

단계를 구성하려면 대화 상자와 함께 작업 항목을 할당할 참가자를 식별하는 **참가자 선택기**&#x200B;를 선택합니다.

#### 동적 참가자 단계 - 구성 {#dynamic-participant-step-configuration}

단계를 구성하려면 다음 탭을 편집하고 사용합니다.

* [일반](#step-properties-common-tab)
* **참가자 선택기**

   * **참가자 선택기**: 만든 [참가자 선택기의 이름](#developingtheparticipantchooser).
   * **인수**: 필요한 모든 인수.
   * **전자 메일**: 사용자에게 전자 메일 알림을 전송할지 여부입니다.

* **대화 상자**

   * **대화 경로**: **대화 참가자 단계**&#x200B;에서와 같이 사용자가 만드는 [대화 상자의 대화 노드에 대한 경로](#dialog-participant-step-creating-a-dialog).

#### 동적 참가자 단계 - 참가자 선택기 개발 {#dynamic-participant-step-developing-the-participant-chooser}

참가자 선택기를 만듭니다. 따라서 모든 선택 논리나 기준을 사용할 수 있습니다. 예를 들어 참가자 선택기는 작업 항목이 가장 적은 사용자(그룹 내)를 선택할 수 있습니다. 워크플로우 모델에서 **동적 참가자 단계** 구성 요소의 다른 인스턴스에서 사용할 참가자 선택기를 원하는 수만큼 만들 수 있습니다.

작업 항목을 할당할 사용자를 선택하는 OSGi 서비스 또는 ECMAScript를 만듭니다.

* **ECMAscript**

  스크립트에는 사용자 ID를 `String` 값으로 반환하는 getParticipant 함수가 포함되어야 합니다. 사용자 지정 스크립트를 `/apps/myapp/workflow/scripts` 폴더 또는 하위 폴더 등에 저장합니다.

  샘플 스크립트는 표준 AEM 인스턴스에 포함됩니다.

  `/libs/workflow/scripts/initiator-participant-chooser.ecma`

  >[!CAUTION]
  >
  >`/libs` 경로에서 아무 것도 변경하지 마십시오.
  >
  >
  >그 이유는 다음에 인스턴스를 업그레이드할 때 `/libs`의 콘텐츠가 덮어쓰기되며 핫픽스 또는 기능 팩을 적용할 때 덮어쓰기될 수 있기 때문입니다.

  이 스크립트는 워크플로 개시자를 참가자로 선택합니다.

  ```
  function getParticipant() {
      return workItem.getWorkflow().getInitiator();
  }
  ```

  >[!NOTE]
  >
  >**워크플로 개시자 참가자 선택기** 구성 요소는 **동적 참가자 단계**&#x200B;를 확장하고 이 스크립트를 단계 구현으로 사용합니다.

* **OSGi 서비스**

  서비스는 [com.day.cq.workflow.exec.ParticipantStepChooser](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/workflow/exec/ParticipantStepChooser.html) 인터페이스를 구현해야 합니다. 인터페이스는 다음 멤버를 정의합니다.

   * `SERVICE_PROPERTY_LABEL` 필드: 참가자 선택기의 이름을 지정하려면 이 필드를 사용하십시오. **동적 참가자 단계** 속성의 사용 가능한 참가자 선택기 목록에 이름이 나타납니다.

   * `getParticipant` 메서드: 동적으로 확인된 사용자 ID를 `String` 값으로 반환합니다.

  >[!CAUTION]
  >
  >`getParticipant` 메서드가 동적으로 확인된 사용자 ID를 반환합니다. 이 ID는 그룹 ID 또는 사용자 ID일 수 있습니다.
  >
  >
  >하지만 참가자 목록이 반환되면 **참가자 단계**&#x200B;에 대해서만 그룹 ID를 사용할 수 있습니다. **동적 참가자 단계**&#x200B;의 경우 빈 목록이 반환되어 위임에 사용할 수 없습니다.

  **동적 참가자 단계** 구성 요소에서 구현을 사용할 수 있도록 하려면 서비스를 내보내는 OSGi 번들에 Java™ 클래스를 추가하고 AEM 서버에 번들을 배포합니다.

  >[!NOTE]
  >
  >**임의 참가자 선택기**&#x200B;은(는) 임의 사용자(`com.day.cq.workflow.impl.process.RandomParticipantChooser`)를 선택하는 샘플 서비스입니다. **임의 참가자 선택** r 단계 구성 요소 샘플은 **동적 참가자 단계**&#x200B;를 확장하고 이 서비스를 단계 구현으로 사용합니다.

#### 동적 참가자 단계 - 예제 참가자 선택기 서비스 {#dynamic-participant-step-example-participant-chooser-service}

다음 Java™ 클래스는 `ParticipantStepChooser` 인터페이스를 구현합니다. 클래스는 워크플로우를 시작한 참가자의 이름을 반환합니다. 이 코드는 샘플 스크립트(`initiator-participant-chooser.ecma`)가 사용하는 것과 동일한 논리를 사용합니다.

`@Property` 주석은 `SERVICE_PROPERTY_LABEL` 필드의 값을 `Workflow Initiator Participant Chooser`(으)로 설정합니다.

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

**동적 참가자 단계** 속성 대화 상자에서 **참가자 선택기** 목록에 이 서비스를 나타내는 항목 `Workflow Initiator Participant Chooser (script)`이(가) 포함됩니다.

워크플로우 모델이 시작되면 로그에는 워크플로우를 시작한 사용자와 작업 항목을 할당한 사용자의 ID가 표시됩니다. 이 예에서는 `admin` 사용자가 워크플로를 시작했습니다.

`13.09.2015 15:48:53.037 *INFO* [10.176.129.223 [1347565733037] POST /etc/workflow/instances HTTP/1.1] com.adobe.example.InitiatorParticipantChooser Assigning Dynamic Participant Step work item to admin`

### 양식 참가자 단계 {#form-participant-step}

작업 항목을 열 때 **양식 참가자 단계**&#x200B;에서 양식을 표시합니다. 사용자가 양식을 작성하여 제출하면 필드 데이터가 워크플로 페이로드의 노드에 저장됩니다.

단계를 구성하려면 작업 항목을 지정할 그룹이나 사용자를 지정하고 양식에 대한 경로를 지정합니다.

>[!CAUTION]
>
>이 섹션에서는 페이지 작성을 위한 기초 구성 요소 [&#128279;](/help/sites-authoring/default-components-foundation.md#form)의 Forms 섹션에 대해 설명합니다.

#### 양식 참가자 단계 - 구성 {#form-participant-step-configuration}

단계를 구성하려면 다음 탭을 편집하고 사용합니다.

* [일반](#step-properties-common-tab)
* [사용자/그룹](#step-properties-user-group-tab)
* **양식**

   * **양식 경로**: 만든 [양식의 경로](#form-participant-step-creating-the-form).

#### 양식 참가자 단계 - 양식 만들기 {#form-participant-step-creating-the-form}

정상적으로 **양식 참가자 단계**&#x200B;에 사용할 양식을 만드십시오. 단, 양식 참가자 단계의 양식에는 다음 구성이 있어야 합니다.

* **Start of Form** 구성 요소의 **Action Type** 속성이 `Edit Workflow Controlled Resource(s)`(으)로 설정되어 있어야 합니다.
* **Start of Form** 구성 요소에는 `Form Identifier` 속성 값이 있어야 합니다.
* 양식 구성 요소에는 필드 데이터가 저장되는 노드의 경로로 설정된 **요소 이름** 속성이 있어야 합니다. 경로는 워크플로 페이로드 콘텐츠에서 노드를 찾아야 합니다. 이 값은 다음 형식을 사용합니다.

  `./jcr:content/path_to_node`

* 양식에는 **워크플로 제출 단추** 구성 요소가 포함되어야 합니다. 구성 요소의 속성을 구성하지 않습니다.

워크플로우의 요구 사항에 따라 필드 데이터를 저장할 위치가 결정됩니다. 예를 들어 필드 데이터를 사용하여 페이지 콘텐츠의 속성을 구성할 수 있습니다. 다음 **요소 이름** 속성 값은 필드 데이터를 `jcr:content` 노드의 `redirectTarget` 속성 값으로 저장합니다.

`./jcr:content/redirectTarget`

다음 예제에서는 필드 데이터가 페이로드 페이지에서 **Text** 구성 요소의 콘텐츠로 사용됩니다.

`./jcr:content/par/text_3/text`

첫 번째 예제는 `cq:Page` 구성 요소가 렌더링하는 모든 페이지에 사용할 수 있습니다. 두 번째 예제는 페이로드 페이지에 ID가 `text_3`인 **Text** 구성 요소가 포함된 경우에만 사용할 수 있습니다.

양식은 저장소의 어디에나 배치할 수 있지만 워크플로 사용자는 양식을 읽을 수 있는 권한이 있어야 합니다.

### 임의 참가자 선택기 {#random-participant-chooser}

**임의 참가자 선택기** 단계는 목록에서 임의로 선택된 사용자에게 생성된 작업 항목을 할당하는 참가자 선택기입니다.

![wf-31](assets/wf-31.png)

#### 임의 참가자 선택기 - 구성 {#random-participant-chooser-configuration}

단계를 구성하려면 다음 탭을 편집하고 사용합니다.

* [일반](#step-properties-common-tab)
* **인수**

   * **참가자**: 선택할 수 있는 사용자 목록을 지정합니다. 목록에 사용자를 추가하려면 **항목 추가**&#x200B;를 클릭하고 사용자 노드의 홈 경로 또는 사용자 ID를 입력하십시오. 사용자의 순서는 작업 항목이 할당될 가능성에 영향을 주지 않습니다.

### 워크플로우 개시자 참가자 선택기 {#workflow-initiator-participant-chooser}

**워크플로 개시자 참가자 선택기** 단계는 생성된 작업 항목을 워크플로를 시작한 사용자에게 할당하는 참가자 선택기입니다. **Common** 속성 외에 구성할 속성이 없습니다.

#### 워크플로우 개시자 참가자 선택기 - 구성 {#workflow-initiator-participant-chooser-configuration}

단계를 구성하려면 다음 탭을 사용하여 편집합니다.

* [일반](#step-properties-common-tab)

## 프로세스 단계 {#process-step}

**프로세스 단계**&#x200B;에서 ECMAScript를 실행하거나 OSGi 서비스를 호출하여 자동 처리를 수행합니다.

![wf-32](assets/wf-32.png)

### 프로세스 단계 - 구성 {#process-step-configuration}

단계를 구성하려면 다음 탭을 편집하고 사용합니다.

* [일반](#step-properties-common-tab)
* **프로세스**

   * **프로세스**: 실행할 프로세스 구현입니다. 드롭다운 메뉴를 사용하여 ECMAScript 또는 OSGi 서비스를 선택합니다. 다음에 대한 정보:

      * 표준 ECMAScript 및 OSGi 서비스에서는 [프로세스 단계에 내장된 프로세스](/help/sites-developing/workflows-process-ref.md)를 참조하십시오.
      * 프로세스 단계에 대한 ECMAScript를 만들려면 [ECMAScript를 사용하여 프로세스 단계 구현](/help/sites-developing/workflows-customizing-extending.md#using-ecmascript)을 참조하십시오.
      * 프로세스 단계에 대한 OSGi 서비스를 만드는 중입니다. [Java™ 클래스를 사용하여 프로세스 단계 구현](/help/sites-developing/workflows-customizing-extending.md#implementing-a-process-step-with-a-java-class)을 참조하세요.

   * **핸들러 진행**: 실행 후 워크플로우를 자동으로 다음 단계로 진행하려면 이 옵션을 선택하십시오. 선택하지 않은 경우 구현 스크립트는 워크플로우 개선을 처리해야 합니다.
   * **인수**: 프로세스에 전달할 인수.

## 변수 설정 {#set-variable}

변수 설정 단계에서는 변수의 값을 설정하고 값이 설정되는 순서를 정의할 수 있습니다. 변수는 변수 설정 단계에서 변수 매핑이 나열된 순서로 설정됩니다.

![매핑을 추가하여 변수 설정](assets/set_variable_addmappingnew.png)

### 변수 설정 - 구성 {#setvariable}

단계를 구성하려면 다음 탭을 편집하고 사용합니다.

* [일반](/help/sites-developing/workflows-step-ref.md#step-properties-common-tab)
* **매핑**

   * **변수 선택:** 이 옵션을 사용하여 값을 설정할 변수를 선택합니다.
   * **매핑 모드 선택:** 변수에 대한 값을 설정하려면 매핑 모드를 선택하십시오. 변수의 데이터 유형에 따라 다음 옵션을 사용하여 변수의 값을 설정할 수 있습니다.

      * **리터럴:** 지정할 정확한 값을 알고 있는 경우 옵션을 사용하십시오.
      * **식:** 사용할 값이 식을 기반으로 계산되는 경우 옵션을 사용합니다. 표현식은 제공된 표현식 편집기에서 생성됩니다.
      * **JSON 점 표기법:** 옵션을 사용하여 JSON 또는 FDM 형식 변수에서 값을 검색합니다.
      * **XPATH:** 옵션을 사용하여 XML 형식 변수에서 값을 검색합니다.
      * **페이로드 관련 값:** 변수에 저장할 값을 페이로드 관련 경로에서 사용할 수 있는 경우 옵션을 사용합니다.
      * **절대 경로:** 변수에 저장할 값을 절대 경로에서 사용할 수 있는 경우 옵션을 사용합니다.

   * **값 지정:** 변수에 매핑하려면 값을 지정하십시오. 이 필드에서 지정하는 값은 매핑 모드에 따라 다릅니다.
   * **매핑 추가:** 이 옵션을 사용하여 더 많은 매핑을 추가하여 변수의 값을 설정하십시오.
