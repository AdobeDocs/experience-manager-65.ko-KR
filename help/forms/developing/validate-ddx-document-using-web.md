---
title: 웹 서비스 API를 사용하여 DDX 문서의 유효성 검사
description: 어셈블러 서비스 API를 사용하여 DDX 문서의 유효성을 검사합니다.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/validating_ddx_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
role: Developer
exl-id: 069e5b10-ab93-4492-a70d-6a0d462105a6
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Document Services,APIs & Integrations
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '634'
ht-degree: 0%

---

# 웹 서비스 API를 사용하여 DDX 문서의 유효성 검사 {#validate-a-ddx-document-using-theweb-service-api}

**이 문서의 샘플과 예제는 JEE 환경의 AEM Forms에 대해서만 적용됩니다.**

어셈블러 서비스 API(웹 서비스)를 사용하여 DDX 문서의 유효성을 검사합니다.

1. 프로젝트 파일을 포함합니다.

   MTOM을 사용하는 Microsoft .NET 프로젝트를 만듭니다. WSDL 정의 `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`을(를) 사용하는지 확인하십시오.

   >[!NOTE]
   >
   >localhost를 Forms 서버의 IP 주소로 바꿉니다.

1. PDF 어셈블러 클라이언트를 만듭니다.

   * 기본 생성자를 사용하여 `AssemblerServiceClient` 개체를 만듭니다.
   * `System.ServiceModel.EndpointAddress` 생성자를 사용하여 `AssemblerServiceClient.Endpoint.Address` 개체를 만듭니다. WSDL을 지정하는 문자열 값을 AEM Forms 서비스에 전달합니다(예: `http://localhost:8080/soap/services/AssemblerService?blob=mtom`). `lc_version` 특성은 사용할 필요가 없습니다. 이 속성은 서비스 참조를 만들 때 사용됩니다.
   * `AssemblerServiceClient.Endpoint.Binding` 필드의 값을 가져와 `System.ServiceModel.BasicHttpBinding` 개체를 만듭니다. 반환 값을 `BasicHttpBinding`(으)로 캐스팅합니다.
   * `System.ServiceModel.BasicHttpBinding` 개체의 `MessageEncoding` 필드를 `WSMessageEncoding.Mtom`(으)로 설정합니다. 이 값은 MTOM이 사용되도록 합니다.
   * 다음 작업을 수행하여 기본 HTTP 인증을 활성화합니다.

      * `AssemblerServiceClient.ClientCredentials.UserName.UserName` 필드에 AEM Forms 사용자 이름을 지정하십시오.
      * 필드 `AssemblerServiceClient.ClientCredentials.UserName.Password`에 해당 암호 값을 지정하십시오.
      * 상수 값 `HttpClientCredentialType.Basic`을(를) 필드 `BasicHttpBindingSecurity.Transport.ClientCredentialType`에 할당합니다.
      * 상수 값 `BasicHttpSecurityMode.TransportCredentialOnly`을(를) 필드 `BasicHttpBindingSecurity.Security.Mode`에 할당합니다.

1. 기존 DDX 문서를 참조합니다.

   * 해당 생성자를 사용하여 `BLOB` 개체를 만듭니다. `BLOB` 개체는 DDX 문서를 저장하는 데 사용됩니다.
   * 해당 생성자를 호출하고 DDX 문서의 파일 위치와 파일을 열 모드를 나타내는 문자열 값을 전달하여 `System.IO.FileStream` 개체를 만듭니다.
   * `System.IO.FileStream` 개체의 내용을 저장하는 바이트 배열을 만듭니다. `System.IO.FileStream` 개체의 `Length` 속성을 가져와서 바이트 배열의 크기를 결정할 수 있습니다.
   * `System.IO.FileStream` 개체의 `Read` 메서드를 호출하고 바이트 배열, 시작 위치 및 읽을 스트림 길이를 전달하여 바이트 배열을 스트림 데이터로 채웁니다.
   * 해당 `MTOM` 속성을 바이트 배열의 내용으로 할당하여 `BLOB` 개체를 채웁니다.

1. 런타임 옵션을 설정하여 DDX 문서의 유효성을 검사합니다.

   * 생성자를 사용하여 런타임 옵션을 저장하는 `AssemblerOptionSpec` 개체를 만듭니다.
   * `AssemblerOptionSpec` 개체의 `validateOnly` 데이터 멤버에 true 값을 할당하여 어셈블러 서비스에 DDX 문서의 유효성을 검사하도록 지시하는 런타임 옵션을 설정하십시오.
   * `AssemblerOptionSpec` 개체의 `logLevel` 데이터 멤버에 문자열 값을 할당하여 어셈블러 서비스에서 로그 파일에 쓰는 정보의 양을 설정하십시오. 메서드 DDX 문서의 유효성을 검사할 때 유효성 검사 프로세스에 도움이 되도록 로그 파일에 자세한 정보를 기록해야 합니다. 따라서 값 `FINE` 또는 `FINER`을(를) 지정할 수 있습니다. 설정할 수 있는 런타임 옵션에 대한 자세한 내용은 [AEM Forms API 참조](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)의 `AssemblerOptionSpec` 클래스 참조를 참조하십시오.

1. 유효성 검사를 수행합니다.

   `AssemblerServiceClient` 개체의 `invokeDDX` 메서드를 호출하고 다음 값을 전달하십시오.

   * DDX 문서를 나타내는 `BLOB` 개체입니다.
   * 일반적으로 PDF 문서를 저장하는 `Map` 개체의 값 `null`입니다.
   * 런타임 옵션을 지정하는 `AssemblerOptionSpec` 개체입니다.

   `invokeDDX` 메서드는 DDX 문서가 유효한지 여부를 지정하는 정보가 포함된 `AssemblerResult` 개체를 반환합니다.

1. 로그 파일에 유효성 검사 결과를 저장합니다.

   * 해당 생성자를 호출하고 로그 파일의 파일 위치와 파일을 열 모드를 나타내는 문자열 값을 전달하여 `System.IO.FileStream` 개체를 만듭니다. 파일 이름 확장명이 .xml인지 확인합니다.
   * `AssemblerResult` 개체의 `jobLog` 데이터 멤버의 값을 가져와서 로그 정보를 저장하는 `BLOB` 개체를 만듭니다.
   * `BLOB` 개체의 내용을 저장하는 바이트 배열을 만듭니다. `BLOB` 개체의 `MTOM` 필드 값을 가져와서 바이트 배열을 채웁니다.
   * 해당 생성자를 호출하고 `System.IO.FileStream` 개체를 전달하여 `System.IO.BinaryWriter` 개체를 만듭니다.
   * `System.IO.BinaryWriter` 개체의 `Write` 메서드를 호출하고 바이트 배열을 전달하여 바이트 배열의 내용을 PDF 파일에 씁니다.

   >[!NOTE]
   >
   >DDX 문서가 올바르지 않으면 `OperationException`이(가) throw됩니다. catch 문 내에서 `OperationException` 개체의 `jobLog` 멤버 값을 가져올 수 있습니다.

**추가 참조**

[DDX 문서 검증](/help/forms/developing/validating-ddx-documents.md#validating-ddx-documents)

[MTOM을 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
