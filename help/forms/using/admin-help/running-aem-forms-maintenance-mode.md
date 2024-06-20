---
title: 유지 관리 모드에서 AEM Forms 실행
description: 유지 관리 모드는 DSC 패치, AEM Forms 업그레이드 또는 서비스 팩 적용과 같은 작업을 수행할 때 유용합니다. 유지 관리 모드에서 AEM Forms를 실행하는 방법에 대해 자세히 알아보십시오.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_aem_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 6f5ce18b-26b4-4c31-b48a-43ccbb3912f6
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: e821be5233fd5f6688507096790d219d25903892
workflow-type: tm+mt
source-wordcount: '256'
ht-degree: 0%

---

# 유지 관리 모드에서 AEM Forms 실행 {#running-aem-forms-in-maintenance-mode}

유지 관리 모드는 DSC 패치, AEM Forms 업그레이드 또는 서비스 팩 적용과 같은 작업을 수행할 때 유용합니다.

서버가 유지 관리 모드에 있는 동안 프로세스를 호출하지 마십시오. 서버가 유지 관리 모드에 있는 동안 프로세스가 호출되면 다음과 같은 결과가 발생합니다.

* 프로세스가 오래 지속되는 경우 작업 데이터베이스에 추가되지만 시작되지 않습니다. 유지 관리 모드를 종료하면 유지 관리 모드에서 서버를 다시 시작한 경우에도 AEM Forms는 해당 대기열에서 장기 작업을 처리합니다.
* 그 과정이 짧으면 바로 처리된다.

**AEM 양식을 유지 관리 모드로 설정**

1. 웹 브라우저에서 다음을 입력합니다.

   `https://[hostname]:[port]/dsc/servlet/DSCStartupServlet?maintenanceMode=pause&user=[administrator username]&password=[password]`

   브라우저 창에 &quot;일시 중지됨&quot; 메시지가 표시됩니다.

   >[!NOTE]
   >
   >유지 관리 모드일 때 서버를 종료해도 다시 시작할 때 유지 관리 모드입니다. 유지 관리 작업을 마치면 유지 관리 모드를 해제합니다.

**AEM Forms가 유지 관리 모드에서 실행되고 있는지 확인**

1. 웹 브라우저에서 다음을 입력합니다.

   `https://[hostname]:[port]/dsc/servlet/DSCStartupServlet?maintenanceMode=isPaused&user=[administrator username]&password=[password]`

   브라우저 창에 상태가 표시됩니다. 상태가 &quot;true&quot;이면 서버가 유지 관리 모드에서 실행 중이고 &quot;false&quot;이면 서버가 유지 관리 모드가 아닙니다.

**유지 관리 모드 끄기**

1. 웹 브라우저에서 다음을 입력합니다.

   `https://[hostname]:[port]/dsc/servlet/DSCStartupServlet?maintenanceMode=resume&user=[administrator username]&password=[password]`

   브라우저 창에 &quot;지금 실행 중&quot; 메시지가 표시됩니다.
