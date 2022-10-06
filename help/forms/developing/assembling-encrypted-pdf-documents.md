---
title: 암호화된 PDF 문서 정리
seo-title: Assembling Encrypted PDF Documents
description: Java API 및 웹 서비스 API를 사용하여 암호화된 PDF 문서를 어셈블합니다.
seo-description: Assemble encrypted PDF documents using the Java API and Web Service API.
uuid: d0948ec9-ab67-4fe4-9062-1c4938460b43
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 6d75c7b1-9c0e-47f3-bdb1-61acf16b97f9
role: Developer
exl-id: 2caaca74-640a-4257-a81b-3e8b295cd182
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1659'
ht-degree: 0%

---

# 암호화된 PDF 문서 정리 {#assembling-encrypted-pdf-documents}

**이 문서의 샘플 및 예제는 JEE 환경의 AEM Forms용입니다.**

어셈블러 서비스를 사용하여 암호로 PDF 문서를 암호화할 수 있습니다. PDF 문서가 암호로 암호화되면 사용자는 Adobe Reader 또는 Acrobat에서 PDF 문서를 보려면 암호를 지정해야 합니다. 암호로 PDF 문서를 암호화하려면 DDX 문서에 PDF 문서를 암호화하는 데 필요한 암호화 요소 값이 있어야 합니다.

이 토론을 위해 다음 DDX 문서가 사용된다고 가정하십시오.

```xml
 <?xml version="1.0" encoding="UTF-8"?>
 <DDX xmlns="https://ns.adobe.com/DDX/1.0/">
        <PDF result="EncryptLoan.pdf" encryption="userProtect">
         <PDF source="inDoc" />
     </PDF>
     <PasswordEncryptionProfile name="userProtect" compatibilityLevel="Acrobat7">
         <OpenPassword>AdobeOpen</OpenPassword>
        </PasswordEncryptionProfile>
 </DDX>
```

이 DDX 문서 내에서 소스 속성에 값이 할당되었음을 알 수 있습니다 `inDoc`. 하나의 입력 PDF 문서만 어셈블러 서비스에 전달되고 하나의 PDF 문서가 반환되는 경우 `invokeOneDocument` 작업, 값 할당 `inDoc` 를 PDF 소스 속성에 추가합니다. 를 호출할 때 `invokeOneDocument` 작업, `inDoc` 값은 DDX 문서에 지정해야 하는 사전 정의된 키입니다.

반면 입력 PDF 문서를 어셈블러 서비스에 두 개 이상 전달할 때 `invokeDDX` 작업. 이 경우 입력 PDF 문서의 파일 이름을 `source` 속성을 사용합니다.

암호와 함께 PDF 문서를 암호화하기 위해 암호화 서비스가 AEM Forms 설치에 포함되지 않아도 됩니다. 자세한 내용은 [PDF 문서 암호화 및 암호 해독](/help/forms/developing/encrypting-decrypting-pdf-documents.md).

