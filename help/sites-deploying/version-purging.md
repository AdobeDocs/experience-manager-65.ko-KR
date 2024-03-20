---
title: 버전 삭제
description: 이 문서에서는 버전 삭제에 사용 가능한 옵션에 대해 설명합니다.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring
content-type: reference
docset: aem65
feature: Configuring
exl-id: 6f0b1951-bdda-475f-b6c0-bc18de082b7c
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '726'
ht-degree: 0%

---

# 버전 삭제{#version-purging}

표준 설치에서 Adobe Experience Manager(AEM)는 콘텐츠를 업데이트한 후 페이지를 활성화하면 페이지 또는 노드의 버전을 생성합니다.

>[!NOTE]
>
>콘텐츠를 변경하지 않으면 페이지가 활성화되었지만 새 버전이 만들어지지 않았다는 메시지가 표시됩니다.

다음을 사용하여 요청에 대한 추가 버전을 만들 수 있습니다. **버전 관리** 사이드 킥의 탭 이러한 버전은 저장소에 저장되며 필요한 경우 복원할 수 있습니다.

이러한 버전은 삭제되지 않으므로 시간이 지남에 따라 저장소 크기가 커지므로 관리해야 합니다.

AEM에는 저장소를 관리하는 데 도움이 되는 다양한 메커니즘이 포함되어 있습니다.

* 다음 [버전 관리자](#version-manager)
새 버전을 만들 때 이전 버전을 제거하도록 구성할 수 있습니다.

* 다음 [버전 제거](/help/sites-deploying/monitoring-and-maintaining.md#purgeversionstool) 도구 저장소 모니터링 및 유지 관리의 일부로 사용됩니다.
이를 통해 다음 매개 변수에 따라 노드의 이전 버전 또는 노드 계층을 제거하도록 개입할 수 있습니다.

   * 저장소에 보관할 최대 버전 수.
이 수를 초과하면 가장 오래된 버전이 제거됩니다.

   * 저장소에 보관된 버전의 최대 기간.
버전 사용 기간이 이 값을 초과하면 저장소에서 제거됩니다.

* 다음 [버전 제거 유지 관리 작업](/help/sites-administering/operations-dashboard.md#automated-maintenance-tasks). 버전 제거 유지 관리 작업을 예약하여 이전 버전을 자동으로 삭제할 수 있습니다. 따라서 버전 제거 도구를 수동으로 사용할 필요가 없습니다.

>[!CAUTION]
>
>저장소 크기를 최적화하려면 버전 제거 작업을 자주 실행합니다. 제한된 트래픽 양이 있는 업무 시간 외에 작업을 예약해야 합니다.

## 버전 관리자 {#version-manager}

제거 도구를 사용하여 명시적으로 제거하는 것 외에도 새 버전을 작성할 때 이전 버전을 제거하도록 버전 관리자를 구성할 수 있습니다.

버전 관리자를 구성하려면 [구성 만들기](/help/sites-deploying/configuring-osgi.md) 대상:

`PID com.day.cq.wcm.core.impl.VersionManagerImpl`

다음 옵션을 사용할 수 있습니다.

* `versionmanager.createVersionOnActivation` (부울, 기본값: true) 페이지가 활성화될 때 버전을 만들지 여부를 지정합니다.
버전 관리자가 인정하는 버전 생성을 억제하도록 복제 에이전트가 구성되어 있지 않으면 버전이 만들어집니다.
버전은 포함 된 경로에서 활성화가 발생하는 경우에만 만들어집니다. `versionmanager.ivPaths` (아래 참조)

* `versionmanager.ivPaths`(문자열[], 기본값: `{"/"}`) 활성화 시 버전이 묵시적으로 생성되는 경로를 지정합니다. `versionmanager.createVersionOnActivation` 가 true로 설정되어 있는 경우

* `versionmanager.purgingEnabled` (부울, 기본값: false) 새 버전이 만들어질 때 지우기를 활성화할지 여부를 정의합니다.

* `versionmanager.purgePaths` (문자열[], 기본값: {&quot;/content&quot;}) 새 버전이 생성될 때 버전을 제거할 경로를 지정합니다.

* `versionmanager.maxAgeDays` (int, 기본값: 30) 버전 삭제 시 구성된 값보다 오래된 버전이 제거됩니다. 값이 1보다 작으면, 버전의 에이지를 기준으로 퍼지가 수행되지 않는다.

* `versionmanager.maxNumberVersions` (int, 기본값 5) 버전 삭제 시 n번째 최신 버전보다 오래된 버전은 제거됩니다. 값이 1보다 작은 경우에는 버전의 수에 기초하여 퍼지가 행해지지 않는다.

* `versionmanager.minNumberVersions` (int, 기본값 0) 나이에 관계없이 유지되는 최소 버전 수입니다. 이 값을 1보다 작은 값으로 설정하면 최소 버전 수가 유지되지 않습니다.

>[!NOTE]
>
>저장소에 많은 버전을 유지하는 것은 권장되지 않습니다. 따라서 버전 제거 작업을 구성할 때는 제거에서 너무 많은 버전을 제외하지 않도록 주의하십시오. 그렇게 하지 않으면 저장소 크기가 제대로 최적화되지 않습니다. 비즈니스 요구 사항으로 인해 많은 수의 버전을 유지하는 경우 Adobe 지원 센터에 문의하여 저장소 크기를 최적화할 수 있는 대체 방법을 확인하십시오.

### 보존 옵션 결합 {#combining-retention-options}

유지할 버전을 정의하는 옵션( `maxAgeDays`, `maxNumberVersions`, `minNumberVersions`)는 요구 사항에 따라 결합할 수 있습니다.

예를 들어 유지할 최대 버전 수와 유지할 가장 오래된 버전을 정의할 경우:

* 설정:

   * `maxNumberVersions` = 7

   * `maxAgeDays` = 30

* 포함:

   * 지난 60일 내에 10개의 버전이 만들어졌습니다
   * 이러한 버전 중 3개가 지난 30일 이내에 생성되었습니다

* 이는 다음을 의미합니다.

   * 마지막 세 버전은 유지됩니다

예를 들어 유지할 최대 AND 최소 버전 수와 유지할 가장 오래된 버전을 정의하는 경우:

* 설정:

   * `maxNumberVersions` = 3
   * `maxAgeDays` = 30
   * `minNumberVersions` = 3

* 포함:

   * 5 버전은 60 일 전에 만들어졌습니다.

* 이는 다음을 의미합니다.

   * 세 가지 버전이 유지됩니다.

## 버전 제거 도구 {#purge-versions-tool}

다음 [버전 제거](/help/sites-deploying/monitoring-and-maintaining.md#purgeversionstool) 도구는 저장소의 노드 또는 노드 계층 구조를 삭제하기 위한 것입니다. 기본 목적은 이전 버전의 노드를 제거하여 저장소 크기를 줄이는 데 도움이 됩니다.
