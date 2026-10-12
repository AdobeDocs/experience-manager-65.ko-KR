---
title: Administration Console 실행 시 고려 사항
description: 이 문서에는 Administration Console을 실행할 때 고려해야 할 몇 가지 사항이 나와 있습니다.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_application_server
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: e15dae6f-d30d-4770-a5ca-34f522a01d31
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '147'
ht-degree: 8%
---
# Administration Console 실행 시 고려 사항 {#considerations-when-running-administrationconsole}

>[!NOTE]
> 
> 사용자에게 관리자 콘솔에 액세스할 수 있는 관리자 권한이 있는지 확인하십시오.

다음은 관리 콘솔을 실행할 때 고려해야 할 몇 가지 사항입니다.

* URL `https://[hostname]:'port'/adminui`을(를) 사용하여 관리 콘솔에 액세스하는 경우 지정된 호스트 이름에는 밑줄 문자를 사용할 수 없습니다. 그렇지 않으면 관리 콘솔의 일부 영역에 대한 링크가 제대로 작동하지 않을 수 있습니다.
* 일본어 OS의 Windows 탐색기에서 관리 콘솔을 실행하는 경우 다음과 같은 문제가 발생할 수 있습니다.

  * 링크를 클릭하면 예상 링크가 아닌 로그인 페이지로 돌아갑니다.
  * 링크를 클릭하면 권한 오류가 표시됩니다.

  가장 좋은 방법은 링크가 실패하지 않도록 Mozilla Firefox와 같은 다른 브라우저에서 관리 콘솔을 실행하는 것입니다.

* 관리 콘솔에서 검색을 수행할 때는 백슬래시 문자()를 사용하지 마십시오.
