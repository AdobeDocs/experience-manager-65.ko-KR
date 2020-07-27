---
title: PDF 포트폴리오 취합
seo-title: PDF 포트폴리오 취합
description: 'null'
seo-description: 'null'
uuid: 1778c90b-9d26-466b-a7c7-401d737395e0
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 023f0d9e-bfde-4879-a839-085fadffb48e
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '1785'
ht-degree: 0%

---


# PDF 포트폴리오 취합 {#assembling-pdf-portfolios}

어셈블러 Java 및 웹 서비스 API를 사용하여 PDF 포트폴리오를 취합할 수 있습니다. 포트폴리오는 워드 파일, 이미지 파일(예: jpeg 파일), PDF 문서 등 다양한 유형의 여러 문서를 결합할 수 있습니다. 포트폴리오의 레이아웃은 미리 보기를 통해 *격자*, 이미지 *에서 레이아웃* 또는 회전 *과 같은 다양한 스타일로 설정할 수*&#x200B;있습니다.

다음 그림은 이미지 스타일 레이아웃이 있는 포트폴리오 *의* 스크린샷입니다.

![ap_ap_portfolio](assets/ap_ap_portfolio.png)

PDF 포트폴리오를 만드는 것은 문서 모음을 전달하는 데 있어 종이가 필요 없는 대안으로 사용할 수 있습니다. AEM Forms을 사용하면 구조화된 DDC 문서를 포함하는 어셈블러 서비스를 호출하여 포트폴리오를 만들 수 있습니다. 다음 DCX 문서는 PDF 포트폴리오를 만드는 DDX 문서의 예입니다.

```xml
 <DDX xmlns="https://ns.adobe.com/DDX/1.0/">
     <PDF result="portfolio1.pdf">
         <Portfolio>
             <Navigator source="myNavigator">
                 <Resource name="navigator/image.xxx" source="myImage.png"/>
             </Navigator>
         </Portfolio>
         <PackageFiles source="dog1"  >
              <FieldData name="X">72</FieldData>
             <FieldData name="Y">72</FieldData>
             <File filename="saint_bernard.jpg" mimetype="image/jpeg"/>
         </PackageFiles>
         <PackageFiles source="dog2"  >
             <FieldData name="X">120</FieldData>
             <FieldData name="Y">216</FieldData>
             <File filename="greyhound.pdf"/>
         </PackageFiles>
     </PDF>
 </DDX>
```

DXX 문서에는 중첩된 `Portfolio` 태그가 포함된 `Navigator` 태그가 포함되어야 합니다. 태그 `<Resource name="navigator/image.xxx" source="myImage.png"/>` 는 onImage 레이아웃 탐색기 `myNavigator` 로 지정된 경우에만 필요합니다. `AdobeOnImage.nav`. 이 태그를 사용하면 어셈블러 서비스가 포트폴리오 배경으로 사용할 이미지를 선택할 수 있습니다. 패키지된 파일의 파일 이름 및 MIME 유형을 정의하는 `PackageFiles` 및 `File` 태그를 포함합니다.

