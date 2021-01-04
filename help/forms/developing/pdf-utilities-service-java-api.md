---
title: PDF 유틸리티 서비스 Java APIQ빠른 시작(SOAP)
seo-title: PDF 유틸리티 서비스 Java APIQ빠른 시작(SOAP)
description: PDF 유틸리티 서비스를 사용하여 PDF 문서를 XDP 문서로 변환하고, XDP 문서를 PDF 문서로 변환하고, PDF 문서 속성을 검색하고, PDF 문서의 저장 스타일을 설정하고, PDF 문서의 기밀 정보를 가릴 수 있습니다.
seo-description: PDF 유틸리티 서비스를 사용하여 PDF 문서를 XDP 문서로 변환하고, XDP 문서를 PDF 문서로 변환하고, PDF 문서 속성을 검색하고, PDF 문서의 저장 스타일을 설정하고, PDF 문서의 기밀 정보를 가릴 수 있습니다.
uuid: 96bb2bd5-b274-43d4-a664-49cc1c526b3f
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: 4ec4c674-d7d3-4988-9d77-78d274970672
translation-type: tm+mt
source-git-commit: 07889ead2ae402b5fb738ca08c7efe076ef33e44
workflow-type: tm+mt
source-wordcount: '503'
ht-degree: 0%

---


# PDF 유틸리티 서비스 Java API 빠른 시작(SOAP) {#pdf-utilities-service-java-apiquick-start-soap}

다음 빠른 시작을 PDF 유틸리티 서비스에 사용할 수 있습니다.

