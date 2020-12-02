---
title: PDF 서비스 Java API QuickStart(SOAP) 생성
seo-title: PDF 서비스 Java API QuickStart(SOAP) 생성
description: 'null'
seo-description: 'null'
uuid: f8c4a476-de5e-440a-b419-0bd1d7fde5ca
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: a7c0c4cf-7476-41e7-8d4e-564e6a21458d
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '299'
ht-degree: 0%

---


# PDF 서비스 Java API 빠른 시작(SOAP) {#generate-pdf-service-java-api-quickstart-soap} 생성

SOAP(Java API Quick Start)는 PDF 생성 서비스에서 사용할 수 있습니다.

[빠른 시작(SOAP 모드):Java API를 사용하여 Microsoft Word 문서를 PDF 문서로 변환](generate-pdf-service-java-api.md#quick-start-soap-mode-converting-a-microsoft-word-document-to-a-pdf-document-using-the-java-api)

[빠른 시작(SOAP 모드):Java API를 사용하여 HTML 내용을 PDF 문서로 변환](generate-pdf-service-java-api.md#quick-start-soap-mode-converting-html-content-to-a-pdf-document-using-the-java-api)

[빠른 시작(SOAP 모드):Java API(SOAP 모드)를 사용하여 PDF 문서를 RTF 파일로 변환](generate-pdf-service-java-api.md#quick-start-soap-mode-converting-a-pdf-document-to-an-rtf-file-using-the-java-api-soap-mode)

AEM Forms 작업은 AEM Forms 강력한 형식의 API를 사용하여 수행할 수 있으며 연결 모드는 SOAP로 설정해야 합니다.

>[!NOTE]
>
>AEM Forms과 함께 프로그래밍에 있는 빠른 시작은 JBoss Application Server 및 Microsoft Windows 운영 체제에 배포되는 Forms 서버를 기반으로 합니다. 그러나 UNIX와 같은 다른 운영 체제를 사용하는 경우 Windows 특정 경로를 해당 운영 체제에서 지원되는 경로로 바꿉니다. 마찬가지로 다른 J2EE 응용 프로그램 서버를 사용하는 경우 올바른 연결 속성을 지정해야 합니다. [연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)을 참조하십시오.

## 빠른 시작(SOAP 모드):Java API {#quick-start-soap-mode-converting-a-microsoft-word-document-to-a-pdf-document-using-the-java-api}를 사용하여 Microsoft Word 문서를 PDF 문서로 변환

다음 코드 예제에서는 *Loan.doc*&#x200B;이라는 Word 파일을 *Loan.pdf*&#x200B;이라는 PDF 문서로 변환합니다. ([Word 문서를 PDF 문서로 변환](/help/forms/developing/converting-file-formats-pdf.md#converting-word-documents-to-pdf-documents)을 참조하십시오.)

```java
 /*
     * This Java Quick Start uses the SOAP mode and contains the following JAR files
     * in the class path:
     * 1. adobe-generatepdf-client.jar
     * 2. adobe-livecycle-client.jar
     * 3. adobe-usermanager-client.jar
     * 4. adobe-utilities.jar
     * 5. jboss-client.jar (use a different JAR file if the forms server is not deployed
     * on JBoss)
     * 6. activation.jar (required for SOAP mode)
     * 7. axis.jar (required for SOAP mode)
     * 8. commons-codec-1.3.jar (required for SOAP mode)
     * 9.  commons-collections-3.1.jar  (required for SOAP mode)
     * 10. commons-discovery.jar (required for SOAP mode)
     * 11. commons-logging.jar (required for SOAP mode)
     * 12. dom3-xml-apis-2.5.0.jar (required for SOAP mode)
     * 13. jaxen-1.1-beta-9.jar (required for SOAP mode)
     * 14. jaxrpc.jar (required for SOAP mode)
     * 15. log4j.jar (required for SOAP mode)
     * 16. mail.jar (required for SOAP mode)
     * 17. saaj.jar (required for SOAP mode)
     * 18. wsdl4j.jar (required for SOAP mode)
     * 19. xalan.jar (required for SOAP mode)
     * 20. xbean.jar (required for SOAP mode)
     * 21. xercesImpl.jar (required for SOAP mode)
     *
     * These JAR files are located in the following path:
     * <install directory>/sdk/client-libs/common
     *
     * The adobe-utilities.jar file is located in the following path:
     * <install directory>/sdk/client-libs/jboss
     *
     * The jboss-client.jar file is located in the following path:
     * <install directory>/jboss/bin/client
     *
     * SOAP required JAR files are located in the following path:
     * <install directory>/sdk/client-libs/thirdparty
     *
     * If you want to invoke a remote forms server instance and there is a
     * firewall between the client application and the server, then it is
     * recommended that you use the SOAP mode. When using the SOAP mode,
     * you have to include these additional JAR files
     *
     * For information about the SOAP
     * mode, see "Setting connection properties" in Programming
     * with AEM Forms
     */
 import java.io.File;
 import java.io.FileInputStream;
 import java.util.Properties;
 
 import com.adobe.idp.Document;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 import com.adobe.livecycle.generatepdf.client.CreatePDFResult;
 import com.adobe.livecycle.generatepdf.client.GeneratePdfServiceClient;
 
 public class ConvertWordDocumentSOAP {
 
     public static void main(String[] args)
     {
         try{
         //Set connection properties required to invoke AEM Forms using SOAP mode
         Properties connectionProps = new Properties();
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://'[server]:[port]'");
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
 
         //Create a ServiceClientFactory instance
         ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps);
 
         //Create a GeneratePdfServiceClient object
         GeneratePdfServiceClient pdfGenClient = new GeneratePdfServiceClient(myFactory);
 
         //Get a Microsoft Word file document to convert to a PDF document
         String inputFileName = "C:\\Adobe\\Loan.doc";
         FileInputStream fileInputStream = new FileInputStream(inputFileName);
         Document inDoc = new Document(fileInputStream);
 
         //Set createPDF2 parameter values
         String adobePDFSettings = "Smallest_File_Size";
          String securitySettings = "No Security";
          String fileTypeSettings = "Filetype Settings";
 
          //Convert the Word document to a PDF document
          CreatePDFResult result = pdfGenClient.createPDF2(
             inDoc,
             inputFileName,
             fileTypeSettings,
             adobePDFSettings,
             securitySettings,
             null,
             null);
 
          //Get the newly created document
          Document createdDocument = result.getCreatedDocument();
 
          //Save the converted PDF document as a PDF file
         createdDocument.copyToFile(new File("C:\\Adobe\\Loan.pdf"));
     }
     catch (Exception e) {
         System.out.println("Error OCCURRED: " + e.getMessage());
         }
     }
 }
```

## 빠른 시작(SOAP 모드):Java API {#quick-start-soap-mode-converting-html-content-to-a-pdf-document-using-the-java-api}를 사용하여 HTML 내용을 PDF 문서로 변환

다음 Java 코드 예는 https://www.adobe.com에 있는 HTML 내용을 *AdobeHTML.pdf*&#x200B;라는 PDF 문서로 변환합니다. (HTML 문서를 PDF 문서로 변환[을(를) 참조하십시오.)](/help/forms/developing/converting-file-formats-pdf.md#converting-html-documents-to-pdf-documents)

```java
 /*
     * This Java Quick Start uses the SOAP mode and contains the following JAR files
     * in the class path:
     * 1. adobe-generatepdf-client.jar
     * 2. adobe-livecycle-client.jar
     * 3. adobe-usermanager-client.jar
     * 4. adobe-utilities.jar
     * 5. jboss-client.jar (use a different JAR file if the forms server is not deployed
     * on JBoss)
     * 6. activation.jar (required for SOAP mode)
     * 7. axis.jar (required for SOAP mode)
     * 8. commons-codec-1.3.jar (required for SOAP mode)
     * 9.  commons-collections-3.1.jar  (required for SOAP mode)
     * 10. commons-discovery.jar (required for SOAP mode)
     * 11. commons-logging.jar (required for SOAP mode)
     * 12. dom3-xml-apis-2.5.0.jar (required for SOAP mode)
     * 13. jaxen-1.1-beta-9.jar (required for SOAP mode)
     * 14. jaxrpc.jar (required for SOAP mode)
     * 15. log4j.jar (required for SOAP mode)
     * 16. mail.jar (required for SOAP mode)
     * 17. saaj.jar (required for SOAP mode)
     * 18. wsdl4j.jar (required for SOAP mode)
     * 19. xalan.jar (required for SOAP mode)
     * 20. xbean.jar (required for SOAP mode)
     * 21. xercesImpl.jar (required for SOAP mode)
     *
     * These JAR files are located in the following path:
     * <install directory>/sdk/client-libs/common
     *
     * The adobe-utilities.jar file is located in the following path:
     * <install directory>/sdk/client-libs/jboss
     *
     * The jboss-client.jar file is located in the following path:
     * <install directory>/jboss/bin/client
     *
     * SOAP required JAR files are located in the following path:
     * <install directory>/sdk/client-libs/thirdparty
     *
     * If you want to invoke a remote forms server instance and there is a
     * firewall between the client application and the server, then it is
     * recommended that you use the SOAP mode. When using the SOAP mode,
     * you have to include these additional JAR files
     *
     * For information about the SOAP
     * mode, see "Setting connection properties" in Programming
     * with AEM Forms
     */
 import java.io.File;
 import java.util.Properties;
 import com.adobe.idp.Document;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 import com.adobe.livecycle.generatepdf.client.GeneratePdfServiceClient;
 import com.adobe.livecycle.generatepdf.client.HtmlToPdfResult;
 
 public class ConvertHTMLSOAP {
 
     public static void main(String[] args)
     {
         try{
         //Set connection properties required to invoke AEM Forms using SOAP mode
         Properties connectionProps = new Properties();
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://'[server]:[port]'");
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
 
         //Create a ServiceClientFactory instance
         ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps);
 
         //Create a GeneratePdfServiceClient object
         GeneratePdfServiceClient pdfGenClient = new GeneratePdfServiceClient(myFactory);
 
         //Get an HTML document to convert to a PDF document a
         String inputFileName = "https://www.adobe.com";
 
          String securitySettings = "No Security";
         String fileTypeSettings = "Standard";
 
          //Convert HTML content to a PDF document
          HtmlToPdfResult result = pdfGenClient.htmlToPDF2(
                  inputFileName,
                  fileTypeSettings,
                  securitySettings,
                  null,
                 null);
 
          //Get the newly created document
          Document createdDocument = result.getCreatedDocument();
 
          //Save the PDF document as a PDF file
         createdDocument.copyToFile(new File("C:\\AdobeHTML.pdf"));
     }
     catch (Exception e) {
         System.out.println("Error OCCURRED: " + e.getMessage());
     }
     }
 }
```

## 빠른 시작(SOAP 모드):Java API(SOAP 모드) {#quick-start-soap-mode-converting-a-pdf-document-to-an-rtf-file-using-the-java-api-soap-mode}를 사용하여 PDF 문서를 RTF 파일로 변환

다음 코드 예제에서는 *Loan.pdf*&#x200B;라는 PDF 문서를 *Loan.rtf*&#x200B;라는 RTF 문서로 변환합니다. ([PDF 문서를 이미지가 아닌 형식으로 변환](/help/forms/developing/converting-file-formats-pdf.md#converting-pdf-documents-to-non-image-formats)을 참조하십시오.)

```java
 /*
     * This Java Quick Start uses the SOAP mode and contains the following JAR files
     * in the class path:
     * 1. adobe-generatepdf-client.jar
     * 2. adobe-livecycle-client.jar
     * 3. adobe-usermanager-client.jar
     * 4. adobe-utilities.jar
     * 5. jboss-client.jar (use a different JAR file if the forms server is not deployed
     * on JBoss)
     * 6. activation.jar (required for SOAP mode)
     * 7. axis.jar (required for SOAP mode)
     * 8. commons-codec-1.3.jar (required for SOAP mode)
     * 9.  commons-collections-3.1.jar  (required for SOAP mode)
     * 10. commons-discovery.jar (required for SOAP mode)
     * 11. commons-logging.jar (required for SOAP mode)
     * 12. dom3-xml-apis-2.5.0.jar (required for SOAP mode)
     * 13. jaxen-1.1-beta-9.jar (required for SOAP mode)
     * 14. jaxrpc.jar (required for SOAP mode)
     * 15. log4j.jar (required for SOAP mode)
     * 16. mail.jar (required for SOAP mode)
     * 17. saaj.jar (required for SOAP mode)
     * 18. wsdl4j.jar (required for SOAP mode)
     * 19. xalan.jar (required for SOAP mode)
     * 20. xbean.jar (required for SOAP mode)
     * 21. xercesImpl.jar (required for SOAP mode)
     *
     * These JAR files are located in the following path:
     * <install directory>/sdk/client-libs/common
     *
     * The adobe-utilities.jar file is located in the following path:
     * <install directory>/sdk/client-libs/jboss
     *
     * The jboss-client.jar file is located in the following path:
     * <install directory>/jboss/bin/client
     *
     * SOAP required JAR files are located in the following path:
     * <install directory>/sdk/client-libs/thirdparty
     *
     * If you want to invoke a remote forms server instance and there is a
     * firewall between the client application and the server, then it is
     * recommended that you use the SOAP mode. When using the SOAP mode,
     * you have to include these additional JAR files
     *
     * For information about the SOAP
     * mode, see "Setting connection properties" in Programming
     * with AEM Forms
     */
 import java.io.File;
 import java.io.FileInputStream;
 import java.util.Properties;
 import com.adobe.idp.Document;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 import com.adobe.livecycle.generatepdf.client.ConvertPDFFormatType;
 import com.adobe.livecycle.generatepdf.client.ExportPDFResult;
 import com.adobe.livecycle.generatepdf.client.GeneratePdfServiceClient;
 
 
 public class GeneratePdf_ExportPDFSOAP {
 
     public static void main(String[] args)
     {
         try{
             //Set connection properties required to invoke AEM Forms using SOAP mode
             Properties connectionProps = new Properties();
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://'[server]:[port]'");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
 
             //Create a ServiceClientFactory instance
             ServiceClientFactory factory = ServiceClientFactory.createInstance(connectionProps);
 
             //Create a GeneratePdfServiceClient object
             GeneratePdfServiceClient pdfGenClient = new GeneratePdfServiceClient(factory);
 
             //Get a PDF document to convert to an RTF document
             String inputFileName = "C:\\Adobe\\Loan.pdf.pdf";
             FileInputStream fileInputStream = new FileInputStream(inputFileName);
             Document inDoc = new Document(fileInputStream);
 
             //Convert a PDF document to a RTF document
             ExportPDFResult result = pdfGenClient.exportPDF2(
                 inDoc,
                 inputFileName,
                 ConvertPDFFormatType.RTF,
                 null);
 
          //Get the newly created RTF document
          Document createdDocument = result.getConvertedDocument();
 
          //Save the RTF file
         createdDocument.copyToFile(new File("C:\\Adobe\\Loan.pdf.rtf"));
         }
         catch (Exception e) {
             System.out.println("Error OCCURRED: " + e.getMessage());
         }
     }
 }
```

