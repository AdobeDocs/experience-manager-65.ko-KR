---
title: 컬렉션, 코드 조각 및 코드 조각 템플릿에 대한 다중 임차인
description: 멀티 테넌트 기능을 사용하여 고객 조직을 기반으로 CRX 저장소의 콘텐츠를 분리하여 무단 액세스를 방지하는 방법에 대해 알아봅니다.
contentOwner: AG
role: Architect, Admin, Leader
feature: Collections
exl-id: f95560c9-f1b9-4e86-94a7-70347d268d8f
source-git-commit: bb46b0301c61c07a8967d285ad7977514efbe7ab
workflow-type: tm+mt
source-wordcount: '220'
ht-degree: 1%

---

# 컬렉션, 코드 조각 및 코드 조각 템플릿에 대한 다중 임차인 {#multi-tenancy-for-collections-snippets-and-snippet-templates}

다중 임차인 기능을 사용하면 조직 접두사 및 조직 ID를 기반으로 CRX의 콘텐츠를 분리하여 다른 조직의 사용자가 콘텐츠를 무단으로 액세스하지 못하도록 보호할 수 있습니다.

[!DNL Adobe Experience Manager Assets] 각 조직의 데이터를 다른 경로에 저장합니다. 각 조직별 경로는 CRX에 다른 유형의 자산이 저장되는 기존 위치에 포함된 조직 접두사 및 조직 ID로 식별됩니다.

예를 들어 다음 이름의 폴더를 만드는 경우 `Demo`, [!DNL Experience Manager] 에셋은 일반적으로 다음 위치에 폴더를 저장합니다. `../content/dam/Demo`. 다중 임차인이 활성화되면 이제 다음 위치에 데이터를 저장할 수 있습니다. `../content/dam/<organization prefix>/<organization id>Demo`

예를 들어 다음과 같은 경우 [!DNL Adobe Marketing Cloud] 사용자 [!DNL Assets] (요청 시) `aodpremium` 조직, 다중 임차인 기능을 사용하여 다음을 구성할 수 있습니다. `../content/dam/<mac>/<aodpremium>Demo` 콘텐츠를 분리하는 경로입니다. 이 예에서는 `mac` 는 조직 접두사이며, `aodpremium` 는 조직 ID입니다.

사용자의 조직과 ID를 기반으로,에 이 적격 경로가 표시됩니다. [!DNL Assets] 인터페이스 및 여러 마법사(예: 분리 작업을 수행하기 위한 이동 및 코드 조각 만들기 마법사)

다중 임차인 기능을 사용하여 다음 유형의 에셋 및 구성 요소를 분리할 수 있습니다.

* 컬렉션
* 공용 컬렉션
* 카탈로그(페이지 추가/선택 마법사 포함)
* 템플릿
* 코드 조각 템플릿
* Lightbox
