---
title: 워크플로우 작업
description: Adobe Experience Manager의 워크플로에서는 페이지나 에셋에서 수행되는 일련의 단계들을 자동화할 수 있습니다.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
exl-id: 7383d590-c6b7-440a-a33d-196dce9736ef
solution: Experience Manager, Experience Manager Sites
feature: Authoring,Workflow
role: User,Admin,Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: c45915cf-e157-4af7-a80d-97b905bcb3a5
    internal-label: Experience Manager Sites
feature_v2:
  - id: e2c1b6d3-bb7e-4fe8-8c72-f7b403298e91
    internal-label: Authoring
  - id: f6a6f91a-8819-530a-8e7b-c50884a25aef
    internal-label: Workflow
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 751e1826ed53df7522418e50a206f0fe622256a4
workflow-type: tm+mt
source-wordcount: '178'
ht-degree: 74%
---
# 워크플로우 작업{#working-with-workflows}

AEM 워크플로에서는 (하나 이상의) 페이지 및/또는 에셋에서 수행되는 일련의 단계들을 자동화할 수 있습니다.

예를 들어 편집자는 게시할 때 사이트 관리자가 페이지를 활성화하기 전에 콘텐츠를 검토해야 합니다. 이 예제를 자동화하는 워크플로는 필요한 작업을 수행할 때가 되면 각 참가자에게 알립니다.

1. 작성자는 페이지에 이 워크플로를 적용합니다.
1. 편집자는 페이지 콘텐츠를 검토해야 함을 나타내는 작업 항목을 수신합니다. 완료되면 작업 항목이 완료되었음을 나타냅니다.
1. 그러면 사이트 관리자는 페이지 활성화를 요청하는 작업 항목을 수신합니다. 완료되면 작업 항목이 완료되었음을 나타냅니다.

일반적으로 다음이 진행됩니다.

* 콘텐츠 작성자는 페이지에 워크플로를 적용하고 워크플로에 참여합니다.
* 사용하는 워크플로는 조직의 비즈니스 프로세스마다 고유합니다.

다음 페이지에 이 내용이 나와 있습니다.

* [페이지에 워크플로 적용](/help/sites-authoring/workflows-applying.md)
* [워크플로에 참여](/help/sites-authoring/workflows-participating.md)
