---
title: 워크플로우 모범 사례
seo-title: Workflow Best Practices
description: Adobe Experience Manager에서 워크플로우 작업에 대한 모범 사례를 알아봅니다.
seo-description: null
uuid: 79be4055-c2ef-428e-9054-103c6cfde1d2
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: 0be8b88c-6f57-4dcc-ae11-77b378a2decd
exl-id: 14775476-6fe5-4583-8ab5-b55fef892174
source-git-commit: 10b370fd8f855f71c6d7d791c272137bb5e04d97
workflow-type: tm+mt
source-wordcount: '1925'
ht-degree: 1%

---

# 워크플로우 모범 사례{#workflow-best-practices}

워크플로를 사용하면 Adobe Experience Manager(AEM) 활동을 자동화할 수 있습니다.

종종 AEM 환경에서 발생하는 대량의 처리를 나타내므로 사용자 지정 워크플로우 단계가 모범 사례에 따라 작성되지 않거나 기본 워크플로우가 가능한 한 효율적으로 실행되도록 구성되지 않으면 시스템이 문제를 일으킬 수 있습니다.

따라서 워크플로우 구현을 신중하게 계획하는 것이 좋습니다.

## 구성 {#configuration}

워크플로우 프로세스(사용자 정의 및/또는 기본 제공)를 구성할 때 몇 가지 주의해야 할 사항이 있습니다.

### 임시 워크플로 {#transient-workflows}

