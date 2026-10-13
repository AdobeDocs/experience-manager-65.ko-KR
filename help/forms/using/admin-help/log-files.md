---
title: 로그 파일
description: 런타임 오류나 시작 오류와 같은 이벤트는 애플리케이션 서버 로그 파일에 기록되며, 이 로그 파일은 모든 텍스트 편집기를 사용하여 열 수 있습니다.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_aem_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 23a65be4-3277-4c73-9189-a9b4d7be73cd
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
source-wordcount: '118'
ht-degree: 97%
---
# 로그 파일 {#log-files}

런타임 오류나 시작 오류와 같은 이벤트는 애플리케이션 서버 로그 파일에 기록됩니다. 애플리케이션 서버에 배포하는 데 문제가 있는 경우 로그 파일을 사용하여 문제를 찾을 수 있습니다. 모든 텍스트 편집기를 사용하여 로그 파일을 열 수 있습니다.

(JBoss) 다음과 같은 로그 파일은 `[appserver root]/server/'server'/log` 디렉터리에 있습니다.

* boot.log
* server.log.*[yyyy-mm-dd]*
* server.log

(WebLogic) 도메인 로그 파일은 `[appserverdomain]` 디렉터리에 있고 서버 로그 파일은 `[appserverdomain]/servers/[appserver name]/logs` 디렉터리에 있습니다.

* `access.log`
* `[appserver name].log`
* `[appserver name].out.[incremental number]`

(WebSphere) 다음과 같은 로그 파일은 `[appserver root]/profiles/default/logs/[appserver name]` 디렉터리에 있습니다.

* SystemErr.log
* SystemOut.log
* StartServer.log
