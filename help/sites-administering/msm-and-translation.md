---
title: 다중 사이트 관리자 및 번역
description: 프로젝트 간 콘텐츠를 재사용하고 Adobe Experience Manager에서 다국어 웹 사이트를 관리하는 방법을 알아봅니다.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: site-features
content-type: reference
exl-id: 8f11f5de-f5af-4ce7-a448-2b4299de2930
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '365'
ht-degree: 33%

---

# 다중 사이트 관리자 및 번역 {#msm-and-translation}

웹 사이트 및 페이지 관리에 다음 관리 도구를 사용할 수 있습니다.

* MSM(다중 사이트 관리자)을 사용하면 여러 위치에서 동일한 사이트 콘텐츠를 사용할 수 있지만 변형은 가능합니다.

   * [콘텐츠 재사용: 다중 사이트 관리자 및 Live Copy](/help/sites-administering/msm.md)

* 번역을 사용하면 페이지 콘텐츠, 에셋 및 사용자 생성 콘텐츠의 번역을 자동화하여 다국어 웹 사이트를 만들고 관리할 수 있습니다.

   * [다국어 사이트를 위한 콘텐츠 번역](/help/sites-administering/translation.md)

* 이 두 가지 기능을 결합하여 두 웹 사이트를 모두 지원할 수 있습니다. [다국적 및 다국어](#multinational-and-multilingual-sites).

## 다국적 및 다국어 사이트 {#multinational-and-multilingual-sites}

다중 사이트 관리자 와 번역 워크플로를 결합하여 사용함으로써 다국적 및 다국어 사이트를 위한 콘텐츠를 효율적으로 만들 수 있습니다. 특정 국가에 대해 하나의 언어로 마스터 사이트를 만든 다음 필요한 경우 번역을 사용하여 해당 콘텐츠를 다른 사이트의 기초로 사용합니다.

* 마스터 사이트를 다른 언어로 [번역](/help/sites-administering/translation.md)합니다.

* [다중 사이트 관리자](/help/sites-administering/msm.md)를 사용하여 다음과 같은 작업을 수행합니다.

   * 마스터 사이트의 콘텐츠 및 번역을 다시 사용하여 다른 국가 및 문화에 대한 사이트를 만듭니다.
   * 다중 사이트 관리자의 사용을 한 언어 이내로 제한해야 합니다(예: 국가 사이트의 영어 마스터 > 영어 분기, 국가 사이트의 프랑스어 마스터 > 프랑스어 분기).
   * 필요한 경우 라이브 카피의 요소를 분리하여 현지화 세부 사항을 추가합니다.

다음 다이어그램은 주요 개념이 어떻게 교차하는지를 보여 줍니다(모든 수준/요소를 포함하지는 않음).

![MSM 및 번역의 주요 개념을 보여 주는 다이어그램](assets/chlimage_1-71a.png)

>[!NOTE]
>
>이 시나리오 및 이와 비슷한 시나리오에서 MSM은 이렇게 다양한 언어 버전을 관리하지 않습니다.
>
>* [MSM](/help/sites-administering/msm.md) 는 언어 경계 내에서 블루프린트(예: 글로벌 마스터)에서 라이브 카피(예: 로컬 사이트)로의 번역된 콘텐츠 배포를 관리합니다.
>* AEM의 [번역](/help/sites-administering/translation.md) 통합 기능과 서드파티 번역 관리 서비스는 다양한 언어 및 콘텐츠 번역을 관리합니다.
>
>고급 사용 사례의 경우 여러 언어 마스터에 걸쳐 MSM을 사용할 수도 있습니다.

>[!NOTE]
>
>모든 사용 사례는 다음 모범 사례를 읽어보시기 바랍니다.
>
>* [MSM 모범 사례](/help/sites-administering/msm-best-practices.md); 특히:
>
>   * [사이트 생성](/help/sites-administering/msm-best-practices.md#create-site)
>   * [MSM 및 다국어 웹 사이트](/help/sites-administering/msm-best-practices.md#msm-and-multilingual-websites)
>
>* [번역 모범 사례](/help/sites-administering/tc-bp.md)
