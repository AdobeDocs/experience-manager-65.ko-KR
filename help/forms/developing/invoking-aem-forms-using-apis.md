---
title: API를 사용하여 AEM Forms 호출
seo-title: API를 사용하여 AEM Forms 호출
description: 'null'
seo-description: 'null'
uuid: d100e106-e508-4d3c-ba8c-b5fe13c9e2d6
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: development-tools
discoiquuid: 1825e12c-0306-4e0a-9643-47ce1ce82132
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# API를 사용하여 AEM Forms 호출 {#invoking-aem-forms-using-apis}

Adobe Experience Manager Forms는 공유 인프라 내에서 작동하는 서비스로 구성되어 있는 J2EE 기반의 기업 소프트웨어입니다. 서비스 작업은 일반적으로 문서를 소비하거나 생성합니다. AEM Forms를 사용하면 양식 워크플로우를 전자 양식, 문서 보안 및 문서 생성과 결합하여 통합된 서비스 세트에 통합할 수 있습니다. 이러한 서비스는 방화벽 내외부에서 액세스할 수 있습니다.

클라이언트 응용 프로그램은 Java API, 웹 서비스, Remoting 및 REST를 사용하여 프로그래밍 방식으로 AEM Forms 서비스를 호출할 수 있습니다. 관리 콘솔을 사용하여 프로그래밍 방식으로 호출하여 AEM Forms 서비스를 이용할 수 있는 끝점을 노출하도록 서비스를 구성할 수 있습니다. 기본적으로 대부분의 서비스는 Remoting, Java 및 웹 서비스 끝점을 노출하도록 미리 구성됩니다.

비즈니스 요구 사항에 따라 사용할 호출 방법이 결정됩니다. 예를 들어 Java API를 사용하여 AEM Forms 기능을 Java 엔티티 및 Message Bean과 같은 Java 엔터프라이즈 애플리케이션에 통합할 수 있습니다. 마찬가지로 웹 서비스를 사용하여 AEM Forms 기능을 .NET 프로젝트(또는 웹 서비스 표준을 지원하는 개발 환경으로 개발된 기타 프로젝트)에 통합할 수 있습니다.

EJB(Enterprise JavaBeans™)가 J2EE 컨테이너를 필요로 하는 방식과 유사한 서비스 컨테이너를 실행해야 합니다. AEM Forms에는 서비스 컨테이너의 구현이 하나만 포함됩니다. 서비스 컨테이너는 배포 및 모든 요청이 올바른 서비스로 전송되도록 하는 등 서비스의 수명을 관리합니다. 또한 서비스가 소비하거나 생성하는 문서를 관리합니다.

>[!NOTE]
>
>AEM 양식을 사용한 프로그래밍에는 감시 폴더 또는 이메일을 사용하여 AEM Forms를 호출하는 방법에 대한 정보가 포함되어 있지 않습니다.

