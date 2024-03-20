---
title: 출력 서비스 개요
description: 출력을 사용하면 XML 양식 데이터를 디자이너에서 만든 양식 디자인과 병합하여 다양한 형식의 문서 출력 스트림을 만들 수 있습니다.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_output
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: e99b72d0-fbd5-4150-a225-1a91ad4c5867
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '260'
ht-degree: 0%

---

# 출력 서비스 개요 {#overview-of-output-service}

출력을 사용하면 XML 양식 데이터를 디자이너에서 만든 양식 디자인과 병합하여 다양한 형식의 문서 출력 스트림을 만들 수 있습니다. 출력 스트림은 네트워크 프린터, 로컬 프린터 또는 디스크 파일로 전송될 수 있습니다

관리 콘솔의 [출력] 페이지를 사용하여 출력 서비스를 관리할 수 있습니다. 사용자가 구성하는 설정은 동일한 설정이 AEM Forms API를 통해 지정되지 않은 경우 런타임에 사용됩니다. AEM Forms SDK를 통해 수행한 구성은 관리 콘솔을 사용하여 구성된 설정을 무시합니다.

출력 서비스에 대한 자세한 내용은 [서비스 참조](https://www.adobe.com/go/learn_aemforms_services_61).

관리 콘솔의 출력 페이지에서 다음과 같은 여러 작업을 수행할 수 있습니다.

* 다국어화를 위해 문자 집합을 지정합니다. (참조: [문자 집합 변경](/help/forms/using/admin-help/change-character-set.md#change-the-character-set).)
* URL, URI, XCI 및 파일 위치에 대한 절대 및 상대 경로를 지정합니다. (참조: [출력을 위한 파일 위치 지정](/help/forms/using/admin-help/specify-file-locations-output.md#specify-file-locations-for-output).)
* 캐시 크기 및 정책을 구성합니다. (참조: [캐시 모드 지정](/help/forms/using/admin-help/configuring-caching-output.md#specifying-the-cache-mode) 및 [캐시 설정 구성](/help/forms/using/admin-help/configuring-caching-output.md#configuring-cache-settings).)
* 애플리케이션 서버에서 글꼴을 사용할 수 있도록 합니다. (참조: [글꼴 사용 가능](/help/forms/using/admin-help/make-fonts-available.md#make-fonts-available).)
* 포함할 글꼴을 지정합니다. (참조: [포함할 글꼴 지정](/help/forms/using/admin-help/specify-fonts-embed.md#specify-fonts-to-embed).)
* XCI 구성 옵션을 지정합니다. (참조: [XCI 구성 옵션 지정](/help/forms/using/admin-help/specify-xci-configuration-options.md#specify-xci-configuration-options).)
* 보안 설정을 지정합니다. (참조: [보안 설정 지정](/help/forms/using/admin-help/specify-security-settings.md#specify-security-settings).)

설정을 변경한 후 [저장]을 클릭하여 [출력]에 적용합니다. 변경 사항을 적용하려면 서버를 다시 시작하지 않아도 되지만 캐시 설정을 구성할 때 출력 서비스를 다시 시작해야 할 수도 있습니다.
