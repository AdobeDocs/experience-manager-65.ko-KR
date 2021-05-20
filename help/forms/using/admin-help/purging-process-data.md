---
title: 프로세스 데이터 삭제
seo-title: 프로세스 데이터 삭제
description: 장기간 프로세스가 호출될 때 생성되는 프로세스 데이터는 너무 커져서 AEM Forms 성능이 저하되고 불필요한 디스크 공간이 사용될 수 있습니다. 프로세스 데이터를 삭제하는 방법을 참조하십시오.
seo-description: 장기간 프로세스가 호출될 때 생성되는 프로세스 데이터는 너무 커져서 AEM Forms 성능이 저하되고 불필요한 디스크 공간이 사용될 수 있습니다. 프로세스 데이터를 삭제하는 방법을 참조하십시오.
uuid: 2f04452c-71c6-452c-88c2-7560d35e7dec
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_aem_forms_database
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 3157bb92-4b07-40f2-be4c-8f5807f9a380
exl-id: 0da59dbe-f050-4ee5-b74c-4380b3543b97
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '232'
ht-degree: 0%

---

# 프로세스 데이터 삭제 {#purging-process-data}

장기간 프로세스가 호출될 때 생성되는 프로세스 데이터는 너무 커져서 AEM Forms 성능이 저하되고 불필요한 디스크 공간이 사용될 수 있습니다. 레코드가 더 이상 필요하지 않은 경우 프로세스 데이터를 삭제하는 것이 좋습니다. AEM Forms는 프로세스 데이터를 삭제하는 몇 가지 방법을 제공합니다.

* 관리 콘솔을 사용하여 장기 처리 프로세스와 관련된 오래된 레코드를 일회성 삭제하거나 일반 자동 삭제를 스케줄링할 수 있습니다. ([작업 관리자 데이터베이스에서 레코드 제거](/help/forms/using/admin-help/purge-records-job-manager-database.md#purge-records-from-the-job-manager-database)를 참조하십시오.)
* AEM Forms Java API 및 웹 서비스 API를 사용하여 긴 기간 프로세스와 관련된 프로세스 데이터를 프로그래밍 방식으로 제거할 수 있습니다. ([AEM Forms를 사용한 프로그래밍에서 &quot;프로세스 데이터 제거&quot;를 참조하십시오.)](https://www.adobe.com/go/learn_aemforms_programming_63)
* 프로세스 이름 및 기타 매개변수에 따라 프로세스를 삭제하려면 프로세스 삭제 도구를 사용합니다. 자세한 내용은 *[aem_forms root]*\sdk\misc\Foundation\ProcessPurgeTool\ReadMe.txt에 있는 프로세스 삭제 도구 추가 정보 파일을 참조하십시오.
