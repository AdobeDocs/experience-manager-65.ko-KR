---
title: Portable Protection Library를 사용하여 정책으로 보호된 PDF 문서 Reader 확장
seo-title: Portable Protection Library를 사용하여 정책으로 보호된 PDF 문서 Reader 확장
description: Reader 확장을 사용하면 Acrobat Reader을 통해 Adobe PDF 문서에서 대화형 기능을 사용할 수 있습니다. PPL(Portable Protection Library)을 사용하여 DRM 보호 PDF 문서를 읽을 수 있습니다.
seo-description: Reader 확장을 사용하면 Acrobat Reader을 통해 Adobe PDF 문서에서 대화형 기능을 사용할 수 있습니다. PPL(Portable Protection Library)을 사용하여 DRM 보호 PDF 문서를 읽을 수 있습니다.
uuid: 0da17641-d24c-43c2-b918-8b5abe1e5473
contentOwner: khsingh
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: document_services
discoiquuid: 83ca522e-d16e-4196-9aa7-84f85de8dee2
feature: 문서 보안
exl-id: fe5d83e8-5e36-4146-a20a-dab2213055e2
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '835'
ht-degree: 0%

---

# Reader: Portable Protection Library {#reader-extending-policy-protected-pdf-documents-using-portable-protection-library} 를 사용하여 정책으로 보호된 PDF 문서 확장

문서 보안 정책으로 보호된 PDF 문서를 읽기/확장하려면 문서 보안, Reader 확장 및 Java 프로그래밍 언어의 개념을 잘 알고 있어야 합니다.

문서 보안을 사용하여 인증된 사용자만 특정 PDF 문서에 대한 액세스를 제한할 수 있습니다. 받는 사람이 보호된 문서를 사용하는 방법을 결정할 수도 있습니다. 예를 들어 수신자가 문서 보안 정책으로 보호된 문서의 텍스트를 인쇄, 복사 또는 편집할 수 있는지 여부를 지정할 수 있습니다. 문서 보안에 대한 자세한 내용은 [문서 보안 정보](/help/forms/using/admin-help/document-security.md)를 참조하십시오.