>[!NOTE]
>
>어셈블러 서비스에 대한 자세한 내용은 AEM Forms에 대한 [서비스 참조를 참조하십시오](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>DDX 문서에 대한 자세한 내용은 어셈블러 서비스 [및 DDX 참조를 참조하십시오](https://www.adobe.com/go/learn_aemforms_ddx_63).

## 단계 요약 {#summary-of-steps}

PDF 포트폴리오를 만들려면 다음 작업을 수행하십시오.

1. 프로젝트 파일 포함
1. PDF 어셈블러 클라이언트 만들기
1. 기존 DDX 문서를 참조합니다.
1. 필요한 문서를 참조하십시오.
1. 런타임 옵션을 설정합니다.
1. 포트폴리오 취합
1. 취합된 포트폴리오를 저장합니다.

**프로젝트 파일 포함**

개발 프로젝트에 필요한 파일을 포함합니다. Java를 사용하여 클라이언트 응용 프로그램을 만드는 경우 필요한 JAR 파일을 포함합니다. 웹 서비스를 사용하는 경우 프록시 파일을 포함해야 합니다.

프로젝트의 클래스 경로에 다음 JAR 파일을 추가해야 합니다.

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar(AEM Forms이 JBoss에 배포된 경우 필요)
* jbossall-client.jar(AEM Forms이 JBoss에 배포된 경우 필요)

**PDF 어셈블러 클라이언트 만들기**

어셈블리 작업을 프로그래밍 방식으로 수행하려면 먼저 어셈블러 서비스 클라이언트를 만듭니다.

**기존 DCX 문서 참조**

PDF 포트폴리오를 취합하려면 DCX 문서를 참조해야 합니다. 이 DDX 문서에는 `Portfolio`및 `Navigator` 및 `PackageFiles` 요소가 포함되어야 합니다.

**필요한 문서 참조**

PDF 포트폴리오를 취합하려면 취합할 문서를 나타내는 모든 파일을 참조합니다. 예를 들어 DDX 문서에 지정된 모든 이미지 파일을 어셈블러 서비스로 전달합니다. 이러한 파일은 이 섹션에 지정된 DCX 문서에서 참조됩니다. *myImage.png* 및 *saint_bernard.jpg*.

PDF 포트폴리오를 취합할 때 NAV 파일(네비게이터 파일)을 어셈블러 서비스에 전달합니다. 어셈블러 서비스로 전달하는 NAV 파일은 만들 PDF 포트폴리오의 유형에 따라 달라집니다. 예를 들어 이미지 *에서* 레이아웃을 만들려면 AdobeOnImage.nav 파일을 전달합니다. 다음 폴더에서 NAV 파일을 찾을 수 있습니다.

`<Install folder>\Acrobat 9.0\Acrobat\Navigators`

Acrobat 9 이상 설치 디렉토리에서 NAV 파일을 복사합니다. 클라이언트 응용 프로그램이 액세스할 수 있는 위치에 NAV 파일을 배치합니다. 모든 파일은 맵 컬렉션 개체 내의 어셈블러 서비스로 전달됩니다.

>[!NOTE]
>
>PDF 포트폴리오 취합 관련 빠른 시작은 AdobeOnImage.nav를 사용합니다.

**런타임 옵션 설정**

작업을 수행하는 동안 어셈블러 서비스의 동작을 제어하는 런타임 옵션을 설정할 수 있습니다. 예를 들어 오류가 발생한 경우 어셈블리 서비스에서 작업을 계속 처리하도록 하는 옵션을 설정할 수 있습니다.

**포트폴리오 취합**

PDF 포트폴리오를 취합하려면 작업을 `invokeDDX` 호출합니다. 어셈블러 서비스는 컬렉션 개체 내의 PDF 포트폴리오를 반환합니다.

**어셈블된 포트폴리오 저장**

컬렉션 개체 내에서 PDF 포트폴리오가 반환됩니다. 컬렉션 개체를 반복하고 PDF 포트폴리오를 PDF 파일로 저장할 수 있습니다.

**참고 항목**

[Java API를 사용하여 PDF 포트폴리오 취합](#assemble-a-pdf-portfolio-using-the-java-api)

[웹 서비스 API를 사용하여 PDF 포트폴리오 취합](#assemble-a-pdf-portfolio-using-the-web-service-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[프로그래밍 방식으로 PDF 문서 취합](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## Java API를 사용하여 PDF 포트폴리오 취합 {#assemble-a-pdf-portfolio-using-the-java-api}

Assembler Service API(Java)를 사용하여 PDF 포트폴리오를 조합합니다.

1. 프로젝트 파일 포함

   Java 프로젝트의 클래스 경로에 adobe-assembler-client.jar와 같은 클라이언트 JAR 파일을 포함합니다.

1. PDF 어셈블러 클라이언트 만들기

   * 연결 속성을 포함하는 `ServiceClientFactory` 개체를 만듭니다.
   * 생성자를 사용하여 개체를 `AssemblerServiceClient` 만들고 개체를 `ServiceClientFactory` 전달합니다.

1. 기존 DDX 문서를 참조합니다.

   * 생성자를 사용하여 DCX 문서를 나타내는 `java.io.FileInputStream` 개체를 만들고 DDX 파일의 위치를 지정하는 문자열 값을 전달합니다.
   * 생성자를 사용하여 개체를 `com.adobe.idp.Document` 만들고 개체를 `java.io.FileInputStream` 전달합니다.

1. 필요한 문서를 참조하십시오.

   * 생성자를 사용하여 입력 PDF 문서를 저장하는 데 사용되는 `java.util.Map` 개체를 `HashMap` 만듭니다.
   * 생성자를 사용하여 `java.io.FileInputStream` 개체를 만듭니다. 필요한 NAV 파일의 위치를 전달합니다. 포트폴리오를 만드는 데 필요한 각 파일에 대해 이 작업을 반복합니다.
   * 개체를 만들고 NAV 파일이 포함된 `com.adobe.idp.Document` `java.io.FileInputStream` 개체를 전달합니다(포트폴리오를 만드는 데 필요한 각 파일에 대해 이 작업을 반복합니다).
   * 해당 메서드를 호출하고 다음 인수를 전달하여 `java.util.Map` 개체에 `put` 항목을 추가합니다.

      * 키 이름을 나타내는 문자열 값입니다. 이 값은 DDX 문서에 지정된 소스 요소의 값과 일치해야 합니다. 포트폴리오를 만드는 데 필요한 각 파일에 대해 이 작업을 반복합니다.
      * PDF 문서를 포함하는 `com.adobe.idp.Document` 오브젝트입니다. 포트폴리오를 만드는 데 필요한 각 파일에 대해 이 작업을 반복합니다.

1. 런타임 옵션을 설정합니다.

   * 생성자를 사용하여 런타임 옵션을 저장하는 `AssemblerOptionSpec` 객체를 만듭니다.
   * 개체에 속하는 메서드를 호출하여 비즈니스 요구 사항에 맞게 런타임 옵션을 `AssemblerOptionSpec` 설정합니다. 예를 들어 오류가 발생할 때 어셈블리 서비스에서 작업을 계속 처리하도록 지정하려면 `AssemblerOptionSpec` 개체의 `setFailOnError` 메서드를 호출하고 전달합니다 `false`.

1. 포트폴리오 취합

   개체의 `AssemblerServiceClient` `invokeDDX` 메서드를 호출하고 다음 필수 값을 전달합니다.

   * 사용할 DCX 문서를 나타내는 `com.adobe.idp.Document` 개체
   * PDF 포트폴리오를 작성하는 데 필요한 파일이 포함된 `java.util.Map` 개체입니다.
   * 기본 글꼴 및 작업 로그 수준을 포함하여 런타임 옵션을 지정하는 `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` 개체

   이 `invokeDDX` `com.adobe.livecycle.assembler.client.AssemblerResult` 메서드는 조합된 PDF 포트폴리오와 발생한 모든 예외가 포함된 개체를 반환합니다.

1. 취합된 포트폴리오를 저장합니다.

   PDF 포트폴리오를 얻으려면 다음 작업을 수행하십시오.

   * 개체의 `AssemblerResult` 메서드를 `getDocuments` 호출합니다. 이 메서드는 `java.util.Map` 개체를 반환합니다.
   * 결과 개체를 찾을 때까지 개체 `java.util.Map` 를 반복하십시오 `com.adobe.idp.Document` .
   * 오브젝트의 `com.adobe.idp.Document` 방법을 불러와 PDF `copyToFile` 포트폴리오를 추출합니다.

**참고 항목**

[빠른 시작(SOAP 모드): Java API를 사용하여 PDF 포트폴리오 취합](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-assembling-pdf-portfolios-using-the-java-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 웹 서비스 API를 사용하여 PDF 포트폴리오 취합 {#assemble-a-pdf-portfolio-using-the-web-service-api}

Assembler Service API(웹 서비스)를 사용하여 PDF 포트폴리오를 조합합니다.

1. 프로젝트 파일 포함

   MTOM을 사용하는 Microsoft .NET 프로젝트를 만듭니다. 서비스 참조를 설정할 때 다음 WSDL 정의를 사용해야 합니다. `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >AEM Forms `localhost` 를 호스팅하는 서버의 IP 주소로 대체합니다.

1. PDF 어셈블러 클라이언트 만들기

   * 기본 생성자를 사용하여 `AssemblerServiceClient` 개체를 만듭니다.
   * 생성자를 사용하여 `AssemblerServiceClient.Endpoint.Address` 개체를 `System.ServiceModel.EndpointAddress` 만듭니다. WSDL을 지정하는 문자열 값을 AEM Forms 서비스에 전달합니다(예: `http://localhost:8080/soap/services/AssemblerService?blob=mtom`). 속성을 사용할 필요는 `lc_version` 없습니다. 이 속성은 서비스 참조를 만들 때 사용됩니다.
   * 필드의 값을 `System.ServiceModel.BasicHttpBinding` 가져와 개체를 `AssemblerServiceClient.Endpoint.Binding` 만듭니다. 반환 값을 다음으로 캐스팅합니다 `BasicHttpBinding`.
   * 개체 `System.ServiceModel.BasicHttpBinding` 필드를 (으)로 `MessageEncoding` 설정합니다 `WSMessageEncoding.Mtom`. 이 값을 사용하면 MTOM이 사용됩니다.
   * 다음 작업을 수행하여 기본 HTTP 인증을 활성화합니다.

      * 필드에 AEM 양식 사용자 이름을 지정합니다 `AssemblerServiceClient.ClientCredentials.UserName.UserName`.
      * 해당 암호 값을 필드에 지정합니다 `AssemblerServiceClient.ClientCredentials.UserName.Password`.
      * 필드에 상수 값 `HttpClientCredentialType.Basic` 을 지정합니다 `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * 필드에 상수 값 `BasicHttpSecurityMode.TransportCredentialOnly` 을 지정합니다 `BasicHttpBindingSecurity.Security.Mode`.

1. 기존 DDX 문서를 참조합니다.

   * 생성자를 사용하여 `BLOB` 개체를 만듭니다. 이 `BLOB` 개체는 DDX 문서를 저장하는 데 사용됩니다.
   * 생성자를 호출하고 DDX 문서의 파일 위치와 파일을 열 모드를 나타내는 문자열 값을 전달하여 `System.IO.FileStream` 개체를 만듭니다.
   * 개체의 내용을 저장하는 바이트 배열을 `System.IO.FileStream` 만듭니다. 개체의 속성을 가져와 바이트 배열의 크기를 결정할 수 `System.IO.FileStream` `Length` 있습니다.
   * 개체의 메서드를 호출하여 바이트 배열을 스트림 데이터로 `System.IO.FileStream` 채웁니다 `Read` . 바이트 배열, 시작 위치 및 스트림 길이를 전달합니다.
   * 바이트 배열의 컨텐츠로 해당 `BLOB` `MTOM` 속성을 지정하여 개체를 채웁니다.

1. 필요한 문서를 참조하십시오.

   * 각 입력 파일에 대해 생성자를 사용하여 `BLOB` 개체를 만듭니다. 이 `BLOB` 개체는 입력 파일을 저장하는 데 사용됩니다.
   * 생성자를 호출하고 입력 파일의 파일 위치와 파일을 열 모드를 나타내는 문자열 값을 전달하여 `System.IO.FileStream` 개체를 만듭니다.
   * 개체의 내용을 저장하는 바이트 배열을 `System.IO.FileStream` 만듭니다. 개체의 속성을 가져와 바이트 배열의 크기를 결정할 수 `System.IO.FileStream` `Length` 있습니다.
   * 개체의 메서드를 호출하여 바이트 배열을 스트림 데이터로 `System.IO.FileStream` 채웁니다 `Read` . 바이트 배열, 시작 위치 및 스트림 길이를 전달합니다.
   * 바이트 배열의 내용으로 해당 `BLOB` `MTOM` 필드를 할당하여 개체를 채웁니다.
   * 개체를 `MyMapOf_xsd_string_To_xsd_anyType` 만듭니다. 이 컬렉션 개체는 PDF 포트폴리오를 만드는 데 필요한 입력 파일을 저장하는 데 사용됩니다.
   * 각 입력 파일에 대해 `MyMapOf_xsd_string_To_xsd_anyType_Item` 개체를 만듭니다.
   * 키 이름을 나타내는 문자열 값을 `MyMapOf_xsd_string_To_xsd_anyType_Item` 개체의 `key` 필드에 할당합니다. 이 값은 DDX 문서에 지정된 요소의 값과 일치해야 합니다. 각 입력 파일에 대해 이 작업을 수행합니다.
   * 입력 파일을 저장하는 `BLOB` 객체를 `MyMapOf_xsd_string_To_xsd_anyType_Item` 객체 `value` 필드에 지정합니다. 각 입력 PDF 문서에 대해 이 작업을 수행합니다.
   * 개체에 `MyMapOf_xsd_string_To_xsd_anyType_Item` 개체를 `MyMapOf_xsd_string_To_xsd_anyType` 추가합니다. 개체의 `MyMapOf_xsd_string_To_xsd_anyType` 메서드를 호출하고 개체를 `Add` `MyMapOf_xsd_string_To_xsd_anyType` 전달합니다. 각 입력 PDF 문서에 대해 이 작업을 수행합니다.

1. 런타임 옵션을 설정합니다.

   * 생성자를 사용하여 런타임 옵션을 저장하는 `AssemblerOptionSpec` 객체를 만듭니다.
   * 객체에 속하는 데이터 멤버에 값을 할당하여 비즈니스 요구 사항에 맞게 런타임 옵션을 `AssemblerOptionSpec` 설정합니다. 예를 들어 오류가 발생할 때 어셈블리 서비스에서 작업을 계속 처리하도록 지정하려면 개체 `false` 의 `AssemblerOptionSpec` 데이터 `failOnError` 멤버에 할당합니다.

1. 포트폴리오 취합

   개체의 `AssemblerServiceClient` 메서드를 `invokeDDX` 호출하고 다음 값을 전달합니다.

   * DCX 문서를 나타내는 `BLOB` 개체
   * 필수 파일이 포함된 `MyMapOf_xsd_string_To_xsd_anyType` 개체
   * 런타임 옵션을 지정하는 `AssemblerOptionSpec` 개체

   이 `invokeDDX` `AssemblerResult` 메서드는 작업 결과와 발생한 예외를 포함하는 개체를 반환합니다.

1. 취합된 포트폴리오를 저장합니다.

   새로 만든 PDF 포트폴리오를 얻으려면 다음 작업을 수행하십시오.

   * 결과 PDF 문서 `AssemblerResult` 가 포함된 개체인 개체의 `documents` 필드에 `Map` 액세스합니다.
   * 객체를 반복하여 결과 문서를 `Map` 가져옵니다. 그런 다음 해당 어레이 멤버 `value` 를 a로 캐스팅합니다 `BLOB`.
   * 개체의 속성에 액세스하여 PDF 문서를 나타내는 이진 데이터 `BLOB` 를 `MTOM` 추출합니다. PDF 파일에 기록할 수 있는 바이트 배열을 반환합니다.

**참고 항목**

[MTOM을 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRef를 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
