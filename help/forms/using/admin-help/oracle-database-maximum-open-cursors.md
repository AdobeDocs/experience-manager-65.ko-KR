---
title: Oracle 데이터베이스 최대 열린 커서 임계값
description: oracle에서 열린 커서의 최대값을 구성하는 방법에 대해 알아봅니다.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_aem_forms_database
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 5be26485-afe5-47ac-918c-e2fff4f394b2
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: e821be5233fd5f6688507096790d219d25903892
workflow-type: tm+mt
source-wordcount: '82'
ht-degree: 0%

---

# Oracle 데이터베이스 최대 열린 커서 임계값 {#oracle-database-maximum-open-cursors-threshold}

oracle의 열린 커서에 대한 최대값을 구성하려면 이 값을 응용 프로그램에 적합한 숫자로 조정해야 할 수 있습니다. 중간 부하 하에서 열린 평균 커서는 2700개임이 분명하다. 3000의 상한으로 시작하는 것이 좋습니다. 자세한 내용을 보려면 [https://www.orafaq.com/node/758](https://www.orafaq.com/node/758).
