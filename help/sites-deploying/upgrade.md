---
title: AEM 6.5로 업그레이드
seo-title: AEM 6.5로 업그레이드
description: 이전 AEM 설치를 AEM 6.5로 업그레이드하는 기본 방법에 대해 알아봅니다.
seo-description: 이전 AEM 설치를 AEM 6.5로 업그레이드하는 기본 방법에 대해 알아봅니다.
uuid: 45368056-273c-4f1a-9da6-e7ba5c2bbc0d
contentOwner: sarchiz
topic-tags: upgrading
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
discoiquuid: ebd99cc4-8762-4c28-a177-d62dac276afe
docset: aem65
targetaudience: target-audience upgrader
feature: Upgrading
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '721'
ht-degree: 4%

---


# AEM 6.5로 업그레이드 {#upgrading-to-aem}

이 섹션에서는 AEM 6.5로 AEM 설치 업그레이드를 다룹니다.

* [업그레이드 계획](/help/sites-deploying/upgrade-planning.md)
* [Pattern Detector를 사용한 업그레이드 복잡성 평가](/help/sites-deploying/pattern-detector.md)
* [AEM 6.5의 이전 버전과의 호환성](/help/sites-deploying/backward-compatibility.md)

<!--* [Using Offline Reindexing To Reduce Downtime During an Upgrade](/help/sites-deploying/upgrade-offline-reindexing.md)-->
* [업그레이드 절차](/help/sites-deploying/upgrade-procedure.md)
* [코드 및 사용자 정의 업그레이드](/help/sites-deploying/upgrading-code-and-customizations.md)
* [업그레이드 전 유지 관리 작업](/help/sites-deploying/pre-upgrade-maintenance-tasks.md)
* [즉석 업그레이드 수행](/help/sites-deploying/in-place-upgrade.md)
* [업그레이드 확인 후 및 문제 해결](/help/sites-deploying/post-upgrade-checks-and-troubleshooting.md)
* [지속적인 업그레이드](/help/sites-deploying/sustainable-upgrades.md)
* [지연 컨텐츠 마이그레이션](/help/sites-deploying/lazy-content-migration.md)
* [AEM 6.5의 저장소 재구성](/help/sites-deploying/repository-restructuring.md)

이러한 절차와 관련된 AEM 인스턴스를 쉽게 참조하기 위해 다음 용어가 이 문서 전체에서 사용됩니다.

* *source* 인스턴스는 업그레이드하려는 AEM 인스턴스입니다.
* *target* 인스턴스는 업그레이드하려는 인스턴스입니다.

>[!NOTE]
>
>업그레이드 신뢰도를 향상시키기 위한 노력의 일환으로 AEM은 포괄적인 저장소 재구성을 겪었습니다. 새 구조에 정렬하는 방법에 대한 자세한 내용은 [AEM의 리포지토리 구조화를 참조하십시오.](/help/sites-deploying/repository-restructuring.md)

## 무엇이 변경되었습니까?{#what-has-changed}

다음은 AEM의 최근 여러 릴리스에서 메모의 주요 변경 사항입니다.

