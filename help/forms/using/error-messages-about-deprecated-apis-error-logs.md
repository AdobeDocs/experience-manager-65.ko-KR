---
title: 오류 로그에서 사용되지 않는 API에 대한 오류 메시지
description: 오류 로그에서 사용되지 않는 API에 대한 오류 메시지
source-git-commit: b05666883645ca11784292e4bfb5bf9c1e35a43b
workflow-type: tm+mt
source-wordcount: '102'
ht-degree: 7%

---


# 오류 로그에서 사용되지 않는 API에 대한 오류 메시지 {#error-messages-about-deprecated-apis-in-error-logs}

이 문제는 다음 버전에 적용됩니다.

* Experience Manager 6.5 Forms

## 문제 {#issue}

* error.log 파일에 다음 오류 메시지가 표시됩니다.
   ` *WARN* [default task-36] org.apache.jackrabbit.oak.spi.security.principal.AclGroupDeprecation use of deprecated java.acl.Group-related API - this method is going to be removed in future Oak releases - see OAK-7358 for details` (NPR-38282)

## 해결 {#workaround}

1. 설치 [Experience Manager Forms 서비스 팩 13 이상(6.5.13.0 이상)](https://experienceleague.adobe.com/docs/experience-manager-65/release-notes/release-notes.html?lang=ko-KR)
1. 소프트웨어 배포에서 패키지(.jar 파일(해상도가 있는 파일)를 다운로드하려면 다음 링크를 사용하십시오.

   https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?pack[...]pack/com.adobe.livecycle.dsc.externalloginmodule-4.0.8.jar

1. Experience Manager 구성 관리자를 열고 다운로드한 com.adobe.livecycle.dsc.externalloginmodule-4.0.8.jar 파일을 설치합니다.

문제가 해결되었습니다.