---
title: XCI 구성 옵션 지정
description: XCI 구성 옵션을 지정하는 방법을 알아봅니다. 적응형 양식에 대한 사용자 지정 XCI 파일 값을 지정하여 양식 렌더링 중에 사용할 수 있습니다.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_output
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 8fbff12a-4923-4151-a758-c1e44dee9160
source-git-commit: 6caf3ef4a00275f0f73be52b6a9ccba77d277f1a
workflow-type: tm+mt
source-wordcount: '149'
ht-degree: 1%

---

# XCI 구성 옵션 지정 {#specify-xci-configuration-options}

출력을 사용하면 렌더링에 사용하는 사용자 지정 XCI 파일을 지정할 수 있습니다. 다음을 참조하십시오 [출력을 위한 파일 위치 지정](/help/forms/using/admin-help/specify-file-locations-output.md#specify-file-locations-for-output).

기본적으로 출력은 다음을 포함하여 XCI 파일에 지정된 옵션 중 일부를 무시합니다.

* `config/present/xdp/packets`
* `config/present/pdf/creator`
* `config/present/pdf/producer`
* `config/present/pdf/compression/compressObjectStream`

위에 나열된 옵션의 재정의를 취소하는 옵션을 선택할 수 있습니다. 이 경우 출력은 사용자 지정 XCI 파일에 지정된 값을 사용합니다.

1. 관리 콘솔에서 다음을 클릭합니다. **서비스** > 출력.
1. 시스템 기본 XCI 옵션 사용 확인란을 선택하거나 선택 취소합니다. 이 옵션을 선택하면 Output에서는 패킷, 생성자, 생성자 및 compressObjectStream 설정에 대한 기본값을 사용합니다. 이 옵션을 선택 해제하면 출력에서 사용자 지정 XCI 파일에 지정된 값을 사용합니다.
1. **저장**&#x200B;을 클릭합니다.
