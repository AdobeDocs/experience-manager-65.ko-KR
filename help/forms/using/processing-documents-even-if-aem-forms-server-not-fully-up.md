---
title: AEM Forms 서버는 모든 서비스가 실행되고 실행되기 전에도 문서 처리를 시작합니다.
description: AEM Forms 서버는 JEE 서버와 OSGi 서버에서 모든 서비스가 실행되고 실행되기 전에도 문서 처리를 시작합니다.
exl-id: 1a1bc1cb-e0ce-49a0-9b05-ae59f900cfb2
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
source-wordcount: '129'
ht-degree: 3%
---
# AEM Forms 서버는 모든 서비스가 실행되고 실행되기 전에도 문서 처리를 시작합니다{#aem-forms-server-start-processing-documents-even-if-it-is-not-fully-up}

## 문제 {#issue}

<!--When user restarts AEM Forms server, the current calling processes or services still continue such as rendering PDF documents and more. It causes the restart of the AEM Forms server to not startup correctly.-->

AEM Forms 서버가 완전히 작동하고 모든 애플리케이션이 실행 중이기 전에 AEM Forms 서버가 문서 처리를 시작합니다.


## 적용 대상 {#applies-to}

이 솔루션은 JEE 서버의 AEM Forms 및 OSGi 서버의 AEM Forms에 적용됩니다.

## 솔루션 {#solution}

이 문제를 해결하려면 서버를 시작하는 동안 [일괄 처리 파일](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/deploying/command-line-start-and-stop.html?lang=ko#windows-platform-start-bat-script-example)에 인수 `Dcom.adobe.livecycle.dsc.deferServiceStart=true`을(를) 추가하십시오.
