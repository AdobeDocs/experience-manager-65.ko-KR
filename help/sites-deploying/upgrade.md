---
title: AEM 6.5로 업그레이드
seo-title: AEM 6.5로 업그레이드
description: 이전 AEM 설치를 AEM 6.5로 업그레이드하는 기본 사항에 대해 알아봅니다.
seo-description: 이전 AEM 설치를 AEM 6.5로 업그레이드하는 기본 사항에 대해 알아봅니다.
uuid: 45368056-273c-4f1a-9da6-e7ba5c2bbc0d
contentOwner: sarchiz
topic-tags: upgrading
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
discoiquuid: ebd99cc4-8762-4c28-a177-d62dac276afe
docset: aem65
targetaudience: target-audience upgrader
translation-type: tm+mt
source-git-commit: 5035c9630b5e861f4386e1b5ab4f4ae7a8d26149

---


# AEM 6.5로 업그레이드 {#upgrading-to-aem}

이 섹션에서는 AEM 설치를 AEM 6.5로 업그레이드하는 것을 다룹니다.

* [업그레이드 계획](/help/sites-deploying/upgrade-planning.md)
* [Pattern Detector를 사용하여 업그레이드 복잡성 평가](/help/sites-deploying/pattern-detector.md)
* [AEM 6.5의 이전 버전과의 호환성](/help/sites-deploying/backward-compatibility.md)
* [업그레이드 절차](/help/sites-deploying/upgrade-procedure.md)
* [코드 및 사용자 정의 업그레이드](/help/sites-deploying/upgrading-code-and-customizations.md)
* [업그레이드 전 유지 관리 작업](/help/sites-deploying/pre-upgrade-maintenance-tasks.md)
* [즉석 업그레이드 수행](/help/sites-deploying/in-place-upgrade.md)
* [업그레이드 후 확인 및 문제 해결](/help/sites-deploying/post-upgrade-checks-and-troubleshooting.md)
* [지속적인 업그레이드](/help/sites-deploying/sustainable-upgrades.md)
* [레이지 컨텐츠 마이그레이션](/help/sites-deploying/lazy-content-migration.md)
* [AEM 6.5의 저장소 재구성](/help/sites-deploying/repository-restructuring.md)

이러한 절차와 관련된 AEM 인스턴스를 쉽게 참조하기 위해 다음 용어가 이 문서 전체에서 사용됩니다.

* 소스 ** 인스턴스는 업그레이드할 AEM 인스턴스입니다.
* 대상 ** 인스턴스는 업그레이드할 인스턴스입니다.

>[!NOTE]
>
>업그레이드의 안정성을 개선하기 위한 노력의 일환으로 AEM은 포괄적인 저장소 재구성을 완료했습니다. 새 구조에 정렬하는 방법에 대한 자세한 내용은 AEM의 [리포지토리 재구성을 참조하십시오.](/help/sites-deploying/repository-restructuring.md)

## 무엇이 변경되었습니까? {#what-has-changed}

다음은 AEM의 최근 몇 릴리스에 대한 메모의 주요 변경 사항입니다.