[빠른 시작(SOAP 모드):Java API를 사용하여 PDF 문서를 XDP 문서로 변환](pdf-utilities-service-java-api.md#quick-start-soap-mode-converting-a-pdf-document-to-an-xdp-document-using-the-java-api)

[빠른 시작(SOAP 모드):Java API를 사용하여 XDP 문서를 PDF 문서로 변환](pdf-utilities-service-java-api.md#quick-start-soap-mode-converting-an-xdp-document-to-a-pdf-document-using-the-java-api)

[빠른 시작(SOAP 모드):Java API를 사용하여 PDF 문서 속성 검색](pdf-utilities-service-java-api.md#quick-start-soap-mode-retrieving-pdf-document-properties-using-the-java-api)

[빠른 시작(SOAP 모드):Java API를 사용하여 PDF 문서에 대한 저장 스타일 설정](pdf-utilities-service-java-api.md#quick-start-soap-mode-setting-the-save-style-for-a-pdf-document-using-the-java-api)

[빠른 시작(SOAP 모드):PDF 문서 기밀 정보 가리기](pdf-utilities-service-java-api.md#quick-start-soap-mode-sanitizing-pdf-documents)

AEM Forms 작업은 AEM Forms 강력한 형식의 API를 사용하여 수행할 수 있으며 연결 모드는 SOAP로 설정해야 합니다.

>[!NOTE]
>
>AEM 양식을 사용한 프로그래밍에 있는 빠른 시작은 Forms Server 운영 체제를 기반으로 합니다. 그러나 UNIX와 같은 다른 운영 체제를 사용하는 경우에는 Windows 관련 경로를 해당 운영 체제에서 지원되는 경로로 바꿉니다. 마찬가지로 다른 J2EE 응용 프로그램 서버를 사용하는 경우 유효한 연결 속성을 지정해야 합니다. [연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)을 참조하십시오.

## 빠른 시작(SOAP 모드):Java API {#quick-start-soap-mode-converting-a-pdf-document-to-an-xdp-document-using-the-java-api}를 사용하여 PDF 문서를 XDP 문서로 변환

다음 코드 예제에서는 PDF 문서를 XDP 문서로 변환합니다. ([PDF 문서를 XDP 문서로 변환](/help/forms/developing/pdf-utilities.md#converting-pdf-documents-into-xdp-documents) 참조).

```java
 /*
     * This Java Quick Start uses the SOAP mode and contains the following JAR files
     * in the class path:
     * 1. adobe-pdfutility-client.jar
     * 2. adobe-livecycle-client.jar
     * 3. adobe-usermanager-client.jar
    * 4. activation.jar (required for SOAP mode)
    * 5. axis.jar (required for SOAP mode)
    * 6. commons-codec-1.3.jar (required for SOAP mode)
    * 7. commons-collections-3.2.jar  (required for SOAP mode)
    * 8. commons-discovery.jar (required for SOAP mode)
    * 9. commons-logging.jar (required for SOAP mode)
    * 10. dom3-xml-apis-2.5.0.jar (required for SOAP mode)
    * 11. jaxen-1.1-beta-9.jar (required for SOAP mode)
    * 12. jaxrpc.jar (required for SOAP mode)
    * 13. log4j.jar (required for SOAP mode)
    * 14. mail.jar (required for SOAP mode)
    * 15. saaj.jar (required for SOAP mode)
    * 16. wsdl4j.jar (required for SOAP mode)
    * 17. xalan.jar (required for SOAP mode)
    * 18. xbean.jar (required for SOAP mode)
    * 19. xercesImpl.jar (required for SOAP mode)
     *
     * The JBoss files must be kept in the jboss\client folder. You can copy the client folder to
     * your local development environment and then include the 3 JBoss JAR files in your class path
     *
     * These JAR files are located in the following path:
     * <install directory>/sdk/client-libs/common
     *
     *
     * <install directory>/jboss/bin/client
     *
     * If you want to invoke a remote forms server instance and there is a
     * firewall between the client application and the server, then it is
     * recommended that you use the SOAP mode. When using the SOAP mode,
     * you have to include additional JAR files located in the following
     * path
     * <install directory>/sdk/client-libs/thirdparty
     *
     * For information about the SOAP
     * mode and the additional JAR files that need to be included,
     * see "Setting connection properties" in Programming
     * with AEM Forms
     *
     * For complete details about the location of the AEM Forms JAR files,
     * see "Including AEM Forms Java library files" in Programming
     * with AEM Forms
     */
 
 import java.util.*;
 import com.adobe.livecycle.pdfutility.client.*;
 import java.io.*;
 import com.adobe.idp.Document;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 
 public class ConvertPDFToXDP
 {
     public static void main(String[] args)
     {
         try
         {
             //Set connection properties required to invoke AEM Forms
             Properties connectionProps = new Properties();
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://'[server]:[port]'");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
 
             // Create a ServiceClientFactory object
             ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps);
 
             // Create a PDF Utility client
             PDFUtilityServiceClient pdfUt = new PDFUtilityServiceClient(myFactory);
 
             // Specify a PDF document to convert to an XDP file
             FileInputStream fileInputStream = new FileInputStream("C:\\Adobe\Loan.pdf");
             Document inDoc = new Document(fileInputStream);
 
             // Convert the PDF document to an XDP file
             Document myXDP = pdfUt.convertPDFtoXDP(inDoc);
 
             //Save the returned Document object as an XDP file
             File xdpFile = new File("C:\\Adobe\Loan.xdp");
             myXDP.copyToFile(xdpFile);
         }
         catch (Exception e)
         {
             e.printStackTrace();
         }
     }
 }
 
```

## 빠른 시작(SOAP 모드):Java API {#quick-start-soap-mode-converting-an-xdp-document-to-a-pdf-document-using-the-java-api}를 사용하여 XDP 문서를 PDF 문서로 변환

다음 코드 예제에서는 XDP 문서를 PDF 문서로 변환합니다. ([XDP 문서를 PDF 문서로 변환](/help/forms/developing/pdf-utilities.md#converting-xdp-documents-into-pdf-documents) 참조)

```java
 /*
     * This Java Quick Start uses the SOAP mode and contains the following JAR files
     * in the class path:
     * 1. adobe-pdfutility-client.jar
     * 2. adobe-livecycle-client.jar
     * 3. adobe-usermanager-client.jar
    * 4. activation.jar (required for SOAP mode)
    * 5. axis.jar (required for SOAP mode)
    * 6. commons-codec-1.3.jar (required for SOAP mode)
    * 7. commons-collections-3.2.jar  (required for SOAP mode)
    * 8. commons-discovery.jar (required for SOAP mode)
    * 9. commons-logging.jar (required for SOAP mode)
    * 10. dom3-xml-apis-2.5.0.jar (required for SOAP mode)
    * 11. jaxen-1.1-beta-9.jar (required for SOAP mode)
    * 12. jaxrpc.jar (required for SOAP mode)
    * 13. log4j.jar (required for SOAP mode)
    * 14. mail.jar (required for SOAP mode)
    * 15. saaj.jar (required for SOAP mode)
    * 16. wsdl4j.jar (required for SOAP mode)
    * 17. xalan.jar (required for SOAP mode)
    * 18. xbean.jar (required for SOAP mode)
    * 19. xercesImpl.jar (required for SOAP mode)
     *
     * The JBoss files must be kept in the jboss\client folder. You can copy the client folder to
     * your local development environment and then include the 3 JBoss JAR files in your class path
     *
     * These JAR files are located in the following path:
     * <install directory>/sdk/client-libs/common
     *
     *
     * <install directory>/jboss/bin/client
     *
     * If you want to invoke a remote forms server instance and there is a
     * firewall between the client application and the server, then it is
     * recommended that you use the SOAP mode. When using the SOAP mode,
     * you have to include additional JAR files located in the following
     * path
     * <install directory>/sdk/client-libs/thirdparty
     *
     * For information about the SOAP
     * mode and the additional JAR files that need to be included,
     * see "Setting connection properties" in Programming
     * with AEM Forms
     *
     * For complete details about the location of the AEM Forms JAR files,
     * see "Including AEM Forms Java library files" in Programming
     * with AEM Forms
     */
 import com.adobe.livecycle.pdfutility.client.*;
 import java.util.*;
 import java.io.*;
 import com.adobe.idp.Document;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 
 public class ConvertXDPToPDF
 {
     public static void main(String[] args)
     {
         try
         {
             //Set connection properties required to invoke AEM Forms
             Properties connectionProps = new Properties();
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://'[server]:[port]'");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
 
             // Create a ServiceClientFactory object
             ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps);
 
             // Create a PDF Utility client
             PDFUtilityServiceClient pdfUt = new PDFUtilityServiceClient(myFactory);
 
             // Specify an XDP file to convert to a PDF document
             FileInputStream fileInputStream = new FileInputStream("C:\\Adobe\Loan.xdp");
             Document inDoc = new Document(fileInputStream);
 
             // Convert the XDP file to a PDF document
             Document myPDF = pdfUt.convertXDPtoPDF(inDoc);
 
             //Save the returned Document object as a PDF file
             File pdfFile = new File("C:\\Adobe\Loan.pdf");
             myPDF.copyToFile(pdfFile);
         }
         catch (Exception e)
         {
             e.printStackTrace();
         }
     }
 }
 
```

## 빠른 시작(SOAP 모드):Java API {#quick-start-soap-mode-retrieving-pdf-document-properties-using-the-java-api}을 사용하여 PDF 문서 속성 검색

다음 코드 예제에서는 문서가 PDF 문서인지 여부를 결정하고, 그렇다면 문서를 읽을 수 있는 가장 이른 Acrobat 버전입니다. ([PDF 문서 속성 검색](/help/forms/developing/pdf-utilities.md#retrieving-pdf-document-properties)을 참조하십시오.)

```java
 /*
     * This Java Quick Start uses the SOAP mode and contains the following JAR files
     * in the class path:
     * 1. adobe-pdfutility-client.jar
     * 2. adobe-livecycle-client.jar
     * 3. adobe-usermanager-client.jar
     * 4. activation.jar (required for SOAP mode)
     * 5. axis.jar (required for SOAP mode)
     * 6. commons-codec-1.3.jar (required for SOAP mode)
     * 7. commons-collections-3.2.jar  (required for SOAP mode)
     * 8. commons-discovery.jar (required for SOAP mode)
     * 9. commons-logging.jar (required for SOAP mode)
     * 10. dom3-xml-apis-2.5.0.jar (required for SOAP mode)
     * 11. jaxen-1.1-beta-9.jar (required for SOAP mode)
     * 12. jaxrpc.jar (required for SOAP mode)
     * 13. log4j.jar (required for SOAP mode)
     * 14. mail.jar (required for SOAP mode)
     * 15. saaj.jar (required for SOAP mode)
     * 16. wsdl4j.jar (required for SOAP mode)
     * 17. xalan.jar (required for SOAP mode)
     * 18. xbean.jar (required for SOAP mode)
     * 19. xercesImpl.jar (required for SOAP mode)
     *
     * The JBoss files must be kept in the jboss\client folder. You can copy the client folder to
     * your local development environment and then include the 3 JBoss JAR files in your class path
     *
     * These JAR files are located in the following path:
     * <install directory>/sdk/client-libs/common
     *
     *
     * <install directory>/jboss/bin/client
     *
     * If you want to invoke a remote forms server instance and there is a
     * firewall between the client application and the server, then it is
     * recommended that you use the SOAP mode. When using the SOAP mode,
     * you have to include additional JAR files located in the following
     * path
     * <install directory>/sdk/client-libs/thirdparty
     *
     * For information about the SOAP
     * mode and the additional JAR files that need to be included,
     * see "Setting connection properties" in Programming
     * with AEM Forms
     *
     * For complete details about the location of the AEM Forms JAR files,
     * see "Including AEM Forms Java library files" in Programming
     * with AEM Forms
     */
 import com.adobe.livecycle.pdfutility.client.*;
 import java.util.*;
 import java.io.*;
 import com.adobe.idp.Document;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 
 public class RetrievePDFProperties
 {
     public static void main(String[] args)
     {
         try
         {
             //Set connection properties required to invoke AEM Forms
             Properties connectionProps = new Properties();
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://'[server]:[port]'");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
 
             // Create a ServiceClientFactory object
             ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps);
 
             // Create a PDF Utility client
             PDFUtilityServiceClient pdfUt = new PDFUtilityServiceClient(myFactory);
 
             // Specify a document whose properties are retrieved
             FileInputStream fileInputStream = new FileInputStream("C:\\Adobe\Loan.pdf");
             Document inDoc = new Document(fileInputStream);
 
             // Create a properties options specification
             PDFPropertiesOptionSpec optionsSpec = new PDFPropertiesOptionSpec();
 
             // Set the properties to be evaluated in the options specification.
             // In this example, the options specification will be used to determine
             // if the document is a PDF document, and if so,
             // which Acrobat version is required to read it.
             optionsSpec.setIsPDFDocument(true);
             optionsSpec.setQueryRequiredAcrobatVersion(true);
 
             // Perform the query and retrieve the document properties
             PDFPropertiesResult propertiesResult = pdfUt.getPDFProperties(inDoc, optionsSpec);
 
             // Inspect the result and determine whether the file is a PDF document
             if (propertiesResult.getIsPDFDocument().booleanValue())
             {
                 System.out.println("Loan.pdf has been verified to be a PDF document.");
 
                 // Determine the required Acrobat version for reading the document
                 String acrobatVersion = propertiesResult.getRequiredAcrobatVersion();
                 System.out.println("The required Acrobat version is: " + acrobatVersion);
             }
         }
         catch (Exception e)
         {
             System.out.println("Error occurred: " + e.getMessage());
         }
     }
 }
 
 
```

## 빠른 시작(SOAP 모드):Java API {#quick-start-soap-mode-setting-the-save-style-for-a-pdf-document-using-the-java-api}을 사용하여 PDF 문서에 대한 저장 스타일 설정

다음 코드 예제에서는 빠른 웹 보기를 위해 저장 모드를 설정한 다음 PDF 문서를 암호화된 암호화 서비스에 전달합니다. 빠른 웹 보기를 위해 저장된 암호화된 PDF 문서는* FastWebViewLoan.pdf*라는 PDF 파일로 저장됩니다. ([PDF 문서 저장 모드 설정](/help/forms/developing/pdf-utilities.md#setting-pdf-document-save-modes)을 참조하십시오.)

```java
 /*
     * This Java Quick Start uses the SOAP mode and contains the following JAR files
     * in the class path:
     * 1. adobe-pdfutility-client.jar
     * 2. adobe-livecycle-client.jar
     * 3. adobe-usermanager-client.jar
     * 4. activation.jar (required for SOAP mode)
     * 5. axis.jar (required for SOAP mode)
     * 6. commons-codec-1.3.jar (required for SOAP mode)
     * 7. commons-collections-3.2.jar  (required for SOAP mode)
     * 8. commons-discovery.jar (required for SOAP mode)
     * 9. commons-logging.jar (required for SOAP mode)
     * 10. dom3-xml-apis-2.5.0.jar (required for SOAP mode)
     * 11. jaxen-1.1-beta-9.jar (required for SOAP mode)
     * 12. jaxrpc.jar (required for SOAP mode)
     * 13. log4j.jar (required for SOAP mode)
     * 14. mail.jar (required for SOAP mode)
     * 15. saaj.jar (required for SOAP mode)
     * 16. wsdl4j.jar (required for SOAP mode)
     * 17. xalan.jar (required for SOAP mode)
     * 18. xbean.jar (required for SOAP mode)
     * 19. xercesImpl.jar (required for SOAP mode)
     *
     * The JBoss files must be kept in the jboss\client folder. You can copy the client folder to
     * your local development environment and then include the 3 JBoss JAR files in your class path
     *
     * These JAR files are located in the following path:
     * <install directory>/sdk/client-libs/common
     *
     *
     * <install directory>/jboss/bin/client
     *
     * If you want to invoke a remote forms server instance and there is a
     * firewall between the client application and the server, then it is
     * recommended that you use the SOAP mode. When using the SOAP mode,
     * you have to include additional JAR files located in the following
     * path
     * <install directory>/sdk/client-libs/thirdparty
     *
     * For information about the SOAP
     * mode and the additional JAR files that need to be included,
     * see "Setting connection properties" in Programming
     * with AEM Forms
     *
     * For complete details about the location of the AEM Forms JAR files,
     * see "Including AEM Forms Java library files" in Programming
     * with AEM Forms
     */
 import com.adobe.livecycle.encryption.client.EncryptionServiceClient;
 import com.adobe.livecycle.encryption.client.PasswordEncryptionCompatability;
 import com.adobe.livecycle.encryption.client.PasswordEncryptionOption;
 import com.adobe.livecycle.encryption.client.PasswordEncryptionOptionSpec;
 import com.adobe.livecycle.encryption.client.PasswordEncryptionPermission;
 import com.adobe.livecycle.pdfutility.client.*;
 import java.util.*;
 import java.io.*;
 import com.adobe.idp.Document;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 
 public class SaveDocument
 {
     public static void main(String[] args)
     {
         try
         {
             //Set connection properties required to invoke AEM Forms
             Properties connectionProps = new Properties();
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://'[server]:[port]'");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
 
             // Create a ServiceClientFactory object
             ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps);
 
             // Create a PDF Utility client
             PDFUtilityServiceClient pdfUt = new PDFUtilityServiceClient(myFactory);
 
             // Specify a document to be saved
             FileInputStream fileInputStream = new FileInputStream("C:\\Adobe\Loan.pdf");
             Document inDoc = new Document(fileInputStream);
 
             // Specify the save option
             PDFUtilitySaveMode saveMode = new PDFUtilitySaveMode();
             saveMode.setSaveStyle("FAST_WEB_VIEW");
             Document outFastWebView = pdfUt.setSaveMode(inDoc, saveMode, true);
 
             //Pass the document that is saved as 'Fast
             //Web View'  to the Encryption service
             EncryptionServiceClient encryptClient = new EncryptionServiceClient(myFactory);
 
             //Create a PasswordEncryptionOptionSpec object that
             //stores encryption run-time values
             PasswordEncryptionOptionSpec passSpec = new PasswordEncryptionOptionSpec();
 
             //Specify the PDF document resource to encrypt
             passSpec.setEncryptOption(PasswordEncryptionOption.ALL);
 
             //Specify the permission associated with the password
             List encrypPermissions = new ArrayList();
             encrypPermissions.add(PasswordEncryptionPermission.PASSWORD_EDIT_EXTRACT);
             encrypPermissions.add(PasswordEncryptionPermission.PASSWORD_EDIT_FORM_FILL);
             passSpec.setPermissionsRequested(encrypPermissions);
 
             //Specify the Acrobat version
             passSpec.setCompatability(PasswordEncryptionCompatability.ACRO_7);
 
             //Specify the password values
             passSpec.setDocumentOpenPassword("OpenPassword");
             passSpec.setPermissionPassword("PermissionPassword");
 
             //Encrypt the PDF document
             Document encryptDoc = encryptClient.encryptPDFUsingPassword(inDoc,passSpec);
 
             //Save the encrypted document that is saved as FAST_WEB_VIEW
             //as a PDF file named FastWebViewLoan.pdf
             File pdfFile = new File("C:\\Adobe\FastWebViewLoan.pdf");
             encryptDoc.copyToFile(pdfFile);
 
             // Inspect the document?s save option
             PDFUtilitySaveMode verifySaveMode = pdfUt.getSaveMode(outFastWebView);
             String verifySaveStyle = verifySaveMode.getSaveStyle();
             System.out.println("The save mode is " + verifySaveStyle);
         }
         catch (Exception e)
         {
             System.out.println("Error occurred: " + e.getMessage());
         }
     }
 }
 
```

## 빠른 시작(SOAP 모드):Java API {#quick-start-soap-mode-converting-a-document-to-a-pdf-a-2b-document-using-the-java-api}를 사용하여 문서를 PDF/A-2b 문서로 변환

다음 Java 코드 예제에서는 *Loan.pdf*&#x200B;라는 PDF 문서를 *LoanArchive.pdf*&#x200B;라는 PDF 파일로 저장한 PDF/A-2b 문서로 변환합니다. ([문서를 PDF/A 문서로 변환](/help/forms/developing/pdf-a-documents.md#converting-documents-to-pdf-a-documents) 참조)

```java
/*
 * This Java Quick Start uses the SOAP mode and contains the following JAR files
 * in the class path:
 * 1. adobe-docconverter-client.jar
 * 2. adobe-livecycle-client.jar
 * 3. adobe-usermanager-client.jar
 *
 * These JAR files are located in the following path:
 * <install directory>/Adobe/Adobe_Experience_Manager_forms/sdk/client-libs/common
 *
 * <install directory>/Adobe/Adobe_Experience_Manager_forms/sdk/client-libs/jboss
 *
 * <install directory>/Adobe/Adobe_Experience_Manager_forms/jboss/bin/client
 *
 * If you want to invoke a remote AEM Forms instance and there is a
 * firewall between the client application and AEM Forms, then it is
 * recommended that you use the SOAP mode. When using the SOAP mode,
 * you have to include additional JAR files located in the following
 * path
 * <install directory>/Adobe/Adobe_Experience_Manager_forms/sdk/client-libs/thirdparty
 *
 * For information about the SOAP
 * mode and the additional JAR files that need to be included,
 * see "Setting connection properties" in Programming
 * with AEM Forms
 *
 * For complete details about the location of the AEM Forms JAR files,
 * see "Including AEM Forms library files" in Programming
 * with AEM Forms
 */
import java.util.*;
import java.io.File;
import java.io.FileInputStream;
import com.adobe.idp.Document;
import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
import com.adobe.livecycle.docconverter.client.DocConverterServiceClient;
import com.adobe.livecycle.docconverter.client.PDFAConversionOptionSpec;
import com.adobe.livecycle.docconverter.client.PDFAConversionResult;
import com.adobe.livecycle.docconverter.client.PDFAConversionOptionSpec.Compliance;

public class CreatePDFADocument {

    public static void main(String[] args) {
    try{
        //Set connection properties required to invoke AEM Forms
        Properties connectionProps = new Properties();
        connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://'[server]:[port]'");
        connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
        connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
        connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
        connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");

        //Create a ServiceClientFactory instance
        ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps);

        //Create a DocConverterServiceClient object
        DocConverterServiceClient docConverter = new DocConverterServiceClient(myFactory);

        //Reference a PDF document to convert to a PDF/A document
        FileInputStream myPDF = new FileInputStream("C:\\Adobe\\Loan.pdf");
        Document inDoc = new Document(myPDF);

        //Create a PDFAConversionOptionSpec object and set
        //tracking information
        PDFAConversionOptionSpec spec = new PDFAConversionOptionSpec();
        spec.setLogLevel("FINE");
        spec.setCompliance(Compliance.PDFA_2B);

        //Convert the PDF document to a PDF/A document
        PDFAConversionResult result =  docConverter.toPDFA(inDoc,spec);

        //Save the PDF/A file
        Document pdfADoc= result.getPDFADocument();
        File pdfAFile = new File("C:\\Adobe\\LoanArchive.pdf");
        pdfADoc.copyToFile(pdfAFile);
   }catch (Exception e) {
        e.printStackTrace();
    }
  }
}
```

## 빠른 시작(SOAP 모드):PDF 문서 기밀 정보 가리기 {#quick-start-soap-mode-sanitizing-pdf-documents}

다음 Java 코드 예제에서는 *Loan.pdf*&#x200B;라는 PDF 문서를 정리합니다.

```java
/*
 * This Java Quick Start uses the SOAP mode and contains the following JAR files
 * in the class path:
 * 1. adobe-docconverter-client.jar
 * 2. adobe-livecycle-client.jar
 * 3. adobe-usermanager-client.jar
 *
 * These JAR files are located in the following path:
 * <install directory>/Adobe/Adobe_Experience_Manager_forms/sdk/client-libs/common
 *
 * <install directory>/Adobe/Adobe_Experience_Manager_forms/sdk/client-libs/jboss
 *
 * <install directory>/Adobe/Adobe_Experience_Manager_forms/jboss/bin/client
 *
 * If you want to invoke a remote AEM Forms instance and there is a
 * firewall between the client application and AEM Forms, then it is
 * recommended that you use the SOAP mode. When using the SOAP mode,
 * you have to include additional JAR files located in the following
 * path
 * <install directory>/Adobe/Adobe_Experience_Manager_forms/sdk/client-libs/thirdparty
 *
 * For information about the SOAP
 * mode and the additional JAR files that need to be included,
 * see "Setting connection properties" in Programming
 * with AEM Forms
 *
 * For complete details about the location of the AEM Forms JAR files,
 * see "Including AEM Forms library files" in Programming
 * with AEM Forms
 */
import java.io.File;
import java.io.FileInputStream;
import java.util.Properties;
import com.adobe.idp.Document;
import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
import com.adobe.livecycle.pdfutility.client.PDFUtilityServiceClient;
import com.adobe.livecycle.pdfutility.client.SanitizationResult;
public class Sanitization {
    public static void main (String[] args){

        try {
            //Set connection properties required to invoke AEM Forms
            Properties connectionProps = new Properties();
            connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://'[server]:[port]'");
            connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
            connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
            connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
            connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");

          //Create a ServiceClientFactory instance
            ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps);

          //Create a PDFUtilityServiceClient object
            PDFUtilityServiceClient pdfutility = new PDFUtilityServiceClient(myFactory);

          //Reference a PDF document to Sanitize
            FileInputStream myPDF;
            myPDF = new FileInputStream("C://loan.pdf");
            Document inDoc = new Document(myPDF);

            //Sanitize the document.
            SanitizationResult result = pdfutility.sanitize(inDoc);

            //Save the Sanitized document
            if(result.isSanitizationSuccessful()){
                Document pdfADoc= result.getDocument();
                File pdfAFile = new File("C://annotations_sanitized.pdf");
                pdfADoc.copyToFile(pdfAFile);
            }
        } catch (Exception e) {
            e.printStackTrace();
        }

    }
}
```

