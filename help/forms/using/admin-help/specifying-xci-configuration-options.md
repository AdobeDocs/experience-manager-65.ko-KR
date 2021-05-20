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
exl-id: 7cd10389-63e6-41f2-a132-92fd9e40a9b7
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '141'
ht-degree: 1%

---

# XCI 구성 옵션 {#specifying-xci-configuration-options} 지정

Forms을 사용하면 렌더링에 사용할 사용자 지정 XCI 파일을 지정할 수 있습니다. ([Forms에 대한 위치 구성](/help/forms/using/admin-help/configuring-locations-forms.md#configuring-locations-for-forms)을 참조하십시오.) 기본적으로 Forms은 다음을 포함하여 XCI 파일에 지정된 일부 옵션을 무시합니다.

* `config/present/xdp/packets`
* `config/present/pdf/creator`
* `config/present/pdf/producer`
* `config/present/pdf/compression/compressObjectStream`

위에 나열된 옵션에 대한 무시를 취소하는 옵션을 선택할 수 있습니다. 이 경우 Forms에서는 사용자 지정 XCI 파일에 지정된 값을 사용합니다.

1. 관리 콘솔에서 서비스 > Forms 를 클릭합니다.
1. 시스템 기본 XCI 옵션 사용 확인란을 선택하거나 선택 취소합니다. 이 옵션을 선택하면 Forms은 패킷, 생성자, 생성자 및 compressObjectStream 설정에 해당 기본값을 사용합니다. 이 옵션을 선택 취소하면 Forms에서 사용자 지정 XCI 파일에 지정된 값을 사용합니다.
1. 저장을 클릭합니다.
