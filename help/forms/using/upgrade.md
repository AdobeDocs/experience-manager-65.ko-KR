---
title: AEM 6.5 Forms로 업그레이드
description: AEM 6.3 Forms 및 AEM 6.4 Forms에서 AEM 6.5 Forms으로 직접 업그레이드할 수 있습니다.
content-type: reference
topic-tags: installing
geptopics: SG_AEMFORMS/categories/jee
docset: aem65
role: Admin,User
exl-id: 2fc8abec-8ba6-40b7-bbb1-4288eeea7c86
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,AEM Forms Upgrade
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '364'
ht-degree: 6%

---

# AEM 6.5 Forms로 업그레이드 {#upgrade-to-aem-forms}

| 버전 | 문서 링크 |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [여기 클릭](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/setup-configure-migrate/migrate-to-forms-as-a-cloud-service.html) |
| AEM 6.5 | 이 문서 |


AEM 6.5 Forms에는 양식 및 서신에 대한 생성, 관리 및 사용자 경험을 간소화하는 몇 가지 새로운 기능과 개선 사항이 포함되어 있습니다. AEM 6.5 Forms의 모든 새로운 기능과 향상된 기능에 대해 알아보려면 다음을 참조하십시오. [새로운 기능 요약 문서](../../forms/using/whats-new.md).

기존 LiveCycle 또는 AEM Forms 설치를 업그레이드하여 기존 데이터, 프로세스 및 에셋을 그대로 유지하면서 AEM 6.5 Forms에서 제공하는 새로운 기능과 개선 사항을 얻을 수 있습니다. 업그레이드 시 메타데이터와 프로세스의 상태도 유지됩니다. 업그레이드 경로를 선택하여 업그레이드를 시작할 수 있습니다.

다음 다이어그램은 OSGi에서 AEM Forms에 사용할 수 있는 업그레이드 경로를 표시합니다.

![OSGi 업그레이드 흐름](do-not-localize/osgi-upgrade-path.png)

다음 위치에서 직접 업그레이드를 수행할 수 있습니다.

* OSGi의 AEM 6.3 Forms
* OSGi의 AEM 6.4 Forms

에서 다중 홉 업그레이드를 수행할 수도 있습니다.

* OSGi의 AEM 6.0 Forms
* OSGi의 AEM 6.1 Forms
* OSGi의 AEM 6.2 Forms

다음 다이어그램은 JEE의 AEM Forms에 사용할 수 있는 업그레이드 경로를 표시합니다.

![JEE 업그레이드 6.5](do-not-localize/jee-upgrade-6-5.png)


다음 위치에서 직접 업그레이드를 수행할 수 있습니다.

* JEE의 AEM 6.3 Forms
* JEE의 AEM 6.4 Forms
* JEE의 AEM 6.5.x.x Forms

에서 다중 홉 업그레이드를 수행할 수도 있습니다.

* LiveCycle ES4 SP1
* JEE의 AEM 6.0 Forms
* JEE의 AEM 6.1 Forms
* JEE의 AEM 6.2 Forms

JEE의 AEM 6.5.18.0 Forms은 두 가지 유형의 설치 관리자를 제공합니다. [전체 설치 관리자](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html) 및 [패치 설치 관리자](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html).

**전체 설치 관리자**: 전체 설치 관리자를 사용하여 새로운 AEM Forms 인스턴스를 설정하거나 AEM 6.5.x.x Forms on JEE에서 AEM 6.5.18.0 Forms으로 업그레이드를 수행할 수 있습니다.

**패치 설치 관리자**: 패치 설치 관리자는 이미 AEM 6.5.x.x 버전을 사용 중인 고객을 위한 것입니다. 패치 설치 관리자를 사용하여 최신 버전의 AEM Forms으로 업그레이드할 수 있습니다.

다음 이미지는 전체 및 패치 설치 관리자를 사용하기 위한 시나리오를 보여 줍니다.

![전체 설치 관리자 및 패치 설치 관리자](/help/forms/using/assets/full-and-patch-installer.png)

다음을 참조하십시오. [AEM 6.5 Forms 서비스 팩 설치 지침](https://experienceleague.adobe.com/docs/experience-manager-65/release-notes/aem-forms-current-service-pack-installation-instructions.html) jee 환경에 대한 최신 서비스 팩을 설치하는 문서입니다.

<!--
[Work in Progress]

Migration involves moving only assets (PDF, XDP, images, adaptive forms, correspondence management assets) from one server to another - processes (LCA), settings, configurations, and a few other pieces of metadata are not migrated. Perform the following steps to migrate to AEM 6.3 Forms:

1. Set up a fresh environment of [AEM 6.3 Forms](https://adobe.com/go/learn_aemforms_documentation_63).
1. Move XDP or other compatible assets to the freshly set instance. For detailed instructions, see [Importing and exporting assets to AEM Forms](../../forms/using/import-export-forms-templates.md). [
   ](../../forms/using/import-export-forms-templates.md)
1. Build the required services, if any.

   For example, if you are using AEM Forms on JEE Document Services, changes are required in the code to use document services available in AEM Forms on OSGi.

1. Perform post-installation activities:

    * **Run Migration Utility**

      The migration utility makes the adaptive forms and correspondence management assets of earlier versions compatible with AEM 6.3 forms. You can download the utility from AEM Software Distribution. For step-by-step information to configure and use the migration utility, see [migration utility](../../forms/using/migration-utility.md) documentation.

    * **Reconfigure Adobe Sign**

      If you had Adobe Sign configured in the previous version of AEM Forms, then reconfigure Adobe Sign from AEM Cloud services. For more details, see [Integrate Adobe Sign with AEM Forms](../../forms/using/adobe-sign-integration-adaptive-forms.md).

      Moreover, AEM 6.3 Forms release has introduced many new Adobe Sign features. For step-by-step information to use Adobe Sign, see [Using Adobe Sign in an adaptive form](../../forms/using/working-with-adobe-sign.md).

    * **Reconfigure analytics and reports**

      In AEM 6.3 Forms, traffic variable for source and success event for impression are not available. So, when you upgrade to AEM 6.3 Forms, AEM Forms stops sending data to Adobe Analytics server and analytics reports for adaptive forms are not available. Moreover, AEM 6.3 Forms introduces traffic variable for the version of form analytics and success event for the amount of time spent on a field. So, reconfigure analytics and reports for your AEM Forms environment. For detailed steps, see [Configuring analytics and reports](../../forms/using/configure-analytics-forms-documents.md).

      Methods to calculate average fill time for forms and average read time for have changed. So, when you upgrade to AEM 6.3 forms, older data (data from previous AEM Forms release) for these metrics is available only in Adobe Analytics. It is not visible in AEM Forms analytics reports. For these metrics, AEM Forms analytics reports display data which is captured after performing the upgrade.
      
      -->


