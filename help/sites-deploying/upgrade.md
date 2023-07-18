---
title: Adobe Experience Manager 6.5로 업그레이드
description: 이전 AEM(Adobe Experience Manager) 설치를 AEM 6.5로 업그레이드하는 기본 사항에 대해 알아봅니다.
contentOwner: sarchiz
topic-tags: upgrading
content-type: reference
docset: aem65
targetaudience: target-audience upgrader
feature: Upgrading
exl-id: 722d544c-c342-4c1c-80e5-d0a1244f4d36
source-git-commit: 26c0411d6cc16f4361cfa9e6b563eba0bfafab1e
workflow-type: tm+mt
source-wordcount: '678'
ht-degree: 0%

---

# Adobe Experience Manager(AEM) 6.5로 업그레이드 {#upgrading-to-aem}

이 섹션에서는 AEM 설치를 AEM 6.5로 업그레이드하는 방법에 대해 설명합니다.

* [업그레이드 계획](/help/sites-deploying/upgrade-planning.md)
* [패턴 감지기를 사용한 업그레이드 복잡성 평가](/help/sites-deploying/pattern-detector.md)
* [AEM 6.5의 이전 버전과의 호환성](/help/sites-deploying/backward-compatibility.md)
  <!--* [Using Offline Reindexing To Reduce Downtime During an Upgrade](/help/sites-deploying/upgrade-offline-reindexing.md)-->
* [업그레이드 프로시저](/help/sites-deploying/upgrade-procedure.md)
* [코드 및 사용자 지정 업그레이드](/help/sites-deploying/upgrading-code-and-customizations.md)
* [업그레이드 전 유지 관리 작업](/help/sites-deploying/pre-upgrade-maintenance-tasks.md)
* [즉석 업그레이드 수행](/help/sites-deploying/in-place-upgrade.md)
* [업그레이드 후 확인 및 문제 해결](/help/sites-deploying/post-upgrade-checks-and-troubleshooting.md)
* [지속 가능한 업그레이드](/help/sites-deploying/sustainable-upgrades.md)
* [소극적 컨텐츠 마이그레이션](/help/sites-deploying/lazy-content-migration.md)
* [AEM 6.5의 저장소 재구성](/help/sites-deploying/repository-restructuring.md)

이러한 절차에 포함된 AEM 인스턴스를 더 쉽게 참조할 수 있도록 이 문서 전체에서 다음 용어가 사용됩니다.

* 다음 *소스* 인스턴스는 업그레이드 중인 AEM 인스턴스입니다.
* 다음 *target* 인스턴스는 업그레이드하려는 인스턴스입니다.

>[!NOTE]
>
>AEM은 업그레이드의 안정성을 개선하기 위한 노력의 일환으로 포괄적인 저장소 구조 조정을 거쳤습니다. 새 구조에 맞게 조정하는 방법에 대한 자세한 내용은 [AEM의 저장소 재구성.](/help/sites-deploying/repository-restructuring.md)

## 변경 사항 {#what-has-changed}

다음은 AEM의 지난 몇 가지 릴리스에 대한 주요 변경 사항입니다.

