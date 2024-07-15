---
title: PDF Portfolio 어셈블
description: PDF 포트폴리오를 결합하여 word 파일, 이미지 파일 및 PDF 문서를 비롯한 다양한 유형의 여러 문서를 결합합니다. Java API 및 웹 서비스 API를 사용하여 PDF 포트폴리오를 조합할 수 있습니다.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
exl-id: d2bd7c3e-4f75-4234-a7aa-ee8524430493
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Document Services
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '1815'
ht-degree: 0%

---

# PDF Portfolio 어셈블 {#assembling-pdf-portfolios}

**이 문서의 샘플과 예제는 JEE 환경의 AEM Forms에 대해서만 적용됩니다.**

어셈블러 Java 및 웹 서비스 API를 사용하여 PDF Portfolio을 어셈블할 수 있습니다. 포트폴리오는 word 파일, 이미지 파일(예: jpeg 파일), PDF 문서 등 다양한 유형의 여러 문서를 결합할 수 있습니다. 포트폴리오의 레이아웃은 *미리 보기가 있는 격자*, *이미지에서* 레이아웃 또는 *회전*&#x200B;과 같은 다른 스타일로 설정할 수 있습니다.

다음 그림은 *이미지* 스타일 레이아웃이 있는 포트폴리오의 스크린샷입니다.

![ap_ap_portfolio](assets/ap_ap_portfolio.png)

PDF Portfolio 만들기는 문서 컬렉션을 전달하는 데 페이퍼리스 대체 요소로 사용됩니다. AEM Forms을 사용하면 구조화된 DDX 문서로 어셈블러 서비스를 호출하여 포트폴리오를 만들 수 있습니다. 다음 DDX 문서는 PDF Portfolio을 만드는 DDX 문서의 예입니다.

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

DXX 문서에는 중첩된 `Navigator` 태그가 있는 `Portfolio` 태그가 있어야 합니다. `<Resource name="navigator/image.xxx" source="myImage.png"/>` 태그는 `myNavigator`이(가) onImage 레이아웃 탐색기로 할당된 경우에만 필요합니다. `AdobeOnImage.nav`. 이 태그를 사용하면 어셈블러 서비스에서 포트폴리오 배경으로 사용할 이미지를 선택할 수 있습니다. `PackageFiles` 및 `File` 태그를 포함하여 패키지된 파일의 파일 이름과 MIME 형식을 정의합니다.

