---
title: WS-security 헤더를 사용하여 자격 증명 전달
description: WS-security 헤더를 사용하여 자격 증명을 전달하는 방법 알아보기
exl-id: 519d57ad-81ab-4caf-ae25-4390ae2eee13
source-git-commit: 1807919078996b1cf1cbd1f2d90c3b14cb660e2c
workflow-type: tm+mt
source-wordcount: '215'
ht-degree: 0%

---

# WS-Security 헤더를 사용하여 자격 증명 전달 {#using-execute-script-service-aem-forms-jee-workbench}

웹 서비스를 사용하여 JEE 서비스에서 AEM Forms을 호출할 때 WS-Security 헤더를 사용하여 JEE에서 AEM Forms에 필요한 클라이언트 인증 정보를 전달할 수 있습니다. WS-Security는 클라이언트 인증, 메시지 기밀 유지 및 메시지 무결성을 구현하기 위한 SOAP 확장을 정의합니다. 따라서 JEE의 AEM Forms이 독립 실행형 서버로 배포되거나 클러스터된 환경 내에 배포될 때 JEE 서비스에서 AEM Forms을 호출할 수 있습니다.

JEE의 AEM Forms에 WS-Security 헤더를 전달하는 방법은 Axis 생성 Java 클래스를 사용하는지 또는 서비스의 기본 SOAP 스택을 사용하는 .NET 클라이언트 어셈블리를 사용하는지에 따라 다릅니다.

>[!NOTE]
>
>WS-Security 헤더를 사용하여 서비스를 호출하는 예제로서 이 항목은 암호화 서비스를 호출하여 암호로 PDF 문서를 암호화합니다.

이 문서에서는 다음 주제를 다룹니다.

* Axis 생성 Java 클래스를 사용하여 클라이언트 인증 전달

* 암호화 서비스를 호출하는 데 필요한 Axis 라이브러리 파일 생성

* WS-Security 헤더를 사용하여 암호화 서비스 호출

* .NET 클라이언트 어셈블리를 사용하여 클라이언트 인증 전달

* WS-Security 헤더를 사용하여 암호화 서비스 호출


## 요구 사항 {#requirements}

이 문서를 최대한 활용하려면 JEE 소프트웨어의 AEM Forms에 대해 깊이 있게 이해해야 합니다.

>[!MORELIKETHIS]
>
>* [WS-Security 헤더를 사용하여 자격 증명 전달](assets/passing-credentials-using-ws-security-headers.pdf)
