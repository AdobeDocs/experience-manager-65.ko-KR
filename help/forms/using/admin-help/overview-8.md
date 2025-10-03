---
title: 출력 서비스 개요
description: 출력 서비스를 사용하면 Designer에서 만든 양식 디자인과 XML 양식 데이터를 병합하여 다양한 형식의 문서 출력 스트림을 만들 수 있습니다.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_output
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: e99b72d0-fbd5-4150-a225-1a91ad4c5867
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: e821be5233fd5f6688507096790d219d25903892
workflow-type: ht
source-wordcount: '260'
ht-degree: 100%

---

# 출력 서비스 개요 {#overview-of-output-service}

출력 서비스를 사용하면 Designer에서 만든 양식 디자인과 XML 양식 데이터를 병합하여 다양한 형식의 문서 출력 스트림을 만들 수 있습니다. 이 출력 스트림을 네트워크 프린터, 로컬 프린터 또는 디스크 파일로 전송할 수 있습니다.

관리 콘솔의 출력 페이지에서 출력 서비스를 관리할 수 있습니다. 구성한 설정은 AEM Forms API를 통해 동등한 설정이 지정되지 않은 경우 런타임에 사용됩니다. AEM Forms SDK를 통해 수행한 구성은 관리 콘솔을 사용하여 구성한 설정을 재정의합니다.

출력 서비스에 대한 자세한 내용은 [서비스 참조](https://www.adobe.com/go/learn_aemforms_services_61)를 참조하십시오.

관리 콘솔의 출력 페이지에서 다음과 같은 여러 작업을 수행할 수 있습니다.

* 국제화를 위해 문자 세트를 지정합니다. ([문자 세트 변경](/help/forms/using/admin-help/change-character-set.md#change-the-character-set)을 참조하십시오.)
* URL, URI, XCI 및 파일 위치에 대한 절대 경로와 상대 경로를 지정합니다. ([출력 파일 위치 지정](/help/forms/using/admin-help/specify-file-locations-output.md#specify-file-locations-for-output)을 참조하십시오.)
* 캐시 크기와 정책을 구성합니다. ([캐시 모드 지정](/help/forms/using/admin-help/configuring-caching-output.md#specifying-the-cache-mode) 및 [캐시 설정 구성](/help/forms/using/admin-help/configuring-caching-output.md#configuring-cache-settings)을 참조하십시오.)
* 애플리케이션 서버에서 글꼴을 사용 가능하도록 제공합니다. ([글꼴을 사용 가능하도록 제공](/help/forms/using/admin-help/make-fonts-available.md#make-fonts-available)을 참조하십시오.)
* 임베드할 글꼴을 지정합니다. ([임베드할 글꼴 지정](/help/forms/using/admin-help/specify-fonts-embed.md#specify-fonts-to-embed)을 참조하십시오.)
* XCI 구성 옵션을 지정합니다. ([XCI 구성 옵션 지정](/help/forms/using/admin-help/specify-xci-configuration-options.md#specify-xci-configuration-options)을 참조하십시오.)
* 보안 설정을 지정합니다. ([보안 설정 지정](/help/forms/using/admin-help/specify-security-settings.md#specify-security-settings)을 참조하십시오.)

설정을 변경한 후 저장을 클릭하여 해당 설정을 출력에 적용합니다. 서버를 다시 시작하지 않아도 변경 사항이 적용되지만, 캐시 설정을 구성할 때는 출력 서비스를 다시 시작해야 할 수 있습니다.
