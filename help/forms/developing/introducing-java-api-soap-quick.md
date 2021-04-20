---
title: Java API QuickStart 소개
seo-title: Java API QuickStart 소개
description: Java API QuickStart 소개
uuid: 480e1809-f789-4ad8-b5d5-2d97aba8411a
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop, development-tools
discoiquuid: 38fd51ec-347e-4ae3-86d4-9d2429f79bdd
role: Developer
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '526'
ht-degree: 0%

---


# Java API 빠른 시작 {#introducing-java-api-quickstart} 소개

**이 문서의 샘플과 예는 JEE 환경의 AEM Forms에만 해당됩니다.**

Adobe AEM Forms API 빠른 시작을 사용하면 AEM Forms 서비스와 상호 작용하는 프로그램을 개발하는 데 소요되는 시간을 단축할 수 있습니다. *빠른*&#x200B;시작은 프로젝트에 복사하여 붙여넣을 수 있고 시작점으로 사용할 수 있는 전체 프로그램입니다. 빠른 시작을 실행하여 사용자 요구에 맞게 어떻게 동작하는지를 확인하고 수정할 수 있습니다.

AEM Forms 작업은 AEM Forms 강력한 형식의 API를 사용하여 수행할 수 있으며 연결 모드는 SOAP로 설정해야 합니다.

강력한 형식의 Java API 빠른 시작은 Java 애플리케이션을 실행하는 데 필요한 JAR 파일 목록을 제공합니다. 대부분의 Java 빠른 시작은 `main` 내에서 실행되는 콘솔 응용 프로그램입니다. 그러나 Forms Java의 강력한 형식의 API 빠른 시작은 웹 응용 프로그램 내에서 실행되는 Java 서블릿으로 구현됩니다.

JAR 파일 목록은 빠른 시작 시작 부분에 있는 주석 섹션에 있습니다. 예를 들어 다음 주석은 출력 빠른 시작 위치에 있으며 각 Java 빠른 시작 부분에 있는 일반적인 JAR 파일 목록입니다.

```java
 /*
     * This Java Quick Start uses the SOAP mode and contains the following JAR files
     * in the class path:
     * 1. adobe-output-client.jar
     * 2. adobe--client.jar
     * 3. adobe-usermanager-client.jar
     *
     * These JAR files are located in the following path:
     * <install directory>/Adobe/Adobe_Experience_Manager_forms/SDK/client-libs/common
     *
     * The adobe-utilities.jar file is located in the following path:
     * <install directory>/Adobe/Adobe_Experience_Manager_forms/SDK/client-libs/jboss
     *
     * The jboss-client.jar file is located in the following path:
     * <install directory>/Adobe/Adobe_Experience_Manager_forms/jboss/bin/client
     *
     * If you want to invoke a remote AEM Forms instance and there is a
     * firewall between the client application and AEM Forms, then it is
     * recommended that you use the SOAP mode. When using the SOAP mode,
     * you have to include additional JAR files located in the following
     * path
     * <install directory>/Adobe/Adobe_Experience_Manager_forms/SDK/client-libs/thirdparty
     *
     * For information about the SOAP
     * mode and the additional JAR files that need to be included,
     * see "Setting connection properties" in Programming
     * with AEM Forms
     *
     * For complete details about the location of the AEM Forms JAR files,
     * see "Including AEM Forms library files" in Programming
     * with AEM Forms
     */
```

## 여러 서비스 빠른 시작 {#multiple-services-quick-start}

대부분의 빠른 시작은 작업을 수행하기 위해 *JEE에서 AEM Forms을 사용한 프로그래밍*&#x200B;에 있습니다. 그러나 일부 빠른 시작은 지정된 워크플로우를 수행하기 위해 여러 AEM Forms 서비스를 호출합니다. 다음 목록은 둘 이상의 AEM Forms 서비스를 호출하는 Java 빠른 시작을 제공합니다.

[빠른 시작(SOAP 모드):Java API를 사용하여 AEM Forms 저장소에 있는 문서를 출력 서비스로](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-passing-a-document-located-in-the-repository-to-the-output-service-using-the-java-api)  전달(저장소 및 출력 서비스 호출)

[빠른 시작(SOAP 모드):Java API를 사용하여 조각을 기반으로 PDF](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-creating-a-pdf-document-based-on-fragments-using-the-java-api)  문서 만들기(어셈블리 및 출력 서비스 호출)

[빠른 시작(SOAP 모드):Java API를 사용하여 제출된 XML 데이터를 사용하여 PDF](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-creating-pdf-documents-with-submitted-xml-data-using-the-java-api)  문서 만들기(Forms, 출력 및 문서 관리 서비스 호출)

[빠른 시작(SOAP 모드):Java API를 사용하여 Forms 서비스에 문서를](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-passing-documents-to-the-forms-service-using-the-java-api)  전달(Forms 및 문서 관리 서비스 호출)

[빠른 시작(SOAP 모드):Java API를 사용하여 XFA 기반 양식에 디지털](/help/forms/developing/signature-service-java-api-quick.md#quick-start-soap-mode-digitally-signing-a-xfa-based-form-using-the-java-api)  서명(Forms 및 서명 서비스 호출)

[빠른 시작(SOAP 모드):Java API를 사용하여 역할 및](/help/forms/developing/user-manager-java-api-quick.md#quick-start-soap-mode-managing-roles-and-permissions-using-the-java-api)  권한 관리(DirectoryManager 및 AuthorizationManager 서비스 호출)

[빠른 시작(SOAP 모드):Java API를 사용하여 문서를 출력 서비스로](/help/forms/developing/output-service-java-api-quick.md#quick-start-soap-mode-passing-documents-to-the-output-service-using-the-java-api)  전달(출력 및 문서 관리 서비스 호출)

>[!NOTE]
>
>AEM Forms을 사용한 프로그래밍에 있는 빠른 시작은 JBoss® Application Server 및 Microsoft® Windows® 운영 체제에 배포되는 AEM Forms을 기반으로 합니다. 그러나 UNIX®와 같은 다른 운영 체제를 사용하는 경우에는 Windows 관련 경로를 해당 운영 체제에서 지원되는 경로로 바꿉니다. 마찬가지로 다른 J2EE 응용 프로그램 서버를 사용하는 경우 유효한 연결 속성을 지정해야 합니다. ([연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)을 참조하십시오.)

>[!NOTE]
>
>대부분의 웹 서비스 빠른 시작은 C#으로 작성되며 .NET 프레임워크를 사용합니다. 그러나 SOAP 표준을 지원하는 모든 개발 환경에서 AEM Forms 서비스를 호출할 수 있는 클라이언트 응용 프로그램 논리를 만들 수 있습니다. ([웹 서비스를 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-web-services)을 참조하십시오.)

