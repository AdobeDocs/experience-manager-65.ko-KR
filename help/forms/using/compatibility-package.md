---
title: 호환성 패키지
description: AEM Forms 6.5에 호환성 패키지를 설치하면 AEM Forms 6.4 및 이전 버전의 서신 관리 에셋과 더 이상 사용되지 않는 적응형 양식 템플릿 및 페이지를 사용할 수 있습니다
contentOwner: gtalwar
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management, installing
geptopics: SG_AEMFORMS/categories/jee
docset: aem65
role: Admin
exl-id: bb16017c-a1bf-40d8-a78d-827c05b7ee2e
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '355'
ht-degree: 2%

---

# 호환성 패키지{#compatibility-package}

## 개요 {#overview}

대화형 통신은 AEM Forms 6.5에서 고객 커뮤니케이션을 만들기 위한 기본적이고 권장되는 방법입니다. AEM Forms 6.5에서 문자를 계속 사용하려면 최신 버전을 설치해야 합니다 [AEMFD 호환성 패키지](https://helpx.adobe.com/kr/aem-forms/kb/aem-forms-releases.html).

AEMFD 호환성 패키지를 통해 다음과 같은 작업을 수행할 수 있습니다. [AEM Forms 6.5에서 AEM Forms 6.4, 6.3 및 6.2의 다음 자산을 사용합니다.](../../forms/using/compatibility-package.md#add-support-for-aem-forms-and-assets-in-aem-forms)

* 문서 단편
* 편지
* 데이터 사전
* 적응형 양식 더 이상 사용되지 않는 템플릿 및 페이지

자세한 내용은 [호환성 패키지를 설치하여 AEM Forms 6.5와 호환되도록 만든 자산](../../forms/using/compatibility-package.md#assetsmadecompatible).

## AEM Forms 6.5에서 AEM Forms 6.4, 6.3 및 6.2 자산에 대한 지원 추가 {#add-support-for-aem-forms-and-assets-in-aem-forms}

업그레이드를 수행한 후 다음을 수행하여 AEMFD 호환성 패키지를 설치하고 에셋을 6.5와 호환되도록 합니다.

다음을 수행했는지 확인: [AEM 호환성 패키지](https://helpx.adobe.com/kr/aem-forms/kb/aem-forms-releases.html) 사전 설치됨.

1. 최신 6.5 설치 [호환성 패키지](https://helpx.adobe.com/kr/aem-forms/kb/aem-forms-releases.html).

   패키지 업로드 및 설치에 대한 자세한 내용은 [패키지를 사용하여 작업하는 방법](/help/sites-administering/package-manager.md).

1. 로그가 안정되면 서버를 다시 시작합니다.
1. 자산을 6.5와 호환되도록 하려면 마이그레이션 유틸리티를 사용하십시오.

   >[!NOTE]
   >
   > SDK를 다시 시작하려면 &#39;Ctrl + C&#39; 명령을 사용하는 것이 좋습니다. Java 프로세스 중지와 같은 대체 방법을 사용하여 AEM SDK를 다시 시작하면 AEM 개발 환경이 일치하지 않을 수 있습니다.

   자세한 내용은 [마이그레이션 유틸리티](../../forms/using/migration-utility.md).

## 호환성 패키지를 설치하여 AEM Forms 6.5와 호환되도록 만든 자산 {#assetsmadecompatible}

호환성 패키지를 설치하여 다음 에셋 및 템플릿을 AEM Forms 6.5와 호환되도록 할 수 있습니다.

* AEM 6.4 및 이전 버전의 서신 관리 에셋:

   * [편지](../../forms/using/create-letter.md)
   * [데이터 사전](/help/forms/using/data-dictionary.md)
   * 문서 단편

* 적응형 양식 사용 중단된 템플릿:

   * /libs/fd/af/templates/blankTemplate2
   * /libs/fd/af/templates/simpleEnrollmentTemplate
   * /libs/fd/af/templates/simpleEnrollmentTemplate2
   * /libs/fd/af/templates/surveyTemplate
   * /libs/fd/af/templates/surveyTemplate2
   * /libs/fd/af/templates/tabEnrollmentTemplate
   * /libs/fd/af/templates/tabEnrollmentTemplate2
   * /libs/fd/afaddon/templates/advancedEnrollmentTemplate
   * /libs/fd/afaddon/templates/advancedEnrollmentTemplate2

* 적응형 양식 더 이상 사용되지 않는 페이지:

   * /libs/fd/af/components/page/survey
   * /libs/fd/af/components/page/tabbedenrollment
   * /libs/fd/afaddon/components/page/advancedenrollment
