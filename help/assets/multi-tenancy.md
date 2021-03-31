---
title: 컬렉션, 코드 단편 및 코드 단편 템플릿에 대한 멀티 테넌시
description: 멀티 테넌시 기능을 사용하여 고객 조직을 기반으로 CRX 저장소의 컨텐츠를 분리하여 무단 액세스를 방지하는 방법을 살펴봅니다.
contentOwner: AG
role: 아키텍트, 관리자, 리더
feature: 컬렉션
translation-type: tm+mt
source-git-commit: 174e0703ae541641e3dc602e700bcd31624ae62c
workflow-type: tm+mt
source-wordcount: '224'
ht-degree: 1%

---


# 컬렉션, 코드 단편 및 코드 단편 템플릿에 대한 멀티 테넌시 {#multi-tenancy-for-collections-snippets-and-snippet-templates}

멀티 테넌트 기능을 사용하면 조직 접두사 및 조직 ID를 기반으로 CRX의 컨텐츠를 분리하여 다른 조직의 사용자가 무단 액세스로부터 컨텐츠를 보호할 수 있습니다.

[!DNL Adobe Experience Manager Assets] 각 조직의 데이터를 다른 경로로 저장합니다. 각 조직별 경로는 조직 접두사와 조직 ID로 식별됩니다
다양한 유형의 에셋이 CRX에 저장되는 기존 위치에 포함되어 있습니다.

예를 들어 `Demo` 폴더를 만드는 경우 일반적으로 [!DNL Experience Manager] 자산은 `../content/dam/Demo`에 폴더를 저장합니다. 멀티 테넌시가 활성화되면 이제 데이터를 `../content/dam/<organization prefix>/<organization id>Demo`에 저장할 수 있습니다.

예를 들어 `aodpremium` 조직에 할당된 [!DNL Assets](주문형)의 [!DNL Adobe Marketing Cloud] 사용자의 경우 멀티 테넌시 기능을 사용하여 `../content/dam/<mac>/<aodpremium>Demo` 경로를 구성하여 컨텐츠를 분리할 수 있습니다. 이 예에서 `mac`은 조직 접두사이고 `aodpremium`은 조직 ID입니다.

사용자의 조직 및 ID를 기반으로, 이 정규화된 경로는 [!DNL Assets] 인터페이스와 분리를 적용할 이동 및 조각 만들기 마법사를 비롯한 다양한 마법사에 표시됩니다.

멀티 테넌트 기능을 사용하면 다음 유형의 자산 및 구성 요소를 분리할 수 있습니다.

* 컬렉션
* 공개 컬렉션
* 카탈로그(페이지 추가/선택 마법사 포함)
* 템플릿
* 코드 단편 템플릿
* Lightbox
