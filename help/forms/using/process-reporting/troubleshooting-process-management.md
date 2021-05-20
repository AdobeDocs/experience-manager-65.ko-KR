---
title: 프로세스 보고 문제 해결
seo-title: 프로세스 보고 문제 해결
description: JEE 프로세스 보고에서 AEM Forms의 문제 해결
seo-description: JEE 프로세스 보고에서 AEM Forms의 문제 해결
page-status-flag: de-activated
uuid: 1c1cc27c-fbed-4366-bffe-e1581d269a93
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 0a818d19-8804-4c69-b721-31c347c593c0
exl-id: 165d4c69-d7ca-45f8-a9de-764cb8ecab7e
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '116'
ht-degree: 0%

---

# 프로세스 보고 문제 해결 {#troubleshooting-process-reporting}

## Microsoft Windows 7에서 Internet Explorer 9에서 필터를 만들 때 발생하는 문제 {#issues-faced-in-creating-filters-on-internet-explorer-on-microsoft-windows}

사전 정의된 보고서에 대한 필터를 만드는 경우 **Internet Explorer 9** Microsoft Windows 7 **환경에 대해 간헐적으로 다음 문제가 발생합니다.**

* 값 필드의 드롭다운 목록에는 값 대신 고유 식별자가 표시됩니다.
* 값 필드의 Calendar 컨트롤에는 일본어 문자가 표시됩니다.
* 조건 필드가 표시되지 않습니다.
* 값 필드의 Calendar 컨트롤이 표시되지 않습니다.

### 해상도 {#resolution}

프로세스 보고에 여전히 로그인되어 있는 동안:

1. 브라우저 캐시를 지웁니다.
1. 브라우저 화면을 새로 고칩니다.
