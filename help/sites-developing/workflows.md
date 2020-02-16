---
title: 워크플로우 개발 및 확장
seo-title: 워크플로우 개발 및 확장
description: AEM 파섹
seo-description: AEM 파섹
uuid: 5a857589-3b13-4519-bda2-b1dab6005550
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: 8954e3df-3afa-4d53-a7e1-255f3b8f499f
translation-type: tm+mt
source-git-commit: 2fc35bfd93585a586cb1d4e3299261611db49ba6

---


# 워크플로우 개발 및 확장{#developing-and-extending-workflows}

AEM 파섹

워크플로우를 통해 AEM 환경에서 리소스 관리 및 컨텐츠 게시 프로세스를 자동화할 수 있습니다. 워크플로우는 개별 작업을 수행하는 각 단계와 함께 일련의 단계로 구성됩니다. 논리 및 런타임 데이터를 사용하여 프로세스를 계속할 수 있는 시기에 대한 결정을 내리고 가능한 여러 단계 중 하나에서 다음 단계를 선택할 수 있습니다.

예를 들어 웹 페이지를 만들고 게시하기 위한 비즈니스 프로세스에는 다양한 참가자의 승인 및 승인 작업이 포함됩니다. 이러한 프로세스는 AEM 워크플로우를 사용하여 모델링하고 특정 컨텐츠에 적용할 수 있습니다.

주요 내용은 아래에 설명되어 있고 다음 페이지에서는 자세한 내용을 다룹니다.

* [워크플로우 모델 만들기](/help/sites-developing/workflows-models.md)
* [워크플로우 기능 확장](/help/sites-developing/workflows-customizing-extending.md)
* [프로그래밍 방식으로 워크플로우와 인터랙션](/help/sites-developing/workflows-program-interaction.md)
* [워크플로우 단계 참조](/help/sites-developing/workflows-step-ref.md)
* [워크플로우 프로세스 참조](/help/sites-developing/workflows-process-ref.md)
* [워크플로우 우수 사례](/help/sites-developing/workflows-best-practices.md)

