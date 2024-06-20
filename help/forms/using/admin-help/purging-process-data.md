---
title: 프로세스 데이터 삭제
description: 오래 지속되는 프로세스를 호출할 때 생성되는 프로세스 데이터가 너무 커지면 AEM Forms 성능이 저하되고 불필요한 디스크 공간이 사용될 수 있습니다. 프로세스 데이터를 삭제하는 방법을 확인하십시오.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_aem_forms_database
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 0da59dbe-f050-4ee5-b74c-4380b3543b97
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: e821be5233fd5f6688507096790d219d25903892
workflow-type: tm+mt
source-wordcount: '187'
ht-degree: 0%

---

# 프로세스 데이터 삭제 {#purging-process-data}

오래 지속되는 프로세스를 호출할 때 생성되는 프로세스 데이터가 너무 커지면 AEM Forms 성능이 저하되고 불필요한 디스크 공간이 사용될 수 있습니다. 레코드가 더 이상 필요하지 않은 경우 프로세스 데이터를 제거하는 것이 좋습니다. AEM forms는 프로세스 데이터를 삭제하는 여러 가지 방법을 제공합니다.

* 관리 콘솔을 사용하여 장기 보존된 프로세스와 관련된 오래된 레코드를 한 번 제거하거나, 정기적인 자동 제거를 예약합니다. (참조: [작업 관리자 데이터베이스에서 레코드 제거](/help/forms/using/admin-help/purge-records-job-manager-database.md#purge-records-from-the-job-manager-database).)
* AEM Forms Java API 및 웹 서비스 API를 사용하여 수명이 긴 프로세스와 관련된 프로세스 데이터를 프로그래밍 방식으로 제거할 수 있습니다. (&quot;프로세스 데이터 제거&quot; 참조) [AEM Forms를 사용한 프로그래밍](https://www.adobe.com/go/learn_aemforms_programming_63).)
* 프로세스 삭제 도구를 사용하여 프로세스 이름과 기타 매개변수를 기준으로 프로세스를 삭제합니다. 자세한 내용은 프로세스 제거 도구 추가 정보 파일을 참조하십시오. *[aem_forms 루트]*\sdk\misc\Foundation\ProcessPurgeTool\ReadMe.txt입니다.
