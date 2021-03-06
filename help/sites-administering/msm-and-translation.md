---
title: 웹 사이트 관리
seo-title: 웹 사이트 관리
description: AEM에서 다국어 웹 사이트를 관리하는 방법을 알아봅니다.
seo-description: AEM에서 다국어 웹 사이트를 관리하는 방법을 알아봅니다.
uuid: a32d458b-a5ad-46ef-a68c-4717c63b4bdd
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: site-features
content-type: reference
discoiquuid: fabaa3e8-1657-4ed4-abb2-990117bec39c
exl-id: 8f11f5de-f5af-4ce7-a448-2b4299de2930
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '351'
ht-degree: 2%

---

# 웹 사이트 관리{#website-administration}

웹 사이트 및 페이지를 관리하는 데 사용할 수 있는 관리 도구는 다음과 같습니다.

* MSM(Multi Site Manager)을 사용하면 여러 위치에서 동일한 사이트 콘텐츠를 사용할 수 있고 변형을 허용합니다.

   * [컨텐츠 재사용:다중 사이트 관리자 및 Live Copy](/help/sites-administering/msm.md)

* 번역 기능을 사용하면 페이지 콘텐츠, 자산 및 사용자 생성 콘텐츠의 번역을 자동화하여 다국어 웹 사이트를 제작 및 유지 관리할 수 있습니다.

   * [다국어 사이트의 컨텐츠 번역](/help/sites-administering/translation.md)

* 이 두 기능을 결합하여 [다국적 및 다국어](#multinational-and-multilingual-sites)인 웹 사이트를 제공할 수 있습니다.

## 다국적 및 다국어 사이트 {#multinational-and-multilingual-sites}

다중 사이트 관리자 와 번역 워크플로우의 통합을 사용하여 다국적 및 다국어 사이트용 콘텐츠를 효율적으로 만들 수 있습니다. 특정 국가에 대해 하나의 언어로 마스터 사이트를 만든 다음 필요한 경우 번역을 사용하여 해당 컨텐츠를 다른 사이트의 기반으로 사용합니다.

* [](/help/sites-administering/translation.md) 마스터 사이트를 다른 언어로 번역합니다.

* [다중 사이트 관리자](/help/sites-administering/msm.md)를 사용하여 다음을 수행할 수 있습니다.

   * 다른 국가 및 문화권 사이트를 만들려면 마스터 사이트 및 번역의 콘텐츠를 다시 사용합니다.
   * Multi Site Manager의 사용을 국가 사이트의 영어 마스터 -> 영어 분기, 국가 사이트의 프랑스어 마스터 -> 프랑스어 언어 분기 등 한 언어 내의 컨텐츠로 제한해야 합니다.
   * 필요한 경우 Live Copy의 요소를 분리하여 현지화 세부 사항을 추가합니다.

다음 다이어그램은 기본 개념이 어떻게 교차하는지를 보여줍니다(하지만 관련된 모든 수준/요소는 표시되지 않음).

![chlimage_1-71](assets/chlimage_1-71a.png)

>[!NOTE]
>
>이 경우 비교 가능한 시나리오 MSM은 이와 같은 서로 다른 언어 버전을 관리하지 않습니다.
>
>* [](/help/sites-administering/msm.md) MSM은 언어의 경계 내에서 블루프린트(예: 전역 마스터)에서 라이브 카피(예: 로컬 사이트)로 번역된 컨텐츠의 배포를 관리합니다.
>* AEM의 [번역](/help/sites-administering/translation.md) 통합 기능은 타사 번역 관리 서비스와 함께 언어를 관리하고 컨텐츠를 이러한 다른 언어로 번역할 수 있습니다.
>
>고급 사용 사례를 위해 MSM은 언어 마스터에서 사용할 수도 있습니다.

>[!NOTE]
>
>모든 사용 사례에 대해 다음 우수 사례를 읽는 것이 좋습니다.
>
>* [MSM에 대한 우수 사례](/help/sites-administering/msm-best-practices.md);특히
>
>   * [사이트 만들기](/help/sites-administering/msm-best-practices.md#create-site)
>   * [MSM 및 다국어 웹 사이트](/help/sites-administering/msm-best-practices.md#msm-and-multilingual-websites)
>* [번역 우수 사례](/help/sites-administering/tc-bp.md)

