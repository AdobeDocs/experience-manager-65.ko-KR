---
title: 암호화된 PDF 문서 어셈블
description: Java API 및 웹 서비스 API를 사용하여 암호화된 PDF 문서를 조합합니다.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
exl-id: 2caaca74-640a-4257-a81b-3e8b295cd182
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '1641'
ht-degree: 0%

---

# 암호화된 PDF 문서 어셈블 {#assembling-encrypted-pdf-documents}

**이 문서의 샘플 및 예제는 JEE 환경의 AEM Forms에 대해서만 적용됩니다.**

어셈블러 서비스를 사용하여 암호로 PDF 문서를 암호화할 수 있습니다. PDF 문서가 암호로 암호화되면 사용자는 암호를 지정하여 Adobe Reader 또는 Acrobat에서 PDF 문서를 확인해야 합니다. 암호로 PDF 문서를 암호화하려면 DDX 문서에 PDF 문서를 암호화하는 데 필요한 암호화 요소 값이 들어 있어야 합니다.

이러한 논의를 위해 다음과 같은 DDX 문서가 사용된다고 가정하자.

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

이 DDX 문서 내에서 소스 속성에 값이 할당됩니다 `inDoc`. 한 개의 입력 PDF 문서만 어셈블러 서비스에 전달되고 한 개의 PDF 문서가 반환되는 경우 `invokeOneDocument` 작업, 값 할당 `inDoc` PDF 소스 속성에 매핑할 수도 있습니다. 를 호출할 때 `invokeOneDocument` 작업, `inDoc` 값은 DDX 문서에 지정해야 하는 미리 정의된 키입니다.

반대로 두 개 이상의 입력 PDF 문서를 어셈블러 서비스에 전달할 때 `invokeDDX` 작업. 이 경우 입력 PDF 문서의 파일 이름을 `source` 특성.

암호로 PDF 문서를 암호화하기 위해 암호화 서비스가 AEM Forms 설치에 포함될 필요는 없습니다. 다음을 참조하십시오 [PDF 문서 암호화 및 복호화](/help/forms/developing/encrypting-decrypting-pdf-documents.md).

