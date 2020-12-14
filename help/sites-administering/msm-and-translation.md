---
title: 웹 사이트 관리
seo-title: 웹 사이트 관리
description: AEM에서 다국어 웹 사이트를 관리하는 방법을 살펴볼 수 있습니다.
seo-description: AEM에서 다국어 웹 사이트를 관리하는 방법을 살펴볼 수 있습니다.
uuid: a32d458b-a5ad-46ef-a68c-4717c63b4bdd
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: site-features
content-type: reference
discoiquuid: fabaa3e8-1657-4ed4-abb2-990117bec39c
translation-type: tm+mt
source-git-commit: 0885fb6eb6b6a6b8fefd522b2656c8f64e0a537e
workflow-type: tm+mt
source-wordcount: '351'
ht-degree: 2%

---


# 웹 사이트 관리{#website-administration}

웹 사이트 및 페이지를 관리하는 데 사용할 수 있는 관리 도구는 다음과 같습니다.

* MSM(Multi Site Manager)을 사용하면 여러 위치에서 동일한 사이트 컨텐츠를 사용하고 변형을 허용할 수 있습니다.

   * [컨텐츠 재활용:다중 사이트 관리자 및 Live Copy](/help/sites-administering/msm.md)

* 번역 기능을 사용하면 페이지 컨텐츠, 자산 및 사용자 생성 컨텐츠의 번역 작업을 자동화하여 다국어 웹 사이트를 제작 및 유지 관리할 수 있습니다.

   * [다국어 사이트의 컨텐츠 번역](/help/sites-administering/translation.md)

* 이 두 기능은 모두 [다국적 및 다국어](#multinational-and-multilingual-sites)인 웹 사이트에 맞게 결합할 수 있습니다.

## 다국적 및 다국어 사이트 {#multinational-and-multilingual-sites}

다중 사이트 관리자 및 번역 워크플로우의 통합을 통해 다국적 사이트와 다국어 사이트의 컨텐츠를 효율적으로 만들 수 있습니다. 특정 국가에서 하나의 언어로 마스터 사이트를 만든 다음 필요한 경우 번역을 사용하여 해당 컨텐츠를 다른 사이트의 기초로 사용할 수 있습니다.

* [마스터 ](/help/sites-administering/translation.md) 사이트를 다른 언어로 변환합니다.

* [다중 사이트 관리자](/help/sites-administering/msm.md)를 사용하여 다음을 수행합니다.

   * 마스터 사이트 및 번역 컨텐츠의 컨텐츠를 다시 사용하여 다른 국가 및 문화를 위한 사이트를 만들 수 있습니다.
   * 여러 사이트 관리자를 국가 사이트의 영어 마스터 -> 영어 분기, 프랑스어 마스터 -> 국가 사이트의 프랑스어 분기 등 하나의 언어 내의 컨텐츠로 제한할 수 있습니다.
   * 필요한 경우 Live Copy의 요소를 분리하여 로컬라이제이션 세부 사항을 추가합니다.

다음 다이어그램은 기본 개념이 교차하는 방식을 보여 줍니다(관련된 모든 레벨/요소는 표시되지 않음).

![chlimage_1-71](assets/chlimage_1-71a.png)

>[!NOTE]
>
>이와 유사한 시나리오에서는 MSM이 이와 같이 다른 언어 버전을 관리하지 않습니다.
>
>* [MSM언어](/help/sites-administering/msm.md) 의 경계 내에서 번역된 컨텐츠의 블루프린트(예: 글로벌 마스터)에서 Live Copy(예: 로컬 사이트)로의 배포를 관리합니다.
>* 제3자 번역 관리 서비스와 함께 AEM의 [번역](/help/sites-administering/translation.md) 통합 기능은 언어를 관리하고 컨텐츠를 이러한 다른 언어로 번역합니다.

>
>
고급 사용 사례의 경우 MSM은 언어 마스터 간에 사용될 수 있습니다.

>[!NOTE]
>
>모든 사용 사례의 경우 다음 우수 사례를 읽는 것이 좋습니다.
>
>* [MSM에 대한 우수 사례](/help/sites-administering/msm-best-practices.md);특히:
   >
   >   
   * [사이트 만들기](/help/sites-administering/msm-best-practices.md#create-site)
   >   * [MSM 및 다국어 웹 사이트](/help/sites-administering/msm-best-practices.md#msm-and-multilingual-websites)
>
>* [번역 우수 사례](/help/sites-administering/tc-bp.md)

