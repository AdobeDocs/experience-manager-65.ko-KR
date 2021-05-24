---
title: 워크플로우 우수 사례
seo-title: 워크플로우 우수 사례
description: 워크플로우 우수 사례
seo-description: 'null'
uuid: 79be4055-c2ef-428e-9054-103c6cfde1d2
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: 0be8b88c-6f57-4dcc-ae11-77b378a2decd
exl-id: 14775476-6fe5-4583-8ab5-b55fef892174
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1924'
ht-degree: 1%

---

# 워크플로우 우수 사례{#workflow-best-practices}

워크플로우를 통해 Adobe Experience Manager(AEM) 활동을 자동화할 수 있습니다.

종종 AEM 환경에서 발생하는 많은 양의 처리를 나타내므로 사용자 지정 워크플로우 단계가 우수 사례에 따라 작성되지 않거나 기본 워크플로우가 최대한 효율적으로 실행되도록 구성되지 않으면 결과적으로 시스템이 손상될 수 있습니다.

따라서 워크플로우 구현을 신중하게 계획하는 것이 좋습니다.

## 구성 {#configuration}

워크플로우 프로세스(사용자 지정 및/또는 기본 제공)를 구성할 때 기억해야 할 사항이 몇 가지 있습니다.

### 임시 워크플로우 {#transient-workflows}