AEM 6.0에는 새로운 Jackrabbit Oak 저장소가 도입되었습니다. 지속성 관리자가에 의해 대체되었습니다. [마이크로 커널](/help/sites-deploying/platform.md#contentbody_title_4). 버전 6.1부터 CRX2는 더 이상 지원되지 않습니다. 5.6.1 인스턴스에서 CRX2 저장소를 마이그레이션하려면 crx2oak라는 마이그레이션 도구를 실행해야 합니다. 자세한 내용은 [CRX2OAK 마이그레이션 도구 사용](/help/sites-deploying/using-crx2oak.md).

Assets Insights를 사용 중이고 AEM 6.2 이전 버전에서 업그레이드하는 경우 에셋을 마이그레이션하고 JMX 빈을 통해 ID를 생성해야 합니다. Adobe의 내부 테스트의 경우 TarMK 환경의 125K 자산이 한 시간 만에 마이그레이션되었지만 결과는 다를 수 있습니다.

6.3에서 `SegmentNodeStore`: TarMK 구현의 기초입니다. AEM 6.3 이전 버전에서 업그레이드하는 경우 업그레이드의 일부로 시스템 다운타임과 관련된 저장소 마이그레이션이 필요합니다.

Adobe 엔지니어링에서는 약 20분이 소요될 것으로 예상하고 있습니다. 리인덱싱할 필요는 없습니다. 또한 새 저장소 형식을 사용할 수 있는 crx2oak 도구의 새 버전이 출시되었습니다.

**AEM 6.3에서 AEM 6.5로 업그레이드하는 경우 이 마이그레이션이 필요하지 않습니다.**

업그레이드 전 유지 관리 작업이 자동화를 지원하도록 최적화되었습니다.

crx2oak 도구 명령줄 사용 옵션이 자동화에 적합하고 추가 업그레이드 경로를 지원하도록 변경되었습니다.

업그레이드 후 검사를 자동화할 수도 있습니다.

수정 버전의 주기적 가비지 수집 및 데이터 저장소 가비지 수집은 이제 정기적으로 수행해야 하는 일상적인 유지 관리 작업입니다. AEM 6.3이 도입됨에 따라 Adobe은 온라인 수정 버전 정리를 지원하고 권장합니다. 다음을 참조하십시오 [개정 정리](/help/sites-deploying/revision-cleanup.md) 를 참조하십시오.

AEM은 최근에 다음을 도입했습니다. [패턴 탐지기](/help/sites-deploying/pattern-detector.md) 업그레이드 계획을 시작할 때 업그레이드의 복잡성을 평가합니다. 6.5는 또한 [이전 버전과의 호환성](/help/sites-deploying/backward-compatibility.md) 기능. 마지막으로, 의 모범 사례 [지속 가능한 업그레이드](/help/sites-deploying/sustainable-upgrades.md) 도 추가됩니다.

최신 AEM 버전에서 변경된 사항에 대한 자세한 내용은 전체 릴리스 노트를 참조하십시오.

* [Adobe Experience Manager 6.5 최신 서비스 팩 릴리스 노트](/help/release-notes/release-notes.md)

## 업그레이드 개요 {#upgrade-overview}

AEM 업그레이드는 여러 단계로 진행되며 경우에 따라 여러 달이 지나기도 합니다. 업그레이드 프로젝트에 포함된 내용과 이 설명서에 포함된 내용에 대한 개요는 다음과 같습니다.

![screen_shot_2018-03-30at80708am](assets/screen_shot_2018-03-30at80708am.png)

## 업그레이드 흐름 {#upgrade-overview-1}

아래 다이어그램은 전반적인 권장 흐름을 캡처하여 업그레이드 접근 방식을 강조합니다. Adobe이 도입한 새 기능에 대한 참조를 확인합니다. 업그레이드는 패턴 감지기로 시작해야 합니다( 참조) [패턴 감지기를 사용한 업그레이드 복잡성 평가](/help/sites-deploying/pattern-detector.md)) 생성된 보고서의 패턴을 기반으로 AEM 6.4와의 호환성을 위해 사용할 경로를 결정할 수 있습니다.

6.5에는 모든 새 기능을 이전 버전과 호환되도록 유지하는 데 중요한 초점이 맞춰져 있었지만, 일부 이전 버전과의 호환성 문제가 여전히 발생하는 경우 호환성 모드를 사용하면 사용자 지정 코드가 6.5를 준수하도록 개발을 일시적으로 연기할 수 있습니다. 이 접근 방식은 업그레이드 직후 개발 노력을 피하는 데 도움이 됩니다( 참조) [AEM 6.5의 이전 버전과의 호환성](/help/sites-deploying/backward-compatibility.md)).

마지막으로, 6.5 개발 사이클에서 지속 가능한 업그레이드에 도입된 기능(참조) [지속 가능한 업그레이드](/help/sites-deploying/sustainable-upgrades.md))를 사용하면 모범 사례를 따라 향후 업그레이드를 보다 효율적이고 원활하게 수행할 수 있습니다.

![6_4_upgrade_overviewflowchart-newpage3](assets/6_4_upgrade_overviewflowchart-newpage3.png)
