---
title: AEM 6.5 Forms으로 업그레이드
seo-title: AEM 6.5 Forms으로 업그레이드
description: AEM 6.3 Forms 및 AEM 6.4 Forms에서 AEM 6.5 Forms으로 바로 업그레이드할 수 있습니다.
seo-description: AEM 6.3 Forms 및 AEM 6.4 Forms에서 AEM 6.5 Forms으로 바로 업그레이드할 수 있습니다.
uuid: 7a38cd72-2d01-4af7-b6a3-00dc34c4f02b
content-type: reference
topic-tags: installing
geptopics: SG_AEMFORMS/categories/jee
discoiquuid: f89921ef-c638-4a07-88d5-3dd8614c5166
docset: aem65
translation-type: tm+mt
source-git-commit: 1dfc8fa91d3e5ae8ca49cf1f3cb739b59feb18cf
workflow-type: tm+mt
source-wordcount: '232'
ht-degree: 0%

---


# AEM 6.5 Forms으로 업그레이드{#upgrade-to-aem-forms}

AEM 6.5 Forms에는 양식과 통신의 제작, 관리 및 사용자 경험을 간소화하는 몇 가지 새로운 기능과 향상된 기능이 포함되어 있습니다. AEM 6.5 Forms의 새로운 기능과 개선 사항에 대해 자세히 알아보려면 [새로운 기능 요약 문서](../../forms/using/whats-new.md)를 참조하십시오.

기존 LiveCycle 또는 AEM Forms 설치를 업그레이드하면 기존 데이터, 프로세스 및 에셋을 그대로 유지하면서 AEM 6.5 Forms에서 제공하는 새로운 기능과 향상된 기능을 얻을 수 있습니다. 업그레이드 시 프로세스의 메타데이터 및 상태도 유지됩니다. 업그레이드를 시작할 업그레이드 경로를 선택할 수 있습니다.

다음 다이어그램은 OSGi에서 AEM Forms에 사용할 수 있는 업그레이드 경로를 보여줍니다.

![](do-not-localize/osgi-upgrade-path.png)

다음 위치에서 직접 업그레이드를 수행할 수 있습니다.

* OSGi 기반의 AEM 6.3 Forms
* OSGi 기반의 AEM 6.4 Forms

또한

* OSGi 기반의 AEM 6.0 Forms
* OSGi 기반의 AEM 6.1 Forms
* OSGi 기반의 AEM 6.2 Forms

다음 다이어그램은 JEE에서 AEM Forms에 사용할 수 있는 업그레이드 경로를 보여줍니다.

![](do-not-localize/jee-upgrade-6-5.png)

다음 위치에서 직접 업그레이드를 수행할 수 있습니다.

* AEM 6.3 Forms on JEE
* AEM 6.4 Forms on JEE

또한

* LiveCycle ES2
* LiveCycle ES3
* LiveCycle ES4 SP1
* AEM 6.0 Forms on JEE
* AEM 6.1 Forms on JEE
* AEM 6.2 Forms on JEE

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
