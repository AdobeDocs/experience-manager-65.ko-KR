---
title: Oracle 데이터베이스 최대 열린 커서 임계값
seo-title: Oracle database maximum open cursors threshold
description: oracle에서 열린 커서에 대한 최대 값 구성에 대해 알아봅니다.
seo-description: Learn about configuring a maximum value for open cursors in Oracle.
uuid: c1d20997-f853-4772-b1c6-8cea73221d0a
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_aem_forms_database
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: d3565776-1b7d-498c-9840-b17f80170d9b
exl-id: 5be26485-afe5-47ac-918c-e2fff4f394b2
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '84'
ht-degree: 0%

---

# Oracle 데이터베이스 최대 열린 커서 임계값 {#oracle-database-maximum-open-cursors-threshold}

oracle에서 열린 커서에 대한 최대 값을 구성하려면 이 값을 애플리케이션에 적합한 숫자로 조정해야 할 수 있습니다. 적당한 부하에, 열린 평균 커서는 2700이었다는 것이 명백합니다. 를 상한 3000으로 시작하는 것이 좋습니다. 자세한 내용을 보려면 [https://www.orafaq.com/node/758](https://www.orafaq.com/node/758).