AEM 6.0은 새로운 Jackrabbit Oak 저장소를 도입했습니다. 지속성 관리자가 Micro Kernels로 [바뀌었습니다](/help/sites-deploying/platform.md#contentbody_title_4). 버전 6.1부터 CRX2는 더 이상 지원되지 않습니다. CRX2oak라는 마이그레이션 도구를 실행하여 5.6.1 인스턴스에서 CRX2 저장소를 마이그레이션해야 합니다. 자세한 내용은 CRX2OAK [마이그레이션 도구 사용을 참조하십시오](/help/sites-deploying/using-crx2oak.md).

자산 통찰력을 사용하고 AEM 6.2 이전 버전에서 업그레이드하는 경우, 자산을 마이그레이션해야 하며 JMX bean을 통해 생성된 ID가 있어야 합니다. Adobe의 내부 테스트에서 TarMK 환경의 125K 에셋이 1시간 만에 마이그레이션되었지만 결과가 달라질 수 있습니다.

6.3에서는 TarMK 구현의 `SegmentNodeStore`기초가 되는 새로운 형식을 도입했습니다. AEM 6.3 이전 버전에서 업그레이드하는 경우 업그레이드의 일부로 저장소 마이그레이션이 필요하며 시스템 다운타임이 포함됩니다.

Adobe Engineering은 20분 정도 걸릴 것으로 예상하고 있습니다. 다시 색인화할 필요는 없습니다. 또한 새로운 버전의 crx2oak 툴이 새로운 저장소 포맷으로 작동되도록 출시되었습니다.

**AEM 6.3에서 AEM 6.5로 업그레이드하는 경우에는 이 마이그레이션이 필요하지 않습니다.**

업그레이드 전 유지 관리 작업은 자동화를 지원하도록 최적화되었습니다.

crx2oak 도구 명령줄 사용 옵션이 자동화 친화적이며 더 많은 업그레이드 경로를 지원하도록 변경되었습니다.

또한 업그레이드 후 확인을 통해 자동화 기능을 사용할 수 있습니다.

개정판 및 데이터 저장소 가비지 수집에 대한 주기적인 가비지 수집은 이제 주기적으로 수행해야 하는 반복적인 유지 관리 작업입니다. AEM 6.3의 도입으로 Adobe는 온라인 개정 정리를 지원하고 권장합니다. 이러한 [작업을 구성하는](/help/sites-deploying/revision-cleanup.md) 방법에 대한 자세한 내용은 개정 정리를 참조하십시오.

AEM에서는 최근 [업그레이드를](/help/sites-deploying/pattern-detector.md) 계획할 때 업그레이드의 복잡성을 평가하기 위한 패턴 탐지기 기능을 도입했습니다. 6.5는 기능 [이전 버전과의 호환성에](/help/sites-deploying/backward-compatibility.md) 중점을 두고 있습니다. 마지막으로 [지속적인 업그레이드에](/help/sites-deploying/sustainable-upgrades.md) 대한 모범 사례도 추가되었습니다.

최근 AEM 버전에서 변경된 내용에 대한 자세한 내용은 전체 릴리스 정보를 참조하십시오.

* [https://helpx.adobe.com/kr/experience-manager/6-2/release-notes.html](https://helpx.adobe.com/experience-manager/6-2/release-notes.html)
* [https://helpx.adobe.com/kr/experience-manager/6-3/release-notes.html](https://helpx.adobe.com/experience-manager/6-3/release-notes.html)
* [https://helpx.adobe.com/kr/experience-manager/6-4/release-notes.html](https://helpx.adobe.com/experience-manager/6-4/release-notes.html)
* [https://helpx.adobe.com/kr/experience-manager/6-5/release-notes.html](https://helpx.adobe.com/experience-manager/6-5/release-notes.html)

## 업그레이드 개요 {#upgrade-overview}

AEM 업그레이드는 여러 단계로, 때로 여러 달에 걸쳐 이루어집니다. 다음 개요는 업그레이드 프로젝트에 포함된 내용과 이 설명서에 포함된 컨텐츠에 대한 개요로 제공됩니다.

![screen_shot_2018-03-30at80708am](assets/screen_shot_2018-03-30at80708am.png)

## 업그레이드 흐름 {#upgrade-overview-1}

아래 다이어그램은 전체 권장 플로우를 강조 표시한 것입니다. Adobe가 도입한 새로운 기능을 참조하십시오. 업그레이드는 생성된 보고서의 패턴을 기반으로 AEM 6.4 [와의 호환성을 위해](/help/sites-deploying/pattern-detector.md)사용할 경로를 결정할 수 있도록 해주는 패턴 탐지기(패턴 탐색을 통한 업그레이드 복잡성 평가 참조)로 시작해야 합니다.

6.5에서는 모든 새로운 기능이 이전 버전과 호환되도록 하는 데 중점을 두었지만, 일부 이전 버전과의 호환성 문제가 여전히 표시되는 경우 호환성 모드를 사용하면 사용자 지정 코드를 6.5와 호환되도록 개발을 일시적으로 연기시킬 수 있습니다.이 방법은 업그레이드 직후 개발 노력을 피하는 데 도움이 됩니다(AEM [6.5의 이전 호환성 참조](/help/sites-deploying/backward-compatibility.md)).

마지막으로 6.5 개발 주기 동안 지속적인 업그레이드(지속 가능한 업그레이드 참조)에 도입된 기능을 [사용하면](/help/sites-deploying/sustainable-upgrades.md)Best Practice를 통해 향후 업그레이드를 보다 효율적이고 매끄럽게 진행할 수 있습니다.

![6_4_upgrade_overviewflowchart-newpage3](assets/6_4_upgrade_overviewflowchart-newpage3.png)

