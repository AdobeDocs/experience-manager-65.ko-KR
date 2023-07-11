---
title: JEE의 AEM 6.5 Forms으로 업그레이드
description: AEM 6.1 Forms, AEM 6.2 Forms 및 LiveCycle ES4 SP1에서 AEM 6.3 Forms으로 직접 업그레이드할 수 있습니다.
uuid: 1435246a-9215-4d88-b52c-59a5c329bb77
content-type: reference
products: SG_EXPERIENCEMANAGER/6.3/FORMS
topic-tags: installing
geptopics: SG_AEMFORMS/categories/jee
discoiquuid: e745033f-8015-4fae-9d82-99d35802c0a6
role: Admin
exl-id: 722e75a0-bcb3-465e-bb74-ea94a3b99fd3
source-git-commit: e9f64722ba7df0a7f43aaf1005161483e04142f5
workflow-type: tm+mt
source-wordcount: '382'
ht-degree: 1%

---

# JEE의 AEM 6.5 Forms으로 업그레이드 {#upgrade-to-aem-forms-jee}

AEM 6.5.12.0 Forms on JEE는 전체 설치 프로그램과 패치 설치 프로그램의 두 가지 설치 프로그램을 제공합니다.

**전체 설치 관리자**: 다음을 사용할 수 있습니다 [JEE 전체 설치 프로그램의 AEM 6.5.12.0](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html) 새로운 AEM Forms 인스턴스를 설정하거나 JEE의 AEM 6.3 Forms, JEE의 AEM 6.4 및 JEE의 AEM 6.5.x.x Forms에서 JEE의 AEM 6.5.12.0 Forms으로 바로 업그레이드 수행.

**패치 설치 관리자**: [JEE 패치 설치 프로그램의 AEM 6.5.12.0](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html) 는 이미 AEM 6.5.x.x 버전을 사용 중인 고객을 위한 것입니다. 패치 설치 관리자를 사용하여 최신 버전의 AEM Forms으로 업그레이드할 수 있습니다.

다음 표에서는 전체 및 패치 설치 관리자를 사용하기 위한 시나리오를 보여 줍니다.

![전체 및 패치 설치 프로그램 시나리오](assets/full-and-patch-installer.png)

전체 설치 관리자를 사용하여 기존 JEE의 AEM 6.3 Forms 또는 JEE의 AEM 6.4 Forms을 JEE의 AEM 6.5.12.0 Forms으로 업그레이드하려면 다음 절차를 수행하십시오.

1. 에서 AEM 6.5 Forms on JEE 설치 프로그램을 다운로드합니다. [소프트웨어 배포](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html). 설치 관리자를 사용하려면 유효한 유지 관리 및 지원 계약이 필요합니다.
1. 다음을 참조하십시오 [업그레이드 체크리스트 및 계획](https://www.adobe.com/go/learn_aemforms_upgrade_checklist_65) 성공적인 업그레이드를 위해 수행할 검사에 대해 알아봅니다.
1. 다음을 참조하십시오 [AEM Forms으로 업그레이드 준비](https://www.adobe.com/go/learn_aemforms_prepareupgrade_65) 최소한의 서버 다운타임으로 업그레이드가 올바르게 실행되도록 하는 작업을 배우고 수행합니다.
1. 기존 환경 및 애플리케이션 서버에 따라 다음 문서 중 하나를 선택하고 지침을 따릅니다.

   * [AEM 6.3 또는 AEM 6.4 Forms에서 JBoss용 AEM 6.5 Forms으로 업그레이드](https://www.adobe.com/go/learn_aemforms_upgradeJBoss_65)
   * [AEM 6.3 또는 AEM 6.4 Forms에서 WebSphere용 AEM 6.5 Forms으로 업그레이드](https://www.adobe.com/go/learn_aemforms_upgradeWebSphere_65)
   * [AEM 6.3 또는 AEM 6.4 Forms에서 AEM 6.5 Forms for JBoss 턴키로 업그레이드](https://www.adobe.com/go/learn_aemforms_upgradeTurnkey_65)

LiveCycle ES2, LiveCycle ES3, AEM 6.0 Forms, AEM 6.1 Forms, AEM 6.2 Forms에서 AEM 6.5 Forms으로 직접 업그레이드할 수 없습니다. 하나 이상의 LiveCycle 또는 AEM Forms 버전으로 중간 업그레이드를 수행한 다음 AEM 6.5 Forms으로 업그레이드할 수 있습니다. 중간 버전 및 해당 업그레이드 지침 목록은 다음을 참조하십시오. [업그레이드 경로 선택](upgrade.md).
