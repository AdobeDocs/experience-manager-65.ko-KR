---
title: AdministrationConsole 실행 시 고려 사항
seo-title: AdministrationConsole 실행 시 고려 사항
description: 이 문서에서는 관리 콘솔을 실행할 때 고려해야 할 몇 가지 사항을 나열합니다.
seo-description: 이 문서에서는 관리 콘솔을 실행할 때 고려해야 할 몇 가지 사항을 나열합니다.
uuid: e260f187-4728-44f3-a5c1-7388ff3965c4
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_application_server
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 525c4afc-e109-4546-b78c-1efee63edc43
exl-id: e15dae6f-d30d-4770-a5ca-34f522a01d31
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '146'
ht-degree: 0%

---

# 관리 콘솔 {#considerations-when-running-administrationconsole} 실행 시 고려 사항

다음은 관리 콘솔을 실행할 때 고려해야 할 몇 가지 사항입니다.

* URL `https://[hostname]:'port'/adminui`을 사용하여 관리 콘솔에 액세스하면 지정된 호스트 이름에 밑줄 문자를 사용할 수 없습니다. 그렇지 않으면 관리 콘솔의 일부 영역에 대한 링크가 제대로 작동하지 않을 수 있습니다.
* 일본어 OS에서 Windows 탐색기에서 관리 콘솔을 실행하는 경우 다음 문제를 해결할 수 있습니다.

   * 링크를 클릭하면 예상되는 링크 대신 로그인 페이지로 돌아갑니다.
   * 링크를 클릭하면 권한 오류가 표시됩니다.

   우수 사례는 링크가 실패하지 않도록 Mozilla Firefox와 같은 다른 브라우저에서 관리 콘솔을 실행하는 것입니다.

* 관리 콘솔에서 검색을 수행할 때 백슬래시 문자()를 사용하지 마십시오.
