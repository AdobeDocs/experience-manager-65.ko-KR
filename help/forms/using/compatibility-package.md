---
title: 호환성 패키지
seo-title: 호환성 패키지
description: AEM Forms 6.5에 호환성 패키지를 설치하면 AEM Forms 6.4 및 이전 버전의 통신 관리 에셋과 더 이상 사용되지 않는 적응형 양식 템플릿 및 페이지를 사용할 수 있습니다
seo-description: AEM Forms 6.4에 호환성 패키지를 설치하면 AEM Forms 6.4의 통신 관리 에셋과 더 이상 사용되지 않는 적응형 양식 템플릿 및 페이지를 사용할 수 있습니다
uuid: b49633d6-2cb3-422c-a314-25f3b8a37b7f
contentOwner: gtalwar
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
geptopics: SG_AEMFORMS/categories/jee
discoiquuid: 73e8ccc6-f857-493e-b6e3-878f93e2a356
docset: aem65
translation-type: tm+mt
source-git-commit: dca52c05c413fc96bf7fab012a3be52f6769c2e0

---


# 호환성 패키지{#compatibility-package}

## 개요 {#overview}

인터랙티브한 커뮤니케이션은 AEM Forms 6.5에서 고객 커뮤니케이션을 제작하는 데 기본적으로 권장됩니다.AEM Forms 6.5에서 문자를 계속 사용하려면 최신 AEMFD [호환성 패키지를](https://helpx.adobe.com/aem-forms/kb/aem-forms-releases.html)설치해야 합니다.

또한 AEM Forms 6.5에서 AEM Forms 6.4, 6.3 및 6.2의 다음 자산을 [사용할 수 있습니다.](../../forms/using/compatibility-package.md#add-support-for-aem-forms-and-assets-in-aem-forms)

* 문서 조각
* 편지
* 데이터 사전
* 적응형 양식의 가치 하락 템플릿 및 페이지

자세한 내용은 호환성 [패키지를](../../forms/using/compatibility-package.md#assetsmadecompatible)설치하여 AEM Forms 6.5와 호환되는 자산을 참조하십시오.

## AEM Forms 6.5에서 AEM Forms 6.4, 6.3 및 6.2 자산에 대한 지원 추가 {#add-support-for-aem-forms-and-assets-in-aem-forms}

업그레이드를 수행한 후 다음을 수행하여 AEMFD 호환성 패키지를 설치하고 자산을 6.5와 호환되도록 하십시오.

AEM 호환성 [패키지가](https://helpx.adobe.com/aem-forms/kb/aem-forms-releases.html) 미리 설치되어 있는지 확인합니다.

1. 최신 6.5 호환성 [패키지를](https://helpx.adobe.com/aem-forms/kb/aem-forms-releases.html)설치합니다.

   패키지 업로드 및 설치에 대한 자세한 내용은 패키지 [작업](/help/sites-administering/package-manager.md)방법을 참조하십시오.

1. 로그가 안정되면 서버를 다시 시작합니다.
1. 마이그레이션 유틸리티를 사용하여 에셋을 6.5와 호환되게 합니다.

   자세한 내용은 [마이그레이션 유틸리티를](../../forms/using/migration-utility.md)참조하십시오.

## 호환성 패키지를 설치하여 AEM Forms 6.5와 호환되는 자산 {#assetsmadecompatible}

호환성 패키지를 설치하여 AEM Forms 6.5와 호환되는 다음 자산 및 템플릿을 만들 수 있습니다.

* AEM 6.4 및 이전 버전의 통신 관리 자산:

   * [편지](../../forms/using/create-letter.md)
   * [데이터 사전](/help/forms/using/data-dictionary.md)
   * 문서 단편

* 적응형 양식의 가치 하락 템플릿:

   * /libs/fd/af/templates/blankTemplate2
   * /libs/fd/af/templates/simpleEnrollmentTemplate
   * /libs/fd/af/templates/simpleEnrollmentTemplate2
   * /libs/fd/af/templates/surveyTemplate
   * /libs/fd/af/templates/surveyTemplate2
   * /libs/fd/af/templates/tabbedEnrollmentTemplate
   * /libs/fd/af/templates/tabbedEnrollmentTemplate2
   * /libs/fd/afaddon/templates/advancedEnrollmentTemplate
   * /libs/fd/afaddon/templates/advancedEnrollmentTemplate2

* 적응형 양식의 가치 하락 페이지:

   * /libs/fd/af/components/page/survey
   * /libs/fd/af/components/page/tabbedenrollment
   * /libs/fd/afaddon/components/page/advanced롤링

