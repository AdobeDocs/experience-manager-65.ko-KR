---
title: MySQL용 6.5.12.0으로 업그레이드하는 동안 데이터베이스를 백업하지 못했습니다.
description: 사용자가 Experience Manager 6.5.12.0으로 업그레이드하고 "MySQL 업그레이드"를 클릭하면 구성 관리자가 이전 Experience Manager Forms 데이터베이스를 백업하지 못합니다.
exl-id: 1af000fa-439b-4ffd-8b5a-3ba45f0c524c
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,AEM Forms on JEE
role: User, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: 94663796-0ee7-58b9-84f4-b425ebb69e83
    internal-label: AEM Forms on JEE
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '102'
ht-degree: 11%
---
# MySQL 6.5.12.0으로 업그레이드하는 동안 데이터베이스 백업 실패 {#issue}

사용자가 Experience Manager 6.5.12.0(으)로 업그레이드하고 &quot;MySQL 업그레이드&quot;를 클릭하면 구성 관리자가 이전 Experience Manager Forms 데이터베이스를 백업하지 못하고 다음 오류가 표시됩니다.

`Failed to backup the previous Adobe Experience Manager Forms Database`


## 적용 대상 {#applies-to}

* Experience Manager 6.5 Forms

## 솔루션 {#solution}

이 문제를 해결하려면 데이터베이스의 max_packet_size를 100M로 늘리거나 필요에 따라 {AEM_HOME}/mysql에 있는 my.ini 파일에서 늘리십시오.