Reader 확장을 사용하여 Acrobat Reader을 통해 Adobe PDF 문서에서 대화형 기능을 활성화할 수 있습니다. 이러한 대화형 기능은 일반적으로 Adobe Acrobat Professional과 Standard를 통해서만 사용할 수 있습니다. Reader 확장을 사용할 수 있는 대화형 기능에 대해 알아보려면 [Adobe Experience Manager Forms DocAssurance 서비스&#x200B;](/help/forms/using/overview-aem-document-services.md)**.**

문서를 네트워크를 통해 이동할 필요 없이 휴대용 보호 라이브러리를 사용하여 문서에 정책을 적용할 수 있습니다. 보안 자격 증명과 보호 정책 세부 사항만 네트워크를 통해 이동합니다. 실제 문서는 클라이언트 및 보호 정책이 클라이언트에 로컬로 적용되지 않습니다.

## Reader 확장 문서 보안 정책으로 보호된 PDF 문서 {#reader-extending-document-security-policy-protected-pdf-documents}

정책으로 보호된 문서는 암호화된 문서입니다. 표준 Reader 확장 API를 사용하여 정책으로 보호된 PDF 문서의 사용 권한을 적용, 제거 및 검색할 수 없습니다. Portable Protection Library의 Reader 확장 서비스만 문서 보안 정책으로 보호된 PDF 문서의 사용 권한을 적용, 제거 및 검색할 수 있는 API를 제공합니다.

### Reader 확장 서비스 {#reader-extensions-service}

Reader 확장 서비스는 정책으로 보호된 PDF 문서에 사용 권한을 추가하여 Adobe Acrobat Reader을 사용하여 PDF 문서를 열 때 일반적으로 사용할 수 없는 기능을 활성화합니다. 또한 정책으로 보호된 문서의 사용 권한을 제거하고 검색하는 API도 있습니다.

Reader 확장 서비스는 PDF 표준 1.6 이상을 기반으로 한 PDF 문서를 완전히 지원합니다. Acrobat Reader 외에도, 타사 사용자는 정책에 의해 보호된 PDF 문서를 사용하기 위해 추가 소프트웨어 또는 플러그인이 필요하지 않습니다.

Reader 확장 서비스를 사용하여 다음 작업을 수행할 수 있습니다.

* 정책으로 보호된 PDF 문서에 사용 권한을 적용합니다.
* 정책으로 보호된 PDF 문서의 사용 권한을 제거합니다.
* 정책으로 보호된 PDF 문서에 적용된 사용 권한을 검색합니다.

### 문서 보안 정책으로 보호된 PDF 문서에 사용 권한 적용 {#apply-usage-rights-to-a-document-security-policy-protected-pdf-document}

`applyUsageRights`Java API를 사용하여 정책으로 보호된 PDF 문서에 사용 권한을 적용할 수 있습니다. 사용 권한은 Acrobat에서 기본적으로 사용할 수 있지만, 양식에 주석을 추가하거나, 양식 필드를 작성하고, 양식을 저장하는 기능과 같이 Adobe Reader에서는 사용할 수 없는 기능과 관련이 있습니다. 사용 권한이 적용된 PDF 문서를 권한 사용 문서라고 합니다. Adobe Reader에서 권한 사용 문서를 여는 사용자는 해당 특정 문서에 대해 사용 가능한 작업을 수행할 수 있습니다.

**구문:** `InputStream applyUsageRights(InputStream inputFile, File certFile, String credentialPassword, UsageRights usageRights)`

<table>
 <tbody>
  <tr>
   <td><p><strong>매개 변수</strong></p> </td>
   <td><p><strong>설명</strong></p> </td>
  </tr>
  <tr>
   <td><p>inputFile</p> </td>
   <td><p>사용 권한을 적용할 PDF 문서를 나타내는 InputStream을 지정합니다. LiveCycle Rights Management 또는 AEM Forms 문서 보안 보호 문서를 사용할 수 있습니다.</p> </td>
  </tr>
  <tr>
   <td><p>certFile</p> </td>
   <td><p>.jks 파일을 나타내는 File 개체를 지정합니다. .jks 파일은 키 저장소 파일입니다. 사용 권한을 부여하는 인증서를 가리킵니다.</p> </td>
  </tr>
  <tr>
   <td><p>credentialPassword</p> </td>
   <td><p>키 저장소의 암호를 지정합니다. </p> </td>
  </tr>
  <tr>
   <td><p>usageRights</p> </td>
   <td><p><a href="https://help.adobe.com/en_US/livecycle/11.0/ProgramLC/javadoc/com/adobe/livecycle/readerextensions/client/UsageRights.html" target="_blank">UsageRights</a> 형식의 개체를 지정합니다. usageRights 개체는 정책으로 보호된 PDF 문서에 적용할 수 있는 개별 권한을 나타냅니다.</p> </td>
  </tr>
 </tbody>
</table>

### 정책으로 보호된 PDF 문서에 적용된 사용 권한을 검색합니다.   {#retrieve-usage-rights-applied-to-a-policy-protected-pdf-document-nbsp}

`getDocumentUsageRights`Java API를 사용하여 정책으로 보호된 PDF 문서에 적용된 Reader 확장 사용 권한을 검색할 수 있습니다. 사용 권한에 대한 정보를 검색하면 정책으로 보호된 PDF 문서에 대해 기능 판독기 확장 기능을 사용하도록 설정할 수 있습니다.

**구문:** `public GetUsageRightsResult getDocumentUsageRights(InputStream inDoc)`

<table>
 <tbody>
  <tr>
   <td><p><strong>매개 변수</strong></p> </td>
   <td><p><strong>설명</strong></p> </td>
  </tr>
  <tr>
   <td><p>inDoc</p> </td>
   <td><p>사용 권한을 검색할 PDF 문서를 나타내는 InputStream을 지정합니다. LiveCycle Rights Management 또는 AEM Forms 문서 보안 보호 문서를 사용할 수 있습니다.</p> </td>
  </tr>
 </tbody>
</table>

#### 코드 샘플 {#code-sample}

```java
//Create a ServiceClientFactory instance
ServiceClientFactory factory = ServiceClientFactory.createInstance(connectionProps);
//Create a RightsManagementClient object
RightsManagementClient2 rmClient2= new RightsManagementClient2(factory);

String inputFileName = "C:\\Sample\\protected.pdf"; //Input file can be RM protected or unprotected pdf file
File certFile = new File("C:\\Sample\\cert.jks"); //RE certificate file
String password = "password"; //password for RE certificate
UsageRights usageRights = getUsageRights(true,true,false,false,true,true,false,false,false,false,true);

//RE rights to be applied on the file : FormFillIn, FormDataImportExport, SubmitStandalone, OnlineForms, DynamicFormField, DynamicFormPages, BarcodeDecoding, DigitalSignatures, Comments, CommentsOnline, EmbeddedFiles

InputStream inputFileStream = new FileInputStream(inputFileName);
InputStream output = rmClient2.getRightsManagementReaderExtensionService().applyUsageRights(inputFileStream, certFile, credentialPassword, rights);

String outputFileName = "C:\\Sample\\ReAdded.pdf";
//Save the PDF document
File myFile = new File(outputFileName);
FileOutputStream outputStream = new FileOutputStream(myFile);

int read = 0;
byte[] bytes = new byte[1024];

while ((read = output.read(bytes)) != -1) {

    outputStream.write(bytes, 0, read);
}

System.out.println("UsageRights applied successfully to the document. ”);
 outputStream.close();
inputFileStream.close();

//Get Usage Rights for the output pdf document
InputStream fileWithRe = new FileInputStream(myFile);

GetUsageRightsResult usageRights = rmClient2.getRightsManagementReaderExtensionService().getDocumentUsageRights(fileWithRe);

UsageRights rights = usageRights.getRights();
String right1 = rights1.toString();
System.out.println("RE rights for the file are :\n"+right1);
 fileWithRe.close();
```

### 정책으로 보호된 PDF 문서의 사용 권한 제거 {#remove-usage-rights-of-a-policy-protected-pdf-document}

`removeUsageRights`Java API를 사용하여 정책으로 보호된 문서에서 사용 권한을 제거할 수 있습니다. 문서에서 다른 AEM Forms 작업을 수행하려면 정책으로 보호된 PDF 문서에서 사용 권한을 제거해야 합니다. 예를 들어 사용 권한을 설정하기 전에 PDF 문서에 디지털 서명(또는 인증)해야 합니다. 따라서 정책으로 보호된 문서에 대해 작업을 수행하려면 PDF 문서에서 사용 권한을 제거하고 문서에 디지털 서명을 하는 등의 기타 작업을 수행한 다음 문서에 사용 권한을 다시 적용해야 합니다.

**구문:** `InputStream removeUsageRights(InputStream inputFile)`

<table>
 <tbody>
  <tr>
   <td><p><strong>매개 변수</strong></p> </td>
   <td><p><strong>설명</strong></p> </td>
  </tr>
  <tr>
   <td><p> </p> <p>inputFile</p> </td>
   <td>사용<br /> 권한을 제거할 PDF 문서를 나타내는 InputStream을 지정합니다. LiveCycle Rights Management 또는 AEM Forms 문서 보안 보호 문서를 사용할 수 있습니다.</td>
  </tr>
 </tbody>
</table>

#### 코드 샘플 {#code-sample-1}

```java
//Create a ServiceClientFactory instance
ServiceClientFactory factory = ServiceClientFactory.createInstance(connectionProps);
//Create a RightsManagementClient object
RightsManagementClient2 rmClient2= new RightsManagementClient2(factory);

String inputFileName = "C:\\Sample\\fileWithRe.pdf"; //Input file can be RM protected or unprotected pdf file
InputStream inputFileStream = new FileInputStream(inputFileName);

InputStream fileStream = rmClient2.getRightsManagementReaderExtensionService().removeUsageRights(inputFileStream);

String outputFileName = "C:\\Sample\\ReRemoveded.pdf";
//Save the PDF document
File myFile = new File(outputFileName);
FileOutputStream outputStream = new FileOutputStream(myFile);

int read = 0;
byte[] bytes = new byte[1024];

while ((read = fileStream.read(bytes)) != -1) {

    outputStream.write(bytes, 0, read);
}
System.out.println("RE rights removed successfully from the document.”);
outputStream.close();
inputFileStream.close();
```
