---
title: XCI 구성 옵션 지정
seo-title: XCI 구성 옵션 지정
description: XCI 구성 옵션을 지정하는 방법을 알아봅니다.
seo-description: XCI 구성 옵션을 지정하는 방법을 알아봅니다.
uuid: 5d3c10c1-4a93-4336-b311-20faaf835b9f
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 162c9fda-f4d4-4ad5-a9ab-7554828e821c
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '141'
ht-degree: 1%

---


# XCI 구성 옵션 지정 {#specifying-xci-configuration-options}

Forms에서는 렌더링에 사용할 사용자 정의 XCI 파일을 지정할 수 있습니다. (Forms[에 대한 위치 구성을 참조하십시오.) ](/help/forms/using/admin-help/configuring-locations-forms.md#configuring-locations-for-forms) 기본적으로 Forms은 다음을 포함하여 XCI 파일에 지정된 일부 옵션을 무시합니다.

* `config/present/xdp/packets`
* `config/present/pdf/creator`
* `config/present/pdf/producer`
* `config/present/pdf/compression/compressObjectStream`

위에 나열된 옵션에 대한 재정의를 취소하는 옵션을 선택할 수 있습니다. 이 경우 Forms은 사용자 정의 XCI 파일에 지정된 값을 사용합니다.

1. 관리 콘솔에서 서비스 > Forms을 클릭합니다.
1. [시스템 기본 XCI 옵션 사용] 확인란을 선택하거나 선택 취소합니다. 이 옵션을 선택하면 Forms은 패킷, 작성자, 프로듀서 및 compressObjectStream 설정에 대한 기본값을 사용합니다. 이 옵션을 선택 해제하면 Forms에서 사용자 정의 XCI 파일에 지정된 값을 사용합니다.
1. 저장을 클릭합니다.

