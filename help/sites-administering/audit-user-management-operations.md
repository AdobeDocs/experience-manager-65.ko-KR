---
title: AEM에서 사용자 관리 작업을 감사하는 방법
seo-title: AEM에서 사용자 관리 작업을 감사하는 방법
description: AEM에서 사용자 관리 작업을 감사하는 방법을 알아봅니다.
seo-description: AEM에서 사용자 관리 작업을 감사하는 방법을 알아봅니다.
uuid: 9d177afb-172c-4858-a678-254c97cfa472
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: Security
content-type: reference
discoiquuid: ba6a56e5-b91c-4779-9154-d4300b2827f8
docset: aem65
exl-id: 7a4406c9-2f98-4bf8-b32c-1ec1e7ff36f0
feature: 작업
translation-type: tm+mt
source-git-commit: 9134130f349c6c7a06ad9658a87f78a86b7dbf9c
workflow-type: tm+mt
source-wordcount: '326'
ht-degree: 1%

---

# AEM{#how-to-audit-user-management-operations-in-aem}에서 사용자 관리 작업을 감사하는 방법

## 소개 {#introduction}

AEM에서는 권한 변경 사항을 기록할 수 있는 기능을 도입하여 나중에 감사할 수 있습니다.

향상된 기능을 통해 사용자의 권한 및 그룹 할당에 대한 감사 CRUD(만들기, 읽기, 업데이트, 삭제) 작업을 수행할 수 있습니다. 보다 구체적으로 말하면 다음과 같이 기록됩니다.

* 새 사용자가 만들어집니다.
* 그룹에 추가되는 사용자
* 기존 사용자 또는 그룹의 권한 변경 사항

기본적으로 항목은 `error.log` 파일에 기록됩니다. 모니터링을 쉽게 하려면 별도의 로그 파일로 리디렉션하는 것이 좋습니다. 아래 단락에 있는 이 작업을 수행하는 방법에 대한 자세한 내용을 살펴보십시오.

## 출력을 별도의 로그 파일 {#redirecting-the-output-to-a-separate-log-file}으로 리디렉션합니다.

로깅 출력을 별도의 로그 파일로 리디렉션하려면 새 **Apache Sling 로깅 로거** 구성을 만들어야 합니다. 아래 예에서 개별 파일의 이름으로 `useraudit.log`을 사용합니다.

1. *https://serveraddress:serverport/system/console/configMgr*&#x200B;로 이동하여 웹 콘솔로 이동합니다.
1. **Apache Sling 로깅 로거 구성**&#x200B;을 검색합니다. 그런 다음 항목 오른쪽의 &quot;+&quot;를 눌러 새 공장 구성을 만듭니다.
1. 다음 구성을 만듭니다.

   * **로그 수준:** 정보
   * **로그 파일:** logs/useraudit.log
   * **메시지 패턴:** 레벨 기본값
   * **Logger:** com.adobe.granite.security.user.internal.audit, com.adobe.granite.security.user.internal.servlets.AuthorizableServlet

   두 로거를 **로거** 필드에 모두 입력하려면 첫 번째 이름을 입력한 다음 &quot;+&quot; 버튼을 누르고 두 번째 로거 이름을 입력하여 다른 필드를 만들어야 합니다.

## 출력 예 {#example-output}

올바르게 구성된 경우 출력은 다음과 같아야 합니다.