높은 수집 로드를 최적화하기 위해 [임시 워크플로우임](/help/sites-developing/workflows.md#transient-workflows).

워크플로우가 일시적인 경우 중간 작업 단계와 관련된 런타임 데이터가 실행될 때 JCR에서 지속되지 않습니다(출력 렌디션은 지속됨).

장점은 다음과 같습니다.

* 워크플로우 처리 시간 최대 10% 단축.
* 저장소 증가 대폭 감소
* 제거하는 데 더 이상 CRUD 워크플로우가 필요하지 않습니다.
* 또한 TAR 파일 수를 줄여 줍니다.

>[!CAUTION]
>
>감사 목적으로 워크플로우 런타임 데이터를 유지/보관해야 하는 경우 이 기능을 활성화하지 마십시오.

### DAM 워크플로우 조정 {#tuning-dam-workflows}

DAM 워크플로우에 대한 성능 조정 지침은 [AEM Assets 성능 조정 안내서](/help/assets/performance-tuning-guidelines.md).

### 최대 동시 워크플로 수 구성 {#configure-the-maximum-number-of-concurrent-workflows}

AEM을 사용하면 여러 워크플로우 스레드를 동시에 실행할 수 있습니다. 기본적으로 스레드 수는 시스템의 프로세서 코어 수의 절반으로 구성됩니다.

실행 중인 워크플로우에서 시스템 리소스가 많이 필요한 경우, 이는 AEM이 작성 UI 렌더링과 같은 다른 작업에 사용할 수 있는 시간이 거의 없음을 의미할 수 있습니다. 그 결과, 벌크 이미지 업로드 등의 활동 중에 시스템이 부진할 수 있다.

Adobe 이 문제를 해결하려면 다음 수를 구성하는 것이 좋습니다. **최대 병렬 작업** 시스템에 있는 프로세서 코어 수의 절반~4분의 3 수준입니다. 이렇게 하면 이러한 워크플로우를 처리할 때 시스템이 응답성을 유지할 수 있는 충분한 용량이 허용됩니다.

구성하려면 **최대 병렬 작업**, 다음 중 하나를 수행할 수 있습니다.

* 구성 **[OSGi 구성](/help/sites-deploying/configuring-osgi.md)** AEM 웹 콘솔에서, **대기열: Granite 워크플로우 대기열** (an **Apache Sling 작업 큐 구성**).

* 다음에서 대기열 캔 구성 **Sling 작업** AEM 웹 콘솔 옵션, **작업 큐 구성: Granite 워크플로 큐**, `http://localhost:4502/system/console/slingevent`.

또한에 대한 별도의 구성이 있습니다. **Granite Workflow 외부 프로세스 작업 큐**. 다음과 같은 외부 바이너리를 시작하는 워크플로우 프로세스에 사용됩니다. **InDesign Server** 또는 **이미지 매직**.

### 개별 작업 큐 구성 {#configure-individual-job-queues}

경우에 따라 개별 작업 단위로 동시 스레드 또는 기타 대기열 옵션을 제어하도록 개별 작업 대기열을 구성하는 것이 유용합니다. 를 통해 웹 콘솔에서 개별 대기열을 추가하고 구성할 수 있습니다. **Apache Sling 작업 큐 구성** 공장. 나열할 적절한 주제를 찾으려면 워크플로우 모델을 실행하고 **Sling 작업** 콘솔(예: at) `http://localhost:4502/system/console/slingevent`.

임시 워크플로우에 대해서도 개별 작업 대기열을 추가할 수 있습니다.

### 워크플로우 삭제 구성 {#configure-workflow-purging}

표준 설치에서 AEM은 일별 및 주별 유지 관리 활동을 예약하고 구성할 수 있는 유지 관리 콘솔을 제공합니다. 예를 들면 다음과 같습니다.

`http://localhost:4502/libs/granite/operations/content/maintenance.html`

기본적으로 **주간 유지 관리 창** 다음 포함 **워크플로 삭제** 작업이 실행되기 전에 구성해야 합니다. 워크플로 삭제를 구성하려면 다음을 수행합니다. **Adobe Granite 워크플로우 삭제 구성** 을(를) 웹 콘솔에 추가해야 합니다.

AEM의 유지 관리 작업에 대한 자세한 내용은 [작업 대시보드](/help/sites-administering/operations-dashboard.md).

## 사용자 지정 {#customization}

사용자 지정 워크플로우 프로세스를 작성할 때 몇 가지 주의해야 할 사항이 있습니다.

### 위치 {#locations}

워크플로 모델, 런처, 스크립트 및 알림의 정의는 유형에 따라 리포지토리에 유지됩니다(즉, 사용자 지정 등).

>[!NOTE]
>
>참조: [AEM 6.5의 저장소 재구성](/help/sites-deploying/repository-restructuring.md).

#### 위치 - 워크플로 모델 {#locations-workflow-models}

워크플로 모델은 유형에 따라 저장소에 저장됩니다.

* 기본 워크플로우 디자인은 다음 경로에 보관됩니다.

  `/libs/settings/workflow/models/`

  >[!CAUTION]
  >
  >금지 사항:
  >
  >* 이 폴더에 사용자 지정 워크플로 모델 배치
  >* 에서 모든 항목 편집 `/libs`
  >
  >업그레이드 시 또는 핫픽스, 누적 수정 팩 또는 서비스 팩을 설치할 때 변경 사항을 덮어쓸 수 있습니다.

* 사용자 지정 워크플로 디자인은 아래에 유지됩니다.

  ```
  /conf/global/settings/workflow/models/...
  ```

* 런타임 워크플로우 디자인(기본 및 사용자 지정 모두)은 다음 경로 아래에 유지됩니다.

  `/var/workflow/models/`

* 레거시 워크플로 디자인(디자인 타임 및 런타임 모두)은 다음 경로 아래에 유지됩니다.

  `/etc/workflow/models/`

  >[!NOTE]
  >
  >이러한 디자인이 편집되는 경우 *AEM UI 사용*&#x200B;를 클릭하면 세부 정보가 새 위치에 복사됩니다.

#### 위치 - 워크플로우 런처 {#locations-workflow-launchers}

워크플로 시작 관리자 정의는 유형에 따라 저장소에도 저장됩니다.

* 즉시 사용 가능한 워크플로우 런처는 다음 경로 아래에 유지됩니다.

  `/libs/settings/workflow/launcher/`

  >[!CAUTION]
  >
  >금지 사항:
  >
  >* 이 폴더에 사용자 지정 워크플로우 런처를 배치합니다.
  >* 에서 모든 항목 편집 `/libs`
  >
  >업그레이드 시 또는 핫픽스, 누적 수정 팩 또는 서비스 팩을 설치할 때 변경 사항을 덮어쓸 수 있습니다.

* 사용자 지정 워크플로우 런처는 아래에 보관됩니다.

  ```
  /conf/global/settings/workflow/launcher/...
  ```

* 레거시 워크플로 시작 프로그램은 다음 경로에 보관됩니다.

  `/etc/workflow/launcher/`

  >[!NOTE]
  >
  >이러한 정의가 편집되는 경우 *AEM UI 사용*&#x200B;를 클릭하면 세부 정보가 새 위치에 복사됩니다.

#### 위치 - 워크플로 스크립트 {#locations-workflow-scripts}

워크플로 스크립트는 유형에 따라 저장소에도 저장됩니다.

* 기본 워크플로우 스크립트는 다음 경로 아래에 보관됩니다.

  `/libs/workflow/scripts/`

  >[!CAUTION]
  >
  >금지 사항:
  >
  >* 이 폴더에 사용자 지정 워크플로 스크립트를 배치합니다.
  >* 에서 모든 항목 편집 `/libs`
  >
  >업그레이드 시 또는 핫픽스, 누적 수정 팩 또는 서비스 팩을 설치할 때 변경 사항을 덮어쓸 수 있습니다.

* 사용자 지정 워크플로우 스크립트는 다음에 보관됩니다.

  ```
  /apps/workflow/scripts/...
  ```

* 레거시 워크플로우 스크립트는 다음 경로 아래에 보관됩니다.

  `/etc/workflow/scripts/`

#### 위치 - 워크플로 알림 {#locations-workflow-notifications}

또한 워크플로 알림은 유형에 따라 저장소에 저장됩니다.

* 기본 워크플로우 알림 정의는 다음 경로 아래에 유지됩니다.

  `/libs/settings/workflow/notification/`

  >[!CAUTION]
  >
  >금지 사항:
  >
  >* 이 폴더에 사용자 지정 워크플로 알림 정의를 배치합니다.
  >* 에서 모든 항목 편집 `/libs`
  >
  >업그레이드 시 또는 핫픽스, 누적 수정 팩 또는 서비스 팩을 설치할 때 변경 사항을 덮어쓸 수 있습니다.

* 사용자 지정 워크플로우 알림 정의는 아래에 있습니다.

  ```
  /conf/global/settings/workflow/notification/...
  ```

  >[!NOTE]
  >
  >워크플로우 알림 텍스트를 무시하려면 아래에 오버레이된 경로를 만듭니다.
  >
  >
  >`/conf/global/settings/workflow/notification/<path-under-libs>`

* 이전 워크플로우 알림 정의는 다음 경로에 유지됩니다.

  `/etc/workflow/notification/`

### 프로세스 세션 {#process-sessions}

모든 사용자 지정 개발에서와 마찬가지로 가능하면 항상 사용자의 세션을 사용하는 것이 좋습니다.

* 보안 지침을 최대한 준수할 것
* 시스템에서 세션 열기 및 닫기를 관리하도록 허용

워크플로우 프로세스를 구현할 때:

* 워크플로우 세션이 제공되며, 특별한 사유가 없는 한 사용해야 합니다.
* 상태가 일치하지 않고 워크플로우 엔진에서 발생할 수 있는 동시성 문제가 발생하므로 워크플로우 단계에서 새 세션을 만들면 안 됩니다.
* 워크플로우의 프로세스 단계 내에서 새 JCR 세션을 획득해서는 안 됩니다. 프로세스 단계 API에서 제공하는 워크플로우 세션을 jcr 세션으로 조정해야 합니다. 예:

```
public void execute(WorkItem item, WorkflowSession workflowSession, MetaDataMap args) throws WorkflowException {
        // to obtain a jcr session:
        javax.jcr.Session jcrSession = workflowSession.adaptTo(javax.jcr.Session.class);

        // to obtain a sling resource resolver:
        org.apache.sling.api.resource.ResourceResolver slingResourceResolver = workflowSession.adaptTo(org.apache.sling.api.resource.ResourceResolver.class);
```

세션 저장:

* 워크플로 프로세스 내에서 `WorkflowSession` 은(는) 저장소를 수정하는 데 사용되고 세션을 명시적으로 저장하지 않습니다. 워크플로우는 완료될 때 세션을 저장합니다.
* `Session.Save` 은(는) 워크플로 단계 내에서 호출하면 안 됩니다.

   * 워크플로우 jcr 세션을 조정하는 것이 좋습니다. 그런 다음 `save` 워크플로 실행이 완료되면 워크플로 엔진이 세션을 자동으로 저장하므로 이 필요하지 않습니다.
   * 프로세스 단계에서 자체 jcr 세션을 만들지 않는 것이 좋습니다.

* 불필요한 저장을 제거함으로써 오버헤드를 줄여 워크플로우의 효율성을 높일 수 있습니다.

>[!CAUTION]
>
>여기에 권장 사항에도 불구하고 자체 jcr 세션을 만드는 경우 저장해야 합니다.

### 런처 수/범위 최소화 {#minimize-the-number-scope-of-launchers}

모든 작업을 담당하는 청취자가 한 명 있습니다. [워크플로우 런처](/help/sites-administering/workflows-starting.md#workflows-launchers) 등록됨:

* 다른 런처의 글로빙 속성에 지정된 모든 경로에서 변경 사항을 수신하게 됩니다.
* 이벤트가 발송되면 워크플로우 엔진은 각 런처를 평가하여 실행 여부를 결정합니다.

런처를 너무 많이 만들면 평가 프로세스가 더 느리게 실행됩니다.

단일 런처에서 저장소 루트에 글로빙 경로를 만들면 워크플로 엔진은 저장소의 모든 노드에 대한 만들기/수정 이벤트를 수신하고 평가하게 됩니다. 이러한 이유로 필요한 런처만 만들고 글로빙 경로를 가능한 구체적으로 만드는 것이 좋습니다.

이러한 런처가 워크플로 동작에 미치는 영향 때문에 사용 중이 아닌 바로 사용 가능한 런처를 비활성화하는 것도 도움이 될 수 있습니다.

### 런처 구성 개선 사항 {#configuration-enhancements-for-launchers}

사용자 정의 [런처 구성](/help/sites-administering/workflows-starting.md#workflows-launchers) 이(가) 다음을 지원하도록 향상되었습니다.

* 여러 조건 &quot;AND&quot;를 함께 사용해야 합니다.
* 단일 조건 내에 OR 조건이 있습니다.
* 기능 플래그의 활성화 여부에 따라 런처를 비활성화/활성화합니다.
* 런처 조건에서 정규 표현식을 지원합니다.

### 다른 워크플로우에서 워크플로우 시작 안 함 {#do-not-start-workflows-from-other-workflows}

워크플로우에서는 메모리에서 만든 객체와 저장소에서 추적한 노드 측면에서 모두 상당한 오버헤드를 처리할 수 있습니다. 따라서 추가 워크플로우를 시작하는 것보다 워크플로우가 자체 내에서 처리되도록 하는 것이 좋습니다.

한 세트의 콘텐츠에서 비즈니스 프로세스를 구현한 다음 해당 콘텐츠를 활성화하는 워크플로우가 이러한 예에 해당합니다. 을(를) 시작하는 것보다 이러한 각 노드를 활성화하는 사용자 지정 워크플로우 프로세스를 만드는 것이 좋습니다. **콘텐츠 활성화** 게시해야 하는 각 콘텐츠 노드에 대한 모델입니다. 이 접근 방식은 추가 개발 작업이 필요하지만 각 활성화에 대해 별도의 워크플로우 인스턴스를 시작하는 것보다 실행할 때 더 효율적입니다.

또 다른 예는 여러 노드를 처리하고, 워크플로우 패키지를 만든 다음, 상기 패키지를 활성화하는 워크플로우입니다. 패키지를 만든 다음 패키지를 페이로드로 사용하여 별도의 워크플로우를 시작하는 대신 패키지를 만드는 단계에서 워크플로우의 페이로드를 변경한 다음 단계를 호출하여 동일한 워크플로우 모델 내에서 패키지를 활성화할 수 있습니다.

### 핸들러 진행 {#handler-advance}

워크플로우 모델을 디자인할 때 워크플로우 단계에서 핸들러를 미리 활성화할 수 있는 옵션이 있습니다. 또는 워크플로우 단계에 코드를 추가하여 다음에 실행할 단계를 결정한 다음 실행할 수 있습니다.

더 나은 성능을 제공하므로 핸들러를 미리 사용하는 것이 좋습니다.

### 워크플로 단계 {#workflow-stages}

다음을 정의할 수 있습니다. [워크플로 단계](/help/sites-developing/workflows.md#workflow-stages)을 클릭한 다음 작업/단계를 특정 워크플로 단계에 할당합니다.

이 정보는 다음을 클릭할 때 워크플로우의 진행률을 표시하는 데 사용됩니다. [**워크플로 정보** 에서 작업 항목 탭 **받은 편지함**](/help/sites-authoring/workflows-participating.md#opening-a-workflow-item-to-view-details-and-take-actions). 기존 워크플로 모델을 편집하여 단계를 추가할 수 있습니다.

### 페이지 활성화 프로세스 단계 {#activate-page-process-step}

다음 **페이지 활성화 프로세스** 단계는 페이지를 활성화하지만 참조된 DAM 에셋을 자동으로 찾지 않고 활성화하지도 않습니다.

이 단계를 워크플로우 모델의 일부로 사용하려는 경우 이 점을 염두에 두어야 합니다.

### 업그레이드 고려 사항 {#upgrade-considerations}

인스턴스를 업그레이드할 때:

* 인스턴스가 업그레이드되기 전에 모든 사용자 정의 워크플로 모델이 백업되었는지 확인하십시오.
* 사용자 지정 워크플로가 아래에 저장되지 않았는지 확인합니다. [위치](#locations):

   * `/libs/settings/workflow/models/projects`

>[!NOTE]
>
>참조: [AEM 6.5의 저장소 재구성](/help/sites-deploying/repository-restructuring.md).

## 시스템 도구 {#system-tools}

워크플로우 모니터링, 유지 관리 및 문제 해결에 도움이 되는 다양한 시스템 도구가 있습니다. 아래의 모든 예제 URL 사용 `localhost:4502`, 그러나 모든 작성자 인스턴스에서 사용할 수 있어야 합니다( `<hostname>:<port>`).

### Sling 작업 처리 콘솔 {#sling-job-handling-console}

`http://localhost:4502/system/console/slingevent`

Sling 작업 처리 콘솔에 다음이 표시됩니다.

* 마지막 다시 시작 이후 시스템의 작업 상태에 대한 통계입니다.
* 또한 모든 작업 대기열에 대한 구성을 표시하고 구성 관리자에서 바로 가기를 편집할 수 있습니다.

### 워크플로우 보고서 도구 {#workflow-report-tool}

성능 저하를 방지하기 위해 워크플로우 보고 도구를 6.3에서 제거하고 있습니다.

### 워크플로우 유지 관리 작업 MBean {#workflow-maintenance-operations-mbean}

`http://localhost:4502/system/console/jmx/com.adobe.granite.workflow:type=Maintenance`

워크플로우 유지 관리 MBean은 완료된 워크플로우 삭제 및 워크플로우 통계 검색과 같은 몇 가지 유용한 유지 관리 루틴을 노출합니다.

## 추가 정보 {#further-information}

자세한 내용은 다음을 참조하십시오.

* [워크플로를 사용하여 작업](/help/sites-authoring/workflows.md)
* [워크플로 관리](/help/sites-administering/workflows.md)
* [워크플로 개발 및 확장](/help/sites-developing/workflows.md)
* [성능 최적화](/help/sites-deploying/configuring-performance.md)
