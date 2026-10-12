---
title: 모바일 장치용 콘텐츠 페이지 작성
description: 모바일용 작성 시 여러 에뮬레이터 간을 전환하여 최종 사용자에게 표시되는 내용을 확인할 수 있습니다.
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
exl-id: 9c6c6386-5ffd-4fa6-9aa1-f5b0e31d1046
solution: Experience Manager, Experience Manager Sites
feature: Authoring
role: User,Admin,Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: c45915cf-e157-4af7-a80d-97b905bcb3a5
    internal-label: Experience Manager Sites
feature_v2:
  - id: e2c1b6d3-bb7e-4fe8-8c72-f7b403298e91
    internal-label: Authoring
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '229'
ht-degree: 63%
---
# 모바일 디바이스용 페이지 작성{#authoring-a-page-for-mobile-devices}

모바일 페이지를 작성할 때는 모바일 디바이스를 에뮬레이션하는 방식으로 페이지가 표시됩니다. 페이지를 작성할 때에는 몇 개의 에뮬레이터 간을 전환하여 페이지에 액세스할 때 최종 사용자에게 표시되는 내용을 확인할 수 있습니다.

디바이스는 페이지를 렌더링할 디바이스의 기능에 따라 카테고리 기능, 스마트와 터치로 그룹화됩니다. 최종 사용자가 모바일 페이지에 액세스하면 AEM이 디바이스를 감지하여 디바이스 그룹에 해당하는 표현 데이터를 전송합니다.

>[!NOTE]
>
>기존 표준 사이트를 기반으로 모바일 사이트를 만들려면 표준 사이트의 Live Copy를 만드십시오. [다른 채널용 Live Copy 만들기](/help/sites-administering/msm-livecopy.md)를 참조하세요.
>
>AEM 개발자는 새 디바이스 그룹을 만들 수 있습니다. [장치 그룹 필터 만들기](/help/sites-developing/groupfilters.md)를 참조하세요.

다음 절차를 사용하여 모바일 페이지를 작성하십시오.

1. 전역 탐색에서 **Sites** 콘솔을 엽니다.
1. **We.Retail** > **미국** > **영어** 페이지를 엽니다.

1. **미리 보기** 모드로 전환합니다.
1. 페이지 맨 위에서 장치 아이콘을 클릭하여 원하는 에뮬레이터로 전환합니다.
1. 구성 요소 브라우저에서 페이지로 구성 요소를 드래그하여 놓습니다.

페이지는 다음과 유사합니다.

![mobileidapdemu](assets/mobileipademu.png)

>[!NOTE]
>
>모바일 디바이스에서 작성 인스턴스의 페이지를 요청하면 에뮬레이터가 비활성화됩니다.
