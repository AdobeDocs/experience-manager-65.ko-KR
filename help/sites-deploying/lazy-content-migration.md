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
solution: Experience Manager, Experience Manager Sites
role: Admin
source-git-commit: 48d12388d4707e61117116ca7eb533cea8c7ef34
workflow-type: tm+mt
source-wordcount: '693'
ht-degree: 2%

---

# 소극적 컨텐츠 마이그레이션 {#lazy-content-migration}

이전 버전과의 호환성을 위해 Adobe Experience Manager(AEM) 6.3으로 시작하는 **/etc** 및 **/content**&#x200B;의 콘텐츠 및 구성은 업그레이드 즉시 터치하거나 변형되지 않습니다. 이는 이러한 구조에 대한 고객 애플리케이션의 종속성이 그대로 유지되도록 하기 위한 것입니다. 기본 제공 AEM 6.5의 컨텐츠가 다른 위치에서 호스팅되더라도 이러한 컨텐츠 구조와 관련된 기능은 여전히 동일합니다.

이러한 모든 위치가 자동으로 변환되지는 않지만 지연 콘텐츠 마이그레이션이라고도 하는 몇 가지 지연된 `CodeUpgradeTasks`이(가) 있습니다. 이렇게 하면 고객이 이 시스템 속성으로 인스턴스를 다시 시작하여 이러한 자동 변환을 트리거할 수 있습니다.

```shell
-Dcom.adobe.upgrade.forcemigration=true
```

이렇게 하면 마이그레이션하는 동안 `CodeUpgradeTasks`이(가) 실행됩니다.

이 업그레이드 프로세스는 효율적인 실행이 목적이지만 동기적으로 수행되기 때문에 처리해야 하는 컨텐츠의 양에 따라 다운타임이 발생합니다. Adobe은 프로덕션 시스템 이전의 스테이징 환경에서 실행 시간을 평가하여 유지 관리 기간에 따라 계획을 수립하는 것을 권장합니다.

이 작업에는 일반적으로 응용 프로그램 조정이 필요하므로 이 작업은 해당 응용 프로그램 배포와 함께 수행해야 합니다.

다음은 6.5에 도입된 `CodeUpgradeTasks`의 전체 목록입니다.

