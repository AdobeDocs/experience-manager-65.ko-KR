---
title: 워크플로 개발 및 확장
description: AEM은 워크플로 모델을 만들고, 워크플로 단계를 개발하며, 워크플로와 프로그래밍 방식으로 상호 작용하기 위한 여러 가지 도구와 리소스를 제공합니다
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
exl-id: 041b1767-8b6c-4887-a70d-abc96a116976
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '1460'
ht-degree: 3%

---


# 워크플로 개발 및 확장{#developing-and-extending-workflows}

AEM은 워크플로 모델을 만들고, 워크플로 단계를 개발하며, 워크플로와 프로그래밍 방식으로 상호 작용하기 위한 여러 가지 도구와 리소스를 제공합니다.

워크플로를 사용하면 AEM 환경에서 리소스를 관리하고 콘텐츠를 게시하는 프로세스를 자동화할 수 있습니다. 워크플로우는 일련의 단계로 구성되며 각 단계는 개별 작업을 수행합니다. 논리 및 런타임 데이터를 사용하여 프로세스를 계속할 수 있는 시기를 결정하고 가능한 여러 단계 중 하나에서 다음 단계를 선택할 수 있습니다.

예를 들어 웹 페이지를 만들고 게시하기 위한 비즈니스 프로세스에는 다양한 참가자의 승인 및 승인 작업이 포함됩니다. 이러한 프로세스는 AEM 워크플로우를 사용하여 모델링하고 특정 콘텐츠에 적용할 수 있습니다.

주요 측면은 아래에 설명되어 있으며, 다음 페이지에서는 자세한 내용을 다룹니다.

* [워크플로 모델 만들기](/help/sites-developing/workflows-models.md)
* [워크플로 기능 확장](/help/sites-developing/workflows-customizing-extending.md)
* [프로그래밍 방식으로 워크플로우와 상호 작용](/help/sites-developing/workflows-program-interaction.md)
* [워크플로 단계 참조](/help/sites-developing/workflows-step-ref.md)
* [워크플로 프로세스 참조](/help/sites-developing/workflows-process-ref.md)
* [워크플로우 모범 사례](/help/sites-developing/workflows-best-practices.md)

