---
title: 웹 서비스 API를 사용하여 PDF 문서 디스어셈블
description: 어셈블러 서비스 API를 사용하여 PDF 문서를 디스어셈블합니다.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/programmatically_disassembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
role: Developer
exl-id: de2f90ad-5dea-40a0-8c6d-d6b08228310d
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '718'
ht-degree: 0%

---

# 웹 서비스 API를 사용하여 PDF 문서 디스어셈블 {#disassemble-a-pdf-document-usingthe-web-service-api}

**이 문서의 샘플 및 예제는 JEE 환경의 AEM Forms에 대해서만 적용됩니다.**

어셈블러 서비스 API(웹 서비스)를 사용하여 PDF 문서를 디스어셈블합니다.

1. 프로젝트 파일을 포함합니다.

   MTOM을 사용하는 Microsoft .NET 프로젝트를 만듭니다. 서비스 참조를 설정할 때 다음 WSDL 정의를 사용하는지 확인합니다. `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >바꾸기 `localhost` AEM Forms을 호스팅하는 서버의 IP 주소입니다.

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
   * 만들기 `System.IO.FileStream` 해당 생성자를 호출하여 개체를 작성합니다. DDX 문서의 파일 위치와 파일을 열 모드를 나타내는 문자열 값을 전달합니다.
   * 의 콘텐츠를 저장하는 바이트 배열 만들기 `System.IO.FileStream` 개체. 를 가져와서 바이트 배열의 크기를 결정할 수 있습니다 `System.IO.FileStream` 개체 `Length` 속성.
   * 를 호출하여 바이트 배열을 스트림 데이터로 채우기 `System.IO.FileStream` 개체 `Read` 바이트 배열, 시작 위치 및 읽을 스트림 길이를 전달하는 방법.
   * 채우기 `BLOB` 개체 할당 `MTOM` 속성을 바이트 배열의 콘텐츠와 함께 사용합니다.

1. 분해하려면 PDF 문서를 참조합니다.

   * 만들기 `BLOB` 개체를 만들 때 사용됩니다. 다음 `BLOB` 객체는 입력 PDF 문서를 저장하는 데 사용됩니다. 이 `BLOB` 개체가 로 전달됨 `invokeOneDocument` as a argument인수 .
   * 만들기 `System.IO.FileStream` 개체를 호출하고 입력 PDF 문서의 파일 위치와 파일을 열 모드를 나타내는 문자열 값을 전달합니다.
   * 의 콘텐츠를 저장하는 바이트 배열 만들기 `System.IO.FileStream` 개체. 를 가져와서 바이트 배열의 크기를 결정할 수 있습니다 `System.IO.FileStream` 개체 `Length` 속성.
   * 를 호출하여 바이트 배열을 스트림 데이터로 채우기 `System.IO.FileStream` 개체 `Read` 바이트 배열, 시작 위치 및 읽을 스트림 길이를 전달하는 방법.
   * 채우기 `BLOB` 개체 할당 `MTOM` 바이트 배열의 내용을 입력합니다.
   * 만들기 `MyMapOf_xsd_string_To_xsd_anyType` 개체. 이 컬렉션 개체는 분해할 PDF을 저장하는 데 사용됩니다.
   * 만들기 `MyMapOf_xsd_string_To_xsd_anyType_Item` 개체.
   * 키 이름을 나타내는 문자열 값을 `MyMapOf_xsd_string_To_xsd_anyType_Item` 개체 `key` 필드. 이 값은 DDX 문서에 지정된 PDF 원본 요소의 값과 일치해야 합니다.
   * 할당 `BLOB` 에 PDF 문서를 저장하는 개체 `MyMapOf_xsd_string_To_xsd_anyType_Item` 개체 `value` 필드.
   * 추가 `MyMapOf_xsd_string_To_xsd_anyType_Item` 에 대한 오브젝트 `MyMapOf_xsd_string_To_xsd_anyType` 개체. 호출 `MyMapOf_xsd_string_To_xsd_anyType` 개체 `Add` 메서드 및 전달 `MyMapOf_xsd_string_To_xsd_anyType` 개체.

1. 런타임 옵션을 설정합니다.

   * 만들기 `AssemblerOptionSpec` 생성자를 사용하여 런타임 옵션을 저장하는 개체입니다.
   * 에 속한 데이터 멤버에 값을 할당하여 비즈니스 요구 사항을 충족하는 런타임 옵션을 설정합니다. `AssemblerOptionSpec` 개체. 예를 들어 오류가 발생할 때 어셈블러 서비스에서 작업 처리를 계속하도록 하려면 다음을 할당합니다 `false` (으)로 `AssemblerOptionSpec` 개체 `failOnError` 필드.

1. PDF 문서를 디스어셈블합니다.

   호출 `AssemblerServiceClient` 개체 `invokeDDX` 메서드를 실행하고 다음 값을 전달합니다.

   * A `BLOB` PDF 문서를 디스어셈블하는 DDX 문서를 나타내는 개체입니다
   * 다음 `MyMapOf_xsd_string_To_xsd_anyType` 분해할 PDF 문서가 포함된 개체
   * An `AssemblerOptionSpec` 런타임 옵션을 지정하는 개체입니다

   다음 `invokeDDX` 메서드가 다음을 반환합니다. `AssemblerResult` 작업 결과와 발생한 예외를 포함하는 객체입니다.

1. 분해된 PDF 문서를 저장합니다.

   새로 생성된 PDF 문서를 가져오려면 다음 작업을 수행합니다.

   * 액세스 `AssemblerResult` 개체 `documents` 필드: `Map` 분해된 PDF 문서가 포함된 객체입니다.
   * 다음을 반복합니다. `Map` 객체를 사용하여 각 결과 문서를 가져올 수 있습니다. 그런 다음 해당 배열 멤버의 `value` (으)로 `BLOB`.
   * 에 액세스하여 PDF 문서를 나타내는 이진 데이터 추출 `BLOB` 개체 `MTOM` 속성. PDF 파일에 쓸 수 있는 바이트 배열이 반환됩니다.

**추가 참조**

[프로그래밍 방식으로 PDF 문서 디스어셈블](/help/forms/developing/programmatically-disassembling-pdf-documents.md#programmatically-disassembling-pdf-documents)

[MTOM을 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
