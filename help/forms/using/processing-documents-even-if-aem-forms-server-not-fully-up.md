---
title: AEM Forms 서버는 모든 서비스가 실행되고 실행되기 전에도 문서 처리를 시작합니다.
description: AEM Forms 서버는 JEE 서버와 OSGi 서버에서 모든 서비스가 실행되고 실행되기 전에도 문서 처리를 시작합니다.
exl-id: 1a1bc1cb-e0ce-49a0-9b05-ae59f900cfb2
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 9f59606bb58b9e90f07bd22e89f3213afb54a697
workflow-type: tm+mt
source-wordcount: '111'
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
