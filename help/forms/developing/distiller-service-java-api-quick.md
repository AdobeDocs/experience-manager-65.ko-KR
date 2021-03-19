---
title: Distiller 서비스 Java API QuickStart(SOAP)
seo-title: Distiller 서비스 Java API QuickStart(SOAP)
description: Distiller 서비스 Java API QuickStart(SOAP)
uuid: 7781f074-cea4-4109-892b-118cfad4ec36
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: 59dd61d1-c6b1-4bea-b666-4aa7897384a1
role: 개발자
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '183'
ht-degree: 0%

---


# Distiller 서비스 Java API 빠른 시작(SOAP) {#distiller-service-java-api-quickstart-soap}

Distiller® 서비스에서 Java API 빠른 시작(SOAP)을 사용할 수 있습니다.

[빠른 시작(SOAP 모드):Java API를 사용하여 PostScript 파일을 PDF 문서로 변환](distiller-service-java-api-quick.md#quick-start-soap-mode-converting-a-postscript-file-to-a-pdf-document-using-the-java-api)

AEM Forms 작업은 AEM Forms 강력한 형식의 API를 사용하여 수행할 수 있으며 연결 모드는 SOAP로 설정해야 합니다.

>[!NOTE]
>
>AEM 양식을 사용한 프로그래밍에 있는 빠른 시작은 JBoss Application Server 및 Microsoft Windows 운영 체제에 배포되는 Forms Server를 기반으로 합니다. 그러나 UNIX와 같은 다른 운영 체제를 사용하는 경우에는 Windows 관련 경로를 해당 운영 체제에서 지원되는 경로로 바꿉니다. 마찬가지로 다른 J2EE 응용 프로그램 서버를 사용하는 경우 유효한 연결 속성을 지정해야 합니다. [연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)을 참조하십시오.

## 빠른 시작(SOAP 모드):Java API {#quick-start-soap-mode-converting-a-postscript-file-to-a-pdf-document-using-the-java-api}를 사용하여 PostScript 파일을 PDF 문서로 변환

다음 코드 예제에서는 *Loan.ps*&#x200B;이라는 PostScript 파일을 *Loan.pdf*&#x200B;라는 PDF 파일로 변환합니다. ([PostScript를 PDF 문서로 변환](/help/forms/developing/converting-postscript-pdf-documents.md#converting-postscript-to-pdf-documents) 참조)

```java
 /*
     * This Java Quick Start uses the SOAP mode and contains the following JAR files
     * in the class path:
     * 1. adobe-distiller-client.jar
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
 import com.adobe.livecycle.generatepdf.client.CreatePDFResult;
 import com.adobe.idp.Document;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 import com.adobe.livecycle.distiller.client.DistillerServiceClient;

 public class JavaAPICreatePDFSoap {

     public static void main(String[] args)
     {
         try
         {
         //Set connection properties required to invoke AEM Forms using SOAP mode
         Properties connectionProps = new Properties();
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://'[server]:[port]'");
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");

         // Create a ServiceClientFactory instance
         ServiceClientFactory factory = ServiceClientFactory.createInstance(connectionProps);

         DistillerServiceClient disClient = new DistillerServiceClient(factory );

         // Get a PS file document to convert to a PDF document and populate a com.adobe.idp.Document object
         String inputFileName = "C:\\Adobe\Loan.ps";
         FileInputStream fileInputStream = new FileInputStream(inputFileName);
         Document inDoc = new Document(fileInputStream);

         //Set run-time options
         String adobePDFSettings = "Standard";
          String securitySettings = "No Security";

          //Convert a PS  file into a PDF file
         CreatePDFResult result = new CreatePDFResult();
         result = disClient.createPDF(
                 inDoc,
                 inputFileName,
                      adobePDFSettings,
                 securitySettings,
                 null,
                 null
             );

          //Get the newly created document
          Document createdDocument = result.getCreatedDocument();

          //Save the PDF file
         createdDocument.copyToFile(new File("C:\\Adobe\Loan.pdf"));
         }
         catch (Exception e) {
             e.printStackTrace();
         }
     }
 }
```
