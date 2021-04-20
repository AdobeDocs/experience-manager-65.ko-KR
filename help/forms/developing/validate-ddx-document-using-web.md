---
title: 웹 서비스 API를 사용하여 DCX 문서 유효성 검사
seo-title: 웹 서비스 API를 사용하여 DCX 문서 유효성 검사
description: Assembler Service API를 사용하여 DDC 문서의 유효성을 확인합니다.
seo-description: Assembler Service API를 사용하여 DDC 문서의 유효성을 확인합니다.
uuid: f6125746-6138-4e46-a1c4-fb24fd7399c5
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/validating_ddx_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: a6fe91ab-3aa0-4b3d-87c0-6cf69a2c4cc4
role: Developer
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '659'
ht-degree: 0%

---


# 웹 서비스 API {#validate-a-ddx-document-using-theweb-service-api}을(를) 사용하여 DCX 문서의 유효성 검사

**이 문서의 샘플과 예는 JEE 환경의 AEM Forms에만 해당됩니다.**

Assembler Service API(웹 서비스)를 사용하여 DCX 문서의 유효성을 확인합니다.

1. 프로젝트 파일 포함

   MTOM을 사용하는 Microsoft .NET 프로젝트를 만듭니다. 다음 WSDL 정의를 사용해야 합니다.`http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >localhost를 양식 서버의 IP 주소로 바꿉니다.

1. PDF Assembler 클라이언트를 만듭니다.

   * 기본 생성자를 사용하여 `AssemblerServiceClient` 객체를 만듭니다.
   * `System.ServiceModel.EndpointAddress` 생성자를 사용하여 `AssemblerServiceClient.Endpoint.Address` 객체를 만듭니다. WSDL을 지정하는 문자열 값을 AEM Forms 서비스(예: `http://localhost:8080/soap/services/AssemblerService?blob=mtom`)에 전달합니다. `lc_version` 특성을 사용할 필요가 없습니다. 이 속성은 서비스 참조를 만들 때 사용됩니다.
   * `AssemblerServiceClient.Endpoint.Binding` 필드의 값을 가져와서 `System.ServiceModel.BasicHttpBinding` 개체를 만듭니다. 반환 값을 `BasicHttpBinding`으로 캐스팅합니다.
   * `System.ServiceModel.BasicHttpBinding` 개체의 `MessageEncoding` 필드를 `WSMessageEncoding.Mtom`로 설정합니다. 이 값을 사용하면 MTOM이 사용됩니다.
   * 다음 작업을 수행하여 기본 HTTP 인증을 활성화합니다.

      * AEM 양식 사용자 이름을 `AssemblerServiceClient.ClientCredentials.UserName.UserName` 필드에 지정합니다.
      * 해당 암호 값을 `AssemblerServiceClient.ClientCredentials.UserName.Password` 필드에 지정합니다.
      * `BasicHttpBindingSecurity.Transport.ClientCredentialType` 필드에 상수 값 `HttpClientCredentialType.Basic`을 할당합니다.
      * `BasicHttpBindingSecurity.Security.Mode` 필드에 상수 값 `BasicHttpSecurityMode.TransportCredentialOnly`을 할당합니다.

1. 기존 DCX 문서를 참조합니다.

   * 생성자를 사용하여 `BLOB` 객체를 만듭니다. `BLOB` 개체는 DCX 문서를 저장하는 데 사용됩니다.
   * 생성자를 호출하고 DCX 문서의 파일 위치 및 파일을 열 모드를 나타내는 문자열 값을 전달하여 `System.IO.FileStream` 객체를 만듭니다.
   * `System.IO.FileStream` 객체의 내용을 저장하는 바이트 배열을 만듭니다. `System.IO.FileStream` 객체의 `Length` 속성을 가져와 바이트 배열의 크기를 결정할 수 있습니다.
   * `System.IO.FileStream` 객체의 `Read` 메서드를 호출하고 바이트 배열, 시작 위치 및 읽을 스트림 길이를 전달하여 바이트 배열을 스트림 데이터로 채웁니다.
   * 바이트 배열의 내용으로 `MTOM` 속성을 할당하여 `BLOB` 객체를 채웁니다.

1. 런타임 옵션을 설정하여 DCX 문서의 유효성을 확인합니다.

   * 생성자를 사용하여 런타임 옵션을 저장하는 `AssemblerOptionSpec` 객체를 만듭니다.
   * 값을 `AssemblerOptionSpec` 개체의 `validateOnly` 데이터 멤버에 true를 할당하여 어셈블러 서비스에 DCX 문서의 유효성을 검사하도록 하는 런타임 옵션을 설정합니다.
   * 어셈블러 서비스가 로그 파일에 쓰는 정보의 양을 `AssemblerOptionSpec` 개체의 `logLevel` 데이터 멤버에 문자열 값을 할당하여 설정합니다. 메서드를 사용하여 DCX 문서의 유효성을 검사할 때 유효성 검사 프로세스를 지원할 로그 파일에 자세한 정보를 기록할 수 있습니다. 따라서 `FINE` 또는 `FINER` 값을 지정할 수 있습니다. 설정할 수 있는 런타임 옵션에 대한 자세한 내용은 [AEM Forms API 참조](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)의 `AssemblerOptionSpec` 클래스 참조를 참조하십시오.

1. 유효성 검사를 수행합니다.

   `AssemblerServiceClient` 객체의 `invokeDDX` 메서드를 호출하고 다음 값을 전달합니다.

   * DCX 문서를 나타내는 `BLOB` 객체입니다.
   * 일반적으로 PDF 문서를 저장하는 `Map` 개체에 대한 `null` 값입니다.
   * 런타임 옵션을 지정하는 `AssemblerOptionSpec` 객체입니다.

   `invokeDDX` 메서드는 DCX 문서의 유효성 여부를 지정하는 정보가 포함된 `AssemblerResult` 객체를 반환합니다.

1. 확인 결과를 로그 파일에 저장합니다.

   * 생성자를 호출하고 로그 파일의 파일 위치 및 파일을 열 모드를 나타내는 문자열 값을 전달하여 `System.IO.FileStream` 객체를 만듭니다. 파일 이름 확장자가 .xml인지 확인합니다.
   * `AssemblerResult` 개체의 `jobLog` 데이터 멤버의 값을 가져와 로그 정보를 저장하는 `BLOB` 개체를 만듭니다.
   * `BLOB` 객체의 내용을 저장하는 바이트 배열을 만듭니다. `BLOB` 객체의 `MTOM` 필드 값을 가져와 바이트 배열을 채웁니다.
   * 생성자를 호출하고 `System.IO.FileStream` 객체를 전달하여 `System.IO.BinaryWriter` 객체를 만듭니다.
   * `System.IO.BinaryWriter` 객체의 `Write` 메서드를 호출하고 바이트 배열을 전달하여 바이트 배열의 내용을 PDF 파일에 기록합니다.

   >[!NOTE]
   >
   >DCX 문서가 유효하지 않으면 `OperationException`이(가) 발생합니다. catch 문 내에서 `OperationException` 객체의 `jobLog` 멤버 값을 가져올 수 있습니다.

**참고 항목**

[DCX 문서 유효성 확인](/help/forms/developing/validating-ddx-documents.md#validating-ddx-documents)

[MTOM을 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
