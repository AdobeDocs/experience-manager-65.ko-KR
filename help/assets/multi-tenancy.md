---
title: 컬렉션, 코드 조각 및 코드 조각 템플릿에 대한 다중 임차인
description: 다중 임차인 기능을 사용하여 고객 조직에 따라 CRX 저장소의 콘텐츠를 분리하여 무단 액세스를 방지하는 방법에 대해 알아봅니다.
contentOwner: AG
role: Architect, Admin, Leader
feature: Collections
exl-id: f95560c9-f1b9-4e86-94a7-70347d268d8f
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '220'
ht-degree: 1%

---

# 컬렉션, 코드 조각 및 코드 조각 템플릿에 대한 다중 임차인 {#multi-tenancy-for-collections-snippets-and-snippet-templates}

다중 임차인 기능을 사용하면 조직 접두사 및 조직 ID를 기반으로 CRX의 콘텐츠를 분리하여 다른 조직의 사용자가 콘텐츠를 무단으로 액세스하지 못하도록 보호할 수 있습니다.

[!DNL Adobe Experience Manager Assets]은(는) 각 조직의 데이터를 다른 경로에 저장합니다. 각 조직별 경로는 조직 접두사 및 조직 ID로 식별됩니다
CRX에서 다양한 유형의 에셋이 저장되는 기존 위치에 포함됩니다.

예를 들어 이름이 `Demo`인 폴더를 만드는 경우 [!DNL Experience Manager] 자산은 일반적으로 폴더를 `../content/dam/Demo`에 저장합니다. 다중 테넌시가 활성화되면 이제 `../content/dam/<organization prefix>/<organization id>Demo`에 데이터를 저장할 수 있습니다.

예를 들어 `aodpremium` 조직에 할당된 [!DNL Assets]의 [!DNL Adobe Marketing Cloud] 사용자(주문형)에 대해 다중 임차인 기능을 사용하여 콘텐츠를 분리하도록 `../content/dam/<mac>/<aodpremium>Demo` 경로를 구성할 수 있습니다. 이 예제에서 `mac`은 조직 접두사이고 `aodpremium`은 조직 ID입니다.

사용자의 조직과 ID를 기반으로 이 정규화된 경로가 [!DNL Assets] 인터페이스와 격리를 적용하기 위한 이동 및 코드 조각 만들기 마법사를 비롯한 다양한 마법사에 표시됩니다.

다중 임차인 기능을 사용하여 다음 유형의 에셋 및 구성 요소를 분리할 수 있습니다.

* 컬렉션
* 공용 컬렉션
* 카탈로그(페이지 추가/선택 마법사 포함)
* 템플릿
* 코드 조각 템플릿
* Lightbox
