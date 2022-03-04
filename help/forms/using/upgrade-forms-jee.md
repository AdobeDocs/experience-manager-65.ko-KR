---
title: AEM 6.5 Forms로 업그레이드
seo-title: Upgrade to AEM 6.5 Forms
description: AEM 6.1 Forms, AEM 6.2 Forms 및 LiveCycle ES4 SP1에서 AEM 6.3 Forms으로 직접 업그레이드할 수 있습니다.
seo-description: You can perform a direct upgrade from AEM 6.1 Forms, AEM 6.2 Forms, and LiveCycle ES4 SP1 to AEM 6.3 Forms.
uuid: 1435246a-9215-4d88-b52c-59a5c329bb77
content-type: reference
products: SG_EXPERIENCEMANAGER/6.3/FORMS
topic-tags: installing
geptopics: SG_AEMFORMS/categories/jee
discoiquuid: e745033f-8015-4fae-9d82-99d35802c0a6
role: Admin
exl-id: 722e75a0-bcb3-465e-bb74-ea94a3b99fd3
source-git-commit: 2e6d688818e9cc337444bcda2a49485e9167a113
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---

# JEE의 AEM 6.5 Forms으로 업그레이드 {#upgrade-to-aem-forms-jee}

JEE의 AEM 6.5.12.0 Forms은 두 가지 유형의 설치 프로그램을 제공합니다. 전체 설치 프로그램 및 패치 설치 프로그램입니다.

**전체 설치 관리자**: 를 사용할 수 있습니다 [JEE 전체 설치 프로그램의 AEM 6.5.12.0](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html) 최신 AEM Forms 인스턴스를 설정하거나 JEE의 AEM 6.3 Forms에서 업그레이드, JEE의 AEM 6.5.x.x Forms에서 JEE의 AEM 6.5.12.0 Forms으로 즉시 업그레이드

**패치 설치 프로그램**: [JEE 패치 설치 프로그램의 AEM 6.5.12.0](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html) AEM 6.5.x.x 버전을 이미 사용하는 고객을 위한 것입니다. 패치 설치 프로그램을 사용하여 최신 버전의 AEM Forms으로 업그레이드할 수 있습니다.

다음 표에서는 전체 및 패치 설치 관리자를 사용하기 위한 세션을 설명합니다.

![](assets/full-and-patch-installer.png)

전체 설치 프로그램을 사용하여 JEE의 기존 AEM 6.3 Forms 또는 JEE의 AEM 6.4 Forms을 JEE의 AEM 6.5.12.0 Forms으로 업그레이드하려면 다음 절차를 수행하십시오.

1. JEE 설치 프로그램에서 AEM 6.5 Forms 를 다운로드합니다. [소프트웨어 배포](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html). 설치 관리자를 사용하려면 유효한 유지 관리 및 지원 계약이 필요합니다.
1. 자세한 내용은 [업그레이드 검사 목록 및 계획](https://www.adobe.com/go/learn_aemforms_upgrade_checklist_65) 성공적인 업그레이드를 위해 수행할 검사에 대해 알아보십시오.
1. 자세한 내용은 [AEM Forms으로 업그레이드 준비](https://www.adobe.com/go/learn_aemforms_prepareupgrade_65) 서버 다운타임을 최소화하면서 업그레이드가 올바르게 실행되도록 하는 작업을 배우고 수행하려면 다음을 수행하십시오.
1. 기존 환경과 애플리케이션 서버에 따라 다음 문서 중 하나를 선택하고 지침을 따릅니다.

   * [AEM 6.3 또는 AEM 6.4 Forms에서 JBoss용 AEM 6.5 Forms으로 업그레이드](http://www.adobe.com/go/learn_aemforms_upgradeJBoss_65)
   * [AEM 6.3 또는 AEM 6.4 Forms에서 WebSphere용 AEM 6.5 Forms으로 업그레이드](http://www.adobe.com/go/learn_aemforms_upgradeWebSphere_65)
   * [AEM 6.3 또는 AEM 6.4 Forms에서 JBoss 턴키용 AEM 6.5 Forms으로 업그레이드](http://www.adobe.com/go/learn_aemforms_upgradeTurnkey_65)

LiveCycle ES2, LiveCycle ES3, AEM 6.0 Forms, AEM 6.1 Forms, AEM 6.2 Forms에서 AEM 6.5로 직접 업그레이드할 Forms 수 없습니다. 하나 이상의 LiveCycle 또는 AEM Forms 버전으로 중간 업그레이드를 수행한 다음, AEM 6.5 Forms으로 업그레이드할 수 있습니다. 중간 버전 및 해당 업그레이드 지침에 대해서는 [업그레이드 경로 선택](upgrade.md).
