---
title: 소극적 컨텐츠 마이그레이션
description: Adobe Experience Manager 6.4의 레이지 콘텐츠 마이그레이션에 대해 알아봅니다.
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: upgrading
docset: aem65
feature: Upgrading
exl-id: 946c7c2a-806b-4461-a38b-9c2e5ef1e958
source-git-commit: 3885cc51f7e821cdb352737336a29f9c4f0c2f41
workflow-type: tm+mt
source-wordcount: '687'
ht-degree: 6%

---

# 소극적 컨텐츠 마이그레이션 {#lazy-content-migration}

이전 버전과의 호환성, 콘텐츠 및 구성을 위해 **/etc** 및 **/content** Adobe Experience Manager(AEM) 6.3부터 업그레이드와 함께 즉시 작업하거나 변환되지 않습니다. 이는 이러한 구조에 대한 고객 애플리케이션의 종속성이 그대로 유지되도록 하기 위한 것입니다. 기본 제공 AEM 6.5의 컨텐츠가 다른 위치에서 호스팅되더라도 이러한 컨텐츠 구조와 관련된 기능은 여전히 동일합니다.

그러한 위치들이 모두 자동으로 변환되지는 않을 수 있지만, 몇 가지 지연이 있다 `CodeUpgradeTasks` 레이지 콘텐츠 마이그레이션이라고도 합니다. 이렇게 하면 고객이 이 시스템 속성으로 인스턴스를 다시 시작하여 이러한 자동 변환을 트리거할 수 있습니다.

```shell
-Dcom.adobe.upgrade.forcemigration=true
```

이로 인해 다음이 발생합니다. `CodeUpgradeTasks` 마이그레이션 중에 실행할 수 있습니다.

이 업그레이드 프로세스는 효율적인 실행이 목적이지만 동기적으로 수행되기 때문에 처리해야 하는 컨텐츠의 양에 따라 다운타임이 발생합니다. Adobe은 프로덕션 시스템 이전의 스테이징 환경에서 실행 시간을 평가하여 유지 관리 기간에 따라 계획을 수립하는 것을 권장합니다.

이 작업에는 일반적으로 응용 프로그램 조정이 필요하므로 이 작업은 해당 응용 프로그램 배포와 함께 수행해야 합니다.

다음은 의 전체 목록입니다. `CodeUpgradeTasks` 6.5에 도입됨:

| **이름** | **관련성** **이전 AEM 버전의 경우** | **마이그레이션** **유형** | **세부 사항** |
|---|---|---|---|
| `Cq561ProjectContentUpgrade` | &lt; 5.6.1 | 즉시 |  |
| `Cq60MSMContentUpgrade` | &lt; 6.0 | 즉시 | 모두 감지 `LiveRelationShips` 출처: `VersionStorage` 이(가) 삭제되고 제외 속성이 부모에 추가됨 |
| `Cq61CloudServicesContentUpgrade` | &lt; 6.1 | 즉시 | 기본적으로 보안을 위해 cloudservices 재구성 |
| `Cq62ConfContentUpgrade` | &lt; 6.2 | 즉시 | 에서 속성 기반 연결 제거 **/content** 끝 **/conf** (OSGi 메커니즘으로 대체됨), 는 해당 OSGi 구성을 생성합니다. |
| `Cq62FormsContentUpgrade` | &lt; 6.2 | 즉시 | merge_preserve 처리로 인해 기본적으로 보안 거부 규칙은 지정된 권한을 무시하므로 업그레이드 시 순서를 변경해야 합니다 |
| `CQ62Html5SmartFileUpgrade` | &lt; 6.2 | 즉시 | Html5SmartFile 위젯을 사용하여 구성 요소를 감지하고 컨텐츠에서 구성 요소 사용을 검색하고 지속성을 재구성하여 바이너리를 한 수준 아래로 효과적으로 이동하고 구성 요소 수준에 저장하지 않습니다. |
| `Cq62ProjectsCodeUpgrade` | &lt; 6.2 | 즉시 | 이전 스타일 프로젝트를 다음으로 이동 **/etc/projects** 끝 **/content/projects** |
| `Cq62TargetCampaignsContentUpgrade` | &lt; 6.2 | 즉시 | 컨테이너 레이어를 계층(영역)에 소개하고 참조를 조정합니다. |
| `Cq62TargetContentUpgrade` | &lt; 6.2 | 즉시 | 고정 위치 이름을 대상 구성 요소로 설정합니다. |
| `Cq62WorkflowContentUpgrade` | &lt; 6.2 | 즉시 | 6.2 구조, 인스턴스, 알림을 미리 예측한 다음 백업 위치에서 다시 병합하는 워크플로우 모델의 복잡한 변환 **/var/backup** |
| `CQ63AssetsMetadataFormsUpdate` | &lt; 6.3 | 즉시 | 에서 에셋, 사용자 지정 메타데이터 스키마 및 처리 프로필 이동 **/apps** 끝 **/conf** 메타데이터 스키마 및 메타데이터 프로필 양식을 coral2에서 coral3로 변환합니다. |
| `CQ63AssetsSearchFacetsUpdate` | &lt; 6.3 | 즉시 | 에서 에셋 및 사용자 지정 검색 패싯 이동 **/apps** 끝 **/conf** 메타데이터 스키마 및 메타데이터 프로필 양식을 coral2에서 coral3로 변환합니다. |
| `CQ63InboxItemsUpgrade` | &lt; 6.3 | 즉시 | 받은 편지함 항목 정렬을 위한 InboxItems 업데이트(효율적인 정렬을 위해 메타데이터 조정) |
| `CQ63MetadataSchemaConfigUpdate` | &lt; 6.3 | 즉시 | 상대 경로를 다음으로 대체하여 폴더의 metadataSchema 속성을 조정합니다. **/conf** 의 대신에 **/apps** |
| `CQ63MobileAppsNavUpgrade` | &lt; 6.3 | 즉시 | 탐색 구조 조정 |
| `CQ63MonitoringDashboardsConfigUpdate` | &lt; 6.3 | 즉시 | 모니터링 대시보드에 대한 사용자 정의 구성을 다음에서 이동합니다. **/libs** 및 **/apps** |
| `CQ63ProcessingProfileConfigUpdate` | &lt; 6.3 | 즉시 | Assets의 processingProfile 속성(6.1까지 사용)을 6.3 이상 구조와 일치하도록 변환합니다. 또한 프로필의 상대 경로를으로 조정합니다 **/conf** 의 대신에 **/apps**. |
| `CQ63ToolsMenuEntriesContentUpgrade` | &lt; 6.3 | 즉시 | 업그레이드가 있는 경우 오래된 CRXDE Lite 및 웹 콘솔 메뉴 항목을 제거하는 업그레이드 작업입니다. |
| `CQ64CommunitiesConfigsCleanupTask` | &lt; 6.3 | 지연됨 | SRP 클라우드 구성, 커뮤니티 watchwords 구성 이동, 정리 **/etc/social** 및 **/etc/enablement** (레이지 마이그레이션이 실행될 때 모든 참조 및 데이터를 조정해야 하며, 더 이상 이 구조에 따라 애플리케이션 부품이 없어야 합니다.) |
| `CQ64LegacyCloudSettingsCleanupTask` | &lt; 6.4 | 지연됨 | 정리 **/etc/cloudsettings** (ContextHub 구성 포함). 구성은 첫 번째 액세스 시 자동으로 마이그레이션됩니다. 의 이 콘텐츠 업그레이드와 함께 레이지 콘텐츠 마이그레이션이 시작되는 경우 **/etc/cloudsettings** 는 업그레이드 전에 패키지를 통해 보존하고 암시적 변환이 시작되도록 다시 설치하고 완료 후 패키지를 후속 제거해야 합니다. |
| `CQ64UsersTitleFixTask` | &lt; 6.4 | 지연됨 | 기존 제목 구조를 사용자 프로필 노드의 제목으로 조정합니다. |
| `CQ64CommerceMigrationTask` | &lt; 6.4 | 지연됨 | 다음에서 상거래 콘텐츠 마이그레이션 **/etc/commerce** 끝 **/var/commerce**. 마이그레이션 중에 콘텐츠가 이동되고 이동된 콘텐츠에 대한 참조가 새 위치를 반영하도록 업데이트됩니다. |
| `CQ65DMMigrationTask` | &lt; 6.5 | 지연됨 | 에서 레거시 카탈로그 설정 및 Dynamic Media Cloud Services 설정 마이그레이션 **/etc** 끝 **/conf** |
| `CQ65LegacyClientlibsCleanupTask` | &lt; 6.5 | 지연됨 | 아래에 있는 기존 clientlibs 정리 **/etc/clientlibs** |
