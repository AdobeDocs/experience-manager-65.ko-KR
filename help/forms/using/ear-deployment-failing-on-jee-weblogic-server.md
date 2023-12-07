---
title: JEE WebLogic Server에서 EAR 배포 실패
description: JEE WebLogic Server에서 EAR 배포 실패를 해결하는 단계
exl-id: b87a9eee-ee56-4dca-b4a3-a42c91db0b4f
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '97'
ht-degree: 7%

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
