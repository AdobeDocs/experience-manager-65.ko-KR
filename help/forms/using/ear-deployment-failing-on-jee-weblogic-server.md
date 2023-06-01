---
title: JEE WebLogic Server에서 EAR 배포 실패
seo-title: EAR Deployment failing on JEE Weblogic Server
description: JEE WebLogic Server에서 EAR 배포 실패를 해결하는 단계
seo-description: Steps to resolve EAR Deployment failing on JEE Weblogic Server
source-git-commit: 45bb54a2666c2c196a8fb52795a7f428aa751e4d
workflow-type: tm+mt
source-wordcount: '103'
ht-degree: 6%

---


# JEE WebLogic Server에서 EAR 배포 실패 {#ear-deployment-failing-on-jee-weblogic-server}

## 문제 {#issue}

사용자가 를 배포하려고 할 때 `adobe-livecycle-weblogic.ear`, `Null Pointer` 예외가 발생했습니다 .

## 적용 대상 {#applies-to}

이 솔루션은 다음에 적용됩니다.

* WebLogic JEE 서버 버전 12.2.1.x의 AEM Forms.

## 솔루션 {#solution}

문제를 해결하려면 다음 단계를 수행합니다.

1. 로 이동 `<domain_home>\bin` 설치된 WebLogic JEE 서버의 디렉토리.

1. 편집 `setDomainEnv.cmd` 또는 `setDomainEnv.sh` 파일, 형식 `applicable`.

1. 의 마지막 항목 검색 `JAVA_OPTS` 및 추가 `-DANTLR_USE_DIRECT_CLASS_LOADING=true` 할 수 있습니다. 예를 들어 업데이트된 문자열은 다음과 같이 나타납니다.

       OPTIONS OPTIONS &#39;JAVA_LOADS=%JAVA_LOADS% -DANTLR_USE_DIRECT_CLASS_LOADING=true&#39; 설정
   
1. 변경 사항을 저장합니다.


