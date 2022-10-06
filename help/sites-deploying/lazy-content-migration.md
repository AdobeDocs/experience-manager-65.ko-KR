---
title: 레이지 컨텐츠 마이그레이션
seo-title: Lazy Content Migration
description: AEM 6.4의 레이지 컨텐츠 마이그레이션에 대해 알아봅니다.
seo-description: Learn about Lazy Content Migration in AEM 6.4.
uuid: f5b0aa84-5638-4708-9da2-89964d394632
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: upgrading
discoiquuid: d72b8844-d782-4b5b-8999-338217dbefb9
docset: aem65
feature: Upgrading
exl-id: 946c7c2a-806b-4461-a38b-9c2e5ef1e958
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '694'
ht-degree: 6%

---

# 레이지 컨텐츠 마이그레이션 {#lazy-content-migration}

이전 버전과의 호환성, 콘텐츠 및 구성을 위해 **/etc** 및 **/content** AEM 6.3부터 업그레이드로 즉시 터치하거나 변형되지 않습니다. 이 작업은 해당 구조에 대한 고객 애플리케이션의 종속성이 그대로 유지되도록 하기 위해 수행됩니다. 즉시 사용 가능한 AEM 6.5의 컨텐츠가 다른 위치에서 호스팅되더라도 이러한 컨텐츠 구조와 관련된 기능은 여전히 동일합니다.

이러한 모든 위치가 자동으로 변형되는 것은 아니지만, 몇 가지 지연이 있습니다 `CodeUpgradeTasks` 레이지 컨텐츠 마이그레이션이라고도 합니다. 이를 통해 고객은 이 시스템 속성으로 인스턴스를 다시 시작하여 이러한 자동 변환을 트리거할 수 있습니다.

```shell
-Dcom.adobe.upgrade.forcemigration=true
```

이 경우 `CodeUpgradeTasks` 마이그레이션 중에 실행할 수 없습니다.

목적은 효율적인 실행이지만, 이 업그레이드 프로세스는 동기화되므로 처리해야 하는 컨텐츠의 양에 따라 다운타임이 발생합니다. 유지 관리 기간에 따라 계획을 수립하려면 프로덕션 시스템 앞의 스테이지 환경에서 실행 시간을 평가하는 것이 좋습니다.

일반적으로 응용 프로그램을 조정해야 하므로 이 작업은 해당 응용 프로그램 배포와 함께 수행해야 합니다.

아래는 `CodeUpgradeTasks` 6.5에서 도입됨:

