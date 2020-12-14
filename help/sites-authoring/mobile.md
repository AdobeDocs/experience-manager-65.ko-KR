---
title: 모바일 장치용 페이지 작성
seo-title: 모바일 장치용 페이지 작성
description: 모바일용으로 작성할 때 몇 개의 에뮬레이터 간을 전환하여 최종 사용자에게 표시되는 내용을 확인할 수 있습니다.
seo-description: 모바일용으로 작성할 때 몇 개의 에뮬레이터 간을 전환하여 최종 사용자에게 표시되는 내용을 확인할 수 있습니다.
uuid: a7a1ba68-d608-4819-88d1-0dab5955d3f4
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
discoiquuid: 9554cdb3-b604-4d50-9760-89b9e7a7755f
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '247'
ht-degree: 89%

---


# 모바일 장치용 페이지 작성{#authoring-a-page-for-mobile-devices}

모바일 페이지를 작성할 때는 모바일 장치를 에뮬레이션하는 방식으로 페이지가 표시됩니다. 페이지를 작성할 때에는 몇 개의 에뮬레이터 간을 전환하여 페이지에 액세스할 때 최종 사용자에게 표시되는 내용을 확인할 수 있습니다.

장치는 페이지를 렌더링할 장치의 기능에 따라 카테고리 기능, 스마트와 터치로 그룹화됩니다. 최종 사용자가 모바일 페이지에 액세스하면 AEM이 장치를 감지하여 장치 그룹에 해당하는 표현 데이터를 전송합니다.

>[!NOTE]
>
>기존 표준 사이트를 기반으로 모바일 사이트를 만들려면 표준 사이트의 Live Copy를 만드십시오. ([다른 채널에 대한 Live Copy 만들기](/help/sites-administering/msm-livecopy.md)를 참조하십시오.)
>
>AEM 개발자는 새 장치 그룹을 만들 수 있습니다. ([장치 그룹 필터 만들기](/help/sites-developing/groupfilters.md)를 참조하십시오.)

다음 절차를 사용하여 모바일 페이지를 작성하십시오.

1. 전역 탐색에서 **Sites** 콘솔을 엽니다.
1. **We.Retail** -> **미국** -> **영어** 페이지를 엽니다.

1. **미리 보기** 모드로 전환합니다.
1. 페이지 맨 위에서 장치 아이콘을 클릭하여 원하는 에뮬레이터로 전환합니다.
1. 구성 요소 브라우저에 있는 구성 요소를 페이지에 드래그하여 놓습니다.

페이지 모습은 다음과 유사합니다.

![mobileipadum](assets/mobileipademu.png)

>[!NOTE]
>
>모바일 장치에서 작성 인스턴스의 페이지를 요청하면 에뮬레이터가 비활성화됩니다.

