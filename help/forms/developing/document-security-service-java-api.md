---
title: Document Security Service JavaAPI 빠른 시작(SOAP)
description: Document Security Service JavaAPI 빠른 시작(SOAP)
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
role: Developer
exl-id: 76d855cf-ebfa-487a-b1c8-755e7e45dd73
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,APIs & Integrations,AEM Forms on JEE
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '1071'
ht-degree: 0%

---

# Document Security Service Java API 빠른 시작(SOAP) {#document-security-service-javaapi-quick-start-soap}

Rights Management 서비스에는 SOAP(Java API Quick Start)를 사용할 수 있습니다.

[빠른 시작(SOAP 모드): Java API를 사용하여 정책 만들기](document-security-service-java-api.md#quick-start-soap-mode-creating-a-policy-using-the-java-api)

[빠른 시작(SOAP 모드): Java API를 사용하여 정책 수정](#quick-start-soap-mode-modifying-a-policy-using-the-java-api)

[빠른 시작(SOAP 모드): Java API를 사용하여 정책 삭제](document-security-service-java-api.md#quick-start-soap-mode-deleting-a-policy-using-the-java-api)

[빠른 시작(SOAP 모드): Java API를 사용하여 PDF 문서에 정책 적용](#quick-start-soap-mode-applying-a-policy-to-a-pdf-document-using-the-java-api)

[빠른 시작(SOAP 모드): Java API를 사용하여 PDF 문서에서 정책 제거](document-security-service-java-api.md#quick-start-soap-mode-removing-a-policy-from-a-pdf-document-using-the-java-api)

[빠른 시작(SOAP 모드): Java API를 사용하여 문서 취소](document-security-service-java-api.md#quick-start-soap-mode-revoking-a-document-using-the-java-api)

[빠른 시작(SOAP 모드): Java API를 사용하여 해지된 문서에 대한 액세스 복원](document-security-service-java-api.md#quick-start-soap-mode-reinstating-access-to-a-revoked-document-using-the-java-api)

[빠른 시작(SOAP 모드): Java API를 사용하여 정책으로 보호된 PDF 문서 검사](document-security-service-java-api.md#quick-start-soap-mode-inspecting-policy-protected-pdf-documents-using-the-java-api)

[빠른 시작(SOAP 모드): Java API를 사용하여 워터마크 만들기](document-security-service-java-api.md#quick-start-soap-mode-creating-a-pdf-watermark-using-the-java-api)

[빠른 시작(SOAP 모드): Java API를 사용하여 워터마크 수정](document-security-service-java-api.md#quick-start-soap-mode-modifying-a-watermark-using-the-java-api)

[빠른 시작(SOAP 모드): Java API를 사용하여 이벤트 검색](document-security-service-java-api.md#quick-start-soap-mode-searching-for-events-using-the-java-api)

[빠른 시작(SOAP 모드): Java API를 사용하여 Word 문서에서 정책 제거](document-security-service-java-api.md#quick-start-soap-mode-removing-a-policy-from-a-word-document-using-the-java-api)

AEM Forms 작업은 AEM Forms 강력한 형식의 API를 사용하여 수행할 수 있으며 연결 모드를 SOAP으로 설정해야 합니다.

>[!NOTE]
>
>AEM Forms을 사용한 프로그래밍의 빠른 시작은 Forms 서버 운영 체제를 기반으로 합니다. 그러나 UNIX와 같은 다른 운영 체제를 사용하는 경우에는 Windows 특정 경로를 해당 운영 체제에서 지원하는 경로로 바꿉니다. 마찬가지로 다른 J2EE 응용 프로그램 서버를 사용하는 경우 유효한 연결 속성을 지정해야 합니다. [연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)을 참조하세요.

## 빠른 시작(SOAP 모드): Java API를 사용하여 정책 만들기 {#quick-start-soap-mode-creating-a-policy-using-the-java-api}

다음 Java 코드 예제에서는 *복사 허용*&#x200B;이라는 새 정책을 만듭니다. 정책이 추가되는 정책 집합의 이름은 *전역 정책 집합*&#x200B;입니다. 이 정책 집합은 기본적으로 존재합니다. ([정책 만들기](/help/forms/developing/protecting-documents-policies.md#creating-policies)를 참조하십시오.)

```java
 /*
     * This Java Quick Start uses the SOAP mode and contains the following JAR files
     * in the class path:
     * 1. adobe-rightsmanagement-client.jar
     * 2. adobe-livecycle-client.jar
     * 3. adobe-usermanager-client.jar
     * 4. activation.jar (required for SOAP mode)
     * 5. axis.jar (required for SOAP mode)
     * 6. commons-codec-1.3.jar (required for SOAP  mode)
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
     * These JAR files are in the following path:
     * <install directory>/sdk/client-libs/common
     *
     *
     * <install directory>/jboss/bin/client
     *
     * If you want to invoke a remote Forms Server instance and there is a
     * firewall between the client application and the server, then it is
     * recommended that you use the SOAP mode. When using the SOAP mode,
     * you have to include additional JAR files in the following
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
 
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 import com.adobe.idp.um.api.infomodel.Principal;
 import com.adobe.livecycle.rightsmanagement.client.*;
 import com.adobe.livecycle.rightsmanagement.client.infomodel.*;
 
 public class CreatePolicy {
 
     public static void main(String[] args) {
 
         try
         {
             //Set connection properties required to invoke AEM Forms
             Properties connectionProps = new Properties();
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://'[server]:[port]'");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
 
              //Create a ServiceClientFactory object
             ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps);
 
             //Create a RightsManagementClient object
             RightsManagementClient rightsClient = new RightsManagementClient(myFactory);
 
             //Create a Policy object that represents the new policy
             Policy myPolicy = InfomodelObjectFactory.createPolicy();
 
             //Set policy attributes that are used by the policy
             myPolicy.setName("Allow Copy");
             myPolicy.setDescription("This policy enables users to copy information from the PDF document");
             myPolicy.setPolicySetName("Global Policy Set");
             myPolicy.setOfflineLeasePeriod(30);
             myPolicy.setTracked(true);
 
             //Set the validity period to 30 days
             ValidityPeriod validityPeriod = InfomodelObjectFactory.createValidityPeriod();
             validityPeriod.setRelativeExpirationDays(30);
             myPolicy.setValidityPeriod(validityPeriod);
 
             //Create a PolicyEntry object
             PolicyEntry myPolicyEntry = InfomodelObjectFactory.createPolicyEntry();
 
             //Specify the permissions
             Permission onlinePermission = InfomodelObjectFactory.createPermission(Permission.OPEN_ONLINE) ;
             Permission copyPermission = InfomodelObjectFactory.createPermission(Permission.COPY);
 
             //Add permissions to the policy entry
             myPolicyEntry.addPermission(onlinePermission);
             myPolicyEntry.addPermission(copyPermission);
 
             //Create principal object
              Principal publisherPrincipal = InfomodelObjectFactory.createSpecialPrincipal(InfomodelObjectFactory.PUBLISHER_PRINCIPAL);
 
              //Add a principal object to the policy entry
              myPolicyEntry.setPrincipal(publisherPrincipal);
 
              //Attach the policy entry to the policy
              myPolicy.addPolicyEntry(myPolicyEntry);
 
              //Register the policy
             PolicyManager policyManager = rightsClient.getPolicyManager();
             policyManager.registerPolicy(myPolicy,"Global Policy Set");
             }
         catch (Exception ex)
             {
                 ex.printStackTrace();
             }
         }
 }
 
```

## 빠른 시작(SOAP 모드): Java API를 사용하여 정책 수정 {#quick-start-soap-mode-modifying-a-policy-using-the-java-api}

다음 Java 코드 예제에서는 오프라인 임대 기간을 40일로 설정하여 *복사 허용*&#x200B;이라는 정책을 수정합니다. ([정책 수정](/help/forms/developing/protecting-documents-policies.md#modifying-policies)을 참조하십시오.)

```java
 /*
     * This Java Quick Start uses the SOAP mode and contains the following JAR files
     * in the class path:
     * 1. adobe-rightsmanagement-client.jar
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
     * These JAR files are in the following path:
     * <install directory>/sdk/client-libs/common
     *
     *
     * <install directory>/jboss/bin/client
     *
     * SOAP required JAR files are in the following path:
     * <install directory>/sdk/client-libs/thirdparty
     *
     * If you want to invoke a remote Forms Server instance and there is a
     * firewall between the client application and the server, then it is
     * recommended that you use the SOAP mode. When using the SOAP mode,
     * you have to include these additional JAR files
     *
     * For information about the SOAP
     * mode, see "Setting connection properties" in Programming
     * with AEM Forms
     */
 import java.util.*;
 
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 import com.adobe.livecycle.rightsmanagement.client.*;
 import com.adobe.livecycle.rightsmanagement.client.infomodel.*;
 
 public class ModifyPolicySoap {
 
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
 
                 //Create a ServiceClientFactory object
                 ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps);
 
                 //Create a RightsManagementClient object
                 RightsManagementClient rightsClient = new RightsManagementClient(myFactory);
 
                 //Create a policy manager instance
                 PolicyManager policyManager = rightsClient.getPolicyManager();
 
                 //Retrieve an existing policy
                 Policy myPolicy = policyManager.getPolicy(
                     "Global Policy Set",
                     "Allow Copy") ;
 
                 //Modify policy attributes
                 myPolicy.setOfflineLeasePeriod(40);
                 myPolicy.setTracked(true);
 
                 //Set the validity period to 40 days
                 ValidityPeriod validityPeriod = InfomodelObjectFactory.createValidityPeriod();
                 validityPeriod.setRelativeExpirationDays(40);
                 myPolicy.setValidityPeriod(validityPeriod);
 
                 //Update the policy
                 policyManager.updatePolicy(myPolicy) ;
                   }
 
         catch (Exception ee)
             {
              ee.printStackTrace();
             }
     }
 }
```

## 빠른 시작(SOAP 모드): Java API를 사용하여 정책 삭제 {#quick-start-soap-mode-deleting-a-policy-using-the-java-api}

다음 Java 코드 예제에서는 *복사 허용*&#x200B;이라는 정책을 삭제합니다. ([정책 삭제](/help/forms/developing/protecting-documents-policies.md#deleting-policies)를 참조하십시오.)

```java
 /*
     * * This Java Quick Start uses the SOAP mode and contains the following JAR files
     * in the class path:
     * 1. adobe-rightsmanagement-client.jar
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
     * These JAR files are in the following path:
     * <install directory>/sdk/client-libs/common
     *
     *
     * <install directory>/jboss/bin/client
     *
     * If you want to invoke a remote Forms Server instance and there is a
     * firewall between the client application and the server, then it is
     * recommended that you use the SOAP mode. When using the SOAP mode,
     * you have to include additional JAR files in the following
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
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 import com.adobe.livecycle.rightsmanagement.client.*;
 
 public class DeletePolicy {
 
     public static void main(String[] args) {
      try
       {
         //Set connection properties required to invoke AEM Forms
         Properties connectionProps = new Properties();
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://'[server]:[port]'");
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
 
         //Create a ServiceClientFactory object
         ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps);
 
         //Create a RightsManagementClient object
          RightsManagementClient rightsClient = new RightsManagementClient(myFactory);
 
          //Create a policy manager instance
          PolicyManager policyManager = rightsClient.getPolicyManager();
 
          //Delete the AllowCopy policy
          policyManager.deletePolicy("Global Policy Set", "Allow Copy") ;
           }
     catch (Exception ee)
         {
          ee.printStackTrace();
         }
     }
 }
 
```

## 빠른 시작(SOAP 모드): Java API를 사용하여 PDF 문서에 정책 적용 {#quick-start-soap-mode-applying-a-policy-to-a-pdf-document-using-the-java-api}

다음 Java 코드 예제에서는 *복사 허용* 정책을 *Loan.pdf* PDF 문서에 적용합니다. 정책이 추가되는 정책 집합의 이름은 *전역 정책 집합*&#x200B;입니다. 정책으로 보호된 문서는 *PolicyProtectedLoanDoc.pdf라는 PDF 파일로 저장됩니다. *([PDF 문서에 정책 적용](/help/forms/developing/protecting-documents-policies.md#applying-policies-to-pdf-documents)을 참조하십시오.)

```java
 /*
     * This Java Quick Start uses the SOAP mode and contains the following JAR files
     * in the class path:
     * 1. adobe-rightsmanagement-client.jar
     * 2. adobe-livecycle-client.jar
     * 3. adobe-usermanager-client.jar
     * 4. activation.jar (required for SOAP mode)
     * 5. axis.jar (required for SOAP mode)
     * 6. commons-codec-1.3.jar (required for SOAP  mode)
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
     * These JAR files are in the following path:
     * <install directory>/sdk/client-libs/common
     *
     *
     * <install directory>/jboss/bin/client
     *
     * SOAP required JAR files are in the following path:
     * <install directory>/sdk/client-libs/thirdparty
     *
     * If you want to invoke a remote Forms Server instance and there is a
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
 import com.adobe.idp.Document;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 import com.adobe.livecycle.rightsmanagement.RMSecureDocumentResult;
 import com.adobe.livecycle.rightsmanagement.client.*;
 
 public class ApplyPolicySoap {
 
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
         ServiceClientFactory factory = ServiceClientFactory.createInstance(connectionProps);
 
         //Create a RightsManagementClient object
         RightsManagementClient rightsClient = new RightsManagementClient(factory);
 
         //Reference a PDF document to which a policy is applied
         FileInputStream is = new FileInputStream("C:\\Adobe\Loan.pdf");
         Document inPDF = new Document(is);
 
         //Create a Document Manager object
         DocumentManager  documentManager = rightsClient.getDocumentManager();
 
         //Apply a policy to the PDF document
         RMSecureDocumentResult rmSecureDocument =  documentManager.protectDocument(
             inPDF,
             "LoanPDF",
             "Global Policy Set",
             "Allow Copy",
             null,
             null,
             null);
 
         //Retrieve the policy-protected PDF document
         Document protectPDF = rmSecureDocument.getProtectedDoc();
 
         //Save the policy-protected PDF document
         File myFile = new File("C:\\Adobe\PolicyProtectedLoanDoc.pdf");
         protectPDF.copyToFile(myFile);
       }
     catch (Exception ee)
      {
         ee.printStackTrace();
      }
     }
 }
```

## 빠른 시작(SOAP 모드): Java API를 사용하여 PDF 문서에서 정책 제거 {#quick-start-soap-mode-removing-a-policy-from-a-pdf-document-using-the-java-api}

다음 코드 예제에서는 PDF 문서 *PolicyProtectedLoanDoc.pdf*&#x200B;에서 정책을 제거합니다. 보안되지 않은 PDF 문서가 *unProtectedLoan.pdf*(으)로 저장됩니다. ([PDF 문서에서 정책 제거](/help/forms/developing/protecting-documents-policies.md#removing-policies-from-pdf-documents)를 참조하십시오.)

```java
 /*
     * * This Java Quick Start uses the SOAP mode and contains the following JAR files
     * in the class path:
     * 1. adobe-rightsmanagement-client.jar
     * 2. adobe-livecycle-client.jar
     * 3. adobe-usermanager-client.jar
     * 4. activation.jar (required for SOAP mode)
     * 5. axis.jar (required for SOAP mode)
     * 6. commons-codec-1.3.jar (required for SOAP  mode)
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
     * These JAR files are in the following path:
     * <install directory>/sdk/client-libs/common
     *
     *
     * <install directory>/jboss/bin/client
     *
     * If you want to invoke a remote Forms Server instance and there is a
     * firewall between the client application and the server, then it is
     * recommended that you use the SOAP mode. When using the SOAP mode,
     * you have to include additional JAR files in the following
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
 import java.io.File;
 import java.io.FileInputStream;
 
 import com.adobe.idp.Document;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 import com.adobe.livecycle.rightsmanagement.client.*;
 
 
 public class RemovePolicy {
 
     public static void main(String[] args) {
 
         try
         {
             //Set connection properties required to invoke AEM Forms
             Properties connectionProps = new Properties();
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://'[server]:[port]'");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
 
             //Create a ServiceClientFactory instance
             ServiceClientFactory factory = ServiceClientFactory.createInstance(connectionProps);
 
             //Create a RightsManagementClient object
             RightsManagementClient rightsClient = new RightsManagementClient(factory);
 
             //Reference a policy-protected PDF document from which to remove a policy
             FileInputStream is = new FileInputStream("C:\\Adobe\PolicyProtectedLoanDoc.pdf");
             Document inPDF = new Document(is);
 
             //Create a Document Manager object
             DocumentManager  documentManager = rightsClient.getDocumentManager();
 
             //Remove a policy from the policy-protected PDF document
             Document unsecurePDF =  documentManager.removeSecurity(inPDF);
 
             //Save the unsecured PDF document
             File myFile = new File("C:\\Adobe\UnProtectedLoan.pdf");
             unsecurePDF.copyToFile(myFile);
           }
 
          catch (Exception ee)
          {
           ee.printStackTrace();
          }
     }
 }
 
```

## 빠른 시작(SOAP 모드): Java API를 사용하여 문서 취소 {#quick-start-soap-mode-revoking-a-document-using-the-java-api}

다음 Java 코드 예제에서는 *PolicyProtectedLoanDoc.pdf*&#x200B;라는 정책으로 보호된 문서를 취소합니다. 수정된 PDF 문서가 다음 URL 위치 `https://'[server]:[port]'/RightsManagement/UpdatedLoan.pdf`에 있습니다. [문서에 대한 액세스 취소](/help/forms/developing/protecting-documents-policies.md#revoking-access-to-documents)를 참조하세요.

```java
 /*
     * * This Java Quick Start uses the SOAP mode and contains the following JAR files
     * in the class path:
     * 1. adobe-rightsmanagement-client.jar
     * 2. adobe-livecycle-client.jar
     * 3. adobe-usermanager-client.jar
     * 4. activation.jar (required for SOAP mode)
     * 5. axis.jar (required for SOAP mode)
     * 6. commons-codec-1.3.jar (required for SOAP  mode)
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
     * These JAR files are in the following path:
     * <install directory>/sdk/client-libs/common
     *
     *
     * <install directory>/jboss/bin/client
     *
     * If you want to invoke a remote Forms Server instance and there is a
     * firewall between the client application and the server, then it is
     * recommended that you use the SOAP mode. When using the SOAP mode,
     * you have to include additional JAR files in the following
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
 import java.io.FileInputStream;
 import java.util.*;
 
 import com.adobe.idp.Document;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 
 import java.net.URL;
 
 import com.adobe.livecycle.rightsmanagement.client.*;
 import com.adobe.livecycle.rightsmanagement.client.infomodel.*;
 
 
 public class RevokeDocument {
 
     public static void main(String[] args) {
 
         try
         {
         //Set connection properties required to invoke AEM Forms
         Properties connectionProps = new Properties();
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://'[server]:[port]'");
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
 
         //Create a ServiceClientFactory instance
         ServiceClientFactory factory = ServiceClientFactory.createInstance(connectionProps);
 
         //Create a RightsManagementClient object
         RightsManagementClient rightsClient = new RightsManagementClient(factory);
 
         //Reference a policy-protected PDF document to revoke
         FileInputStream is = new FileInputStream("C:\\Adobe\PolicyProtectedLoanDoc.pdf");
         Document inPDF = new Document(is);
 
         //Create a Document Manager object
         DocumentManager  documentManager = rightsClient.getDocumentManager();
 
         //Obtain the license identifier value of the policy-protected document
         String revokeLic = documentManager.getLicenseId(inPDF);
 
         //Create a LicenseManager object
         LicenseManager licManager = rightsClient.getLicenseManager();
 
         //Specify the URL to where an updated document is located
         URL myURL = new URL("https://'[server]:[port]'/RightsManagement/UpdatedLoan.pdf");
 
         //Revoke the policy-protected PDF document
         licManager.revokeLicense(revokeLic, License.DOCUMENT_REVISED, myURL);
         }
      catch (Exception ee)
        {
             ee.printStackTrace();
        }
     }
 }
 
```

## 빠른 시작(SOAP 모드): Java API를 사용하여 정책으로 보호된 PDF 문서 검사 {#quick-start-soap-mode-inspecting-policy-protected-pdf-documents-using-the-java-api}

다음 Java 코드 예제에서는 *PolicyProtectedLoanDoc.pd* f라는 정책으로 보호된 PDF 문서를 검사합니다. ([정책으로 보호된 PDF 문서 검사](/help/forms/developing/protecting-documents-policies.md#inspecting-policy-protected-pdf-documents)를 참조하십시오.)

```java
 /*
     * * This Java Quick Start uses the SOAP mode and contains the following JAR files
     * in the class path:
     * 1. adobe-rightsmanagement-client.jar
     * 2. adobe-livecycle-client.jar
     * 3. adobe-usermanager-client.jar
     * 4. activation.jar (required for SOAP mode)
     * 5. axis.jar (required for SOAP mode)
     * 6. commons-codec-1.3.jar (required for SOAP  mode)
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
     * These JAR files are in the following path:
     * <install directory>/sdk/client-libs/common
     *
     *
     * <install directory>/jboss/bin/client
     *
     * If you want to invoke a remote Forms Server instance and there is a
     * firewall between the client application and the server, then it is
     * recommended that you use the SOAP mode. When using the SOAP mode,
     * you have to include additional JAR files in the following
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
 
 import java.io.FileInputStream;
 import java.util.Properties;
 import java.util.Date;
 import java.util.Calendar;
 
 import com.adobe.idp.Document;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 import com.adobe.livecycle.rightsmanagement.client.*;
 import com.adobe.livecycle.rightsmanagement.*;
 
 public class InspectDocument {
 
     public static void main(String[] args) {
 
          try
           {
             //Set connection properties required to invoke AEM Forms
             Properties connectionProps = new Properties();
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://'[server]:[port]'");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
 
             //Create a ServiceClientFactory instance
             ServiceClientFactory factory = ServiceClientFactory.createInstance(connectionProps);
 
             //Create a RightsManagementClient object
             RightsManagementClient rightsClient = new RightsManagementClient(factory);
 
             //Reference a policy-protected PDF document to inspect
             FileInputStream is = new FileInputStream("C:\\Adobe\PolicyProtectedLoanDoc.pdf");
             Document inPDF = new Document(is);
 
             //Create a Document Manager object
             DocumentManager  documentManager = rightsClient.getDocumentManager();
 
             //Inspect the policy-protected document
             RMInspectResult inspectResult = documentManager.inspectDocument(inPDF);
 
             //Get the document name
             String documentName = inspectResult.getDocName();
 
             //Get the name of the policy
             String policyName = inspectResult.getPolicyName();
 
             //Get the name of the document publisher
             String pubName = inspectResult.getPublisherName();
 
             //Display the name of the policy-protected document and the policy
             System.out.println("The policy protected document "+documentName +" is protected with the policy "+policyName +". The name of the publisher is "+pubName+".");
 
               }
         catch (Exception ee)
             {
              ee.printStackTrace();
             }
     }
 }
 
 
```

## 빠른 시작(SOAP 모드): Java API를 사용하여 해지된 문서에 대한 액세스 복원 {#quick-start-soap-mode-reinstating-access-to-a-revoked-document-using-the-java-api}

다음 Java 코드 예제에서는 취소된 PDF 문서 *PolicyProtectedLoanDoc.pdf*&#x200B;에 대한 액세스를 복원합니다. [해지된 문서에 대한 액세스 복원](/help/forms/developing/protecting-documents-policies.md#reinstating-access-to-revoked-documents)을 참조하세요.

```java
 /*
     * * This Java Quick Start uses the SOAP mode and contains the following JAR files
     * in the class path:
     * 1. adobe-rightsmanagement-client.jar
     * 2. adobe-livecycle-client.jar
     * 3. adobe-usermanager-client.jar
     * 4. activation.jar (required for SOAP mode)
     * 5. axis.jar (required for SOAP mode)
     * 6. commons-codec-1.3.jar (required for SOAP  mode)
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
     * These JAR files are in the following path:
     * <install directory>/sdk/client-libs/common
     *
     *
     * <install directory>/jboss/bin/client
     *
     * If you want to invoke a remote Forms Server instance and there is a
     * firewall between the client application and the server, then it is
     * recommended that you use the SOAP mode. When using the SOAP mode,
     * you have to include additional JAR files in the following
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
 import java.io.FileInputStream;
 import java.util.*;
 
 import com.adobe.idp.Document;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 import com.adobe.livecycle.rightsmanagement.client.*;
 
 public class ReinstateDocument {
 
     public static void main(String[] args) {
 
         try
         {
         //Set connection properties required to invoke AEM Forms
         Properties connectionProps = new Properties();
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://'[server]:[port]'");
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
 
         //Create a ServiceClientFactory instance
         ServiceClientFactory factory = ServiceClientFactory.createInstance(connectionProps);
 
         //Create a RightsManagementClient object
         RightsManagementClient rightsClient = new RightsManagementClient(factory);
 
         //Reference a revoked PDF document
         FileInputStream is = new FileInputStream("C:\\Adobe\PolicyProtectedLoanDoc.pdf");
         Document inPDF = new Document(is);
 
         //Create a Document Manager object
         DocumentManager  documentManager = rightsClient.getDocumentManager();
 
         //Obtain the license identifier value of the revoked PDF document
         String revokeLic = documentManager.getLicenseId(inPDF);
 
         //Create a LicenseManager object
         LicenseManager licManager = rightsClient.getLicenseManager();
 
         //Reinstate access to the revoked document
         licManager.unrevokeLicense(revokeLic);
         }
      catch (Exception ee)
        {
             ee.printStackTrace();
        }
     }
 }
 
```

## 빠른 시작(SOAP 모드): Java API를 사용하여 PDF 워터마크 만들기 {#quick-start-soap-mode-creating-a-pdf-watermark-using-the-java-api}

다음 Java 코드 예제에서는 &#39;샘플 PDF 워터마크&#39;라는 새 PDF 워터마크를 만듭니다. 이 워터마크에는 단일 요소가 포함되어 있습니다([워터마크 만들기](/help/forms/developing/protecting-documents-policies.md#creating-watermarks) 참조).

```java
/*
 * This Java Quick Start uses the SOAP mode and contains the following JAR files
 * in the class path:
 * 1. adobe-rightsmanagement-client.jar
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
 * These JAR files are in the following path:
 * <install directory>/Adobe/Adobe_Experience_Manager_forms/sdk/client-libs/common
 *
 * <install directory>/Adobe/Adobe_Experience_Manager_forms/sdk/client-libs/jboss
 *
 * <install directory>/Adobe/Adobe_Experience_Manager_forms/jboss/bin/client
 *
 * SOAP required JAR files are in the following path:
 * <install directory>/Adobe/Adobe_Experience_Manager_forms/sdk/client-libs/thirdparty
 *
 * If you want to invoke a remote Forms Server instance and there is a
 * firewall between the client application and Forms Server, then it is
 * recommended that you use the SOAP mode. When using the SOAP mode,
 * you have to include these additional JAR files
 *
 * For information about the SOAP
 * mode, see "Setting connection properties" in Programming
 * with Forms Server
 */

import java.io.FileInputStream;
import java.io.FileNotFoundException;
import java.util.Properties;
import com.adobe.edc.sdk.SDKException;
import com.adobe.idp.Document;
import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
import com.adobe.livecycle.rightsmanagement.client.RightsManagementClient;
import com.adobe.livecycle.rightsmanagement.client.WatermarkManager;
import com.adobe.livecycle.rightsmanagement.client.infomodel.InfomodelObjectFactory;
import com.adobe.livecycle.rightsmanagement.client.infomodel.PDRLException;
import com.adobe.livecycle.rightsmanagement.client.infomodel.Watermark2;
import com.adobe.livecycle.rightsmanagement.client.infomodel.Watermark2Element;

public class PDFWatermarksSOAPMode {
    public static void main(String[] args) {
        // Set connection properties required to invoke Adobe AEM Forms
        // using SOAP mode
        try {
            Properties connectionProps = new Properties();
            connectionProps.setProperty(
                    ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT,
                    "https://'[server]:[port]'/");
            connectionProps.setProperty(
                    ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,
                    ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
            connectionProps.setProperty(
                    ServiceClientFactoryProperties.DSC_SERVER_TYPE,
                    ServiceClientFactoryProperties.DSC_JBOSS_SERVER_TYPE);
            connectionProps.setProperty(
                    ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME,
                    "administrator");
            connectionProps.setProperty(
                    ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD,
                    "password");

            // Create a ServiceClientFactory object.
            ServiceClientFactory serviceClient = ServiceClientFactory
                    .createInstance(connectionProps);

            // Create a Document Security ServiceClient object.
            RightsManagementClient rmClient = new RightsManagementClient(
                    serviceClient);
            // Get the watermark manager which is used to add, delete or update
            // watermarks.
            WatermarkManager watermarkManager = rmClient.getWatermarkManager();

            // Registering and adding elements to the new watermarks.
            // Create a Watermark2 object using the InfomodelObjectFactory.
            Watermark2 newWatermark = InfomodelObjectFactory.createWatermark2();
            // Create a Watermark2Element object using the
            // InfomodelObjectFactory.
            Watermark2Element element1 = InfomodelObjectFactory
                    .createWatermark2Element();
            // Set the various properties such as name, description,custom text
            // and date.
            element1.setName("PDF element");
            element1.setDescription("This is a Sample PDF element.");
            // Set type of the watermark to Watermark2Element.TYPE_PDF.
            element1.setType(Watermark2Element.TYPE_PDF);
            // Create an IDf document form a PDF file.
            Document doc = new Document(new FileInputStream("C:\\Sample.pdf"));
            element1.setPDFContent(doc, "Watermark Doc");
            // Set the properties for this such rotation,opacity.
            element1.setOpacity(50);
            element1.setRotation(45);//45 degrees rotation.
            element1.setStartPage(5);
            element1.setStartPage(15);//Watermark appears only on pages 10 to 15.
            // Add it to the watermark.
            newWatermark.addWatermarkElement(element1);
            // Set the watermark name.
            newWatermark.setName("Sample PDF Watermark");
            // Register it.
            watermarkManager.registerWatermark2(newWatermark);
        } catch (PDRLException e) {
            System.out.println(e.getCause());
        } catch (SDKException e) {
            e.printStackTrace();
        } catch (FileNotFoundException e) {
            e.printStackTrace();
        }
    }
}
```

## 빠른 시작(SOAP 모드): Java API를 사용하여 텍스트 워터마크 만들기 {#quick-start-soap-mode-creating-a-text-watermark-using-the-java-api}

다음 Java 코드 예제에서는 *샘플 텍스트 워터마크*&#x200B;라는 새 텍스트 워터마크를 만듭니다. 이 워터마크에는 단일 요소가 포함되어 있습니다.

```java
/*
 * This Java Quick Start uses the SOAP mode and contains the following JAR files
 * in the class path:
 * 1. adobe-rightsmanagement-client.jar
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
 * These JAR files are in the following path:
 * <install directory>/Adobe/Adobe_Experience_Manager_forms/sdk/client-libs/common
 *
 * <install directory>/Adobe/Adobe_Experience_Manager_forms/sdk/client-libs/jboss
 *
 * <install directory>/Adobe/Adobe_Experience_Manager_forms/jboss/bin/client
 *
 * SOAP required JAR files are in the following path:
 * <install directory>/Adobe/Adobe_Experience_Manager_forms/sdk/client-libs/thirdparty
 *
 * If you want to invoke a remote Forms Server instance and there is a
 * firewall between the client application and Forms Server, then it is
 * recommended that you use the SOAP mode. When using the SOAP mode,
 * you have to include these additional JAR files
 *
 * For information about the SOAP
 * mode, see "Setting connection properties" in Programming
 * with Forms Server
 */

import com.adobe.livecycle.rightsmanagement.client.RightsManagementClient;
import com.adobe.livecycle.rightsmanagement.client.WatermarkManager;
import com.adobe.livecycle.rightsmanagement.client.infomodel.InfomodelObjectFactory;
import com.adobe.livecycle.rightsmanagement.client.infomodel.PDRLException;
import com.adobe.livecycle.rightsmanagement.client.infomodel.Watermark2;
import com.adobe.livecycle.rightsmanagement.client.infomodel.Watermark2Element;
import com.adobe.edc.sdk.SDKException;
import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
import java.util.Properties;

public class TextWatermarks {
    public static void main(String[] args) {
        try {
            // Set connection properties required to invoke Adobe Document
            // Services using SOAP mode
            Properties connectionProps = new Properties();
            connectionProps.setProperty(
                    ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT,
                    "https://'[server]:[port]'/");
            connectionProps.setProperty(
                    ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,
                    ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
            connectionProps.setProperty(
                    ServiceClientFactoryProperties.DSC_SERVER_TYPE,
                    ServiceClientFactoryProperties.DSC_JBOSS_SERVER_TYPE);
            connectionProps.setProperty(
                    ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME,
                    "administrator");
            connectionProps.setProperty(
                    ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD,
                    "password");

            // Create a ServiceClientFactory object.
            ServiceClientFactory serviceClient = ServiceClientFactory
                    .createInstance(connectionProps);

            // Create a Document Security ServiceClient object.
            RightsManagementClient rmClient = new RightsManagementClient(
                    serviceClient);
            // Get the watermark manager which is used to add, delete or update
            // watermarks.
            WatermarkManager watermarkManager = rmClient.getWatermarkManager();

            // Registering and adding elements to the new watermarks.
            // Create a Watermark2 object using the InfomodelObjectFactory.
            Watermark2 newWatermark = InfomodelObjectFactory.createWatermark2();
            // Create a Watermark2Element object using the
            // InfomodelObjectFactory.
            Watermark2Element element1 = InfomodelObjectFactory
                    .createWatermark2Element();
            // Set the various properties such as name, description,custom text
            // and date.
            element1.setName("First element");
            element1.setDescription("This is a Sample Text Watermark Element.");
            element1.setUserNameIncluded(true);
            element1.setShowOnPrint(false);// This element will not appear on
                                            // print, but will only appear on
                                            // screen.
            // Set the type of the watermark element. It can either be
            // Watermark2Element.TYPE_TEXT or Watermark2Element.TYPE_PDF.
            element1.setType(Watermark2Element.TYPE_TEXT);
            // Provide opacity, rotation page range and other such settings.
            element1.setOpacity(50); // Opacity set to 50%.
            element1.setEndPage(1);// The watermark will appear only on first
                                    // page, start page is 1 by default.

            // Create an element.
            Watermark2Element element2 = InfomodelObjectFactory
                    .createWatermark2Element();
            element2.setName("Second element");
            element2.setCustomText("Confidential");
            // Set type to Watermark2Element.TYPE_TEXT.
            element2.setType(Watermark2Element.TYPE_TEXT);
            // Provide opacity, rotation page range and other such settings.
            element2.setFontName("Times New Roman");
            element2.setFontSize(30);
            element2.setOpacity(30);// 30% opacity.
            element2.setRotation(45);// 45 degrees rotation.
            element2.setShowOnScreen(false);// This element will not appear on
                                            // screen, but will appear when we
                                            // print the document.

            // Add these elements to the watermark in the order in you want them
            // to be applied.
            newWatermark.addWatermarkElement(element1);// Applied first.
            newWatermark.addWatermarkElement(element2);// Applied on top
                                                        // of it.
            newWatermark.setName("Sample Text Watermark");
            watermarkManager.registerWatermark2(newWatermark);
        } catch (PDRLException e) {
            System.out.println(e.getCause());
        } catch (SDKException e) {
            e.printStackTrace();
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

## 빠른 시작(SOAP 모드): Java API를 사용하여 텍스트 워터마크 수정 {#quick-start-soap-mode-modifying-a-text-watermark-using-the-java-api}

다음 Java 코드 예제에서는 &#39;샘플 텍스트 워터마크&#39;라는 워터마크를 수정하고 첫 번째 요소의 불투명도를 100으로 설정합니다.

```java
/*
 * This Java Quick Start uses the SOAP mode and contains the following JAR files
 * in the class path:
 * 1. adobe-rightsmanagement-client.jar
 * 2. adobe-livecycle-client.jar
 * 3. adobe-usermanager-client.jar
 * 4. activation.jar (required for SOAP mode)
 * 5. axis.jar (required for SOAP mode)
 * 6. commons-codec-1.3.jar (required for SOAP mode)
 * 7. commons-collections-3.1.jar  (required for SOAP mode)
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
 * These JAR files are in the following path:
 * <install directory>/Adobe/Adobe_Experience_Manager_forms/sdk/client-libs/common
 *
 * <install directory>/Adobe/Adobe_Experience_Manager_forms/sdk/client-libs/jboss
 *
 * <install directory>/Adobe/Adobe_Experience_Manager_forms/jboss/bin/client
 *
 * SOAP required JAR files are in the following path:
 * <install directory>/Adobe/Adobe_Experience_Manager_forms/sdk/client-libs/thirdparty
 *
 * If you want to invoke a remote Forms Server instance and there is a
 * firewall between the client application and Forms Server, then it is
 * recommended that you use the SOAP mode. When using the SOAP mode,
 * you have to include these additional JAR files
 *
 * For information about the SOAP
 * mode, see "Setting connection properties" in Programming
 * with Forms Server
 */

import java.util.*;
import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
import com.adobe.livecycle.rightsmanagement.client.*;
import com.adobe.livecycle.rightsmanagement.client.infomodel.*;

public class ModifyWatermarks {

    public static void main(String[] args) {
        try {
            // Set connection properties required to invoke AEM Forms using
            // SOAP mode
            Properties connectionProps = new Properties();
            connectionProps.setProperty(
                    ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT,
                    "https://'[server]:[port]'");
            connectionProps.setProperty(
                    ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,
                    ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
            connectionProps.setProperty(
                    ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
            connectionProps.setProperty(
                    ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME,
                    "administrator");
            connectionProps.setProperty(
                    ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD,
                    "password");

            // Create a ServiceClientFactory instance
            ServiceClientFactory factory = ServiceClientFactory
                    .createInstance(connectionProps);

            // Create a RightsManagementClient object
            RightsManagementClient rightsClient = new RightsManagementClient(
                    factory);

            // Create a WatermarkManager object
            WatermarkManager myWatermarkManager = rightsClient
                    .getWatermarkManager();

            // Get the watermark to modify by name
            Watermark2 myWatermark = myWatermarkManager
                    .getWatermarkByName2("Sample Text Watermark");

            // Get the elements in the watermark.
            ArrayList<Watermark2Element> elements = myWatermark
                    .getWatermarkElements();
            // Iterate through the list and modify the opacity attribute of each
            // element.
            for (Iterator<Watermark2Element> iter = elements.iterator(); iter
                    .hasNext();) {
                Watermark2Element elem = iter.next();
                elem.setOpacity(100);
            }
            // Update the watermark
            myWatermarkManager.updateWatermark2(myWatermark);
        }
        catch (Exception ex) {
            ex.printStackTrace();
        }
    }
}
```

## 빠른 시작(SOAP 모드): Java API를 사용하여 워터마크 수정 {#quick-start-soap-mode-modifying-a-watermark-using-the-java-api}

다음 Java 코드 예제에서는 `opacity` 특성의 값을 80으로 수정하여 이름이 *Confidential*&#x200B;인 워터마크를 수정합니다.

```java
 /*
     * * This Java Quick Start uses the SOAP mode and contains the following JAR files
     * in the class path:
     * 1. adobe-rightsmanagement-client.jar
     * 2. adobe-livecycle-client.jar
     * 3. adobe-usermanager-client.jar
     * 4. activation.jar (required for SOAP mode)
     * 5. axis.jar (required for SOAP mode)
     * 6. commons-codec-1.3.jar (required for SOAP  mode)
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
     * These JAR files are in the following path:
     * <install directory>/sdk/client-libs/common
     *
     *
     * <install directory>/jboss/bin/client
     *
     * If you want to invoke a remote Forms Server instance and there is a
     * firewall between the client application and the server, then it is
     * recommended that you use the SOAP mode. When using the SOAP mode,
     * you have to include additional JAR files in the following
     * path
     * <install directory>/sdk/client-libs/thirdparty
     *
    * For complete details about the location of the AEM Forms JAR files,
     * see "Including AEM Forms Java library files" in Programming
     * with AEM Forms
     */
 import java.util.*;
 
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 import com.adobe.livecycle.rightsmanagement.client.*;
 import com.adobe.livecycle.rightsmanagement.client.infomodel.*;
 
 
 public class ModifyWatermarks {
 
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
         ServiceClientFactory factory = ServiceClientFactory.createInstance(connectionProps);
 
         //Create a RightsManagementClient object
         RightsManagementClient rightsClient = new RightsManagementClient(factory);
 
         //Create a WatermarkManager object
         WatermarkManager myWatermarkManager =  rightsClient.getWatermarkManager();
 
         //Get the watermark to modify by name
         Watermark myWatermark = myWatermarkManager.getWatermarkByName("Confidential");
 
         //Modify the opacity attribute
         myWatermark.setOpacity(80);
 
         //Update the watermark
         myWatermarkManager.updateWatermark(myWatermark);
         }
 
     catch (Exception ex)
         {
         ex.printStackTrace();
         }
     }
 }
 
```

## 빠른 시작(SOAP 모드): Java API를 사용하여 이벤트 검색 {#quick-start-soap-mode-searching-for-events-using-the-java-api}

다음 Java 코드 예제에서는 정책 생성 이벤트를 검색합니다.

```java
 /*
     * * This Java Quick Start uses the SOAP mode and contains the following JAR files
     * in the class path:
     * 1. adobe-rightsmanagement-client.jar
     * 2. adobe-livecycle-client.jar
     * 3. adobe-usermanager-client.jar
     * 4. activation.jar (required for SOAP mode)
     * 5. axis.jar (required for SOAP mode)
     * 6. commons-codec-1.3.jar (required for SOAP  mode)
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
     * These JAR files are in the following path:
     * <install directory>/sdk/client-libs/common
     *
     *
     * <install directory>/jboss/bin/client
     *
     * If you want to invoke a remote Forms Server instance and there is a
     * firewall between the client application and the server, then it is
     * recommended that you use the SOAP mode. When using the SOAP mode,
     * you have to include additional JAR files in the following
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
 
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 import com.adobe.livecycle.rightsmanagement.client.*;
 import com.adobe.livecycle.rightsmanagement.client.infomodel.Event;
 import com.adobe.livecycle.rightsmanagement.client.infomodel.EventSearchFilter;
 
 public class SearchEvents {
 
     public static void main(String[] args) {
 
         try
         {
         //Set connection properties required to invoke AEM Forms
         Properties connectionProps = new Properties();
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://'[server]:[port]'");
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
 
         //Create a ServiceClientFactory instance
         ServiceClientFactory factory = ServiceClientFactory.createInstance(connectionProps);
 
         //Create a RightsManagementClient object
         RightsManagementClient rightsClient = new RightsManagementClient(factory);
 
         //Create a EventManager instance
         EventManager eventManager = rightsClient.getEventManager();
 
         //Create a EventSearchFilter object
         EventSearchFilter eventSearchFilter = new EventSearchFilter();
 
         //Search for the POLICY_CREATE_EVENT event
         eventSearchFilter.setEventCode(EventManager.POLICY_CREATE_EVENT);
         Event[] events = eventManager.searchForEvents(eventSearchFilter,20) ;
 
         //Retrieve information about each event
         int index = events.length;
         Calendar rightNow = Calendar.getInstance();
 
         for (int i=0; i<index;i++)
         {
             Event myEvent = events[i];
 
             Date myDate = myEvent.getTimestamp();
             rightNow.setTime(myDate);
             System.out.println("Policy Created on " + rightNow.getTime().toString());
         }
          }
     catch (Exception ee)
         {
          ee.printStackTrace();
         }
     }
 }
 
```

## 빠른 시작(SOAP): Java API를 사용하여 Word 문서에 정책 적용 {#quick-start-soap-applying-a-policy-to-a-word-document-using-the-java-api}

다음 Java 코드 예제에서는 *Loan.doc*&#x200B;이라는 Word 문서에 *복사 허용*&#x200B;이라는 정책을 적용합니다. 정책이 추가되는 정책 집합의 이름은 *전역 정책 집합*&#x200B;입니다. 정책으로 보호된 문서는 *PolicyProtectedLoanDoc.doc라는 DOC 파일로 저장됩니다. *([PDF 문서에 정책 적용](/help/forms/developing/protecting-documents-policies.md#applying-policies-to-pdf-documents)을 참조하십시오.)

```java
 /*
     * * This Java Quick Start uses the SOAP mode and contains the following JAR files
     * in the class path:
     * 1. adobe-rightsmanagement-client.jar
     * 2. adobe-livecycle-client.jar
     * 3. adobe-usermanager-client.jar
     * 4. activation.jar (required for SOAP mode)
     * 5. axis.jar (required for SOAP mode)
     * 6. commons-codec-1.3.jar (required for SOAP  mode)
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
     * These JAR files are in the following path:
     * <install directory>/sdk/client-libs/common
     *
     *
     * <install directory>/jboss/bin/client
     *
     * If you want to invoke a remote Forms Server instance and there is a
     * firewall between the client application and the server, then it is
     * recommended that you use the SOAP mode. When using the SOAP mode,
     * you have to include additional JAR files in the following
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
 import java.io.File;
 import java.io.FileInputStream;
 import com.adobe.idp.Document;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 import com.adobe.livecycle.rightsmanagement.RMSecureDocumentResult;
 import com.adobe.livecycle.rightsmanagement.client.*;
 
 public class ApplyPolicyWordDocument {
 
     public static void main(String[] args) {
     try
      {
         //Set connection properties required to invoke AEM Forms
         Properties connectionProps = new Properties();
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://'[server]:[port]'");
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
 
         //Create a ServiceClientFactory instance
         ServiceClientFactory factory = ServiceClientFactory.createInstance(connectionProps);
 
         //Create a RightsManagementClient object
         RightsManagementClient rightsClient = new RightsManagementClient(factory);
 
         //Reference a Word document to which a policy is applied
         FileInputStream is = new FileInputStream("C:\\Adobe\Loan.doc");
         Document inPDF = new Document(is);
 
         //Create a Document Manager object
         DocumentManager  documentManager = rightsClient.getDocumentManager();
 
         //Apply a policy to the Word document
         RMSecureDocumentResult rmSecureDocument=  documentManager.protectDocument(
             inPDF,
             "Loan.doc",
             "Global Policy Set",
             "Allow Copy",
             null,
             null,
             null);
 
         //Retrieve the policy-protected Word document
         Document protectPDF = rmSecureDocument.getProtectedDoc();
 
         //Save the policy-protected Word document
         File myFile = new File("C:\\PolicyProtectedLoanDoc.doc");
         protectPDF.copyToFile(myFile);
       }
     catch (Exception ee)
      {
         ee.printStackTrace();
      }
     }
 }
 
```

## 빠른 시작(SOAP 모드): Java API를 사용하여 Word 문서에서 정책 제거 {#quick-start-soap-mode-removing-a-policy-from-a-word-document-using-the-java-api}

다음 코드 예제에서는 Word 문서 *PolicyProtectedLoanDoc.doc*&#x200B;에서 정책을 제거합니다. 보안되지 않은 Word 문서가 *unProtectedLoan.doc*(으)로 저장됩니다. [Word 문서에서 정책 제거](/help/forms/developing/protecting-documents-policies.md#removing-policies-from-word-documents)를 참조하십시오.

```java
 /*
     * * This Java Quick Start uses the SOAP mode and contains the following JAR files
     * in the class path:
     * 1. adobe-rightsmanagement-client.jar
     * 2. adobe-livecycle-client.jar
     * 3. adobe-usermanager-client.jar
     * 4. activation.jar (required for SOAP mode)
     * 5. axis.jar (required for SOAP mode)
     * 6. commons-codec-1.3.jar (required for SOAP  mode)
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
     * These JAR files are in the following path:
     * <install directory>/sdk/client-libs/common
     *
     *
     * <install directory>/jboss/bin/client
     *
     * If you want to invoke a remote Forms Server instance and there is a
     * firewall between the client application and the server, then it is
     * recommended that you use the SOAP mode. When using the SOAP mode,
     * you have to include additional JAR files in the following
     * path
     * <install directory>/sdkK/client-libs/thirdparty
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
 import java.io.File;
 import java.io.FileInputStream;
 
 import com.adobe.idp.Document;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 import com.adobe.livecycle.rightsmanagement.client.*;
 
 
 public class RemovePolicyWordDocument {
 
     public static void main(String[] args) {
 
         try
         {
             //Set connection properties required to invoke AEM Forms
             Properties connectionProps = new Properties();
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://'[server]:[port]'");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
 
             //Create a ServiceClientFactory instance
             ServiceClientFactory factory = ServiceClientFactory.createInstance(connectionProps);
 
             //Create a RightsManagementClient object
             RightsManagementClient rightsClient = new RightsManagementClient(factory);
 
             //Reference a policy-protected Word document from which to remove a policy
             FileInputStream is = new FileInputStream("C:\\PolicyProtectedLoanDoc.doc");
             Document inPDF = new Document(is);
 
             //Create a Document Manager object
             DocumentManager  documentManager = rightsClient.getDocumentManager();
 
             //Remove a policy from the policy-protected Word document
             Document unsecurePDF =  documentManager.removeSecurity(inPDF);
 
             //Save the unsecured Word document
             File myFile = new File("C:\\Adobe\UnProtectedLoan.doc");
             unsecurePDF.copyToFile(myFile);
           }
 
          catch (Exception ee)
          {
           ee.printStackTrace();
          }
     }
 }
 
 
```

## 빠른 시작(SOAP 모드): Java API를 사용하여 추상 정책 만들기 {#quick-start-soap-mode-creating-an-abstract-policy-using-the-java-api}

다음 Java 코드 예제에서는 AllowCopy라는 새 추상 정책을 만듭니다. 정책이 추가되는 정책 세트의 이름은 글로벌 정책 세트입니다. 이 정책 집합은 기본적으로 존재합니다. 정책 만들기를 참조하십시오.

```java
/*
 * This Java Quick Start uses the SOAP mode and contains the following JAR files
 * in the class path:
 * 1. adobe-rightsmanagement-client.jar
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
 * These JAR files are in the following path:
 * <install directory>/Adobe/Adobe_Experience_Manager_forms/sdk/client-libs/common
 *
 * <install directory>/Adobe/Adobe_Experience_Manager_forms/sdk/client-libs/jboss
 *
 * <install directory>/Adobe/Adobe_Experience_Manager_forms/jboss/bin/client
 *
 * SOAP required JAR files are in the following path:
 * <install directory>/Adobe/Adobe_Experience_Manager_forms/sdk/client-libs/thirdparty
 *
 * If you want to invoke a remote Forms Server instance and there is a
 * firewall between the client application and Forms Server, then it is
 * recommended that you use the SOAP mode. When using the SOAP mode,
 * you have to include these additional JAR files
 *
 * For information about the SOAP
 * mode, see "Setting connection properties" in Programming
 * with Forms Server
 */

import java.util.*;

import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
import com.adobe.livecycle.rightsmanagement.client.*;
import com.adobe.livecycle.rightsmanagement.client.infomodel.*;

public class CreateAbstractPolicySoap {

    public static void main(String args[]) {

    try{

        //Set connection properties required to invoke Forms Server using SOAP mode
        Properties connectionProps = new Properties();
        connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://'[server]:[port]'");
        connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
        connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "Jboss");
        connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
        connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");

          //Create a ServiceClientFactory object
        ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps);

        //Create a RightsManagementClient object
        RightsManagementClient rightsClient = new RightsManagementClient(myFactory);

        AbstractPolicy abstractPolicy = InfomodelObjectFactory.createAbstractPolicy();

        abstractPolicy.setName("AllowCopy");
        abstractPolicy.setDescription("This abstract policy helps users to create policy that copy information from the PDF document");
        abstractPolicy.setPolicySetName("Global Policy Set");

        abstractPolicy.setOfflineLeasePeriod(30);
        abstractPolicy.setTracked(true);
        abstractPolicy.setEncryptAttachmentsOnly(false);

        ValidityPeriod validityPeriod = InfomodelObjectFactory.createValidityPeriod();
        validityPeriod.setRelativeExpirationDays(30);

        abstractPolicy.setValidityPeriod(validityPeriod);

        //Adding publisher permissions.
        AbstractPolicyEntry userPolicyEntry = InfomodelObjectFactory.createAbstractPolicyEntry();

        Permission onlinePermission = InfomodelObjectFactory.createPermission(Permission.OPEN_ONLINE);
        Permission copyPermission = InfomodelObjectFactory.createPermission(Permission.COPY);

        userPolicyEntry.addPermission(onlinePermission);
        userPolicyEntry.addPermission(copyPermission);

        abstractPolicy.addAbstractPolicyEntry(userPolicyEntry);

        AbstractPolicyManager abstractPolicyManager = rightsClient.getAbstractPolicyManager();

        abstractPolicyManager.registerAbstractPolicy(abstractPolicy, "Global Policy Set");

        AbstractPolicy abstractPolicy1 = abstractPolicyManager.getAbstractPolicy("Global Policy Set","AllowCopy");

        System.out.println("The Abstract Policy was successfully created:" + abstractPolicy1.getName());

        }
        catch (Exception ex) {
            ex.printStackTrace();
        }
    }
}
```

## 빠른 시작(SOAP 모드): Java API를 사용하여 추상 정책 수정 {#quick-start-soap-mode-modifying-an-abstract-policy-using-the-java-api}

다음 Java 코드 예제에서는 AllowCopy라는 추상 정책을 수정합니다. 정책이 수정되는 정책 세트의 이름은 글로벌 정책 세트 입니다. 이 정책 집합은 기본적으로 존재합니다. 정책 만들기를 참조하십시오.

```java
/*
 * This Java Quick Start uses the SOAP mode and contains the following JAR files
 * in the class path:
 * 1. adobe-rightsmanagement-client.jar
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
 * These JAR files are in the following path:
 * <install directory>/Adobe/Adobe_Experience_Manager_forms/sdk/client-libs/common
 *
 * <install directory>/Adobe/Adobe_Experience_Manager_forms/sdk/client-libs/jboss
 *
 * <install directory>/Adobe/Adobe_Experience_Manager_forms/jboss/bin/client
 *
 * SOAP required JAR files are in the following path:
 * <install directory>/Adobe/Adobe_Experience_Manager_forms/sdk/client-libs/thirdparty
 *
 * If you want to invoke a remote Forms Server instance and there is a
 * firewall between the client application and Forms Server, then it is
 * recommended that you use the SOAP mode. When using the SOAP mode,
 * you have to include these additional JAR files
 *
 * For information about the SOAP
 * mode, see "Setting connection properties" in Programming
 * with Forms Server
 */
import java.util.*;

import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
import com.adobe.livecycle.rightsmanagement.client.*;
import com.adobe.livecycle.rightsmanagement.client.infomodel.*;

public class ModifyingAbstractPolicySoap {

    public static void main(String args[]) {

    try{

        //Set connection properties required to invoke Forms Server using SOAP mode
        Properties connectionProps = new Properties();
        connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://'[server]:[port]'");
        connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
        connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "Jboss");
        connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
        connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");

          //Create a ServiceClientFactory object
        ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps);

        //Create a RightsManagementClient object
        RightsManagementClient rightsClient = new RightsManagementClient(myFactory);

        AbstractPolicyManager abstractPolicyManager = rightsClient.getAbstractPolicyManager();

        AbstractPolicy abstractPolicy = abstractPolicyManager.getAbstractPolicy("Global Policy Set","AllowCopy");

        //Modify policy attributes
        abstractPolicy.setOfflineLeasePeriod(40);
        abstractPolicy.setTracked(true);

        //Set the validity period to 40 days
        ValidityPeriod validityPeriod = InfomodelObjectFactory.createValidityPeriod();
        validityPeriod.setRelativeExpirationDays(40);
        abstractPolicy.setValidityPeriod(validityPeriod);

        abstractPolicyManager.updateAbstractPolicy(abstractPolicy);

        System.out.println("The Abstract Policy was updated:" + abstractPolicy.getName());

        }
        catch (Exception ex) {
            ex.printStackTrace();
        }
    }
}
```

## 빠른 시작(SOAP 모드): Java API를 사용하여 추상 정책 삭제 {#quick-start-soap-mode-deleting-an-abstract-policy-using-the-java-api}

다음 Java 코드 예제에서는 AllowCopy라는 추상 정책을 삭제합니다. 정책이 삭제되는 정책 집합은 글로벌 정책 집합으로 이름이 지정됩니다. 이 정책 집합은 기본적으로 존재합니다. 정책 만들기를 참조하십시오.

```java
/*
 * This Java Quick Start uses the SOAP mode and contains the following JAR files
 * in the class path:
 * 1. adobe-rightsmanagement-client.jar
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
 * These JAR files are in the following path:
 * <install directory>/Adobe/Adobe_Experience_Manager_forms/sdk/client-libs/common
 *
 * <install directory>/Adobe/Adobe_Experience_Manager_forms/sdk/client-libs/jboss
 *
 * <install directory>/Adobe/Adobe_Experience_Manager_forms/jboss/bin/client
 *
 * SOAP required JAR files are in the following path:
 * <install directory>/Adobe/Adobe_Experience_Manager_forms/sdk/client-libs/thirdparty
 *
 * If you want to invoke a remote Forms Server instance and there is a
 * firewall between the client application and Forms Server, then it is
 * recommended that you use the SOAP mode. When using the SOAP mode,
 * you have to include these additional JAR files
 *
 * For information about the SOAP
 * mode, see "Setting connection properties" in Programming with AEM Forms
 * with Forms Server
 */
import java.util.*;

import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
import com.adobe.livecycle.rightsmanagement.client.*;

public class DeleteAbstractPolicySoap {

    public static void main(String args[]) {

    try{

        //Set connection properties required to invoke AEM Forms using SOAP mode
        Properties connectionProps = new Properties();
        connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://'[server]:[port]'");
        connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
        connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "Jboss");
        connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
        connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");

          //Create a ServiceClientFactory object
        ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps);

        //Create a RightsManagementClient object
        RightsManagementClient rightsClient = new RightsManagementClient(myFactory);

        AbstractPolicyManager abstractPolicyManager = rightsClient.getAbstractPolicyManager();

        abstractPolicyManager.deleteAbstractPolicy("Global Policy Set", "AllowCopy");

        System.out.println("The Abstract Policy was deleted:");

        }
        catch (Exception ex) {
            ex.printStackTrace();
        }
    }
}
```

## 빠른 시작(SOAP 모드): Protect은 Java API를 사용하여 기존 사용자에 대한 명령문 워크플로의 PDF을 생성합니다 {#quick-start-soap-mode-protect-a-pdf-in-statement-workflow-for-an-existing-user-using-the-java-api}

다음 Java 코드 예제에서는 기존 사용자에 대해 Statement Workflow의 문서를 보호하는 방법을 보여 줍니다.

```java
/*
 * This Java Quick Start uses the SOAP mode and contains the following JAR files
 * in the class path:
 * 1. adobe-rightsmanagement-client.jar
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
 * These JAR files are in the following path:
 * <install directory>/Adobe/Adobe_Experience_Manager_forms/sdk/client-libs/common
 *
 * <install directory>/Adobe/Adobe_Experience_Manager_forms/sdk/client-libs/jboss
 *
 * <install directory>/Adobe/Adobe_Experience_Manager_forms/jboss/bin/client
 *
 * SOAP required JAR files are in the following path:
 * <install directory>/Adobe/Adobe_Experience_Manager_forms/sdk/client-libs/thirdparty
 *
 * If you want to invoke a remote Forms Server instance and there is a
 * firewall between the client application and Forms Server, then it is
 * recommended that you use the SOAP mode. When using the SOAP mode,
 * you have to include these additional JAR files
 *
 * For information about the SOAP
 * mode, see "Setting connection properties" in Programming
 * with Forms Server
 */
import java.util.*;
import java.io.File;
import java.io.FileInputStream;
import com.adobe.idp.Document;
import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
import com.adobe.livecycle.rightsmanagement.client.*;
import com.adobe.livecycle.rightsmanagement.RMSecureDocumentResult;
import com.adobe.edc.common.dto.PublishLicenseDTO;

public class protectStatementWorkFlowExistingUserSoap {

    public static void main(String args[]) {

        try{

            //Set connection properties required to invoke Forms Server using SOAP mode
            Properties connectionProps = new Properties();
            connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://'[server]:[port]'");
            connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
            connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "Jboss");
            connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
            connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");

            //Create a ServiceClientFactory instance
            ServiceClientFactory factory = ServiceClientFactory.createInstance(connectionProps);

            //Create a RightsManagementClient object
            RightsManagementClient rightsClient = new RightsManagementClient(factory);

            DocumentManager documentManager = rightsClient.getDocumentManager();

            //Reference a PDF document to which a policy is applied
            FileInputStream is = new FileInputStream("C:\\Adobe\\Sample.pdf");
            Document inPDF = new Document(is);

            //Get the License for existing user
            PublishLicenseDTO publishLicense = documentManager.getPublishLicenseForUser("DefaultDom","wblue");

            //protect the PDF document using license
            RMSecureDocumentResult rmSecureDocument = documentManager.protectDocument(inPDF, publishLicense);

            //Retrieve the policy-protected PDF document
            Document protectedDocument = rmSecureDocument.protectedDoc;

            //Save the policy-protected PDF document
            String outputFile = "C:\\Adobe\\PolicyProtectedSample.pdf";
            File myFile = new File(outputFile);
            protectedDocument.copyToFile(myFile);

            System.out.println("Protected the PDF With policy");

        }catch(Exception ex){
            ex.printStackTrace();
        }

}

}
```

## 빠른 시작(SOAP 모드): Protect은 Java API를 사용하여 새 사용자에 대한 명령문 워크플로의 PDF을 생성합니다 {#quick-start-soap-mode-protect-a-pdf-in-statement-workflow-for-a-new-user-using-the-java-api}

다음 Java 코드 예제에서는 Statement Workflow에서 문서를 보호하는 방법을 보여 줍니다. 2단계 프로세스입니다.

* 새 사용자, 라이선스 및 정책이 만들어집니다.
* 사용자는 라이센스 및 정책과 연결되고 문서는 보호됩니다.

```java
/*
 * This Java Quick Start uses the SOAP mode and contains the following JAR files
 * in the class path:
 * 1. adobe-rightsmanagement-client.jar
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
 * These JAR files are in the following path:
 * <install directory>/Adobe/Adobe_Experience_Manager_forms/sdk/client-libs/common
 *
 * <install directory>/Adobe/Adobe_Experience_Manager_forms/sdk/client-libs/jboss
 *
 * <install directory>/Adobe/Adobe_Experience_Manager_forms/jboss/bin/client
 *
 * SOAP required JAR files are in the following path:
 * <install directory>/Adobe/Adobe_Experience_Manager_forms/sdk/client-libs/thirdparty
 *
 * If you want to invoke a remote Forms Server instance and there is a
 * firewall between the client application and Forms Server, then it is
 * recommended that you use the SOAP mode. When using the SOAP mode,
 * you have to include these additional JAR files
 *
 * For information about the SOAP
 * mode, see "Setting connection properties" in Programming
 * with Forms Server
 */
import java.util.*;
import java.io.File;
import java.io.FileInputStream;
import com.adobe.idp.Document;
import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
import com.adobe.livecycle.rightsmanagement.client.*;
import com.adobe.livecycle.rightsmanagement.RMSecureDocumentResult;

import com.adobe.idp.um.api.infomodel.PrincipalSearchFilter;
import com.adobe.idp.um.api.infomodel.PrincipalReference;
import com.adobe.livecycle.usermanager.client.DirectoryManagerServiceClient;
import com.adobe.edc.common.dto.PublishLicenseDTO;
import com.adobe.idp.um.api.infomodel.User;
import com.adobe.idp.um.api.impl.UMBaseLibrary;

public class protectStatementWorkFlowSoap {

    public static void main(String args[]) {

        try{

            //Set connection properties required to invoke Forms Server using SOAP mode
            Properties connectionProps = new Properties();
            connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://'[server]:[port]'");
            connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
            connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "Jboss");
            connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
            connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");

            //Create a ServiceClientFactory instance
            ServiceClientFactory factory = ServiceClientFactory.createInstance(connectionProps);

            //Create a RightsManagementClient object
            RightsManagementClient rightsClient = new RightsManagementClient(factory);

            DirectoryManagerServiceClient directoryManagerServiceClient = new DirectoryManagerServiceClient(factory);

            DocumentManager documentManager = rightsClient.getDocumentManager();

            AbstractPolicyManager abstractPolicyManager = rightsClient.getAbstractPolicyManager();

            //Reference a PDF document to which a policy is applied
            FileInputStream is = new FileInputStream("C:\\Adobe\\Sample.pdf");
            Document inPDF = new Document(is);

            //Create user
            String userName = "wblue";
            User user = UMBaseLibrary.createUser(userName, "DefaultDom", userName);
            user.setCommonName(userName);
            user.setGivenName(userName);
            user.setFamilyName("User");
            directoryManagerServiceClient.createLocalUser(user, "password");

            //Ensure that the user was added
            //Create a PrincipalSearchFilter to find the user by ID
            List userList = new ArrayList<PrincipalReference>();
            PrincipalSearchFilter psf = new PrincipalSearchFilter();
            psf.setUserIdAbsolute(user.getUserid());
            psf.setRetrieveOnlyActive();
            List p = directoryManagerServiceClient.findPrincipalReferences(psf);
            PrincipalReference principal = (PrincipalReference)(p.get(0));
            userList.add(principal);

            //Create Policy From AbstractPolicy "test2"
            String newPolicyId = abstractPolicyManager.createPolicyFromAbstractPolicy("Global Policy Set", "PolicyFromAbstractPolicy_AllowCopy","Global Policy Set", "AllowCopy", userList);

            System.out.println("Created policy from abstract policy: " + newPolicyId);

            //Create License for the Policy
            PublishLicenseDTO publishLicense = documentManager.createLicense(newPolicyId, user.getUserid(), "DefaultDom");

            //get the license id from license object
            String licID = publishLicense.getLicenseId();

            //Associate User with License and Policy
            documentManager.associateUserWithLicenseAndPolicy("DefaultDom", user.getUserid(), licID, newPolicyId);

            //protect the PDF document using license
            RMSecureDocumentResult rmSecureDocument = documentManager.protectDocument(inPDF, publishLicense);

            //Retrieve the policy-protected PDF document
            Document protectedDocument = rmSecureDocument.protectedDoc;

            //Save the policy-protected PDF document
            String outputFile = "C:\\Adobe\\PolicyProtected"+ user.getUserid()+".pdf";
            File myFile = new File(outputFile);
            protectedDocument.copyToFile(myFile);

            System.out.println("Protected the PDF With policy");

        }catch(Exception ex){
            ex.printStackTrace();
        }

}

}
```