| **이름** | **관련** **이전 AEM 버전** | **마이그레이션** **유형** | **세부 정보** |
|---|---|---|---|
| `Cq561ProjectContentUpgrade` | &lt; 5.6.1 | 즉시 |  |
| `Cq60MSMContentUpgrade` | &lt; 6.0 | 즉시 | `VersionStorage`에서 삭제된 모든 `LiveRelationShips`을(를) 감지하고 부모에 제외 속성을 추가합니다. |
| `Cq61CloudServicesContentUpgrade` | &lt; 6.1 | 즉시 | 기본적으로 보안을 위해 cloudservices 재구성 |
| `Cq62ConfContentUpgrade` | &lt; 6.2 | 즉시 | **/content**&#x200B;에서 **/conf**(OSGi 메커니즘으로 대체됨)으로의 링크 기반의 속성을 제거하고 해당 OSGi 구성을 생성합니다. |
| `Cq62FormsContentUpgrade` | &lt; 6.2 | 즉시 | merge_preserve 처리로 인해 기본적으로 보안 거부 규칙은 지정된 권한을 무시하므로 업그레이드 시 순서를 변경해야 합니다 |
| `CQ62Html5SmartFileUpgrade` | &lt; 6.2 | 즉시 | Html5SmartFile 위젯을 사용하여 구성 요소를 감지하고 컨텐츠에서 구성 요소 사용을 검색하고 지속성을 재구성하여 바이너리를 한 수준 아래로 효과적으로 이동하고 구성 요소 수준에 저장하지 않습니다. |
| `Cq62ProjectsCodeUpgrade` | &lt; 6.2 | 즉시 | 이전 스타일 프로젝트를 **/etc/projects**&#x200B;에서 **/content/projects**(으)로 이동 |
| `Cq62TargetCampaignsContentUpgrade` | &lt; 6.2 | 즉시 | 컨테이너 레이어를 계층(영역)에 소개하고 참조를 조정합니다. |
| `Cq62TargetContentUpgrade` | &lt; 6.2 | 즉시 | 고정 위치 이름을 대상 구성 요소로 설정합니다. |
| `Cq62WorkflowContentUpgrade` | &lt; 6.2 | 즉시 | 6.2 구조, 인스턴스, 알림을 미리 계산한 다음 **/var/backup**&#x200B;에서 백업 위치에서 다시 병합하는 워크플로우 모델의 복잡한 변환 |
| `CQ63AssetsMetadataFormsUpdate` | &lt; 6.3 | 즉시 | 자산, 사용자 지정 메타데이터 스키마 및 처리 프로필을 **/apps**&#x200B;에서 **/conf**(으)로 이동하고 메타데이터 스키마 및 메타데이터 프로필 양식을 coral2에서 coral3로 변환합니다. |
| `CQ63AssetsSearchFacetsUpdate` | &lt; 6.3 | 즉시 | 자산 및 사용자 지정 검색 패싯을 **/apps**&#x200B;에서 **/conf**(으)로 이동하고 메타데이터 스키마 및 메타데이터 프로필 양식을 coral2에서 coral3로 변환합니다. |
| `CQ63InboxItemsUpgrade` | &lt; 6.3 | 즉시 | 받은 편지함 항목 정렬을 위한 InboxItems 업데이트(효율적인 정렬을 위해 메타데이터 조정) |
| `CQ63MetadataSchemaConfigUpdate` | &lt; 6.3 | 즉시 | 상대 경로를 **/apps** 대신 **/conf**(으)로 바꾸어 폴더의 metadataSchema 속성을 조정합니다. |
| `CQ63MobileAppsNavUpgrade` | &lt; 6.3 | 즉시 | 탐색 구조 조정 |
| `CQ63MonitoringDashboardsConfigUpdate` | &lt; 6.3 | 즉시 | 모니터링 대시보드에 대한 사용자 지정 구성을 **/libs** 및 **/apps**&#x200B;에서 이동합니다. |
| `CQ63ProcessingProfileConfigUpdate` | &lt; 6.3 | 즉시 | Assets의 processingProfile 속성(6.1까지 사용)을 6.3 이상 구조와 일치하도록 변환합니다. 또한 프로필의 상대 경로를 **/apps** 대신 **/conf**(으)로 조정합니다. |
| `CQ63ToolsMenuEntriesContentUpgrade` | &lt; 6.3 | 즉시 | 업그레이드가 있는 경우 오래된 CRXDE Lite 및 웹 콘솔 메뉴 항목을 제거하는 업그레이드 작업입니다. |
| `CQ64CommunitiesConfigsCleanupTask` | &lt; 6.3 | 지연됨 | SRP 클라우드 구성, 커뮤니티 watchwords 구성을 이동하고 **/etc/social** 및 **/etc/enablement**&#x200B;을(를) 정리합니다. 레이지 마이그레이션이 실행될 때 모든 참조 및 데이터를 조정해야 하며 더 이상 이 구조에 따라 응용 프로그램 부분이 달라지지 않아야 합니다. |
| `CQ64LegacyCloudSettingsCleanupTask` | &lt; 6.4 | 지연됨 | **/etc/cloudsettings**&#x200B;을(를) 정리합니다(ContextHub 구성 포함). 구성은 첫 번째 액세스 시 자동으로 마이그레이션됩니다. **/etc/cloudsettings**&#x200B;의 이 콘텐츠 업그레이드와 함께 레이지 콘텐츠 마이그레이션이 시작되는 경우 업그레이드 전에 패키지를 통해 보존하고 암시적 변환이 시작되도록 다시 설치하여 완료 후 패키지를 제거해야 합니다. |
| `CQ64UsersTitleFixTask` | &lt; 6.4 | 지연됨 | 기존 제목 구조를 사용자 프로필 노드의 제목으로 조정합니다. |
| `CQ64CommerceMigrationTask` | &lt; 6.4 | 지연됨 | 상거래 콘텐츠를 **/etc/commerce**&#x200B;에서 **/var/commerce**(으)로 마이그레이션합니다. 마이그레이션 중에 콘텐츠가 이동되고 이동된 콘텐츠에 대한 참조가 새 위치를 반영하도록 업데이트됩니다. |
| `CQ65DMMigrationTask` | &lt; 6.5 | 지연됨 | 레거시 카탈로그 설정 및 Dynamic Media Cloud Service 설정을 **/etc**&#x200B;에서 **/conf**(으)로 마이그레이션 |
| `CQ65LegacyClientlibsCleanupTask` | &lt; 6.5 | 지연됨 | **/etc/clientlibs**&#x200B;에 있는 레거시 clientlibs를 정리합니다. |
