---
title: 유지 관리 모드에서 AEM Forms 실행
description: 유지 관리 모드는 DSC 패치, AEM Forms 업그레이드, 서비스 팩 적용과 같은 작업을 수행할 때 유용합니다. 유지 관리 모드에서 AEM Forms를 실행하는 방법을 자세히 알아봅니다.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_aem_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 6f5ce18b-26b4-4c31-b48a-43ccbb3912f6
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: e821be5233fd5f6688507096790d219d25903892
workflow-type: ht
source-wordcount: '256'
ht-degree: 100%

---

# 유지 관리 모드에서 AEM Forms 실행 {#running-aem-forms-in-maintenance-mode}

유지 관리 모드는 DSC 패치, AEM Forms 업그레이드, 서비스 팩 적용과 같은 작업을 수행할 때 유용합니다.

서버가 유지 관리 모드에 있는 동안에는 어떠한 프로세스도 호출하지 마십시오. 서버가 유지 관리 모드에 있는 동안 프로세스가 호출되면 다음과 같은 일이 발생합니다.

* 장기 프로세스의 경우 작업 데이터베이스에 추가되지만 시작되지는 않습니다. 유지 관리 모드를 종료하면 AEM Forms는 유지 관리 모드 중에 서버가 다시 시작된 경우에도 대기열에 있는 장기 작업을 처리합니다.
* 단기 프로세스라면 즉시 처리됩니다.

**AEM Forms를 유지 관리 모드로 전환**

1. 웹 브라우저에서 다음을 입력합니다.

   `https://[hostname]:[port]/dsc/servlet/DSCStartupServlet?maintenanceMode=pause&user=[administrator username]&password=[password]`

   브라우저 창에 &#39;현재 일시 중지됨&#39;이라는 메시지가 표시됩니다.

   >[!NOTE]
   >
   >유지 관리 모드 중에 서버를 종료하면 다시 시작해도 여전히 유지 관리 모드 상태입니다. 유지 관리 작업이 끝나면 유지 관리 모드를 끄십시오.

**AEM Forms가 유지 관리 모드에서 실행 중인지 확인**

1. 웹 브라우저에서 다음을 입력합니다.

   `https://[hostname]:[port]/dsc/servlet/DSCStartupServlet?maintenanceMode=isPaused&user=[administrator username]&password=[password]`

   브라우저 창에 상태가 표시됩니다. &#39;true&#39; 상태는 서버가 유지 관리 모드에서 실행 중임을 나타내고 &#39;false&#39; 상태는 서버가 유지 관리 모드가 아님을 나타냅니다.

**유지 관리 모드 끄기**

1. 웹 브라우저에서 다음을 입력합니다.

   `https://[hostname]:[port]/dsc/servlet/DSCStartupServlet?maintenanceMode=resume&user=[administrator username]&password=[password]`

   브라우저 창에 &#39;현재 실행 중&#39;이라는 메시지가 표시됩니다.