```xml
19.05.2017 15:15:08.933 *INFO* [0:0:0:0:0:0:0:1 [1495196108932] POST /libs/granite/security/post/authorizables.html HTTP/1.1] com.adobe.granite.security.user.internal.servlets.AuthorizableServlet Create Group 'group1' operation initiated by User 'admin' (administrator)
19.05.2017 15:15:08.934 *INFO* [0:0:0:0:0:0:0:1 [1495196108932] POST /libs/granite/security/post/authorizables.html HTTP/1.1] com.adobe.granite.security.user.internal.audit.AuditAuthorizableAction Group 'group1' was created

19.05.2017 15:16:25.698 *INFO* [0:0:0:0:0:0:0:1 [1495196185696] POST /libs/granite/security/post/authorizables.html HTTP/1.1] com.adobe.granite.security.user.internal.servlets.AuthorizableServlet Create User 'user1' operation initiated by User 'admin' (administrator)
19.05.2017 15:16:25.700 *INFO* [0:0:0:0:0:0:0:1 [1495196185696] POST /libs/granite/security/post/authorizables.html HTTP/1.1] com.adobe.granite.security.user.internal.audit.AuditAuthorizableAction User 'user1' was created

19.05.2017 15:16:25.728 *INFO* [0:0:0:0:0:0:0:1 [1495196185726] POST /home/groups/d/dGf7f7vGrZRLs6HS3AK-.rw.userprops.html HTTP/1.1] com.adobe.granite.security.user.internal.servlets.AuthorizableServlet Edit Membership for Group 'group1' operation initiated by User 'admin' (administrator)
19.05.2017 15:16:25.729 *INFO* [0:0:0:0:0:0:0:1 [1495196185726] POST /home/groups/d/dGf7f7vGrZRLs6HS3AK-.rw.userprops.html HTTP/1.1] com.adobe.granite.security.user.internal.audit.AuditGroupAction User 'user1' was added to the group 'group1'

19.05.2017 15:17:29.830 *INFO* [0:0:0:0:0:0:0:1 [1495196249828] POST /home/users/5/5dI6iK4HkZmrfTjcLBoI.rw.userprops.html HTTP/1.1] com.adobe.granite.security.user.internal.servlets.AuthorizableServlet Password Change for User 'user2' operation initiated by User 'admin' (administrator)
19.05.2017 15:17:29.832 *INFO* [0:0:0:0:0:0:0:1 [1495196249828] POST /home/users/5/5dI6iK4HkZmrfTjcLBoI.rw.userprops.html HTTP/1.1] com.adobe.granite.security.user.internal.audit.AuditAuthorizableAction Password for User 'user2' was changed

19.05.2017 15:17:54.906 *INFO* [0:0:0:0:0:0:0:1 [1495196274904] POST /home/users/5/5dI6iK4HkZmrfTjcLBoI.rw.html HTTP/1.1] com.adobe.granite.security.user.internal.servlets.AuthorizableServlet Delete User 'user2' operation initiated by User 'admin' (administrator)
19.05.2017 15:17:54.906 *INFO* [0:0:0:0:0:0:0:1 [1495196274904] POST /home/users/5/5dI6iK4HkZmrfTjcLBoI.rw.html HTTP/1.1] com.adobe.granite.security.user.internal.audit.AuditAuthorizableAction User 'user2' was removed

19.05.2017 15:19:11.050 *INFO* [0:0:0:0:0:0:0:1 [1495196351049] POST /libs/granite/security/post/authorizables.html HTTP/1.1] com.adobe.granite.security.user.internal.servlets.AuthorizableServlet Create User 'user3' operation initiated by User 'admin' (administrator)
19.05.2017 15:19:11.052 *INFO* [0:0:0:0:0:0:0:1 [1495196351049] POST /libs/granite/security/post/authorizables.html HTTP/1.1] com.adobe.granite.security.user.internal.audit.AuditAuthorizableAction User 'user3' was created
19.05.2017 15:19:36.899 *INFO* [0:0:0:0:0:0:0:1 [1495196376898] POST /home/groups/d/dGf7f7vGrZRLs6HS3AK-.rw.userprops.html HTTP/1.1] com.adobe.granite.security.user.internal.servlets.AuthorizableServlet Edit Membership for Group 'group1' operation initiated by User 'admin' (administrator)

19.05.2017 15:19:36.916 *INFO* [0:0:0:0:0:0:0:1 [1495196376915] POST /home/groups/d/dGf7f7vGrZRLs6HS3AK-.rw.userprops.html HTTP/1.1] com.adobe.granite.security.user.internal.servlets.AuthorizableServlet Edit Membership for Group 'group1' operation initiated by User 'admin' (administrator)
19.05.2017 15:19:36.917 *INFO* [0:0:0:0:0:0:0:1 [1495196376915] POST /home/groups/d/dGf7f7vGrZRLs6HS3AK-.rw.userprops.html HTTP/1.1] com.adobe.granite.security.user.internal.audit.AuditGroupAction User 'user1' was removed from the group 'group1'

19.05.2017 15:21:34.419 *INFO* [0:0:0:0:0:0:0:1 [1495196494417] POST /home/groups/d/dGf7f7vGrZRLs6HS3AK-.rw.html HTTP/1.1] com.adobe.granite.security.user.internal.servlets.AuthorizableServlet Delete Group 'group1' operation initiated by User 'admin' (administrator)
19.05.2017 15:21:34.419 *INFO* [0:0:0:0:0:0:0:1 [1495196494417] POST /home/groups/d/dGf7f7vGrZRLs6HS3AK-.rw.html HTTP/1.1] com.adobe.granite.security.user.internal.audit.AuditAuthorizableAction Group 'group1' was removed

19.05.2017 15:44:10.404 *INFO* [0:0:0:0:0:0:0:1 [1495197850401] POST /home/users/3/35XVpVtLRx4a5J9gKrVG.rw.userprops.html HTTP/1.1] com.adobe.granite.security.user.internal.servlets.AuthorizableServlet Password Change for User 'john' operation initiated by User 'john' (not administrator)
19.05.2017 15:44:10.405 *INFO* [0:0:0:0:0:0:0:1 [1495197850401] POST /home/users/3/35XVpVtLRx4a5J9gKrVG.rw.userprops.html HTTP/1.1] com.adobe.granite.security.user.internal.audit.AuditAuthorizableAction Password for User 'john' was changed
```

## 클래식 UI {#classic-ui}

클래식 UI에서 사용자 추가 및 삭제와 관련하여 감사 로그에 기록된 CRUD 작업에 대한 정보는 영향을 받는 사용자의 ID로 제한되며 변경된 사항이 발생한 경우에 한합니다.

예:

```
10.05.2019 18:01:09.123 INFO [0:0:0:0:0:0:0:1 [1557491469096] POST /libs/cq/security/authorizables/POST HTTP/1.1] com.adobe.granite.security.user.internal.audit.AuditAuthorizableAction User 'test' was created
```