>[!NOTE]
>
>어셈블러 서비스에 대한 자세한 내용은 [AEM Forms용 서비스 참조](https://www.adobe.com/go/learn_aemforms_services_63)를 참조하십시오.

>[!NOTE]
>
>DDX 문서에 대한 자세한 내용은 [어셈블러 서비스 및 DDX 참조](https://www.adobe.com/go/learn_aemforms_ddx_63)를 참조하십시오.

## 단계 요약 {#summary-of-steps}

PDF Portfolio을 만들려면 다음 작업을 수행하십시오.

1. 프로젝트 파일을 포함합니다.
1. PDF 어셈블러 클라이언트를 만듭니다.
1. 기존 DDX 문서를 참조합니다.
1. 필요한 문서를 참조하십시오.
1. 런타임 옵션을 설정합니다.
1. 포트폴리오를 조합합니다.
1. 어셈블된 포트폴리오를 저장합니다.

**프로젝트 파일 포함**

개발 프로젝트에 필요한 파일을 포함합니다. Java를 사용하여 클라이언트 응용 프로그램을 만드는 경우 필요한 JAR 파일을 포함합니다. 웹 서비스를 사용하는 경우 프록시 파일을 포함해야 합니다.

프로젝트의 클래스 경로에 다음 JAR 파일을 추가해야 합니다.

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar (AEM Forms이 JBoss에 배포된 경우 필수)
* jbossall-client.jar(AEM Forms이 JBoss에 배포된 경우 필수)

**PDF 어셈블러 클라이언트 만들기**

어셈블러 작업을 프로그래밍 방식으로 수행하려면 먼저 어셈블러 서비스 클라이언트를 만듭니다.

**기존 DDX 문서 참조**

PDF Portfolio을 어셈블하려면 DDX 문서를 참조해야 합니다. 이 DDX 문서에는 `Portfolio`, `Navigator` 및 `PackageFiles` 요소가 포함되어야 합니다.

**필요한 문서를 참조**

PDF Portfolio을 어셈블하려면 어셈블할 문서를 나타내는 모든 파일을 참조합니다. 예를 들어 DDX 문서에 지정된 모든 이미지 파일을 어셈블러 서비스에 전달합니다. 이러한 파일은 이 섹션에 지정된 DDX 문서에서 참조됩니다. *myImage.png* 및 *saint_bernard.jpg*.

PDF Portfolio을 어셈블할 때 NAV 파일(네비게이터 파일)을 어셈블러 서비스에 전달합니다. 어셈블러 서비스에 전달하는 NAV 파일은 만들 PDF Portfolio 유형에 따라 다릅니다. 예를 들어 *이미지* 레이아웃을 만들려면 AdobeOnImage.nav 파일을 전달합니다. 다음 폴더에서 NAV 파일을 찾을 수 있습니다.

`<Install folder>\Acrobat 9.0\Acrobat\Navigators`

Acrobat 9(또는 그 이상) 설치 디렉토리에서 NAV 파일을 복사합니다. 클라이언트 응용 프로그램에서 액세스할 수 있는 위치에 NAV 파일을 배치합니다. 모든 파일은 Map 컬렉션 개체 내의 어셈블러 서비스로 전달됩니다.

>[!NOTE]
>
>어셈블 PDF Portfolio과 관련된 빠른 시작은 AdobeOnImage.nav를 사용합니다.

**런타임 옵션 설정**

작업을 수행하는 동안 어셈블러 서비스의 동작을 제어하는 런타임 옵션을 설정할 수 있습니다. 예를 들어 오류가 발생하는 경우 어셈블러 서비스에서 작업 처리를 계속하도록 지시하는 옵션을 설정할 수 있습니다.

**포트폴리오 결합**

PDF Portfolio을 어셈블하려면 `invokeDDX` 작업을 호출합니다. 어셈블러 서비스는 컬렉션 개체 내의 PDF Portfolio을 반환합니다.

**어셈블된 포트폴리오를 저장**

PDF Portfolio이 컬렉션 개체 내에서 반환됩니다. 컬렉션 객체를 반복하고 PDF Portfolio을 PDF 파일로 저장합니다.

**추가 참조**

[Java API를 사용하여 PDF Portfolio 결합](#assemble-a-pdf-portfolio-using-the-java-api)

[웹 서비스 API를 사용하여 PDF Portfolio 결합](#assemble-a-pdf-portfolio-using-the-web-service-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[프로그래밍 방식으로 PDF 문서 어셈블](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## Java API를 사용하여 PDF Portfolio 결합 {#assemble-a-pdf-portfolio-using-the-java-api}

어셈블러 서비스 API(Java)를 사용하여 PDF Portfolio을 어셈블합니다.

1. 프로젝트 파일을 포함합니다.

   Java 프로젝트의 클래스 경로에 adobe-assembler-client.jar과 같은 클라이언트 JAR 파일을 포함합니다.

1. PDF 어셈블러 클라이언트를 만듭니다.

   * 연결 속성을 포함하는 `ServiceClientFactory` 개체를 만듭니다.
   * 생성자를 사용하고 `ServiceClientFactory` 개체를 전달하여 `AssemblerServiceClient` 개체를 만듭니다.

1. 기존 DDX 문서를 참조합니다.

   * 생성자를 사용하고 DDX 파일의 위치를 지정하는 문자열 값을 전달하여 DDX 문서를 나타내는 `java.io.FileInputStream` 개체를 만듭니다.
   * 생성자를 사용하고 `java.io.FileInputStream` 개체를 전달하여 `com.adobe.idp.Document` 개체를 만듭니다.

1. 필요한 문서를 참조하십시오.

   * `HashMap` 생성자를 사용하여 입력 PDF 문서를 저장하는 데 사용되는 `java.util.Map` 개체를 만듭니다.
   * 해당 생성자를 사용하여 `java.io.FileInputStream` 개체를 만듭니다. 필요한 NAV 파일의 위치를 전달합니다(포트폴리오를 만드는 데 필요한 각 파일에 대해 이 작업을 반복합니다).
   * `com.adobe.idp.Document` 개체를 만들고 NAV 파일이 포함된 `java.io.FileInputStream` 개체를 전달합니다(포트폴리오를 만드는 데 필요한 각 파일에 대해 이 작업을 반복합니다).
   * `put` 메서드를 호출하고 다음 인수를 전달하여 `java.util.Map` 개체에 항목을 추가합니다.

      * 키 이름을 나타내는 문자열 값입니다. 이 값은 DDX 문서에 지정된 원본 요소의 값과 일치해야 합니다. (포트폴리오를 만드는 데 필요한 각 파일에 대해 이 작업을 반복합니다.)
      * PDF 문서를 포함하는 `com.adobe.idp.Document` 개체입니다. (포트폴리오를 만드는 데 필요한 각 파일에 대해 이 작업을 반복합니다.)

1. 런타임 옵션을 설정합니다.

   * 생성자를 사용하여 런타임 옵션을 저장하는 `AssemblerOptionSpec` 개체를 만듭니다.
   * `AssemblerOptionSpec` 개체에 속하는 메서드를 호출하여 비즈니스 요구 사항을 충족하도록 런타임 옵션을 설정하십시오. 예를 들어 오류가 발생할 때 어셈블러 서비스에서 작업 처리를 계속하도록 하려면 `AssemblerOptionSpec` 개체의 `setFailOnError` 메서드를 호출하고 `false`을(를) 전달합니다.

1. 포트폴리오를 조합합니다.

   `AssemblerServiceClient` 개체의 `invokeDDX` 메서드를 호출하고 다음 필수 값을 전달하십시오.

   * 사용할 DDX 문서를 나타내는 `com.adobe.idp.Document` 개체
   * PDF Portfolio을 만드는 데 필요한 파일을 포함하는 `java.util.Map` 개체입니다.
   * 기본 글꼴 및 작업 로그 수준을 포함하여 런타임 옵션을 지정하는 `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` 개체입니다.

   `invokeDDX` 메서드는 어셈블된 PDF Portfolio과 발생한 모든 예외를 포함하는 `com.adobe.livecycle.assembler.client.AssemblerResult` 개체를 반환합니다.

1. 어셈블된 포트폴리오를 저장합니다.

   PDF Portfolio을 얻으려면 다음 작업을 수행하십시오.

   * `AssemblerResult` 개체의 `getDocuments` 메서드를 호출합니다. 이 메서드는 `java.util.Map` 개체를 반환합니다.
   * 결과 `com.adobe.idp.Document` 개체가 발견될 때까지 `java.util.Map` 개체를 반복합니다.
   * `com.adobe.idp.Document` 개체의 `copyToFile` 메서드를 호출하여 PDF Portfolio을 추출하십시오.

**추가 참조**

[빠른 시작(SOAP 모드): Java API를 사용하여 PDF Portfolio 어셈블](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-assembling-pdf-portfolios-using-the-java-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 웹 서비스 API를 사용하여 PDF Portfolio 결합 {#assemble-a-pdf-portfolio-using-the-web-service-api}

어셈블러 서비스 API(웹 서비스)를 사용하여 PDF Portfolio을 어셈블합니다.

1. 프로젝트 파일을 포함합니다.

   MTOM을 사용하는 Microsoft .NET 프로젝트를 만듭니다. 서비스 참조를 설정할 때 다음 WSDL 정의를 사용하는지 확인하십시오. `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >`localhost`을(를) AEM Forms을 호스팅하는 서버의 IP 주소로 바꾸십시오.

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
   * `System.IO.FileStream` 개체의 `Read` 메서드를 호출하여 바이트 배열을 스트림 데이터로 채웁니다. 읽을 바이트 배열, 시작 위치 및 스트림 길이를 전달합니다.
   * 해당 `MTOM` 속성을 바이트 배열의 내용으로 할당하여 `BLOB` 개체를 채웁니다.

1. 필요한 문서를 참조하십시오.

   * 각 입력 파일에 대해 해당 생성자를 사용하여 `BLOB` 개체를 만듭니다. `BLOB` 개체는 입력 파일을 저장하는 데 사용됩니다.
   * 해당 생성자를 호출하고 입력 파일의 파일 위치와 파일을 열 모드를 나타내는 문자열 값을 전달하여 `System.IO.FileStream` 개체를 만듭니다.
   * `System.IO.FileStream` 개체의 내용을 저장하는 바이트 배열을 만듭니다. `System.IO.FileStream` 개체의 `Length` 속성을 가져와서 바이트 배열의 크기를 결정할 수 있습니다.
   * `System.IO.FileStream` 개체의 `Read` 메서드를 호출하여 바이트 배열을 스트림 데이터로 채웁니다. 읽을 바이트 배열, 시작 위치 및 스트림 길이를 전달합니다.
   * 해당 `MTOM` 필드를 바이트 배열의 내용으로 할당하여 `BLOB` 개체를 채웁니다.
   * `MyMapOf_xsd_string_To_xsd_anyType` 개체를 만듭니다. 이 컬렉션 개체는 PDF Portfolio을 만드는 데 필요한 입력 파일을 저장하는 데 사용됩니다.
   * 각 입력 파일에 대해 `MyMapOf_xsd_string_To_xsd_anyType_Item` 개체를 만듭니다.
   * `MyMapOf_xsd_string_To_xsd_anyType_Item` 개체의 `key` 필드에 키 이름을 나타내는 문자열 값을 지정하십시오. 이 값은 DDX 문서에 지정된 요소의 값과 일치해야 합니다. (각 입력 파일에 대해 이 작업을 수행합니다.)
   * 입력 파일을 저장하는 `BLOB` 개체를 `MyMapOf_xsd_string_To_xsd_anyType_Item` 개체의 `value` 필드에 할당합니다. (각 입력 PDF 문서에 대해 이 작업을 수행합니다.)
   * `MyMapOf_xsd_string_To_xsd_anyType` 개체에 `MyMapOf_xsd_string_To_xsd_anyType_Item` 개체를 추가합니다. `MyMapOf_xsd_string_To_xsd_anyType` 개체의 `Add` 메서드를 호출하고 `MyMapOf_xsd_string_To_xsd_anyType` 개체를 전달하십시오. (각 입력 PDF 문서에 대해 이 작업을 수행합니다.)

1. 런타임 옵션을 설정합니다.

   * 생성자를 사용하여 런타임 옵션을 저장하는 `AssemblerOptionSpec` 개체를 만듭니다.
   * `AssemblerOptionSpec` 개체에 속하는 데이터 멤버에 값을 할당하여 비즈니스 요구 사항에 맞게 런타임 옵션을 설정하십시오. 예를 들어 오류가 발생할 때 어셈블러 서비스에서 작업 처리를 계속하도록 하려면 `AssemblerOptionSpec` 개체의 `failOnError` 데이터 멤버에 `false`을(를) 할당합니다.

1. 포트폴리오를 조합합니다.

   `AssemblerServiceClient` 개체의 `invokeDDX` 메서드를 호출하고 다음 값을 전달하십시오.

   * DDX 문서를 나타내는 `BLOB` 개체
   * 필요한 파일이 포함된 `MyMapOf_xsd_string_To_xsd_anyType` 개체
   * 런타임 옵션을 지정하는 `AssemblerOptionSpec` 개체

   `invokeDDX` 메서드가 작업 결과와 발생한 모든 예외를 포함하는 `AssemblerResult` 개체를 반환합니다.

1. 어셈블된 포트폴리오를 저장합니다.

   새로 만든 PDF Portfolio을 가져오려면 다음 작업을 수행합니다.

   * 결과 PDF 문서를 포함하는 `Map` 개체인 `AssemblerResult` 개체의 `documents` 필드에 액세스합니다.
   * `Map` 개체를 반복하여 각 결과 문서를 가져옵니다. 그런 다음 해당 배열 멤버의 `value`을(를) `BLOB`(으)로 캐스팅합니다.
   * `BLOB` 개체의 `MTOM` 속성에 액세스하여 PDF 문서를 나타내는 이진 데이터를 추출합니다. PDF 파일에 쓸 수 있는 바이트 배열이 반환됩니다.

**추가 참조**

[MTOM을 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[SwaRef를 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