>[!NOTE]
>
>다음에 대한 정보:
>
>* 워크플로우에 참여하려면 [워크플로우 사용](/help/sites-authoring/workflows.md)을 참조하세요.
>* 워크플로우 및 워크플로우 인스턴스 관리는 [워크플로우 관리](/help/sites-administering/workflows.md)를 참조하십시오.
>* 전체 커뮤니티 문서에 대한 자세한 내용은 [Adobe Experience Manager 워크플로를 사용하여 디지털 Assets 수정](https://experienceleague.adobe.com/docs/experience-manager-65/assets/using/assets-workflow.html)을 참조하십시오.
>* [워크플로에 대한 AEM 전문가에게 묻기](https://communities.adobeconnect.com/p5s33iburd54/)를 참조하십시오.
>* 정보 위치를 변경하면 [AEM 6.5의 저장소 재구성](/help/sites-deploying/repository-restructuring.md) 및 [워크플로 모범 사례 - 위치](/help/sites-developing/workflows-best-practices.md#locations)를 참조하십시오.
>

## 모델 {#model}

`WorkflowModel`은(는) 워크플로의 정의(모델)를 나타냅니다. `WorkflowNodes`과(와) `WorkflowTransitions`(으)로 구성됩니다. 전환은 노드를 연결하고 *흐름*&#x200B;을(를) 정의합니다. 모델에는 항상 시작 노드와 끝 노드가 있습니다.

### 런타임 모델 {#runtime-model}

워크플로우 모델의 버전이 관리됩니다. 워크플로 인스턴스를 실행할 때는 워크플로가 시작될 때 사용할 수 있는 대로 워크플로의 런타임 모델을 사용하고 유지합니다.

**동기화**&#x200B;가 워크플로 모델 편집기[&#128279;](/help/sites-developing/workflows-models.md#sync-your-workflow-generate-a-runtime-model)에서 트리거될 때 런타임 모델이 생성됩니다.

특정 인스턴스가 시작된 후 *후*&#x200B;에 발생하는 워크플로 모델 또는 생성된 런타임 모델에 대한 편집 내용이 해당 인스턴스에 적용되지 않습니다.

>[!CAUTION]
>
>수행되는 단계는 **동기화** 작업이 워크플로우 모델 편집기에서 트리거될 때 생성된 [런타임 모델](/help/sites-developing/workflows-models.md#sync-your-workflow-generate-a-runtime-model)에 의해 정의됩니다.
>
>이 시점 이후에 워크플로 모델이 변경되는 경우(**동기화**&#x200B;가 트리거되지 않음) 런타임 인스턴스에 이러한 변경 사항이 반영되지 않습니다. 업데이트 후 생성된 런타임 모델만 변경 사항을 반영합니다. 예외는 기본 ECMA 스크립트이며 이러한 변경 사항이 적용되도록 한 번만 유지됩니다.

### 단계 {#step}

각 단계는 개별 작업을 수행합니다. 워크플로 단계에는 여러 유형이 있습니다.

* 참가자(사용자/그룹): 이 단계에서는 작업 항목을 생성하여 사용자 또는 그룹에 할당합니다. 사용자는 워크플로를 진행하려면 작업 항목을 완료해야 합니다.
* 프로세스(스크립트, Java™ 메서드 호출): 이러한 단계는 시스템에 의해 자동으로 실행됩니다. ECMA 스크립트 또는 Java™ 클래스는 단계를 구현합니다. 비즈니스 논리에 따라 특수 워크플로우 이벤트를 듣고 작업을 수행하도록 서비스를 개발할 수 있습니다.
* 컨테이너(하위 워크플로우): 이 유형의 단계는 다른 워크플로우 모델을 시작합니다.
* OR 분할/조인: 워크플로우에서 다음에 실행할 단계를 결정하는 논리를 사용합니다.
* AND 분할/결합: 여러 단계를 동시에 실행할 수 있습니다.

모든 단계는 다음 공통 속성을 공유합니다. `Autoadvance` 및 `Timeout` 경고(스크립팅 가능).

### 전환 {#transition}

`WorkflowTransition`은(는) `WorkflowModel`의 두 `WorkflowNodes` 간의 전환을 나타냅니다.

* 두 개의 연속 단계 간의 링크를 정의합니다.
* 규칙을 적용할 수 있습니다.

### 작업 항목 {#workitem}

`WorkItem`은(는) `WorkflowModel`의 `Workflow` 인스턴스를 통해 전달되는 단위입니다. 여기에는 인스턴스가 작동하는 `WorkflowData`과(와) 기본 워크플로 단계를 설명하는 `WorkflowNode`에 대한 참조가 포함됩니다.

* 작업을 식별하는 데 사용되며 각 받은 편지함에 입력됩니다.
* 워크플로 인스턴스에는 워크플로 모델에 따라 한 개 이상의 `WorkItems`이 동시에 있을 수 있습니다.
* `WorkItem`이(가) 워크플로 인스턴스를 참조합니다.
* 저장소에서 `WorkItem`은(는) 워크플로 인스턴스 아래에 저장됩니다.

### 페이로드 {#payload}

워크플로우를 통해 고급화해야 하는 리소스를 참조합니다.

페이로드 구현은 경로, UUID 또는 URL별로 저장소의 리소스를 참조하거나 직렬화된 Java™ 개체를 참조합니다. 저장소 리소스를 유연하게 참조하고 생산성이 향상됩니다. 예를 들어 참조된 노드를 양식으로 렌더링할 수 있습니다.

### 라이프사이클 {#lifecycle}

새 워크플로우를 시작할 때(각 워크플로우 모델을 선택하고 페이로드를 정의하여) 만들어지고 끝 노드가 처리되면 종료됩니다.

워크플로 인스턴스에서는 다음 작업을 수행할 수 있습니다.

* 종료
* 일시 중단
* 다시 시작
* 다시 시작

완료 및 종료된 인스턴스가 보관됩니다.

### 받은 편지함 {#inbox}

각 사용자 계정에는 할당된 `WorkItems`에 액세스할 수 있는 고유한 워크플로 받은 편지함이 있습니다.

`WorkItems`은(는) 사용자 계정 또는 사용자 계정이 속한 그룹에 직접 할당됩니다.

### 워크플로 유형 {#workflow-types}

워크플로 모델 콘솔에는 다양한 유형의 워크플로가 있습니다.

![wf-upgraded-03](assets/wf-upgraded-03.png)

* **기본값**

  이러한 유형은 표준 AEM 인스턴스에 포함된 즉시 사용 가능한 워크플로우입니다.

* 사용자 지정 워크플로우(콘솔에 표시기 없음)

  이러한 워크플로우는 새로운 워크플로로 생성되었거나 맞춤화로 오버레이된 기본 제공 워크플로에서 만들어졌습니다.

* **레거시**

  이전 버전의 AEM에서 만든 워크플로우입니다. 이러한 워크플로우는 업그레이드 중에 유지하거나 이전 버전에서 워크플로 패키지로 내보낸 다음 새 버전으로 가져올 수 있습니다.

### 임시 워크플로 {#transient-workflows}

표준 워크플로우는 실행 중에 런타임(내역) 정보를 저장합니다. 워크플로 모델을 **임시**(으)로 정의하여 이러한 기록이 지속되지 않도록 할 수도 있습니다. 이 워크플로우는 정보를 유지하는 데 사용되는 시간과 리소스를 절약하므로 성능 조정에 사용됩니다.

임시 워크플로우는 다음과 같은 모든 워크플로에 사용할 수 있습니다.

* 를 자주 실행합니다.
* 워크플로우 내역은 필요하지 않습니다.

임시 워크플로우는 자산 정보가 중요하지만 워크플로 런타임 내역은 중요하지 않은 많은 자산을 로드하기 위해 도입되었습니다.

>[!NOTE]
>
>자세한 내용은 [임시 워크플로 만들기](/help/sites-developing/workflows-models.md#creating-a-transient-workflow)를 참조하십시오.

>[!CAUTION]
>
>워크플로 모델에 임시 플래그가 지정되면 런타임 정보가 계속 유지되어야 하는 몇 가지 시나리오가 있습니다.
>
>* 페이로드 유형(예: 비디오)은 처리를 위해 외부 단계가 필요합니다. 이 경우 상태 확인을 위해 런타임 기록이 필요합니다.
>* 워크플로우가 **AND 분할**&#x200B;을(를) 입력합니다. 이러한 경우 상태 확인을 위해 런타임 기록이 필요합니다.
>* 임시 워크플로우가 참가자 단계에 진입하면 런타임 시 모드가 임시 모드로 변경됩니다. 작업이 사용자에게 전달되므로 기록이 지속되어야 합니다.
>

>[!CAUTION]
>
>임시 워크플로우 내에서는 **이동 단계**&#x200B;를 사용하면 안 됩니다.
>
>이유는 **이동 단계**&#x200B;에서 `goto` 지점에서 워크플로를 계속하기 위한 슬링 작업을 만들기 때문입니다. 이 메서드는 워크플로우를 일시적으로 만드는 목적을 실패하고 로그 파일에 오류를 생성합니다.
>
>임시 워크플로우에서 선택하려면 **OR 분할**&#x200B;을 사용하십시오.

>[!NOTE]
>
>임시 워크플로우가 에셋 성능에 미치는 영향에 대한 자세한 내용은 [Assets에 대한 우수 사례](/help/assets/performance-tuning-guidelines.md#transient-workflows)를 참조하십시오.

### 여러 리소스 지원 {#multi-resource-support}

워크플로우 모델에 대해 **다중 리소스 지원**&#x200B;을 활성화하면 여러 리소스를 선택하더라도 단일 워크플로우 인스턴스가 시작됩니다. 각각은 패키지로 첨부됩니다.

워크플로 모델에 대해 **다중 리소스 지원**&#x200B;이 활성화되지 않고 여러 리소스를 선택한 경우 각 리소스에 대해 개별 워크플로 인스턴스가 시작됩니다.

>[!NOTE]
>
>자세한 내용은 [다중 리소스 지원을 위한 워크플로우 구성](/help/sites-developing/workflows-models.md#configuring-a-workflow-for-multi-resource-support)을 참조하십시오.

### 워크플로 단계 {#workflow-stages}

워크플로 단계 는 작업을 처리할 때 워크플로의 진행 상황을 시각화하는 데 도움이 됩니다. 워크플로우가 처리를 통해 어디까지 진행되었는지 개요를 제공하는 데 사용할 수 있습니다. 워크플로우가 실행되면 사용자는 **단계**&#x200B;에서 설명한 진행률을 볼 수 있습니다(개별 단계와 반대).

개별 단계 이름이 구체적이고 기술적일 수 있으므로 단계 이름을 정의하여 워크플로우 진행에 대한 개념적 보기를 제공할 수 있습니다.

예를 들어 6단계 4단계로 구성된 워크플로의 경우:

1. [워크플로 진행 상황을 표시하는 워크플로 단계를 구성한 다음 워크플로의 각 단계에 적절한 단계를 할당할 수 있습니다](/help/sites-developing/workflows-models.md#configuring-workflow-stages-that-show-workflow-progress):

   * 여러 단계 이름을 만들 수 있습니다.
   * 그런 다음 각 단계에 개별 단계 이름이 할당됩니다(하나 이상의 단계에 단계 이름을 할당할 수 있음).

   | **단계 이름** | **단계(단계에 할당됨)** |
   |---|---|
   | 1단계 | 만들기 |
   | 2단계 | 만들기 |
   | 3단계 | 검토 |
   | 4단계 | 승인 |
   | 5단계 | 완료 |
   | 6단계 | 완료 |

1. 워크플로우를 실행하면 단계 이름 대신 단계 이름에 따라 진행 상황을 볼 수 있습니다. [받은 편지함](/help/sites-authoring/inbox.md)에 나열된 워크플로 항목[&#128279;](/help/sites-authoring/workflows-participating.md#opening-a-workflow-item-to-view-details-and-take-actions)의 작업 세부 정보 창에 있는 워크플로 정보 탭에 워크플로 진행률이 표시됩니다.

### 워크플로우 및 Forms {#workflows-and-forms}

일반적으로 워크플로는 AEM에서 양식 제출을 처리하는 데 사용됩니다. 표준 AEM 인스턴스에서 사용할 수 있는 [핵심 구성 요소 양식 구성 요소](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/wcm-components/forms/form-container.html) 또는 [AEM Forms 솔루션](/help/forms/using/aem-forms-workflow.md)을 사용할 수 있습니다.

양식을 작성할 때 양식 제출을 워크플로우 모델과 쉽게 연결할 수 있습니다. 예를 들어 저장소의 특정 위치에 콘텐츠를 저장하거나 사용자에게 양식 제출 및 해당 콘텐츠에 대해 알릴 수 있습니다.

### 워크플로우 및 번역 {#workflows-and-translation}

또한 워크플로는 [번역](/help/sites-administering/translation.md) 프로세스의 일부입니다.
