---
title: 유지 관리 모드에서 AEM 양식 실행
seo-title: 유지 관리 모드에서 AEM 양식 실행
description: 유지 관리 모드는 DSC 패치 적용, AEM 양식 업그레이드 또는 서비스 팩 적용과 같은 작업을 수행할 때 유용합니다. 유지 관리 모드에서 AEM 양식 실행에 대한 자세한 내용을 살펴보십시오.
seo-description: 유지 관리 모드는 DSC 패치 적용, AEM 양식 업그레이드 또는 서비스 팩 적용과 같은 작업을 수행할 때 유용합니다. 유지 관리 모드에서 AEM 양식 실행에 대한 자세한 내용을 살펴보십시오.
uuid: 9aa3be20-f17e-4384-b4ce-daaee2898c96
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_aem_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 94047c12-ba3d-457a-954f-e035c7cc3ecd
translation-type: tm+mt
source-git-commit: 317fadfe48724270e59644d2ed9a90fbee95cf9f
workflow-type: tm+mt
source-wordcount: '294'
ht-degree: 0%

---


# 유지 관리 모드에서 AEM 양식 실행 {#running-aem-forms-in-maintenance-mode}

유지 관리 모드는 DSC 패치 적용, AEM 양식 업그레이드 또는 서비스 팩 적용과 같은 작업을 수행할 때 유용합니다.

서버가 유지 관리 모드에 있는 동안에는 모든 프로세스를 호출하지 마십시오. 서버가 유지 관리 모드에 있는 동안 프로세스가 호출되면 다음과 같이 됩니다.

* 프로세스가 오래 지속되는 경우 작업 데이터베이스에 추가되지만 시작되지 않습니다. 유지 관리 모드를 종료하면 유지 관리 모드에서 서버를 다시 시작하더라도 AEM 양식은 대기열에서 긴 작업을 처리합니다.
* 프로세스가 짧으면 즉시 처리됩니다.

**유지 관리 모드에서 AEM 양식 삽입**

1. 웹 브라우저에서 다음을 입력합니다.

   `https://[hostname]:[port]/dsc/servlet/DSCStartupServlet?maintenanceMode=pause&user=[administrator username]&password=[password]`

   브라우저 창에 &quot;이제 일시 중지됨&quot; 메시지가 표시됩니다.

   >[!NOTE]
   >
   >유지 관리 모드인 상태에서 서버를 종료하면 서버를 다시 시작할 때 유지 관리 모드가 계속 됩니다. 유지 관리 작업이 끝나면 유지 관리 모드를 해제해야 합니다.

**AEM 양식이 유지 관리 모드에서 실행 중인지 확인**

1. 웹 브라우저에서 다음을 입력합니다.

   `https://[hostname]:[port]/dsc/servlet/DSCStartupServlet?maintenanceMode=isPaused&user=[administrator username]&password=[password]`

   브라우저 창에 상태가 표시됩니다. 상태가 &quot;true&quot;이면 서버가 유지 관리 모드에서 실행 중임을 나타내고, &quot;false&quot;는 서버가 유지 관리 모드가 아님을 나타냅니다.

**유지 관리 모드 해제**

1. 웹 브라우저에서 다음을 입력합니다.

   `https://[hostname]:[port]/dsc/servlet/DSCStartupServlet?maintenanceMode=resume&user=[administrator username]&password=[password]`

   &quot;지금 실행 중&quot; 메시지가 브라우저 창에 표시됩니다.

