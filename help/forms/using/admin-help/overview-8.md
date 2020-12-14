---
title: 출력 서비스 개요
seo-title: 출력 서비스 개요
description: 출력을 사용하면 Designer에서 만든 양식 디자인과 XML 양식 데이터를 병합하여 문서 출력 스트림을 다양한 형식으로 만들 수 있습니다.
seo-description: 출력을 사용하면 Designer에서 만든 양식 디자인과 XML 양식 데이터를 병합하여 문서 출력 스트림을 다양한 형식으로 만들 수 있습니다.
uuid: 7890b0a6-bae5-4ad5-ae41-503b988ba3da
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_output
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 5a96f5ea-6fe3-44b1-b314-14097b9e9c01
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '292'
ht-degree: 0%

---


# 출력 서비스 {#overview-of-output-service} 개요

출력을 사용하면 Designer에서 만든 양식 디자인과 XML 양식 데이터를 병합하여 문서 출력 스트림을 다양한 형식으로 만들 수 있습니다. 출력 스트림을 네트워크 프린터, 로컬 프린터 또는 디스크 파일로 보낼 수 있습니다.

관리 콘솔의 출력 페이지를 사용하여 출력 서비스를 관리할 수 있습니다. 구성하는 설정은 AEM 양식 API를 통해 해당 설정이 지정되지 않은 런타임에 사용됩니다. AEM 양식 SDK를 통해 구성한 내용은 관리 콘솔을 사용하여 구성된 설정을 무시합니다.

출력 서비스에 대한 자세한 내용은 [서비스 참조](https://www.adobe.com/go/learn_aemforms_services_61)를 참조하십시오.

관리 콘솔의 출력 페이지에서 다음과 같은 여러 작업을 수행할 수 있습니다.

* 국제화 문자 집합을 지정합니다. 자세한 내용은 [문자 세트](/help/forms/using/admin-help/change-character-set.md#change-the-character-set) 변경을 참조하십시오.
* URL, URI, XCI 및 파일 위치에 대한 절대 및 상대 경로를 지정합니다. 자세한 내용은 [출력](/help/forms/using/admin-help/specify-file-locations-output.md#specify-file-locations-for-output)의 파일 위치 지정을 참조하십시오.
* 캐시 크기 및 정책을 구성합니다. ([캐시 모드 지정](/help/forms/using/admin-help/configuring-caching-output.md#specifying-the-cache-mode) 및 [캐시 설정 구성](/help/forms/using/admin-help/configuring-caching-output.md#configuring-cache-settings)을 참조하십시오.)
* 응용 프로그램 서버에서 글꼴을 사용할 수 있도록 합니다. ([글꼴을 사용할 수 있도록 설정](/help/forms/using/admin-help/make-fonts-available.md#make-fonts-available) 참조)
* 포함할 글꼴을 지정합니다. ([포함할 글꼴 지정](/help/forms/using/admin-help/specify-fonts-embed.md#specify-fonts-to-embed)을 참조하십시오.)
* XCI 구성 옵션을 지정합니다. 자세한 내용은 [XCI 구성 옵션 지정](/help/forms/using/admin-help/specify-xci-configuration-options.md#specify-xci-configuration-options)을 참조하십시오.
* 보안 설정을 지정합니다. 자세한 내용은 [보안 설정 지정](/help/forms/using/admin-help/specify-security-settings.md#specify-security-settings)을 참조하십시오.

설정을 변경한 후 [저장]을 클릭하여 [출력]에 적용합니다. 변경 사항을 적용하기 위해 서버를 다시 시작할 필요는 없지만 캐시 설정을 구성할 때 출력 서비스를 다시 시작해야 할 수도 있습니다.
