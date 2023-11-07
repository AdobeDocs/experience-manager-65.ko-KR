---
title: 웹 서비스를 사용하여 AEM Forms 호출
description: WSDL 생성을 완벽하게 지원하는 웹 서비스를 사용하여 AEM Forms 프로세스를 호출합니다.
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: coding
role: Developer
exl-id: 3139564f-9346-4933-8e39-2e1642bff097
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '9888'
ht-degree: 0%

---

# 웹 서비스를 사용하여 AEM Forms 호출 {#invoking-aem-forms-using-web-services}

**이 문서의 샘플 및 예제는 JEE 환경의 AEM Forms에 대해서만 적용됩니다.**

서비스 컨테이너의 대부분의 AEM Forms 서비스는 WSDL(웹 서비스 정의 언어) 생성을 완벽하게 지원하여 웹 서비스를 노출하도록 구성됩니다. 즉, AEM Forms 서비스의 기본 SOAP 스택을 사용하는 프록시 개체를 만들 수 있습니다. 따라서 AEM Forms 서비스는 다음 SOAP 메시지를 교환 및 처리할 수 있습니다.

* **SOAP 요청**: 작업을 요청하는 클라이언트 애플리케이션이 Forms 서비스로 보냅니다.
* **SOAP 응답**: SOAP 요청이 처리된 후 Forms 서비스에 의해 클라이언트 애플리케이션으로 전송됩니다.

웹 서비스를 사용하면 Java API를 사용하여 수행할 수 있는 것과 동일한 AEM Forms 서비스 작업을 수행할 수 있습니다. 웹 서비스를 사용하여 AEM Forms 서비스를 호출하면 SOAP를 지원하는 개발 환경에서 클라이언트 애플리케이션을 만들 수 있다는 이점이 있습니다. 클라이언트 응용 프로그램은 특정 개발 환경이나 프로그래밍 언어에 바인딩되어 있지 않습니다. 예를들어, Microsoft Visual Studio .NET 및 C#을 프로그래밍 언어로 사용하여 클라이언트 응용 프로그램을 만들 수 있습니다.

