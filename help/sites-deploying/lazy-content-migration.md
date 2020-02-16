---
title: 레이지 컨텐츠 마이그레이션
seo-title: 레이지 컨텐츠 마이그레이션
description: AEM 6.4의 레이지 컨텐츠 마이그레이션에 대해 알아봅니다.
seo-description: AEM 6.4의 레이지 컨텐츠 마이그레이션에 대해 알아봅니다.
uuid: f5b0aa84-5638-4708-9da2-89964d394632
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: upgrading
discoiquuid: d72b8844-d782-4b5b-8999-338217dbefb9
docset: aem65
translation-type: tm+mt
source-git-commit: 7d93df515bf98f0a947428b8093e059d63b21a34

---


# 레이지 컨텐츠 마이그레이션 {#lazy-content-migration}

이전 버전과의 호환성을 위해, AEM 6.3부터 시작하는 **컨텐츠** 및/등의 **구성 및 컨텐츠는** 업그레이드 시 즉시 제작되거나 변형되지 않습니다. 이러한 작업은 해당 구조에 대한 고객 애플리케이션의 종속성이 그대로 유지되도록 하기 위해 수행됩니다. AEM 6.5의 외부 컨텐츠가 다른 곳에서 호스팅되더라도 이러한 컨텐츠 구조와 관련된 기능은 여전히 동일합니다.

이러한 모든 위치가 자동으로 변환되지는 않지만, 지연 컨텐츠 마이그레이션이라고도 `CodeUpgradeTasks` 하는 몇 가지 지연이 있습니다. 이 시스템 속성을 사용하여 인스턴스를 다시 시작하여 이러한 자동 변형을 트리거할 수 있습니다.

```shell
-Dcom.adobe.upgrade.forcemigration=true
```

이로 인해 마이그레이션 중에 `CodeUpgradeTasks` 해당 항목이 실행됩니다.

목표는 효율적인 실행이지만, 이 업그레이드 프로세스는 동기식으로 진행되므로 처리해야 하는 컨텐츠의 양에 따라 다운타임이 발생합니다. 유지 관리 기간에 따라 계획을 수립하려면 프로덕션 시스템 앞의 스테이지 환경에서 실행 시간을 평가하는 것이 좋습니다.

일반적으로 응용 프로그램을 조정해야 하므로 이 작업은 해당 응용 프로그램 배포와 함께 수행해야 합니다.

다음은 6.5에서 `CodeUpgradeTasks` 소개된 전체 목록입니다.

