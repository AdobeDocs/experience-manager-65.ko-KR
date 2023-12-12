---
title: AEM Forms에도 불구하고 여러 서비스 실행이 시작되지 않았습니다.
description: AEM Forms이 완전히 시작되지 않았더라도 여러 서비스를 처리합니다.
exl-id: 4ec40412-15b1-434b-a919-2cf23f48077c
source-git-commit: faa628ac4a4631564141f68f3efc9d69a67e5c40
workflow-type: tm+mt
source-wordcount: '96'
ht-degree: 4%

---

# AEM Forms에도 불구하고 여러 서비스 실행이 완전히 시작되지 않음{#steps-to-resolve-error-after-installing-service-pack}


## 문제 {#issue}

사용자가 AEM Forms을 다시 시작할 때 PDF 문서 렌더링 등과 같은 현재 호출 프로세스가 계속 진행됩니다. 이로 인해 AEM Forms 서버가 다시 시작되지 않습니다.

## 적용 대상 {#applies-to}

이 솔루션은 JEE 서버의 AEM Forms 및 OSGi 서버의 AEM Forms에 적용됩니다.

## 솔루션 {#solution}

문제를 해결하려면 인수를 추가합니다. `Dcom.adobe.livecycle.dsc.deferServiceStart=true` 끝 [배치 파일](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/deploying/command-line-start-and-stop.html#windows-platform-start-bat-script-example) 서버를 시작하는 동안.
