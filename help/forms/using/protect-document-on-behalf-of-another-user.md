---
title: 다른 사용자를 대신하여 문서 Protect
description: AEM Forms Document Security Java SDK는 편집 권한 없이 다른 사용자를 대신하여 문서를 보호할 수 있도록 사용자 계정용 API를 제공합니다.
uuid: 76f4b30b-6d0c-4cae-98b3-334efdbf27bb
geptopics: SG_AEMFORMS/categories/working_with_document_security
discoiquuid: 7cb8140d-dd62-4659-8cc7-21361bd5d3f6
feature: Document Security
exl-id: e5c80569-d3c0-4358-9b91-b98a64d1c004
source-git-commit: 20b0d0db54dc30285c056a10032f02ba45f8baca
workflow-type: tm+mt
source-wordcount: '385'
ht-degree: 1%

---

# 다른 사용자를 대신하여 문서 Protect {#protect-a-document-on-behalf-of-another-user}

AEM Forms Document Security Java SDK는 문서 편집 권한을 획득하지 않고도 사용자 계정이 다른 사용자를 대신하여 문서를 보호할 수 있도록 하는 API를 제공합니다. API는 워크플로우 프로세스에서 또는 프로그래밍 방식으로 문서 서비스로 사용할 수 있습니다. 새 API:

* **보호 문서 사용** 대신 문서에 정책을 적용하기 위한 ProtectDocument API

  다른 사용자 계정입니다. 정책을 적용하는 데 사용되는 사용자 계정의 권한은 문서 보호로 제한됩니다. 문서를 열고 볼 수 있는 권한은 없습니다. RMSecureDocumentResult protectDocument(Document inDoc, String documentName, String policySetName, String policyName, RMLocale 로케일, 부울 bExactMatchForNames)

* **createLicenseUse** 다른 사용자 계정을 대신하여 정책에 대한 라이선스를 만들기 위한 CreateLicense API입니다. PublishLicenseDTO createLicense(String policyId, String documentName, 부울 logSecureDocEvent)
* **protectDocumentWithCoverPageUse** 다른 사용자를 대신하여 정책을 적용하고 문서에 표지를 추가하는 ProtectDocumentWithCoverPage API입니다. 정책을 적용하는 데 사용되는 사용자 계정의 권한은 문서 보호로 제한됩니다. 문서를 열고 볼 수 있는 권한은 없습니다. RMSecureDocumentResult protectDocumentWithCoverPage(Document inDoc, String documentName, String policySetName, String policyName, Document coverDoc, 부울 bExactMatchForNames)

## API를 사용하여 다른 사용자 대신 문서 보호 {#using-the-apis-to-protect-a-document-on-behalf-of-another-user}

문서를 편집할 수 있는 권한을 획득하지 않고 다른 사용자를 대신하여 문서를 보호하려면 다음 단계를 수행하십시오.