AEM 6.0은 새로운 Jackrabbit Oak 저장소를 도입했습니다. 지속성 관리자가 [Micro Kernels](/help/sites-deploying/platform.md#contentbody_title_4)로 대체되었습니다. 버전 6.1부터 CRX2는 더 이상 지원되지 않습니다. 5.6.1 인스턴스에서 CRX2 저장소를 마이그레이션하려면 crx2oak라는 마이그레이션 도구를 실행해야 합니다. 자세한 내용은 [CRX2OAK 마이그레이션 도구 사용](/help/sites-deploying/using-crx2oak.md)을 참조하십시오.

자산 통찰력을 사용하고 AEM 6.2 이전 버전에서 업그레이드하는 경우, 자산을 마이그레이션해야 하며 JMX Bean을 통해 ID를 만들어야 합니다. 내부 테스트에서 TarMK 환경의 125K 에셋이 1시간 내에 마이그레이션되었지만 결과가 달라질 수 있습니다.

6.3에서는 TarMK 구현의 기초가 되는 `SegmentNodeStore`의 새로운 형식을 도입했습니다. AEM 6.3 이전 버전에서 업그레이드하는 경우 시스템 다운타임을 포함하여 업그레이드의 일부로 저장소 마이그레이션이 필요합니다.

Adobe 공대는 이것이 약 20분 정도 될 것으로 예상하고 있습니다. 다시 색인화할 필요는 없습니다. 또한 새로운 저장소 형식과 연동되도록 crx2oak 도구의 새 버전이 릴리스되었습니다.

**AEM 6.3에서 AEM 6.5로 업그레이드하는 경우 이 마이그레이션이 필요하지 않습니다.**

업그레이드 전 유지 관리 작업은 자동화를 지원하도록 최적화되었습니다.

crx2oak 도구 명령줄 사용 옵션이 자동화 옵션이 되었고 더 많은 업그레이드 경로를 지원하도록 변경되었습니다.

또한 업그레이드 후 확인 작업을 자동화할 수 있습니다.

이제 주기적으로 수정본을 수집하거나 데이터를 저장하는 가비지 수집은 정기적으로 수행되어야 하는 반복적인 유지 관리 작업입니다. AEM 6.3이 소개되면서 Adobe은 온라인 개정 정리를 지원하고 권장합니다. 이러한 작업을 구성하는 방법에 대한 자세한 내용은 [개정 정리](/help/sites-deploying/revision-cleanup.md)를 참조하십시오.

AEM은 업그레이드 계획을 시작할 때 업그레이드의 복잡성을 평가하기 위해 [Pattern Detector](/help/sites-deploying/pattern-detector.md)를 최근 도입했습니다. 6.5는 기능 [이전 버전과의 호환성](/help/sites-deploying/backward-compatibility.md)에도 중점을 둡니다. 마지막으로 [지속 가능한 업그레이드](/help/sites-deploying/sustainable-upgrades.md)에 대한 우수 사례가 추가됩니다.

최신 AEM 버전에서 변경된 내용에 대한 자세한 내용은 전체 릴리스 정보를 참조하십시오.

* [https://helpx.adobe.com/kr/experience-manager/6-2/release-notes.html](https://helpx.adobe.com/kr/experience-manager/6-2/release-notes.html)
* [https://helpx.adobe.com/kr/experience-manager/6-3/release-notes.html](https://helpx.adobe.com/kr/experience-manager/6-3/release-notes.html)
* [https://helpx.adobe.com/kr/experience-manager/6-4/release-notes.html](https://helpx.adobe.com/kr/experience-manager/6-4/release-notes.html)
* [https://helpx.adobe.com/kr/experience-manager/6-5/release-notes.html](https://helpx.adobe.com/kr/experience-manager/6-5/release-notes.html)

## 업그레이드 개요 {#upgrade-overview}

AEM 업그레이드는 여러 단계로 여러 달에 걸쳐 진행되는 프로세스입니다. 다음 개요는 업그레이드 프로젝트에 포함된 내용과 이 설명서에 포함된 컨텐츠의 개요로 제공됩니다.

![screen_shot_2018-03-30at80708am](assets/screen_shot_2018-03-30at80708am.png)

## 업그레이드 흐름 {#upgrade-overview-1}

아래 다이어그램에는 업그레이드 방법을 강조 표시하는 전체 권장 흐름이 나와 있습니다. Adobe에서 도입한 새로운 기능에 대한 참조를 확인하십시오. 업그레이드는 생성된 보고서의 패턴을 기반으로 AEM 6.4와의 호환성을 위해 사용할 경로를 결정할 수 있는 패턴 탐지기([Pattern Detector](/help/sites-deploying/pattern-detector.md) 참조)로 시작해야 합니다.

6.5에서는 모든 새로운 기능을 이전 버전과 호환되도록 하는 데 중점을 두었지만, 이전 버전과의 호환성 문제가 여전히 남아 있는 경우, 호환성 모드를 사용하면 사용자 지정 코드를 6.5와 준수하도록 개발을 일시적으로 중단할 수 있습니다. 이 방법을 사용하면 업그레이드 후 바로 개발 작업을 방지할 수 있습니다(AEM 6.5](/help/sites-deploying/backward-compatibility.md)의 [이전 호환성 참조).

마지막으로 6.5 개발 주기 동안 지속적인 업그레이드에 도입된 기능([지속 가능한 업그레이드](/help/sites-deploying/sustainable-upgrades.md) 참조)을 사용하면 향후 업그레이드를 보다 효율적이고 매끄럽게 수행할 수 있도록 모범 사례를 준수할 수 있습니다.

![6_4_upgrade_overviewflowflowchart-newpage3](assets/6_4_upgrade_overviewflowchart-newpage3.png)

