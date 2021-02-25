---
title: 웹 서비스를 사용하여 AEM Forms 호출
seo-title: 웹 서비스를 사용하여 AEM Forms 호출
description: WSDL 생성을 완벽하게 지원하는 웹 서비스를 사용하여 AEM Forms 프로세스를 호출합니다.
seo-description: WSDL 생성을 완벽하게 지원하는 웹 서비스를 사용하여 AEM Forms 프로세스를 호출합니다.
uuid: 66bcd010-c476-4b66-831d-a48307d8d67a
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: coding
discoiquuid: d5722281-bea9-4fc7-abdc-e678899e0a15
translation-type: tm+mt
source-git-commit: 9cf46a26d2aa2e41b924a4de89cf8ab5fdeeefc6
workflow-type: tm+mt
source-wordcount: '10004'
ht-degree: 0%

---


# 웹 서비스 {#invoking-aem-forms-using-web-services}를 사용하여 AEM Forms 호출

**이 문서의 샘플과 예는 JEE 환경의 AEM Forms에만 해당됩니다.**

서비스 컨테이너의 대부분의 AEM Forms 서비스는 WSDL(웹 서비스 정의 언어) 생성에 대한 완벽한 지원을 통해 웹 서비스를 제공하도록 구성됩니다. 즉, AEM Forms 서비스의 기본 SOAP 스택을 사용하는 프록시 개체를 만들 수 있습니다. 따라서 AEM Forms 서비스는 다음 SOAP 메시지를 교환하고 처리할 수 있습니다.

* **SOAP 요청**:작업을 요청하는 클라이언트 응용 프로그램에서 Forms 서비스로 전송됩니다.
* **SOAP 응답**:SOAP 요청이 처리된 후 Forms 서비스에서 클라이언트 응용 프로그램으로 전송됩니다.

웹 서비스를 사용하여 Java API를 사용하여 할 수 있는 동일한 AEM Forms 서비스 작업을 수행할 수 있습니다. 웹 서비스를 사용하여 AEM Forms 서비스를 호출할 때의 이점은 SOAP를 지원하는 개발 환경에서 클라이언트 애플리케이션을 만들 수 있다는 것입니다. 클라이언트 응용 프로그램은 특정 개발 환경 또는 프로그래밍 언어에 바인딩되지 않습니다. 예를 들어 Microsoft Visual Studio .NET 및 C#을 프로그래밍 언어로 사용하여 클라이언트 응용 프로그램을 만들 수 있습니다.

