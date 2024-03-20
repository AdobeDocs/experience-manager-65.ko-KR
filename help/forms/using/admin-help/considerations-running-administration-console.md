---
title: Administration Console 실행 시 고려 사항
description: 이 문서에는 Administration Console을 실행할 때 고려해야 할 몇 가지 사항이 나와 있습니다.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_application_server
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: e15dae6f-d30d-4770-a5ca-34f522a01d31
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '135'
ht-degree: 0%

---

# Administration Console 실행 시 고려 사항 {#considerations-when-running-administrationconsole}

다음은 관리 콘솔을 실행할 때 고려해야 할 몇 가지 사항입니다.

* URL을 사용하여 관리 콘솔에 액세스하는 경우 `https://[hostname]:'port'/adminui`, 지정된 호스트 이름에는 밑줄 문자를 사용할 수 없습니다. 그렇지 않으면 관리 콘솔의 일부 영역에 대한 링크가 제대로 작동하지 않을 수 있습니다.
* 일본어 OS의 Windows 탐색기에서 관리 콘솔을 실행하는 경우 다음과 같은 문제가 발생할 수 있습니다.

   * 링크를 클릭하면 예상 링크가 아닌 로그인 페이지로 돌아갑니다.
   * 링크를 클릭하면 권한 오류가 표시됩니다.

  가장 좋은 방법은 링크가 실패하지 않도록 Mozilla Firefox와 같은 다른 브라우저에서 관리 콘솔을 실행하는 것입니다.

* 관리 콘솔에서 검색을 수행할 때는 백슬래시 문자()를 사용하지 마십시오.
