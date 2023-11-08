---
title: 웹 서비스 API를 사용하여 DDX 문서의 유효성 검사
seo-title: Validate a DDX document using theweb service API
description: 어셈블러 서비스 API를 사용하여 DDX 문서의 유효성을 검사합니다.
seo-description: Use the Assembler Service API to validate a DDX document.
uuid: f6125746-6138-4e46-a1c4-fb24fd7399c5
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/validating_ddx_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: a6fe91ab-3aa0-4b3d-87c0-6cf69a2c4cc4
role: Developer
exl-id: 069e5b10-ab93-4492-a70d-6a0d462105a6
source-git-commit: c4cd9a61a226ace2a72d60b5b7b7432de12cb873
workflow-type: tm+mt
source-wordcount: '640'
ht-degree: 0%

---

# 웹 서비스 API를 사용하여 DDX 문서의 유효성 검사 {#validate-a-ddx-document-using-theweb-service-api}

**이 문서의 샘플 및 예제는 JEE 환경의 AEM Forms에 대해서만 적용됩니다.**

어셈블러 서비스 API(웹 서비스)를 사용하여 DDX 문서의 유효성을 검사합니다.

1. 프로젝트 파일을 포함합니다.

   MTOM을 사용하는 Microsoft .NET 프로젝트를 만듭니다. 다음 WSDL 정의를 사용하는지 확인합니다. `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >localhost를 Forms 서버의 IP 주소로 바꿉니다.

1. PDF 어셈블러 클라이언트를 만듭니다.

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
   * 채우기 `BLOB` 개체 할당 `MTOM` 속성을 바이트 배열의 콘텐츠와 함께 사용합니다.

1. 런타임 옵션을 설정하여 DDX 문서의 유효성을 검사합니다.

   * 만들기 `AssemblerOptionSpec` 생성자를 사용하여 런타임 옵션을 저장하는 개체입니다.
   * true 값을 로 할당하여 어셈블러 서비스에서 DDX 문서의 유효성을 검사하도록 지시하는 런타임 옵션을 설정합니다. `AssemblerOptionSpec` 개체 `validateOnly` 데이터 구성원입니다.
   * 문자열 값을 로 할당하여 어셈블러 서비스에서 로그 파일에 쓰는 정보의 양을 설정합니다. `AssemblerOptionSpec` 개체 `logLevel` 데이터 구성원입니다. 메서드 DDX 문서의 유효성을 검사할 때 유효성 검사 프로세스에 도움이 되도록 로그 파일에 자세한 정보를 기록해야 합니다. 따라서 값을 지정할 수 있습니다 `FINE` 또는 `FINER`. 설정할 수 있는 런타임 옵션에 대한 자세한 내용은 `AssemblerOptionSpec` 의 클래스 참조 [AEM Forms API 참조](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

1. 유효성 검사를 수행합니다.

   호출 `AssemblerServiceClient` 개체 `invokeDDX` 메서드를 실행하고 다음 값을 전달합니다.

   * A `BLOB` DDX 문서를 나타내는 개체입니다.
   * 값 `null` 대상: `Map` 일반적으로 PDF 문서를 저장하는 객체입니다.
   * An `AssemblerOptionSpec` 런타임 옵션을 지정하는 개체입니다.

   다음 `invokeDDX` 메서드가 다음을 반환합니다. `AssemblerResult` DDX 문서가 유효한지 여부를 지정하는 정보가 포함된 개체입니다.

1. 로그 파일에 유효성 검사 결과를 저장합니다.

   * 만들기 `System.IO.FileStream` 개체를 호출하고 로그 파일의 파일 위치와 파일을 열 모드를 나타내는 문자열 값을 전달합니다. 파일 이름 확장명이 .xml인지 확인합니다.
   * 만들기 `BLOB` 값을 가져와서 로그 정보를 저장하는 개체 `AssemblerResult` 개체 `jobLog` 데이터 구성원입니다.
   * 의 콘텐츠를 저장하는 바이트 배열 만들기 `BLOB` 개체. 의 값을 가져와서 바이트 배열 채우기 `BLOB` 개체 `MTOM` 필드.
   * 만들기 `System.IO.BinaryWriter` 개체를 호출하고 `System.IO.FileStream` 개체.
   * 를 호출하여 바이트 배열의 내용을 PDF 파일에 씁니다 `System.IO.BinaryWriter` 개체 `Write` 메서드 및 바이트 배열 전달.

   >[!NOTE]
   >
   >DDX 문서가 유효하지 않은 경우 `OperationException` 이 throw됩니다. catch 문 내에서 `OperationException` 개체 `jobLog` 멤버.

**추가 참조**

[DDX 문서 검증](/help/forms/developing/validating-ddx-documents.md#validating-ddx-documents)

[MTOM을 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
