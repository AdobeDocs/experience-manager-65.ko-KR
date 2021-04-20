---
title: 서명 서비스 Java API QuickStart(SOAP)
seo-title: 서명 서비스 Java API QuickStart(SOAP)
description: 서명 서비스를 사용하여 PDF 문서에 서명 필드를 추가하고, 서명 필드 이름을 검색하고, 서명 필드를 수정하고, PDF 문서에 디지털 서명을 하고, XFA 기반 양식에 디지털 서명을 하고, PDF 문서를 인증하고, 디지털 서명을 확인하고, 여러 디지털 서명을 검증하고, 디지털 서명을 제거할 수 있습니다.
seo-description: 서명 서비스를 사용하여 PDF 문서에 서명 필드를 추가하고, 서명 필드 이름을 검색하고, 서명 필드를 수정하고, PDF 문서에 디지털 서명을 하고, XFA 기반 양식에 디지털 서명을 하고, PDF 문서를 인증하고, 디지털 서명을 확인하고, 여러 디지털 서명을 검증하고, 디지털 서명을 제거할 수 있습니다.
uuid: ae6adf23-b119-45f6-bd57-73d8d9ca8ecb
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: 07fffbd5-5430-4abc-b532-0840ecc7b1b0
role: Developer
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '888'
ht-degree: 0%

---


# 서명 서비스 Java API 빠른 시작(SOAP) {#signature-service-java-api-quickstart-soap}

서명 서비스에 대해 Java API 빠른 시작(SOAP)을 사용할 수 있습니다.