>[!NOTE]
>
>자세한 내용:
>
>* 워크플로우에 참여하려면 워크플로우 [사용을 참조하십시오](/help/sites-authoring/workflows.md).
>* 워크플로우 및 워크플로우 인스턴스 관리를 참조하십시오 [](/help/sites-administering/workflows.md).
>* 엔드 투 엔드 커뮤니티 아티클의 경우 Adobe [Experience Manager 워크플로우를 사용하여 디지털 자산 수정을 참조하십시오.](https://helpx.adobe.com/experience-manager/using/modify_asset_workflow.html)
>* 워크플로우에 [대한 AEM 전문가에게 묻기 웨비나를 참조하십시오](https://bit.ly/ATACE218).
>* 엔드 투 엔드 커뮤니티 아티클의 경우 사용자 [지정 Adobe Experience Manager 6.3 동적 참가자 단계](https://helpx.adobe.com/experience-manager/using/dynamic-steps-aem63.html)만들기를 참조하십시오.
>* 정보 위치를 변경하면 AEM 6.5 [의 리포지토리 재조정](/help/sites-deploying/repository-restructuring.md) 및 [워크플로우 우수 사례 - 위치를 참조하십시오](/help/sites-developing/workflows-best-practices.md#locations).
>



## 모델 {#model}

A `WorkflowModel` 는 워크플로우의 정의(모델)를 나타냅니다. 그리고 `WorkflowNodes` 로 `WorkflowTransitions`만들어졌어요 전환은 노드를 연결하고 *흐름을*&#x200B;정의합니다. 모델에는 항상 시작 노드와 끝 노드가 있습니다.

### 런타임 모델 {#runtime-model}

워크플로우 모델에는 버전이 지정됩니다. 워크플로우 인스턴스를 실행하면 워크플로우가 시작될 때 사용 가능한 대로 워크플로우의 런타임 모델을 사용(및 유지)합니다.

런타임 모델은 워크플로우 모델 편집기에서 [Sync **를** 트리거하면](/help/sites-developing/workflows-models.md#sync-your-workflow-generate-a-runtime-model)생성됩니다.

특정 인스턴스가 시작된 *후* 생성된 워크플로우 모델 및/또는 런타임 모델에 대한 편집 내용은 해당 인스턴스에 적용되지 않습니다.

>[!CAUTION]
>
>수행되는 단계는 [런타임 모델에](/help/sites-developing/workflows-models.md#sync-your-workflow-generate-a-runtime-model)의해 정의된 단계입니다.이는 워크플로우 모델 편집기에서 **동기화** 작업이 트리거될 때 생성됩니다.
>
>이 시점 이후(Sync가 트리거되지 않음) **에** 워크플로우 모델이 변경되면 런타임 인스턴스에는 해당 변경 내용이 반영되지 않습니다. 업데이트 후에 생성된 런타임 모델만 변경 사항을 반영합니다. 예외적인 것은 기본 ECMA 스크립트로, 한 번만 유지되므로 변경 사항이 적용됩니다.

### 단계{#step}

각 단계는 개별 작업을 수행합니다. 다음과 같은 다양한 유형의 워크플로우 단계가 있습니다.

* 참가자(사용자/그룹):이러한 단계에서는 작업 항목을 생성하여 사용자나 그룹에 할당합니다. 사용자는 작업 항목을 완료하여 워크플로우를 진행해야 합니다.
* 프로세스(스크립트, Java 메서드 호출):이러한 단계는 시스템에 의해 자동으로 실행됩니다. ECMA 스크립트 또는 Java 클래스는 단계를 구현합니다. 특별한 워크플로우 이벤트를 수신하고 비즈니스 로직에 따라 작업을 수행하도록 서비스를 개발할 수 있습니다.
* 컨테이너(하위 워크플로우):이 유형의 단계는 다른 워크플로우 모델을 시작합니다.
* OR 분할/참여:로직을 사용하여 워크플로우에서 다음 단계로 실행할 단계를 결정합니다.
* AND 분할/참여:여러 단계를 동시에 실행할 수 있습니다.

모든 단계는 다음과 같은 일반적인 속성을 공유합니다.및 `Autoadvance` 경고(스크립팅 가능)를 `Timeout` 표시합니다.

### 전환 {#transition}

A `WorkflowTransition` 는 두 개의 `WorkflowNodes` a의 전환을 `WorkflowModel`나타냅니다.

* 두 연속 단계 사이의 링크를 정의합니다.
* 규칙을 적용할 수 있습니다.

### 작업 항목 {#workitem}

A `WorkItem` 는 A의 `Workflow` 인스턴스를 통과하는 `WorkflowModel`단위입니다. 여기에는 인스턴스가 `WorkflowData` 작동하는 것과 기본 워크플로우 단계를 설명하는 `WorkflowNode` 에 대한 참조가 포함되어 있습니다.

* 작업을 식별하는 데 사용되며 각 받은 편지함에 들어갑니다.
* 워크플로우 인스턴스에는 워크플로우 모델에 따라 `WorkItems` 동시에 하나 이상의 항목이 포함될 수 있습니다.
* 워크플로우 인스턴스를 `WorkItem` 참조합니다.
* 보관소에서는 워크플로우 인스턴스 아래에 `WorkItem` 저장됩니다.

### 페이로드 {#payload}

워크플로우를 통해 고급화해야 하는 리소스를 참조합니다.

페이로드 구현은 저장소의 리소스(경로, UUID 또는 URL별) 또는 직렬화된 Java 객체를 참조합니다. 저장소의 리소스 참조는 매우 유연하고 매우 생산성이 뛰어난 기능과 함께 사용할 수 있습니다.예를 들어 참조된 노드를 양식으로 렌더링할 수 있습니다.

### 라이프사이클 {#lifecycle}

새 워크플로우를 시작할 때(해당 워크플로우 모델을 선택하고 페이로드를 정의하여) 생성되며, 끝 노드가 처리되면 종료됩니다.

워크플로우 인스턴스에서 다음 작업을 수행할 수 있습니다.

* 종료
* 일시 중단
* 다시 시작
* 다시 시작

완료되고 종료된 인스턴스는 보관됩니다.

### 받은 편지함 {#inbox}

각 사용자 계정에는 지정된 계정에 액세스할 수 있는 고유한 워크플로우 받은 편지함이 `WorkItems` 있습니다.

이 `WorkItems` 필드는 사용자 계정 직접 또는 사용자가 속한 그룹에 할당됩니다.

### 워크플로우 유형 {#workflow-types}

워크플로우 모델 콘솔에는 다음과 같은 다양한 유형의 워크플로우가 있습니다.

![wf-upgraded-03](assets/wf-upgraded-03.png)

* **기본값**

   표준 AEM 인스턴스에 포함된 특별 워크플로우입니다.

* 사용자 정의 워크플로우(콘솔에 표시기 없음)

   이러한 워크플로우는 새로운 워크플로우로 또는 사용자 정의 내용으로 오버레이된 기본 워크플로우에서 만든 워크플로우입니다.

* **기존**

   이전 버전의 AEM에서 만든 워크플로우 이러한 항목은 업그레이드 중에 유지되거나 이전 버전에서 워크플로우 패키지로 내보낸 다음 새 버전으로 가져올 수 있습니다.

### 일시적인 워크플로우 {#transient-workflows}

표준 워크플로우는 실행 중에 런타임(내역) 정보를 저장합니다. 워크플로우 모델을 일시적(Temporary) **으로** 정의하여 이러한 내역이 지속되지 않도록 할 수도 있습니다. 이 기능은 정보를 지속하는 데 사용되는 시간/리소스를 절약하거나 사용하지 않으므로 성능 조정에 사용됩니다.

다음과 같은 모든 워크플로우에 임시 워크플로우를 사용할 수 있습니다.

* 를 자주 실행합니다.
* 워크플로우 내역이 필요하지 않습니다.

워크플로우 런타임 내역은 중요하지만 자산 정보가 중요한 많은 자산을 로드하기 위해 일시적인 워크플로우가 도입되었습니다.

>[!NOTE]
>
>자세한 [내용은 임시](/help/sites-developing/workflows-models.md#creating-a-transient-workflow) 워크플로우 만들기를 참조하십시오.

>[!CAUTION]
>
>워크플로우 모델이 일시적 으로 플래그로 지정되면 런타임 정보가 계속 유지될 경우 몇 가지 시나리오가 있습니다.
>
>* 페이로드 유형(예: 비디오)에는 처리를 위한 외부 단계가 필요합니다.이 경우 상태 확인을 위해 런타임 내역이 필요합니다.
>* 워크플로우가 AND **분할로 들어갑니다**.이 경우 상태 확인을 위해 런타임 내역이 필요합니다.
>* 임시 워크플로우가 참가자 단계에 들어가면 모드(런타임 시)가 비일시적 워크플로우로 변경됩니다.작업이 사용자에게 전달되면 내역을 유지해야 합니다.
>



>[!CAUTION]
>
>일시적인 워크플로우 내에서는 이동 단계를 사용할 **수 없습니다**.
>
>이는 이동 **단계가** 슬링 작업을 만들어 `goto` 시점에 워크플로우를 계속합니다. 이로 인해 워크플로우가 일시적으로 중단되고 로그 파일에서 오류가 발생합니다.
>
>임시 워크플로우에서 결정을 내리기 위해 OR 분할을 사용할 수 **있습니다**.

>[!NOTE]
>
>일시적인 [워크플로우가](/help/assets/performance-tuning-guidelines.md#transient-workflows) 자산 성능에 미치는 영향에 대한 자세한 내용은 자산 모범 사례를 참조하십시오.

### 여러 리소스 지원 {#multi-resource-support}

워크플로우 **모델에 대한** 다중 리소스 지원 활성화는 여러 리소스를 선택하더라도 단일 워크플로우 인스턴스가 시작됨을 의미합니다.이러한 항목은 패키지로 첨부됩니다.

워크플로우 **모델에 대해 다중 리소스** 지원이 활성화되지 않고 여러 리소스를 선택한 경우 각 리소스에 대해 개별 워크플로우 인스턴스가 시작됩니다.

>[!NOTE]
>
>자세한 [내용은 다중 리소스 지원을 위한](/help/sites-developing/workflows-models.md#configuring-a-workflow-for-multi-resource-support) 워크플로우 구성을 참조하십시오.

### 워크플로우 단계 {#workflow-stages}

워크플로우 단계는 작업 처리 시 워크플로우의 진행 상황을 시각화하는 데 도움이 됩니다. 워크플로우를 실행할 때와 마찬가지로 사용자는 개별 단계가 아닌 스테이지에서 설명하는 진행 상황을 볼 수 **있으므로** 처리 과정의 개요를 제공하는 데 사용할 수 있습니다.

개별 단계 이름은 구체적이고 기술적일 수 있으므로 워크플로우 진행에 대한 개념적인 보기를 제공하도록 스테이지 이름을 정의할 수 있습니다.

예를 들어 6단계 및 4단계의 워크플로우의 경우

1. 워크플로우 단계(워크플로우 진행 표시)를 [구성한 다음 워크플로우의](/help/sites-developing/workflows-models.md#configuring-workflow-stages-that-show-workflow-progress)각 단계에 적절한 단계를 지정할 수 있습니다.

   * 여러 스테이지 이름을 만들 수 있습니다.
   * 그런 다음 각 단계에 개별 스테이지 이름이 지정됩니다(하나 이상의 단계에 스테이지 이름을 지정할 수 있음).
   | **단계 이름** | **단계(단계에 지정됨)** |
   |---|---|
   | 1단계 | 만들기 |
   | 2단계 | 만들기 |
   | 3단계 | 리뷰 |
   | 4단계 | 승인 |
   | 5단계 | 완료 |
   | 6단계 | 완료 |

1. 워크플로우가 실행되면 사용자는 단계 이름 대신 스테이지 이름에 따라 진행 상황을 볼 수 있습니다. 워크플로우 진행 상태는 받은 편지함에 [나열된 작업 항목의](/help/sites-authoring/workflows-participating.md#opening-a-workflow-item-to-view-details-and-take-actions) 작업 세부 사항 창의 워크플로우 정보 탭에 표시됩니다 [](/help/sites-authoring/inbox.md).

### 워크플로우 및 양식 {#workflows-and-forms}

일반적으로 워크플로우는 AEM에서 양식 제출을 처리하는 데 사용됩니다. 표준 AEM 인스턴스에서 사용할 수 있는 구성 요소의 [핵심 구성 요소](https://helpx.adobe.com/experience-manager/core-components/using/form-container.html) 또는 AEM Forms 솔루션에서 사용할 [수 있습니다](/help/forms/using/aem-forms-workflow.md).

새 양식을 만들 때 양식 제출은 워크플로우 모델과 쉽게 연결될 수 있습니다.예를 들어, 컨텐츠를 저장소의 특정 위치에 저장하거나 사용자에게 양식 제출 및 해당 컨텐츠에 대해 알리기 위해.

### 워크플로우 및 번역 {#workflows-and-translation}

워크플로우는 번역 프로세스의 핵심 [부분이기도](/help/sites-administering/translation.md) 합니다.
