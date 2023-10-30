---
title: API를 사용하여 AEM Forms을 호출하는 방법
description: Java API, 웹 서비스, 원격 및 REST를 사용하여 AEM Forms 서비스를 호출합니다.
uuid: d100e106-e508-4d3c-ba8c-b5fe13c9e2d6
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: coding, development-tools
discoiquuid: 1825e12c-0306-4e0a-9643-47ce1ce82132
role: Developer
exl-id: 0e92d1ad-12bd-4bfd-81cc-9be8e376c5ca
source-git-commit: 0e5b89617d481c69882ec5d4658e76855aa9b691
workflow-type: tm+mt
source-wordcount: '293'
ht-degree: 0%

---

# API를 사용하여 AEM Forms 호출 {#invoking-aem-forms-using-apis}

**이 문서의 샘플 및 예제는 JEE 환경의 AEM Forms에 대해서만 적용됩니다.**

Adobe Experience Manager Forms은 공유 인프라 내에서 작동하는 서비스로 구성된 J2EE 기반 엔터프라이즈 소프트웨어입니다. 서비스 작업은 일반적으로 문서를 사용하거나 생성합니다. AEM Forms을 사용하면 통합 및 통합 서비스 세트에서 양식 워크플로우와 전자 양식, 문서 보안 및 문서 생성을 결합할 수 있습니다. 이러한 서비스는 방화벽 내부 및 외부에서 액세스할 수 있습니다.

클라이언트 애플리케이션은 Java API, 웹 서비스, 원격 및 REST를 사용하여 프로그래밍 방식으로 AEM Forms 서비스를 호출할 수 있습니다. 관리 콘솔을 사용하여 프로그래밍 방식으로 호출하여 AEM Forms 서비스를 사용할 수 있도록 하는 엔드포인트가 표시되도록 서비스를 구성할 수 있습니다. 기본적으로 대부분의 서비스는 원격, Java 및 웹 서비스 끝점을 노출하도록 사전 구성되어 있습니다.

비즈니스 요구 사항에 따라 사용할 호출 방법이 결정됩니다. 예를 들어 Java API를 사용하여 AEM Forms 기능을 Java Entity 및 Message Beans와 같은 Java 엔터프라이즈 애플리케이션에 통합할 수 있습니다. 마찬가지로 웹 서비스를 사용하여 AEM Forms 기능을 .NET 프로젝트(또는 웹 서비스 표준을 지원하는 개발 환경으로 개발된 기타 프로젝트)에 통합할 수 있습니다.

서비스를 실행하려면 EJB(Enterprise JavaBeans™)에 J2EE 컨테이너가 필요한 방법과 유사한 서비스 컨테이너가 필요합니다. AEM Forms에는 서비스 컨테이너의 구현이 하나만 포함되어 있습니다. 서비스 컨테이너는 서비스를 배포하고 모든 요청이 올바른 서비스로 전송되도록 하는 등 서비스 수명을 관리합니다. 또한 서비스가 소비하거나 생성하는 문서를 관리합니다.

>[!NOTE]
>
>AEM Forms를 사용한 프로그래밍에는 감시 폴더 또는 이메일을 사용하여 AEM Forms을 호출하는 방법에 대한 정보가 포함되어 있지 않습니다.
