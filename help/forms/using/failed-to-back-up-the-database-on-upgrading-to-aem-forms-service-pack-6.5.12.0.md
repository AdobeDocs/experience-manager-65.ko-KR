---
title: MySQL용 6.5.12.0으로 업그레이드하는 동안 데이터베이스를 백업하지 못했습니다.
description: 사용자가 Experience Manager 6.5.12.0으로 업그레이드하고 "MySQL 업그레이드"를 클릭하면 구성 관리자가 이전 Experience Manager Forms 데이터베이스를 백업하지 못합니다.
source-git-commit: bf974331157e21b28c0daa5b878ac927ce5a2304
workflow-type: tm+mt
source-wordcount: '106'
ht-degree: 0%

---

# MySQL용 6.5.12.0으로 업그레이드하는 동안 데이터베이스 백업 실패(#issue)

사용자가 Experience Manager 6.5.12.0으로 업그레이드하고 &quot;MySQL 업그레이드&quot;를 클릭하면 구성 관리자가 이전 Experience Manager Forms 데이터베이스를 백업하지 못하고 다음과 같은 오류가 표시됩니다.

`Failed to backup the previous Adobe Experience Manager Forms Database`


## 적용 대상 {#applies-to}

* Experience Manager 6.5 Forms

## 솔루션 {#solution}

이 문제를 해결하려면 데이터베이스의 max_packet_size를 100M로 늘리거나 다음에 있는 my.ini 파일에서 필요에 따라 늘리십시오. {AEM_HOME}/mysql.
