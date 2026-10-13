---
title: 자격 증명 서비스 Java&trade, API 빠른 시작(SOAP)
description: Java&trade; API 빠른 시작(SOAP)을 사용하여 AEM Forms에서 자격 증명을 가져오고 삭제하는 방법에 대해 알아봅니다.
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
role: Developer
exl-id: 0ea00ef5-9923-4c03-a724-32f9ebdc650f
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,APIs & Integrations,AEM Forms on JEE
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: 516393bc-fa69-5e74-a04e-f7ec9ffe2c5e
    internal-label: APIs & Integrations
  - id: 94663796-0ee7-58b9-84f4-b425ebb69e83
    internal-label: AEM Forms on JEE
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '233'
ht-degree: 0%
---
# 자격 증명 서비스 Java™ API 빠른 시작(SOAP) {#credential-service-java-api-quickstart-soap}

자격 증명 서비스에 Java™ API 빠른 시작(SOAP)을 사용할 수 있습니다.

[빠른 시작(SOAP 모드): Java™ API를 사용하여 자격 증명 가져오기](credential-service-java-api-quick.md#quick-start-soap-mode-importing-credentials-using-the-java-api)

[빠른 시작(SOAP 모드): Java™ API를 사용하여 자격 증명 삭제](credential-service-java-api-quick.md#quick-start-soap-mode-deleting-credentials-using-the-java-api)

AEM Forms 작업은 AEM Forms 강력한 형식의 API를 사용하여 수행할 수 있으며 연결 모드를 SOAP으로 설정해야 합니다.

>[!NOTE]
>
>AEM Forms를 사용한 프로그래밍의 빠른 시작은 JBoss® 및 Windows 운영 체제에 배포되는 Forms 서버를 기반으로 합니다. 그러나 UNIX®와 같은 다른 운영 체제를 사용하는 경우에는 Windows 특정 경로를 해당 운영 체제에서 지원하는 경로로 바꿉니다. 마찬가지로 다른 J2EE 응용 프로그램 서버를 사용하는 경우 유효한 연결 속성을 지정해야 합니다. [연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)을 참조하세요.

>[!NOTE]
>
>웹 서비스를 사용하여 자격 증명 서비스 작업을 수행할 수 없습니다.

## 빠른 시작(SOAP 모드): Java™ API를 사용하여 자격 증명 가져오기 {#quick-start-soap-mode-importing-credentials-using-the-java-api}

다음 코드 예제에서는 *cred.p12* 파일을 기반으로 자격 증명을 가져옵니다. 자격 증명을 가져오는 데 사용되는 별칭 값은 `Secure`입니다. [Trust Manager API를 사용하여 자격 증명 가져오기](/help/forms/developing/credentials.md#importing-credentials-by-using-the-trust-manager-api)를 참조하십시오.

```java
 /*
     * This Java Quick Start uses the SOAP mode and contains the following JAR files
     * in the class path:
     * 1. adobe-truststore-client.jar
     * 2. adobe-livecycle-client.jar
     * 3. adobe-usermanager-client.jar
     * 4. adobe-utilities.jar
     * 5. jboss-client.jar (use a different JAR file if the Forms Server is not deployed
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
     * These JAR files are in the following path:
     * <install directory>/sdk/client-libs/common
     *
     * The adobe-utilities.jar file is in the following path:
     * <install directory>/sdk/client-libs/jboss
     *
     * The jboss-client.jar file is in the following path:
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
 import java.io.FileInputStream;
 import java.util.Properties;
 import com.adobe.idp.Document;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 import com.adobe.truststore.client.CredentialServiceClient;
 
 public class ImportCredentialSoap {
 
     public static void main(String[] args) {
            try {
 
          //Set connection properties required to invoke AEM Forms using SOAP mode
              Properties connectionProps = new Properties();
              connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://'[server]:[port]'");
              connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
              connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
              connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
              connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
 
             //Create a ServiceClientFactory object
             ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps);
 
             //Create a CredentialServiceClient instance
             CredentialServiceClient certClient = new CredentialServiceClient(myFactory);
 
             //Reference a credential based on a P12 file
             FileInputStream myCred = new FileInputStream("C:\\Adobe\cred.p12");
             Document credential = new Document(myCred);
 
             //Create a string array to store usage values
             String[] usage = new String[1];
             usage[0] = "truststore.usage.type.sign";
 
             //Import the credential
             certClient.importCredential("secure",credential,"password",usage);
             System.out.println("Credential was uploaded");
 
            }catch (Exception e) {
                e.printStackTrace();
            }
 
            }
 }
 
 
 
```

## 빠른 시작(SOAP 모드): Java™ API를 사용하여 자격 증명 삭제 {#quick-start-soap-mode-deleting-credentials-using-the-java-api}

다음 코드 예제에서는 별칭 값 *secure*&#x200B;을(를) 기반으로 자격 증명을 삭제합니다. [Trust Manager API를 사용하여 자격 증명 삭제](/help/forms/developing/credentials.md#deleting-credentials-by-using-the-trust-manager-api)를 참조하십시오.

```java
 /*
     * This Java Quick Start uses the SOAP mode and contains the following JAR files
     * in the class path:
     * 1. adobe-truststore-client.jar
     * 2. adobe-livecycle-client.jar
     * 3. adobe-usermanager-client.jar
     * 4. adobe-utilities.jar
     * 5. jboss-client.jar (use a different JAR file if the Forms Server is not deployed
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
     * These JAR files are in the following path:
     * <install directory>/sdk/client-libs/common
     *
     * The adobe-utilities.jar file is in the following path:
     * <install directory>/sdk/client-libs/jboss
     *
     * The jboss-client.jar file is in the following path:
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
 
 import java.util.Properties;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 import com.adobe.truststore.client.CredentialServiceClient;
 
 public class DeleteCertificateSoap {
 
 
     public static void main(String[] args)
     {
     try {
 
         //Set connection properties required to invoke AEM Forms using SOAP mode
         Properties connectionProps = new Properties();
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://'[server]:[port]'");
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
 
         //Create a ServiceClientFactory object
         ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps);
 
         //Create a CredentialServiceClient instance
         CredentialServiceClient certClient = new CredentialServiceClient(myFactory);
 
         //Delete the certificate
         certClient.deleteCredential("secure");
         System.out.println("Credential was deleted");
 
        }catch (Exception e) {
            e.printStackTrace();
        }
 
        }
 
 }
 
```
