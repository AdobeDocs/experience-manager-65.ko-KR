---
title: 컬렉션, 코드 조각 및 코드 조각 템플릿을 위한 멀티 테넌시
description: 멀티 테넌트 관리 기능을 통해 고객 조직을 기반으로 CRX 저장소의 컨텐츠를 분리하여 무단 액세스를 방지하는 방법을 살펴볼 수 있습니다.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 9fc1201db83ae0d3bb902d4dc3ab6d78cc1dc251
workflow-type: tm+mt
source-wordcount: '220'
ht-degree: 1%

---


# Multi-tenancy for Collections, snippets, and snippet templates {#multi-tenancy-for-collections-snippets-and-snippet-templates}

멀티 테넌시 기능을 사용하면 조직 접두사 및 조직 ID를 기반으로 CRX의 컨텐츠를 분리하여 다른 조직의 사용자가 인증되지 않은 액세스로부터 컨텐츠를 보호할 수 있습니다.

[!DNL Adobe Experience Manager Assets] 각 조직의 데이터를 다른 경로로 저장합니다. 각 조직별 경로는 서로 다른 유형의 에셋이 CRX에 저장된 기존 위치에 포함되어 있는 조직 접두사와 조직 ID로 식별됩니다.

예를 들어, 이름이 지정된 폴더를 만드는 경우 자산 `Demo`은 일반적으로 폴더를 다음 위치에 [!DNL Experience Manager] 저장합니다 `../content/dam/Demo`. 멀티 테넌시가 활성화되면 `../content/dam/<organization prefix>/<organization id>Demo`

예를 들어, 조직에 할당된 On-Demand [!DNL Adobe Marketing Cloud] 사용자 [!DNL Assets] 의 경우 `aodpremium` 다중 테넌시 기능을 사용하여 `../content/dam/<mac>/<aodpremium>Demo` 경로를 구성하여 컨텐츠를 분리할 수 있습니다. 이 예에서 `mac` 는 조직 접두사이며 조직 ID `aodpremium` 입니다.

사용자의 조직 및 ID를 기반으로, 이 정규화된 경로가 인터페이스와 다양한 마법사(예: 이동 및 코드 조각 만들기 마법사)에 표시되어 분리를 적용합니다. [!DNL Assets]

멀티 테넌시 기능을 사용하면 다음 유형의 자산 및 구성 요소를 분리할 수 있습니다.

* 컬렉션
* 공개 컬렉션
* 카탈로그(페이지 추가/선택 마법사 포함)
* 템플릿
* 코드 조각 템플릿
* Lightbox