1. 정책 집합을 만듭니다. 예: PolicySet1.
1. 새로 만든 정책 집합에 정책을 만듭니다. 예: PolicySet1의 Policy1.
1. 최종 사용자 역할을 가진 Rights Management을 만듭니다. 예: User1. 새로 만든 사용자에게 Policy1로 보호된 문서를 볼 수 있는 권한을 제공합니다.
1. 새 역할 만들기. 예를 들어 Role1입니다. 새로 만든 역할에 서비스 호출 권한을 제공합니다. 새로 생성된 역할을 가진 사용자를 만듭니다. 예를 들어 User2.User2 또는 관리자를 사용하여 SDK 연결을 만들고 protectDocument 서비스를 호출할 수 있습니다.

   이제 문서를 보호하는 사용자에게 문서를 편집할 권한을 제공하지 않고 다음 샘플 코드를 실행하여 문서를 보호할 수 있습니다.

   ```java
   import java.io.File;
   import java.io.FileInputStream;
   import java.io.FileNotFoundException;
   import java.io.FileOutputStream;
   import java.io.IOException;
   import java.io.InputStream;
   import java.util.Properties;
   
   import com.adobe.edc.common.dto.PublishLicenseDTO;
   import com.adobe.edc.sdk.SDKException;
   import com.adobe.idp.Document;
   import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
   import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
   import com.adobe.livecycle.rightsmanagement.RMSecureDocumentResult;
   import com.adobe.livecycle.rightsmanagement.client.DocumentManager;
   import com.adobe.livecycle.rightsmanagement.client.RightsManagementClient;
   import com.adobe.livecycle.rightsmanagement.client.RightsManagementClient2;
   
   public class PublishAsProtectAPI {
   
   private static final String unprotectedFileName = "C:\\unprotected.pdf";
   private static final String protectedFileName = "C:\\protect.pdf";
   private static final String coverFileName = "C:\\CoverPage.pdf";
   private static final String POLICY_ID = "2EF66008-5E2D-1034-9B06-00000A292C18"; 
   
   public static void main(String[] args) {
   
   try {
   
   Properties connectionProps = new Properties();
   connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT,"http://localhost:8080");
   connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
   connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
   connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME,"administrator");
   connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD,"password");
   
   // Create a ServiceClientFactory instance
   ServiceClientFactory factory = ServiceClientFactory.createInstance(connectionProps);
   testProtectDocument(factory);
   testProtectDocumentWithCoverPage(factory);
   testProtectDocumentJavaPPL(factory);
   
   } 
   catch (Exception ex) {
   ex.printStackTrace(); }
   }
   
   private static void testProtectDocument(ServiceClientFactory factory) throws FileNotFoundException, SDKException {
   // Create a RightsManagementClient object
   RightsManagementClient rmClient = new RightsManagementClient(factory);
   // Create a Document Manager object
   DocumentManager documentManager = rmClient.getDocumentManager();
   //Reference a policy-protected PDF document from which to remove a policy
   FileInputStream is = new FileInputStream(unprotectedFileName);
   Document inPDF = new Document(is);
   long startTime = System.currentTimeMillis();
   //Remove a policy from the policy-protected PDF document
   RMSecureDocumentResult securePDF = documentManager.protectDocument(inPDF, "test", "newPolicySet", "latest", "DefaultDom", "administrator", null, true);
   System.out.println("Total Time taken for protectDocument = " + (System.currentTimeMillis() - startTime));
   //Save the unsecured PDF document
   File myFile = new File(protectedFileName);
   securePDF.getProtectedDoc().copyToFile(myFile);
   }
   
   private static void testProtectDocumentWithCoverPage(ServiceClientFactory factory) throws FileNotFoundException, SDKException {
   // Create a RightsManagementClient object
   RightsManagementClient rmClient = new RightsManagementClient(factory);
   // Create a Document Manager object
   DocumentManager documentManager = rmClient.getDocumentManager();
   //Reference a policy-protected PDF document from which to remove a policy
   FileInputStream is = new FileInputStream(unprotectedFileName);
   Document inPDF = new Document(is);
   FileInputStream coverIS = new FileInputStream(coverFileName);
   Document inCoverPDF = new Document(coverIS);
   long startTime = System.currentTimeMillis();
   //Remove a policy from the policy-protected PDF document
   RMSecureDocumentResult securePDF = documentManager.protectDocumentWithCoverPage(inPDF, "test", "newPolicySet", "latestPolicy", inCoverPDF, true);
   System.out.println("Total Time taken for Page0ProtectDocument = " + (System.currentTimeMillis() - startTime));
   //Save the unsecured PDF document
   File myFile = new File(protectedFileName);
   securePDF.getProtectedDoc().copyToFile(myFile);
   }
   
   private static PublishLicenseDTO testProtectDocumentJavaPPL (ServiceClientFactory factory) throws SDKException, FileNotFoundException, IOException {
   // Create a RightsManagementClient object
   RightsManagementClient2 rmClient2 = new RightsManagementClient2(factory);
   // Create a Document Manager object
   DocumentManager documentManager = rmClient2.getDocumentManager();
   long startTime = System.currentTimeMillis();
   PublishLicenseDTO license = documentManager.createLicense(POLICY_ID, "Out.pdf", true);
   System.out.println("Create License totalTime = " + (System.currentTimeMillis() - startTime));
   startTime = System.currentTimeMillis();
   // Reference a PDF document to which a policy is applied
   InputStream inputFileStream = new FileInputStream(unprotectedFileName);
   // Apply a policy to the PDF document
   InputStream protectPDF = rmClient2.getRightsManagementEncryptionService().protectDocument(inputFileStream, license);
   // Save the policy-protected PDF document
   File myFile = new File(protectedFileName);
   // write the inputStream to a FileOutputStream
   FileOutputStream outputStream = new FileOutputStream(myFile);
   int read = 0;
   byte[] bytes = new byte[1024];
   while ((read = protectPDF.read(bytes)) != -1) {
   outputStream.write(bytes, 0, read);
   }
   System.out.println("protectPDFDocument totalTime = " + (System.currentTimeMillis() - startTime));
   outputStream.close();
   inputFileStream.close();
   System.out.println("Document Protected Successfully");
   return license;
   }
   }
   ```
