---
title: 프로세스 데이터 제거
description: 장기 프로세스를 호출할 때 생성되는 프로세스 데이터는 너무 커질 수 있으며, 이로 인해 AEM Forms 성능이 저하되고 불필요한 디스크 공간이 사용됩니다. 프로세스 데이터를 제거하는 방법을 살펴보십시오.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_aem_forms_database
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 0da59dbe-f050-4ee5-b74c-4380b3543b97
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 6a9806d8f40f711a610c130c63d9ab9b2460d075
workflow-type: ht
source-wordcount: '199'
ht-degree: 100%

---

# 프로세스 데이터 제거 {#purging-process-data}

>[!NOTE]
> 
> 사용자에게 관리자 콘솔에 액세스할 수 있는 관리자 권한이 있는지 확인하십시오.

장기 프로세스를 호출할 때 생성되는 프로세스 데이터는 너무 커질 수 있으며, 이로 인해 AEM Forms 성능이 저하되고 불필요한 디스크 공간이 사용됩니다. 더 이상 레코드가 필요하지 않으면 프로세스 데이터를 제거하는 것이 좋습니다. AEM Forms는 프로세스 데이터를 제거하는 여러 가지 방법을 제공합니다.

* 관리 콘솔을 사용하여 장기 프로세스와 관련된 더 이상 사용되지 않는 레코드를 한 번만 제거하거나 정기 자동 제거를 예약할 수 있습니다. ([작업 관리자 데이터베이스에서 레코드 제거](/help/forms/using/admin-help/purge-records-job-manager-database.md#purge-records-from-the-job-manager-database)를 참조하십시오.)
* AEM Forms Java API와 웹 서비스 API를 사용하면 장기 프로세스와 관련된 프로세스 데이터를 프로그래밍 방식으로 제거할 수 있습니다. ([AEM Forms를 사용한 프로그래밍](https://www.adobe.com/go/learn_aemforms_programming_63)의 &#39;프로세스 데이터 제거&#39;를 참조하십시오.)
* 프로세스 제거 도구를 사용하여 프로세스 이름과 기타 매개변수를 기준으로 프로세스를 제거합니다. 자세한 내용은 *[aem_forms root]*\sdk\misc\Foundation\ProcessPurgeTool\ReadMe.txt에 있는 프로세스 제거 도구 추가 정보 파일을 참조하십시오.