AEM Forms 서비스는 SOAP 프로토콜을 통해 노출되며 WSI Basic Profile 1.1을 준수합니다. WSI(Web Services Interoperability)는 플랫폼 간에 웹 서비스 상호 운용성을 촉진하는 개방형 표준 조직입니다. 자세한 내용은 [https://www.ws-i.org/](https://www.ws-i.org).

AEM Forms은 다음과 같은 웹 서비스 표준을 지원합니다.

* **인코딩**: 문서 및 리터럴 인코딩만 지원합니다(WSI 기본 프로필에 따른 기본 인코딩). (참조: [Base64 인코딩을 사용하여 AEM Forms 호출](#invoking-aem-forms-using-base64-encoding).)
* **MTOM**: 첨부 파일을 SOAP 요청으로 인코딩하는 방법을 나타냅니다. (참조: [MTOM을 사용하여 AEM Forms 호출](#invoking-aem-forms-using-mtom).)
* **SwaRef**: 첨부 파일을 SOAP 요청으로 인코딩하는 다른 방법을 나타냅니다. (참조: [SwaRef를 사용하여 AEM Forms 호출](#invoking-aem-forms-using-swaref).)
* **첨부 파일이 있는 SOAP**: MIME과 DIME(Direct Internet Message Encapsulation)을 모두 지원합니다. 이러한 프로토콜은 SOAP를 통해 첨부 파일을 전송하는 표준 방법입니다. Microsoft Visual Studio .NET 응용 프로그램은 DIME을 사용합니다. (참조: [Base64 인코딩을 사용하여 AEM Forms 호출](#invoking-aem-forms-using-base64-encoding).)
* **WS-Security**: 사용자 이름과 암호를 WS 보안 SOAP 헤더의 일부로 보내는 표준 방법인 사용자 이름 암호 토큰 프로필을 지원합니다. AEM Forms은 HTTP 기본 인증도 지원합니다. s

웹 서비스를 사용하여 AEM Forms 서비스를 호출하려면 일반적으로 서비스 WSDL을 사용하는 프록시 라이브러리를 만듭니다. 다음 *웹 서비스를 사용하여 AEM Forms 호출* 섹션은 JAX-WS를 사용하여 서비스를 호출하는 Java 프록시 클래스를 생성합니다. (참조: [JAX-WS를 사용하여 Java 프록시 클래스 생성](#creating-java-proxy-classes-using-jax-ws).)

다음 URL 정의를 지정하여 서비스 WDSL을 검색할 수 있습니다(대괄호로 묶인 항목은 선택 사항).

```java
 https://<your_serverhost>:<your_port>/soap/services/<service_name>?wsdl[&version=<version>][&async=true|false][lc_version=<lc_version>]
```

여기에서

* *your_serverhost* AEM Forms을 호스팅하는 J2EE 애플리케이션 서버의 IP 주소를 나타냅니다.
* *your_port* J2EE 응용 프로그램 서버가 사용하는 HTTP 포트를 나타냅니다.
* *service_name* 는 서비스 이름을 나타냅니다.
* *버전* 서비스의 대상 버전을 나타냅니다(기본적으로 최신 서비스 버전이 사용됨).
* `async` 값 지정 `true` 비동기 호출을 위해 추가 작업을 활성화하려면( `false` 기본적으로).
* *lc_version* 호출하려는 AEM Forms 버전을 나타냅니다.

다음 표에는 서비스 WSDL 정의가 나열되어 있습니다(AEM Forms이 로컬 호스트에 배포되고 post가 8080이라고 가정).

<table>
 <thead>
  <tr>
   <th><p>서비스</p></th>
   <th><p>WSDL 정의</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>어셈블러</p></td>
   <td><p><code>http://localhost:8080/soap/services/ AssemblerService?wsdl</code></p></td>
  </tr>
  <tr>
   <td><p>뒤로 및 복원</p></td>
   <td><p><code>http://localhost:8080/soap/services/BackupService?wsdl</code></p></td>
  </tr>
  <tr>
   <td><p>바코드 형식</p></td>
   <td><p><code>http://localhost:8080/soap/services/ BarcodedFormsService?wsdl</code></p></td>
  </tr>
  <tr>
   <td><p>PDF 변환</p></td>
   <td><p><code>http://localhost:8080/soap/services/ ConvertPDFService?wsdl</code></p></td>
  </tr>
  <tr>
   <td><p>Distiller</p></td>
   <td><p><code>http://localhost:8080/soap/services/ DistillerService?wsdl</code></p></td>
  </tr>
  <tr>
   <td><p>DocConverter </p></td>
   <td><p><code>http://localhost:8080/soap/services/DocConverterService?WSDL</code></p></td>
  </tr>
  <tr>
   <td><p>DocumentManagement</p></td>
   <td><p><code>http://localhost:8080/soap/services/DocumentManagementService?WSDL</code></p></td>
  </tr>
  <tr>
   <td><p>암호화 </p></td>
   <td><p><code>http://localhost:8080/soap/services/EncryptionService?wsdl</code></p></td>
  </tr>
  <tr>
   <td><p>Forms</p></td>
   <td><p><code>http://localhost:8080/soap/services/FormsService?wsdl</code></p></td>
  </tr>
  <tr>
   <td><p>양식 데이터 통합</p></td>
   <td><p><code>http://localhost:8080/soap/services/FormDataIntegration?wsdl</code></p></td>
  </tr>
  <tr>
   <td><p>PDF 생성</p></td>
   <td><p><code>http://localhost:8080/soap/services/ GeneratePDFService?wsdl</code></p></td>
  </tr>
  <tr>
   <td><p>3D PDF 생성</p></td>
   <td><p><code>http://localhost:8080/soap/services/Generate3dPDFService?WSDL</code></p></td>
  </tr>
  <tr>
   <td><p>출력</p></td>
   <td><p><code>http://localhost:8080/soap/services/ OutputService?wsdl</code></p></td>
  </tr>
  <tr>
   <td><p>PDF 유틸리티 </p></td>
   <td><p><code>http://localhost:8080/soap/services/ PDFUtilityService?wsdl</code></p></td>
  </tr>
  <tr>
   <td><p>Acrobat Reader DC 확장</p></td>
   <td><p><code>http://localhost:8080/soap/services/ ReaderExtensionsService?wsdl</code></p></td>
  </tr>
  <tr>
   <td><p>저장소</p></td>
   <td><p><code>http://localhost:8080/soap/services/ RepositoryService?wsdl</code></p></td>
  </tr>
  <tr>
   <td><p>Rights Management </p></td>
   <td><p><code>http://localhost:8080/soap/services/ RightsManagementService?wsdl</code></p></td>
  </tr>
  <tr>
   <td><p>서명 </p></td>
   <td><p><code>http://localhost:8080/soap/services/ SignatureService?wsdl</code></p></td>
  </tr>
  <tr>
   <td><p>XMP 유틸리티</p></td>
   <td><p><code>http://localhost:8080/soap/services/ XMPUtilityService?wsdl</code></p></td>
  </tr>
 </tbody>
</table>

**AEM Forms 프로세스 WSDL 정의**

Workbench에서 생성된 프로세스에 속한 WSDL에 액세스하려면 WSDL 정의 내에서 응용 프로그램 이름과 프로세스 이름을 지정합니다. 애플리케이션 이름이 다음과 같다고 가정합니다. `MyApplication` 프로세스의 이름은 입니다. `EncryptDocument`. 이 경우 다음 WSDL 정의를 지정합니다.

```java
 http://localhost:8080/soap/services/MyApplication/EncryptDocument?wsdl
```

>[!NOTE]
>
>예제에 대한 자세한 내용 `MyApplication/EncryptDocument` 단기 프로세스, 참조 [단기 프로세스 예](/help/forms/developing/aem-forms-processes.md).

>[!NOTE]
>
>응용 프로그램에는 폴더가 포함될 수 있습니다. 이 경우 WSDL 정의에 폴더 이름을 지정합니다.

```java
 http://localhost:8080/soap/services/MyApplication/[<folderA>/.../<folderZ>/]EncryptDocument?wsdl
```

**웹 서비스를 사용하여 새 기능에 액세스**

웹 서비스를 사용하여 새로운 AEM Forms 서비스 기능에 액세스할 수 있습니다. 예를 들어 AEM Forms에서는 MTOM을 사용하여 첨부 파일을 인코딩하는 기능이 도입되었습니다. (참조: [MTOM을 사용하여 AEM Forms 호출](#invoking-aem-forms-using-mtom).)

AEM Forms에 도입된 새로운 기능에 액세스하려면 다음을 지정하십시오. `lc_version` wsdl 정의에 있는 특성입니다. 예를 들어 MTOM 지원을 포함한 새 서비스 기능에 액세스하려면 다음 WSDL 정의를 지정합니다.

```java
 http://localhost:8080/soap/services/MyApplication/EncryptDocument?wsdl&lc_version=9.0.1
```

>[!NOTE]
>
>를 설정할 때 `lc_version` 속성에서 세 자리를 사용해야 합니다. 예를 들어, 9.0.1은 버전 9.0과 같습니다.

**웹 서비스 BLOB 데이터 유형**

AEM Forms 서비스 WSDL은 여러 데이터 유형을 정의합니다. 웹 서비스에서 노출되는 가장 중요한 데이터 유형 중 하나는 `BLOB` 유형. 이 데이터 유형은 `com.adobe.idp.Document` AEM Forms Java API 작업 시 클래스. (참조: [Java API를 사용하여 AEM Forms 서비스에 데이터 전달](/help/forms/developing/invoking-aem-forms-using-java.md#passing-data-to-aem-forms-services-using-the-java-api).)

A `BLOB` object는 AEM Forms services에서 이진 데이터(예: PDF 파일, XML 데이터 등)를 보내고 검색합니다. 다음 `BLOB` 형식은 다음과 같이 서비스 WSDL에서 정의됩니다.

```xml
 <complexType name="BLOB">
     <sequence>
         <element maxOccurs="1" minOccurs="0" name="contentType"
             type="xsd:string"/>
         <element maxOccurs="1" minOccurs="0" name="binaryData"
             type="xsd:base64Binary"/>
         <element maxOccurs="1" minOccurs="0" name="attachmentID"
             type="xsd:string"/>
         <element maxOccurs="1" minOccurs="0" name="remoteURL"
             type="xsd:string"/>
         <element maxOccurs="1" minOccurs="0" name="MTOM"
             type="xsd:base64Binary"
             xmime:expectedContentTypes="*/*"
             xmlns:xmime="https://www.w3.org/2005/05/xmlmime"/>
         <element maxOccurs="1" minOccurs="0" name="swaRef"
             type="tns1:swaRef"/>
         <element maxOccurs="1" minOccurs="0" name="attributes"
             type="impl:MyMapOf_xsd_string_To_xsd_anyType"/>
     </sequence>
 </complexType>
```

다음 `MTOM` 및 `swaRef` 필드는 AEM Forms에서만 지원됩니다. 다음을 포함하는 URL을 지정하는 경우에만 이러한 새 필드를 사용할 수 있습니다. `lc_version` 속성.

**서비스 요청에서 BLOB 개체 제공**

AEM Forms 서비스 작업에 필요한 경우 `BLOB` 을(를) 입력 값으로 입력하고 의 인스턴스를 `BLOB` 애플리케이션 논리를 입력합니다. (많은 웹 서비스 빠른 시작 위치: *AEM Forms를 사용한 프로그래밍* blob 데이터 형식으로 작업하는 방법을 보여 줍니다.)

에 속한 필드에 값 할당 `BLOB` 인스턴스를 다음과 같이 표시합니다.

* **Base64**: 데이터를 Base64 형식으로 인코딩된 텍스트로 전달하려면 `BLOB.binaryData` 필드 및 MIME 형식의 데이터 형식 설정(예: `application/pdf`)에 있는 `BLOB.contentType` 필드. (참조: [Base64 인코딩을 사용하여 AEM Forms 호출](#invoking-aem-forms-using-base64-encoding).)
* **MTOM**: MTOM 첨부 파일에 이진 데이터를 전달하려면 `BLOB.MTOM` 필드. 이 설정은 Java JAX-WS 프레임워크 또는 SOAP 프레임워크의 기본 API를 사용하여 데이터를 SOAP 요청에 연결합니다. (참조: [MTOM을 사용하여 AEM Forms 호출](#invoking-aem-forms-using-mtom).)
* **SwaRef**: WS-I SwaRef 첨부 파일에 이진 데이터를 전달하려면 `BLOB.swaRef` 필드. 이 설정은 Java JAX-WS 프레임워크를 사용하여 데이터를 SOAP 요청에 연결합니다. (참조: [SwaRef를 사용하여 AEM Forms 호출](#invoking-aem-forms-using-swaref).)
* **MIME 또는 DIME 첨부 파일**: MIME 또는 DIME 첨부 파일로 데이터를 전달하려면 SOAP 프레임워크의 기본 API를 사용하여 SOAP 요청에 데이터를 첨부합니다. 에서 첨부 파일 식별자 설정 `BLOB.attachmentID` 필드. (참조: [Base64 인코딩을 사용하여 AEM Forms 호출](#invoking-aem-forms-using-base64-encoding).)
* **원격 URL**: 데이터가 웹 서버에서 호스팅되고 HTTP URL을 통해 액세스할 수 있는 경우 `BLOB.remoteURL` 필드. (참조: [HTTP를 통해 BLOB 데이터를 사용하여 AEM Forms 호출](#invoking-aem-forms-using-blob-data-over-http).)

**서비스에서 반환된 BLOB 개체의 데이터에 액세스**

반환된 전송 프로토콜 `BLOB` 객체는 몇 가지 요소에 따라 다르며, 다음 순서로 간주되면 기본 조건이 충족될 때 중지됩니다.

1. **대상 URL은 전송 프로토콜을 지정합니다.**. SOAP 호출에서 지정된 대상 URL에 매개 변수가 포함된 경우 `blob="`*BLOB_TYPE*&quot;, 그런 다음 *BLOB_TYPE* 전송 프로토콜을 결정합니다. *BLOB_TYPE* 는 base64, dime, mime, http, mtom 또는 swaref에 대한 자리 표시자입니다.
1. **서비스 SOAP 끝점이 스마트**. 다음 조건이 참인 경우 입력 문서와 동일한 전송 프로토콜을 사용하여 출력 문서가 반환됩니다.

   * 출력 Blob 개체에 대한 서비스의 SOAP 끝점 매개 변수 기본 프로토콜이 Smart로 설정되어 있습니다.

     SOAP 끝점이 있는 각 서비스에 대해 관리 콘솔을 사용하여 반환된 모든 BLOB에 대한 전송 프로토콜을 지정할 수 있습니다. (참조: [관리 도움말](https://www.adobe.com/go/learn_aemforms_admin_63).)

   * AEM Forms 서비스는 하나 이상의 문서를 입력으로 취합니다.

1. **서비스 SOAP 끝점이 Smart가 아닙니다.**. 구성된 프로토콜은 문서 전송 프로토콜을 결정하고, 데이터는 해당 위치에서 반환된다 `BLOB` 필드. 예를 들어 SOAP 끝점이 DIME으로 설정된 경우 반환된 Blob는 `blob.attachmentID` 입력 문서의 전송 프로토콜과 관계없이 표시되는 필드입니다.
1. **그렇지 않은 경우**. 서비스가 문서 유형을 입력으로 취하지 않으면 출력 문서가 `BLOB.remoteURL` HTTP 프로토콜 위의 필드입니다.

첫 번째 조건에 설명된 대로 접미사를 사용하여 SOAP 끝점 URL을 다음과 같이 확장하여 반환된 문서의 전송 유형을 보장할 수 있습니다.

```java
     https://<your_serverhost>:<your_port>/soap/services/<service
     name>?blob=base64|dime|mime|http|mtom|swaref
```

다음은 전송 유형과 데이터를 얻는 필드 간의 상관 관계입니다.

* **Base64 형식**: 를 설정합니다. `blob` 접미사 `base64` 에 데이터를 반환하려면 `BLOB.binaryData` 필드.
* **MIME 또는 DIME 첨부 파일**: 를 설정합니다. `blob` 접미사 `DIME` 또는 `MIME` 에 반환된 첨부 파일 식별자가 있는 해당 첨부 파일 유형으로 데이터 반환 `BLOB.attachmentID` 필드. SOAP 프레임워크의 자체 API를 사용하여 첨부 파일에서 데이터를 읽습니다.
* **원격 URL**: 를 설정합니다. `blob` 접미사 `http` 를 사용하여 데이터를 응용 프로그램 서버에 유지하고 `BLOB.remoteURL` 필드.
* **MTOM 또는 SwaRef**: 를 설정합니다. `blob` 접미사 `mtom` 또는 `swaref` 에 반환된 첨부 파일 식별자가 있는 해당 첨부 파일 유형으로 데이터 반환 `BLOB.MTOM` 또는 `BLOB.swaRef` 필드. SOAP 프레임워크의 기본 API를 사용하여 첨부 파일에서 데이터를 읽습니다.

>[!NOTE]
>
>를 채울 때는 30MB를 초과하지 않는 것이 좋습니다. `BLOB` 개체 `setBinaryData` 메서드를 사용합니다. 그렇지 않으면 `OutOfMemory` 예외가 발생했습니다.

>[!NOTE]
>
>MTOM 전송 프로토콜을 사용하는 JAX WS 기반 응용 프로그램은 25MB의 송수신 데이터로 제한됩니다. 이 제한은 JAX-WS의 버그 때문입니다. 전송 파일과 수신 파일의 통합 크기가 25MB를 초과하는 경우 MTOM 전송 프로토콜 대신 SwaRef 전송 프로토콜을 사용합니다. 그렇지 않으면 `OutOfMemory` 예외.

**base64 인코딩 바이트 배열의 MTOM 전송**

이외에도 `BLOB` 그러나 MTOM 프로토콜은 모든 바이트 배열 매개 변수 또는 복잡한 유형의 바이트 배열 필드를 지원합니다. 즉, MTOM을 지원하는 클라이언트 SOAP 프레임워크는 `xsd:base64Binary` 요소를 MTOM 첨부 파일로 사용할 수 있습니다(base64로 인코딩된 텍스트 대신). AEM Forms SOAP 끝점은 이 유형의 바이트 배열 인코딩을 읽을 수 있습니다. 그러나 AEM Forms 서비스는 항상 바이트 배열 형식을 base64로 인코딩된 텍스트로 반환합니다. 출력 바이트 배열 매개 변수는 MTOM을 지원하지 않습니다.

많은 양의 이진 데이터를 반환하는 AEM Forms 서비스에서는 바이트 배열 형식이 아닌 Document/BLOB 형식을 사용합니다. 문서 유형은 대량의 데이터를 전송하는 데 훨씬 효율적입니다.

## 웹 서비스 데이터 유형 {#web-service-data-types}

다음 표에는 Java 데이터 유형이 나열되어 있으며 해당 웹 서비스 데이터 유형이 표시됩니다.

<table>
 <thead>
  <tr>
   <th><p>Java 데이터 유형</p></th>
   <th><p>웹 서비스 데이터 유형</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p><code>java.lang.byte[]</code></p></td>
   <td><p><code>xsd:base64Binary</code></p></td>
  </tr>
  <tr>
   <td><p><code>java.lang.Boolean</code></p></td>
   <td><p><code>xsd:boolean</code></p></td>
  </tr>
  <tr>
   <td><p><code>java.util.Date</code></p></td>
   <td><p>다음 <code>DATE</code> type은 다음과 같이 서비스 WSDL에 정의됩니다.</p><p><code>&lt;complexType name="DATE"&gt;</code></p><p><code>&lt;sequence&gt;</code></p><p><code>&lt;element maxOccurs="1" minOccurs="0" name="date" </code><code>type="xsd:dateTime" /&gt; </code></p><p><code>&lt;element maxOccurs="1" minOccurs="0" name="calendar" </code><code>type="xsd:dateTime" /&gt; </code></p><p><code>&lt;/sequence&gt;</code></p><p><code>&lt;/complexType&gt;</code></p><p>AEM Forms 서비스 작업이 다음을 수행하는 경우 <code>java.util.Date</code> 값을 입력하면 SOAP 클라이언트 응용 프로그램에서 <code>DATE.date</code> 필드. 설정 <code>DATE.calendar</code> 이 경우 필드는 런타임 예외를 발생시킵니다. 서비스가 를 반환하는 경우 <code>java.util.Date</code>, 날짜가 <code>DATE.date</code> 필드.</p></td>
  </tr>
  <tr>
   <td><p><code>java.util.Calendar</code></p></td>
   <td><p>다음 <code>DATE</code> type은 다음과 같이 서비스 WSDL에 정의됩니다.</p><p><code>&lt;complexType name="DATE"&gt;</code></p><p><code>&lt;sequence&gt;</code></p><p><code>&lt;element maxOccurs="1" minOccurs="0" name="date" </code><code>type="xsd:dateTime" /&gt; </code></p><p><code>&lt;element maxOccurs="1" minOccurs="0" name="calendar" </code><code>type="xsd:dateTime" /&gt; </code></p><p><code>&lt;/sequence&gt;</code></p><p><code>&lt;/complexType&gt;</code></p><p>AEM Forms 서비스 작업이 다음을 수행하는 경우 <code>java.util.Calendar</code> 값을 입력하면 SOAP 클라이언트 응용 프로그램에서 <code>DATE.caledendar</code> 필드. 설정 <code>DATE.date</code> 이 경우 필드에 런타임 예외가 발생합니다. 서비스가 를 반환하는 경우 <code>java.util.Calendar</code>를 입력하면 날짜가 <code>DATE.calendar</code> 필드. </p></td>
  </tr>
  <tr>
   <td><p><code>java.math.BigDecimal</code></p></td>
   <td><p><code>xsd:decimal</code></p></td>
  </tr>
  <tr>
   <td><p><code>com.adobe.idp.Document</code></p></td>
   <td><p><code>BLOB</code></p></td>
  </tr>
  <tr>
   <td><p><code>java.lang.Double</code></p></td>
   <td><p><code>xsd:double</code></p></td>
  </tr>
  <tr>
   <td><p><code>java.lang.Float</code></p></td>
   <td><p><code>xsd:float</code></p></td>
  </tr>
  <tr>
   <td><p><code>java.lang.Integer</code></p></td>
   <td><p><code>xsd:int</code></p></td>
  </tr>
  <tr>
   <td><p><code>java.util.List</code></p></td>
   <td><p><code>MyArrayOf_xsd_anyType</code></p></td>
  </tr>
  <tr>
   <td><p><code>java.lang.Long</code></p></td>
   <td><p><code>xsd:long</code></p></td>
  </tr>
  <tr>
   <td><p><code>java.util.Map</code></p></td>
   <td><p>다음 <code>apachesoap:Map</code>서비스 WSDL에서 다음과 같이 정의됩니다.</p><p><code>&lt;schema elementFormDefault="qualified" targetNamespace="https://xml.apache.org/xml-soap" xmlns="https://www.w3.org/2001/XMLSchema"&gt;</code></p><p><code>&lt;complexType name="mapItem"&gt;</code></p><p><code>&lt;sequence&gt;</code></p><p><code>&lt;element name="key" nillable="true" type="xsd:anyType"/&gt;</code></p><p><code>&lt;element name="value" nillable="true" type="xsd:anyType"/&gt;</code></p><p><code>&lt;/sequence&gt;</code></p><p><code>&lt;/complexType&gt;</code></p><p><code>&lt;complexType name="Map"&gt;</code></p><p><code>&lt;sequence&gt;</code></p><p><code>&lt;element maxOccurs="unbounded" minOccurs="0" name="item" </code><code>type="apachesoap:mapItem"/&gt;</code></p><p><code>&lt;/sequence&gt;</code></p><p><code>&lt;/complexType&gt;</code></p><p><code>&lt;/schema&gt;</code></p><p>맵은 키/값 쌍의 시퀀스로 표시됩니다.</p></td>
  </tr>
  <tr>
   <td><p><code>java.lang.Object</code></p></td>
   <td><p><code>$1</code></p></td>
  </tr>
  <tr>
   <td><p><code>java.lang.Short</code></p></td>
   <td><p><code>xsd:short</code></p></td>
  </tr>
  <tr>
   <td><p><code>java.lang.String</code></p></td>
   <td><p><code>xsd:string</code></p></td>
  </tr>
  <tr>
   <td><p><code>org.w3c.dom.Document</code></p></td>
   <td><p>다음과 같이 서비스 WSDL에 정의된 XML 유형입니다.</p><p><code>&lt;complexType name="XML"&gt;</code></p><p><code>&lt;sequence&gt;</code></p><p><code>&lt;element maxOccurs="1" minOccurs="0" name="document" </code><code>type="xsd:string" /&gt; </code></p><p><code>&lt;element maxOccurs="1" minOccurs="0" name="element" </code><code>type="xsd:string" /&gt; </code></p><p><code>&lt;/sequence&gt;</code></p><p><code>&lt;/complexType&gt;</code></p><p>AEM Forms 서비스 작업에서 <code>org.w3c.dom.Document</code> 값을 반환하고에서 XML 데이터를 <code>XML.document</code> 필드.</p><p>설정 <code>XML.element</code> 필드에서 런타임 예외가 발생합니다. 서비스가 다음을 반환하는 경우 <code>org.w3c.dom.Document</code>를 입력하면 XML 데이터가 <code>XML.document</code> 필드.</p></td>
  </tr>
  <tr>
   <td><p><code>org.w3c.dom.Element</code></p></td>
   <td><p>다음과 같이 서비스 WSDL에 정의된 XML 유형입니다.</p><p><code>&lt;complexType name="XML"&gt;</code></p><p><code>&lt;sequence&gt;</code></p><p><code>&lt;element maxOccurs="1" minOccurs="0" name="document" </code><code>type="xsd:string" /&gt; </code></p><p><code>&lt;element maxOccurs="1" minOccurs="0" name="element" </code><code>type="xsd:string" /&gt; </code></p><p><code>&lt;/sequence&gt;</code></p><p><code>&lt;/complexType&gt;</code></p><p>AEM Forms 서비스 작업이 다음을 수행하는 경우 <code>org.w3c.dom.Element</code> 입력으로 XML 데이터를 <code>XML.element</code> 필드.</p><p>설정 <code>XML.document</code> 필드에서 런타임 예외가 발생합니다. 서비스가 다음을 반환하는 경우 <code>org.w3c.dom.Element</code>그런 다음 XML 데이터가 <code>XML.element</code> 필드.</p></td>
  </tr>
 </tbody>
</table>

## JAX-WS를 사용하여 Java 프록시 클래스 생성 {#creating-java-proxy-classes-using-jax-ws}

JAX-WS를 사용하여 Forms 서비스 WSDL을 Java 프록시 클래스로 변환할 수 있습니다. 이러한 클래스를 사용하면 AEM Forms 서비스 작업을 호출할 수 있습니다. Apache Ant를 사용하면 AEM Forms 서비스 WSDL을 참조하여 Java 프록시 클래스를 생성하는 빌드 스크립트를 만들 수 있습니다. 다음 단계를 수행하여 JAX-WS 프록시 파일을 생성할 수 있습니다.

1. 클라이언트 컴퓨터에 Apache Ant를 설치합니다. (참조: [https://ant.apache.org/bindownload.cgi](https://ant.apache.org/bindownload.cgi).)

   * bin 디렉터리를 클래스 경로에 추가합니다.
   * 설정 `ANT_HOME` 환경 변수를 Ant를 설치한 디렉토리에 추가합니다.

1. JDK 1.6 이상을 설치합니다.

   * 클래스 경로에 JDK bin 디렉토리를 추가합니다.
   * 클래스 경로에 JRE bin 디렉토리를 추가합니다. 이 상자는 다음 위치에 있습니다. `[JDK_INSTALL_LOCATION]/jre` 디렉토리.
   * 설정 `JAVA_HOME` 환경 변수를 JDK를 설치한 디렉토리에 추가합니다.

   JDK 1.6에는 build.xml 파일에 사용되는 wsimport 프로그램이 포함되어 있습니다. JDK 1.5에는 해당 프로그램이 포함되어 있지 않습니다.

1. 클라이언트 컴퓨터에 JAX-WS를 설치합니다. (참조: [XML Web Services용 Java API](https://jax-ws.dev.java.net/jax-ws-ea3/docs/mtom-swaref.html).)
1. JAX-WS 및 Apache Ant를 사용하여 Java 프록시 클래스를 생성합니다. 이 작업을 수행하기 위한 Ant 빌드 스크립트를 만듭니다. 다음 스크립트는 build.xml이라는 샘플 Ant 빌드 스크립트입니다.

   ```xml
    <?xml version="1.0" encoding="UTF-8"?>
    
    <project basedir="." default="compile">
    
    <property name="port" value="8080" />
    <property name="host" value="localhost" />
    <property name="username" value="administrator" />
    <property name="password" value="password" />
    <property name="tests" value="all" />
    
    <target name="clean" >
           <delete dir="classes" />
    </target>
    
    <target name="wsdl" depends="clean">
           <mkdir dir="classes"/>
           <exec executable="wsimport" failifexecutionfails="false" failonerror="true" resultproperty="foundWSIMPORT">
               <arg line="-keep -d classes https://${host}:${port}/soap/services/EncryptionService?wsdl&lc_version=9.0.1"/>
           </exec>
           <fail unless="foundWSIMPORT">
              !!! Failed to execute JDK's wsimport tool. Make sure that JDK 1.6 (or later) is on your PATH !!!
           </fail>
    </target>
    
    <target name="compile" depends="clean, wsdl" >
         <javac destdir="./classes" fork="true" debug="true">
            <src path="./src"/>
         </javac>
    </target>
    
    <target name="run">
         <java classname="Client" fork="yes" failonerror="true" maxmemory="200M">
            <classpath>
              <pathelement location="./classes"/>
            </classpath>
            <arg value="${port}"/>
            <arg value="${host}"/>
            <arg value="${username}"/>
            <arg value="${password}"/>
            <arg value="${tests}"/>
         </java>
    </target>
    </project>
   ```

   이 Ant 빌드 스크립트 내에서 `url` localhost에서 실행 중인 암호화 서비스 WSDL을 참조하도록 속성을 설정합니다. 다음 `username` 및 `password` 속성을 유효한 AEM forms 사용자 이름 및 암호로 설정해야 합니다. URL에 `lc_version` 특성. 을 지정하지 않고 `lc_version` 옵션을 사용하면 새 AEM Forms 서비스 작업을 호출할 수 없습니다.

   >[!NOTE]
   >
   >바꾸기 `EncryptionService`Java 프록시 클래스를 사용하여 호출할 AEM Forms 서비스 이름으로 예를 들어 Rights Management 서비스에 대한 Java 프록시 클래스를 생성하려면 다음을 지정합니다.

   ```java
    http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1
   ```

1. BAT 파일을 만들어 Ant 빌드 스크립트를 실행합니다. 다음 명령은 Ant 빌드 스크립트 실행을 담당하는 BAT 파일 내에 위치할 수 있습니다.

   ```java
    ant -buildfile "build.xml" wsdl
   ```

   C:\Program Files\Java\jaxws-ri\bin 디렉터리에 ANT 빌드 스크립트를 배치합니다. 스크립트는에 JAVA 파일을 기록합니다./classes 폴더 스크립트는 서비스를 호출할 수 있는 JAVA 파일을 생성합니다.

1. JAVA 파일을 JAR 파일로 패키징합니다. Eclipse에서 작업하는 경우 다음 단계를 수행합니다.

   * 프록시 JAVA 파일을 JAR 파일로 패키지하는 데 사용되는 Java 프로젝트를 생성합니다.
   * 프로젝트에 소스 폴더를 만듭니다.
   * 만들기 `com.adobe.idp.services` 소스 폴더의 패키지
   * 다음 항목 선택 `com.adobe.idp.services` 패키지를 만든 다음 adobe/idp/services 폴더에서 패키지로 JAVA 파일을 가져옵니다.
   * 필요한 경우 `org/apache/xml/xmlsoap` 소스 폴더의 패키지
   * 소스 폴더를 선택한 다음 org/apache/xml/xmlsoap 폴더에서 JAVA 파일을 가져옵니다.
   * Java 컴파일러의 준수 수준을 5.0 이상으로 설정합니다.
   * 프로젝트를 빌드합니다.
   * 프로젝트를 JAR 파일로 내보냅니다.
   * 클라이언트 프로젝트의 클래스 경로에 있는 이 JAR 파일을 가져옵니다. 또한 모든 JAR 파일을에서 가져옵니다. &lt;install directory=&quot;&quot;>\Adobe\Adobe_Experience_Manager_forms\sdk\client-libs\thirdparty입니다.

   >[!NOTE]
   >
   >AEM Forms를 사용한 프로그래밍 의 모든 Java 웹 서비스 빠른 시작(Forms 서비스 제외)은 JAX-WS를 사용하여 Java 프록시 파일을 만듭니다. 또한 모든 Java 웹 서비스 빠른 시작은 SwaRef를 사용합니다. (참조: [SwaRef를 사용하여 AEM Forms 호출](#invoking-aem-forms-using-swaref).)

**추가 참조**

[Apache Axis를 사용하여 Java 프록시 클래스 생성](#creating-java-proxy-classes-using-apache-axis)

[Base64 인코딩을 사용하여 AEM Forms 호출](#invoking-aem-forms-using-base64-encoding)

[HTTP를 통해 BLOB 데이터를 사용하여 AEM Forms 호출](#invoking-aem-forms-using-blob-data-over-http)

[SwaRef를 사용하여 AEM Forms 호출](#invoking-aem-forms-using-swaref)

## Apache Axis를 사용하여 Java 프록시 클래스 생성 {#creating-java-proxy-classes-using-apache-axis}

Apache Axis WSDL2Java 도구를 사용하여 Forms 서비스를 Java 프록시 클래스로 변환할 수 있습니다. 이러한 클래스를 사용하면 Forms 서비스 작업을 호출할 수 있습니다. Apache Ant를 사용하면 서비스 WSDL에서 Axis 라이브러리 파일을 생성할 수 있습니다. URL에서 Apache Axis를 다운로드할 수 있습니다 [https://ws.apache.org/axis/](https://ws.apache.org/axis/).

>[!NOTE]
>
>Forms 서비스와 관련된 웹 서비스 빠른 시작은 Apache Axis를 사용하여 만든 Java 프록시 클래스를 사용합니다. Forms 웹 서비스 빠른 시작에서는 Base64도 인코딩 유형으로 사용합니다. (참조: [Forms 서비스 API 빠른 시작](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts).)

다음 단계를 수행하여 Axis Java 라이브러리 파일을 생성할 수 있습니다.

1. 클라이언트 컴퓨터에 Apache Ant를 설치합니다. 다음에서 사용할 수 있습니다. [https://ant.apache.org/bindownload.cgi](https://ant.apache.org/bindownload.cgi).

   * bin 디렉터리를 클래스 경로에 추가합니다.
   * 설정 `ANT_HOME` 환경 변수를 Ant를 설치한 디렉토리에 추가합니다.

1. 클라이언트 컴퓨터에 Apache Axis 1.4를 설치합니다. 다음에서 사용할 수 있습니다. [https://ws.apache.org/axis/](https://ws.apache.org/axis/).
1. 의 Axis 설치 지침에 설명된 대로 웹 서비스 클라이언트에서 Axis JAR 파일을 사용하도록 클래스 경로를 설정합니다. [https://ws.apache.org/axis/java/install.html](https://ws.apache.org/axis/java/install.html).
1. Axis에서 Apache WSDL2Java 도구를 사용하여 Java 프록시 클래스를 생성합니다. 이 작업을 수행하기 위한 Ant 빌드 스크립트를 만듭니다. 다음 스크립트는 build.xml이라는 샘플 Ant 빌드 스크립트입니다.

   ```java
    <?xml version="1.0"?>
    <project name="axis-wsdl2java">
    
    <path id="axis.classpath">
    <fileset dir="C:\axis-1_4\lib" >
        <include name="**/*.jar" />
    </fileset>
    </path>
    
    <taskdef resource="axis-tasks.properties" classpathref="axis.classpath" />
    
    <target name="encryption-wsdl2java-client" description="task">
    <axis-wsdl2java
        output="C:\JavaFiles"
        testcase="false"
        serverside="false"
        verbose="true"
        username="administrator"
        password="password"
        url="http://localhost:8080/soap/services/EncryptionService?wsdl&lc_version=9.0.1" >
    </axis-wsdl2java>
    </target>
    
    </project>
   ```

   이 Ant 빌드 스크립트 내에서 `url` localhost에서 실행 중인 암호화 서비스 WSDL을 참조하도록 속성을 설정합니다. 다음 `username` 및 `password` 속성을 유효한 AEM forms 사용자 이름 및 암호로 설정해야 합니다.

1. BAT 파일을 만들어 Ant 빌드 스크립트를 실행합니다. 다음 명령은 Ant 빌드 스크립트 실행을 담당하는 BAT 파일 내에 위치할 수 있습니다.

   ```java
    ant -buildfile "build.xml" encryption-wsdl2java-client
   ```

   JAVA 파일은 다음에 지정된 대로 C:\JavaFiles 폴더에 기록됩니다. `output` 속성. Forms 서비스를 성공적으로 호출하려면 이러한 JAVA 파일을 클래스 경로로 가져옵니다.

   기본적으로 이러한 파일은 라는 Java 패키지에 속합니다 `com.adobe.idp.services`. 이러한 JAVA 파일을 JAR 파일에 배치하는 것이 좋습니다. 그런 다음 JAR 파일을 클라이언트 애플리케이션의 클래스 경로로 가져옵니다.

   >[!NOTE]
   >
   >.JAVA 파일을 JAR에 넣는 방법은 여러 가지가 있습니다. 한 가지 방법은 Eclipse와 같은 Java IDE를 사용하는 것입니다. Java 프로젝트를 만들고 `com.adobe.idp.services`패키지(모든 .JAVA 파일이 이 패키지에 속함). 그런 다음 모든 .JAVA 파일을 패키지로 가져옵니다. 마지막으로 프로젝트를 JAR 파일로 내보냅니다.

1. 에서 URL 수정 `EncryptionServiceLocator` 클래스를 사용하여 인코딩 유형을 지정할 수 있습니다. 예를 들어 base64를 사용하려면 다음을 지정합니다 `?blob=base64` 을(를) 확인하기 위해 `BLOB` object는 이진 데이터를 반환합니다. 즉, `EncryptionServiceLocator` 클래스에서 다음 코드 행을 찾습니다.

   ```java
    http://localhost:8080/soap/services/EncryptionService;
   ```

   및 을 다음과 같이 변경합니다.

   ```java
    http://localhost:8080/soap/services/EncryptionService?blob=base64;
   ```

1. Java 프로젝트의 클래스 경로에 다음 Axis JAR 파일을 추가합니다.

   * activation.jar
   * axis.jar
   * commons-codec-1.3.jar
   * commons-collections-3.1.jar
   * commons-discovery.jar
   * commons-logging.jar
   * dom3-xml-apis-2.5.0.jar
   * jai_imageio.jar
   * jaxen-1.1-beta-9.jar
   * jaxrpc.jar
   * log4j.jar
   * mail.jar
   * saaj.jar
   * wsdl4j.jar
   * xalan.jar
   * xbean.jar
   * xercesImpl.jar

   이러한 JAR 파일은 `[install directory]/Adobe/Adobe Experience Manager Forms/sdk/lib/thirdparty` 디렉토리.

**추가 참조**

[JAX-WS를 사용하여 Java 프록시 클래스 생성](#creating-java-proxy-classes-using-jax-ws)

[Base64 인코딩을 사용하여 AEM Forms 호출](#invoking-aem-forms-using-base64-encoding)

[HTTP를 통해 BLOB 데이터를 사용하여 AEM Forms 호출](#invoking-aem-forms-using-blob-data-over-http)

## Base64 인코딩을 사용하여 AEM Forms 호출 {#invoking-aem-forms-using-base64-encoding}

Base64 인코딩을 사용하여 AEM Forms 서비스를 호출할 수 있습니다. Base64 인코딩은 웹 서비스 호출 요청으로 전송된 첨부 파일을 인코딩합니다. 즉, `BLOB` 데이터가 전체 SOAP 메시지가 아닌 Base64로 인코딩되었습니다.

&quot;Base64 인코딩을 사용하여 AEM Forms 호출&quot;에서 이름이 인 다음 AEM Forms 단기 프로세스 호출을 설명합니다. `MyApplication/EncryptDocument` base64 인코딩을 사용하여

>[!NOTE]
>
>이 프로세스는 기존 AEM Forms 프로세스를 기반으로 하지 않습니다. 코드 예제를 따르려면 `MyApplication/EncryptDocument` Workbench를 사용합니다. (참조: [Workbench 사용](https://www.adobe.com/go/learn_aemforms_workbench_63).)

이 프로세스가 호출되면 다음 작업을 수행합니다.

1. 프로세스에 전달되는 비보안 PDF 문서를 가져옵니다. 이 작업은 `SetValue` 작업. 이 프로세스의 입력 매개 변수는 `document` 이름이 인 프로세스 변수 `inDoc`.
1. 암호로 PDF 문서를 암호화합니다. 이 작업은 `PasswordEncryptPDF` 작업. 암호로 암호화된 PDF 문서가 이라는 프로세스 변수에 반환됩니다 `outDoc`.

### Base64 인코딩을 사용하는 .NET 클라이언트 어셈블리 만들기 {#creating-a-net-client-assembly-that-uses-base64-encoding}

.NET 클라이언트 어셈블리를 만들어 Microsoft Visual Studio .NET 프로젝트에서 Forms 서비스를 호출할 수 있습니다. base64 인코딩을 사용하는 .NET 클라이언트 어셈블리를 만들려면 다음 단계를 수행합니다.

1. AEM Forms 호출 URL을 기반으로 프록시 클래스를 만듭니다.
1. .NET 클라이언트 어셈블리를 생성하는 Microsoft Visual Studio .NET 프로젝트를 만듭니다.

**프록시 클래스 만들기**

Microsoft Visual Studio와 함께 제공되는 도구를 사용하여 .NET 클라이언트 어셈블리를 만드는 데 사용되는 프록시 클래스를 만들 수 있습니다. 도구의 이름은 wsdl.exe이며 Microsoft Visual Studio 설치 폴더에 있습니다. 프록시 클래스를 만들려면 명령 프롬프트를 열고 wsdl.exe 파일이 포함된 폴더로 이동합니다. wsdl.exe 도구에 대한 자세한 내용은 *MSDN 도움말*.

명령 프롬프트에서 다음 명령을 입력합니다.

```java
 wsdl https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?WSDL&lc_version=9.0.1
```

기본적으로 이 도구는 WSDL의 이름을 기반으로 하는 동일한 폴더에 CS 파일을 만듭니다. 이 경우 이름이 인 CS 파일이 만들어집니다 *EncryptDocumentService.cs*. 이 CS 파일을 사용하여 호출 URL에 지정된 서비스를 호출할 수 있는 프록시 개체를 만듭니다.

다음을 포함하도록 프록시 클래스의 URL 수정 `?blob=base64` 을(를) 확인하기 위해 `BLOB` object는 이진 데이터를 반환합니다. 프록시 클래스에서 다음 코드 행을 찾습니다.

```java
 "https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument";
```

및 을 다음과 같이 변경합니다.

```java
 "https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?blob=base64";
```

다음 *Base64 인코딩을 사용하여 AEM Forms 호출* 섹션 사용 `MyApplication/EncryptDocument` 예를 들어, 다른 Forms 서비스용 .NET 클라이언트 어셈블리를 만드는 경우 다음을 바꾸십시오. `MyApplication/EncryptDocument` (서비스 이름 포함)

**.NET 클라이언트 어셈블리 개발**

.NET 클라이언트 어셈블리를 만드는 Visual Studio 클래스 라이브러리 프로젝트를 만듭니다. wsdl.exe를 사용하여 만든 CS 파일을 이 프로젝트로 가져올 수 있습니다. 이 프로젝트는 다른 Visual Studio .NET 프로젝트에서 서비스를 호출하는 데 사용할 수 있는 DLL 파일(.NET 클라이언트 어셈블리)을 생성합니다.

1. Microsoft Visual Studio .NET을 시작합니다.
1. 클래스 라이브러리 프로젝트를 만들고 이름을 DocumentService로 지정합니다.
1. wsdl.exe를 사용하여 만든 CS 파일을 가져옵니다.
1. 다음에서 **프로젝트** 메뉴, 선택 **참조 추가**.
1. 참조 추가 대화 상자에서 **System.Web.Services.dll**.
1. 클릭 **선택** 그런 다음 을 클릭합니다. **확인**.
1. 프로젝트를 컴파일하고 빌드합니다.

>[!NOTE]
>
>이 프로시저에서는 SOAP 요청을 로 보낼 때 사용할 수 있는 DocumentService.dll이라는 .NET 클라이언트 어셈블리를 만듭니다. `MyApplication/EncryptDocument` 서비스.

>[!NOTE]
>
>를 추가했는지 확인하십시오. `?blob=base64` .NET 클라이언트 어셈블리를 만드는 데 사용되는 프록시 클래스의 URL에 매핑할 수 없습니다. 그렇지 않으면 `BLOB` 개체.

**.NET 클라이언트 어셈블리 참조**

새로 만든 .NET 클라이언트 어셈블리를 클라이언트 응용 프로그램을 개발하는 컴퓨터에 배치합니다. .NET 클라이언트 어셈블리를 디렉터리에 배치한 후 프로젝트에서 참조할 수 있습니다. 또한 `System.Web.Services` 프로젝트의 라이브러리입니다. 이 라이브러리를 참조하지 않으면 .NET 클라이언트 어셈블리를 사용하여 서비스를 호출할 수 없습니다.

1. 다음에서 **프로젝트** 메뉴, 선택 **참조 추가**.
1. 다음을 클릭합니다. **.NET** 탭.
1. 클릭 **찾아보기** DocumentService.dll 파일을 찾습니다.
1. 클릭 **선택** 그런 다음 을 클릭합니다. **확인**.

**Base64 인코딩을 사용하는 .NET 클라이언트 어셈블리를 사용하여 서비스 호출**

다음을 호출할 수 있습니다. `MyApplication/EncryptDocument` Base64 인코딩을 사용하는 .NET 클라이언트 어셈블리를 사용하는 서비스(Workbench에서 빌드됨)입니다. 를 호출하려면 `MyApplication/EncryptDocument` 서비스에서 다음 단계를 수행합니다.

1. 다음을 사용하는 Microsoft .NET 클라이언트 어셈블리를 만듭니다. `MyApplication/EncryptDocument` 서비스 WSDL.
1. 클라이언트 Microsoft .NET 프로젝트를 만듭니다. 클라이언트 프로젝트에서 Microsoft .NET 클라이언트 어셈블리를 참조합니다. 참조 `System.Web.Services`.
1. Microsoft .NET 클라이언트 어셈블리를 사용하여 `MyApplication_EncryptDocumentService` 기본 생성자를 호출하여 개체를 작성합니다.
1. 설정 `MyApplication_EncryptDocumentService` 개체 `Credentials` 이 있는 속성 `System.Net.NetworkCredential` 개체. 다음 범위 내 `System.Net.NetworkCredential` 생성자에서 AEM forms 사용자 이름과 해당 암호를 지정합니다. .NET 클라이언트 응용 프로그램에서 AEM Forms과 SOAP 메시지를 성공적으로 교환할 수 있도록 하려면 인증 값을 설정하십시오.
1. 만들기 `BLOB` 개체를 만들 때 사용됩니다. 다음 `BLOB` 개체는에 대한 PDF 문서 전달을 저장하는 데 사용됩니다. `MyApplication/EncryptDocument` 프로세스.
1. 만들기 `System.IO.FileStream` 해당 생성자를 호출하여 개체를 작성합니다. PDF 문서의 파일 위치와 파일을 열 모드를 나타내는 문자열 값을 전달합니다.
1. 의 콘텐츠를 저장하는 바이트 배열 만들기 `System.IO.FileStream` 개체. 를 가져와서 바이트 배열의 크기를 결정할 수 있습니다 `System.IO.FileStream` 개체 `Length` 속성.
1. 를 호출하여 바이트 배열을 스트림 데이터로 채우기 `System.IO.FileStream` 개체 `Read` 메서드를 사용합니다. 읽을 바이트 배열, 시작 위치 및 스트림 길이를 전달합니다.
1. 채우기 `BLOB` 개체 할당 `binaryData` 속성을 바이트 배열의 콘텐츠와 함께 사용합니다.
1. 호출 `MyApplication/EncryptDocument` 를 호출하여 프로세스를 `MyApplication_EncryptDocumentService` 개체 `invoke` 메서드 및 전달 `BLOB` PDF 문서가 포함된 객체입니다. 이 프로세스는 내의 암호화된 PDF 문서를 반환합니다. `BLOB` 개체.
1. 만들기 `System.IO.FileStream` 개체를 호출하고 암호로 암호화된 문서의 파일 위치를 나타내는 문자열 값을 전달합니다.
1. 의 데이터 콘텐츠를 저장하는 바이트 배열 만들기 `BLOB` 개체에서 반환한 개체 `MyApplicationEncryptDocumentService` 개체 `invoke` 메서드를 사용합니다. 의 값을 가져와서 바이트 배열 채우기 `BLOB` 개체 `binaryData` 데이터 구성원입니다.
1. 만들기 `System.IO.BinaryWriter` 개체를 호출하고 `System.IO.FileStream` 개체.
1. 를 호출하여 바이트 배열 내용을 PDF 파일에 씁니다 `System.IO.BinaryWriter` 개체 `Write` 메서드 및 바이트 배열 전달.

### Java 프록시 클래스 및 Base64 인코딩을 사용하여 서비스 호출 {#invoking-a-service-using-java-proxy-classes-and-base64-encoding}

Java 프록시 클래스 및 Base64를 사용하여 AEM Forms 서비스를 호출할 수 있습니다. 를 호출하려면 `MyApplication/EncryptDocument` Java 프록시 클래스를 사용하는 서비스에서는 다음 단계를 수행합니다.

1. 다음을 사용하는 JAX-WS를 사용하여 Java 프록시 클래스 만들기 `MyApplication/EncryptDocument` 서비스 WSDL. 다음 WSDL 끝점을 사용합니다.

   `https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?WSDL&lc_version=9.0.1`

   >[!NOTE]
   >
   >바꾸기 `hiro-xp` *AEM Forms을 호스팅하는 J2EE 애플리케이션 서버의 IP 주소입니다.*

1. JAX-WS를 사용하여 만든 Java 프록시 클래스를 JAR 파일에 패키지합니다.
1. 다음 경로에 Java 프록시 JAR 파일과 JAR 파일을 포함합니다.

   &lt;install directory=&quot;&quot;>\Adobe\Adobe_Experience_Manager_forms\sdk\client-libs\thirdparty

   를 Java 클라이언트 프로젝트의 클래스 경로에 추가합니다.

1. 만들기 `MyApplicationEncryptDocumentService` 개체를 만들 때 사용됩니다.
1. 만들기 `MyApplicationEncryptDocument` 를 호출하여 개체 `MyApplicationEncryptDocumentService` 개체 `getEncryptDocument` 메서드를 사용합니다.
1. 다음 데이터 멤버에 값을 할당하여 AEM Forms을 호출하는 데 필요한 연결 값을 설정합니다.

   * WSDL 끝점 및 인코딩 유형을 `javax.xml.ws.BindingProvider` 개체 `ENDPOINT_ADDRESS_PROPERTY` 필드. 를 호출하려면 `MyApplication/EncryptDocument` base64 인코딩을 사용하는 서비스에서는 다음 URL 값을 지정합니다.

     `https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?blob=base64`

   * AEM Forms 사용자를 `javax.xml.ws.BindingProvider` 개체 `USERNAME_PROPERTY` 필드.
   * 에 해당 암호 값을 할당합니다. `javax.xml.ws.BindingProvider` 개체 `PASSWORD_PROPERTY` 필드.

   다음 코드 예제에서는 이 애플리케이션 논리를 보여 줍니다.

   ```java
    //Set connection values required to invoke AEM Forms
    String url = "https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?blob=base64";
    String username = "administrator";
    String password = "password";
    ((BindingProvider) encryptDocClient).getRequestContext().put(BindingProvider.ENDPOINT_ADDRESS_PROPERTY, url);
    ((BindingProvider) encryptDocClient).getRequestContext().put(BindingProvider.USERNAME_PROPERTY, username);
    ((BindingProvider) encryptDocClient).getRequestContext().put(BindingProvider.PASSWORD_PROPERTY, password);
   ```

1. 에 보낼 PDF 문서 검색 `MyApplication/EncryptDocument` 을(를) 만드는 방법 `java.io.FileInputStream` 개체를 만들 때 사용됩니다. PDF 문서의 위치를 지정하는 문자열 값을 전달합니다.
1. 바이트 배열을 만들어 의 내용으로 채웁니다. `java.io.FileInputStream` 개체.
1. 만들기 `BLOB` 개체를 만들 때 사용됩니다.
1. 채우기 `BLOB` 개체 `setBinaryData` 메서드 및 바이트 배열 전달. 다음 `BLOB` 개체 `setBinaryData` 는 Base64 인코딩을 사용할 때 호출할 메서드입니다. 서비스 요청에서 BLOB 개체 공급을 참조하십시오.
1. 호출 `MyApplication/EncryptDocument` 를 호출하여 프로세스를 `MyApplicationEncryptDocument` 개체 `invoke` 메서드를 사용합니다. 전달 `BLOB` PDF 문서가 포함된 객체입니다. invoke 메서드는 `BLOB` 암호화된 PDF 문서를 포함하는 개체입니다.
1. 를 호출하여 암호화된 PDF 문서를 포함하는 바이트 배열을 만듭니다. `BLOB` 개체 `getBinaryData` 메서드를 사용합니다.
1. 암호화된 PDF 문서를 PDF 파일로 저장합니다. 바이트 배열을 파일에 씁니다.

**추가 참조**

[빠른 시작: Java 프록시 파일 및 Base64 인코딩을 사용하여 서비스 호출](/help/forms/developing/invocation-api-quick-starts.md#quick-start-invoking-a-service-using-java-proxy-files-and-base64-encoding)

[Base64 인코딩을 사용하는 .NET 클라이언트 어셈블리 만들기](#creating-a-net-client-assembly-that-uses-base64-encoding)

## MTOM을 사용하여 AEM Forms 호출 {#invoking-aem-forms-using-mtom}

웹 서비스 표준 MTOM을 사용하여 AEM Forms 서비스를 호출할 수 있습니다. 이 표준은 PDF 문서와 같은 바이너리 데이터가 인터넷이나 인트라넷을 통해 전송되는 방식을 정의합니다. MTOM의 특징은 `XOP:Include` 요소를 생성하지 않습니다. 이 요소는 XML XOP(Binary Optimized Packaging) 사양에 정의되어 SOAP 메시지의 이진 첨부 파일을 참조합니다.

여기에서는 MTOM을 사용하여 다음과 같은 AEM Forms 단기 프로세스를 호출하는 방법에 대해 설명합니다 `MyApplication/EncryptDocument`.

>[!NOTE]
>
>이 프로세스는 기존 AEM Forms 프로세스를 기반으로 하지 않습니다. 코드 예제를 따르려면 `MyApplication/EncryptDocument` Workbench를 사용합니다. (참조: [Workbench 사용](https://www.adobe.com/go/learn_aemforms_workbench_63).)

이 프로세스가 호출되면 다음 작업을 수행합니다.

1. 프로세스에 전달되는 비보안 PDF 문서를 가져옵니다. 이 작업은 `SetValue` 작업. 이 프로세스의 입력 매개 변수는 `document` 이름이 인 프로세스 변수 `inDoc`.
1. 암호로 PDF 문서를 암호화합니다. 이 작업은 `PasswordEncryptPDF` 작업. 암호로 암호화된 PDF 문서가 이라는 프로세스 변수에 반환됩니다 `outDoc`.

>[!NOTE]
>
>AEM Forms 버전 9에서 MTOM 지원이 추가되었습니다.

>[!NOTE]
>
>MTOM 전송 프로토콜을 사용하는 JAX WS 기반 응용 프로그램은 25MB의 송수신 데이터로 제한됩니다. 이 제한은 JAX-WS의 버그 때문입니다. 전송 파일과 수신 파일의 통합 크기가 25MB를 초과하는 경우 MTOM 전송 프로토콜 대신 SwaRef 전송 프로토콜을 사용합니다. 그렇지 않으면 `OutOfMemory` 예외.

여기에서는 Microsoft .NET 프로젝트 내에서 MTOM을 사용하여 AEM Forms 서비스를 호출하는 방법에 대해 설명합니다. 사용되는 .NET 프레임워크는 3.5이고 개발 환경은 Visual Studio 2008입니다. 개발 컴퓨터에 WSE(Web Service Enhancements)가 설치되어 있으면 제거합니다. .NET 3.5 프레임워크는 WCF(Windows Communication Foundation)라는 SOAP 프레임워크를 지원합니다. MTOM을 사용하여 AEM Forms을 호출하는 경우 WSE가 아닌 WCF만 지원됩니다.

### MTOM을 사용하여 서비스를 호출하는 .NET 프로젝트 만들기 {#creating-a-net-project-that-invokes-a-service-using-mtom}

웹 서비스를 사용하여 AEM Forms 서비스를 호출할 수 있는 Microsoft .NET 프로젝트를 만들 수 있습니다. 먼저 Visual Studio 2008을 사용하여 Microsoft .NET 프로젝트를 만듭니다. AEM Forms 서비스를 호출하려면 프로젝트 내에서 호출할 AEM Forms 서비스에 대한 서비스 참조를 만듭니다. 서비스 참조를 만들 때 AEM Forms 서비스에 대한 URL을 지정하십시오.

```java
 http://localhost:8080/soap/services/MyApplication/EncryptDocument?WSDL&lc_version=9.0.1
```

바꾸기 `localhost` AEM Forms을 호스팅하는 J2EE 애플리케이션 서버의 IP 주소입니다. 바꾸기 `MyApplication/EncryptDocument` 를 호출하려는 AEM Forms 서비스의 이름으로 바꿉니다. 예를 들어 Rights Management 작업을 호출하려면 다음을 지정합니다.

`http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`

다음 `lc_version` 옵션을 사용하면 MTOM과 같은 AEM Forms 기능을 사용할 수 있습니다. 을 지정하지 않고 `lc_version` 옵션을 선택하면 MTOM을 사용하여 AEM Forms을 호출할 수 없습니다.

서비스 참조를 만든 후에는 .NET 프로젝트 내에서 AEM Forms 서비스와 연결된 데이터 형식을 사용할 수 있습니다. AEM Forms 서비스를 호출하는 .NET 프로젝트를 만들려면 다음 단계를 수행하십시오.

1. Microsoft Visual Studio 2008을 사용하여 .NET 프로젝트를 만듭니다.
1. 다음에서 **프로젝트** 메뉴, 선택 **서비스 참조 추가**.
1. 다음에서 **주소** 대화 상자에서 AEM Forms 서비스에 WSDL을 지정합니다. 예:

   ```java
    http://localhost:8080/soap/services/MyApplication/EncryptDocument?WSDL&lc_version=9.0.1
   ```

1. 클릭 **이동** 그런 다음 을 클릭합니다. **확인**.

### .NET 프로젝트에서 MTOM을 사용하여 서비스 호출 {#invoking-a-service-using-mtom-in-a-net-project}

다음을 고려하십시오. `MyApplication/EncryptDocument` 비보안 PDF 문서를 수락하고 암호로 암호화된 PDF 문서를 반환하는 프로세스입니다. 를 호출하려면 `MyApplication/EncryptDocument` (Workbench에 내장된) MTOM을 사용하여 프로세스를 수행하려면 다음 단계를 수행합니다.

1. Microsoft .NET 프로젝트를 만듭니다.
1. 만들기 `MyApplication_EncryptDocumentClient` 기본 생성자를 사용하여 개체를 작성합니다.
1. 만들기 `MyApplication_EncryptDocumentClient.Endpoint.Address` 을 사용하여 개체 `System.ServiceModel.EndpointAddress` 생성자입니다. WSDL을 지정하는 문자열 값을 AEM Forms 서비스 및 인코딩 형식에 전달합니다.

   ```java
    https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?blob=mtom
   ```

   를 사용할 필요가 없습니다. `lc_version` 특성. 이 속성은 서비스 참조를 만들 때 사용됩니다. 그러나 다음을 지정해야 합니다 `?blob=mtom`.

   >[!NOTE]
   >
   >바꾸기 `hiro-xp` *AEM Forms을 호스팅하는 J2EE 애플리케이션 서버의 IP 주소입니다.*

1. 만들기 `System.ServiceModel.BasicHttpBinding` 의 값을 가져와서 개체 `EncryptDocumentClient.Endpoint.Binding` 데이터 구성원입니다. 반환 값을 다음으로 캐스트 `BasicHttpBinding`.
1. 설정 `System.ServiceModel.BasicHttpBinding` 개체 `MessageEncoding` 데이터 멤버 대상 `WSMessageEncoding.Mtom`. 이 값은 MTOM이 사용되도록 합니다.
1. 다음 작업을 수행하여 기본 HTTP 인증을 활성화합니다.

   * 데이터 멤버에 AEM Forms 사용자 이름 할당 `MyApplication_EncryptDocumentClient.ClientCredentials.UserName.UserName`.
   * 해당 암호 값을 데이터 멤버에 할당 `MyApplication_EncryptDocumentClient.ClientCredentials.UserName.Password`.
   * 상수 값 지정 `HttpClientCredentialType.Basic` 데이터 멤버에게 `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
   * 상수 값 지정 `BasicHttpSecurityMode.TransportCredentialOnly` 데이터 멤버에게 `BasicHttpBindingSecurity.Security.Mode`.

   다음 코드 예제에서는 이러한 작업을 보여 줍니다.

   ```java
    //Enable BASIC HTTP authentication
    encryptProcess.ClientCredentials.UserName.UserName = "administrator";
    encryptProcess.ClientCredentials.UserName.Password = "password";
    b.Security.Transport.ClientCredentialType = HttpClientCredentialType.Basic;
    b.Security.Mode = BasicHttpSecurityMode.TransportCredentialOnly;
    b.MaxReceivedMessageSize = 4000000;
    b.MaxBufferSize = 4000000;
    b.ReaderQuotas.MaxArrayLength = 4000000;
   ```

1. 만들기 `BLOB` 개체를 만들 때 사용됩니다. 다음 `BLOB` 개체는에 전달할 PDF 문서를 저장하는 데 사용됩니다 `MyApplication/EncryptDocument` 프로세스.
1. 만들기 `System.IO.FileStream` 해당 생성자를 호출하여 개체를 작성합니다. PDF 문서의 파일 위치와 파일을 열 모드를 나타내는 문자열 값을 전달합니다.
1. 의 콘텐츠를 저장하는 바이트 배열 만들기 `System.IO.FileStream` 개체. 를 가져와서 바이트 배열의 크기를 결정할 수 있습니다 `System.IO.FileStream` 개체 `Length` 속성.
1. 를 호출하여 바이트 배열을 스트림 데이터로 채우기 `System.IO.FileStream` 개체 `Read` 메서드를 사용합니다. 읽을 바이트 배열, 시작 위치 및 스트림 길이를 전달합니다.
1. 채우기 `BLOB` 개체 할당 `MTOM` 바이트 배열의 내용이 포함된 데이터 멤버입니다.
1. 호출 `MyApplication/EncryptDocument` 를 호출하여 프로세스를 `MyApplication_EncryptDocumentClient` 개체 `invoke` 메서드를 사용합니다. 전달 `BLOB` PDF 문서가 포함된 객체입니다. 이 프로세스는 내의 암호화된 PDF 문서를 반환합니다. `BLOB` 개체.
1. 만들기 `System.IO.FileStream` 해당 생성자를 호출하고 보안 PDF 문서의 파일 위치를 나타내는 문자열 값을 전달하여 객체를 생성합니다.
1. 의 데이터 콘텐츠를 저장하는 바이트 배열 만들기 `BLOB` 에서 반환한 개체 `invoke` 메서드를 사용합니다. 의 값을 가져와서 바이트 배열 채우기 `BLOB` 개체 `MTOM` 데이터 구성원입니다.
1. 만들기 `System.IO.BinaryWriter` 개체를 호출하고 `System.IO.FileStream` 개체.
1. 를 호출하여 바이트 배열의 내용을 PDF 파일에 씁니다 `System.IO.BinaryWriter` 개체 `Write` 메서드 및 바이트 배열 전달.

>[!NOTE]
>
>대부분의 AEM Forms 서비스 작업에는 MTOM 빠른 시작이 있습니다. 서비스의 해당 빠른 시작 섹션에서 이러한 빠른 시작을 볼 수 있습니다. 예를 들어 출력 빠른 시작 섹션을 보려면 [출력 서비스 API 빠른 시작](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap).

**추가 참조**

[빠른 시작: .NET 프로젝트에서 MTOM을 사용하여 서비스 호출](/help/forms/developing/invocation-api-quick-starts.md#quick-start-invoking-a-service-using-mtom-in-a-net-project)

[웹 서비스를 사용하여 여러 서비스에 액세스](#accessing-multiple-services-using-web-services)

[인간 중심의 장기 프로세스를 호출하는 ASP.NET 웹 애플리케이션 만들기](/help/forms/developing/invoking-human-centric-long-lived.md#creating-an-asp-net-web-application-that-invokes-a-human-centric-long-lived-process)

## SwaRef를 사용하여 AEM Forms 호출 {#invoking-aem-forms-using-swaref}

SwaRef를 사용하여 AEM Forms 서비스를 호출할 수 있습니다. 의 콘텐츠 `wsi:swaRef` XML 요소는 첨부 파일에 대한 참조를 저장하는 SOAP 본문 내에 첨부 파일로 전송됩니다. SwaRef를 사용하여 Forms 서비스를 호출하는 경우 XML Web services용 Java API(JAX-WS)를 사용하여 Java 프록시 클래스를 만듭니다. (참조: [XML Web Services용 Java API](https://jax-ws.dev.java.net/jax-ws-ea3/docs/mtom-swaref.html).)

여기에서는 다음 Forms 단기 프로세스 호출에 대해 설명합니다. `MyApplication/EncryptDocument` SwaRef를 사용하여

>[!NOTE]
>
>이 프로세스는 기존 AEM Forms 프로세스를 기반으로 하지 않습니다. 코드 예제를 따르려면 `MyApplication/EncryptDocument` Workbench를 사용합니다. (참조: [Workbench 사용](https://www.adobe.com/go/learn_aemforms_workbench_63).)

이 프로세스가 호출되면 다음 작업을 수행합니다.

1. 프로세스에 전달되는 비보안 PDF 문서를 가져옵니다. 이 작업은 `SetValue` 작업. 이 프로세스의 입력 매개 변수는 `document` 이름이 인 프로세스 변수 `inDoc`.
1. 암호로 PDF 문서를 암호화합니다. 이 작업은 `PasswordEncryptPDF` 작업. 암호로 암호화된 PDF 문서가 이라는 프로세스 변수에 반환됩니다 `outDoc`.

>[!NOTE]
>
>AEM Forms에 SwaRef 지원이 추가됨

아래에서는 Java 클라이언트 애플리케이션 내에서 SwaRef를 사용하여 Forms 서비스를 호출하는 방법에 대해 설명합니다. Java 응용 프로그램은 JAX-WS를 사용하여 만든 프록시 클래스를 사용합니다.

### SwaRef를 사용하는 JAX-WS 라이브러리 파일을 사용하여 서비스 호출 {#invoke-a-service-using-jax-ws-library-files-that-use-swaref}

를 호출하려면 `MyApplication/EncryptDocument` jax-WS 및 SwaRef를 사용하여 만든 Java 프록시 파일을 사용하여 프로세스를 수행하려면 다음 단계를 수행하십시오.

1. 다음을 사용하는 JAX-WS를 사용하여 Java 프록시 클래스 만들기 `MyApplication/EncryptDocument` 서비스 WSDL. 다음 WSDL 끝점을 사용합니다.

   ```java
    https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?WSDL&lc_version=9.0.1
   ```

   자세한 내용은 [JAX-WS를 사용하여 Java 프록시 클래스 생성](#creating-java-proxy-classes-using-jax-ws).

   >[!NOTE]
   >
   >바꾸기 `hiro-xp` *AEM Forms을 호스팅하는 J2EE 애플리케이션 서버의 IP 주소입니다.*

1. JAX-WS를 사용하여 만든 Java 프록시 클래스를 JAR 파일에 패키지합니다.
1. 다음 경로에 Java 프록시 JAR 파일과 JAR 파일을 포함합니다.

   &lt;install directory=&quot;&quot;>\Adobe\Adobe_Experience_Manager_forms\sdk\client-libs\thirdparty

   를 Java 클라이언트 프로젝트의 클래스 경로에 추가합니다.

1. 만들기 `MyApplicationEncryptDocumentService` 개체를 만들 때 사용됩니다.
1. 만들기 `MyApplicationEncryptDocument` 를 호출하여 개체 `MyApplicationEncryptDocumentService` 개체 `getEncryptDocument` 메서드를 사용합니다.
1. 다음 데이터 멤버에 값을 할당하여 AEM Forms을 호출하는 데 필요한 연결 값을 설정합니다.

   * WSDL 끝점 및 인코딩 유형을 `javax.xml.ws.BindingProvider` 개체 `ENDPOINT_ADDRESS_PROPERTY` 필드. 를 호출하려면 `MyApplication/EncryptDocument` swaRef 인코딩을 사용하는 서비스에서 다음 URL 값을 지정합니다.

     ` https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?blob=swaref`

   * AEM Forms 사용자를 `javax.xml.ws.BindingProvider` 개체 `USERNAME_PROPERTY` 필드.
   * 에 해당 암호 값을 할당합니다. `javax.xml.ws.BindingProvider` 개체 `PASSWORD_PROPERTY` 필드.

   다음 코드 예제에서는 이 애플리케이션 논리를 보여 줍니다.

   ```java
    //Set connection values required to invoke AEM Forms
    String url = "https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?blob=swaref";
    String username = "administrator";
    String password = "password";
    ((BindingProvider) encryptDocClient).getRequestContext().put(BindingProvider.ENDPOINT_ADDRESS_PROPERTY, url);
    ((BindingProvider) encryptDocClient).getRequestContext().put(BindingProvider.USERNAME_PROPERTY, username);
    ((BindingProvider) encryptDocClient).getRequestContext().put(BindingProvider.PASSWORD_PROPERTY, password);
   ```

1. 에 보낼 PDF 문서 검색 `MyApplication/EncryptDocument` 을(를) 만드는 방법 `java.io.File` 개체를 만들 때 사용됩니다. PDF 문서의 위치를 지정하는 문자열 값을 전달합니다.
1. 만들기 `javax.activation.DataSource` 을 사용하여 개체 `FileDataSource` 생성자입니다. 전달 `java.io.File` 개체.
1. 만들기 `javax.activation.DataHandler` 개체를 생성자를 사용하고 `javax.activation.DataSource` 개체.
1. 만들기 `BLOB` 개체를 만들 때 사용됩니다.
1. 채우기 `BLOB` 개체 `setSwaRef` 메서드 및 전달 `javax.activation.DataHandler` 개체.
1. 호출 `MyApplication/EncryptDocument` 를 호출하여 프로세스를 `MyApplicationEncryptDocument` 개체 `invoke` 메서드 및 전달 `BLOB` PDF 문서가 포함된 객체입니다. invoke 메서드는 `BLOB` 암호화된 PDF 문서가 포함된 개체입니다.
1. 채우기 `javax.activation.DataHandler` 를 호출하여 개체 `BLOB` 개체 `getSwaRef` 메서드를 사용합니다.
1. 변환 `javax.activation.DataHandler` 에 대한 오브젝트 `java.io.InputSteam` 를 호출하여 인스턴스 `javax.activation.DataHandler` 개체 `getInputStream` 메서드를 사용합니다.
1. 다음을 작성합니다. `java.io.InputSteam` 인스턴스를 암호화된 PDF 문서를 나타내는 PDF 파일로 복사합니다.

>[!NOTE]
>
>대부분의 AEM Forms 서비스 작업에는 SwaRef 빠른 시작이 있습니다. 서비스의 해당 빠른 시작 섹션에서 이러한 빠른 시작을 볼 수 있습니다. 예를 들어 출력 빠른 시작 섹션을 보려면 [출력 서비스 API 빠른 시작](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap).

**추가 참조**

[빠른 시작: Java 프로젝트에서 SwaRef를 사용하여 서비스 호출](/help/forms/developing/invocation-api-quick-starts.md#quick-start-invoking-a-service-using-swaref-in-a-java-project)

## HTTP를 통해 BLOB 데이터를 사용하여 AEM Forms 호출 {#invoking-aem-forms-using-blob-data-over-http}

웹 서비스를 사용하여 AEM Forms 서비스를 호출하고 HTTP를 통해 BLOB 데이터를 전달할 수 있습니다. base64 인코딩, DIME 또는 MIME을 사용하는 대신 HTTP를 통해 BLOB 데이터를 전달하는 것은 대체 기술입니다. 예를 들어 DIME 또는 MIME을 지원하지 않는 웹 서비스 개선 3.0을 사용하는 Microsoft .NET 프로젝트에서 HTTP를 통해 데이터를 전달할 수 있습니다. HTTP를 통해 BLOB 데이터를 사용할 때 AEM Forms 서비스가 호출되기 전에 입력 데이터가 업로드됩니다.

&quot;HTTP를 통해 BLOB 데이터를 사용하여 AEM Forms 호출&quot;에서는 다음과 같은 AEM Forms 단기 프로세스 호출을 설명합니다. `MyApplication/EncryptDocument` HTTP를 통해 BLOB 데이터를 전달합니다.

>[!NOTE]
>
>이 프로세스는 기존 AEM Forms 프로세스를 기반으로 하지 않습니다. 코드 예제를 따르려면 `MyApplication/EncryptDocument` Workbench를 사용합니다. (참조: [Workbench 사용](https://www.adobe.com/go/learn_aemforms_workbench_63).)

이 프로세스가 호출되면 다음 작업을 수행합니다.

1. 프로세스에 전달되는 비보안 PDF 문서를 가져옵니다. 이 작업은 `SetValue` 작업. 이 프로세스의 입력 매개 변수는 `document` 이름이 인 프로세스 변수 `inDoc`.
1. 암호로 PDF 문서를 암호화합니다. 이 작업은 `PasswordEncryptPDF` 작업. 암호로 암호화된 PDF 문서가 이라는 프로세스 변수에 반환됩니다 `outDoc`.

>[!NOTE]
>
>SOAP를 사용하여 AEM Forms을 호출하는 방법에 대해 잘 알고 있는 것이 좋습니다. (참조: [웹 서비스를 사용하여 AEM Forms 호출](#invoking-aem-forms-using-web-services).)

### HTTP를 통해 데이터를 사용하는 .NET 클라이언트 어셈블리 만들기 {#creating-a-net-client-assembly-that-uses-data-over-http}

HTTP를 통해 데이터를 사용하는 클라이언트 어셈블리를 만들려면 [Base64 인코딩을 사용하여 AEM Forms 호출](#invoking-aem-forms-using-base64-encoding). 단, 다음을 포함하도록 프록시 클래스의 URL을 수정합니다 `?blob=http` 대신 `?blob=base64`. 이 작업을 수행하면 데이터가 HTTP를 통해 전달됩니다. 프록시 클래스에서 다음 코드 행을 찾습니다.

```java
 "http://localhost:8080/soap/services/MyApplication/EncryptDocument";
```

및 을 다음과 같이 변경합니다.

```java
 "http://localhost:8080/soap/services/MyApplication/EncryptDocument?blob=http";
```

**.NET clienMyApplication/EncryptDocument 어셈블리 참조**

클라이언트 응용 프로그램을 개발하는 컴퓨터에 새 .NET 클라이언트 어셈블리를 배치합니다. .NET 클라이언트 어셈블리를 디렉터리에 배치한 후 프로젝트에서 참조할 수 있습니다. 참조 `System.Web.Services` 프로젝트의 라이브러리입니다. 이 라이브러리를 참조하지 않으면 .NET 클라이언트 어셈블리를 사용하여 서비스를 호출할 수 없습니다.

1. 다음에서 **프로젝트** 메뉴, 선택 **참조 추가**.
1. 다음을 클릭합니다. **.NET** 탭.
1. 클릭 **찾아보기** DocumentService.dll 파일을 찾습니다.
1. 클릭 **선택** 그런 다음 을 클릭합니다. **확인**.

**HTTP를 통해 BLOB 데이터를 사용하는 .NET 클라이언트 어셈블리를 사용하여 서비스 호출**

다음을 호출할 수 있습니다. `MyApplication/EncryptDocument` HTTP를 통해 데이터를 사용하는 .NET 클라이언트 어셈블리를 사용하는 서비스(Workbench에서 빌드됨). 를 호출하려면 `MyApplication/EncryptDocument` 서비스에서 다음 단계를 수행합니다.

1. .NET 클라이언트 어셈블리를 만듭니다.
1. Microsoft .NET 클라이언트 어셈블리를 참조합니다. 클라이언트 Microsoft .NET 프로젝트를 만듭니다. 클라이언트 프로젝트에서 Microsoft .NET 클라이언트 어셈블리를 참조합니다. 참조 `System.Web.Services`.
1. Microsoft .NET 클라이언트 어셈블리를 사용하여 `MyApplication_EncryptDocumentService` 기본 생성자를 호출하여 개체를 작성합니다.
1. 설정 `MyApplication_EncryptDocumentService` 개체 `Credentials` 이 있는 속성 `System.Net.NetworkCredential` 개체. 다음 범위 내 `System.Net.NetworkCredential` 생성자에서 AEM forms 사용자 이름과 해당 암호를 지정합니다. .NET 클라이언트 응용 프로그램에서 AEM Forms과 SOAP 메시지를 성공적으로 교환할 수 있도록 하려면 인증 값을 설정하십시오.
1. 만들기 `BLOB` 개체를 만들 때 사용됩니다. 다음 `BLOB` 개체를 사용하여 데이터를 `MyApplication/EncryptDocument` 프로세스.
1. 에 문자열 값 할당 `BLOB` 개체 `remoteURL` 에 전달할 PDF 문서의 URI 위치를 지정하는 데이터 멤버 `MyApplication/EncryptDocument`서비스.
1. 호출 `MyApplication/EncryptDocument` 를 호출하여 프로세스를 `MyApplication_EncryptDocumentService` 개체 `invoke` 메서드 및 전달 `BLOB` 개체. 이 프로세스는 내의 암호화된 PDF 문서를 반환합니다. `BLOB` 개체.
1. 만들기 `System.UriBuilder` 개체를 생성자를 사용하고 반환된 값을 전달하여 `BLOB` 개체 `remoteURL` 데이터 구성원입니다.
1. 변환 `System.UriBuilder` 에 대한 오브젝트 `System.IO.Stream` 개체. (이 목록 다음에 나오는 C# 빠른 시작은 이 작업을 수행하는 방법을 보여 줍니다.)
1. 바이트 배열을 만들어 `System.IO.Stream` 개체.
1. 만들기 `System.IO.BinaryWriter` 개체를 호출하고 `System.IO.FileStream` 개체.
1. 를 호출하여 바이트 배열 내용을 PDF 파일에 씁니다 `System.IO.BinaryWriter` 개체 `Write` 메서드 및 바이트 배열 전달.

### HTTP를 통해 Java 프록시 클래스 및 BLOB 데이터를 사용하여 서비스 호출 {#invoking-a-service-using-java-proxy-classes-and-blob-data-over-http}

HTTP를 통해 Java 프록시 클래스 및 BLOB 데이터를 사용하여 AEM Forms 서비스를 호출할 수 있습니다. 를 호출하려면 `MyApplication/EncryptDocument` Java 프록시 클래스를 사용하는 서비스에서는 다음 단계를 수행합니다.

1. 다음을 사용하는 JAX-WS를 사용하여 Java 프록시 클래스 만들기 `MyApplication/EncryptDocument` 서비스 WSDL. 다음 WSDL 끝점을 사용합니다.

   ```java
    https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?WSDL&lc_version=9.0.1
   ```

   자세한 내용은 [JAX-WS를 사용하여 Java 프록시 클래스 생성](#creating-java-proxy-classes-using-jax-ws).

   >[!NOTE]
   >
   >바꾸기 `hiro-xp` *AEM Forms을 호스팅하는 J2EE 애플리케이션 서버의 IP 주소입니다.*

1. JAX-WS를 사용하여 만든 Java 프록시 클래스를 JAR 파일에 패키지합니다.
1. 다음 경로에 Java 프록시 JAR 파일과 JAR 파일을 포함합니다.

   &lt;install directory=&quot;&quot;>\Adobe\Adobe_Experience_Manager_forms\sdk\client-libs\thirdparty

   를 Java 클라이언트 프로젝트의 클래스 경로에 추가합니다.

1. 만들기 `MyApplicationEncryptDocumentService` 개체를 만들 때 사용됩니다.
1. 만들기 `MyApplicationEncryptDocument` 를 호출하여 개체 `MyApplicationEncryptDocumentService` 개체 `getEncryptDocument` 메서드를 사용합니다.
1. 다음 데이터 멤버에 값을 할당하여 AEM Forms을 호출하는 데 필요한 연결 값을 설정합니다.

   * WSDL 끝점 및 인코딩 유형을 `javax.xml.ws.BindingProvider` 개체 `ENDPOINT_ADDRESS_PROPERTY` 필드. 를 호출하려면 `MyApplication/EncryptDocument` http 인코딩에 대해 BLOB를 사용하는 서비스에서는 다음 URL 값을 지정합니다.

     `https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?blob=http`

   * AEM Forms 사용자를 `javax.xml.ws.BindingProvider` 개체 `USERNAME_PROPERTY` 필드.
   * 에 해당 암호 값을 할당합니다. `javax.xml.ws.BindingProvider` 개체 `PASSWORD_PROPERTY` 필드.

   다음 코드 예제에서는 이 애플리케이션 논리를 보여 줍니다.

   ```java
    //Set connection values required to invoke AEM Forms
    String url = "https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?blob=http";
    String username = "administrator";
    String password = "password";
    ((BindingProvider) encryptDocClient).getRequestContext().put(BindingProvider.ENDPOINT_ADDRESS_PROPERTY, url);
    ((BindingProvider) encryptDocClient).getRequestContext().put(BindingProvider.USERNAME_PROPERTY, username);
    ((BindingProvider) encryptDocClient).getRequestContext().put(BindingProvider.PASSWORD_PROPERTY, password);
   ```

1. 만들기 `BLOB` 개체를 만들 때 사용됩니다.
1. 채우기 `BLOB` 개체 `setRemoteURL` 메서드를 사용합니다. 에 전달할 PDF 문서의 URI 위치를 지정하는 문자열 값 전달 `MyApplication/EncryptDocument` 서비스.
1. 호출 `MyApplication/EncryptDocument` 를 호출하여 프로세스를 `MyApplicationEncryptDocument` 개체 `invoke` 메서드 및 전달 `BLOB` PDF 문서가 포함된 객체입니다. 이 프로세스는 내의 암호화된 PDF 문서를 반환합니다. `BLOB` 개체.
1. 바이트 배열을 만들어 암호화된 PDF 문서를 나타내는 데이터 스트림을 저장합니다. 호출 `BLOB` 개체 `getRemoteURL` 메서드(사용 `BLOB` 개체에서 반환한 개체 `invoke` 메서드).
1. 만들기 `java.io.File` 개체를 만들 때 사용됩니다. 이 개체는 암호화된 PDF 문서를 나타냅니다.
1. 만들기 `java.io.FileOutputStream` 개체를 생성자를 사용하고 `java.io.File` 개체.
1. 호출 `java.io.FileOutputStream` 개체 `write` 메서드를 사용합니다. 암호화된 PDF 문서를 나타내는 데이터 스트림이 포함된 바이트 배열을 전달합니다.

## DIME를 사용하여 AEM Forms 호출 {#invoking-aem-forms-using-dime}

첨부 파일이 있는 SOAP를 사용하여 AEM Forms 서비스를 호출할 수 있습니다. AEM Forms은 MIME 및 DIME 웹 서비스 표준을 모두 지원합니다. DIME를 사용하면 첨부 파일을 인코딩하는 대신 호출 요청과 함께 PDF 문서와 같은 바이너리 첨부 파일을 보낼 수 있습니다. 다음 *DIME를 사용하여 AEM Forms 호출* 다음 AEM Forms 단기 프로세스 호출에 대해 설명합니다. `MyApplication/EncryptDocument` DIME를 사용합니다.

이 프로세스가 호출되면 다음 작업을 수행합니다.

1. 프로세스에 전달되는 비보안 PDF 문서를 가져옵니다. 이 작업은 `SetValue` 작업. 이 프로세스의 입력 매개 변수는 `document` 이름이 인 프로세스 변수 `inDoc`.
1. 암호로 PDF 문서를 암호화합니다. 이 작업은 `PasswordEncryptPDF` 작업. 암호로 암호화된 PDF 문서가 이라는 프로세스 변수에 반환됩니다 `outDoc`.

이 프로세스는 기존 AEM Forms 프로세스를 기반으로 하지 않습니다. 코드 예제를 따르려면 이라는 프로세스를 만듭니다 `MyApplication/EncryptDocument` Workbench를 사용합니다. (참조: [Workbench 사용](https://www.adobe.com/go/learn_aemforms_workbench_63).)

>[!NOTE]
>
>DIME를 사용하여 AEM Forms 서비스 작업을 호출하는 것은 더 이상 사용되지 않습니다. MTOM을 사용하는 것이 좋습니다. (참조: [MTOM을 사용하여 AEM Forms 호출](#invoking-aem-forms-using-mtom).)

### DIME을 사용하는 .NET 프로젝트 만들기 {#creating-a-net-project-that-uses-dime}

DIME을 사용하여 Forms 서비스를 호출할 수 있는 .NET 프로젝트를 만들려면 다음 작업을 수행하십시오.

* 개발 컴퓨터에 웹 서비스 개선 사항 2.0을 설치합니다.
* .NET 프로젝트 내에서 FormsAEM Forms 서비스에 대한 웹 참조를 만듭니다.

**웹 서비스 개선 사항 2.0 설치**

개발 컴퓨터에 웹 서비스 개선 사항 2.0을 설치하고 Microsoft Visual Studio .NET과 통합합니다. 에서 웹 서비스 개선 사항 2.0을 다운로드할 수 있습니다. [Microsoft 다운로드 센터.](https://www.microsoft.com/downloads/search.aspx)

이 웹 페이지에서 웹 서비스 개선 사항 2.0을 검색하고 개발 컴퓨터에 다운로드합니다. 이 다운로드는 Microsoft WSE 2.0 SPI.msi라는 파일을 컴퓨터에 저장합니다. 설치 프로그램을 실행하고 온라인 지침을 따르십시오.

>[!NOTE]
>
>웹 서비스 개선 사항 2.0은 DIME를 지원합니다. Microsoft Visual Studio의 지원되는 버전은 2003입니다. 웹 서비스 개선 사항 2.0을 사용하여 작업하는 경우 이 버전입니다. 웹 서비스 개선 사항 3.0은 DIME를 지원하지 않지만 MTOM을 지원합니다.

**AEM Forms 서비스에 대한 웹 참조 만들기**

개발 컴퓨터에 Web Services Enhancements 2.0을 설치하고 Microsoft .NET 프로젝트를 만든 후 Forms 서비스에 대한 웹 참조를 만듭니다. 예를 들어 웹 참조를 만들려면 `MyApplication/EncryptDocument` Forms이 로컬 컴퓨터에 설치되어 있다고 가정하고 다음 URL을 지정하십시오.

```java
     http://localhost:8080/soap/services/MyApplication/EncryptDocument?WSDL
```

웹 참조를 만든 후에는 .NET 프로젝트 내에서 사용할 수 있는 프록시 데이터 형식은 다음과 같습니다. `EncryptDocumentService` 및 `EncryptDocumentServiceWse`. 를 호출하려면 `MyApplication/EncryptDocument` dime을 사용한 프로세스에서는 `EncryptDocumentServiceWse` 유형.

>[!NOTE]
>
>Forms 서비스에 대한 웹 참조를 만들려면 먼저 프로젝트에서 웹 서비스 개선 사항 2.0을 참조하십시오. (&quot;웹 서비스 개선 사항 2.0 설치&quot; 참조)

**WSE 라이브러리 참조**

1. 프로젝트 메뉴에서 참조 추가를 선택합니다.
1. 참조 추가 대화 상자에서 Microsoft.Web.Services2.dll을 선택합니다.
1. System.Web.Services.dll을 선택합니다.
1. 선택 을 클릭한 다음 확인 을 클릭합니다.

**Forms 서비스에 대한 웹 참조 만들기**

1. 프로젝트 메뉴에서 웹 참조 추가를 선택합니다.
1. URL 대화 상자에서 Forms 서비스의 URL을 지정합니다.
1. 실행을 클릭한 다음 참조 추가를 클릭합니다.

>[!NOTE]
>
>.NET 프로젝트에서 WSE 라이브러리를 사용하도록 설정해야 합니다. 프로젝트 탐색기에서 프로젝트 이름을 마우스 오른쪽 단추로 클릭하고 WSE 2.0 사용을 선택합니다. 표시되는 대화 상자의 확인란이 선택되어 있는지 확인합니다.

**.NET 프로젝트에서 DIME를 사용하여 서비스 호출**

DIME를 사용하여 Forms 서비스를 호출할 수 있습니다. 다음을 고려하십시오. `MyApplication/EncryptDocument` 비보안 PDF 문서를 수락하고 암호로 암호화된 PDF 문서를 반환하는 프로세스입니다. 를 호출하려면 `MyApplication/EncryptDocument` dime을 사용하여 프로세스를 수행하려면 다음 단계를 수행하십시오.

1. DIME를 사용하여 Forms 서비스를 호출할 수 있는 Microsoft .NET 프로젝트를 만듭니다. 웹 서비스 개선 사항 2.0을 포함하고 AEM Forms 서비스에 대한 웹 참조를 만들어야 합니다.
1. 웹 참조를 로 설정한 후 `MyApplication/EncryptDocument` 프로세스, 만들기 `EncryptDocumentServiceWse` 기본 생성자를 사용하여 개체를 작성합니다.
1. 설정 `EncryptDocumentServiceWse` 개체 `Credentials` 이(가) 있는 데이터 멤버 `System.Net.NetworkCredential` AEM forms 사용자 이름 및 암호 값을 지정하는 값입니다.
1. 만들기 `Microsoft.Web.Services2.Dime.DimeAttachment` 개체, 개체, 개체, 개체 또는 개체의 생성자를 사용하고 다음 값을

   * GUID 값을 지정하는 문자열 값입니다. GUID 값을 가져오려면 `System.Guid.NewGuid.ToString` 메서드를 사용합니다.
   * 콘텐츠 유형을 지정하는 문자열 값입니다. 이 프로세스에는 PDF 문서가 필요하므로 `application/pdf`.
   * A `TypeFormat` 열거형 값입니다. 지정 `TypeFormat.MediaType`.
   * AEM Forms 프로세스에 전달할 PDF 문서의 위치를 지정하는 문자열 값입니다.

1. 만들기 `BLOB` 개체를 만들 때 사용됩니다.
1. DIME 첨부 파일을 `BLOB` 을(를) 할당하여 개체 `Microsoft.Web.Services2.Dime.DimeAttachment` 개체 `Id` 데이터 멤버 값 `BLOB` 개체 `attachmentID` 데이터 구성원입니다.
1. 호출 `EncryptDocumentServiceWse.RequestSoapContext.Attachments.Add` 메서드 및 전달 `Microsoft.Web.Services2.Dime.DimeAttachment` 개체.
1. 호출 `MyApplication/EncryptDocument` 를 호출하여 프로세스를 `EncryptDocumentServiceWse` 개체 `invoke` 메서드 및 전달 `BLOB` DIME 첨부 파일이 포함된 개체입니다. 이 프로세스는 내의 암호화된 PDF 문서를 반환합니다. `BLOB` 개체.
1. 반환된 값을 가져와 첨부 파일 식별자 값 가져오기 `BLOB` 개체 `attachmentID` 데이터 구성원입니다.
1. 의 첨부 파일 반복 `EncryptDocumentServiceWse.ResponseSoapContext.Attachments` 첨부 파일 식별자 값을 사용하여 암호화된 PDF 문서를 가져옵니다.
1. 획득 `System.IO.Stream` 의 값을 가져와서 개체 `Attachment` 개체 `Stream` 데이터 구성원입니다.
1. 바이트 배열을 만들고 해당 바이트 배열을 `System.IO.Stream` 개체 `Read` 메서드를 사용합니다. 이 메서드는 암호화된 PDF 문서를 나타내는 데이터 스트림으로 바이트 배열을 채웁니다.
1. 만들기 `System.IO.FileStream` 개체를 호출하고 PDF 파일 위치를 나타내는 문자열 값을 전달합니다. 이 개체는 암호화된 PDF 문서를 나타냅니다.
1. 만들기 `System.IO.BinaryWriter` 개체를 호출하고 `System.IO.FileStream` 개체.
1. 를 호출하여 바이트 배열의 내용을 PDF 파일에 씁니다 `System.IO.BinaryWriter` 개체 `Write` 메서드 및 바이트 배열 전달.

### DIME를 사용하는 Apache Axis Java 프록시 클래스 생성 {#creating-apache-axis-java-proxy-classes-that-use-dime}

Apache Axis WSDL2Java 도구를 사용하여 서비스 WSDL을 Java 프록시 클래스로 변환하여 서비스 작업을 호출할 수 있습니다. Apache Ant를 사용하면 AEM Forms 서비스 WSDL에서 서비스를 호출할 수 있는 Axis 라이브러리 파일을 생성할 수 있습니다. (참조: [Apache Axis를 사용하여 Java 프록시 클래스 생성](#creating-java-proxy-classes-using-apache-axis).)

Apache Axis WSDL2Java 도구는 SOAP 요청을 서비스로 전송하는 데 사용되는 메서드가 포함된 JAVA 파일을 생성합니다. 서비스에서 받은 SOAP 요청은 Axis 생성 라이브러리에 의해 디코딩되고 메서드 및 인수로 다시 변환됩니다.

를 호출하려면 `MyApplication/EncryptDocument` 축 생성 라이브러리 파일과 DIME를 사용하여 Workbench에서 빌드된 서비스를 사용하려면 다음 단계를 수행하십시오.

1. 다음을 사용하는 Java 프록시 클래스 만들기 `MyApplication/EncryptDocument` apache Axis를 사용하여 WSDL을 서비스합니다. (참조: [Apache Axis를 사용하여 Java 프록시 클래스 생성](#creating-java-proxy-classes-using-apache-axis).)
1. 클래스 경로에 Java 프록시 클래스를 포함합니다.
1. 만들기 `MyApplicationEncryptDocumentServiceLocator` 개체를 만들 때 사용됩니다.
1. 만들기 `URL` 개체. 생성자를 사용하고 AEM Forms 서비스 WSDL 정의를 지정하는 문자열 값을 전달합니다. 다음을 지정해야 합니다. `?blob=dime` SOAP 끝점 URL의 끝에 있습니다. 예를 들어,

   ```java
    https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?blob=dime.
   ```

1. 만들기 `EncryptDocumentSoapBindingStub` 개체를 호출하고 `MyApplicationEncryptDocumentServiceLocator`오브젝트 및 `URL` 개체.
1. 다음을 호출하여 AEM Forms 사용자 이름 및 암호 값 설정 `EncryptDocumentSoapBindingStub` 개체 `setUsername` 및 `setPassword` 메서드를 사용합니다.

   ```java
    encryptionClientStub.setUsername("administrator");
    encryptionClientStub.setPassword("password");
   ```

1. 에 보낼 PDF 문서 검색 `MyApplication/EncryptDocument` 를 만들어 서비스 제공 `java.io.File` 개체. PDF 문서 위치를 지정하는 문자열 값을 전달합니다.
1. 만들기 `javax.activation.DataHandler` 개체를 생성자를 사용하고 `javax.activation.FileDataSource` 개체. 다음 `javax.activation.FileDataSource` 개체를 만들려면 생성자를 사용하고 `java.io.File` PDF 문서를 나타내는 개체입니다.
1. 만들기 `org.apache.axis.attachments.AttachmentPart` 개체를 생성자를 사용하고 `javax.activation.DataHandler` 개체.
1. 다음을 호출하여 첨부 파일 첨부 `EncryptDocumentSoapBindingStub` 개체 `addAttachment` 메서드 및 전달 `org.apache.axis.attachments.AttachmentPart` 개체.
1. 만들기 `BLOB` 개체를 만들 때 사용됩니다. 채우기 `BLOB` 를 호출하여 첨부 파일 식별자 값이 있는 개체 `BLOB` 개체 `setAttachmentID` 첨부 파일 식별자 값 전달 방법. 이 값은 다음을 호출하여 얻을 수 있습니다. `org.apache.axis.attachments.AttachmentPart` 개체 `getContentId` 메서드를 사용합니다.
1. 호출 `MyApplication/EncryptDocument` 를 호출하여 프로세스를 `EncryptDocumentSoapBindingStub` 개체 `invoke` 메서드를 사용합니다. 전달 `BLOB` DIME 첨부 파일이 포함된 개체입니다. 이 프로세스는 내의 암호화된 PDF 문서를 반환합니다. `BLOB` 개체.
1. 반환된 을 호출하여 첨부 파일 식별자 값 가져오기 `BLOB` 개체 `getAttachmentID` 메서드를 사용합니다. 이 메서드는 반환된 첨부 파일의 식별자 값을 나타내는 문자열 값을 반환합니다.
1. 다음을 호출하여 첨부 파일 가져오기 `EncryptDocumentSoapBindingStub` 개체 `getAttachments` 메서드를 사용합니다. 이 메서드는 배열의 `Objects` 첨부 파일을 나타냅니다.
1. 첨부 파일 반복( `Object` array)를 참조하고 첨부 파일 식별자 값을 사용하여 암호화된 PDF 문서를 가져옵니다. 각 요소는 `org.apache.axis.attachments.AttachmentPart` 개체.
1. 다음을 획득 `javax.activation.DataHandler` 를 호출하여 첨부 파일과 연결된 개체 `org.apache.axis.attachments.AttachmentPart` 개체 `getDataHandler` 메서드를 사용합니다.
1. 획득 `java.io.FileStream` 를 호출하여 개체 `javax.activation.DataHandler` 개체 `getInputStream` 메서드를 사용합니다.
1. 바이트 배열을 만들고 해당 바이트 배열을 `java.io.FileStream` 개체 `read` 메서드를 사용합니다. 이 메서드는 암호화된 PDF 문서를 나타내는 데이터 스트림으로 바이트 배열을 채웁니다.
1. 만들기 `java.io.File` 개체를 만들 때 사용됩니다. 이 개체는 암호화된 PDF 문서를 나타냅니다.
1. 만들기 `java.io.FileOutputStream` 개체를 생성자를 사용하고 `java.io.File` 개체.
1. 호출 `java.io.FileOutputStream` 개체 `write` 암호화된 PDF 문서를 나타내는 데이터 스트림이 포함된 바이트 배열을 전달합니다.

**추가 참조**

[빠른 시작: Java 프로젝트에서 DIME를 사용하여 서비스 호출](/help/forms/developing/invocation-api-quick-starts.md#quick-start-invoking-a-service-using-dime-in-a-java-project)

## SAML 기반 인증 사용 {#using-saml-based-authentication}

AEM Forms은 서비스를 호출할 때 다양한 웹 서비스 인증 모드를 지원합니다. 한 인증 모드는 웹 서비스 호출에서 기본 인증 헤더를 사용하여 사용자 이름과 암호 값을 모두 지정하는 것입니다. AEM Forms은 SAML 어설션 기반 인증도 지원합니다. 클라이언트 애플리케이션이 웹 서비스를 사용하여 AEM Forms 서비스를 호출하는 경우 클라이언트 애플리케이션은 다음 방법 중 하나로 인증 정보를 제공할 수 있습니다.

* 기본 인증의 일부로 자격 증명 전달
* WS-Security 헤더의 일부로 사용자 이름 토큰 전달
* WS-Security 헤더의 일부로 SAML 어설션 전달
* WS-Security 헤더의 일부로 Kerberos 토큰 전달

AEM Forms은 표준 인증서 기반 인증을 지원하지 않지만 다른 양식의 인증서 기반 인증을 지원합니다.

>[!NOTE]
>
>AEM Forms을 사용한 프로그래밍 의 웹 서비스 빠른 시작은 인증을 수행할 사용자 이름과 암호 값을 지정합니다.

AEM Forms 사용자의 ID는 비밀 키를 사용하여 서명된 SAML 어설션을 통해 나타낼 수 있습니다. 다음 XML 코드에서는 SAML 어설션의 예를 보여 줍니다.

```xml
 <Assertion xmlns="urn:oasis:names:tc:SAML:1.0:assertion"
     xmlns:saml="urn:oasis:names:tc:SAML:1.0:assertion"
     xmlns:samlp="urn:oasis:names:tc:SAML:1.0:protocol"
     AssertionID="fd4bd0c87302780e0d9bbfa8726d5bc0" IssueInstant="2008-04-17T13:47:00.720Z" Issuer="LiveCycle"
     MajorVersion="1" MinorVersion="1">
     <Conditions NotBefore="2008-04-17T13:47:00.720Z" NotOnOrAfter="2008-04-17T15:47:00.720Z">
     </Conditions>
     <AuthenticationStatement
         AuthenticationInstant="2008-04-17T13:47:00.720Z"
         AuthenticationMethod="urn:oasis:names:tc:SAML:1.0:am:unspecified">
         <Subject>
             <NameIdentifier NameQualifier="DefaultDom">administrator</NameIdentifier>
             <SubjectConfirmation>
                 <ConfirmationMethod>urn:oasis:names:tc:SAML:1.0:cm:sender-vouches</ConfirmationMethod>
             </SubjectConfirmation>
         </Subject>
     </AuthenticationStatement>
     <ds:Signature >
         <ds:SignedInfo>
             <ds:CanonicalizationMethod Algorithm="https://www.w3.org/2001/10/xml-exc-c14n#"></ds:CanonicalizationMethod>
             <ds:SignatureMethod    Algorithm="https://www.w3.org/2000/09/xmldsig#hmac-sha1"></ds:SignatureMethod>
             <ds:Reference URI="#fd4bd0c87302780e0d9bbfa8726d5bc0">
                 <ds:Transforms>
                     <ds:Transform Algorithm="https://www.w3.org/2000/09/xmldsig#enveloped-signature"></ds:Transform>
                     <ds:Transform Algorithm="https://www.w3.org/2001/10/xml-exc-c14n#">
                         <ec:InclusiveNamespaces
                             PrefixList="code ds kind rw saml samlp typens #default">
                         </ec:InclusiveNamespaces>
                     </ds:Transform>
                 </ds:Transforms>
                 <ds:DigestMethod Algorithm="https://www.w3.org/2000/09/xmldsig#sha1"></ds:DigestMethod>
                 <ds:DigestValue>hVrtqjWr+VzaVUIpQx0YI9lIjaY=</ds:DigestValue>
             </ds:Reference>
         </ds:SignedInfo>
         <ds:SignatureValue>UMbBb+cUcPtcWDCIhXes4n4FxfU=</ds:SignatureValue>
     </ds:Signature>
 </Assertion>
```

이 예제 어설션은 관리자 사용자에 대해 발행됩니다. 이 어설션에는 다음과 같은 주목할 만한 항목이 포함되어 있습니다.

* 특정 기간 동안 유효합니다.
* 특정 사용자에 대해 발급됩니다.
* 디지털 서명되어 있습니다. 따라서 수정하면 서명이 손상될 수 있습니다.
* 사용자 이름 및 암호와 유사한 사용자 ID의 토큰으로 AEM Forms에 표시될 수 있습니다.

클라이언트 애플리케이션은 다음을 반환하는 모든 AEM Forms AuthenticationManager API에서 어설션을 검색할 수 있습니다. `AuthResult` 개체. 다음을 얻을 수 있습니다. `AuthResult` 다음 두 가지 방법 중 하나를 수행하여 인스턴스:

* AuthenticationManager API에 의해 노출된 인증 방법을 사용하여 사용자 인증. 일반적으로 사용자 이름과 암호를 사용합니다. 하지만 인증서 인증을 사용할 수도 있습니다.
* 사용 `AuthenticationManager.getAuthResultOnBehalfOfUser` 메서드를 사용합니다. 이 메서드를 사용하면 클라이언트 애플리케이션에서 `AuthResult` 모든 AEM forms 사용자에 대한 개체입니다.

가져온 SAML 토큰을 사용하여 AEM Forms 사용자를 인증할 수 있습니다. 이 SAML 어설션(xml 조각)은 사용자 인증을 위한 웹 서비스 호출과 함께 WS-Security 헤더의 일부로 보낼 수 있습니다. 일반적으로 클라이언트 애플리케이션은 사용자를 인증했지만 사용자 자격 증명을 저장하지 않았습니다. (또는 사용자가 사용자 이름과 암호를 사용하지 않는 메커니즘을 통해 해당 클라이언트에 로그온했습니다.) 이 경우 클라이언트 애플리케이션은 AEM Forms을 호출하고 AEM Forms 호출이 허용되는 특정 사용자를 가장해야 합니다.

특정 사용자를 가장하려면 `AuthenticationManager.getAuthResultOnBehalfOfUser` 웹 서비스를 사용하는 방법입니다. 이 메서드는 `AuthResult` 해당 사용자에 대한 SAML 어설션이 포함된 인스턴스입니다.

그런 다음 해당 SAML 어설션을 사용하여 인증이 필요한 서비스를 호출합니다. 이 작업에는 어설션을 SOAP 헤더의 일부로 보내는 작업이 포함됩니다. 이 어설션으로 웹 서비스 호출이 수행되면 AEM Forms은 사용자를 해당 어설션에 표시된 사용자로 식별합니다. 즉, 어설션에 지정된 사용자가 서비스를 호출하는 사용자입니다.

### Apache Axis 클래스 및 SAML 기반 인증 사용 {#using-apache-axis-classes-and-saml-based-authentication}

Axis 라이브러리를 사용하여 만든 Java 프록시 클래스별로 AEM Forms 서비스를 호출할 수 있습니다. (참조: [Apache Axis를 사용하여 Java 프록시 클래스 생성](#creating-java-proxy-classes-using-apache-axis).)

SAML 기반 인증을 사용하는 AXIS를 사용하는 경우 Axis에 요청 및 응답 핸들러를 등록합니다. Apache Axis는 호출 요청을 AEM Forms에 보내기 전에 핸들러를 호출합니다. 처리기를 등록하려면 확장하는 Java 클래스를 만듭니다 `org.apache.axis.handlers.BasicHandler`.

**축을 사용하여 AssertionHandler 만들기**

다음 Java 클래스 `AssertionHandler.java`는 를 확장하는 Java 클래스의 예를 보여 줍니다 `org.apache.axis.handlers.BasicHandler`.

```java
 public class AssertionHandler extends BasicHandler {
        public void invoke(MessageContext ctx) throws AxisFault {
            String assertion = (String) ctx.getProperty(LC_ASSERTION);
 
            //no assertion hence nothing to insert
            if(assertion == null) return;
 
            try {
                MessageElement samlElement = new MessageElement(convertToXML(assertion));
                SOAPHeader header = (SOAPHeader) ctx.getRequestMessage().getSOAPHeader();
                //Create the wsse:Security element which would contain the SAML element
                SOAPElement wsseHeader = header.addChildElement("Security", "wsse", WSSE_NS);
                wsseHeader.appendChild(samlElement);
                //remove the actor attribute as in LC we do not specify any actor. This would not remove the actor attribute though
                //it would only remove it from the soapenv namespace
                wsseHeader.getAttributes().removeNamedItem("actor");
            } catch (SOAPException e) {
                throw new AxisFault("Error occured while adding the assertion to the SOAP Header",e);
            }
        }
 }
```

**핸들러 등록**

Axis에 핸들러를 등록하려면 client-config.wsdd 파일을 만듭니다. 기본적으로 Axis는 이 이름의 파일을 찾습니다. 다음 XML 코드는 client-config.wsdd 파일의 예입니다. 자세한 내용은 Axis 설명서 를 참조하십시오.

```xml
 <deployment xmlns="https://xml.apache.org/axis/wsdd/" xmlns:java="https://xml.apache.org/axis/wsdd/providers/java">
     <transport name="http" pivot="java:org.apache.axis.transport.http.HTTPSender"/>
      <globalConfiguration >
       <requestFlow >
        <handler type="java:com.adobe.idp.um.example.AssertionHandler" />
       </requestFlow >
      </globalConfiguration >
 </deployment>
 
```

**AEM Forms 서비스 호출**

다음 코드 예제에서는 SAML 기반 인증을 사용하여 AEM Forms 서비스를 호출합니다.

```java
 public class ImpersonationExample {
        . . .
        public void  authenticateOnBehalf(String superUsername,String password,
                String canonicalName,String domainName) throws UMException, RemoteException{
            ((org.apache.axis.client.Stub) authenticationManager).setUsername(superUsername);
            ((org.apache.axis.client.Stub) authenticationManager).setPassword(password);
 
            //Step 1 - Invoke the Auth manager api to get an assertion for the user to be impersonated
            AuthResult ar = authenticationManager.getAuthResultOnBehalfOfUser(canonicalName, domainName, null);
            String assertion = ar.getAssertion();
            //Step 2 - Setting the assertion here to be picked later by the AssertionHandler. Note that stubs are not threadSafe
            //hence should not be reused. For this simple example we have made them instance variable but care should be taken
            //regarding the thread safety
            ((javax.xml.rpc.Stub) authorizationManager)._setProperty(AssertionHandler.LC_ASSERTION, assertion);
        }
 
        public Role findRole(String roleId) throws UMException, RemoteException{
            //This api would be invoked under bob's user rights
            return authorizationManager.findRole(roleId);
        }
 
        public static void main(String[] args) throws Exception {
            ImpersonationExample ie = new ImpersonationExample("http://localhost:5555");
            //Get the SAML assertion for the user to impersonate and store it in stub
            ie.authenticateOnBehalf(
                    "administrator", //The Super user which has the required impersonation permission
                    "password", // Password of the super user as referred above
                    "bob", //Cannonical name of the user to impersonate
                    "testdomain" //Domain of the user to impersonate
                    );
 
            Role r = ie.findRole("BASIC_ROLE_ADMINISTRATOR");
            System.out.println("Role "+r.getName());
        }
 }
```

### .NET 클라이언트 어셈블리 및 SAML 기반 인증 사용 {#using-a-net-client-assembly-and-saml-based-authentication}

.NET 클라이언트 어셈블리 및 SAML 기반 인증을 사용하여 Forms 서비스를 호출할 수 있습니다. 이렇게 하려면 WSE(Web Service Enhancements 3.0)를 사용해야 합니다. WSE를 사용하는 .NET 클라이언트 어셈블리를 만드는 방법에 대한 자세한 내용은 [DIME을 사용하는 .NET 프로젝트 만들기](#creating-a-net-project-that-uses-dime).

>[!NOTE]
>
>DIME 섹션은 WSE 2.0을 사용합니다. SAML 기반 인증을 사용하려면 DIME 항목에 지정된 것과 동일한 지침을 따르십시오. 그러나 WSE 2.0을 WSE 3.0으로 바꿉니다. 개발 컴퓨터에 웹 서비스 개선 사항 3.0을 설치하고 Microsoft Visual Studio .NET과 통합합니다. 에서 웹 서비스 개선 사항 3.0을 다운로드할 수 있습니다. [Microsoft 다운로드 센터](https://www.microsoft.com/downloads/search.aspx).

WSE 아키텍처는 정책, 어설션 및 보안 토큰 데이터 유형을 사용합니다. 간단히 웹 서비스 호출의 경우 정책을 지정합니다. 정책에는 여러 개의 어설션이 있을 수 있습니다. 각 어설션은 필터를 포함할 수 있습니다. 필터는 웹 서비스 호출의 특정 단계에서 호출되며, 해당 단계에서 SOAP 요청을 수정할 수 있습니다. 자세한 내용은 웹 서비스 개선 사항 3.0 설명서를 참조하십시오.

**어설션 및 필터 생성**

다음 C# 코드 예제에서는 필터 및 어설션 클래스를 만듭니다. 이 코드 예제에서는 SamlAssertionOutputFilter를 만듭니다. 이 필터는 SOAP 요청이 AEM Forms으로 전송되기 전에 WSE 프레임워크에 의해 호출됩니다.

```java
 class LCSamlPolicyAssertion : Microsoft.Web.ServicES4.Design.PolicyAssertion
 {
        public override Microsoft.Web.ServicES4.SoapFilter CreateClientOutputFilter(FilterCreationContext context)
        {
           return new SamlAssertionOutputFilter();
        }
        . . .
 }
 
 
 class SamlAssertionOutputFilter : SendSecurityFilter
 {
        public override void SecureMessage(SoapEnvelope envelope, Security security)
        {
           // Get the SamlToken from the SessionState
           SamlToken samlToken = envelope.Context.Credentials.UltimateReceiver.GetClientToken<SamlToken>();
           security.Tokens.Add(samlToken);
        }
 }
```

**SAML 토큰 만들기**

SAML 어설션을 나타내는 클래스를 생성합니다. 이 클래스에서 수행하는 주요 작업은 데이터 값을 문자열에서 xml로 변환하고 공백을 유지하는 것입니다. 이 어설션 xml은 나중에 SOAP 요청으로 가져옵니다.

```java
 class SamlToken : SecurityToken
 {
        public const string SAMLAssertion = "https://docs.oasis-open.org/wss/oasis-wss-saml-token-profile-1.1#SAMLV1.1";
        private XmlElement _assertionElement;
 
        public SamlToken(string assertion)
             : base(SAMLAssertion)
        {
           XmlDocument xmlDoc = new XmlDocument();
           //The white space has to be preserved else the digital signature would get broken
           xmlDoc.PreserveWhitespace = true;
           xmlDoc.LoadXml(assertion);
           _assertionElement = xmlDoc.DocumentElement;
         }
 
         public override XmlElement GetXml(XmlDocument document)
         {
            return (XmlElement)document.ImportNode(_assertionElement, true);
         }
        . . .
 }
```

**AEM Forms 서비스 호출**

다음 C# 코드 예제에서는 SAML 기반 인증을 사용하여 Forms 서비스를 호출합니다.

```java
 public class ImpersonationExample
 {
        . . .
        public void AuthenticateOnBehalf(string superUsername, string password, string canonicalName, string domainName)
        {
            //Create a policy for UsernamePassword Token
            Policy usernamePasswordPolicy = new Policy();
            usernamePasswordPolicy.Assertions.Add(new UsernameOverTransportAssertion());
 
            UsernameToken token = new UsernameToken(superUsername, password, PasswordOption.SendPlainText);
            authenticationManager.SetClientCredential(token);
            authenticationManager.SetPolicy(usernamePasswordPolicy);
 
            //Get the SAML assertion for impersonated user
            AuthClient.AuthenticationManagerService.AuthResult ar
                = authenticationManager.getAuthResultOnBehalfOfUser(canonicalName, domainName, null);
            System.Console.WriteLine("Received assertion " + ar.assertion);
 
            //Create a policy for inserting SAML assertion
            Policy samlPolicy = new Policy();
            samlPolicy.Assertions.Add(new LCSamlPolicyAssertion());
            authorizationManager.SetPolicy(samlPolicy);
            //Set the SAML assertion obtained previously as the token
            authorizationManager.SetClientCredential(new SamlToken(ar.assertion));
        }
 
        public Role findRole(string roleId)
        {
            return authorizationManager.findRole(roleId);
        }
 
        static void Main(string[] args)
        {
            ImpersonationExample ie = new ImpersonationExample("http://localhost:5555");
            ie.AuthenticateOnBehalf(
                 "administrator", //The Super user which has the required impersonation permission
                 "password", // Password of the super user as referred above
                 "bob", //Cannonical name of the user to impersonate
                 "testdomain" //Domain of the user to impersonate
                 );
 
         Role r = ie.findRole("BASIC_ROLE_ADMINISTRATOR");
            System.Console.WriteLine("Role "+r.name);
     }
 }
```

## 웹 서비스 사용 시 관련 고려 사항 {#related-considerations-when-using-web-services}

웹 서비스를 사용하여 특정 AEM Forms 서비스 작업을 호출할 때 문제가 발생하는 경우가 있습니다. 이 논의의 목적은 이러한 문제를 식별하고 가능한 경우 해결책을 제공하는 것입니다.

### 비동기적으로 서비스 작업 호출 {#invoking-service-operations-asynchronously}

PDF 생성과 같은 AEM Forms 서비스 작업을 비동기적으로 호출하려고 하는 경우 `htmlToPDF` 작업, a `SoapFaultException` 발생합니다. 이 문제를 해결하려면 다음을 매핑하는 사용자 지정 바인딩 XML 파일을 만듭니다 `ExportPDF_Result` 요소 및 기타 요소를 다른 클래스에 추가합니다. 다음 XML은 사용자 지정 바인딩 파일을 나타냅니다.

```xml
 <bindings
        xmlns:xsd="https://www.w3.org/2001/XMLSchema"
        xmlns:jxb="https://java.sun.com/xml/ns/jaxb" jxb:version="1.0"
        xmlns:wsdl="https://schemas.xmlsoap.org/wsdl/"
      wsdlLocation="http://localhost:8080/soap/services/GeneratePDFService?wsdl&async=true&lc_version=9.0.0"
        xmlns="https://java.sun.com/xml/ns/jaxws">
        <enableAsyncMapping>false</enableAsyncMapping>
        <package name="external_customize.client"/>
        <enableWrapperStyle>true</enableWrapperStyle>
        <bindings node="/wsdl:definitions/wsdl:types/xsd:schema[@targetNamespace='https://adobe.com/idp/services']/xsd:element[@name='ExportPDF_Result']">
            <jxb:class name="ExportPDFAsyncResult">
            </jxb:class>
        </bindings>
        <bindings node="/wsdl:definitions/wsdl:types/xsd:schema[@targetNamespace='https://adobe.com/idp/services']/xsd:element[@name='CreatePDF_Result']">
            <jxb:class name="CreatePDFAsyncResult">
            </jxb:class>
        </bindings>
        <bindings node="/wsdl:definitions/wsdl:types/xsd:schema[@targetNamespace='https://adobe.com/idp/services']/xsd:element[@name='HtmlToPDF_Result']">
            <jxb:class name="HtmlToPDFAsyncResult">
            </jxb:class>
        </bindings>
        <bindings node="/wsdl:definitions/wsdl:types/xsd:schema[@targetNamespace='https://adobe.com/idp/services']/xsd:element[@name='OptimizePDF_Result']">
            <jxb:class name="OptimizePDFAsyncResult">
            </jxb:class>
        </bindings>
        <!--bindings node="//wsdl:portType[@name='GeneratePDFService']/wsdl:operation[@name='HtmlToPDF_Result']">
            <jxb:class name="HtmlToPDFAsyncResult"/>
        </bindings-->
 </bindings>
```

JAX-WS를 사용하여 Java 프록시 파일을 생성할 때 이 XML 파일을 사용하십시오. (참조: [JAX-WS를 사용하여 Java 프록시 클래스 생성](#creating-java-proxy-classes-using-jax-ws).)

JAX-WS 도구(wsimport.exe)를 실행할 때 -를 사용하여 이 XML 파일을 참조합니다. `b` 명령줄 옵션입니다. 업데이트 `wsdlLocation` AEM Forms의 URL을 지정하는 바인딩 XML 파일의 요소입니다.

비동기 호출이 작동하도록 하려면 끝점 URL 값을 수정하고 을 지정합니다 `async=true`. 예를 들어 JAX-WS로 만든 Java 프록시 파일의 경우 다음에 대해 다음을 지정합니다. `BindingProvider.ENDPOINT_ADDRESS_PROPERTY`.

`https://server:port/soap/services/ServiceName?wsdl&async=true&lc_version=9.0.0`

다음 목록은 비동기적으로 호출될 때 사용자 지정 바인딩 파일이 필요한 다른 서비스를 지정합니다.

* PDFG3D
* 작업 관리자
* Application Manager
* 디렉터리 관리자
* Distiller
* Rights Management
* 문서 관리

### J2EE 애플리케이션 서버의 차이점 {#differences-in-j2ee-application-servers}

특정 J2EE 응용 프로그램 서버를 사용하여 만든 프록시 라이브러리가 다른 J2EE 응용 프로그램 서버에서 호스팅된 AEM Forms을 성공적으로 호출하지 못하는 경우가 있습니다. WebSphere에 배포된 AEM Forms을 사용하여 생성된 프록시 라이브러리를 고려합니다. 이 프록시 라이브러리는 JBoss Application Server에 배포된 AEM Forms 서비스를 호출할 수 없습니다.

다음과 같은 일부 AEM Forms 복합 데이터 유형 `PrincipalReference`는 AEM Forms이 WebSphere에 배포될 때 JBoss 애플리케이션 서버와 비교하여 다르게 정의됩니다. 다른 J2EE 응용 프로그램 서비스에서 사용하는 JDK의 차이점이 WSDL 정의에 차이가 있는 이유입니다. 따라서 동일한 J2EE 애플리케이션 서버에서 생성된 프록시 라이브러리를 사용합니다.

### 웹 서비스를 사용하여 여러 서비스에 액세스 {#accessing-multiple-services-using-web-services}

네임스페이스 충돌로 인해 데이터 개체를 여러 서비스 WSDL 간에 공유할 수 없습니다. 서로 다른 서비스는 데이터 형식을 공유할 수 있으므로 서비스는 WSDL에서 이러한 형식의 정의를 공유합니다. 예를들어, `BLOB` 데이터 형식을 동일한 .NET 클라이언트 프로젝트에 추가합니다. 그렇게 하려고 하면 컴파일 오류가 발생합니다.

다음 목록은 여러 서비스 WSDL 간에 공유할 수 없는 데이터 형식을 지정합니다.

* `User`
* `Principals`
* `PrincipalReference`
* `Groups`
* `Roles`
* `BLOB`

이 문제를 방지하려면 데이터 형식을 완전히 정규화하는 것이 좋습니다. 예를 들어 서비스 참조를 사용하여 Forms 서비스와 서명 서비스를 모두 참조하는 .NET 응용 프로그램을 생각해 보십시오. 두 서비스 참조에 모두 `BLOB` 클래스. 을(를) 사용하려면 `BLOB` 인스턴스, 의 자격을 완전히 갖춤 `BLOB` 개체를 선언할 때 개체가 반환됩니다. 이 접근 방식은 다음 코드 예제와 같습니다. 이 코드 예제에 대한 자세한 내용은 [대화형 Forms 디지털 서명](/help/forms/developing/digitally-signing-certifying-documents.md#digitally-signing-interactive-forms).

다음 C# 코드 예제는 Forms 서비스에서 렌더링하는 대화형 양식에 서명합니다. 클라이언트 응용 프로그램에는 두 개의 서비스 참조가 있습니다. 다음 `BLOB` Forms 서비스와 연결된 인스턴스는 `SignInteractiveForm.ServiceReference2` 네임스페이스입니다. 마찬가지로 `BLOB` 서명 서비스와 연결된 인스턴스는 `SignInteractiveForm.ServiceReference1` 네임스페이스입니다. 서명된 대화형 양식은 이름이 인 PDF 파일로 저장됩니다. *LoanXFASigned.pdf*.

```csharp
 ???/**
     * Ensure that you create a .NET project that uses
     * MS Visual Studio 2008 and version 3.5 of the .NET
     * framework. This is required to invoke a
     * AEM Forms service using MTOM.
     *
     * For information, see "Invoking AEM Forms using MTOM" in Programming with AEM forms
     */
 using System;
 using System.Collections.Generic;
 using System.Linq;
 using System.Text;
 using System.ServiceModel;
 using System.IO;
 
 //A reference to the Signature service
 using SignInteractiveForm.ServiceReference1;
 
 //A reference to the Forms service
 using SignInteractiveForm.ServiceReference2;
 
 namespace SignInteractiveForm
 {
        class Program
        {
            static void Main(string[] args)
            {
                try
                {
                    //Because BLOB objects are used in both service references
                    //it is necessary to fully-qualify the BLOB objects
 
                    //Retrieve the form -- invoke the Forms service
                    SignInteractiveForm.ServiceReference2.BLOB formData = GetForm();
 
                    //Create a BLOB object associated with the Signature service
                    SignInteractiveForm.ServiceReference1.BLOB sigData = new SignInteractiveForm.ServiceReference1.BLOB();
 
                    //Transfer the byte stream from one Forms BLOB object to the
                    //Signature BLOB object
                    sigData.MTOM = formData.MTOM;
 
                    //Sign the Form -- invoke the Signature service
                    SignForm(sigData);
                }
                catch (Exception ee)
                {
                    Console.WriteLine(ee.Message);
                }
            }
 
            //Creates an interactive PDF form based on a XFA form - invoke the Forms service
            private static SignInteractiveForm.ServiceReference2.BLOB GetForm()
            {
 
                try
                {
                    //Create a FormsServiceClient object
                    FormsServiceClient formsClient = new FormsServiceClient();
                    formsClient.Endpoint.Address = new System.ServiceModel.EndpointAddress("https://hiro-xp:8080/soap/services/FormsService?blob=mtom");
 
                    //Enable BASIC HTTP authentication
                    BasicHttpBinding b = (BasicHttpBinding)formsClient.Endpoint.Binding;
                    b.MessageEncoding = WSMessageEncoding.Mtom;
                    formsClient.ClientCredentials.UserName.UserName = "administrator";
                    formsClient.ClientCredentials.UserName.Password = "password";
                    b.Security.Transport.ClientCredentialType = HttpClientCredentialType.Basic;
                    b.Security.Mode = BasicHttpSecurityMode.TransportCredentialOnly;
                    b.MaxReceivedMessageSize = 2000000;
                    b.MaxBufferSize = 2000000;
                    b.ReaderQuotas.MaxArrayLength = 2000000;
 
                    //Create a BLOB to store form data
                    SignInteractiveForm.ServiceReference2.BLOB formData = new SignInteractiveForm.ServiceReference2.BLOB();
                    SignInteractiveForm.ServiceReference2.BLOB pdfForm = new SignInteractiveForm.ServiceReference2.BLOB();
 
                    //Specify a XML form data
                    string path = "C:\\Adobe\Loan.xml";
                    FileStream fs = new FileStream(path, FileMode.Open);
 
                    //Get the length of the file stream
                    int len = (int)fs.Length;
                    byte[] ByteArray = new byte[len];
 
                    fs.Read(ByteArray, 0, len);
                    formData.MTOM = ByteArray;
 
                    //Specify a XML form data
                    string path2 = "C:\\Adobe\LoanSigXFA.pdf";
                    FileStream fs2 = new FileStream(path2, FileMode.Open);
 
                    //Get the length of the file stream
                    int len2 = (int)fs2.Length;
                    byte[] ByteArray2 = new byte[len2];
 
                    fs2.Read(ByteArray2, 0, len2);
                    pdfForm.MTOM = ByteArray2;
 
                    PDFFormRenderSpec renderSpec = new PDFFormRenderSpec();
                    renderSpec.generateServerAppearance = true;
 
                    //Set out parameter values
                    long pageCount = 1;
                    String localValue = "en_US";
                    FormsResult result = new FormsResult();
 
                    //Render an interactive PDF form
                    formsClient.renderPDFForm2(
                        pdfForm,
                        formData,
                        renderSpec,
                        null,
                        null,
                        out pageCount,
                        out localValue,
                        out result);
 
                    //Write the data stream to the BLOB object
                    SignInteractiveForm.ServiceReference2.BLOB outForm = result.outputContent;
                    return outForm;
                }
                catch (Exception ee)
                {
                    Console.WriteLine(ee.Message);
                }
                return null;
            }
 
            //Sign the form -- invoke the Signature service
            private static void SignForm(SignInteractiveForm.ServiceReference1.BLOB inDoc)
            {
 
                try
                {
                    //Create a SignatureServiceClient object
                    SignatureServiceClient signatureClient = new SignatureServiceClient();
                    signatureClient.Endpoint.Address = new System.ServiceModel.EndpointAddress("https://hiro-xp:8080/soap/services/SignatureService?blob=mtom");
 
                    //Enable BASIC HTTP authentication
                    BasicHttpBinding b = (BasicHttpBinding)signatureClient.Endpoint.Binding;
                    b.MessageEncoding = WSMessageEncoding.Mtom;
                    signatureClient.ClientCredentials.UserName.UserName = "administrator";
                    signatureClient.ClientCredentials.UserName.Password = "password";
                    b.Security.Transport.ClientCredentialType = HttpClientCredentialType.Basic;
                    b.Security.Mode = BasicHttpSecurityMode.TransportCredentialOnly;
                    b.MaxReceivedMessageSize = 2000000;
                    b.MaxBufferSize = 2000000;
                    b.ReaderQuotas.MaxArrayLength = 2000000;
 
                    //Specify the name of the signature field
                    string fieldName = "form1[0].grantApplication[0].page1[0].SignatureField1[0]";
 
                    //Create a Credential object
                    Credential myCred = new Credential();
                    myCred.alias = "secure";
 
                    //Specify the reason to sign the document
                    string reason = "The document was reviewed";
 
                    //Specify the location of the signer
                    string location = "New York HQ";
 
                    //Specify contact information
                    string contactInfo = "Tony Blue";
 
                    //Create a PDFSignatureAppearanceOptions object
                    //and show date information
                    PDFSignatureAppearanceOptionSpec appear = new PDFSignatureAppearanceOptionSpec();
                    appear.showDate = true;
 
                    //Sign the PDF document
                    SignInteractiveForm.ServiceReference1.BLOB signedDoc = signatureClient.sign(
                        inDoc,
                        fieldName,
                        myCred,
                        HashAlgorithm.SHA1,
                        reason,
                        location,
                        contactInfo,
                        appear,
                        true,
                        null,
                        null,
                        null);
 
                    //Populate a byte array with BLOB data that represents the signed form
                    byte[] outByteArray = signedDoc.MTOM;
 
                    //Save the signed PDF document
                    string fileName = "C:\\Adobe\LoanXFASigned.pdf";
                    FileStream fs2 = new FileStream(fileName, FileMode.OpenOrCreate);
 
                    //Create a BinaryWriter object
                    BinaryWriter w = new BinaryWriter(fs2);
                    w.Write(outByteArray);
                    w.Close();
                    fs2.Close();
                }
 
                catch (Exception ee)
                {
                    Console.WriteLine(ee.Message);
                }
            }
        }
 }
 
 
```

### 잘못된 프록시 파일을 생성할 때 문자로 시작하는 서비스 {#services-starting-with-the-letter-i-produce-invalid-proxy-files}

Microsoft .Net 3.5 및 WCF를 사용하는 경우 일부 AEM Forms 생성 프록시 클래스의 이름이 잘못되었습니다. 이 문제는 IBMFilenetContentRepositoryConnector, IDPSschedulerService 또는 이름이 문자 I로 시작하는 다른 서비스에 대해 프록시 클래스를 만들 때 발생합니다. 예를 들어 IBMFileNetContentRepositoryConnector의 경우 생성된 클라이언트의 이름은 입니다. `BMFileNetContentRepositoryConnectorClient`. 생성된 프록시 클래스에서 편지 I이 누락되었습니다.