AEM Forms 서비스는 SOAP 프로토콜을 통해 노출되며 WSI Basic Profile 1.1 규격입니다. WSI(Web Services Interoperability)는 플랫폼 간 웹 서비스 상호 운용성을 높이는 개방형 표준 조직입니다. 자세한 내용은 [https://www.ws-i.org/](https://www.ws-i.org)을 참조하십시오.

AEM Forms은 다음과 같은 웹 서비스 표준을 지원합니다.

* **인코딩**:문서 및 리터럴 인코딩만 지원합니다(WSI 기본 프로파일에 따라 선호하는 인코딩). (Base64 인코딩](#invoking-aem-forms-using-base64-encoding)을 사용하여 AEM Forms 호출 참조)[
* **MTOM**:SOAP 요청이 있는 첨부 파일을 인코딩하는 방법을 나타냅니다. (MTOM](#invoking-aem-forms-using-mtom)을 사용하여 AEM Forms 호출 참조)[
* **SwaRef**:SOAP 요청이 있는 첨부 파일을 인코딩하는 또 다른 방법을 나타냅니다. (SwaRef](#invoking-aem-forms-using-swaref)을(를) 사용하여 AEM Forms 호출 참조)[
* **첨부 파일이 있는 SOAP**:MIME 및 DIME(직접 인터넷 메시지 캡슐화)를 모두 지원합니다. 이러한 프로토콜은 SOAP를 통해 첨부 파일을 전송하는 일반적인 방법입니다. Microsoft Visual Studio .NET 응용 프로그램은 DIME를 사용합니다. (Base64 인코딩](#invoking-aem-forms-using-base64-encoding)을 사용하여 AEM Forms 호출 참조)[
* **WS-Security**:WS 보안 SOAP 헤더의 일부로 사용자 이름과 암호를 전송하는 표준 방법인 사용자 이름 암호 토큰 프로필을 지원합니다. AEM Forms은 HTTP 기본 인증도 지원합니다. (WS-Security 헤더](https://www.adobe.com/devnet/livecycle/articles/passing_credentials.html)를 사용하여 자격 증명 전달을 참조하십시오.)[

웹 서비스를 사용하여 AEM Forms 서비스를 호출하려면 일반적으로 서비스 WSDL을 사용하는 프록시 라이브러리를 만듭니다. *웹 서비스를 사용하여 AEM Forms 호출* 섹션에서는 JAX-WS를 사용하여 Java 프록시 클래스를 만들어 서비스를 호출합니다. (JAX-WS](#creating-java-proxy-classes-using-jax-ws)를 사용하여 Java 프록시 클래스 만들기를 참조하십시오.)[

다음 URL 정의를 지정하여 서비스 WDSL을 검색할 수 있습니다(대괄호 안의 항목은 선택 사항).

```java
 https://<your_serverhost>:<your_port>/soap/services/<service_name>?wsdl[&version=<version>][&async=true|false][lc_version=<lc_version>]
```

where:

* *your_* serverhostream에서는 AEM Forms을 호스팅하는 J2EE 응용 프로그램 서버의 IP 주소를 표시합니다.
* *your_* profile은 J2EE 응용 프로그램 서버에서 사용하는 HTTP 포트를 나타냅니다.
* *service_* name서비스 이름을 나타냅니다.
* *버전* 서비스의 대상 버전을 나타냅니다(기본적으로 최신 서비스 버전이 사용됩니다).
* `async` 비동기 호출 `true` 에 대한 추가 작업을 활성화할 값을 지정합니다(기본값 `false` 으로).
* *lc_* versioninvoke호출할 AEM Forms 버전을 나타냅니다.

다음 표에는 서비스 WSDL 정의가 나열됩니다(AEM Forms이 로컬 호스트에 배포되고 게시물이 8080이라고 가정).

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
   <td><p>바코드 양식</p></td>
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
   <td><p>문서 관리</p></td>
   <td><p><code>http://localhost:8080/soap/services/DocumentManagementService?WSDL</code></p></td>
  </tr>
  <tr>
   <td><p>암호화 </p></td>
   <td><p><code>http://localhost:8080/soap/services/EncryptionService?wsdl</code></p></td>
  </tr>
  <tr>
   <td><p>양식</p></td>
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
   <td><p>권한 관리 </p></td>
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

Workbench에서 만든 프로세스에 속하는 WSDL에 액세스하려면 WSDL 정의 내에서 응용 프로그램 이름과 프로세스 이름을 지정해야 합니다. 응용 프로그램의 이름이 `MyApplication`이고 프로세스 이름이 `EncryptDocument`이라고 가정합니다. 이 경우 다음 WSDL 정의를 지정합니다.

```java
 http://localhost:8080/soap/services/MyApplication/EncryptDocument?wsdl
```

>[!NOTE]
>
>`MyApplication/EncryptDocument` 짧은 사용 프로세스에 대한 자세한 내용은 [짧은 사용 프로세스 예](/help/forms/developing/aem-forms-processes.md)를 참조하십시오.

>[!NOTE]
>
>응용 프로그램에는 폴더가 포함될 수 있습니다. 이 경우 WSDL 정의에서 폴더 이름을 지정합니다.

```java
 http://localhost:8080/soap/services/MyApplication/[<folderA>/.../<folderZ>/]EncryptDocument?wsdl
```

**웹 서비스를 사용하여 새 기능 액세스**

웹 서비스를 사용하여 새로운 AEM Forms 서비스 기능에 액세스할 수 있습니다. 예를 들어 AEM Forms에서는 MTOM을 사용하여 첨부 파일을 인코딩하는 기능이 도입되었습니다. (MTOM](#invoking-aem-forms-using-mtom)을 사용하여 AEM Forms 호출 참조)[

AEM Forms에 도입된 새 기능에 액세스하려면 WSDL 정의에 `lc_version` 속성을 지정합니다. 예를 들어, 새 서비스 기능(MTOM 지원 포함)에 액세스하려면 다음 WSDL 정의를 지정합니다.

```java
 http://localhost:8080/soap/services/MyApplication/EncryptDocument?wsdl&lc_version=9.0.1
```

>[!NOTE]
>
>`lc_version` 속성을 설정할 때 3자리 숫자를 사용해야 합니다. 예를 들어 9.0.1은 버전 9.0과 같습니다.

**웹 서비스 BLOB 데이터 유형**

AEM Forms 서비스 WSDL은 다양한 데이터 유형을 정의합니다. 웹 서비스에 노출되는 가장 중요한 데이터 형식 중 하나는 `BLOB` 유형입니다. 이 데이터 유형은 AEM Forms Java API로 작업할 때 `com.adobe.idp.Document` 클래스에 매핑됩니다. (Java API](/help/forms/developing/invoking-aem-forms-using-java.md#passing-data-to-aem-forms-services-using-the-java-api)를 사용하여 AEM Forms 서비스에 데이터 전달을 참조하십시오.)[

`BLOB` 개체는 AEM Forms 서비스를 통해 바이너리 데이터(예: PDF 파일, XML 데이터 등)를 보내고 검색합니다. `BLOB` 유형은 다음과 같이 서비스 WSDL에 정의됩니다.

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

`MTOM` 및 `swaRef` 필드는 AEM Forms에서만 지원됩니다. 이러한 새 필드는 `lc_version` 속성을 포함하는 URL을 지정하는 경우에만 사용할 수 있습니다.

**서비스 요청에 BLOB 개체 제공**

AEM Forms 서비스 작업에 입력 값으로 `BLOB` 유형이 필요한 경우 응용 프로그램 논리에 `BLOB` 유형의 인스턴스를 만듭니다. (대부분의 웹 서비스 빠른 시작 위치는 *AEM 양식을 사용한 프로그래밍*&#x200B;에 있으며 BLOB 데이터 유형을 사용하여 작업하는 방법을 보여줍니다.)

다음과 같이 `BLOB` 인스턴스에 속하는 필드에 값을 할당합니다.

* **Base64**:데이터를 Base64 형식으로 인코딩된 텍스트로 전달하려면  `BLOB.binaryData` 필드에 데이터를 설정하고 필드에 데이터 유형(예: MIME 형식) `application/pdf`을  `BLOB.contentType` 설정합니다. (Base64 인코딩](#invoking-aem-forms-using-base64-encoding)을 사용하여 AEM Forms 호출 참조)[
* **MTOM**:MTOM 첨부 파일에서 이진 데이터를 전달하려면 필드에 데이터를  `BLOB.MTOM` 설정합니다. 이 설정은 Java JAX-WS 프레임워크 또는 SOAP 프레임워크의 기본 API를 사용하여 데이터를 SOAP 요청에 첨부합니다. (MTOM](#invoking-aem-forms-using-mtom)을 사용하여 AEM Forms 호출 참조)[
* **SwaRef**:WS-I SwaRef 첨부 파일에서 이진 데이터를 전달하려면 필드에 데이터를  `BLOB.swaRef` 설정합니다. 이 설정은 Java JAX-WS 프레임워크를 사용하여 데이터를 SOAP 요청에 첨부합니다. (SwaRef](#invoking-aem-forms-using-swaref)을(를) 사용하여 AEM Forms 호출 참조)[
* **MIME 또는 DIME 첨부**:MIME 또는 DIME 첨부 파일로 데이터를 전달하려면 SOAP 프레임워크의 기본 API를 사용하여 데이터를 SOAP 요청에 첨부합니다. `BLOB.attachmentID` 필드에 첨부 파일 식별자를 설정합니다. (Base64 인코딩](#invoking-aem-forms-using-base64-encoding)을 사용하여 AEM Forms 호출 참조)[
* **원격 URL**:데이터가 웹 서버에 호스팅되고 HTTP URL을 통해 액세스할 수 있는 경우 필드에 HTTP URL을  `BLOB.remoteURL` 설정합니다. (HTTP](#invoking-aem-forms-using-blob-data-over-http)를 통해 BLOB 데이터를 사용하여 AEM Forms 호출 참조)[

**서비스에서 반환되는 BLOB 개체의 데이터에 액세스**

반환된 `BLOB` 개체에 대한 전송 프로토콜은 몇 가지 요소에 따라 다르며, 기본 조건이 충족될 때 중지되는 다음 순서로 간주됩니다.

1. **Target URL은 전송 프로토콜을 지정합니다**. SOAP 호출에서 지정된 대상 URL에 `blob="`*BLOB_TYPE*&quot; 매개 변수가 포함된 경우 *BLOB_TYPE*&#x200B;은(는) 전송 프로토콜을 결정합니다. *BLOB_* TYPE은 base64, 다임, MIME, http, mtom 또는 swaref의 자리 표시자입니다.
1. **서비스 SOAP 끝점이 Smart입니다**. 다음 조건이 true이면 출력 문서가 입력 문서와 동일한 전송 프로토콜을 사용하여 반환됩니다.

   * 서비스의 SOAP 끝점 매개 변수 출력 Blob 개체에 대한 기본 프로토콜이 Smart로 설정됩니다.

      SOAP 끝점이 있는 각 서비스에 대해 관리 콘솔을 사용하여 반환된 모든 블로브에 대한 전송 프로토콜을 지정할 수 있습니다. ([관리 도움말](https://www.adobe.com/go/learn_aemforms_admin_63)을 참조하십시오.)

   * AEM Forms 서비스는 하나 이상의 문서를 입력으로 사용합니다.

1. **서비스 SOAP 끝점이 스마트하지 않습니다**. 구성된 프로토콜은 문서 전송 프로토콜을 결정하고, 데이터는 해당 `BLOB` 필드에 반환됩니다. 예를 들어 SOAP 끝점이 DIME로 설정된 경우 반환된 blob는 입력 문서의 전송 프로토콜에 관계없이 `blob.attachmentID` 필드에 있습니다.
1. **그렇지 않으면**. 서비스가 문서 유형을 입력으로 가져가지 않으면 출력 문서가 HTTP 프로토콜의 `BLOB.remoteURL` 필드에 반환됩니다.

첫 번째 조건에 설명된 대로, 다음과 같이 SOAP 끝점 URL을 접미어로 확대하여 반환된 문서의 전송 유형을 확인할 수 있습니다.

```java
     https://<your_serverhost>:<your_port>/soap/services/<service
     name>?blob=base64|dime|mime|http|mtom|swaref
```

다음은 데이터를 얻는 필드와 전송 유형 간의 상관입니다.

* **Base64 형식**:필드 `blob` 의 데이터 `base64` 를 반환하려면 접미사를 로  `BLOB.binaryData` 설정합니다.
* **MIME 또는 DIME 첨부**:접미사 `blob` 를  `DIME` 또는 `MIME` 로 설정하여 필드에 반환되는 첨부 ID가 있는 해당 첨부 파일 유형으로 데이터를  `BLOB.attachmentID` 반환합니다. SOAP 프레임워크의 독점 API를 사용하여 첨부 파일의 데이터를 읽습니다.
* **원격 URL**:애플리케이션 서버 `blob` 에 데이터를  `http` 유지하고 필드의 데이터를 가리키는 URL을 반환하려면 접미어를 다음으로  `BLOB.remoteURL` 설정합니다.
* **MTOM 또는 SwaRef**:접미어를  `blob` 또는으로  `mtom` 설정하거나,  `swaref` 또는 필드에 반환되는 첨부 ID가 있는 해당 첨부 파일 형식 `BLOB.MTOM` 으로 데이터를  `BLOB.swaRef` 반환합니다. SOAP 프레임워크의 기본 API를 사용하여 첨부 파일의 데이터를 읽습니다.

>[!NOTE]
>
>`setBinaryData` 메서드를 호출하여 `BLOB` 개체를 채울 때는 30MB를 초과하지 않는 것이 좋습니다. 그렇지 않으면 `OutOfMemory` 예외가 발생할 가능성이 있습니다.

>[!NOTE]
>
>MTOM 전송 프로토콜을 사용하는 JAX WS 기반 애플리케이션은 전송 및 수신 데이터의 25MB로 제한됩니다. 이 제한은 JAX-WS의 버그로 인한 것입니다. 전송 및 수신한 파일의 크기가 25MB를 초과하는 경우 MTOM 대신 SwaRef 전송 프로토콜을 사용합니다. 그렇지 않으면 `OutOfMemory` 예외가 발생할 수 있습니다.

**base64로 인코딩된 바이트 배열의 MTOM 전송**

MTOM 프로토콜은 `BLOB` 객체 외에도 복잡한 유형의 바이트 배열 매개 변수 또는 바이트 배열 필드를 지원합니다. 즉, MTOM을 지원하는 클라이언트 SOAP 프레임워크는 모든 `xsd:base64Binary` 요소를 MTOM 첨부 파일로 보낼 수 있습니다(base64로 인코딩된 텍스트 대신). AEM Forms SOAP 끝점은 이 유형의 바이트 배열 인코딩을 읽을 수 있습니다. 그러나 AEM Forms 서비스는 항상 바이트 배열 유형을 base64 인코딩 텍스트로 반환합니다. 출력 바이트 배열 매개 변수는 MTOM을 지원하지 않습니다.

많은 양의 이진 데이터를 반환하는 AEM Forms 서비스는 바이트 배열 유형이 아닌 문서/BLOB 형식을 사용합니다. 문서 유형은 대량의 데이터를 전송하는 데 훨씬 효율적입니다.

## 웹 서비스 데이터 유형 {#web-service-data-types}

다음 표는 Java 데이터 유형을 나열하고 해당 웹 서비스 데이터 유형을 보여줍니다.

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
   <td><p>다음과 같이 서비스 WSDL에 정의된 <code>DATE</code> 유형입니다.</p><p><code>&lt;complexType name="DATE"&gt;</code></p><p><code>&lt;sequence&gt;</code></p><p><code>&lt;element maxOccurs="1" minOccurs="0" name="date" </code><code>type="xsd:dateTime" /&gt; </code></p><p><code>&lt;element maxOccurs="1" minOccurs="0" name="calendar" </code><code>type="xsd:dateTime" /&gt; </code></p><p><code>&lt;/sequence&gt;</code></p><p><code>&lt;/complexType&gt;</code></p><p>AEM Forms 서비스 작업이 <code>java.util.Date</code> 값을 입력으로 사용하는 경우 SOAP 클라이언트 응용 프로그램은 <code>DATE.date</code> 필드에 날짜를 전달해야 합니다. 이 경우 <code>DATE.calendar</code> 필드를 설정하면 런타임 예외가 발생합니다. 서비스가 <code>java.util.Date</code>을 반환하면 날짜가 <code>DATE.date</code> 필드에 다시 표시됩니다.</p></td>
  </tr>
  <tr>
   <td><p><code>java.util.Calendar</code></p></td>
   <td><p>다음과 같이 서비스 WSDL에 정의된 <code>DATE</code> 유형입니다.</p><p><code>&lt;complexType name="DATE"&gt;</code></p><p><code>&lt;sequence&gt;</code></p><p><code>&lt;element maxOccurs="1" minOccurs="0" name="date" </code><code>type="xsd:dateTime" /&gt; </code></p><p><code>&lt;element maxOccurs="1" minOccurs="0" name="calendar" </code><code>type="xsd:dateTime" /&gt; </code></p><p><code>&lt;/sequence&gt;</code></p><p><code>&lt;/complexType&gt;</code></p><p>AEM Forms 서비스 작업이 <code>java.util.Calendar</code> 값을 입력으로 사용하는 경우 SOAP 클라이언트 응용 프로그램은 <code>DATE.caledendar</code> 필드에 날짜를 전달해야 합니다. 이 경우 <code>DATE.date</code> 필드를 설정하면 런타임 예외가 발생합니다. 서비스가 <code>java.util.Calendar</code>을 반환하면 날짜가 <code>DATE.calendar</code> 필드에 반환됩니다. </p></td>
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
   <td><p>다음과 같이 서비스 WSDL에 정의된 <code>apachesoap:Map</code>:</p><p><code>&lt;schema elementFormDefault="qualified" targetNamespace="https://xml.apache.org/xml-soap" xmlns="https://www.w3.org/2001/XMLSchema"&gt;</code></p><p><code>&lt;complexType name="mapItem"&gt;</code></p><p><code>&lt;sequence&gt;</code></p><p><code>&lt;element name="key" nillable="true" type="xsd:anyType"/&gt;</code></p><p><code>&lt;element name="value" nillable="true" type="xsd:anyType"/&gt;</code></p><p><code>&lt;/sequence&gt;</code></p><p><code>&lt;/complexType&gt;</code></p><p><code>&lt;complexType name="Map"&gt;</code></p><p><code>&lt;sequence&gt;</code></p><p><code>&lt;element maxOccurs="unbounded" minOccurs="0" name="item" </code><code>type="apachesoap:mapItem"/&gt;</code></p><p><code>&lt;/sequence&gt;</code></p><p><code>&lt;/complexType&gt;</code></p><p><code>&lt;/schema&gt;</code></p><p>맵은 키/값 쌍의 시퀀스로 표시됩니다.</p></td>
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
   <td><p>다음과 같이 서비스 WSDL에 정의된 XML 유형입니다.</p><p><code>&lt;complexType name="XML"&gt;</code></p><p><code>&lt;sequence&gt;</code></p><p><code>&lt;element maxOccurs="1" minOccurs="0" name="document" </code><code>type="xsd:string" /&gt; </code></p><p><code>&lt;element maxOccurs="1" minOccurs="0" name="element" </code><code>type="xsd:string" /&gt; </code></p><p><code>&lt;/sequence&gt;</code></p><p><code>&lt;/complexType&gt;</code></p><p>AEM Forms 서비스 작업에서 <code>org.w3c.dom.Document</code> 값을 허용하는 경우 <code>XML.document</code> 필드에 XML 데이터를 전달합니다.</p><p><code>XML.element</code> 필드를 설정하면 런타임 예외가 발생합니다. 서비스가 <code>org.w3c.dom.Document</code>을 반환하면 XML 데이터가 <code>XML.document</code> 필드에 반환됩니다.</p></td>
  </tr>
  <tr>
   <td><p><code>org.w3c.dom.Element</code></p></td>
   <td><p>다음과 같이 서비스 WSDL에 정의된 XML 유형입니다.</p><p><code>&lt;complexType name="XML"&gt;</code></p><p><code>&lt;sequence&gt;</code></p><p><code>&lt;element maxOccurs="1" minOccurs="0" name="document" </code><code>type="xsd:string" /&gt; </code></p><p><code>&lt;element maxOccurs="1" minOccurs="0" name="element" </code><code>type="xsd:string" /&gt; </code></p><p><code>&lt;/sequence&gt;</code></p><p><code>&lt;/complexType&gt;</code></p><p>AEM Forms 서비스 작업이 <code>org.w3c.dom.Element</code>을(를) 입력으로 사용하는 경우 <code>XML.element</code> 필드에 XML 데이터를 전달합니다.</p><p><code>XML.document</code> 필드를 설정하면 런타임 예외가 발생합니다. 서비스가 <code>org.w3c.dom.Element</code>을 반환하면 XML 데이터가 <code>XML.element</code> 필드에 다시 추가됩니다.</p></td>
  </tr>
 </tbody>
</table>

**Adobe 개발자 웹 사이트**

Adobe 개발자 웹 사이트에는 웹 서비스 API를 사용하여 AEM Forms 서비스를 호출하는 방법에 대해 설명하는 다음 문서가 포함되어 있습니다.

[양식 렌더링 ASP.NET 응용 프로그램 만들기](https://www.adobe.com/devnet/livecycle/articles/asp_net.html)

[사용자 지정 구성 요소를 사용하여 웹 서비스 호출](https://www.adobe.com/devnet/livecycle/articles/extend_webservices.html)

>[!NOTE]
>
>사용자 지정 구성 요소를 사용하여 웹 서비스를 호출하면 제3자 웹 서비스를 호출하는 AEM Forms 구성 요소를 만드는 방법에 대해 설명합니다.

## JAX-WS {#creating-java-proxy-classes-using-jax-ws}를 사용하여 Java 프록시 클래스 만들기

JAX-WS를 사용하여 Forms 서비스 WSDL을 Java 프록시 클래스로 변환할 수 있습니다. 이러한 클래스를 사용하여 AEM Forms 서비스 작업을 호출할 수 있습니다. Apache Ant를 사용하면 AEM Forms 서비스 WSDL을 참조하여 Java 프록시 클래스를 생성하는 빌드 스크립트를 만들 수 있습니다. 다음 단계를 수행하여 JAX-WS 프록시 파일을 생성할 수 있습니다.

1. 클라이언트 컴퓨터에 Apache Ant를 설치합니다. (자세한 내용은 [https://ant.apache.org/bindownload.cgi](https://ant.apache.org/bindownload.cgi)을 참조하십시오.)

   * 클래스 경로에 bin 디렉토리를 추가합니다.
   * `ANT_HOME` 환경 변수를 Ant를 설치한 디렉토리로 설정합니다.

1. JDK 1.6 이상을 설치합니다.

   * 클래스 경로에 JDK 저장소 디렉토리를 추가합니다.
   * 클래스 경로에 JRE 저장소 디렉토리를 추가합니다. 이 저장소는 `[JDK_INSTALL_LOCATION]/jre` 디렉토리에 있습니다.
   * `JAVA_HOME` 환경 변수를 JDK를 설치한 디렉토리로 설정합니다.

   JDK 1.6에는 build.xml 파일에 사용되는 wsimport 프로그램이 포함되어 있습니다. JDK 1.5에는 해당 프로그램이 포함되어 있지 않습니다.

1. 클라이언트 컴퓨터에 JAX-WS를 설치합니다. ([XML Web Services용 Java API](https://jax-ws.dev.java.net/jax-ws-ea3/docs/mtom-swaref.html)를 참조하십시오.)
1. JAX-WS 및 Apache Ant를 사용하여 Java 프록시 클래스를 생성합니다. 이 작업을 수행할 Ant 빌드 스크립트를 만듭니다. 다음 스크립트는 build.xml이라는 샘플 Ant 빌드 스크립트입니다.

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

   이 Ant 빌드 스크립트 내에서 `url` 속성이 localhost에서 실행되는 암호화 서비스 WSDL을 참조하도록 설정되어 있습니다. `username` 및 `password` 속성은 유효한 AEM 양식 사용자 이름과 암호로 설정해야 합니다. URL에 `lc_version` 특성이 포함되어 있습니다. `lc_version` 옵션을 지정하지 않으면 새 AEM Forms 서비스 작업을 호출할 수 없습니다.

   >[!NOTE]
   >
   >`EncryptionService`을(를) Java 프록시 클래스를 사용하여 호출할 AEM Forms 서비스 이름으로 대체합니다. 예를 들어 Rights Management 서비스에 대한 Java 프록시 클래스를 만들려면 다음을 지정합니다.

   ```java
    http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1
   ```

1. BAT 파일을 만들어 Ant 빌드 스크립트를 실행합니다. 다음 명령은 Ant 빌드 스크립트를 실행하는 BAT 파일 내에서 찾을 수 있습니다.

   ```java
    ant -buildfile "build.xml" wsdl
   ```

   C:\Program Files\Java\jaxws-ri\bin directory폴더에 ANT 빌드 스크립트를 배치합니다. 스크립트는 JAVA 파일을/classes 폴더를 참조하십시오. 이 스크립트는 서비스를 호출할 수 있는 JAVA 파일을 생성합니다.

1. JAVA 파일을 JAR 파일로 패키지화합니다. Eclipse에서 작업하는 경우 다음 단계를 수행합니다.

   * 프록시 JAVA 파일을 JAR 파일로 패키징하는 데 사용되는 새 Java 프로젝트를 만듭니다.
   * 프로젝트에서 소스 폴더를 만듭니다.
   * 소스 폴더에 `com.adobe.idp.services` 패키지를 만듭니다.
   * `com.adobe.idp.services` 패키지를 선택한 다음 adobe/idp/services 폴더의 JAVA 파일을 패키지로 가져옵니다.
   * 필요한 경우 소스 폴더에 `org/apache/xml/xmlsoap` 패키지를 만듭니다.
   * 소스 폴더를 선택한 다음 org/apache/xml/xmlsoap 폴더에서 JAVA 파일을 가져옵니다.
   * Java 컴파일러의 준수 수준을 5.0 이상으로 설정합니다.
   * 프로젝트를 빌드합니다.
   * 프로젝트를 JAR 파일로 내보냅니다.
   * 이 JAR 파일을 클라이언트 프로젝트의 클래스 경로로 가져옵니다. 또한 &lt;Install Directory>\Adobe\Adobe_Experience_Manager_forms\sdk\client-libs\thirdparty에 있는 모든 JAR 파일을 가져옵니다.

   >[!NOTE]
   >
   >AEM 양식을 사용한 프로그래밍에 있는 모든 Java 웹 서비스 빠른 시작(Forms 서비스 제외)은 JAX-WS를 사용하여 Java 프록시 파일을 만듭니다. 또한 모든 Java 웹 서비스 빠른 시작 시 SwaRef를 사용하십시오. (SwaRef](#invoking-aem-forms-using-swaref)을(를) 사용하여 AEM Forms 호출 참조)[

**참고 항목**

[Apache Axis를 사용하여 Java 프록시 클래스 만들기](#creating-java-proxy-classes-using-apache-axis)

[Base64 인코딩을 사용하여 AEM Forms 호출](#invoking-aem-forms-using-base64-encoding)

[HTTP를 통해 BLOB 데이터를 사용하여 AEM Forms 호출](#invoking-aem-forms-using-blob-data-over-http)

[SwaRef를 사용하여 AEM Forms 호출](#invoking-aem-forms-using-swaref)

## Apache Axis {#creating-java-proxy-classes-using-apache-axis}을(를) 사용하여 Java 프록시 클래스 만들기

Apache Axis WSDL2Java 도구를 사용하여 Forms 서비스를 Java 프록시 클래스로 변환할 수 있습니다. 이러한 클래스를 사용하여 Forms 서비스 작업을 호출할 수 있습니다. Apache Ant를 사용하면 서비스 WSDL에서 축 라이브러리 파일을 생성할 수 있습니다. URL [https://ws.apache.org/axis/](https://ws.apache.org/axis/)에서 Apache Axis를 다운로드할 수 있습니다.

>[!NOTE]
>
>Forms 서비스와 연관된 웹 서비스 빠른 시작 부분에서는 Apache Axis를 사용하여 만든 Java 프록시 클래스를 사용합니다. Forms 웹 서비스 빠른 시작 또한 인코딩 유형으로 Base64를 사용합니다. ([Forms 서비스 API 빠른 시작](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)을 참조하십시오.)

다음 단계를 수행하여 축 Java 라이브러리 파일을 생성할 수 있습니다.

1. 클라이언트 컴퓨터에 Apache Ant를 설치합니다. [https://ant.apache.org/bindownload.cgi](https://ant.apache.org/bindownload.cgi)에서 사용할 수 있습니다.

   * 클래스 경로에 bin 디렉토리를 추가합니다.
   * `ANT_HOME` 환경 변수를 Ant를 설치한 디렉토리로 설정합니다.

1. 클라이언트 컴퓨터에 Apache Axis 1.4를 설치합니다. [https://ws.apache.org/axis/](https://ws.apache.org/axis/.md)에서 사용할 수 있습니다.
1. [https://ws.apache.org/axis/java/install.html](https://ws.apache.org/axis/java/install.html)의 축 설치 지침에 설명된 대로 웹 서비스 클라이언트에서 축 JAR 파일을 사용하도록 클래스 경로를 설정합니다.
1. 축의 Apache WSDL2Java 도구를 사용하여 Java 프록시 클래스를 생성합니다. 이 작업을 수행할 Ant 빌드 스크립트를 만듭니다. 다음 스크립트는 build.xml이라는 샘플 Ant 빌드 스크립트입니다.

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

   이 Ant 빌드 스크립트 내에서 `url` 속성이 localhost에서 실행되는 암호화 서비스 WSDL을 참조하도록 설정되어 있습니다. `username` 및 `password` 속성은 유효한 AEM 양식 사용자 이름과 암호로 설정해야 합니다.

1. BAT 파일을 만들어 Ant 빌드 스크립트를 실행합니다. 다음 명령은 Ant 빌드 스크립트를 실행하는 BAT 파일 내에서 찾을 수 있습니다.

   ```java
    ant -buildfile "build.xml" encryption-wsdl2java-client
   ```

   JAVA 파일은 C:\JavaFiles folder as specified by the `output` 속성에 기록됩니다. Forms 서비스를 성공적으로 호출하려면 이러한 JAVA 파일을 클래스 경로로 가져옵니다.

   기본적으로 이러한 파일은 `com.adobe.idp.services`이라는 Java 패키지에 속합니다. JAR 파일에 이러한 JAVA 파일을 배치하는 것이 좋습니다. 그런 다음 JAR 파일을 클라이언트 응용 프로그램의 클래스 경로로 가져옵니다.

   >[!NOTE]
   >
   >.JAVA 파일을 JAR에 넣는 방법은 다양합니다. 한 가지 방법은 Eclipse와 같은 Java IDE를 사용하는 것입니다. Java 프로젝트를 만들고 `com.adobe.idp.services` 패키지를 만듭니다(모든 .JAVA 파일이 이 패키지에 속함). 그런 다음 모든 .JAVA 파일을 패키지에 가져옵니다. 마지막으로 프로젝트를 JAR 파일로 내보냅니다.

1. `EncryptionServiceLocator` 클래스의 URL을 수정하여 인코딩 유형을 지정합니다. 예를 들어 base64를 사용하려면 `?blob=base64`을 지정하여 `BLOB` 객체가 이진 데이터를 반환하도록 하십시오. 즉, `EncryptionServiceLocator` 클래스에서 다음 코드 행을 찾습니다.

   ```java
    http://localhost:8080/soap/services/EncryptionService;
   ```

   를 다음과 같이 변경합니다.

   ```java
    http://localhost:8080/soap/services/EncryptionService?blob=base64;
   ```

1. Java 프로젝트의 클래스 경로에 다음 축 JAR 파일을 추가합니다.

   * activation.jar
   * axis.jar
   * commons-codec-1.3.jar
   * commons-collections-3.1.jar
   * commons-discovery.jar
   * commons-logging.jar
   * dom3-xml-api-2.5.0.jar
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

   이러한 JAR 파일은 `[install directory]/Adobe/Adobe Experience Manager Forms/sdk/lib/thirdparty` 디렉토리에 있습니다.

**참고 항목**

[JAX-WS를 사용하여 Java 프록시 클래스 만들기](#creating-java-proxy-classes-using-jax-ws)

[Base64 인코딩을 사용하여 AEM Forms 호출](#invoking-aem-forms-using-base64-encoding)

[HTTP를 통해 BLOB 데이터를 사용하여 AEM Forms 호출](#invoking-aem-forms-using-blob-data-over-http)

## Base64 인코딩을 사용하여 AEM Forms 호출 {#invoking-aem-forms-using-base64-encoding}

Base64 인코딩을 사용하여 AEM Forms 서비스를 호출할 수 있습니다. Base64 인코딩은 웹 서비스 호출 요청과 함께 전송된 첨부 파일을 인코딩합니다. 즉, `BLOB` 데이터는 전체 SOAP 메시지가 아니라 Base64로 인코딩됩니다.

&quot;Base64 인코딩을 사용하여 AEM Forms 호출&quot;에서는 Base64 인코딩을 사용하여 `MyApplication/EncryptDocument`이라는 짧은 기간 프로세스를 호출하는 방법에 대해 설명합니다.

>[!NOTE]
>
>이 프로세스는 기존 AEM Forms 프로세스를 기반으로 하지 않습니다. 코드 예제를 따라 하려면 Workbench를 사용하여 `MyApplication/EncryptDocument` 프로세스를 만듭니다. ([Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63) 사용 참조)

이 프로세스가 호출되면 다음 작업을 수행합니다.

1. 프로세스에 전달된 보안되지 않은 PDF 문서를 가져옵니다. 이 작업은 `SetValue` 작업을 기반으로 합니다. 이 프로세스의 입력 매개 변수는 `inDoc`이라는 `document` 프로세스 변수입니다.
1. 암호로 PDF 문서를 암호화합니다. 이 작업은 `PasswordEncryptPDF` 작업을 기반으로 합니다. 암호로 암호화된 PDF 문서는 `outDoc` 프로세스 변수에 반환됩니다.

### Base64 인코딩을 사용하는 .NET 클라이언트 어셈블리 만들기 {#creating-a-net-client-assembly-that-uses-base64-encoding}

.NET 클라이언트 어셈블리를 만들어 Microsoft Visual Studio .NET 프로젝트에서 Forms 서비스를 호출할 수 있습니다. base64 인코딩을 사용하는 .NET 클라이언트 어셈블리를 만들려면 다음 단계를 수행하십시오.

1. AEM Forms 호출 URL을 기반으로 프록시 클래스를 만듭니다.
1. .NET 클라이언트 어셈블리를 생성하는 Microsoft Visual Studio .NET 프로젝트를 만듭니다.

**프록시 클래스 만들기**

Microsoft Visual Studio에 지정된 도구를 사용하여 .NET 클라이언트 어셈블리를 만드는 데 사용되는 프록시 클래스를 만들 수 있습니다. 도구의 이름은 wsdl.exe이며 Microsoft Visual Studio 설치 폴더에 있습니다. 프록시 클래스를 만들려면 명령 프롬프트를 열고 wsdl.exe 파일이 포함된 폴더로 이동합니다. wsdl.exe 도구에 대한 자세한 내용은 *MSDN 도움말*&#x200B;을 참조하십시오.

명령 프롬프트에서 다음 명령을 입력합니다.

```java
 wsdl https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?WSDL&lc_version=9.0.1
```

기본적으로 이 도구는 WSDL의 이름을 기반으로 하는 동일한 폴더에 CS 파일을 만듭니다. 이 경우 *EncryptDocumentService.cs*&#x200B;라는 CS 파일이 만들어집니다. 이 CS 파일을 사용하여 호출 URL에 지정된 서비스를 호출할 수 있는 프록시 개체를 만듭니다.

`BLOB` 객체가 이진 데이터를 반환하도록 프록시 클래스의 URL을 `?blob=base64`을 포함하도록 수정합니다. 프록시 클래스에서 다음 코드 행을 찾습니다.

```java
 "https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument";
```

를 다음과 같이 변경합니다.

```java
 "https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?blob=base64";
```

*Base64 Encoding* 섹션을 사용하여 AEM Forms 호출 섹션은 `MyApplication/EncryptDocument`를 예로 사용합니다. 다른 Forms 서비스에 대한 .NET 클라이언트 어셈블리를 만드는 경우 `MyApplication/EncryptDocument`을(를) 서비스 이름으로 바꾸십시오.

**.NET 클라이언트 어셈블리 개발**

.NET 클라이언트 어셈블리를 생성하는 Visual Studio 클래스 라이브러리 프로젝트를 만듭니다. wsdl.exe를 사용하여 만든 CS 파일을 이 프로젝트로 가져올 수 있습니다. 이 프로젝트는 다른 Visual Studio .NET 프로젝트에서 서비스를 호출하는 데 사용할 수 있는 DLL 파일(.NET 클라이언트 어셈블리)을 생성합니다.

1. Microsoft Visual Studio .NET을 시작합니다.
1. 클래스 라이브러리 프로젝트를 만들고 이름을 DocumentService로 지정합니다.
1. wsdl.exe를 사용하여 만든 CS 파일을 가져옵니다.
1. **프로젝트** 메뉴에서 **참조 추가**&#x200B;를 선택합니다.
1. 참조 추가 대화 상자에서 **System.Web.Services.dll**&#x200B;을 선택합니다.
1. **선택**&#x200B;을 클릭한 다음 **확인**&#x200B;을 클릭합니다.
1. 프로젝트를 컴파일하고 빌드합니다.

>[!NOTE]
>
>이 절차에서는 SOAP 요청을 `MyApplication/EncryptDocument` 서비스로 보내는 데 사용할 수 있는 DocumentService.dll이라는 .NET 클라이언트 어셈블리를 만듭니다.

>[!NOTE]
>
>.NET 클라이언트 어셈블리를 만드는 데 사용되는 프록시 클래스의 URL에 `?blob=base64`을(를) 추가해야 합니다. 그렇지 않으면 `BLOB` 개체에서 이진 데이터를 검색할 수 없습니다.

**.NET 클라이언트 어셈블리 참조**

클라이언트 응용 프로그램을 개발할 컴퓨터에 새로 만든 .NET 클라이언트 어셈블리를 배치합니다. .NET 클라이언트 어셈블리를 디렉토리에 배치한 후 프로젝트에서 참조할 수 있습니다. 프로젝트의 `System.Web.Services` 라이브러리도 참조합니다. 이 라이브러리를 참조하지 않으면 .NET 클라이언트 어셈블리를 사용하여 서비스를 호출할 수 없습니다.

1. **프로젝트** 메뉴에서 **참조 추가**&#x200B;를 선택합니다.
1. **.NET** 탭을 클릭합니다.
1. **찾아보기**&#x200B;를 클릭하고 DocumentService.dll 파일을 찾습니다.
1. **선택**&#x200B;을 클릭한 다음 **확인**&#x200B;을 클릭합니다.

**Base64 인코딩을 사용하는 .NET 클라이언트 어셈블리를 사용하여 서비스 호출**

Base64 인코딩을 사용하는 .NET 클라이언트 어셈블리를 사용하여 `MyApplication/EncryptDocument` 서비스(Workbench에 내장된)를 호출할 수 있습니다. `MyApplication/EncryptDocument` 서비스를 호출하려면 다음 단계를 수행하십시오.

1. `MyApplication/EncryptDocument` 서비스 WSDL을 사용하는 Microsoft .NET 클라이언트 어셈블리를 만듭니다.
1. 클라이언트 Microsoft .NET 프로젝트를 만듭니다. 클라이언트 프로젝트에서 Microsoft .NET 클라이언트 어셈블리를 참조합니다. `System.Web.Services`도 참조합니다.
1. Microsoft .NET 클라이언트 어셈블리를 사용하여 기본 생성자를 호출하여 `MyApplication_EncryptDocumentService` 객체를 만듭니다.
1. `MyApplication_EncryptDocumentService` 개체의 `Credentials` 속성을 `System.Net.NetworkCredential` 개체로 설정합니다. `System.Net.NetworkCredential` 생성자 내에서 AEM 양식 사용자 이름과 해당 암호를 지정합니다. .NET 클라이언트 응용 프로그램이 AEM Forms과 SOAP 메시지를 성공적으로 교환할 수 있도록 하려면 인증 값을 설정합니다.
1. 생성자를 사용하여 `BLOB` 객체를 만듭니다. `BLOB` 개체는 `MyApplication/EncryptDocument` 프로세스에 PDF 문서 전달을 저장하는 데 사용됩니다.
1. 생성자를 호출하여 `System.IO.FileStream` 객체를 만듭니다. PDF 문서의 파일 위치와 파일을 열 모드를 나타내는 문자열 값을 전달합니다.
1. `System.IO.FileStream` 객체의 내용을 저장하는 바이트 배열을 만듭니다. `System.IO.FileStream` 객체의 `Length` 속성을 가져와 바이트 배열의 크기를 결정할 수 있습니다.
1. `System.IO.FileStream` 객체의 `Read` 메서드를 호출하여 바이트 배열을 스트림 데이터로 채웁니다. 바이트 배열, 시작 위치 및 읽을 스트림 길이를 전달합니다.
1. 바이트 배열의 내용으로 `binaryData` 속성을 할당하여 `BLOB` 객체를 채웁니다.
1. `MyApplication_EncryptDocumentService` 개체의 `invoke` 메서드를 호출하고 PDF 문서가 포함된 `BLOB` 개체를 전달하여 `MyApplication/EncryptDocument` 프로세스를 호출합니다. 이 프로세스는 `BLOB` 개체 내에서 암호화된 PDF 문서를 반환합니다.
1. 생성자를 호출하고 암호로 암호화된 문서의 파일 위치를 나타내는 문자열 값을 전달하여 `System.IO.FileStream` 객체를 만듭니다.
1. `MyApplicationEncryptDocumentService` 객체의 `invoke` 메서드에서 반환되는 `BLOB` 개체의 데이터 내용을 저장하는 바이트 배열을 만듭니다. `BLOB` 객체의 `binaryData` 데이터 멤버 값을 가져와 바이트 배열을 채웁니다.
1. 생성자를 호출하고 `System.IO.FileStream` 객체를 전달하여 `System.IO.BinaryWriter` 객체를 만듭니다.
1. `System.IO.BinaryWriter` 객체의 `Write` 메서드를 호출하고 바이트 배열을 전달하여 바이트 배열 내용을 PDF 파일에 씁니다.

### Java 프록시 클래스와 Base64 인코딩 {#invoking-a-service-using-java-proxy-classes-and-base64-encoding}을 사용하여 서비스 호출

Java 프록시 클래스 및 Base64를 사용하여 AEM Forms 서비스를 호출할 수 있습니다. Java 프록시 클래스를 사용하여 `MyApplication/EncryptDocument` 서비스를 호출하려면 다음 단계를 수행하십시오.

1. `MyApplication/EncryptDocument` 서비스 WSDL을 사용하는 JAX-WS를 사용하여 Java 프록시 클래스를 만듭니다. 다음 WSDL 끝점을 사용합니다.

   `https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?WSDL&lc_version=9.0.1`

   >[!NOTE]
   >
   >AEM Forms을 호스팅하는 J2EE 응용 프로그램 서버의 IP 주소로 `hiro-xp` *을(를) 바꿉니다.*

1. JAX-WS를 사용하여 만든 Java 프록시 클래스를 JAR 파일로 패키지화합니다.
1. 다음 경로에 있는 Java 프록시 JAR 파일과 JAR 파일을 포함합니다.

   &lt;install Directory=&quot;&quot;>\Adobe\Adobe_Experience_Manager_forms\sdk\client-libs\thirdparty

   을 Java 클라이언트 프로젝트의 클래스 경로에 추가합니다.

1. 생성자를 사용하여 `MyApplicationEncryptDocumentService` 객체를 만듭니다.
1. `MyApplicationEncryptDocumentService` 객체의 `getEncryptDocument` 메서드를 호출하여 `MyApplicationEncryptDocument` 객체를 만듭니다.
1. 다음 데이터 멤버에 값을 할당하여 AEM Forms을 호출하는 데 필요한 연결 값을 설정합니다.

   * WSDL 끝점과 인코딩 유형을 `javax.xml.ws.BindingProvider` 객체의 `ENDPOINT_ADDRESS_PROPERTY` 필드에 할당합니다. Base64 인코딩을 사용하여 `MyApplication/EncryptDocument` 서비스를 호출하려면 다음 URL 값을 지정합니다.

      `https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?blob=base64`

   * AEM 양식 사용자를 `javax.xml.ws.BindingProvider` 개체의 `USERNAME_PROPERTY` 필드에 할당합니다.
   * 해당 암호 값을 `javax.xml.ws.BindingProvider` 개체의 `PASSWORD_PROPERTY` 필드에 할당합니다.

   다음 코드 예제에서는 이 응용 프로그램 논리를 보여 줍니다.

   ```java
    //Set connection values required to invoke AEM Forms
    String url = "https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?blob=base64";
    String username = "administrator";
    String password = "password";
    ((BindingProvider) encryptDocClient).getRequestContext().put(BindingProvider.ENDPOINT_ADDRESS_PROPERTY, url);
    ((BindingProvider) encryptDocClient).getRequestContext().put(BindingProvider.USERNAME_PROPERTY, username);
    ((BindingProvider) encryptDocClient).getRequestContext().put(BindingProvider.PASSWORD_PROPERTY, password);
   ```

1. 생성자를 사용하여 `java.io.FileInputStream` 개체를 만들어 `MyApplication/EncryptDocument` 프로세스로 전송할 PDF 문서를 검색합니다. PDF 문서의 위치를 지정하는 문자열 값을 전달합니다.
1. 바이트 배열을 만들어 `java.io.FileInputStream` 객체의 내용으로 채웁니다.
1. 생성자를 사용하여 `BLOB` 객체를 만듭니다.
1. `setBinaryData` 메서드를 호출하고 바이트 배열을 전달하여 `BLOB` 객체를 채웁니다. `BLOB` 개체의 `setBinaryData`은 Base64 인코딩을 사용할 때 호출할 메서드입니다. 서비스 요청에서 BLOB 개체 공급을 참조하십시오.
1. `MyApplicationEncryptDocument` 객체의 `invoke` 메서드를 호출하여 `MyApplication/EncryptDocument` 프로세스를 호출합니다. PDF 문서를 포함하는 `BLOB` 개체를 전달합니다. invoke 메서드는 암호화된 PDF 문서를 포함하는 `BLOB` 객체를 반환합니다.
1. `BLOB` 개체의 `getBinaryData` 메서드를 호출하여 암호화된 PDF 문서를 포함하는 바이트 배열을 만듭니다.
1. 암호화된 PDF 문서를 PDF 파일로 저장할 수 있습니다. 바이트 배열을 파일에 씁니다.

**참고 항목**

[빠른 시작:Java 프록시 파일 및 Base64 인코딩을 사용하여 서비스 호출](/help/forms/developing/invocation-api-quick-starts.md#quick-start-invoking-a-service-using-java-proxy-files-and-base64-encoding)

[Base64 인코딩을 사용하는 .NET 클라이언트 어셈블리 만들기](#creating-a-net-client-assembly-that-uses-base64-encoding)

## MTOM {#invoking-aem-forms-using-mtom}을 사용하여 AEM Forms 호출

웹 서비스 표준 MTOM을 사용하여 AEM Forms 서비스를 호출할 수 있습니다. 이 표준은 PDF 문서와 같은 이진 데이터가 인터넷이나 인트라넷을 통해 전송되는 방식을 정의합니다. MTOM의 기능은 `XOP:Include` 요소를 사용하는 것입니다. 이 요소는 SOAP 메시지의 바이너리 첨부 파일을 참조하기 위해 XOP(XML Binary Optimized Packaging) 사양에 정의되어 있습니다.

여기서 논의는 MTOM을 사용하여 `MyApplication/EncryptDocument`이라는 짧은 AEM Forms 프로세스를 호출하는 것입니다.

>[!NOTE]
>
>이 프로세스는 기존 AEM Forms 프로세스를 기반으로 하지 않습니다. 코드 예제를 따라 하려면 Workbench를 사용하여 `MyApplication/EncryptDocument` 프로세스를 만듭니다. ([Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63) 사용 참조)

이 프로세스가 호출되면 다음 작업을 수행합니다.

1. 프로세스에 전달된 보안되지 않은 PDF 문서를 가져옵니다. 이 작업은 `SetValue` 작업을 기반으로 합니다. 이 프로세스의 입력 매개 변수는 `inDoc`이라는 `document` 프로세스 변수입니다.
1. 암호로 PDF 문서를 암호화합니다. 이 작업은 `PasswordEncryptPDF` 작업을 기반으로 합니다. 암호로 암호화된 PDF 문서는 `outDoc` 프로세스 변수에 반환됩니다.

>[!NOTE]
>
>MTOM 지원이 AEM Forms 버전 9에서 추가되었습니다.

>[!NOTE]
>
>MTOM 전송 프로토콜을 사용하는 JAX WS 기반 애플리케이션은 전송 및 수신 데이터의 25MB로 제한됩니다. 이 제한은 JAX-WS의 버그로 인한 것입니다. 전송 및 수신한 파일의 크기가 25MB를 초과하는 경우 MTOM 대신 SwaRef 전송 프로토콜을 사용합니다. 그렇지 않으면 `OutOfMemory` 예외가 발생할 수 있습니다.

여기에서 설명하는 내용은 Microsoft .NET 프로젝트 내에서 MTOM을 사용하여 AEM Forms 서비스를 호출하는 것입니다. 사용되는 .NET 프레임워크는 3.5이고 개발 환경은 Visual Studio 2008입니다. 웹 서비스 개선 사항(WSE)이 개발 컴퓨터에 설치되어 있는 경우 해당 기능을 제거합니다. .NET 3.5 프레임워크는 WCF(Windows Communication Foundation)라는 SOAP 프레임워크를 지원합니다. MTOM을 사용하여 AEM Forms을 호출하면 WCF(WSE 아님)만 지원됩니다.

### MTOM {#creating-a-net-project-that-invokes-a-service-using-mtom}을 사용하여 서비스를 호출하는 .NET 프로젝트 만들기

웹 서비스를 사용하여 AEM Forms 서비스를 호출할 수 있는 Microsoft .NET 프로젝트를 만들 수 있습니다. 먼저 Visual Studio 2008을 사용하여 Microsoft .NET 프로젝트를 만듭니다. AEM Forms 서비스를 호출하려면 프로젝트 내에서 호출할 AEM Forms 서비스에 대한 서비스 참조를 만듭니다. 서비스 참조를 만들 때 AEM Forms 서비스에 대한 URL을 지정합니다.

```java
 http://localhost:8080/soap/services/MyApplication/EncryptDocument?WSDL&lc_version=9.0.1
```

`localhost`을(를) AEM Forms을 호스팅하는 J2EE 응용 프로그램 서버의 IP 주소로 바꿉니다. 호출할 AEM Forms 서비스의 이름으로 `MyApplication/EncryptDocument`을(를) 바꿉니다. 예를 들어 Rights Management 작업을 호출하려면 다음을 지정합니다.

`http://localhost:8080/soap/services/RightsManagementService?WSDL&lc_version=9.0.1`

`lc_version` 옵션은 MTOM과 같은 AEM Forms 기능을 사용할 수 있도록 합니다. `lc_version` 옵션을 지정하지 않으면 MTOM을 사용하여 AEM Forms을 호출할 수 없습니다.

서비스 참조를 만든 후 AEM Forms 서비스와 관련된 데이터 유형을 .NET 프로젝트 내에서 사용할 수 있습니다. AEM Forms 서비스를 호출하는 .NET 프로젝트를 만들려면 다음 단계를 수행하십시오.

1. Microsoft Visual Studio 2008을 사용하여 .NET 프로젝트를 만듭니다.
1. **프로젝트** 메뉴에서 **서비스 참조 추가**&#x200B;를 선택합니다.
1. **주소** 대화 상자에서 AEM Forms 서비스에 대한 WSDL을 지정합니다. 예,

   ```java
    http://localhost:8080/soap/services/MyApplication/EncryptDocument?WSDL&lc_version=9.0.1
   ```

1. **이동**&#x200B;을 클릭한 다음 **확인**&#x200B;을 클릭합니다.

### .NET 프로젝트 {#invoking-a-service-using-mtom-in-a-net-project}에서 MTOM을 사용하여 서비스 호출

비보안 PDF 문서를 승인하고 암호로 암호화된 PDF 문서를 반환하는 `MyApplication/EncryptDocument` 프로세스를 고려합니다. MTOM을 사용하여 `MyApplication/EncryptDocument` 프로세스(Workbench에 내장되어 있음)를 호출하려면 다음 단계를 수행하십시오.

1. Microsoft .NET 프로젝트를 만듭니다.
1. 기본 생성자를 사용하여 `MyApplication_EncryptDocumentClient` 객체를 만듭니다.
1. `System.ServiceModel.EndpointAddress` 생성자를 사용하여 `MyApplication_EncryptDocumentClient.Endpoint.Address` 객체를 만듭니다. WSDL을 지정하는 문자열 값을 AEM Forms 서비스 및 인코딩 유형으로 전달합니다.

   ```java
    https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?blob=mtom
   ```

   `lc_version` 특성을 사용할 필요가 없습니다. 이 속성은 서비스 참조를 만들 때 사용됩니다. 그러나 `?blob=mtom`을(를) 지정해야 합니다.

   >[!NOTE]
   >
   >AEM Forms을 호스팅하는 J2EE 응용 프로그램 서버의 IP 주소로 `hiro-xp` *을(를) 바꿉니다.*

1. `EncryptDocumentClient.Endpoint.Binding` 데이터 멤버의 값을 가져와 `System.ServiceModel.BasicHttpBinding` 개체를 만듭니다. 반환 값을 `BasicHttpBinding`으로 캐스팅합니다.
1. `System.ServiceModel.BasicHttpBinding` 개체의 `MessageEncoding` 데이터 멤버를 `WSMessageEncoding.Mtom`로 설정합니다. 이 값을 사용하면 MTOM이 사용됩니다.
1. 다음 작업을 수행하여 기본 HTTP 인증을 활성화합니다.

   * AEM 양식 사용자 이름을 데이터 멤버 `MyApplication_EncryptDocumentClient.ClientCredentials.UserName.UserName`에 할당합니다.
   * 해당 암호 값을 데이터 멤버 `MyApplication_EncryptDocumentClient.ClientCredentials.UserName.Password`에 할당합니다.
   * 데이터 멤버 `BasicHttpBindingSecurity.Transport.ClientCredentialType`에 상수 값 `HttpClientCredentialType.Basic`을 할당합니다.
   * 데이터 멤버 `BasicHttpBindingSecurity.Security.Mode`에 상수 값 `BasicHttpSecurityMode.TransportCredentialOnly`을 할당합니다.

   다음 코드 예는 이러한 작업을 보여줍니다.

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

1. 생성자를 사용하여 `BLOB` 객체를 만듭니다. `BLOB` 개체는 `MyApplication/EncryptDocument` 프로세스에 전달할 PDF 문서를 저장하는 데 사용됩니다.
1. 생성자를 호출하여 `System.IO.FileStream` 객체를 만듭니다. PDF 문서의 파일 위치와 파일을 열 모드를 나타내는 문자열 값을 전달합니다.
1. `System.IO.FileStream` 객체의 내용을 저장하는 바이트 배열을 만듭니다. `System.IO.FileStream` 객체의 `Length` 속성을 가져와 바이트 배열의 크기를 결정할 수 있습니다.
1. `System.IO.FileStream` 객체의 `Read` 메서드를 호출하여 바이트 배열을 스트림 데이터로 채웁니다. 바이트 배열, 시작 위치 및 읽을 스트림 길이를 전달합니다.
1. 바이트 배열의 내용으로 `MTOM` 데이터 멤버를 할당하여 `BLOB` 객체를 채웁니다.
1. `MyApplication_EncryptDocumentClient` 객체의 `invoke` 메서드를 호출하여 `MyApplication/EncryptDocument` 프로세스를 호출합니다. PDF 문서를 포함하는 `BLOB` 개체를 전달합니다. 이 프로세스는 `BLOB` 개체 내에서 암호화된 PDF 문서를 반환합니다.
1. 생성자를 호출하고 보안 PDF 문서의 파일 위치를 나타내는 문자열 값을 전달하여 `System.IO.FileStream` 객체를 만듭니다.
1. `invoke` 메서드에서 반환된 `BLOB` 객체의 데이터 내용을 저장하는 바이트 배열을 만듭니다. `BLOB` 객체의 `MTOM` 데이터 멤버 값을 가져와 바이트 배열을 채웁니다.
1. 생성자를 호출하고 `System.IO.FileStream` 객체를 전달하여 `System.IO.BinaryWriter` 객체를 만듭니다.
1. `System.IO.BinaryWriter` 객체의 `Write` 메서드를 호출하고 바이트 배열을 전달하여 바이트 배열의 내용을 PDF 파일에 기록합니다.

>[!NOTE]
>
>대부분의 AEM Forms 서비스 작업은 MTOM 빠른 시작을 갖습니다. 서비스의 해당 빠른 시작 섹션에서 이러한 빠른 시작을 볼 수 있습니다. 예를 들어 출력 빠른 시작 섹션을 보려면 [출력 서비스 API 빠른 시작](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)을 참조하십시오.

**참고 항목**

[빠른 시작:.NET 프로젝트에서 MTOM을 사용하여 서비스 호출](/help/forms/developing/invocation-api-quick-starts.md#quick-start-invoking-a-service-using-mtom-in-a-net-project)

[웹 서비스를 사용하여 여러 서비스 액세스](#accessing-multiple-services-using-web-services)

[인간 중심의 오랜 프로세스를 호출하는 ASP.NET 웹 응용 프로그램 만들기](/help/forms/developing/invoking-human-centric-long-lived.md#creating-an-asp-net-web-application-that-invokes-a-human-centric-long-lived-process)

## SwaRef {#invoking-aem-forms-using-swaref}을(를) 사용하여 AEM Forms 호출

SwaRef를 사용하여 AEM Forms 서비스를 호출할 수 있습니다. `wsi:swaRef` XML 요소의 내용은 첨부 파일에 대한 참조를 저장하는 SOAP 본문 내에 첨부 파일로 전송됩니다. SwaRef를 사용하여 Forms 서비스를 호출할 때 JAX-WS(XML Web Services)용 Java API를 사용하여 Java 프록시 클래스를 만드십시오. ([XML Web Services용 Java API](https://jax-ws.dev.java.net/jax-ws-ea3/docs/mtom-swaref.html)를 참조하십시오.)

여기서 논의는 SwaRef를 사용하여 `MyApplication/EncryptDocument`이라는 짧은 Forms 프로세스를 호출하는 것입니다.

>[!NOTE]
>
>이 프로세스는 기존 AEM Forms 프로세스를 기반으로 하지 않습니다. 코드 예제를 따라 하려면 Workbench를 사용하여 `MyApplication/EncryptDocument` 프로세스를 만듭니다. ([Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63) 사용 참조)

이 프로세스가 호출되면 다음 작업을 수행합니다.

1. 프로세스에 전달된 보안되지 않은 PDF 문서를 가져옵니다. 이 작업은 `SetValue` 작업을 기반으로 합니다. 이 프로세스의 입력 매개 변수는 `inDoc`이라는 `document` 프로세스 변수입니다.
1. 암호로 PDF 문서를 암호화합니다. 이 작업은 `PasswordEncryptPDF` 작업을 기반으로 합니다. 암호로 암호화된 PDF 문서는 `outDoc` 프로세스 변수에 반환됩니다.

>[!NOTE]
>
>AEM Forms에 SwaRef 지원 추가

아래의 논의는 Java 클라이언트 응용 프로그램 내에서 SwaRef를 사용하여 Forms 서비스를 호출하는 방법에 대한 것입니다. Java 응용 프로그램은 JAX-WS를 사용하여 만든 프록시 클래스를 사용합니다.

### SwaRef {#invoke-a-service-using-jax-ws-library-files-that-use-swaref}을(를) 사용하는 JAX-WS 라이브러리 파일을 사용하여 서비스를 호출합니다.

JAX-WS 및 SwaRef를 사용하여 만든 Java 프록시 파일을 사용하여 `MyApplication/EncryptDocument` 프로세스를 호출하려면 다음 단계를 수행하십시오.

1. `MyApplication/EncryptDocument` 서비스 WSDL을 사용하는 JAX-WS를 사용하여 Java 프록시 클래스를 만듭니다. 다음 WSDL 끝점을 사용합니다.

   ```java
    https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?WSDL&lc_version=9.0.1
   ```

   자세한 내용은 [JAX-WS](#creating-java-proxy-classes-using-jax-ws)를 사용하여 Java 프록시 클래스 만들기를 참조하십시오.

   >[!NOTE]
   >
   >AEM Forms을 호스팅하는 J2EE 응용 프로그램 서버의 IP 주소로 `hiro-xp` *을(를) 바꿉니다.*

1. JAX-WS를 사용하여 만든 Java 프록시 클래스를 JAR 파일로 패키지화합니다.
1. 다음 경로에 있는 Java 프록시 JAR 파일과 JAR 파일을 포함합니다.

   &lt;install Directory=&quot;&quot;>\Adobe\Adobe_Experience_Manager_forms\sdk\client-libs\thirdparty

   을 Java 클라이언트 프로젝트의 클래스 경로에 추가합니다.

1. 생성자를 사용하여 `MyApplicationEncryptDocumentService` 객체를 만듭니다.
1. `MyApplicationEncryptDocumentService` 객체의 `getEncryptDocument` 메서드를 호출하여 `MyApplicationEncryptDocument` 객체를 만듭니다.
1. 다음 데이터 멤버에 값을 할당하여 AEM Forms을 호출하는 데 필요한 연결 값을 설정합니다.

   * WSDL 끝점과 인코딩 유형을 `javax.xml.ws.BindingProvider` 객체의 `ENDPOINT_ADDRESS_PROPERTY` 필드에 할당합니다. SwaRef 인코딩을 사용하여 `MyApplication/EncryptDocument` 서비스를 호출하려면 다음 URL 값을 지정합니다.

      ` https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?blob=swaref`

   * AEM 양식 사용자를 `javax.xml.ws.BindingProvider` 개체의 `USERNAME_PROPERTY` 필드에 할당합니다.
   * 해당 암호 값을 `javax.xml.ws.BindingProvider` 개체의 `PASSWORD_PROPERTY` 필드에 할당합니다.

   다음 코드 예제에서는 이 응용 프로그램 논리를 보여 줍니다.

   ```java
    //Set connection values required to invoke AEM Forms
    String url = "https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?blob=swaref";
    String username = "administrator";
    String password = "password";
    ((BindingProvider) encryptDocClient).getRequestContext().put(BindingProvider.ENDPOINT_ADDRESS_PROPERTY, url);
    ((BindingProvider) encryptDocClient).getRequestContext().put(BindingProvider.USERNAME_PROPERTY, username);
    ((BindingProvider) encryptDocClient).getRequestContext().put(BindingProvider.PASSWORD_PROPERTY, password);
   ```

1. 생성자를 사용하여 `java.io.File` 개체를 만들어 `MyApplication/EncryptDocument` 프로세스로 전송할 PDF 문서를 검색합니다. PDF 문서의 위치를 지정하는 문자열 값을 전달합니다.
1. `FileDataSource` 생성자를 사용하여 `javax.activation.DataSource` 객체를 만듭니다. `java.io.File` 개체를 전달합니다.
1. 생성자를 사용하여 `javax.activation.DataHandler` 개체를 만들고 `javax.activation.DataSource` 개체를 전달합니다.
1. 생성자를 사용하여 `BLOB` 객체를 만듭니다.
1. `setSwaRef` 메서드를 호출하고 `javax.activation.DataHandler` 개체를 전달하여 `BLOB` 개체를 채웁니다.
1. `MyApplicationEncryptDocument` 개체의 `invoke` 메서드를 호출하고 PDF 문서가 포함된 `BLOB` 개체를 전달하여 `MyApplication/EncryptDocument` 프로세스를 호출합니다. invoke 메서드는 암호화된 PDF 문서를 포함하는 `BLOB` 객체를 반환합니다.
1. `BLOB` 객체의 `getSwaRef` 메서드를 호출하여 `javax.activation.DataHandler` 객체를 채웁니다.
1. `javax.activation.DataHandler` 객체의 `getInputStream` 메서드를 호출하여 `javax.activation.DataHandler` 객체를 `java.io.InputSteam` 인스턴스로 변환합니다.
1. `java.io.InputSteam` 인스턴스를 암호화된 PDF 문서를 나타내는 PDF 파일에 씁니다.

>[!NOTE]
>
>대부분의 AEM Forms 서비스 작업에는 SwaRef 빠른 시작 기능이 있습니다. 서비스의 해당 빠른 시작 섹션에서 이러한 빠른 시작을 볼 수 있습니다. 예를 들어 출력 빠른 시작 섹션을 보려면 [출력 서비스 API 빠른 시작](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)을 참조하십시오.

**참고 항목**

[빠른 시작:Java 프로젝트에서 SwaRef를 사용하여 서비스 호출](/help/forms/developing/invocation-api-quick-starts.md#quick-start-invoking-a-service-using-swaref-in-a-java-project)

## HTTP {#invoking-aem-forms-using-blob-data-over-http}를 통해 BLOB 데이터를 사용하여 AEM Forms 호출

웹 서비스를 사용하여 AEM Forms 서비스를 호출하고 HTTP를 통해 BLOB 데이터를 전달할 수 있습니다. HTTP를 통해 BLOB 데이터를 전달하는 것은 base64 인코딩, DIME 또는 MIME을 사용하는 대신 다른 방법입니다. 예를 들어 DIME 또는 MIME을 지원하지 않는 Web Service Enhancement 3.0을 사용하는 Microsoft .NET 프로젝트에서 HTTP를 통해 데이터를 전달할 수 있습니다. HTTP를 통해 BLOB 데이터를 사용하는 경우 AEM Forms 서비스를 호출하기 전에 입력 데이터가 업로드됩니다.

&quot;HTTP를 통해 BLOB 데이터를 사용하여 AEM Forms 호출&quot;에서는 BLOB 데이터를 HTTP를 통해 전달하여 `MyApplication/EncryptDocument`이라는 AEM Forms이 짧은 프로세스를 호출하는 방법을 설명합니다.

>[!NOTE]
>
>이 프로세스는 기존 AEM Forms 프로세스를 기반으로 하지 않습니다. 코드 예제를 따라 하려면 Workbench를 사용하여 `MyApplication/EncryptDocument` 프로세스를 만듭니다. ([Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63) 사용 참조)

이 프로세스가 호출되면 다음 작업을 수행합니다.

1. 프로세스에 전달된 보안되지 않은 PDF 문서를 가져옵니다. 이 작업은 `SetValue` 작업을 기반으로 합니다. 이 프로세스의 입력 매개 변수는 `inDoc`이라는 `document` 프로세스 변수입니다.
1. 암호로 PDF 문서를 암호화합니다. 이 작업은 `PasswordEncryptPDF` 작업을 기반으로 합니다. 암호로 암호화된 PDF 문서는 `outDoc` 프로세스 변수에 반환됩니다.

>[!NOTE]
>
>SOAP를 사용한 AEM Forms 호출에 익숙해지는 것이 좋습니다. ([웹 서비스를 사용하여 AEM Forms 호출](#invoking-aem-forms-using-web-services)을 참조하십시오.)

### HTTP {#creating-a-net-client-assembly-that-uses-data-over-http}를 통해 데이터를 사용하는 .NET 클라이언트 어셈블리 만들기

HTTP를 통해 데이터를 사용하는 클라이언트 어셈블리를 만들려면 [Base64 인코딩을 사용하여 AEM Forms 호출](#invoking-aem-forms-using-base64-encoding)에 지정된 프로세스를 따릅니다. 그러나 프록시 클래스의 URL을 `?blob=base64` 대신 `?blob=http`을 포함하도록 수정합니다. 이 작업을 수행하면 데이터가 HTTP를 통해 전달됩니다. 프록시 클래스에서 다음 코드 행을 찾습니다.

```java
 "http://localhost:8080/soap/services/MyApplication/EncryptDocument";
```

를 다음과 같이 변경합니다.

```java
 "http://localhost:8080/soap/services/MyApplication/EncryptDocument?blob=http";
```

**.NET clientMyApplication/EncryptDocument 어셈블리 참조**

클라이언트 응용 프로그램을 개발할 컴퓨터에 새 .NET 클라이언트 어셈블리를 배치합니다. .NET 클라이언트 어셈블리를 디렉토리에 배치한 후 프로젝트에서 참조할 수 있습니다. 프로젝트에서 `System.Web.Services` 라이브러리를 참조합니다. 이 라이브러리를 참조하지 않으면 .NET 클라이언트 어셈블리를 사용하여 서비스를 호출할 수 없습니다.

1. **프로젝트** 메뉴에서 **참조 추가**&#x200B;를 선택합니다.
1. **.NET** 탭을 클릭합니다.
1. **찾아보기**&#x200B;를 클릭하고 DocumentService.dll 파일을 찾습니다.
1. **선택**&#x200B;을 클릭한 다음 **확인**&#x200B;을 클릭합니다.

**HTTP를 통해 BLOB 데이터를 사용하는 .NET 클라이언트 어셈블리를 사용하여 서비스 호출**

HTTP를 통해 데이터를 사용하는 .NET 클라이언트 어셈블리를 사용하여 `MyApplication/EncryptDocument` 서비스(Workbench에 내장되어 있음)를 호출할 수 있습니다. `MyApplication/EncryptDocument` 서비스를 호출하려면 다음 단계를 수행하십시오.

1. .NET 클라이언트 어셈블리를 만듭니다.
1. Microsoft .NET 클라이언트 어셈블리를 참조하십시오. 클라이언트 Microsoft .NET 프로젝트를 만듭니다. 클라이언트 프로젝트에서 Microsoft .NET 클라이언트 어셈블리를 참조합니다. `System.Web.Services`도 참조합니다.
1. Microsoft .NET 클라이언트 어셈블리를 사용하여 기본 생성자를 호출하여 `MyApplication_EncryptDocumentService` 객체를 만듭니다.
1. `MyApplication_EncryptDocumentService` 개체의 `Credentials` 속성을 `System.Net.NetworkCredential` 개체로 설정합니다. `System.Net.NetworkCredential` 생성자 내에서 AEM 양식 사용자 이름과 해당 암호를 지정합니다. .NET 클라이언트 응용 프로그램이 AEM Forms과 SOAP 메시지를 성공적으로 교환할 수 있도록 하려면 인증 값을 설정합니다.
1. 생성자를 사용하여 `BLOB` 객체를 만듭니다. `BLOB` 개체는 `MyApplication/EncryptDocument` 프로세스에 데이터를 전달하는 데 사용됩니다.
1. `MyApplication/EncryptDocument` 서비스에 전달할 PDF 문서의 URI 위치를 지정하는 `BLOB` 객체의 `remoteURL` 데이터 멤버에 문자열 값을 할당합니다.
1. `MyApplication_EncryptDocumentService` 객체의 `invoke` 메서드를 호출하고 `BLOB` 객체를 전달하여 `MyApplication/EncryptDocument` 프로세스를 호출합니다. 이 프로세스는 `BLOB` 개체 내에서 암호화된 PDF 문서를 반환합니다.
1. 생성자를 사용하여 `System.UriBuilder` 개체를 만들고 반환된 `BLOB` 개체의 `remoteURL` 데이터 멤버의 값을 전달합니다.
1. `System.UriBuilder` 개체를 `System.IO.Stream` 개체로 변환합니다. 이 목록 다음에 나오는 C# 빠른 시작에서는 이 작업을 수행하는 방법을 보여 줍니다.
1. 바이트 배열을 만들어 `System.IO.Stream` 개체에 있는 데이터로 채웁니다.
1. 생성자를 호출하고 `System.IO.FileStream` 객체를 전달하여 `System.IO.BinaryWriter` 객체를 만듭니다.
1. `System.IO.BinaryWriter` 객체의 `Write` 메서드를 호출하고 바이트 배열을 전달하여 바이트 배열 내용을 PDF 파일에 씁니다.

### HTTP {#invoking-a-service-using-java-proxy-classes-and-blob-data-over-http}를 통해 Java 프록시 클래스와 BLOB 데이터를 사용하는 서비스 호출

HTTP를 통해 Java 프록시 클래스와 BLOB 데이터를 사용하여 AEM Forms 서비스를 호출할 수 있습니다. Java 프록시 클래스를 사용하여 `MyApplication/EncryptDocument` 서비스를 호출하려면 다음 단계를 수행하십시오.

1. `MyApplication/EncryptDocument` 서비스 WSDL을 사용하는 JAX-WS를 사용하여 Java 프록시 클래스를 만듭니다. 다음 WSDL 끝점을 사용합니다.

   ```java
    https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?WSDL&lc_version=9.0.1
   ```

   자세한 내용은 [JAX-WS](#creating-java-proxy-classes-using-jax-ws)를 사용하여 Java 프록시 클래스 만들기를 참조하십시오.

   >[!NOTE]
   >
   >AEM Forms을 호스팅하는 J2EE 응용 프로그램 서버의 IP 주소로 `hiro-xp` *을(를) 바꿉니다.*

1. JAX-WS를 사용하여 만든 Java 프록시 클래스를 JAR 파일로 패키지화합니다.
1. 다음 경로에 있는 Java 프록시 JAR 파일과 JAR 파일을 포함합니다.

   &lt;install Directory=&quot;&quot;>\Adobe\Adobe_Experience_Manager_forms\sdk\client-libs\thirdparty

   을 Java 클라이언트 프로젝트의 클래스 경로에 추가합니다.

1. 생성자를 사용하여 `MyApplicationEncryptDocumentService` 객체를 만듭니다.
1. `MyApplicationEncryptDocumentService` 객체의 `getEncryptDocument` 메서드를 호출하여 `MyApplicationEncryptDocument` 객체를 만듭니다.
1. 다음 데이터 멤버에 값을 할당하여 AEM Forms을 호출하는 데 필요한 연결 값을 설정합니다.

   * WSDL 끝점과 인코딩 유형을 `javax.xml.ws.BindingProvider` 객체의 `ENDPOINT_ADDRESS_PROPERTY` 필드에 할당합니다. HTTP 인코딩을 통해 BLOB을 사용하여 `MyApplication/EncryptDocument` 서비스를 호출하려면 다음 URL 값을 지정합니다.

      `https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?blob=http`

   * AEM 양식 사용자를 `javax.xml.ws.BindingProvider` 개체의 `USERNAME_PROPERTY` 필드에 할당합니다.
   * 해당 암호 값을 `javax.xml.ws.BindingProvider` 개체의 `PASSWORD_PROPERTY` 필드에 할당합니다.

   다음 코드 예제에서는 이 응용 프로그램 논리를 보여 줍니다.

   ```java
    //Set connection values required to invoke AEM Forms
    String url = "https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?blob=http";
    String username = "administrator";
    String password = "password";
    ((BindingProvider) encryptDocClient).getRequestContext().put(BindingProvider.ENDPOINT_ADDRESS_PROPERTY, url);
    ((BindingProvider) encryptDocClient).getRequestContext().put(BindingProvider.USERNAME_PROPERTY, username);
    ((BindingProvider) encryptDocClient).getRequestContext().put(BindingProvider.PASSWORD_PROPERTY, password);
   ```

1. 생성자를 사용하여 `BLOB` 객체를 만듭니다.
1. `setRemoteURL` 메서드를 호출하여 `BLOB` 객체를 채웁니다. `MyApplication/EncryptDocument` 서비스로 전달할 PDF 문서의 URI 위치를 지정하는 문자열 값을 전달합니다.
1. `MyApplicationEncryptDocument` 개체의 `invoke` 메서드를 호출하고 PDF 문서가 포함된 `BLOB` 개체를 전달하여 `MyApplication/EncryptDocument` 프로세스를 호출합니다. 이 프로세스는 `BLOB` 개체 내에서 암호화된 PDF 문서를 반환합니다.
1. 바이트 배열을 만들어 암호화된 PDF 문서를 나타내는 데이터 스트림을 저장합니다. `BLOB` 객체의 `getRemoteURL` 메서드를 호출합니다. `invoke` 메서드에서 반환되는 `BLOB` 객체를 사용합니다.
1. 생성자를 사용하여 `java.io.File` 객체를 만듭니다. 이 개체는 암호화된 PDF 문서를 나타냅니다.
1. 생성자를 사용하여 `java.io.FileOutputStream` 개체를 만들고 `java.io.File` 개체를 전달합니다.
1. `java.io.FileOutputStream` 객체의 `write` 메서드를 호출합니다. 암호화된 PDF 문서를 나타내는 데이터 스트림이 포함된 바이트 배열을 전달합니다.

## DIME {#invoking-aem-forms-using-dime}을(를) 사용하여 AEM Forms 호출

첨부 파일이 있는 SOAP를 사용하여 AEM Forms 서비스를 호출할 수 있습니다. AEM Forms은 MIME 및 DIME 웹 서비스 표준을 모두 지원합니다. DIME를 사용하면 첨부 파일을 인코딩하는 대신 호출 요청과 함께 PDF 문서와 같은 이진 첨부 파일을 보낼 수 있습니다. *DIME*&#x200B;를 사용하여 AEM Forms 호출 섹션에서는 DIME를 사용하여 `MyApplication/EncryptDocument`라는 짧은 AEM Forms 프로세스를 호출하는 방법에 대해 설명합니다.

이 프로세스가 호출되면 다음 작업을 수행합니다.

1. 프로세스에 전달된 보안되지 않은 PDF 문서를 가져옵니다. 이 작업은 `SetValue` 작업을 기반으로 합니다. 이 프로세스의 입력 매개 변수는 `inDoc`이라는 `document` 프로세스 변수입니다.
1. 암호로 PDF 문서를 암호화합니다. 이 작업은 `PasswordEncryptPDF` 작업을 기반으로 합니다. 암호로 암호화된 PDF 문서는 `outDoc` 프로세스 변수에 반환됩니다.

이 프로세스는 기존 AEM Forms 프로세스를 기반으로 하지 않습니다. 코드 예제를 따라 하려면 워크벤치를 사용하여 `MyApplication/EncryptDocument` 프로세스를 만듭니다. ([Workbench](https://www.adobe.com/go/learn_aemforms_workbench_63) 사용 참조)

>[!NOTE]
>
>DIME를 사용한 AEM Forms 서비스 작업 호출은 더 이상 사용되지 않습니다. MTOM을 사용하는 것이 좋습니다. (MTOM](#invoking-aem-forms-using-mtom)을 사용하여 AEM Forms 호출 참조)[

### DIME {#creating-a-net-project-that-uses-dime}을 사용하는 .NET 프로젝트 만들기

DIME를 사용하여 Forms 서비스를 호출할 수 있는 .NET 프로젝트를 만들려면 다음 작업을 수행하십시오.

* 개발 컴퓨터에 웹 서비스 개선 사항 2.0을 설치합니다.
* .NET 프로젝트 내에서 FormsAEM Forms 서비스에 대한 웹 참조를 만듭니다.

**웹 서비스 개선 사항 설치 2.0**

개발 컴퓨터에 웹 서비스 개선 사항 2.0을 설치하고 Microsoft Visual Studio .NET과 통합합니다. [Microsoft 다운로드 센터에서 웹 서비스 개선 사항 2.0을 다운로드할 수 있습니다.](https://www.microsoft.com/downloads/search.aspx)

이 웹 페이지에서 웹 서비스 개선 사항 2.0을 검색하고 개발 컴퓨터에 다운로드합니다. 이 다운로드에는 Microsoft WSE 2.0 SPI.msi라는 파일이 컴퓨터에 저장됩니다. 설치 프로그램을 실행하고 온라인 지침을 따릅니다.

>[!NOTE]
>
>웹 서비스 개선 사항 2.0은 DIME를 지원합니다. 웹 서비스 개선 사항 2.0에서 작업할 때 지원되는 Microsoft Visual Studio 버전은 2003입니다. 웹 서비스 개선 사항 3.0에서는 DIME를 지원하지 않습니다.하지만 MTOM을 지원합니다.

**AEM Forms 서비스에 대한 웹 참조 만들기**

개발 컴퓨터에 웹 서비스 개선 사항 2.0을 설치하고 Microsoft .NET 프로젝트를 만든 후 Forms 서비스에 대한 웹 참조를 만듭니다. 예를 들어, `MyApplication/EncryptDocument` 프로세스에 대한 웹 참조를 만들고 Forms이 로컬 컴퓨터에 설치되어 있다고 가정하려면 다음 URL을 지정합니다.

```java
     http://localhost:8080/soap/services/MyApplication/EncryptDocument?WSDL
```

웹 참조를 만든 후 .NET 프로젝트 내에서 사용할 수 있는 프록시 데이터 유형은 다음과 같습니다.`EncryptDocumentService` 및 `EncryptDocumentServiceWse`. DIME를 사용하여 `MyApplication/EncryptDocument` 프로세스를 호출하려면 `EncryptDocumentServiceWse` 유형을 사용합니다.

>[!NOTE]
>
>Forms 서비스에 대한 웹 참조를 만들기 전에 프로젝트에서 웹 서비스 개선 사항 2.0을 참조하는지 확인하십시오. (웹 서비스 개선 사항 2.0 설치&quot;를 참조하십시오.)

**WSE 라이브러리 참조**

1. 프로젝트 메뉴에서 참조 추가를 선택합니다.
1. 참조 추가 대화 상자에서 Microsoft.Web.Services2.dll을 선택합니다.
1. System.Web.Services.dll을 선택합니다.
1. 선택을 클릭한 다음 확인을 클릭합니다.

**Forms 서비스에 대한 웹 참조 만들기**

1. 프로젝트 메뉴에서 웹 참조 추가를 선택합니다.
1. [URL] 대화 상자에서 Forms 서비스의 URL을 지정합니다.
1. 이동을 클릭한 다음 참조 추가를 클릭합니다.

>[!NOTE]
>
>.NET 프로젝트에서 WSE 라이브러리를 사용할 수 있도록 설정해야 합니다. 프로젝트 탐색기에서 프로젝트 이름을 마우스 오른쪽 단추로 클릭하고 WSE 2.0 활성화를 선택합니다. 나타나는 대화 상자의 확인란이 선택되어 있는지 확인합니다.

**.NET 프로젝트에서 DIME를 사용하여 서비스 호출**

DIME를 사용하여 Forms 서비스를 호출할 수 있습니다. 비보안 PDF 문서를 승인하고 암호로 암호화된 PDF 문서를 반환하는 `MyApplication/EncryptDocument` 프로세스를 고려합니다. DIME를 사용하여 `MyApplication/EncryptDocument` 프로세스를 호출하려면 다음 단계를 수행하십시오.

1. DIME를 사용하여 Forms 서비스를 호출할 수 있는 Microsoft .NET 프로젝트를 만듭니다. 웹 서비스 개선 사항 2.0을 포함하고 AEM Forms 서비스에 대한 웹 참조를 만들어야 합니다.
1. `MyApplication/EncryptDocument` 프로세스에 대한 웹 참조를 설정한 후 기본 생성자를 사용하여 `EncryptDocumentServiceWse` 개체를 만듭니다.
1. AEM 양식 사용자 이름 및 암호 값을 지정하는 `EncryptDocumentServiceWse` 개체의 `Credentials` 데이터 멤버를 `System.Net.NetworkCredential` 값으로 설정합니다.
1. 해당 생성자를 사용하고 다음 값을 전달하여 `Microsoft.Web.Services2.Dime.DimeAttachment` 객체를 만듭니다.

   * GUID 값을 지정하는 문자열 값입니다. `System.Guid.NewGuid.ToString` 메서드를 호출하여 GUID 값을 얻을 수 있습니다.
   * 컨텐츠 유형을 지정하는 문자열 값입니다. 이 프로세스에는 PDF 문서가 필요하므로 `application/pdf`을(를) 지정합니다.
   * `TypeFormat` 열거형 값입니다. 지정 `TypeFormat.MediaType`.
   * AEM Forms 프로세스로 전달할 PDF 문서의 위치를 지정하는 문자열 값입니다.

1. 생성자를 사용하여 `BLOB` 객체를 만듭니다.
1. `Microsoft.Web.Services2.Dime.DimeAttachment` 개체의 `Id` 데이터 멤버 값을 `BLOB` 개체의 `attachmentID` 데이터 멤버에 할당하여 DIME 첨부 파일을 `BLOB` 개체에 추가합니다.
1. `EncryptDocumentServiceWse.RequestSoapContext.Attachments.Add` 메서드를 호출하고 `Microsoft.Web.Services2.Dime.DimeAttachment` 개체를 전달합니다.
1. `EncryptDocumentServiceWse` 객체의 `invoke` 메서드를 호출하고 DIME 첨부 파일이 포함된 `BLOB` 객체를 전달하여 `MyApplication/EncryptDocument` 프로세스를 호출합니다. 이 프로세스는 `BLOB` 개체 내에서 암호화된 PDF 문서를 반환합니다.
1. 반환된 `BLOB` 개체의 `attachmentID` 데이터 구성원의 값을 가져와 첨부 식별자 값을 가져옵니다.
1. `EncryptDocumentServiceWse.ResponseSoapContext.Attachments`에 있는 첨부 파일을 반복하여 첨부 ID 값을 사용하여 암호화된 PDF 문서를 가져옵니다.
1. `Attachment` 개체의 `Stream` 데이터 멤버의 값을 가져와 `System.IO.Stream` 개체를 가져옵니다.
1. 바이트 배열을 만들고 해당 바이트 배열을 `System.IO.Stream` 객체의 `Read` 메서드에 전달합니다. 이 메서드는 암호화된 PDF 문서를 나타내는 데이터 스트림으로 바이트 배열을 채웁니다.
1. 생성자를 호출하고 PDF 파일 위치를 나타내는 문자열 값을 전달하여 `System.IO.FileStream` 객체를 만듭니다. 이 개체는 암호화된 PDF 문서를 나타냅니다.
1. 생성자를 호출하고 `System.IO.FileStream` 객체를 전달하여 `System.IO.BinaryWriter` 객체를 만듭니다.
1. `System.IO.BinaryWriter` 객체의 `Write` 메서드를 호출하고 바이트 배열을 전달하여 바이트 배열의 내용을 PDF 파일에 기록합니다.

### DIME {#creating-apache-axis-java-proxy-classes-that-use-dime}을 사용하는 Apache 축 Java 프록시 클래스 만들기

Apache Axis WSDL2Java 도구를 사용하여 서비스 WSDL을 Java 프록시 클래스로 변환하여 서비스 작업을 호출할 수 있습니다. Apache Ant를 사용하면 서비스를 호출할 수 있는 AEM Forms 서비스 WSDL에서 축 라이브러리 파일을 생성할 수 있습니다. (Apache Axis](#creating-java-proxy-classes-using-apache-axis)를 사용하여 Java 프록시 클래스 만들기를 참조하십시오.)[

Apache Axis WSDL2Java 도구는 SOAP 요청을 서비스로 보내는 데 사용되는 메서드를 포함하는 JAVA 파일을 생성합니다. 서비스에서 받은 SOAP 요청은 Axis 생성 라이브러리에 의해 디코딩되고 다시 메서드 및 인수로 바뀝니다.

Axis 생성 라이브러리 파일과 DIME를 사용하여 Workbench에 내장된 `MyApplication/EncryptDocument` 서비스를 호출하려면 다음 단계를 수행하십시오.

1. Apache Axis를 사용하여 `MyApplication/EncryptDocument` 서비스 WSDL을 사용하는 Java 프록시 클래스를 만듭니다. (Apache Axis](#creating-java-proxy-classes-using-apache-axis)를 사용하여 Java 프록시 클래스 만들기를 참조하십시오.)[
1. 클래스 경로에 Java 프록시 클래스를 포함합니다.
1. 생성자를 사용하여 `MyApplicationEncryptDocumentServiceLocator` 객체를 만듭니다.
1. 해당 생성자를 사용하고 AEM Forms 서비스 WSDL 정의를 지정하는 문자열 값을 전달하여 `URL` 객체를 만듭니다. SOAP 끝점 URL의 끝에 `?blob=dime`을(를) 지정해야 합니다. 예를 들어

   ```java
    https://hiro-xp:8080/soap/services/MyApplication/EncryptDocument?blob=dime.
   ```

1. 생성자를 호출하고 `MyApplicationEncryptDocumentServiceLocator` 개체 및 `URL` 개체를 전달하여 `EncryptDocumentSoapBindingStub` 개체를 만듭니다.
1. AEM 양식 사용자 이름 및 암호 값은 `EncryptDocumentSoapBindingStub` 개체의 `setUsername` 및 `setPassword` 메서드를 호출하여 설정합니다.

   ```java
    encryptionClientStub.setUsername("administrator");
    encryptionClientStub.setPassword("password");
   ```

1. `java.io.File` 개체를 만들어 `MyApplication/EncryptDocument` 서비스로 보낼 PDF 문서를 검색합니다. PDF 문서 위치를 지정하는 문자열 값을 전달합니다.
1. 생성자를 사용하여 `javax.activation.DataHandler` 개체를 만들고 `javax.activation.FileDataSource` 개체를 전달합니다. `javax.activation.FileDataSource` 개체는 해당 생성자를 사용하여 PDF 문서를 나타내는 `java.io.File` 개체를 전달하여 만들 수 있습니다.
1. 생성자를 사용하여 `org.apache.axis.attachments.AttachmentPart` 개체를 만들고 `javax.activation.DataHandler` 개체를 전달합니다.
1. `EncryptDocumentSoapBindingStub` 객체의 `addAttachment` 메서드를 호출하고 `org.apache.axis.attachments.AttachmentPart` 객체를 전달하여 첨부 파일을 첨부합니다.
1. 생성자를 사용하여 `BLOB` 객체를 만듭니다. `BLOB` 개체의 `setAttachmentID` 메서드를 호출하고 첨부 식별자 값을 전달하여 `BLOB` 개체를 첨부 식별자 값으로 채웁니다. 이 값은 `org.apache.axis.attachments.AttachmentPart` 객체의 `getContentId` 메서드를 호출하여 얻을 수 있습니다.
1. `EncryptDocumentSoapBindingStub` 객체의 `invoke` 메서드를 호출하여 `MyApplication/EncryptDocument` 프로세스를 호출합니다. DIME 첨부 파일이 포함된 `BLOB` 개체를 전달합니다. 이 프로세스는 `BLOB` 개체 내에서 암호화된 PDF 문서를 반환합니다.
1. 반환된 `BLOB` 객체의 `getAttachmentID` 메서드를 호출하여 첨부 식별자 값을 가져옵니다. 이 메서드는 반환된 첨부 파일의 식별자 값을 나타내는 문자열 값을 반환합니다.
1. `EncryptDocumentSoapBindingStub` 개체의 `getAttachments` 메서드를 호출하여 첨부 파일을 검색합니다. 이 메서드는 첨부 파일을 나타내는 `Objects` 배열을 반환합니다.
1. 첨부 파일(`Object` 배열)을 반복하고 첨부 식별자 값을 사용하여 암호화된 PDF 문서를 가져옵니다. 각 요소는 `org.apache.axis.attachments.AttachmentPart` 개체입니다.
1. `org.apache.axis.attachments.AttachmentPart` 객체의 `getDataHandler` 메서드를 호출하여 첨부 파일과 연관된 `javax.activation.DataHandler` 객체를 가져옵니다.
1. `javax.activation.DataHandler` 객체의 `getInputStream` 메서드를 호출하여 `java.io.FileStream` 객체를 가져옵니다.
1. 바이트 배열을 만들고 해당 바이트 배열을 `java.io.FileStream` 객체의 `read` 메서드에 전달합니다. 이 메서드는 암호화된 PDF 문서를 나타내는 데이터 스트림으로 바이트 배열을 채웁니다.
1. 생성자를 사용하여 `java.io.File` 객체를 만듭니다. 이 개체는 암호화된 PDF 문서를 나타냅니다.
1. 생성자를 사용하여 `java.io.FileOutputStream` 개체를 만들고 `java.io.File` 개체를 전달합니다.
1. `java.io.FileOutputStream` 객체의 `write` 메서드를 호출하고 암호화된 PDF 문서를 나타내는 데이터 스트림이 포함된 바이트 배열을 전달합니다.

**참고 항목**

[빠른 시작:Java 프로젝트에서 DIME를 사용하여 서비스 호출](/help/forms/developing/invocation-api-quick-starts.md#quick-start-invoking-a-service-using-dime-in-a-java-project)

## SAML 기반 인증 사용 {#using-saml-based-authentication}

AEM Forms은 서비스를 호출할 때 다양한 웹 서비스 인증 모드를 지원합니다. 하나의 인증 모드는 웹 서비스 호출에서 기본 인증 헤더를 사용하여 사용자 이름과 암호 값을 모두 지정하는 것입니다. AEM Forms은 또한 SAML 어설션 기반 인증을 지원합니다. 클라이언트 응용 프로그램에서 웹 서비스를 사용하여 AEM Forms 서비스를 호출하는 경우 클라이언트 응용 프로그램은 다음 방법 중 하나로 인증 정보를 제공할 수 있습니다.

* 기본 인증의 일부로 자격 증명 전달
* WS-Security 헤더의 일부로 사용자 이름 토큰 전달
* WS-Security 헤더의 일부로 SAML 어설션 전달
* Kerberos 토큰을 WS-Security 헤더의 일부로 전달

AEM Forms은 표준 인증서 기반 인증을 지원하지 않지만 다른 형식으로 인증서 기반 인증을 지원합니다.

>[!NOTE]
>
>AEM Forms을 사용한 프로그래밍에서 웹 서비스 빠른 시작을 통해 인증을 수행할 사용자 이름과 암호 값을 지정합니다.

AEM 양식 사용자의 ID는 비밀 키를 사용하여 서명된 SAML 어설션을 통해 나타낼 수 있습니다. 다음 XML 코드는 SAML 어설션의 예를 보여 줍니다.

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

이 예제 어설션은 관리자 사용자를 위해 발행됩니다. 이 어설션에는 다음과 같은 중요 항목이 포함되어 있습니다.

* 특정 기간 동안 유효합니다.
* 특정 사용자에 대해 발행됩니다.
* 디지털 방식으로 서명됩니다. 따라서 수정은 서명을 손상시킬 수 있습니다.
* 사용자 이름 및 암호와 유사한 사용자 ID의 토큰으로 AEM Forms에 제공될 수 있습니다.

클라이언트 응용 프로그램은 `AuthResult` 객체를 반환하는 모든 AEM Forms AuthenticationManager API에서 어설션을 검색할 수 있습니다. 다음 두 가지 방법 중 하나를 수행하여 `AuthResult` 인스턴스를 얻을 수 있습니다.

* AuthenticationManager API에 노출된 인증 방법을 사용하여 사용자를 인증합니다. 일반적으로 사용자 이름과 암호를 사용합니다.그러나 인증서 인증을 사용할 수도 있습니다.
* `AuthenticationManager.getAuthResultOnBehalfOfUser` 메서드 사용. 이 방법을 사용하면 클라이언트 응용 프로그램이 AEM 양식 사용자의 `AuthResult` 객체를 가져올 수 있습니다.

AEM 양식 사용자는 획득한 SAML 토큰을 사용하여 인증할 수 있습니다. 이 SAML 어설션(xml 조각)은 사용자 인증을 위해 웹 서비스 호출을 사용하여 WS-Security 헤더의 일부로 전송할 수 있습니다. 일반적으로 클라이언트 응용 프로그램은 사용자를 인증했지만 사용자 자격 증명을 저장하지 않았습니다. (또는 사용자가 사용자 이름과 암호를 사용하지 않는 메커니즘을 통해 해당 클라이언트에 로그온했습니다.) 이러한 경우 클라이언트 응용 프로그램은 AEM Forms을 호출하고 특정 사용자를 가장해야 하며, 이 사용자는 AEM Forms을 호출할 수 있습니다.

특정 사용자를 가장하려면 웹 서비스를 사용하여 `AuthenticationManager.getAuthResultOnBehalfOfUser` 메서드를 호출합니다. 이 메서드는 해당 사용자에 대한 SAML 어설션이 포함된 `AuthResult` 인스턴스를 반환합니다.

그런 다음 해당 SAML 어설션을 사용하여 인증이 필요한 모든 서비스를 호출합니다. 이 작업에는 SOAP 헤더의 일부로 어설션을 전송하는 작업이 포함됩니다. 이 어설션으로 웹 서비스 호출이 수행되면 AEM Forms은 해당 어설션으로 사용자를 나타냅니다. 즉, 어설션에 지정된 사용자는 서비스를 호출하는 사용자입니다.

### Apache Axis 클래스 및 SAML 기반 인증 사용 {#using-apache-axis-classes-and-saml-based-authentication}

축 라이브러리를 사용하여 만든 Java 프록시 클래스를 통해 AEM Forms 서비스를 호출할 수 있습니다. (Apache Axis](#creating-java-proxy-classes-using-apache-axis)를 사용하여 Java 프록시 클래스 만들기를 참조하십시오.)[

SAML 기반 인증을 사용하는 AXIS를 사용하는 경우 요청 및 응답 핸들러를 Axis에 등록합니다. Apache Axis는 호출 요청을 AEM Forms으로 보내기 전에 핸들러를 호출합니다. 핸들러를 등록하려면 `org.apache.axis.handlers.BasicHandler`을 확장하는 Java 클래스를 만듭니다.

**축을 사용하여 AssertionHandler 만들기**

`AssertionHandler.java`이라는 다음 Java 클래스는 `org.apache.axis.handlers.BasicHandler`을(를) 확장하는 Java 클래스의 예를 보여 줍니다.

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

Axis에 핸들러를 등록하려면 client-config.wsdd 파일을 만듭니다. 기본적으로 Axis는 이 이름의 파일을 찾습니다. 다음 XML 코드는 client-config.wsdd 파일의 예입니다. 자세한 내용은 축 설명서를 참조하십시오.

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

.NET 클라이언트 어셈블리 및 SAML 기반 인증을 사용하여 Forms 서비스를 호출할 수 있습니다. 이렇게 하려면 웹 서비스 개선 사항 3.0(WSE)을 사용해야 합니다. WSE를 사용하는 .NET 클라이언트 어셈블리를 만드는 방법에 대한 자세한 내용은 [DIME](#creating-a-net-project-that-uses-dime)를 사용하는 .NET 프로젝트 만들기를 참조하십시오.

>[!NOTE]
>
>DIME 섹션은 WSE 2.0을 사용합니다. SAML 기반 인증을 사용하려면 DIME 항목에 지정된 것과 동일한 지침을 따르십시오. 그러나 WSE 2.0을 WSE 3.0으로 바꾸십시오. 개발 컴퓨터에 웹 서비스 개선 사항 3.0을 설치하고 Microsoft Visual Studio .NET과 통합하십시오. [Microsoft 다운로드 센터](https://www.microsoft.com/downloads/search.aspx)에서 웹 서비스 개선 사항 3.0을 다운로드할 수 있습니다.

WSE 아키텍처는 정책, 어설션 및 SecurityToken 데이터 유형을 사용합니다. 웹 서비스 호출을 위해 간단히 정책을 지정합니다. 정책에는 여러 주장이 있을 수 있습니다. 각 어설션에는 필터가 포함될 수 있습니다. 필터는 웹 서비스 호출의 특정 단계에서 호출되며, 이 경우 SOAP 요청을 수정할 수 있습니다. 자세한 내용은 웹 서비스 개선 3.0 설명서를 참조하십시오.

**어설션 및 필터 만들기**

다음 C# 코드 예제에서는 필터 및 어설션 클래스를 만듭니다. 이 코드 예제에서는 SamlAssertionOutputFilter를 만듭니다. 이 필터는 SOAP 요청을 AEM Forms으로 보내기 전에 WSE 프레임워크에서 호출됩니다.

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

SAML 어설션을 나타내는 클래스를 생성합니다. 이 클래스가 수행하는 주요 작업은 데이터 값을 문자열에서 xml로 변환하고 공백을 유지하는 것입니다. 이 어설션 xml은 나중에 SOAP 요청으로 가져옵니다.

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

## 웹 서비스 {#related-considerations-when-using-web-services} 사용 시 관련 고려 사항

웹 서비스를 사용하여 특정 AEM Forms 서비스 작업을 호출할 때 문제가 발생하는 경우가 있습니다. 이 토론의 목적은 이러한 문제를 식별하고 가능한 경우 해결 방법을 제공하는 것이다.

### 서비스 작업을 비동기적으로 호출 {#invoking-service-operations-asynchronously}

PDF 생성 작업의 `htmlToPDF` 작업과 같이 AEM Forms 서비스 작업을 비동기적으로 호출하려고 하면 `SoapFaultException`이 발생합니다. 이 문제를 해결하려면 `ExportPDF_Result` 요소 및 다른 요소를 다른 클래스에 매핑하는 사용자 정의 바인딩 XML 파일을 만드십시오. 다음 XML은 사용자 정의 바인딩 파일을 나타냅니다.

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

JAX-WS를 사용하여 Java 프록시 파일을 만들 때 이 XML 파일을 사용합니다. (JAX-WS](#creating-java-proxy-classes-using-jax-ws)를 사용하여 Java 프록시 클래스 만들기를 참조하십시오.)[

- `b` 명령줄 옵션을 사용하여 JAX-WS 도구(wsimport.exe)를 실행할 때 이 XML 파일을 참조합니다. 바인딩 XML 파일에서 `wsdlLocation` 요소를 업데이트하여 AEM Forms의 URL을 지정합니다.

비동기 호출이 작동하는지 확인하려면 끝점 URL 값을 수정하고 `async=true`을 지정합니다. 예를 들어 JAX-WS로 만든 Java 프록시 파일의 경우 `BindingProvider.ENDPOINT_ADDRESS_PROPERTY`에 대해 다음을 지정합니다.

`https://server:port/soap/services/ServiceName?wsdl&async=true&lc_version=9.0.0`

다음 목록은 비동기적으로 호출할 때 사용자 지정 바인딩 파일이 필요한 다른 서비스를 지정합니다.

* PDFG3D
* 작업 관리자
* 애플리케이션 관리자
* 디렉토리 관리자
* Distiller
* 권한 관리
* 문서 관리

### J2EE 응용 프로그램 서버의 차이점 {#differences-in-j2ee-application-servers}

특정 J2EE 응용 프로그램 서버를 사용하여 만든 프록시 라이브러리가 다른 J2EE 응용 프로그램 서버에서 호스팅되는 AEM Forms을 제대로 호출하지 못하는 경우가 있습니다. WebSphere에 배포된 AEM Forms을 사용하여 생성된 프록시 라이브러리를 고려해 보십시오. 이 프록시 라이브러리는 JBoss 응용 프로그램 서버에 배포된 AEM Forms 서비스를 성공적으로 호출할 수 없습니다.

`PrincipalReference`과 같은 일부 AEM Forms 복합 데이터 유형은 JBoss Application Server와 비교하여 WebSphere에 AEM Forms을 배포할 때 다르게 정의됩니다. 다른 J2EE 응용 프로그램 서비스에서 사용하는 JDK의 차이는 WSDL 정의에 차이가 있는 이유입니다. 따라서 동일한 J2EE 응용 프로그램 서버에서 생성된 프록시 라이브러리를 사용합니다.

### 웹 서비스 {#accessing-multiple-services-using-web-services}를 사용하여 여러 서비스에 액세스

네임스페이스 충돌로 인해 여러 서비스 WSDL 간에 데이터 개체를 공유할 수 없습니다. 다른 서비스는 데이터 형식을 공유할 수 있으므로 서비스는 WSDL에서 이러한 유형의 정의를 공유합니다. 예를 들어 `BLOB` 데이터 유형이 포함된 .NET 클라이언트 어셈블리를 동일한 .NET 클라이언트 프로젝트에 두 개 추가할 수 없습니다. 이 경우 컴파일 오류가 발생합니다.

다음 목록은 여러 서비스 WSDL 간에 공유할 수 없는 데이터 형식을 지정합니다.

* `User`
* `Principals`
* `PrincipalReference`
* `Groups`
* `Roles`
* `BLOB`

이 문제를 방지하려면 데이터 유형의 자격을 완전히 검증하는 것이 좋습니다. 예를 들어 서비스 참조를 사용하여 Forms 서비스와 서명 서비스를 모두 참조하는 .NET 응용 프로그램을 생각해 보십시오. 두 서비스 참조 모두 `BLOB` 클래스를 포함합니다. `BLOB` 인스턴스를 사용하려면 선언할 때 `BLOB` 개체의 자격을 완전히 해제합니다. 이 방법은 다음 코드 예제에 나와 있습니다. 이 코드 예제에 대한 자세한 내용은 [대화형 Forms에 디지털 서명](/help/forms/developing/digitally-signing-certifying-documents.md#digitally-signing-interactive-forms)을 참조하십시오.

다음 C# 코드 예제에서는 Forms 서비스를 통해 렌더링되는 대화형 양식을 서명합니다. 클라이언트 응용 프로그램에는 2개의 서비스 참조가 있습니다. Forms 서비스와 연결된 `BLOB` 인스턴스는 `SignInteractiveForm.ServiceReference2` 네임스페이스에 속합니다. 마찬가지로 서명 서비스와 연결된 `BLOB` 인스턴스는 `SignInteractiveForm.ServiceReference1` 네임스페이스에 속합니다. 서명된 대화형 양식은 *LoanXFASigned.pdf*&#x200B;라는 PDF 파일로 저장됩니다.

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

### I로 시작하는 서비스에서 잘못된 프록시 파일 {#services-starting-with-the-letter-i-produce-invalid-proxy-files} 생성

Microsoft .Net 3.5 및 WCF를 사용할 때 일부 AEM Forms 생성 프록시 클래스의 이름이 잘못되었습니다. 이 문제는 IBMFilenetContentRepositoryConnector, IDPSchedulerService 또는 이름이 I로 시작하는 기타 서비스에 대해 프록시 클래스가 생성될 때 발생합니다. 예를 들어 IBMFileNetContentRepositoryConnector의 경우 생성된 클라이언트의 이름이 `BMFileNetContentRepositoryConnectorClient`입니다. 생성된 프록시 클래스에 없는 문자입니다.

