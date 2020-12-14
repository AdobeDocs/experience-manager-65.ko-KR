---
title: 프로세스 데이터 제거
seo-title: 프로세스 데이터 제거
description: 오래 지속되는 프로세스를 호출할 때 생성되는 프로세스 데이터는 너무 커서 AEM 양식 성능이 저하되고 불필요한 디스크 공간이 사용될 수 있습니다. 프로세스 데이터를 삭제하는 방법을 참조하십시오.
seo-description: 오래 지속되는 프로세스를 호출할 때 생성되는 프로세스 데이터는 너무 커서 AEM 양식 성능이 저하되고 불필요한 디스크 공간이 사용될 수 있습니다. 프로세스 데이터를 삭제하는 방법을 참조하십시오.
uuid: 2f04452c-71c6-452c-88c2-7560d35e7dec
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_aem_forms_database
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 3157bb92-4b07-40f2-be4c-8f5807f9a380
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '232'
ht-degree: 0%

---


# 프로세스 데이터 {#purging-process-data} 제거

오래 지속되는 프로세스를 호출할 때 생성되는 프로세스 데이터는 너무 커서 AEM 양식 성능이 저하되고 불필요한 디스크 공간이 사용될 수 있습니다. 레코드가 더 이상 필요하지 않을 때 프로세스 데이터를 삭제하는 것이 좋습니다. AEM 양식은 다음과 같은 다양한 처리 데이터 제거 방법을 제공합니다.

* 관리 콘솔을 사용하여 오래 지속되는 프로세스와 관련된 오래된 레코드의 일회성 삭제를 수행하거나 정기적으로 자동 삭제를 예약할 수 있습니다. 자세한 내용은 작업 관리자 데이터베이스[에서 레코드 제거를 참조하십시오.](/help/forms/using/admin-help/purge-records-job-manager-database.md#purge-records-from-the-job-manager-database)
* AEM 양식 Java API 및 웹 서비스 API를 사용하여 장기간 처리 프로세스와 관련된 프로세스 데이터를 프로그래밍 방식으로 삭제할 수 있습니다. (AEM 양식[과 함께 프로그래밍의 &quot;프로세스 데이터 제거&quot;를 참조하십시오.)](https://www.adobe.com/go/learn_aemforms_programming_63)
* 프로세스 삭제 도구를 사용하여 프로세스 이름 및 기타 매개 변수에 따라 프로세스를 삭제합니다. 자세한 내용은 *[aem_forms 루트]*\sdk\misc\Foundation\ProcessPurgeTool\ReadMe.txt에 있는 프로세스 제거 도구 읽어보기 파일을 참조하십시오.

