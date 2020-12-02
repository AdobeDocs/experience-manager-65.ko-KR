---
title: 구성 요소 및 서비스 Java APIQ빠른 시작(SOAP)
seo-title: 구성 요소 및 서비스 Java APIQ빠른 시작(SOAP)
description: 구성 요소 및 서비스 Java APIQ빠른 시작(SOAP)
uuid: 7d9ade2d-f927-4558-9e80-df08bd572772
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.4/FORMS
topic-tags: develop
discoiquuid: 14f17126-e744-479b-a8e6-24c131615b46
translation-type: tm+mt
source-git-commit: a873cf3e7efd3bc9cd4744bf09078d9040efcdda
workflow-type: tm+mt
source-wordcount: '455'
ht-degree: 0%

---


# 구성 요소 및 서비스 Java API 빠른 시작(SOAP) {#components-and-services-java-apiquick-start-soap}

구성 요소 및 서비스에 대해 Java API 빠른 시작(SOAP)을 사용할 수 있습니다.


[빠른 시작(SOAP 모드):Java API를 사용하여 구성 요소 배포](components-services-java-api-quick.md#quick-start-soap-mode-deploying-a-component-using-the-java-api)

[빠른 시작(SOAP 모드):Java API를 사용하여 서비스의 실행 컨텍스트 설정](components-services-java-api-quick.md#quick-start-soap-mode-setting-the-execution-context-of-a-service-using-the-java-api)

[빠른 시작(SOAP 모드):Java API를 사용하여 서비스 보안 비활성화](components-services-java-api-quick.md#quick-start-soap-mode-disabling-service-security-using-the-java-api)

[빠른 시작(SOAP 모드):Java API를 사용하여 서비스 시작](components-services-java-api-quick.md#quick-start-soap-mode-starting-a-service-using-the-java-api)

[빠른 시작(SOAP 모드):Java API를 사용하여 서비스 구성 값 수정](components-services-java-api-quick.md#quick-start-soap-mode-modifying-a-services-configuration-values-using-the-java-api)

[빠른 시작(SOAP 모드):Java API를 사용하여 구성 요소 제거](components-services-java-api-quick.md#quick-start-soap-mode-removing-components-using-the-java-api)


AEM Forms 작업은 AEM Forms 강력한 형식의 API를 사용하여 수행할 수 있으며 연결 모드는 SOAP로 설정해야 합니다.

>[!NOTE]
>
>웹 서비스를 사용하여 구성 요소 및 서비스를 프로그래밍 방식으로 조작할 수 없습니다.

>[!NOTE]
>
>AEM 양식을 사용한 프로그래밍에서 빠른 시작은 JBoss 및 Windows 운영 체제에 배포되는 Forms 서버를 기반으로 합니다. 그러나 Unix와 같은 다른 운영 체제를 사용하는 경우에는 Windows 특정 경로를 해당 운영 체제에서 지원되는 경로로 바꿉니다. 마찬가지로 다른 J2EE 응용 프로그램 서버를 사용하는 경우 올바른 연결 속성을 지정해야 합니다. [연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)을 참조하십시오.

>[!NOTE]
>
>사용자 지정 구성 요소가 있고 SOAP 또는 EJB 프로토콜을 사용하여 동일한 로컬 서버에서 DSC를 호출하고 이러한 요청은 업그레이드 후 작동되지 않는 경우 VM([DSC_IN_VM_PASSTHROUGH_STRATEGY](https://help.adobe.com/en_US/AEMForms/6-3/ProgramLC/javadoc/com/adobe/idp/dsc/clientsdk/ServiceClientFactoryProperties.html#DSC_IN_VM_PASSTHROUGH_STRATEGY)) 호출 전략을 사용하십시오. 기본 ServiceClientFactory에서 VM 내 DSC 호출 메서드를 사용하고 SOAP 또는 EJB 프로토콜을 사용하여 ServiceClientFactory를 만들지 마십시오.

## 빠른 시작(SOAP 모드):Java API {#quick-start-soap-mode-deploying-a-component-using-the-java-api}를 사용하여 구성 요소 배포

다음 Java 예는 *adobe-emailSample-dsc.jar*&#x200B;이라는 JAR 파일을 기반으로 하는 구성 요소를 배포합니다.

```java
 /* 
        * This Java Quick Start uses the following JAR files 
        * 1. adobe-taskmanager-client.jar 
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
        * The JBoss files must be kept in the jboss\client folder. You can copy the client folder to  
        * your local development environment and then include the 3 JBoss JAR files in your class path 
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
     */ 
 import java.io.FileInputStream; 
 import java.util.*; 
  
 import com.adobe.idp.Document; 
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory; 
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties; 
 import com.adobe.idp.dsc.registry.component.client.*; 
 import com.adobe.idp.dsc.registry.infomodel.Component; 
  
 public class DeployComponents { 
  
     public static void main(String[] args) { 
          
         try{ 
          
             //Set connection properties required to invoke AEM Forms                                 
             Properties connectionProps = new Properties(); 
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://'[server]:[port]'"); 
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);           
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss"); 
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator"); 
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password"); 
                          
             //Create a ServiceClientFactory object 
             ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps); 
  
             //Create a ComponentRegistryClient object 
             ComponentRegistryClient    componentReg = new ComponentRegistryClient(myFactory);  
              
             //Reference a JAR file that represents the component to deploy 
         //    FileInputStream componentFile = new FileInputStream("C:\\Adobe\adobe-emailSample-dsc.jar");  
              
             FileInputStream componentFile = new FileInputStream("C:\\A22\Bank.jar");  
             Document component = new Document(componentFile);  
              
             //Install the component 
             Component myComponent = componentReg.install(component); 
             componentReg.start(myComponent); 
              
             System.out.println("The component has been deployed");  
             } 
              
         catch(Exception e) 
         { 
             e.printStackTrace(); 
         } 
     } 
 } 
  
 
```

## 빠른 시작(SOAP 모드):Java API {#quick-start-soap-mode-setting-the-execution-context-of-a-service-using-the-java-api}를 사용하여 서비스의 실행 컨텍스트 설정

다음 Java 코드 예제에서는 Run-As Invoker 실행 컨텍스트를 *EncryptDocument*&#x200B;이라는 예제 서비스로 설정합니다.

```java
 /* 
        * This Java Quick Start uses the following JAR files 
        * 1. adobe-taskmanager-client.jar 
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
        * The JBoss files must be kept in the jboss\bin\client folder. You can copy the client folder to  
        * your local development environment and then include the 3 JBoss JAR files in your class path 
        * 
        * These JAR files are located in the following path: 
        * <install directory>/sdk/client-libs/common 
        * 
        * 
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
     */ 
 import java.util.*; 
  
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory; 
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties; 
 import com.adobe.idp.dsc.registry.infomodel.ServiceConfiguration; 
 import com.adobe.idp.dsc.registry.service.ModifyServiceConfigurationInfo; 
 import com.adobe.idp.dsc.registry.service.client.ServiceRegistryClient; 
  
 /* 
     * This Java quick start sets the Run-As Invoker to a service named EncryptDocument 
     */ 
 public class SetRunAsConfiguration { 
      
      public static void main(String[] args) { 
  
     try{ 
         //Set connection properties required to invoke AEM Forms 
         Properties connectionProps = new Properties(); 
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://'[server]:[port]'"); 
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);           
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss"); 
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "tblue"); 
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password"); 
          
         //Create a ServiceRegistryClient object      
         ServiceClientFactory _factory = ServiceClientFactory.createInstance(connectionProps); 
         ServiceRegistryClient _src = new ServiceRegistryClient(_factory); 
          
         //Reference the EncryptDocument service 
         ServiceConfiguration _config  = _src.getHeadActiveConfiguration("EncryptDocument"); 
          
         //Set the RUN_AS_INVOKER execution context 
         ModifyServiceConfigurationInfo _configModifyInfo = new ModifyServiceConfigurationInfo(); 
         _configModifyInfo.setServiceId(_config.getServiceId()); 
         _configModifyInfo.setMajorVersion(_config.getMajorVersion()); 
         _configModifyInfo.setMinorVersion(_config.getMinorVersion()); 
         _configModifyInfo.setRunAsConfiguration(ServiceConfiguration.RUN_AS_INVOKER); 
         _config = _src.modifyConfiguration(_configModifyInfo); 
     }catch (Exception e) { 
          e.printStackTrace(); 
         }     
     } 
 } 
 
```

## 빠른 시작(SOAP 모드):Java API {#quick-start-soap-mode-disabling-service-security-using-the-java-api}를 사용하여 서비스 보안을 비활성화하는 중

다음 Java 코드 예제에서는 EncryptDocument 서비스 예와 이 서비스(값 설정 및 암호화 서비스)에서 호출되는 서비스의 보안을 비활성화합니다.

```java
 /* 
        * This Java Quick Start uses the following JAR files 
        * 1. adobe-taskmanager-client.jar 
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
        * The adobe-utilities.jar file is located in the following path: 
        * <install directory>/sdk/client-libs/jboss 
        * 
        * The jboss-client.jar file is located in the following path: 
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
     */ 
 import java.util.*; 
  
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory; 
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties; 
 import com.adobe.idp.dsc.registry.infomodel.ServiceConfiguration; 
 import com.adobe.idp.dsc.registry.service.ModifyServiceInfo; 
 import com.adobe.idp.dsc.registry.service.client.ServiceRegistryClient; 
  
 /* 
     * This Java quick start disables security from the EncryptDocument process 
     * and each service that is located in this process 
     */ 
 public class DisableSecurity{ 
      
      public static void main(String[] args) { 
  
     try{ 
         //Set connection properties required to invoke AEM Forms                                 
         Properties connectionProps = new Properties(); 
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://'[server]:[port]'"); 
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);           
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss"); 
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator"); 
         connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password"); 
                      
          
         //Create a ServiceRegistryClient object      
         ServiceClientFactory _factory = ServiceClientFactory.createInstance(connectionProps); 
         ServiceRegistryClient _src = new ServiceRegistryClient(_factory); 
          
         //Reference the EncryptDocument process and each service that is  
         //invoked from within the EncryptDocument process 
         ServiceConfiguration encryptDocumentService  = _src.getHeadActiveConfiguration("EncryptDocument"); 
         ServiceConfiguration setValueService  = _src.getHeadActiveConfiguration("SetValue"); 
         ServiceConfiguration encryptionService  = _src.getHeadActiveConfiguration("EncryptionService"); 
          
         //Create a ModifyServiceInfo object 
         ModifyServiceInfo si = new ModifyServiceInfo(); 
          
         //Disable security from the EncryptDocument service 
         si.setId(encryptDocumentService.getServiceId()); 
         si.setSecurityEnabled(false); 
         _src.modifyService(si); 
          
         //Disable security from the SetValue service 
         si.setId(setValueService.getServiceId()); 
         si.setSecurityEnabled(false); 
         _src.modifyService(si); 
          
         //Disable security from the EncryptionService 
         si.setId(encryptionService.getServiceId()); 
         si.setSecurityEnabled(false); 
         _src.modifyService(si); 
              
     }catch (Exception e) { 
          e.printStackTrace(); 
         }     
     } 
 } 
 
```

## 빠른 시작(SOAP 모드):Java API {#quick-start-soap-mode-starting-a-service-using-the-java-api}를 사용하여 서비스 시작

다음 Java 코드 예제에서는 *SendEmailService*&#x200B;라는 서비스를 시작합니다.

```java
 package com.adobe.sample.servicemanager; 
  
 /** 
     * This Java Quick Start uses the following JAR files: 
     * 1. adobe-livecycle-client.jar 
     * 2. adobe-usermanager-client.jar 
     * 3. adobe-workflow-client-sdk.jar 
     * 4. adobe-utilities.jar 
     * 5. jboss-client.jar (use a different JAR file if AEM Forms is not deployed on Jboss) 
     * 6. jacorb.jar (use a different JAR file if the forms server is not deployed on JBoss) 
     * 7. jnp-client.jar (use a different JAR file if the forms server is not deployed on JBoss) 
     */ 
 import java.util.*; 
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory; 
 import com.adobe.idp.dsc.registry.infomodel.ServiceConfiguration; 
 import com.adobe.idp.dsc.registry.service.client.ServiceRegistryClient; 
  
 public class StartService { 
  
     public static void main(String[] args) { 
          
         try{ 
             //Set connection properties required to invoke AEM Forms      
             Properties ConnectionProps = new Properties(); 
             ConnectionProps.setProperty("DSC_DEFAULT_SOAP_ENDPOINT", "https://'[server]:[port]'"); 
             ConnectionProps.setProperty("DSC_TRANSPORT_PROTOCOL","SOAP");           
             ConnectionProps.setProperty("DSC_SERVER_TYPE", "JBoss"); 
             ConnectionProps.setProperty("DSC_CREDENTIAL_USERNAME", "administrator"); 
             ConnectionProps.setProperty("DSC_CREDENTIAL_PASSWORD", "password"); 
              
             //Create a ServiceClientFactory object 
             ServiceClientFactory myFactory = ServiceClientFactory.createInstance(ConnectionProps); 
  
             //Create a ServiceRegistryClient object 
             ServiceRegistryClient serviceReg = new ServiceRegistryClient(myFactory);  
          
             //Reference the SendEmailService 
             ServiceConfiguration myServiceConfig = serviceReg.getHeadActiveConfiguration("SendEmailService"); 
          
             //Start the SendEmailService 
             serviceReg.start(myServiceConfig); 
             } 
              
                 catch(Exception e) 
                 { 
                     e.printStackTrace(); 
                 } 
     } 
 } 
  
 
```

## 빠른 시작(SOAP 모드):Java API {#quick-start-soap-mode-modifying-a-services-configuration-values-using-the-java-api}를 사용하여 서비스 구성 값 수정

다음 Java 예는 SendEmail 서비스에 속하는 구성 값을 수정합니다.

```java
 /* 
     * This Java Quick Start uses the following JAR files 
        * 1. adobe-taskmanager-client.jar 
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
        * The JBoss files must be kept in the jboss\client folder. You can copy the client folder to  
        * your local development environment and then include the 3 JBoss JAR files in your class path 
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
     */ 
 import java.util.*; 
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory; 
 import com.adobe.idp.dsc.registry.infomodel.ConfigParameter; 
 import com.adobe.idp.dsc.registry.infomodel.ServiceConfiguration; 
 import com.adobe.idp.dsc.registry.service.ModifyServiceConfigurationInfo; 
 import com.adobe.idp.dsc.registry.service.client.ServiceRegistryClient; 
  
  
 public class ModifyService { 
  
     public static void main(String[] args) { 
          
         try{ 
             //Set connection properties required to invoke AEM Forms     
             Properties ConnectionProps = new Properties(); 
             ConnectionProps.setProperty("DSC_DEFAULT_SOAP_ENDPOINT", "https://'[server]:[port]'"); 
             ConnectionProps.setProperty("DSC_TRANSPORT_PROTOCOL","SOAP");           
             ConnectionProps.setProperty("DSC_SERVER_TYPE", "JBoss"); 
             ConnectionProps.setProperty("DSC_CREDENTIAL_USERNAME", "administrator"); 
             ConnectionProps.setProperty("DSC_CREDENTIAL_PASSWORD", "password"); 
              
             //Create a ServiceClientFactory object 
             ServiceClientFactory myFactory = ServiceClientFactory.createInstance(ConnectionProps); 
  
             //Create a ServiceRegistryClient object 
             ServiceRegistryClient serviceReg = new ServiceRegistryClient(myFactory);  
          
             //Reference the SendEmailService 
             ServiceConfiguration myServiceConfig = serviceReg.getHeadServiceConfiguration("SendEmailService"); 
                              
             //Create a ModifyServiceConfigurationInfo object 
                 ModifyServiceConfigurationInfo modService = new ModifyServiceConfigurationInfo(); 
                      
             //Set configuration values required by the SendEmailService 
             String serviceId = myServiceConfig.getServiceId(); 
             modService.setServiceId(serviceId); 
             modService.setMajorVersion(1); 
             modService.setConfigParameterAsText("smtpHost","mySMTPSERVER"); 
             modService.setConfigParameterAsText("smtpUser","smyUserName");     
             modService.setConfigParameterAsText("smtpPassword","myPassword");     
                      
             //Modify the service’s configuration values 
             serviceReg.modifyConfiguration(modService); 
                          
             //Conform the new configuration values 
             ServiceConfiguration serviceConfig = serviceReg.getServiceConfiguration("SendEmailService",1,0); 
             ConfigParameter cp = serviceConfig.getConfigParameter("smtpUser"); 
             String configValue = cp.getTextValue();  
             System.out.println(configValue); 
             } 
      
             catch(Exception e) 
             { 
                 e.printStackTrace(); 
             } 
     } 
 } 
  
  
 
```

## 빠른 시작(SOAP 모드):Java API {#quick-start-soap-mode-removing-components-using-the-java-api}를 사용하여 구성 요소 제거

다음 Java 코드 예제에서는 Java API를 사용하여 구성 요소를 제거합니다.

```java
 /* 
     * This Java Quick Start uses the following JAR files 
     * 1. adobe-taskmanager-client.jar 
     * 2. adobe-livecycle-client.jar 
     * 3. adobe-usermanager-client.jar 
     * 4. adobe-utilities.jar 
     * 5. jboss-client.jar (use a different JAR file if the forms server is not deployed 
     * on JBoss) 
     * 6. commons-code-1.3.jar 
     * 7. adobe-workflow-client-sdk.jar 
     * 8. jacorb.jar (use a different JAR file if the forms server is not deployed on JBoss) 
     * 9. jnp-client.jar (use a different JAR file if the forms server is not deployed on JBoss) 
     * 
     * The JBoss files must be kept in the jboss\client folder. You can copy the client folder to  
     * your local development environment and then include the 3 JBoss JAR files in your class path 
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
     */ 
 import java.util.*; 
  
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory; 
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties; 
 import com.adobe.idp.dsc.registry.component.client.*; 
 import com.adobe.idp.dsc.registry.infomodel.Component; 
  
 public class RemoveComponent { 
  
     public static void main(String[] args) { 
          
         try{ 
               //Set connection properties required to invoke AEM Forms                                                                                                                        
               Properties connectionProps = new Properties(); 
               connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://'[server]:[port]'"); 
      connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);           
               connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss"); 
               connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator"); 
               connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password"); 
              
             //Create a ServiceClientFactory object 
             ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps); 
  
             //Create a ComponentRegistryClient object 
             ComponentRegistryClient    componentReg = new ComponentRegistryClient(myFactory);  
              
             //Retrieve the Id of the component to remove from the service container 
             Component myComponent = componentReg.getComponent("com.adobe.livecycle.sample.email.emailSampleComponent", "1.0"); 
              
             //Determine if the component is in a running state 
             if (myComponent.getState()== Component.RUNNING) 
             { 
                 //Stop the component 
                 Component stoppedComponent = componentReg.stop(myComponent); 
                  
                 //Uninstall the component 
                 componentReg.uninstall(stoppedComponent); 
             } 
             else 
                 componentReg.uninstall(myComponent); 
                  
             System.out.println("The component was removed."); 
             } 
              
             catch(Exception e) 
             { 
                 e.printStackTrace(); 
             } 
     } 
 } 
  
  
 
```