| **이름** | **이전** AEM **버전에 대한 관련** | **마이그레이션** 유형 **** | **세부 사항** |
|---|---|---|---|
| `Cq561ProjectContentUpgrade` | &lt; 5.6.1 | 즉시 |  |
| `Cq60MSMContentUpgrade` | &lt; 6.0 | 즉시 | 삭제된 모든 `LiveRelationShips` 항목에서 `VersionStorage` 감지하고 제외 속성을 부모에 추가합니다. |
| `Cq61CloudServicesContentUpgrade` | &lt; 6.1 | 즉시 | 기본 설정을 통해 보안을 위해 클라우드 서비스 재구성 |
| `Cq62ConfContentUpgrade` | &lt; 6.2 | 즉시 | /content **/content** 에서 **/conf** (OSGi 메커니즘으로 대체됨)에 대한 링크 속성을 제거하고 해당 OSGi 구성을 생성합니다. |
| `Cq62FormsContentUpgrade` | &lt; 6.2 | 즉시 | 기본적으로 거부 규칙을 통해 보안을 처리하는 merge_preserve로 인해 업그레이드 시 순서를 다시 지정해야 하는 주어진 권한이 무시됩니다. |
| `CQ62Html5SmartFileUpgrade` | &lt; 6.2 | 즉시 | Html5SmartFile 위젯을 사용하여 구성 요소를 검색하고, 컨텐츠에서 구성 요소의 사용을 검색하고, 지속성을 재구성하여 바이너리를 수준 아래로 효과적으로 이동하고, 구성 요소 수준에 저장하지 않습니다. |
| `Cq62ProjectsCodeUpgrade` | &lt; 6.2 | 즉시 | 이전 스타일 프로젝트를 **/etc/projects** 에서 **/content/projects로 이동** |
| `Cq62TargetCampaignsContentUpgrade` | &lt; 6.2 | 즉시 | 컨테이너 레이어를 계층 구조(영역)에 도입하고 참조를 조정합니다. |
| `Cq62TargetContentUpgrade` | &lt; 6.2 | 즉시 | 고정 위치 이름을 대상 구성 요소로 설정합니다. |
| `Cq62WorkflowContentUpgrade` | &lt; 6.2 | 즉시 | 워크플로우 모델의 복잡한 변환은 6.2 구조, 인스턴스, 알림을 미리 본 다음 백업 위치에서 **/var/backup으로 다시 병합합니다.** |
| `CQ63AssetsMetadataFormsUpdate` | &lt; 6.3 | 즉시 | 자산, 사용자 정의 메타데이터 스키마 및 처리 프로필을 **/앱에서** **/conf** 로 이동하고 메타데이터 스키마 및 메타데이터 프로필 양식을 coral2에서 coral3로 변환합니다. |
| `CQ63AssetsSearchFacetsUpdate` | &lt; 6.3 | 즉시 | 자산 및 사용자 정의 검색 패싯을 **/apps** 에서 **/conf로** 이동하고 메타데이터 스키마 및 메타데이터 프로필 양식을 coral2에서 coral3로 변환합니다. |
| `CQ63InboxItemsUpgrade` | &lt; 6.3 | 즉시 | 받은 편지함 항목 업데이트(효율적인 정렬을 위해 메타데이터 조정) |
| `CQ63MetadataSchemaConfigUpdate` | &lt; 6.3 | 즉시 | /apps 대신 상대 경로를 **/conf** 로 대체하여 폴더의 metadataSchema 속성을 **조정합니다** |
| `CQ63MobileAppsNavUpgrade` | &lt; 6.3 | 즉시 | 탐색 구조 조정 |
| `CQ63MonitoringDashboardsConfigUpdate` | &lt; 6.3 | 즉시 | 모니터링 대시보드에 대한 사용자 지정 구성을 **/libs** 및 **/앱에서 이동합니다.** |
| `CQ63ProcessingProfileConfigUpdate` | &lt; 6.3 | 즉시 | 6.3 이상 구조와 일치하도록 자산에서 processingProfile 속성(6.1까지 사용)을 변환합니다. 또한 **/apps** 대신 프로필의 상대 경로를 **/conf**&#x200B;로 조정합니다. |
| `CQ63ToolsMenuEntriesContentUpgrade` | &lt; 6.3 | 즉시 | 업그레이드 시 오래된 CRXDE Lite 및 웹 콘솔 메뉴 항목을 제거하는 업그레이드 작업 |
| `CQ64CommunitiesConfigsCleanupTask` | &lt; 6.3 | 지연 | SRP 클라우드 구성, 커뮤니티 감시 단어 구성, 정리 **및/etc/social** 및 **/etc/enablement** (지연 마이그레이션이 실행될 때 참조 및 데이터를 조정해야 함 - 더 이상 이 구조에 따라 애플리케이션 부분이 달라서는 안 됨). |
| `CQ64LegacyCloudSettingsCleanupTask` | &lt; 6.4 | 지연 | ContextHub 구성 **포함)을 정리합니다** . 구성은 첫 번째 액세스 시 자동으로 마이그레이션됩니다. In case Lazy Content Migration with upgrade with this content in/ **/etc/cloudsettings** must be recoded with package before the upgrade, and reinstalled to kick in the implicable transformation and with the subsequently uninstall of the package after completed. |
| `CQ64UsersTitleFixTask` | &lt; 6.4 | 지연 | 사용자 프로필 노드의 제목으로 이전 제목 구조를 조정합니다. |
| `CQ64CommerceMigrationTask` | &lt; 6.4 | 지연 | 상거래 컨텐츠를 **/etc/commerce** 에서 **/var/commerce**(으)로 마이그레이션합니다. 마이그레이션 중에는 콘텐트가 이동되고 이동된 콘텐트에 대한 참조가 업데이트되어 새 위치가 반영됩니다. |
| `CQ65DMMigrationTask` | &lt; 6.5 | 지연 | 레거시 카탈로그 설정 및 다이내믹 미디어 클라우드 서비스 설정을 **/등에서** **/conf로 마이그레이션** |
| `CQ65LegacyClientlibsCleanupTask` | &lt; 6.5 | 지연 | 기존 clientlibs **/etc/clientlibs 제거** |