[빠른 시작(SOAP 모드):Java API를 사용하여 PDF 문서에 서명 필드 추가](signature-service-java-api-quick.md#quick-start-soap-mode-adding-a-signature-field-to-a-pdf-document-using-the-java-api)

[빠른 시작(SOAP 모드):Java API를 사용하여 서명 필드 이름 검색](signature-service-java-api-quick.md#quick-start-soap-mode-retrieving-signature-field-names-using-the-java-api)

[빠른 시작(SOAP 모드):Java API를 사용하여 서명 필드 수정](signature-service-java-api-quick.md#quick-start-soap-mode-modifying-a-signature-field-using-the-java-api)

[빠른 시작(SOAP 모드):Java API를 사용하여 PDF 문서에 디지털 서명](signature-service-java-api-quick.md#quick-start-soap-mode-digitally-signing-a-pdf-document-using-the-java-api)

[빠른 시작(SOAP 모드):Java API를 사용하여 XFA 기반 양식에 디지털 서명](signature-service-java-api-quick.md#quick-start-soap-mode-digitally-signing-a-xfa-based-form-using-the-java-api)

[빠른 시작(SOAP 모드):Java API를 사용하여 PDF 문서 인증](signature-service-java-api-quick.md#quick-start-soap-mode-certifying-a-pdf-document-using-the-java-api)

[빠른 시작(SOAP 모드):Java API를 사용하여 디지털 서명 확인](signature-service-java-api-quick.md#quick-start-soap-mode-verifying-a-digital-signature-using-the-java-api)

[빠른 시작(SOAP 모드):Java API를 사용하여 여러 디지털 서명 확인](signature-service-java-api-quick.md#quick-start-soap-mode-verifying-multiple-digital-signatures-using-the-java-api)

[빠른 시작(SOAP 모드):Java API를 사용하여 디지털 서명 제거](signature-service-java-api-quick.md#quick-start-soap-mode-removing-a-digital-signature-using-the-java-api)

AEM Forms 작업은 AEM Forms 강력한 형식의 API를 사용하여 수행할 수 있으며 연결 모드는 SOAP로 설정해야 합니다.

>[!NOTE]
>
>AEM Forms을 사용한 프로그래밍에 있는 빠른 시작은 JBoss Application Server 및 Microsoft Windows 운영 체제에 배포되는 Forms 서버를 기반으로 합니다. 그러나 UNIX와 같은 다른 운영 체제를 사용하는 경우에는 Windows 관련 경로를 해당 운영 체제에서 지원되는 경로로 바꿉니다. 마찬가지로 다른 J2EE 응용 프로그램 서버를 사용하는 경우 유효한 연결 속성을 지정해야 합니다. [연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)을 참조하십시오.

## 빠른 시작(SOAP 모드):Java API {#quick-start-soap-mode-adding-a-signature-field-to-a-pdf-document-using-the-java-api}을 사용하여 PDF 문서에 서명 필드 추가

다음 Java 코드 예제에서는 *SignatureField1*&#x200B;이라는 서명 필드를 *Loan.pdf*&#x200B;라는 PDF 파일을 기반으로 하는 PDF 문서에 추가합니다. 새 서명 필드가 포함된 PDF 문서는 *LoanSig.pdf*&#x200B;라는 PDF 파일로 저장됩니다. ([서명 필드 추가](/help/forms/developing/digitally-signing-certifying-documents.md#adding-signature-fields)를 참조하십시오.)

```java
 /*
     * This Java Quick Start uses the SOAP mode and contains the following JAR files
     * in the class path:
     * 1. adobe-signatures-client.jar
     * 2. adobe-livecycle-client.jar
     * 3. adobe-usermanager-client.jar
    * 4. activation.jar (required for SOAP mode)
     * 5. axis.jar (required for SOAP mode)
     * 6. commons-codec-1.3.jar (required for SOAP mode)
     * 7.  commons-collections-3.1.jar  (required for SOAP mode)
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
 import java.util.*;
 import java.io.File;
 import java.io.FileInputStream;
 import com.adobe.livecycle.signatures.client.*;
 import com.adobe.livecycle.signatures.client.types.*;
 import com.adobe.idp.Document;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 
 public class AddSignatureFieldSOAP {
 
     public static void main(String[] args) {
 
         try
         {
          //Set connection properties required to invoke AEM Forms using SOAP mode
          Properties connectionProps = new Properties();
          connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://'[server]:[port]'");
          connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
          connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
          connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
          connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
 
           //Create a ServiceClientFactory instance
           ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps);
 
           //Create a SignatureServiceClient object
           SignatureServiceClient signClient = new SignatureServiceClient(myFactory);
 
           //Specify a PDF document to which a signature field is added
           FileInputStream fileInputStream = new FileInputStream("C:\\Adobe\Loan.pdf");
           Document inDoc = new Document (fileInputStream);
 
           //Specify the name of the signature field
           String fieldName = "SignatureField1";
 
           //Create a  PositionRectangle object that specifies
           //the signature fields location
           PositionRectangle post = new  PositionRectangle(193,47,133,12);
 
           //Specify the page number that will contain the signature field
           java.lang.Integer pageNum = new java.lang.Integer(1);
 
           //Add a signature field to the PDF document
           Document sigFieldPDF = signClient.addSignatureField(
              inDoc,
              fieldName,
              pageNum,
              post,
              null,
              null);
 
           //Save the PDF document that contains the signature field
           File outFile = new File("C:\\Adobe\LoanSig.pdf");
           sigFieldPDF.copyToFile(outFile);
             }
 
         catch (Exception ee)
             {
                 ee.printStackTrace();
             }
     }
 }
 
 
```

## 빠른 시작(SOAP 모드):Java API {#quick-start-soap-mode-retrieving-signature-field-names-using-the-java-api}를 사용하여 서명 필드 이름을 검색하는 중

다음 Java 코드 예제에서는 *LoanSig.pdf*&#x200B;라는 PDF 문서에 있는 서명 필드의 이름을 검색합니다. ([서명 필드 이름 검색](/help/forms/developing/digitally-signing-certifying-documents.md#retrieving-signature-field-names) 참조)

```java
 /*
     * This Java Quick Start uses the SOAP mode and contains the following JAR files
     * in the class path:
     * 1. adobe-signatures-client.jar
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
 import java.util.*;
 import java.io.FileInputStream;
 import com.adobe.livecycle.signatures.client.*;
 import com.adobe.livecycle.signatures.client.types.*;
 import com.adobe.idp.Document;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 
 public class GetSignatureFieldsSOAP {
 
 public static void main(String[] args) {
     try
     {
         //Set connection properties required to invoke AEM Forms using SOAP mode
         Properties connectionProps = new Properties();
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://'[server]:[port]'");
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
 
         //Create a ServiceClientFactory instance
         ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps);
 
         //Create a SignatureServiceClient object
         SignatureServiceClient signClient = new SignatureServiceClient(myFactory);
 
         //Specify a PDF document that contains signature fields
         FileInputStream fileInputStream = new FileInputStream("C:\\Adobe\LoanSig.pdf");
         Document inDoc = new Document (fileInputStream);
 
         //Retrieve the name of the document’s signature fields
         List fieldNames = signClient.getSignatureFieldList(inDoc);
 
         //Obtain the name of each signature field by iterating through the
         //List object
         Iterator iter = fieldNames.iterator();
         int i = 0 ;
         String fieldName="";
         while (iter.hasNext()) {
             PDFSignatureField signatureField = (PDFSignatureField)iter.next();
             fieldName = signatureField.getName();
             System.out.println("The name of the signature field is " +fieldName);
             i++;
              }
         }
         catch (Exception ee)
         {
             ee.printStackTrace();
         }
     }
 }
```

## 빠른 시작(SOAP 모드):Java API {#quick-start-soap-mode-modifying-a-signature-field-using-the-java-api}을 사용하여 서명 필드 수정

다음 Java 코드 예제에서는 서명이 서명 필드에 적용될 때 양식의 모든 필드를 잠가 SignatureField1이라는 서명 필드를 수정하고 변경 사항이 허용되지 않도록 합니다. 서명 서비스가 수정된 서명 필드가 포함된 PDF 문서를 반환하면 PDF 문서가 RoanSig.pdf라는 PDF 파일로 저장됩니다. (이 예는 Signature 서비스에 전달된 PDF 파일을 덮어씁니다.) ([서명 필드 수정](/help/forms/developing/digitally-signing-certifying-documents.md#modifying-signature-fields) 참조)

```java
 /*
     * This Java Quick Start uses the SOAP mode and contains the following JAR files
     * in the class path:
     * 1. adobe-signatures-client.jar
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
 
 import java.util.*;
 import java.io.File;
 import java.io.FileInputStream;
 import com.adobe.livecycle.signatures.client.*;
 import com.adobe.livecycle.signatures.client.types.*;
 import com.adobe.idp.Document;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 
 public class ModifySignatureFieldSOAP {
 
     public static void main(String[] args) {
 
     try
     {
         //Set connection properties required to invoke AEM Forms using SOAP mode
         Properties connectionProps = new Properties();
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://'[server]:[port]'");
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
 
         //Create a ServiceClientFactory instance
         ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps);
 
         //Create a SignatureServiceClient object
         SignatureServiceClient signClient = new SignatureServiceClient(myFactory);
 
         //Specify a PDF document that contains a signature field to modify
         FileInputStream fileInputStream = new FileInputStream("C:\\Adobe\LoanSig.pdf");
         Document inDoc = new Document (fileInputStream);
 
         //Specify the name of the signature field
         String fieldName = "SignatureField1";
 
         //Create a PDFSignatureFieldProperties
         PDFSignatureFieldProperties fieldProperties = new PDFSignatureFieldProperties();
 
          //Create a PDFSeedValueOptionSpec object that stores
          //seed value dictionary information.
          PDFSeedValueOptionSpec seedOptionsSpec = new PDFSeedValueOptionSpec();
 
          //Disallow changes to the PDF document. Any change to the document invalidates
          //the signature
          seedOptionsSpec.setMdpValue(MDPPermissions.NoChanges);
 
          //Create a FieldMDPOptionSpec object that stores
          //signature field lock dictionary information.
          FieldMDPOptionSpec fieldMDPOptionsSpec = new FieldMDPOptionSpec();
 
          //Lock all fields in the PDF document
          fieldMDPOptionsSpec.setAction(FieldMDPAction.ALL);
 
          //Set dictionary information
          fieldProperties.setSeedValue(seedOptionsSpec);
          fieldProperties.setFieldMDP(fieldMDPOptionsSpec);
 
          //Modify the signature field
          Document modSignatureField =  signClient.modifySignatureField(inDoc,fieldName,fieldProperties);
 
          //Save the PDF document that contains modified signature field
          File file = new File("C:\\Adobe\LoanSig.pdf");
          modSignatureField.copyToFile(file);
 
     }
     catch (Exception ee)
       {
         ee.printStackTrace();
       }
     }
 }
 
```

## 빠른 시작(SOAP 모드):Java API {#quick-start-soap-mode-digitally-signing-a-pdf-document-using-the-java-api}을 사용하여 PDF 문서에 디지털 서명

다음 Java 코드 예제에서는 *LoanSig.pdf*&#x200B;라는 PDF 파일을 기반으로 하는 PDF 문서에 디지털 서명을 합니다. 보안 자격 증명에 대해 지정된 별칭은 안전하며 해지 확인이 수행됩니다. CRL 또는 OCSP 서버 정보가 지정되지 않았으므로 PDF 문서에 디지털 서명하는 데 사용되는 인증서에서 서버 정보를 가져옵니다. 서명된 문서는 *LoanSigned.pdf*&#x200B;라는 PDF 파일로 저장됩니다. (PDF 문서](/help/forms/developing/digitally-signing-certifying-documents.md#digitally-signing-pdf-documents)에 디지털 서명 참조)[

```java
 /*
     * This Java Quick Start uses the SOAP mode and contains the following JAR files
     * in the class path:
     * 1. adobe-signatures-client.jar
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
 import java.util.*;
 import java.io.File;
 import java.io.FileInputStream;
 import com.adobe.livecycle.signatures.client.*;
 import com.adobe.livecycle.signatures.client.types.*;
 import com.adobe.livecycle.signatures.pki.client.types.common.HashAlgorithm;
 import com.adobe.idp.Document;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 
 public class SignDocumentSOAP {
 
 public static void main(String[] args) {
 
     try
     {
       //Set connection properties required to invoke AEM Forms using SOAP mode
         Properties connectionProps = new Properties();
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://'[server]:[port]'");
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
 
       //Create a ServiceClientFactory instance
       ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps);
 
       //Create a SignatureServiceClient object
       SignatureServiceClient signClient = new SignatureServiceClient(myFactory);
 
       //Specify a PDF document to sign
       FileInputStream fileInputStream = new FileInputStream("C:\\Adobe\LoanSig.pdf");
       Document credDoc = new Document (fileInputStream);
 
       //Specify the name of the signature field
       String fieldName = "SignatureField1";
 
       //Create a Credential object
       Credential myCred = Credential.getInstance("secure");
 
       //Specify the reason to sign the document
       String reason = "The document was reviewed";
 
       //Specify the location of the signer
       String location  = "New York HQ";
 
       //Specify contact information
       String contactInfo = "Tony Blue";
 
       //Create a PDFSignatureAppearanceOptions object
       //and show date information
       PDFSignatureAppearanceOptionSpec appear = new  PDFSignatureAppearanceOptionSpec();
       appear.setShowDate(true);
       appear.setShowReason(true);
 
       //Set revocation checking to false
       java.lang.Boolean revCheck = new Boolean(true);
 
       //Create an OCSPOptionSpec object to pass to the sign method
            OCSPOptionSpec ocspSpec = new OCSPOptionSpec();
 
            //Create a CRLOptionSpec object to pass to the sign method
            CRLOptionSpec crlSpec = new CRLOptionSpec();
 
            //Create a TSPOptionSpec object to pass to the sign method
            TSPOptionSpec tspSpec = new TSPOptionSpec();
 
       //Sign the PDF document
       Document signedDoc = signClient.sign(
          credDoc,
          fieldName,
          myCred,
          HashAlgorithm.SHA1,
          reason,
          location,
          contactInfo,
          appear,
          revCheck,
         ocspSpec,
              crlSpec,
              tspSpec);
 
       //Save the signed PDF document
       File outFile = new File("C:\\Adobe\LoanSigned.pdf");
       signedDoc.copyToFile (outFile);
       }
 
     catch (Exception ee)
       {
         ee.printStackTrace();
       }
       }
 }
 
 
```

## 빠른 시작(SOAP 모드):Java API {#quick-start-soap-mode-digitally-signing-a-xfa-based-form-using-the-java-api}를 사용하여 XFA 기반 양식에 디지털 서명

다음 Java 코드 예제에서는 Forms 서비스를 통해 렌더링되는 대화형 양식을 서명합니다. Forms 서비스에서 반환되는 `com.adobe.idp.Document` 인스턴스가 서명 서비스로 전달됩니다. 서명된 대화형 양식은 *LoanXFASigned.pdf*&#x200B;라는 PDF 파일로 저장됩니다.

```java
 /*
     * This Java Quick Start uses the SOAP mode and contains the following JAR files
     * in the class path:
     * 1. adobe-signatures-client.jar
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
 import java.util.*;
 import java.io.File;
 import java.io.FileInputStream;
 
 import com.adobe.livecycle.formsservice.client.FormsResult;
 import com.adobe.livecycle.formsservice.client.FormsServiceClient;
 import com.adobe.livecycle.formsservice.client.PDFFormRenderSpec;
 import com.adobe.livecycle.signatures.client.*;
 import com.adobe.livecycle.signatures.client.types.*;
 import com.adobe.livecycle.signatures.pki.client.types.common.HashAlgorithm;
 import com.adobe.idp.Document;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 
 public class SignXFAFormsSOAP {
 
 public static void main(String[] args) {
 
     try
     {
 
      //Set connection properties required to invoke AEM Forms using SOAP mode
      Properties connectionProps = new Properties();
      connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://'[server]:[port]'");
      connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
      connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
      connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
      connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
 
      //Create a ServiceClientFactory instance
      ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps);
 
      //Get the XFA form to sign
      Document myForm = GetForm(myFactory);
 
     //Sign the XFA form
     SignXFA(myForm,myFactory);
     }
 
     catch (Exception ee)
       {
         ee.printStackTrace();
       }
       }
 
 
 //Creates an interactive PDF form based on a XFA form
 private static Document GetForm(ServiceClientFactory myFactory)
 {
 
     try
     {
     //Create a FormsServiceClient object
     FormsServiceClient formsClient = new FormsServiceClient(myFactory);
 
     //Specify a PDF document to sign
     FileInputStream fileInputStream = new FileInputStream("C:\\Adobe\LoanSigXFA.pdf");
     Document xfaForm = new Document (fileInputStream);
 
     //Retrieve form data
     FileInputStream cData = new FileInputStream("C:\\Adobe\Loan.xml");
     Document oInputData = new Document(cData);
 
     //Cache the PDF form
     PDFFormRenderSpec pdfFormRenderSpec = new PDFFormRenderSpec();
     pdfFormRenderSpec.setGenerateServerAppearance(true);
 
     //Invoke the renderPDFForm2 method
     FormsResult formOut = formsClient.renderPDFForm2(
             xfaForm,               //formQuery
             oInputData,             //inDataDoc
             pdfFormRenderSpec,      //PDFFormRenderSpec
             null,                //urlSpec
             null            //attachments
             );
 
     //Create a Document object that stores form data
     Document myForm = formOut.getOutputContent();
     return myForm;
 }
 
     catch (Exception ee)
       {
         ee.printStackTrace();
       }
     return null;
 
 }
 
 //Sign the PDF document
 private static void SignXFA(Document doc, ServiceClientFactory myFactory)
 {
     try
     {
 
     //Create a SignatureServiceClient object
      SignatureServiceClient signClient = new SignatureServiceClient(myFactory);
 
      //Specify the name of the signature field
      String fieldName = "SignatureField1";
 
      //Create a Credential object
      Credential myCred = Credential.getInstance("secure");
 
      //Specify the reason to sign the document
      String reason = "The document was reviewed";
 
      //Specify the location of the signer
      String location  = "New York HQ";
 
      //Specify contact information
      String contactInfo = "Tony Blue";
 
      //Create a PDFSignatureAppearanceOptions object
      //and show date information
      PDFSignatureAppearanceOptionSpec appear = new  PDFSignatureAppearanceOptionSpec();
      appear.setShowDate(true);
      appear.setShowReason(true);
 
      //Set revocation checking to false
      java.lang.Boolean revCheck = new Boolean(true);
 
      //Create an OCSPOptionSpec object to pass to the sign method
      OCSPOptionSpec ocspSpec = new OCSPOptionSpec();
 
      //Create a CRLOptionSpec object to pass to the sign method
      CRLOptionSpec crlSpec = new CRLOptionSpec();
 
      //Create a TSPOptionSpec object to pass to the sign method
      TSPOptionSpec tspSpec = new TSPOptionSpec();
 
      //Sign the PDF document
       Document signedDoc = signClient.sign(
          doc,
          fieldName,
          myCred,
          HashAlgorithm.SHA1,
          reason,
          location,
          contactInfo,
          appear,
          revCheck,
         ocspSpec,
         crlSpec,
         tspSpec);
 
       //Save the signed PDF document
       File outFile = new File("C:\\Adobe\LoanXFASigned.pdf");
       signedDoc.copyToFile (outFile);
 }
 
     catch (Exception ee)
       {
         ee.printStackTrace();
       }
      }
 }
 
```

## 빠른 시작(SOAP 모드):Java API {#quick-start-soap-mode-certifying-a-pdf-document-using-the-java-api}을 사용하여 PDF 문서 인증

다음 Java 코드 예는 *LoanSig.pdf*&#x200B;라는 PDF 파일을 기반으로 하는 PDF 문서를 인증합니다. 보안 자격 증명에 대해 지정된 별칭이 안전하며 해지 검사를 수행하지 않습니다. 인증된 문서는 *LoanCertified.pdf*&#x200B;라는 PDF 파일로 저장됩니다. ([PDF 문서 인증](/help/forms/developing/digitally-signing-certifying-documents.md#certifying-pdf-documents)을 참조하십시오.)

```java
 /*
     * This Java Quick Start uses the SOAP mode and contains the following JAR files
     * in the class path:
     * 1. adobe-signatures-client.jar
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
 import java.util.*;
 import java.io.File;
 import java.io.FileInputStream;
 import com.adobe.livecycle.signatures.client.*;
 import com.adobe.livecycle.signatures.client.types.*;
 import com.adobe.livecycle.signatures.pki.client.types.common.HashAlgorithm;
 import com.adobe.idp.Document;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 
 public class CertifyDocumentSOAP {
 
     public static void main(String[] args) {
     try
     {
         //Set connection properties required to invoke AEM Forms using SOAP mode
         Properties connectionProps = new Properties();
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://'[server]:[port]'");
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
 
       //Create a ServiceClientFactory instance
       ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps);
 
       //Create a SignatureServiceClient object
       SignatureServiceClient signClient = new SignatureServiceClient(myFactory);
 
       //Specify a PDF document to certify
       FileInputStream fileInputStream = new FileInputStream("C:\\Adobe\LoanSig.pdf");
       Document credDoc = new Document (fileInputStream);
 
       //Specify the name of the signature field
       String fieldName = "SignatureField1";
 
       //Create a Credential object
       Credential myCred = Credential.getInstance("secure");
 
       //Specify the reason to sign the document
       String reason = "The document was reviewed";
 
       //Specify the location of the signer
       String location  = "My company";
 
       //Specify contact information
           String contactInfo = "New York, New York";
 
       //Create a PDFSignatureAppearanceOptions object and show date information
       PDFSignatureAppearanceOptionSpec appear = new  PDFSignatureAppearanceOptionSpec();
       appear.setShowDate(true);
 
       //Set revocation checking to false
            java.lang.Boolean revCheck = new Boolean(false);
 
            //Set locking to false
            java.lang.Boolean lockField = new Boolean(false);
 
            //Specify a legalAttestation value
            String msg = "Any change to this document will invalidate the certificate";
 
            //Create objects to pass to the certify method
            OCSPOptionSpec ocspSpec = new OCSPOptionSpec();
            CRLOptionSpec crlSpec = new CRLOptionSpec();
            TSPOptionSpec tspSpec = new TSPOptionSpec();
 
            //Certify the PDF document
            Document signedDoc = signClient.certify(
               credDoc,
               fieldName,
               myCred,
               HashAlgorithm.SHA1,
               reason,
               location,
               contactInfo,
               MDPPermissions.NoChanges,
               msg,
               appear,
               revCheck,
               lockField,
              ocspSpec,
              crlSpec,
              tspSpec);
 
         //Save the signed PDF document
              File outFile = new File("C:\\Adobe\LoanCertified.pdf");
              signedDoc.copyToFile (outFile);
         }
 
     catch (Exception ee)
         {
         ee.printStackTrace();
         }
     }
 }
```

## 빠른 시작(SOAP 모드):Java API {#quick-start-soap-mode-verifying-a-digital-signature-using-the-java-api}을 사용하여 디지털 서명 확인

다음 Java 코드 예제에서는 LoanSigned.pdf라는 PDF 파일을 기반으로 서명된 PDF 문서에 있는 디지털 서명을 확인합니다. 확인 시간은 현재 시간으로 설정되며 취소 확인 옵션은 최선의 노력으로 설정되어 있습니다. ([디지털 서명 확인](#verifying-digital-signatures)을 참조하십시오.)

```java
 /*
     * This Java Quick Start uses the following JAR files
     * 1. adobe-signatures-client.jar
     * 2. adobe-livecycle-client.jar
     * 3. adobe-usermanager-client.jar
    * 4. activation.jar (required for SOAP mode)
     * 5. axis.jar (required for SOAP mode)
     * 6. commons-codec-1.3.jar (required for SOAP mode)
     * 7.  commons-collections-3.1.jar  (required for SOAP mode)
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
 import java.util.*;
 import java.io.FileInputStream;
 import com.adobe.livecycle.signatures.client.*;
 import com.adobe.livecycle.signatures.client.types.*;
 import com.adobe.livecycle.signatures.pki.client.types.common.RevocationCheckStyle;
 import com.adobe.idp.Document;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 
 public class VerifySignatureSOAP{
 
     public static void main(String[] args) {
 
     try
     {
       //Set connection properties required to invoke AEM Forms using SOAP mode
       Properties connectionProps = new Properties();
       connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://'[server]:[port]'");
      connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
       connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
       connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
       connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
 
       //Create a ServiceClientFactory instance
       ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps);
 
       //Create a SignatureServiceClient object
       SignatureServiceClient signClient = new SignatureServiceClient(myFactory);
 
       //Specify a PDF document that contains a digital signature
       FileInputStream fileInputStream = new FileInputStream("C:\\Adobe\LoanSigned.pdf");
       Document inDoc = new Document (fileInputStream);
 
       //Specify the name of the signature field
       String fieldName = "SignatureField1";
 
       //Create a PKIOptions object that contains PKI run-time options
       PKIOptions pkiOptions = new PKIOptions();
       pkiOptions.setVerificationTime(VerificationTime.CURRENT_TIME);
       pkiOptions.setRevocationCheckStyle(RevocationCheckStyle.BestEffort);
 
       //Verify the digital signature
       PDFSignatureVerificationInfo  signInfo = signClient.verify2(
          inDoc,
          fieldName,
          pkiOptions,
          null);
 
       //Get the Signature Status
       SignatureStatus sigStatus = signInfo.getStatus();
       String myStatus="";
 
       //Determine the status of the signature
       if (sigStatus == SignatureStatus.DynamicFormSignatureUnknown)
              myStatus = "The signatures located in the dynamic PDF form are unknown";
          else if (sigStatus == SignatureStatus.DocumentSignatureUnknown)
              myStatus = "The signatures located in the PDF document are unknown";
          else if (sigStatus == SignatureStatus.CertifiedDynamicFormSignatureTamper)
              myStatus = "The signatures located in a certified PDF form are valid";
          else if (sigStatus == SignatureStatus.SignedDynamicFormSignatureTamper)
              myStatus = "The signatures located in a signed dynamic PDF form are valid";
          else if (sigStatus == SignatureStatus.CertifiedDocumentSignatureTamper)
              myStatus = "The signatures located in a certified PDF document are valid";
          else if (sigStatus == SignatureStatus.SignedDocumentSignatureTamper)
              myStatus = "The signatures located in a signed PDF document are valid";
          else if (sigStatus == SignatureStatus.SignatureFormatError)
              myStatus = "The format of a signature in a signed document is invalid";
          else if (sigStatus == SignatureStatus.DynamicFormSigNoChanges)
              myStatus = "No changes were made to the signed dynamic PDF form";
          else if (sigStatus == SignatureStatus.DocumentSigNoChanges)
              myStatus = "No changes were made to the signed PDF document";
          else if (sigStatus == SignatureStatus.DynamicFormCertificationSigNoChanges)
              myStatus = "No changes were made to the certified dynamic PDF form";
          else if (sigStatus == SignatureStatus.DocumentCertificationSigNoChanges)
              myStatus = "No changes were made to the certified PDF document";
          else if (sigStatus == SignatureStatus.DocSigWithChanges)
              myStatus = "There were changes to a signed PDF document";
         else if (sigStatus == SignatureStatus.CertificationSigWithChanges)
              myStatus = "There were changes made to the PDF document.";
 
       //Get the signature type
       SignatureType sigType = signInfo.getSignatureType();
       String myType = "";
 
       if (sigType.getType() == PDFSignatureType.AUTHORSIG)
              myType="Certification";
       else if(sigType.getType() == PDFSignatureType.RECIPIENTSIG)
              myType="Recipient";
 
       //Get the identity of the signer
       IdentityInformation signerId = signInfo.getSigner();
       String signerMsg = "";
 
      if (signerId.getStatus() == IdentityStatus.UNKNOWN)
          signerMsg = "Identity Unknown";
      else if (signerId.getStatus() == IdentityStatus.TRUSTED)
          signerMsg = "Identity Trusted";
      else if (signerId.getStatus() == IdentityStatus.NOTTRUSTED)
          signerMsg = "Identity Not Trusted";
 
      //Get the Signature properties returned by the Signature service
      SignatureProperties sigProps = signInfo.getSignatureProps();
      String signerName =  sigProps.getSignerName();
 
     System.out.println("The status of the signature is: "+myStatus +". The signer identity is "+signerMsg +". The signature type is "+myType +". The name of the signer is "+signerName+".");
     }
     catch (Exception ee)
     {
         ee.printStackTrace();
     }
      }
 }
 
 
```

## 빠른 시작(SOAP 모드):Java API {#quick-start-soap-mode-verifying-multiple-digital-signatures-using-the-java-api}를 사용하여 여러 디지털 서명 확인

다음 Java 코드 예제에서는 LoanAllSigs.pdf라는 PDF 파일을 기반으로 서명된 PDF 문서에 있는 여러 디지털 서명을 확인합니다. 확인 시간은 현재 시간으로 설정되며 취소 확인 옵션은 최선의 노력으로 설정되어 있습니다. ([여러 디지털 서명 확인](signature-service-java-api-quick.md#quick-start-soap-mode-verifying-multiple-digital-signatures-using-the-java-api)을 참조하십시오.)

```java
 /*
     * This Java Quick Start uses the SOAP mode and contains the following JAR files
     * in the class path:
     * 1. adobe-signatures-client.jar
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
 import java.util.*;
 import java.io.FileInputStream;
 import com.adobe.livecycle.signatures.client.*;
 import com.adobe.livecycle.signatures.client.types.*;
 import com.adobe.livecycle.signatures.pki.client.types.common.RevocationCheckStyle;
 import com.adobe.idp.Document;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 
 public class VerifyAllSignaturesSOAP{
 
     public static void main(String[] args) {
 
     try
     {
       //Set connection properties required to invoke AEM Forms using SOAP mode
       Properties connectionProps = new Properties();
       connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://'[server]:[port]'");
      connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
       connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
       connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
       connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
 
       //Create a ServiceClientFactory instance
       ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps);
 
       //Create a SignatureServiceClient object
       SignatureServiceClient signClient = new SignatureServiceClient(myFactory);
 
       //Specify a PDF document that contains multiple digital signatures
       FileInputStream fileInputStream = new FileInputStream("C:\\Adobe\LoanAllSigs.pdf");
       Document inDoc = new Document (fileInputStream);
 
       //Create a PKIOptions object that contains PKI run-time options
       PKIOptions pkiOptions = new PKIOptions();
       pkiOptions.setVerificationTime(VerificationTime.CURRENT_TIME);
       pkiOptions.setRevocationCheckStyle(RevocationCheckStyle.BestEffort);
 
       //Verify all digital signatures that are located in a PDF document
       PDFDocumentVerificationInfo  allSig = signClient.verifyPDFDocument(
          inDoc,
          pkiOptions,
          null);
 
       //Get a list of all signatures that are located in the PDF document
       List allSignatures = allSig.getVerificationInfos();
 
     //Create an Iterator object and iterate through
     //the List object
     Iterator<PDFSignatureVerificationInfo> iter = allSignatures.iterator();
 
     while (iter.hasNext()) {
            PDFSignatureVerificationInfo signInfo = (PDFSignatureVerificationInfo)iter.next();
 
            //Get the Signature Status
               SignatureStatus sigStatus = signInfo.getStatus();
               String myStatus="";
 
             //Determine the status of the signature
               if (sigStatus == SignatureStatus.DynamicFormSignatureUnknown)
                   myStatus = "The signatures located in the dynamic PDF form are unknown";
               else if (sigStatus == SignatureStatus.DocumentSignatureUnknown)
                   myStatus = "The signatures located in the PDF document are unknown";
               else if (sigStatus == SignatureStatus.CertifiedDynamicFormSignatureTamper)
                   myStatus = "The signatures located in a certified PDF form are valid";
               else if (sigStatus == SignatureStatus.SignedDynamicFormSignatureTamper)
                   myStatus = "The signatures located in a signed dynamic PDF form are valid";
               else if (sigStatus == SignatureStatus.CertifiedDocumentSignatureTamper)
                   myStatus = "The signatures located in a certified PDF document are valid";
               else if (sigStatus == SignatureStatus.SignedDocumentSignatureTamper)
                   myStatus = "The signatures located in a signed PDF document are valid";
               else if (sigStatus == SignatureStatus.SignatureFormatError)
                   myStatus = "The format of a signature in a signed document is invalid";
               else if (sigStatus == SignatureStatus.DynamicFormSigNoChanges)
                   myStatus = "No changes were made to the signed dynamic PDF form";
               else if (sigStatus == SignatureStatus.DocumentSigNoChanges)
                   myStatus = "No changes were made to the signed PDF document";
               else if (sigStatus == SignatureStatus.DynamicFormCertificationSigNoChanges)
                   myStatus = "No changes were made to the certified dynamic PDF form";
               else if (sigStatus == SignatureStatus.DocumentCertificationSigNoChanges)
                   myStatus = "No changes were made to the certified PDF document";
               else if (sigStatus == SignatureStatus.DocSigWithChanges)
                   myStatus = "There were changes to a signed PDF document";
              else if (sigStatus == SignatureStatus.CertificationSigWithChanges)
                   myStatus = "There were changes made to the PDF document.";
 
               //Get the signature type
              SignatureType sigType = signInfo.getSignatureType();
              String myType = "";
 
              if (sigType.getType() == PDFSignatureType.AUTHORSIG)
                  myType="Certification";
              else if(sigType.getType() == PDFSignatureType.RECIPIENTSIG)
                  myType="Recipient";
 
              //Get the Signature properties returned by the Signature service
              SignatureProperties sigProps = signInfo.getSignatureProps();
              String signerName =  sigProps.getSignerName();
 
             System.out.println("The status of the signature is: "+myStatus +". The signature type is "+myType +". The name of the signer is "+signerName+".");
         }
     }
     catch (Exception ee)
     {
         ee.printStackTrace();
     }
      }
 }
```

## 빠른 시작(SOAP 모드):Java API {#quick-start-soap-mode-removing-a-digital-signature-using-the-java-api}을(를) 사용하여 디지털 서명 제거

다음 Java 코드 예제에서는 *SignatureField1*&#x200B;이라는 서명 필드에서 디지털 서명을 제거합니다. 서명 필드를 포함하는 PDF 파일의 이름은 *LoanSigned.pdf*&#x200B;입니다. ([디지털 서명 제거](/help/forms/developing/digitally-signing-certifying-documents.md#removing-digital-signatures)를 참조하십시오.)

```java
 /*
     * This Java Quick Start uses the SOAP mode and contains the following JAR files
     * in the class path:
     * 1. adobe-signatures-client.jar
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
 
 import java.util.*;
 import java.io.File;
 import java.io.FileInputStream;
 import com.adobe.livecycle.signatures.client.*;
 import com.adobe.idp.Document;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 
 public class ClearSignatureFieldSOAP {
 
     public static void main(String[] args) {
 
     try
     {
         //Set connection properties required to invoke AEM Forms using SOAP mode
         Properties connectionProps = new Properties();
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://'[server]:[port]'");
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
 
         //Create a ServiceClientFactory instance
         ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps);
 
         //Create a SignatureServiceClient object
         SignatureServiceClient signClient = new SignatureServiceClient(myFactory);
 
         //Specify a PDF document that contains the signature to remove
         FileInputStream fileInputStream = new FileInputStream("C:\\Adobe\LoanSigned.pdf");
         Document inDoc = new Document (fileInputStream);
 
         //Specify the name of the signature field
         String fieldName = "SignatureField1";
 
         //Clear the signature field
         Document outPDF = signClient.clearSignatureField(inDoc,fieldName);
 
         //Save the PDF document
         File outFile = new File("C:\\Adobe\Loan.pdf");
         outPDF.copyToFile(outFile);
         }
 
     catch (Exception ee)
         {
         ee.printStackTrace();
         }
     }
 }
 
 
 
```

