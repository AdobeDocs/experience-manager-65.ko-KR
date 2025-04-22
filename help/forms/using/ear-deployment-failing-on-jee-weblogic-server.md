---
title: JEE WebLogic Server에서 EAR 배포 실패
seo-title: EAR Deployment failing on JEE Weblogic Server
description: JEE WebLogic Server에서 EAR 배포 실패를 해결하는 단계
source-git-commit: 05712cfcef1d9c37b7cd015133abaf6df0e351d2
workflow-type: tm+mt
source-wordcount: '97'
ht-degree: 7%

---


# JEE WebLogic Server에서 EAR 배포 실패 {#ear-deployment-failing-on-jee-weblogic-server}

## 문제 {#issue}

사용자가 `adobe-livecycle-weblogic.ear`을(를) 배포하려고 할 때 `Null Pointer` 예외가 발생했습니다.

## 적용 대상 {#applies-to}

이 솔루션은 다음에 적용됩니다.

* WebLogic JEE 서버 버전 12.2.1.x의 AEM Forms.

## 솔루션 {#solution}

문제를 해결하려면 다음 단계를 수행합니다.

1. 설치된 WebLogic JEE 서버의 `<domain_home>\bin` 디렉터리로 이동합니다.

1. `setDomainEnv.cmd` 또는 `setDomainEnv.sh` 파일을 `applicable`(으)로 편집합니다.

1. `JAVA_OPTS`의 마지막 항목을 검색하고 `-DANTLR_USE_DIRECT_CLASS_LOADING=true`을(를) 추가합니다. 예를 들어 업데이트된 문자열은 다음과 같이 나타납니다.

       설정 `JAVA_OPTIONS=%JAVA_OPTIONS% -DANTLR_USE_DIRECT_CLASS_LOADING=true`
   
1. 변경 사항을 저장합니다.
