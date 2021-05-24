---
title: 버전 삭제
seo-title: 버전 삭제
description: 이 문서에서는 버전 삭제에 사용할 수 있는 옵션에 대해 설명합니다.
seo-description: 이 문서에서는 버전 삭제에 사용할 수 있는 옵션에 대해 설명합니다.
uuid: a9fa25c7-e60e-4665-a726-99af9aac8f70
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring
content-type: reference
discoiquuid: fb4d7337-7b94-430b-80d2-f1754f823c2b
docset: aem65
feature: 구성
exl-id: 6f0b1951-bdda-475f-b6c0-bc18de082b7c
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '740'
ht-degree: 2%

---

# 버전 삭제{#version-purging}

표준 설치에서는 컨텐츠를 업데이트한 후 페이지를 활성화할 때 AEM에서 새 버전의 페이지 또는 노드를 만듭니다.

>[!NOTE]
>
>컨텐츠가 변경되지 않으면 페이지가 활성화되었다는 메시지가 표시되지만 새 버전이 만들어지지 않습니다

사이드 킥의 **버전 관리** 탭을 사용하여 요청 시 추가 버전을 만들 수 있습니다. 이러한 버전은 리포지토리에 저장되며, 필요한 경우 복원할 수 있습니다.

이러한 버전은 제거되지 않으므로 저장소 크기가 시간이 지남에 따라 확장되므로 관리해야 합니다.

AEM에는 리포지토리를 관리하는 데 도움이 되는 다양한 메커니즘이 포함되어 있습니다.

* [버전 관리자](#version-manager)
새 버전을 만들 때 이전 버전을 삭제하도록 구성할 수 있습니다.

* [버전 삭제](/help/sites-deploying/monitoring-and-maintaining.md#purgeversionstool) 도구
저장소 모니터링 및 유지 관리의 일부로 사용됩니다.
이 매개 변수를 사용하면 다음 매개 변수에 따라 노드의 이전 버전 또는 노드 계층을 제거할 수 있습니다.

   * 저장소에 유지할 최대 버전 수입니다.
이 수를 초과하면 가장 오래된 버전이 제거됩니다.

   * 저장소에 보관되는 모든 버전의 최대 연령
버전의 페이지가 이 값을 초과하면 저장소에서 제거됩니다.

* [버전 삭제 유지 관리 작업](/help/sites-administering/operations-dashboard.md#automated-maintenance-tasks) 버전 삭제 유지 관리 작업을 스케줄링하여 이전 버전을 자동으로 삭제할 수 있습니다. 따라서 버전 삭제 도구를 수동으로 사용할 필요가 최소화됩니다.

>[!CAUTION]
>
>저장소 크기를 최적화하려면 버전 삭제 작업을 자주 실행해야 합니다. 제한된 트래픽 양이 있는 경우 업무 시간 외에 작업을 예약해야 합니다.

## 버전 관리자 {#version-manager}

버전 관리자는 삭제 도구를 사용하여 명시적 삭제 외에 새 버전을 만들 때 이전 버전을 삭제하도록 구성할 수 있습니다.

버전 관리자를 구성하려면 [다음에 대한 구성](/help/sites-deploying/configuring-osgi.md)을 만듭니다.

`PID com.day.cq.wcm.core.impl.VersionManagerImpl`

다음 옵션을 사용할 수 있습니다.

* `versionmanager.createVersionOnActivation` (부울, 기본값:true) 페이지가 활성화될 때 버전을 만들지 여부를 지정합니다.
버전 관리자에서 지정한 버전 생성을 표시하지 않도록 복제 에이전트가 구성되어 있지 않은 한 버전이 생성됩니다.
버전은 `versionmanager.ivPaths`에 포함된 경로에서 활성화가 발생하는 경우에만 만들어집니다(아래 참조).

* `versionmanager.ivPaths`(문자열[], 기본값: `{"/"}`) 가 true로 설정된 경우 활성화 시 암시적으로 버전이 생성되 `versionmanager.createVersionOnActivation` 는 경로를 지정합니다.

* `versionmanager.purgingEnabled` (부울, 기본값:false) 새 버전을 만들 때 제거를 활성화할지 여부를 정의합니다.

* `versionmanager.purgePaths` (문자열[], 기본값:{&quot;/content&quot;}) 새 버전을 만들 때 버전을 삭제할 경로를 지정합니다.

* `versionmanager.maxAgeDays` (int, 기본값:30) 버전 삭제 시 구성된 값보다 오래된 버전이 제거됩니다. 값이 1보다 작으면 버전 나이에 따라 지우기가 수행되지 않습니다.

* `versionmanager.maxNumberVersions` (int, 기본값 5) 버전 삭제 시 n번째 최신 버전보다 오래된 버전이 제거됩니다. 값이 1보다 작으면 버전 수를 기준으로 제거를 수행하지 않습니다.

* `versionmanager.minNumberVersions` (int, 기본값 0) 나이에 관계없이 유지되는 최소 버전 수입니다. 값이 1보다 작은 값으로 설정되면 최소 버전 수는 유지되지 않습니다.

>[!NOTE]
>
>리포지토리에 많은 버전을 유지하는 것은 권장되지 않습니다. 따라서 버전 삭제 작업을 구성할 때 삭제 작업에서 너무 많은 버전을 제외하지 않도록 주의하십시오. 그렇지 않으면 저장소 크기가 제대로 최적화되지 않습니다. 비즈니스 요구 사항으로 인해 많은 버전을 유지하는 경우 Adobe 지원 센터에 문의하여 저장소 크기를 최적화하는 다른 방법을 찾으십시오.

### 유지 옵션 결합 {#combining-retention-options}

요구 사항에 따라 어떤 버전을 유지해야 하는지 정의하는 옵션( `maxAgeDays`, `maxNumberVersions`, `minNumberVersions`)을 결합할 수 있습니다.

예를 들어, 유지할 최대 버전 수와 유지할 가장 오래된 버전을 정의할 때

* 설정:

   * `maxNumberVersions` = 7

   * `maxAgeDays` = 30

* 사용:

   * 지난 60일 내에 만들어진 10개 버전
   * 지난 30일 내에 만들어진 버전 중 3개

* 이것의 의미는 다음과 같습니다.

   * 마지막 3가지 버전이 유지됩니다

예를 들어, 유지할 최대 버전 및 최소 버전 수와 유지할 가장 오래된 버전을 정의할 때

* 설정:

   * `maxNumberVersions` = 3
   * `maxAgeDays` = 30
   * `minNumberVersions` = 3

* 사용:

   * 60일 전에 만들어진 5개 버전

* 이것의 의미는 다음과 같습니다.

   * 3개의 버전이 유지됩니다.

## 버전 제거 도구 {#purge-versions-tool}

[버전 삭제](/help/sites-deploying/monitoring-and-maintaining.md#purgeversionstool) 도구는 저장소의 노드 버전 또는 노드 계층 구조를 삭제하기 위한 것입니다. 기본 목적은 이전 버전의 노드를 제거하여 저장소 크기를 줄이는 데 도움이 됩니다.