>[!NOTE]
>
>어셈블러 서비스에 대한 자세한 내용은 [AEM Forms에 대한 서비스 참조](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>DDX 문서에 대한 자세한 내용은 [어셈블러 서비스 및 DDX 참조](https://www.adobe.com/go/learn_aemforms_ddx_63).

## 단계 요약 {#summary-of-steps}

암호화된 PDF 문서를 어셈블하려면 다음 단계를 수행합니다.

1. 프로젝트 파일을 포함합니다.
1. PDF 어셈블러 클라이언트를 만듭니다.
1. 기존 DDX 문서를 참조합니다.
1. 비보안 PDF 문서를 참조합니다.
1. 런타임 옵션을 설정합니다.
1. 문서를 암호화합니다.
1. 암호화된 PDF 문서를 저장합니다.

**프로젝트 파일 포함**

개발 프로젝트에 필요한 파일을 포함합니다. Java를 사용하여 클라이언트 응용 프로그램을 만드는 경우 필요한 JAR 파일을 포함하십시오. 웹 서비스를 사용하는 경우 프록시 파일을 포함해야 합니다.

프로젝트의 클래스 경로에 다음 JAR 파일을 추가해야 합니다.

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar(AEM Forms이 JBoss에 배포된 경우 필수)
* jbossall-client.jar(AEM Forms이 JBoss에 배포되는 경우 필요)

AEM Forms이 JBoss 이외의 지원되는 J2EE 애플리케이션 서버에 배포된 경우, adobe-utilities.jar 및 jbossall-client.jar 파일을 AEM Forms이 배포된 J2EE 애플리케이션 서버에 고유한 JAR 파일로 바꾸어야 합니다. 모든 AEM Forms JAR 파일의 위치에 대한 자세한 내용은 [AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**어셈블러 클라이언트 만들기**

어셈블러 작업을 프로그래밍 방식으로 수행하려면 먼저 어셈블러 서비스 클라이언트를 만들어야 합니다.

**기존 DDX 문서 참조**

PDF 문서를 어셈블하려면 DDX 문서를 참조해야 합니다. 예를 들어 이 섹션에서 도입된 DDX 문서를 생각해 보십시오. PDF 문서를 암호화하려면 DDX 문서에 `PasswordEncryptionProfile` 요소를 생성하지 않습니다.

**비보안 PDF 문서 참조**

보안되지 않은 PDF 문서를 참조하고 어셈블러 서비스로 전달하여 암호화해야 합니다. 이미 암호화된 PDF 문서를 참조하는 경우 예외가 발생합니다.

**런타임 옵션 설정**

작업을 수행하는 동안 어셈블러 서비스의 동작을 제어하는 런타임 옵션을 설정할 수 있습니다. 예를 들어 오류가 발생하면 어셈블러 서비스에 작업을 계속 처리하도록 지시하는 옵션을 설정할 수 있습니다. 설정할 수 있는 런타임 옵션에 대한 자세한 내용은 `AssemblerOptionSpec` 클래스 참조 [AEM Forms API 참조](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

**문서 암호화**

어셈블러 서비스 클라이언트를 만든 후 암호화 정보를 포함하는 DDX 문서를 참조하고 보안되지 않은 PDF 문서를 참조하며 런타임 옵션을 설정할 수 있습니다 `invokeOneDocument` 작업. 하나의 입력 PDF 문서만 어셈블러 서비스로 전달되고 하나의 문서가 반환되므로 `invokeOneDocument` 작업 대신 `invokeDDX` 작업.

**암호화된 PDF 문서를 저장합니다**

단일 PDF 문서만 어셈블러 서비스에 전달되면 어셈블러 서비스는 수집 객체 대신 단일 문서를 반환합니다. 즉, `invokeOneDocument` 작업을 수행하면 단일 문서가 반환됩니다. 이 섹션에서 참조되는 DDX 문서에는 암호화 정보가 포함되어 있으므로 어셈블러 서비스는 암호로 암호화된 PDF 문서를 반환합니다.

**추가 참조**

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[프로그래밍 방식으로 PDF 문서 조립](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## Java API를 사용하여 암호화된 PDF 문서 조합 {#assemble-an-encrypted-pdf-document-using-the-java-api}

1. 프로젝트 파일을 포함합니다.

   Java 프로젝트의 클래스 경로에 adobe-assembler-client.jar와 같은 클라이언트 JAR 파일을 포함합니다.

1. 어셈블러 클라이언트를 만듭니다.

   * 만들기 `ServiceClientFactory` 연결 속성을 포함하는 객체입니다.
   * 만들기 `AssemblerServiceClient` 생성자를 사용하여 객체를 전달하고 `ServiceClientFactory` 개체.

1. 기존 DDX 문서를 참조합니다.

   * 만들기 `java.io.FileInputStream` 생성자를 사용하고 DDX 파일의 위치를 지정하는 문자열 값을 전달하여 DDX 문서를 나타내는 개체입니다.
   * 만들기 `com.adobe.idp.Document` 생성자를 사용하여 객체를 전달하고 `java.io.FileInputStream` 개체.

1. 비보안 PDF 문서를 참조합니다.

   * 만들기 `java.io.FileInputStream` 생성자를 사용하고 보안되지 않은 PDF 문서의 위치를 전달하여 개체를 가져옵니다.
   * 만들기 `com.adobe.idp.Document` 개체 및 전달 `java.io.FileInputStream` PDF 문서를 포함하는 객체입니다. 이 `com.adobe.idp.Document` 개체가 `invokeOneDocument` 메서드를 사용합니다.

1. 런타임 옵션을 설정합니다.

   * 만들기 `AssemblerOptionSpec` 생성자를 사용하여 런타임 옵션을 저장하는 개체입니다.
   * 에 속한 메서드를 호출하여 비즈니스 요구 사항을 충족하도록 런타임 옵션을 설정합니다. `AssemblerOptionSpec` 개체. 예를 들어 오류가 발생할 때 어셈블러 서비스에서 작업을 계속 처리하도록 하려면 `AssemblerOptionSpec` 개체 `setFailOnError` 메서드 및 전달 `false`.

1. 문서를 암호화합니다.

   를 호출합니다 `AssemblerServiceClient` 개체 `invokeOneDocument` 메서드를 사용하여 다음 값을 전달합니다.

   * A `com.adobe.idp.Document` DDX 문서를 나타내는 객체입니다. 이 DDX 문서에 값이 포함되어 있는지 확인합니다. `inDoc` PDF 소스 요소에 사용됩니다.
   * A `com.adobe.idp.Document` 비보안 PDF 문서를 포함하는 객체입니다.
   * A `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` 기본 글꼴 및 작업 로그 수준을 포함하여 런타임 옵션을 지정하는 개체입니다.

   다음 `invokeOneDocument` 메서드 반환 `com.adobe.idp.Document` 암호로 암호화된 PDF 문서를 포함하는 객체입니다.

1. 암호화된 PDF 문서를 저장합니다.

   * 만들기 `java.io.File` 개체 및 파일 이름 확장명이 .pdf인지 확인합니다.
   * 를 호출합니다 `Document` 개체 `copyToFile` 컨텐츠의 내용 복사 방법 `Document` 개체를 파일로 가져올 수 있습니다. 를 사용해야 합니다 `Document` 개체를 `invokeOneDocument` 메서드가 반환되었습니다.

**추가 참조**

[빠른 시작(SOAP 모드): Java API를 사용하여 암호화된 PDF 문서 어셈블링](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-assembling-an-encrypted-pdf-document-using-the-java-api)

## 웹 서비스 API를 사용하여 암호화된 PDF 문서 조합 {#assemble-an-encrypted-pdf-document-using-the-web-service-api}

1. 프로젝트 파일을 포함합니다.

   MTOM을 사용하는 Microsoft .NET 프로젝트를 만듭니다. 서비스 참조를 설정할 때 다음 WSDL 정의를 사용해야 합니다. `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >바꾸기 `localhost` (AEM Forms을 호스팅하는 서버의 IP 주소 사용)

1. 어셈블러 클라이언트를 만듭니다.

   * 만들기 `AssemblerServiceClient` 기본 생성자를 사용하여 개체를 만듭니다.
   * 만들기 `AssemblerServiceClient.Endpoint.Address` 개체를 `System.ServiceModel.EndpointAddress` 생성자입니다. WSDL을 지정하는 문자열 값을 AEM Forms 서비스에 전달합니다(예: `http://localhost:8080/soap/services/AssemblerService?blob=mtom`). 를 사용할 필요가 없습니다 `lc_version` 속성을 사용합니다. 이 속성은 서비스 참조를 만들 때 사용됩니다.
   * 만들기 `System.ServiceModel.BasicHttpBinding` 개체의 값을 가져와서 `AssemblerServiceClient.Endpoint.Binding` 필드. 반환 값을 다음으로 캐스팅합니다. `BasicHttpBinding`.
   * 설정 `System.ServiceModel.BasicHttpBinding` 개체 `MessageEncoding` 필드 대상 `WSMessageEncoding.Mtom`. 이 값은 MTOM이 사용되도록 합니다.
   * 다음 작업을 수행하여 기본 HTTP 인증을 활성화합니다.

      * 필드에 AEM Forms 사용자 이름을 지정합니다 `AssemblerServiceClient.ClientCredentials.UserName.UserName`.
      * 필드에 해당 암호 값을 지정합니다 `AssemblerServiceClient.ClientCredentials.UserName.Password`.
      * 상수 값 할당 `HttpClientCredentialType.Basic` 아래와 같이 변경하는 것을 의미합니다 `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * 상수 값 할당 `BasicHttpSecurityMode.TransportCredentialOnly` 아래와 같이 변경하는 것을 의미합니다 `BasicHttpBindingSecurity.Security.Mode`.

1. 기존 DDX 문서를 참조합니다.

   * 만들기 `BLOB` 생성자를 사용하여 개체를 작성합니다. 다음 `BLOB` 객체는 DDX 문서를 저장하는 데 사용됩니다.
   * 만들기 `System.IO.FileStream` 개체의 생성자를 호출하고 DDX 문서의 파일 위치와 파일을 열 모드를 나타내는 문자열 값을 전달하여 개체를 엽니다.
   * 의 내용을 저장하는 바이트 배열을 만듭니다 `System.IO.FileStream` 개체. 를 가져와서 바이트 배열의 크기를 결정할 수 있습니다 `System.IO.FileStream` 개체 `Length` 속성을 사용합니다.
   * 를 호출하여 바이트 배열을 스트림 데이터로 채웁니다 `System.IO.FileStream` 개체 `Read` 바이트 배열, 시작 위치 및 읽을 스트림 길이를 전달하는 메서드와 전달
   * 을(를) 채우기 `BLOB` 개체를 할당하여 개체를 개체 개체 `MTOM` 바이트 배열의 내용을 포함하는 필드입니다.

1. 비보안 PDF 문서를 참조합니다.

   * 만들기 `BLOB` 생성자를 사용하여 개체를 작성합니다. 다음 `BLOB` 개체는 입력 PDF 문서를 저장하는 데 사용됩니다. 이 `BLOB` 개체가 `invokeOneDocument` 논쟁으로.
   * 만들기 `System.IO.FileStream` 객체를 사용하여 생성자를 호출하고 입력 PDF 문서의 파일 위치와 파일을 열 모드를 나타내는 문자열 값을 전달합니다.
   * 의 내용을 저장하는 바이트 배열을 만듭니다 `System.IO.FileStream` 개체. 를 가져와서 바이트 배열의 크기를 결정할 수 있습니다 `System.IO.FileStream` 개체 `Length` 속성을 사용합니다.
   * 를 호출하여 바이트 배열을 스트림 데이터로 채웁니다 `System.IO.FileStream` 개체 `Read` 바이트 배열, 시작 위치 및 읽을 스트림 길이를 전달하는 메서드와 전달
   * 을(를) 채우기 `BLOB` 개체를 할당하여 개체를 개체 개체 `MTOM` 바이트 배열의 내용을 포함하는 필드입니다.

1. 런타임 옵션을 설정합니다.

   * 만들기 `AssemblerOptionSpec` 생성자를 사용하여 런타임 옵션을 저장하는 개체입니다.
   * 비즈니스 요구 사항에 맞게 런타임 옵션을 설정하려면 `AssemblerOptionSpec` 개체. 예를 들어 오류가 발생할 때 어셈블러 서비스에서 작업을 계속 처리하도록 지시하려면 을 할당합니다. `false` 변환 후 `AssemblerOptionSpec` 개체 `failOnError` 데이터 멤버.

1. 문서를 암호화합니다.

   를 호출합니다 `AssemblerServiceClient` 개체 `invokeOneDocument` 메서드를 사용하여 다음 값을 전달합니다.

   * A `BLOB` DDX 문서를 나타내는 객체
   * A `BLOB` 비보안 PDF 문서를 나타내는 객체
   * An `AssemblerOptionSpec` 런타임 옵션을 지정하는 객체

   다음 `invokeOneDocument` 메서드 반환 `BLOB` 암호화된 PDF 문서를 포함하는 개체입니다.

1. 암호화된 PDF 문서를 저장합니다.

   * 만들기 `System.IO.FileStream` 개체의 생성자를 호출하고 암호화된 PDF 문서의 파일 위치와 파일을 열 모드를 나타내는 문자열 값을 전달하여 개체를 엽니다.
   * 의 내용을 저장하는 바이트 배열을 만듭니다 `BLOB` 개체를 `invokeOneDocument` 메서드가 반환되었습니다. 의 값을 가져와서 바이트 배열을 채웁니다 `BLOB` 개체 `MTOM` 데이터 멤버.
   * 만들기 `System.IO.BinaryWriter` 생성자를 호출하고 전달하여 개체를 `System.IO.FileStream` 개체.
   * 를 호출하여 PDF 파일에 바이트 배열의 내용을 씁니다. `System.IO.BinaryWriter` 개체 `Write` 메서드를 사용하여 바이트 배열을 전달합니다.

**추가 참조**

[MTOM을 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