>[!NOTE]
>
>어셈블러 서비스에 대한 자세한 내용은 [AEM Forms에 대한 서비스 참조](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>DDX 문서에 대한 자세한 내용은 [어셈블러 서비스 및 DDX 참조](https://www.adobe.com/go/learn_aemforms_ddx_63).

## 단계 요약 {#summary-of-steps}

암호화된 PDF 문서를 어셈블하려면 다음 단계를 수행하십시오.

1. 프로젝트 파일을 포함합니다.
1. PDF 어셈블러 클라이언트를 만듭니다.
1. 기존 DDX 문서를 참조합니다.
1. 보안되지 않은 PDF 문서를 참조합니다.
1. 런타임 옵션을 설정합니다.
1. 문서를 암호화합니다.
1. 암호화된 PDF 문서를 저장합니다.

**프로젝트 파일 포함**

개발 프로젝트에 필요한 파일을 포함하십시오. Java를 사용하여 클라이언트 응용 프로그램을 만드는 경우 필요한 JAR 파일을 포함합니다. 웹 서비스를 사용하는 경우 프록시 파일을 포함해야 합니다.

프로젝트의 클래스 경로에 다음 JAR 파일을 추가해야 합니다.

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar (AEM Forms이 JBoss에 배포된 경우 필수)
* jbossall-client.jar(AEM Forms이 JBoss에 배포된 경우 필수)

AEM Forms이 JBoss 이외의 지원되는 J2EE 애플리케이션 서버에 배포된 경우 adobe-utilities.jar 및 jbossall-client.jar 파일을 AEM Forms이 배포된 J2EE 애플리케이션 서버에 관련된 JAR 파일로 교체해야 합니다. 모든 AEM Forms JAR 파일의 위치에 대한 자세한 내용은 [AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**어셈블러 클라이언트 만들기**

어셈블러 작업을 프로그래밍 방식으로 수행하려면 먼저 어셈블러 서비스 클라이언트를 만들어야 합니다.

**기존 DDX 문서 참조**

PDF 문서를 어셈블하려면 DDX 문서를 참조해야 합니다. 예를 들어 이 섹션에 소개된 DDX 문서를 생각해 보십시오. PDF 문서를 암호화하려면 DDX 문서에 `PasswordEncryptionProfile` 요소를 생성하지 않습니다.

**비보안 PDF 문서 참조**

보안되지 않은 PDF 문서를 참조하고 어셈블러 서비스에 전달하여 암호화해야 합니다. 이미 암호화된 PDF 문서를 참조하는 경우 예외가 throw됩니다.

**런타임 옵션 설정**

작업을 수행하는 동안 어셈블러 서비스의 동작을 제어하는 런타임 옵션을 설정할 수 있습니다. 예를 들어 오류가 발생하는 경우 어셈블러 서비스에서 작업 처리를 계속하도록 지시하는 옵션을 설정할 수 있습니다. 설정할 수 있는 런타임 옵션에 대한 자세한 내용은 `AssemblerOptionSpec` 의 클래스 참조 [AEM Forms API 참조](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

**문서 암호화**

어셈블러 서비스 클라이언트를 만들고 암호화 정보가 포함된 DDX 문서를 참조하고 보안되지 않은 PDF 문서를 참조하며 런타임 옵션을 설정한 후 `invokeOneDocument` 작업. 한 개의 입력 PDF 문서만 어셈블러 서비스에 전달되고 있으며 한 문서는 반환되고 있으므로 `invokeOneDocument` 작업 대신 `invokeDDX` 작업.

**암호화된 PDF 문서 저장**

하나의 PDF 문서만 어셈블러 서비스에 전달되는 경우 어셈블러 서비스는 컬렉션 개체 대신 하나의 문서를 반환합니다. 즉, `invokeOneDocument` 단일 문서가 반환됩니다. 이 섹션에서 참조하는 DDX 문서에는 암호화 정보가 포함되어 있으므로 어셈블러 서비스는 암호로 암호화된 PDF 문서를 반환합니다.

**추가 참조**

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[프로그래밍 방식으로 PDF 문서 어셈블](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## Java API를 사용하여 암호화된 PDF 문서를 어셈블합니다 {#assemble-an-encrypted-pdf-document-using-the-java-api}

1. 프로젝트 파일을 포함합니다.

   Java 프로젝트의 클래스 경로에 adobe-assembler-client.jar과 같은 클라이언트 JAR 파일을 포함합니다.

1. 어셈블러 클라이언트를 만듭니다.

   * 만들기 `ServiceClientFactory` 연결 속성을 포함하는 개체입니다.
   * 만들기 `AssemblerServiceClient` 개체를 생성자를 사용하고 `ServiceClientFactory` 개체.

1. 기존 DDX 문서를 참조합니다.

   * 만들기 `java.io.FileInputStream` 생성자를 사용하고 DDX 파일의 위치를 지정하는 문자열 값을 전달하여 DDX 문서를 나타내는 개체입니다.
   * 만들기 `com.adobe.idp.Document` 개체를 생성자를 사용하고 `java.io.FileInputStream` 개체.

1. 보안되지 않은 PDF 문서를 참조합니다.

   * 만들기 `java.io.FileInputStream` 개체를 만들 때 생성자를 사용하고 보안되지 않은 PDF 문서의 위치를 전달합니다.
   * 만들기 `com.adobe.idp.Document` 개체 및 전달 `java.io.FileInputStream` PDF 문서가 포함된 객체입니다. 이 `com.adobe.idp.Document` 개체가 로 전달됨 `invokeOneDocument` 메서드를 사용합니다.

1. 런타임 옵션을 설정합니다.

   * 만들기 `AssemblerOptionSpec` 생성자를 사용하여 런타임 옵션을 저장하는 개체입니다.
   * 에 속한 메서드를 호출하여 비즈니스 요구 사항을 충족하도록 런타임 옵션을 설정합니다. `AssemblerOptionSpec` 개체. 예를 들어 오류가 발생할 때 어셈블러 서비스에서 작업 처리를 계속하도록 하려면 `AssemblerOptionSpec` 개체 `setFailOnError` 방법 및 통과 `false`.

1. 문서를 암호화합니다.

   호출 `AssemblerServiceClient` 개체 `invokeOneDocument` 메서드를 실행하고 다음 값을 전달합니다.

   * A `com.adobe.idp.Document` DDX 문서를 나타내는 개체입니다. 이 DDX 문서에 값이 포함되어 있는지 확인합니다. `inDoc` PDF 소스 요소용.
   * A `com.adobe.idp.Document` 비보안 PDF 문서가 포함된 개체입니다.
   * A `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` 기본 글꼴 및 작업 로그 수준을 포함하여 런타임 옵션을 지정하는 개체입니다.

   다음 `invokeOneDocument` 메서드가 을 반환합니다. `com.adobe.idp.Document` 암호로 암호화된 PDF 문서가 포함된 개체입니다.

1. 암호화된 PDF 문서를 저장합니다.

   * 만들기 `java.io.File` 개체를 클릭하고 파일 이름 확장명이 .pdf인지 확인합니다.
   * 호출 `Document` 개체 `copyToFile` 콘텐츠 복사 방법 `Document` 파일에 대한 개체입니다. 다음을 사용하는지 확인합니다. `Document` 이 속한 개체 `invokeOneDocument` 메서드가 반환되었습니다.

**추가 참조**

[빠른 시작(SOAP 모드): Java API를 사용하여 암호화된 PDF 문서 어셈블](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-assembling-an-encrypted-pdf-document-using-the-java-api)

## 웹 서비스 API를 사용하여 암호화된 PDF 문서를 어셈블합니다 {#assemble-an-encrypted-pdf-document-using-the-web-service-api}

1. 프로젝트 파일을 포함합니다.

   MTOM을 사용하는 Microsoft .NET 프로젝트를 만듭니다. 서비스 참조를 설정할 때 다음 WSDL 정의를 사용하는지 확인합니다. `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >바꾸기 `localhost` AEM Forms을 호스팅하는 서버의 IP 주소입니다.

1. 어셈블러 클라이언트를 만듭니다.

   * 만들기 `AssemblerServiceClient` 기본 생성자를 사용하여 개체를 작성합니다.
   * 만들기 `AssemblerServiceClient.Endpoint.Address` 을 사용하여 개체 `System.ServiceModel.EndpointAddress` 생성자입니다. WSDL을 지정하는 문자열 값을 AEM Forms 서비스에 전달합니다(예: `http://localhost:8080/soap/services/AssemblerService?blob=mtom`). 를 사용할 필요가 없습니다. `lc_version` 특성. 이 속성은 서비스 참조를 만들 때 사용됩니다.
   * 만들기 `System.ServiceModel.BasicHttpBinding` 의 값을 가져와서 개체 `AssemblerServiceClient.Endpoint.Binding` 필드. 반환 값을 다음으로 캐스트 `BasicHttpBinding`.
   * 설정 `System.ServiceModel.BasicHttpBinding` 개체 `MessageEncoding` 필드 대상 `WSMessageEncoding.Mtom`. 이 값은 MTOM이 사용되도록 합니다.
   * 다음 작업을 수행하여 기본 HTTP 인증을 활성화합니다.

      * 필드에 AEM Forms 사용자 이름 할당 `AssemblerServiceClient.ClientCredentials.UserName.UserName`.
      * 해당 암호 값을 필드에 할당합니다. `AssemblerServiceClient.ClientCredentials.UserName.Password`.
      * 상수 값 지정 `HttpClientCredentialType.Basic` 필드에 `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * 상수 값 지정 `BasicHttpSecurityMode.TransportCredentialOnly` 필드에 `BasicHttpBindingSecurity.Security.Mode`.

1. 기존 DDX 문서를 참조합니다.

   * 만들기 `BLOB` 개체를 만들 때 사용됩니다. 다음 `BLOB` 개체는 DDX 문서를 저장하는 데 사용됩니다.
   * 만들기 `System.IO.FileStream` 개체를 호출하고 DDX 문서의 파일 위치와 파일을 열 모드를 나타내는 문자열 값을 전달하여
   * 의 콘텐츠를 저장하는 바이트 배열 만들기 `System.IO.FileStream` 개체. 를 가져와서 바이트 배열의 크기를 결정할 수 있습니다 `System.IO.FileStream` 개체 `Length` 속성.
   * 를 호출하여 바이트 배열을 스트림 데이터로 채우기 `System.IO.FileStream` 개체 `Read` 바이트 배열, 시작 위치 및 읽을 스트림 길이를 전달하는 방법.
   * 채우기 `BLOB` 개체 할당 `MTOM` 바이트 배열의 내용이 있는 필드입니다.

1. 보안되지 않은 PDF 문서를 참조합니다.

   * 만들기 `BLOB` 개체를 만들 때 사용됩니다. 다음 `BLOB` 객체는 입력 PDF 문서를 저장하는 데 사용됩니다. 이 `BLOB` 개체가 로 전달됨 `invokeOneDocument` as a argument인수 .
   * 만들기 `System.IO.FileStream` 개체를 호출하고 입력 PDF 문서의 파일 위치와 파일을 열 모드를 나타내는 문자열 값을 전달합니다.
   * 의 콘텐츠를 저장하는 바이트 배열 만들기 `System.IO.FileStream` 개체. 를 가져와서 바이트 배열의 크기를 결정할 수 있습니다 `System.IO.FileStream` 개체 `Length` 속성.
   * 를 호출하여 바이트 배열을 스트림 데이터로 채우기 `System.IO.FileStream` 개체 `Read` 바이트 배열, 시작 위치 및 읽을 스트림 길이를 전달하는 방법.
   * 채우기 `BLOB` 개체 할당 `MTOM` 바이트 배열의 내용이 있는 필드입니다.

1. 런타임 옵션을 설정합니다.

   * 만들기 `AssemblerOptionSpec` 생성자를 사용하여 런타임 옵션을 저장하는 개체입니다.
   * 에 속한 데이터 멤버에 값을 할당하여 비즈니스 요구 사항을 충족하는 런타임 옵션을 설정합니다. `AssemblerOptionSpec` 개체. 예를 들어 오류가 발생할 때 어셈블러 서비스에서 작업 처리를 계속하도록 하려면 다음을 할당합니다 `false` (으)로 `AssemblerOptionSpec` 개체 `failOnError` 데이터 구성원입니다.

1. 문서를 암호화합니다.

   호출 `AssemblerServiceClient` 개체 `invokeOneDocument` 메서드를 실행하고 다음 값을 전달합니다.

   * A `BLOB` DDX 문서를 나타내는 개체입니다
   * A `BLOB` 비보안 PDF 문서를 나타내는 개체
   * An `AssemblerOptionSpec` 런타임 옵션을 지정하는 개체입니다

   다음 `invokeOneDocument` 메서드가 을 반환합니다. `BLOB` 암호화된 PDF 문서가 포함된 개체입니다.

1. 암호화된 PDF 문서를 저장합니다.

   * 만들기 `System.IO.FileStream` 개체를 호출하고 암호화된 PDF 문서의 파일 위치와 파일을 열 모드를 나타내는 문자열 값을 전달합니다.
   * 의 콘텐츠를 저장하는 바이트 배열 만들기 `BLOB` 이 속한 개체 `invokeOneDocument` 메서드가 반환되었습니다. 의 값을 가져와서 바이트 배열 채우기 `BLOB` 개체 `MTOM` 데이터 구성원입니다.
   * 만들기 `System.IO.BinaryWriter` 개체를 호출하고 `System.IO.FileStream` 개체.
   * 를 호출하여 바이트 배열의 내용을 PDF 파일에 씁니다 `System.IO.BinaryWriter` 개체 `Write` 메서드 및 바이트 배열 전달.

**추가 참조**

[MTOM을 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