높은 수집 로드를 최적화하려면 [워크플로우를 임시](/help/sites-developing/workflows.md#transient-workflows)으로 정의할 수 있습니다.

워크플로우가 일시적일 때 중간 작업 단계와 관련된 런타임 데이터는 실행 시 JCR에서 지속되지 않습니다(출력 표현물은 물론 지속됨).

다음과 같은 이점이 있습니다.

* 워크플로우 처리 시간 단축최대 10%.
* 저장소 증가를 크게 줄입니다.
* 삭제하는 데 더 이상 CRUD 워크플로우가 필요하지 않습니다.
* 또한 압축할 TAR 파일 수를 줄입니다.

>[!CAUTION]
>
>감사를 위해 워크플로우 런타임 데이터를 유지/아카이빙해야 한다고 비즈니스 지시하는 경우 이 기능을 활성화하지 마십시오.

### DAM 워크플로우 조정 {#tuning-dam-workflows}

DAM 워크플로우에 대한 성능 조정 지침은 [AEM Assets 성능 조정 가이드](/help/assets/performance-tuning-guidelines.md)를 참조하십시오.

### 동시 실행 워크플로우의 최대 수 구성 {#configure-the-maximum-number-of-concurrent-workflows}

AEM에서는 여러 워크플로우 스레드를 동시에 실행할 수 있습니다. 기본적으로 스레드 수는 시스템에 있는 프로세서 코어 수의 절반으로 구성됩니다.

실행 중인 워크플로우가 시스템 리소스를 필요로 하는 경우 AEM에서 작성 UI 렌더링과 같은 다른 작업에 거의 사용하지 않을 수 있습니다. 따라서 벌크 이미지 업로드와 같은 활동 중에는 시스템 속도가 느려질 수 있습니다.

이 문제를 해결하려면 **최대 병렬 작업** 수를 시스템에 있는 프로세서 코어 수의 절반에서 3/4 사이여야 합니다. 이렇게 하면 시스템이 이러한 워크플로우를 처리할 때 응답성을 유지할 수 있는 충분한 용량을 사용할 수 있습니다.

**최대 병렬 작업**&#x200B;을 구성하려면 다음 중 하나를 수행할 수 있습니다.

* AEM 웹 콘솔에서 **[OSGi 구성](/help/sites-deploying/configuring-osgi.md)**&#x200B;을 구성합니다.**큐의 경우:Granite 워크플로우 큐**(**Apache Sling 작업 큐 구성**).

* AEM 웹 콘솔의 **Sling 작업** 옵션에서 큐를 구성할 수 있습니다.**작업 큐 구성의 경우:Granite Workflow 큐**, `http://localhost:4502/system/console/slingevent`에 있습니다.

또한 **Granite Workflow 외부 프로세스 작업 큐**&#x200B;에 대한 별도의 구성이 있습니다. 외부 바이너리를 실행하는 워크플로우 프로세스(예: **InDesign Server** 또는 **이미지 Magick**)에 사용됩니다.

### 개별 작업 큐 구성 {#configure-individual-job-queues}

경우에 따라 개별 작업 기준으로 동시 스레드 또는 기타 큐 옵션을 제어하도록 개별 작업 대기열을 구성하는 것이 유용합니다. **Apache Sling Job Queue Configuration** factory 를 통해 웹 콘솔에서 개별 큐를 추가하고 구성할 수 있습니다. 나열할 적절한 항목을 찾으려면 워크플로우의 모델을 실행하고 **Sling 작업** 콘솔에서 찾습니다.예를 들어 `http://localhost:4502/system/console/slingevent`에서 사용할 수 있습니다.

임시 워크플로우에 대한 개별 작업 큐도 추가할 수 있습니다.

### 워크플로우 삭제 구성 {#configure-workflow-purging}

표준 설치 AEM에서는 일별 및 주별 유지 관리 활동을 예약하고 구성할 수 있는 유지 관리 콘솔을 제공합니다.예를 들어, at:

`http://localhost:4502/libs/granite/operations/content/maintenance.html`

기본적으로 **주별 유지 관리 창**&#x200B;에는 **워크플로우 삭제** 작업이 있지만, 실행되기 전에 구성해야 합니다. 워크플로우 삭제를 구성하려면 웹 콘솔에 새로운 **Granite Workflow 제거 구성 Adobe**&#x200B;를 추가해야 합니다.

AEM의 유지 관리 작업에 대한 자세한 내용은 [작업 대시보드](/help/sites-administering/operations-dashboard.md)를 참조하십시오.

## 사용자 지정 {#customization}

사용자 지정 워크플로우 프로세스를 작성할 때 기억해야 할 몇 가지 사항이 있습니다.

### 위치 {#locations}

워크플로우 모델, 런처, 스크립트 및 알림에 대한 정의는 유형에 따라 저장소에 유지됩니다.즉, 기본 제공, 사용자 정의 등

>[!NOTE]
>
>또한 [AEM 6.5의 저장소 구조 변경](/help/sites-deploying/repository-restructuring.md)을 참조하십시오.

#### 위치 - 워크플로우 모델 {#locations-workflow-models}

워크플로우 모델은 유형에 따라 저장소에 저장됩니다.

* 기본 워크플로우 디자인은 다음 경로 아래에 있습니다.

   `/libs/settings/workflow/models/`

   >[!CAUTION]
   >
   >금지 사항:
   >
   >* 사용자 지정 워크플로우 모델을 이 폴더에 배치합니다.
   >* `/libs`에 있는 모든 항목 편집

   >
   >업그레이드 시 또는 핫픽스, 누적 수정 팩 또는 서비스 팩을 설치할 때 변경 사항을 덮어쓸 수 있습니다.

* 사용자 지정 워크플로우 디자인은 다음 위치에 유지됩니다.

   ```
   /conf/global/settings/workflow/models/...
   ```

* 런타임 워크플로우 디자인(기본 제공 및 사용자 지정 모두)은 다음 경로 아래에 있습니다.

   `/var/workflow/models/`

* 기존 워크플로우 디자인(디자인 타임 및 런타임 모두)은 다음 경로 아래에 유지됩니다.

   `/etc/workflow/models/`

   >[!NOTE]
   >
   >이러한 디자인을 AEM UI *를 사용하여*&#x200B;편집하면 세부 사항이 새 위치에 복사됩니다.

#### 위치 - 워크플로우 런처 {#locations-workflow-launchers}

워크플로우 실행 관리자 정의는 다음과 같은 유형별로 저장소에 저장됩니다.

* 기본 제공 워크플로우 런처는 다음 경로에 있습니다.

   `/libs/settings/workflow/launcher/`

   >[!CAUTION]
   >
   >금지 사항:
   >
   >* 이 폴더에 사용자 지정 워크플로우 런처를 배치합니다.
   >* `/libs`에 있는 모든 항목 편집

   >
   >업그레이드 시 또는 핫픽스, 누적 수정 팩 또는 서비스 팩을 설치할 때 변경 사항을 덮어쓸 수 있습니다.

* 사용자 지정 워크플로우 런처는 다음과 같이 보관됩니다.

   ```
   /conf/global/settings/workflow/launcher/...
   ```

* 이전 워크플로우 런처는 다음 경로에 있습니다.

   `/etc/workflow/launcher/`

   >[!NOTE]
   >
   >이러한 정의를 AEM UI *를 사용하여*&#x200B;편집하면 세부 사항이 새 위치에 복사됩니다.

#### 위치 - 워크플로우 스크립트 {#locations-workflow-scripts}

워크플로우 스크립트는 또한 유형에 따라 저장소에 저장됩니다.

* 기본 워크플로우 스크립트는 다음 경로 아래에 있습니다.

   `/libs/workflow/scripts/`

   >[!CAUTION]
   >
   >금지 사항:
   >
   >* 사용자 지정 워크플로우 스크립트를 이 폴더에 배치합니다.
   >* `/libs`에 있는 모든 항목 편집

   >
   >업그레이드 시 또는 핫픽스, 누적 수정 팩 또는 서비스 팩을 설치할 때 변경 사항을 덮어쓸 수 있습니다.

* 사용자 지정 워크플로우 스크립트는 다음과 같이 보관됩니다.

   ```
   /apps/workflow/scripts/...
   ```

* 기존 워크플로우 스크립트는 다음 경로 아래에 있습니다.

   `/etc/workflow/scripts/`

#### 위치 - 워크플로우 알림 {#locations-workflow-notifications}

워크플로우 알림은 유형별로 저장소에 저장됩니다.

* 기본 워크플로우 알림 정의는 다음 경로 아래에 있습니다.

   `/libs/settings/workflow/notification/`

   >[!CAUTION]
   >
   >금지 사항:
   >
   >* 사용자 지정 워크플로우 알림 정의를 이 폴더에 배치합니다.
   >* `/libs`에 있는 모든 항목 편집

   >
   >업그레이드 시 또는 핫픽스, 누적 수정 팩 또는 서비스 팩을 설치할 때 변경 사항을 덮어쓸 수 있습니다.

* 사용자 지정 워크플로우 알림 정의는 다음과 같이 유지됩니다.

   ```
   /conf/global/settings/workflow/notification/...
   ```

   >[!NOTE]
   >
   >워크플로우 알림 텍스트를 재정의하려면 아래에 오버레이된 경로를 만듭니다.
   >
   >
   >`/conf/global/settings/workflow/notification/<path-under-libs>`

* 기존 워크플로우 알림 정의는 다음 경로 아래에 있습니다.

   `/etc/workflow/notification/`

### 프로세스 세션 {#process-sessions}

모든 사용자 지정 개발에서와 마찬가지로, 가능하면 항상 사용자의 세션을 사용하는 것이 좋습니다.

* 보안 지침을 잘 준수하기 위해
* 시스템에서 세션 열기 및 닫기 관리

워크플로우 프로세스를 구현할 때:

* 워크플로우 세션이 제공되며, 특별한 사유가 없으면 사용해야 합니다.
* 워크플로우 단계에서 새 세션을 만들면 워크플로우 엔진에서 가능한 동시 실행 문제와 함께 상태가 일치하지 않습니다.
* 워크플로우의 프로세스 단계 내에서 새 JCR 세션을 획득하지 않아야 합니다.프로세스 단계 API에서 제공하는 워크플로우 세션을 jcr 세션에 조정해야 합니다. 예:

```
public void execute(WorkItem item, WorkflowSession workflowSession, MetaDataMap args) throws WorkflowException {
        // to obtain a jcr session:
        javax.jcr.Session jcrSession = workflowSession.adaptTo(javax.jcr.Session.class);

        // to obtain a sling resource resolver:
        org.apache.sling.api.resource.ResourceResolver slingResourceResolver = workflowSession.adaptTo(org.apache.sling.api.resource.ResourceResolver.class);
```

세션 저장:

* 워크플로우 프로세스 내에서 `WorkflowSession` 을 사용하여 리포지토리를 수정하는 경우 세션을 명시적으로 저장하지 마십시오. 워크플로우는 완료되면 세션을 저장합니다.
* `Session.Save` 워크플로우 단계 내에서 호출하면 안 됩니다.

   * 워크플로우 jcr 세션을 조정하는 것이 좋습니다.그런 다음 워크플로우 실행이 완료되면 워크플로우 엔진이 세션을 자동으로 저장하므로 `save` 이 필요하지 않습니다.
   * 프로세스 단계에서 자체 jcr 세션을 만들지 않는 것이 좋습니다.

* 불필요한 저하를 제거하여 오버헤드를 줄이고 워크플로우를 보다 효율적으로 만들 수 있습니다.

>[!CAUTION]
>
>여기에서 권장 사항에도 불구하고 고유한 jcr 세션을 만드는 경우 저장해야 합니다.

### 런처 수/범위 최소화 {#minimize-the-number-scope-of-launchers}

등록된 모든 [워크플로 런처](/help/sites-administering/workflows-starting.md#workflows-launchers)에 대한 책임이 있는 리스너가 하나 있습니다.

* 다른 런처의 전역 특성에 지정된 모든 경로에서 변경 사항을 수신합니다.
* 이벤트가 전달되면 워크플로우 엔진은 각 런처를 평가하여 실행해야 하는지 확인합니다.

너무 많은 런처를 만들면 평가 프로세스가 더 느리게 실행됩니다.

단일 시작 관리자에 있는 저장소의 루트에 글로벌 경로를 만들면 워크플로우 엔진이 저장소의 모든 노드에 대해 이벤트를 수신 및 평가하고 생성/수정합니다. 이러한 이유로 필요한 런처를 만들고 가능한 한 구체적으로 글로벌 경로를 만드는 것이 좋습니다.

이러한 런처가 워크플로우 동작에 미치는 영향 때문에 사용하지 않는 기본 런처를 비활성화하는 데에도 도움이 될 수 있습니다.

### 런처 {#configuration-enhancements-for-launchers} 구성 개선

사용자 지정 [시작 관리자 구성](/help/sites-administering/workflows-starting.md#workflows-launchers)이 개선되어 다음을 지원합니다.

* 여러 &quot;AND&quot;를 함께 정의하십시오.
* 단일 조건 내에 OR 조건이 있습니다.
* 기능 플래그가 활성화되어 있는지 또는 비활성화되어 있는지에 따라 런처를 비활성화/활성화합니다.
* 시작 관리자 조건에서 regex를 지원합니다.

### 다른 워크플로우에서 워크플로우를 시작하지 않음 {#do-not-start-workflows-from-other-workflows}

워크플로우는 메모리에서 생성된 객체와 저장소에서 추적된 노드 측면에서 상당한 오버헤드를 수행할 수 있습니다. 이러한 이유로 추가 워크플로우를 시작하지 않고 워크플로우 자체 내에서 처리를 수행하는 것이 좋습니다.

예로는 컨텐츠 세트에서 비즈니스 프로세스를 구현한 다음 해당 컨텐츠를 활성화하는 워크플로우가 있습니다. 게시해야 하는 각 컨텐츠 노드에 대해 **Activate Content** 모델을 시작하지 않고 이러한 각 노드를 활성화하는 사용자 지정 워크플로우 프로세스를 만드는 것이 좋습니다. 이 접근 방식을 사용하려면 추가 개발 작업이 필요하지만, 각 활성화에 대해 별도의 워크플로우 인스턴스를 시작하는 것보다 실행 시 더 효율적입니다.

다른 예로는 여러 노드를 처리하고 워크플로우 패키지를 만든 다음 해당 패키지를 활성화하는 워크플로우가 있습니다. 패키지를 만든 다음 패키지를 페이로드로 사용하여 별도의 워크플로우를 시작하는 대신 패키지를 만드는 단계에서 워크플로우의 페이로드를 변경한 다음 단계를 호출하여 동일한 워크플로우 모델 내에서 패키지를 활성화할 수 있습니다.

### 핸들러 진행 {#handler-advance}

워크플로우 모델을 디자인할 때 워크플로우 단계에서 핸들러를 미리 활성화할 수 있는 옵션이 있습니다. 또는 워크플로우 단계에 코드를 추가하여 다음에 실행해야 하는 단계를 결정한 다음 실행할 수 있습니다.

성능이 향상되므로 핸들러 추가를 사용하는 것이 좋습니다.

### 워크플로우 단계 {#workflow-stages}

[워크플로우 단계](/help/sites-developing/workflows.md#workflow-stages)를 정의한 다음 작업/단계를 특정 워크플로우 단계에 할당할 수 있습니다.

이 정보는 **받은 편지함**](/help/sites-authoring/workflows-participating.md#opening-a-workflow-item-to-view-details-and-take-actions)&#x200B;에서 작업 항목의 [**워크플로우 정보** 탭을 클릭할 때 워크플로우의 진행 상황을 표시하는 데 사용됩니다. 기존 워크플로우 모델을 편집하여 단계를 추가할 수 있습니다.

### 페이지 프로세스 활성화 단계 {#activate-page-process-step}

**페이지 활성화 프로세스** 단계에서는 페이지를 활성화하지만, 참조된 DAM 자산을 자동으로 찾아 활성화하지는 않습니다.

이 단계를 워크플로우 모델의 일부로 사용할 계획이라면 염두에 두어야 할 사항입니다.

### 업그레이드 고려 사항 {#upgrade-considerations}

인스턴스를 업그레이드할 때:

* 인스턴스가 업그레이드되기 전에 모든 사용자 지정 워크플로우 모델이 백업되었는지 확인합니다.
* [위치](#locations)에 저장된 사용자 지정 워크플로우가 없는지 확인합니다.

   * `/libs/settings/workflow/models/projects`

>[!NOTE]
>
>또한 [AEM 6.5의 저장소 구조 변경](/help/sites-deploying/repository-restructuring.md)을 참조하십시오.

## 시스템 도구 {#system-tools}

워크플로우 모니터링, 유지 관리 및 문제 해결에 도움이 되는 많은 시스템 도구를 사용할 수 있습니다. 아래의 모든 예제 URL은 `localhost:4502`을 사용하지만 모든 작성자 인스턴스( `<hostname>:<port>`)에서 사용할 수 있습니다.

### Sling 작업 처리 콘솔 {#sling-job-handling-console}

`http://localhost:4502/system/console/slingevent`

Sling 작업 처리 콘솔이 표시됩니다.

* 마지막 다시 시작 이후 시스템의 작업 상태에 대한 통계입니다.
* 또한 모든 작업 큐에 대한 구성을 표시하고 구성 관리자에서 해당 구성을 편집하는 바로 가기를 제공합니다.

### 워크플로우 보고서 도구 {#workflow-report-tool}

워크플로우 보고 도구는 성능 저하를 방지하기 위해 6.3에서 제거됩니다.

### 워크플로우 유지 관리 작업 MBean {#workflow-maintenance-operations-mbean}

`http://localhost:4502/system/console/jmx/com.adobe.granite.workflow:type=Maintenance`

워크플로우 유지 관리 MBean은 완료된 워크플로우 삭제 및 워크플로우 통계 검색과 같은 여러 유용한 유지 관리 루틴을 표시합니다.

## 추가 정보 {#further-information}

자세한 내용은 다음을 참조하십시오.

* [워크플로우 작업](/help/sites-authoring/workflows.md)
* [워크플로우 관리](/help/sites-administering/workflows.md)
* [워크플로우 개발 및 확장](/help/sites-developing/workflows.md)
* [성능 최적화](/help/sites-deploying/configuring-performance.md)