| **이름** | **관련** **이전 AEM 버전의 경우** | **마이그레이션** **유형** | **세부 사항** |
|---|---|---|---|
| `Cq561ProjectContentUpgrade` | &lt; 5.6.1 | 즉시 |  |
| `Cq60MSMContentUpgrade` | &lt; 6.0 | 즉시 | 모두 검색 `LiveRelationShips` 변환 전: `VersionStorage` 삭제된 항목을 선택하고 상위에 제외 속성을 추가합니다 |
| `Cq61CloudServicesContentUpgrade` | &lt; 6.1 | 즉시 | 기본 설정에 따라 cloudservices의 보안 재구성 |
| `Cq62ConfContentUpgrade` | &lt; 6.2 | 즉시 | 다음에서 링크 기반 속성 제거 **/content** to **/conf** (OSGi 메커니즘으로 대체됨)에서 해당 OSGi 구성을 생성합니다 |
| `Cq62FormsContentUpgrade` | &lt; 6.2 | 즉시 | merge_preserve를 통해 기본적으로 거부 규칙 무시로 인해 주어진 권한을 재정의하여 업그레이드 시 다시 순서를 지정해야 합니다 |
| `CQ62Html5SmartFileUpgrade` | &lt; 6.2 | 즉시 | Html5SmartFile 위젯을 활용하여 구성 요소를 검색하고, 컨텐츠에서 구성 요소의 사용을 검색하고, 지속성을 재구성하므로, 바이너리를 수준 아래로 효과적으로 이동하며 구성 요소 수준에 저장하지 않습니다. |
| `Cq62ProjectsCodeUpgrade` | &lt; 6.2 | 즉시 | 이전 스타일 프로젝트를 **/etc/projects** to **/content/projects** |
| `Cq62TargetCampaignsContentUpgrade` | &lt; 6.2 | 즉시 | 컨테이너 레이어를 계층(영역)으로 소개하고 참조를 조정합니다. |
| `Cq62TargetContentUpgrade` | &lt; 6.2 | 즉시 | 고정 위치 이름을 타겟 구성 요소로 설정합니다. |
| `Cq62WorkflowContentUpgrade` | &lt; 6.2 | 즉시 | 6.2 구조, 인스턴스, 알림을 미리 작성한 다음 백업 위치에서 다시 병합하는 워크플로우 모델의 복잡한 변환 **/var/backup** |
| `CQ63AssetsMetadataFormsUpdate` | &lt; 6.3 | 즉시 | 자산, 사용자 지정 메타데이터 스키마 및 처리 프로필을 **/apps** to **/conf** 및 는 메타데이터 스키마 및 메타데이터 프로필 양식을 coral2에서 coral3로 변환합니다. |
| `CQ63AssetsSearchFacetsUpdate` | &lt; 6.3 | 즉시 | 자산 및 사용자 지정 검색 패싯을 **/apps** to **/conf** 및 는 메타데이터 스키마 및 메타데이터 프로필 양식을 coral2에서 coral3로 변환합니다. |
| `CQ63InboxItemsUpgrade` | &lt; 6.3 | 즉시 | 받은 편지함 항목 순서를 위한 항목 업데이트(효율적인 정렬을 위해 메타데이터 조정) |
| `CQ63MetadataSchemaConfigUpdate` | &lt; 6.3 | 즉시 | 상대 경로를 **/conf** 대신 **/apps** |
| `CQ63MobileAppsNavUpgrade` | &lt; 6.3 | 즉시 | 탐색 구조 조정 |
| `CQ63MonitoringDashboardsConfigUpdate` | &lt; 6.3 | 즉시 | 모니터링 대시보드에 대한 사용자 지정 구성을 **/libs** 및 **/apps** |
| `CQ63ProcessingProfileConfigUpdate` | &lt; 6.3 | 즉시 | 6.3 이상 구조와 일치하도록 Assets에서 processingProfile 속성(6.1까지 사용)을 변환합니다. 또한 프로필의 상대 경로를 **/conf** 대신 **/apps**. |
| `CQ63ToolsMenuEntriesContentUpgrade` | &lt; 6.3 | 즉시 | 업그레이드 시 오래된 CRXDE Lite 및 웹 콘솔 메뉴 항목을 제거하는 업그레이드 작업입니다. |
| `CQ64CommunitiesConfigsCleanupTask` | &lt; 6.3 | 지연 | SRP 클라우드 구성 이동, 커뮤니티 Watchwords 구성, 정리 **/etc/social** 및 **/etc/enablement** (레이지 마이그레이션을 실행할 때 모든 참조 및 데이터를 조정해야 합니다. 이 구조에 따라 애플리케이션 부분이 더 이상 없어야 합니다.) |
| `CQ64LegacyCloudSettingsCleanupTask` | &lt; 6.4 | 지연 | 정리 **/etc/cloudsettings** (ContextHub 구성 포함). 구성은 첫 번째 액세스 시 자동으로 마이그레이션됩니다. 레이지 컨텐츠 마이그레이션이 의 이 컨텐츠 업그레이드와 함께 시작되는 경우 **/etc/cloudsettings** 패키지 업그레이드 전에 패키지를 통해 유지한 다음 다시 설치해야 암시적 변환이 시작될 수 있으며 완료 후 패키지를 다시 제거할 수 있습니다. |
| `CQ64UsersTitleFixTask` | &lt; 6.4 | 지연 | 사용자 프로필 노드에서 제목에 대한 이전 제목 구조를 조정합니다. |
| `CQ64CommerceMigrationTask` | &lt; 6.4 | 지연 | 전자 상거래 콘텐츠 마이그레이션 위치 **/etc/commerce** to **/var/commerce**. 마이그레이션 중에 컨텐츠가 이동되고 이동된 컨텐츠에 대한 참조가 새 위치를 반영하도록 업데이트됩니다. |
| `CQ65DMMigrationTask` | &lt; 6.5 | 지연 | 레거시 카탈로그 설정 및 Dynamic Media Cloud Services 설정을 다음 위치에서 마이그레이션 **/etc** to **/conf** |
| `CQ65LegacyClientlibsCleanupTask` | &lt; 6.5 | 지연 | 아래에 있는 기존 clientlibs 정리 **/etc/clientlibs** |
