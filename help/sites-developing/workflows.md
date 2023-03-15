---
title: 워크플로 개발 및 확장
seo-title: Developing and Extending Workflows
description: AEM은 워크플로 모델을 만들고, 워크플로 단계를 개발하며, 워크플로와 프로그래밍 방식으로 상호 작용하기 위한 여러 가지 도구와 리소스를 제공합니다
seo-description: AEM provides several tools and resources for creating workflow models, developing workflow steps, and for programmatically interacting with workflows
uuid: 5a857589-3b13-4519-bda2-b1dab6005550
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: 8954e3df-3afa-4d53-a7e1-255f3b8f499f
exl-id: 041b1767-8b6c-4887-a70d-abc96a116976
source-git-commit: 82b9b852fa3134f140f8de0bad229282979c8a30
workflow-type: tm+mt
source-wordcount: '1512'
ht-degree: 4%

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
* [워크플로우 우수 사례](/help/sites-developing/workflows-best-practices.md)

>[!NOTE]
>
>다음에 대한:
>
>* 워크플로우에 참여하려면 다음을 참조하십시오. [워크플로우 사용](/help/sites-authoring/workflows.md).
>* 워크플로우 및 워크플로우 인스턴스 관리 참조: [워크플로우 관리](/help/sites-administering/workflows.md).
>* 전체 커뮤니티 문서에 대한 자세한 내용은 [Adobe Experience Manager 워크플로우를 사용하여 디지털 에셋 수정.](https://helpx.adobe.com/experience-manager/using/modify_asset_workflow.html)
>* 다음을 참조하십시오. [워크플로우에 대해 AEM 전문가 웨비나에 문의하십시오.](https://bit.ly/ATACE218).
>* 전체 커뮤니티 문서에 대한 자세한 내용은 [사용자 지정 Adobe Experience Manager 6.3 동적 참가자 단계 만들기](https://helpx.adobe.com/experience-manager/using/dynamic-steps-aem63.html).
>* 정보 위치에 대한 변경 내용은 [AEM 6.5의 저장소 재구성](/help/sites-deploying/repository-restructuring.md) 및 [워크플로우 모범 사례 - 위치](/help/sites-developing/workflows-best-practices.md#locations).
>


## 모델 {#model}

A `WorkflowModel` 워크플로의 정의(모델)를 나타냅니다. 다음으로 구성됩니다. `WorkflowNodes` 및 `WorkflowTransitions`. 변환은 노드를 연결하고 다음을 정의합니다. *흐름*. 모델에는 항상 시작 노드와 끝 노드가 있습니다.

### 런타임 모델 {#runtime-model}

워크플로우 모델의 버전이 관리됩니다. 워크플로 인스턴스를 실행할 때 워크플로의 런타임 모델을 사용(및 유지)합니다(워크플로가 시작될 때 사용 가능).

런타임 모델은 [다음과 같은 경우에 생성됨 **동기화** 은 워크플로 모델 편집기에서 트리거됩니다](/help/sites-developing/workflows-models.md#sync-your-workflow-generate-a-runtime-model).

발생하는 워크플로 모델 및/또는 생성되는 런타임 모델에 대한 편집 *이후* 시작된 특정 인스턴스는 해당 인스턴스에 적용되지 않습니다.

>[!CAUTION]
>
>수행되는 단계는 [런타임 모델](/help/sites-developing/workflows-models.md#sync-your-workflow-generate-a-runtime-model); 이 값은 다음 시간에 생성됩니다. **동기화** 작업이 워크플로우 모델 편집기에서 트리거됩니다.
>
>이 시점 이후에 워크플로 모델이 변경되는 경우(없이) **동기화** 트리거됨)을 지정하면 런타임 인스턴스가 이러한 변경 사항을 반영하지 않습니다. 업데이트 후 생성된 런타임 모델만 변경 사항을 반영합니다. 예외는 기본 ECMA 스크립트이며, 이 스크립트는 한 번만 유지되므로 변경 사항이 적용됩니다.

### 단계 {#step}

각 단계는 개별 작업을 수행합니다. 워크플로 단계에는 여러 유형이 있습니다.

* 참가자(사용자/그룹): 이 단계에서는 작업 항목을 생성하여 사용자 또는 그룹에 할당합니다. 사용자는 워크플로를 진행하려면 작업 항목을 완료해야 합니다.
* 프로세스(스크립트, Java 메서드 호출): 이러한 단계는 시스템에 의해 자동으로 실행됩니다. ECMA 스크립트 또는 Java 클래스는 단계를 구현합니다. 비즈니스 논리에 따라 특수 워크플로우 이벤트를 듣고 작업을 수행하도록 서비스를 개발할 수 있습니다.
* 컨테이너(하위 워크플로우): 이 유형의 단계는 다른 워크플로우 모델을 시작합니다.
* OR 분할/조인: 워크플로우에서 다음에 실행할 단계를 결정하는 논리를 사용합니다.
* AND 분할/결합: 여러 단계를 동시에 실행할 수 있습니다.

모든 단계는 다음과 같은 공통 속성을 공유합니다. `Autoadvance` 및 `Timeout` 경고(스크립트 가능).

### 전환 {#transition}

A `WorkflowTransition` 둘 사이의 전환을 나타냅니다. `WorkflowNodes` / `WorkflowModel`.

* 두 개의 연속 단계 간의 링크를 정의합니다.
* 규칙을 적용할 수 있습니다.

### 작업 항목 {#workitem}

A `WorkItem` 는 을 통해 전달되는 단위입니다. `Workflow` 의 인스턴스 `WorkflowModel`. 여기에는 `WorkflowData` 인스턴스가 작동하는에 대한 및 참조 `WorkflowNode` 기본 워크플로우 단계를 설명합니다.

* 작업을 식별하는 데 사용되며 각 받은 편지함에 입력됩니다.
* 워크플로 인스턴스에는 하나 이상의 인스턴스가 있을 수 있습니다. `WorkItems` 동시에 (워크플로우 모델에 따라).
* 다음 `WorkItem` 은 워크플로 인스턴스를 참조합니다.
* 저장소에서 `WorkItem` 은 워크플로 인스턴스 아래에 저장됩니다.

### 페이로드 {#payload}

워크플로우를 통해 고급화해야 하는 리소스를 참조합니다.

페이로드 구현은 경로, UUID 또는 URL별로 저장소의 리소스를 참조하거나 직렬화된 Java 개체를 참조합니다. 저장소에서 리소스를 참조하는 것은 매우 유연하며 슬링과 함께 매우 생산적입니다. 예를 들어 참조된 노드를 양식으로 렌더링할 수 있습니다.

### 라이프사이클 {#lifecycle}

새 워크플로우를 시작할 때(각 워크플로우 모델을 선택하고 페이로드를 정의하여) 만들어지고 끝 노드가 처리되면 종료됩니다.

워크플로 인스턴스에서는 다음 작업을 수행할 수 있습니다.

* 종료
* 일시 중단
* 다시 시작
* 다시 시작

완료 및 종료된 인스턴스가 보관됩니다.

### 받은 편지함 {#inbox}

각 사용자 계정에는 할당된 워크플로 받은 편지함이 있습니다. `WorkItems` 에 액세스할 수 있습니다.

다음 `WorkItems` 는 사용자 계정 또는 자신이 속한 그룹에 직접 할당됩니다.

### 워크플로 유형 {#workflow-types}

워크플로 모델 콘솔에는 다양한 유형의 워크플로가 있습니다.

![wf-upgraded-03](assets/wf-upgraded-03.png)

* **기본값**

   표준 AEM 인스턴스에 포함된 기본 워크플로입니다.

* 사용자 지정 워크플로우(콘솔에 표시기 없음)

   이는 새 워크플로로 만들어진 워크플로이거나 맞춤화로 오버레이된 기본 제공 워크플로입니다.

* **기존**

   이전 버전의 AEM에서 만든 워크플로우입니다. 업그레이드 중에 유지하거나 이전 버전에서 워크플로우 패키지로 내보낸 다음 새 버전으로 가져올 수 있습니다.

### 임시 워크플로 {#transient-workflows}

표준 워크플로우는 실행 중에 런타임(내역) 정보를 저장합니다. 워크플로우 모델을 다음과 같이 정의할 수도 있습니다. **임시** 그러한 기록이 지속되는 것을 피하기 위해. 정보를 유지하는 데 사용되는 시간/리소스를 절약/피하기 때문에 성능 조정에 사용됩니다.

임시 워크플로우는 다음과 같은 모든 워크플로에 사용할 수 있습니다.

* 를 자주 실행합니다.
* 워크플로우 내역은 필요하지 않습니다.

임시 워크플로우는 자산 정보가 중요하지만 워크플로 런타임 내역은 중요하지 않은 많은 자산을 로드하기 위해 도입되었습니다.

>[!NOTE]
>
>다음을 참조하십시오 [임시 워크플로우 만들기](/help/sites-developing/workflows-models.md#creating-a-transient-workflow) 을 참조하십시오.

>[!CAUTION]
>
>워크플로우 모델에 일시적인 것으로 플래그가 지정된 경우 런타임 정보가 계속 유지되는 몇 가지 시나리오가 있습니다.
>
>* 페이로드 유형(예: 비디오)은 처리를 위해 외부 단계가 필요합니다. 이 경우 상태 확인을 위해 런타임 기록이 필요합니다.
>* 워크플로우가 **AND 분할**; 이 경우 상태 확인을 위해 런타임 내역이 필요합니다.
>* 임시 워크플로우가 참가자 단계에 들어가면 모드(런타임 시)가 임시 모드로 변경됩니다. (작업이 개인에게 전달되므로 내역을 지속해야 합니다.)
>


>[!CAUTION]
>
>임시 워크플로우 내에서는 **이동 단계**.
>
>다음과 같습니다. **이동 단계** 에서 워크플로우를 계속하기 위한 sling 작업을 만듭니다. `goto` 가리켜. 이 작업은 워크플로우를 일시적으로 만들기 위한 목적을 무시하고 로그 파일에 오류를 생성합니다.
>
>임시 워크플로우에서 의사 결정을 내리려면 **OR 분할**.

>[!NOTE]
>
>다음을 참조하십시오 [자산에 대한 우수 사례](/help/assets/performance-tuning-guidelines.md#transient-workflows) 임시 워크플로우가 자산 성능에 미치는 영향에 대한 자세한 정보입니다.

### 여러 리소스 지원 {#multi-resource-support}

활성화 중 **다중 리소스 지원** 워크플로 모델의 경우 여러 리소스를 선택하더라도 단일 워크플로 인스턴스가 시작됨을 의미합니다. 이러한 리소스는 패키지로 첨부됩니다.

If **다중 리소스 지원** 가 워크플로우 모델에 대해 활성화되지 않고 여러 리소스를 선택한 다음 각 리소스에 대해 개별 워크플로우 인스턴스가 시작됩니다.

>[!NOTE]
>
>다음을 참조하십시오 [다중 리소스 지원을 위한 워크플로우 구성](/help/sites-developing/workflows-models.md#configuring-a-workflow-for-multi-resource-support) 을 참조하십시오.

### 워크플로 단계 {#workflow-stages}

워크플로 단계 는 작업을 처리할 때 워크플로의 진행 상황을 시각화하는 데 도움이 됩니다. 워크플로우를 실행할 때 사용자가 다음에 설명된 진행률을 볼 수 있으므로 워크플로우가 처리를 통해 도달하는 기간의 개요를 제공하는 데 사용할 수 있습니다. **단계** (개별 단계와 반대).

개별 단계 이름이 구체적이고 기술적일 수 있으므로 단계 이름을 정의하여 워크플로우 진행에 대한 개념적 보기를 제공할 수 있습니다.

예를 들어 6단계 4단계로 구성된 워크플로의 경우:

1. 다음을 수행할 수 있습니다. [워크플로 진행 상황을 표시하는 워크플로 단계 를 구성한 다음 워크플로의 각 단계에 적절한 단계를 할당합니다](/help/sites-developing/workflows-models.md#configuring-workflow-stages-that-show-workflow-progress):

   * 여러 단계 이름을 만들 수 있습니다.
   * 그런 다음 각 단계에 개별 단계 이름이 할당됩니다(하나 이상의 단계에 단계 이름을 할당할 수 있음).

   | **단계 이름** | **단계(단계에 할당됨)** |
   |---|---|
   | 1단계 | 만들기 |
   | 2단계 | 만들기 |
   | 3단계 | 리뷰 |
   | 4단계 | 승인 |
   | 5단계 | 완료 |
   | 6단계 | 완료 |

1. 워크플로우를 실행하면 단계 이름 대신 단계 이름에 따라 진행 상황을 볼 수 있습니다. 워크플로 진행률이 [작업 항목의 작업 세부 정보 창에 있는 워크플로 정보 탭](/help/sites-authoring/workflows-participating.md#opening-a-workflow-item-to-view-details-and-take-actions) 다음에 나열됨: [받은 편지함](/help/sites-authoring/inbox.md).

### 워크플로우 및 Forms {#workflows-and-forms}

일반적으로 워크플로는 AEM에서 양식 제출을 처리하는 데 사용됩니다. 다음과 같을 수 있습니다. [핵심 구성 요소의 양식 구성 요소](https://helpx.adobe.com/experience-manager/core-components/using/form-container.html) 표준 AEM 인스턴스에서 사용하거나 [AEM Forms 솔루션](/help/forms/using/aem-forms-workflow.md).

새 양식을 작성할 때, 저장소의 특정 위치에 콘텐츠를 저장하거나 사용자에게 양식 제출 및 해당 콘텐츠에 대해 알리는 등의 작업을 위해 양식 제출을 워크플로우 모델과 쉽게 연결할 수 있습니다.

### 워크플로우 및 번역 {#workflows-and-translation}

또한 워크플로우는 의 필수적인 부분입니다. [번역](/help/sites-administering/translation.md) 프로세스.
