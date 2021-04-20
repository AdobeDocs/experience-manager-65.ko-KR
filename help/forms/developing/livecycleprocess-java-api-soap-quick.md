---
title: LiveCycleProcess Java API(SOAP)빠른 시작
seo-title: LiveCycleProcess Java API(SOAP)빠른 시작
description: 'LiveCycleProcess Java API(SOAP) 빠른 시작을 사용하여 프로세스 인스턴스를 검색하고, 프로세스 인스턴스를 일시 중단하며, 일시 중단된 프로세스 인스턴스를 시작하고, 프로세스 인스턴스를 종료하며, 프로세스 데이터를 삭제하고 작업 상태를 검색할 수 있습니다. '
seo-description: LiveCycleProcess Java API(SOAP) 빠른 시작을 사용하여 프로세스 인스턴스를 검색하고, 프로세스 인스턴스를 일시 중단하며, 일시 중단된 프로세스 인스턴스를 시작하고, 프로세스 인스턴스를 종료하며, 프로세스 데이터를 삭제하고 작업 상태를 검색할 수 있습니다.
uuid: ad14fb50-8dd5-44e0-9e48-f0f0334e04d6
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: 9c17fa2d-0337-4204-822e-dcdafebf0e4d
role: Developer
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '468'
ht-degree: 0%

---


# LiveCycleProcess Java API(SOAP) 빠른 시작 {#livecycleprocess-java-api-soap-quick-start}

Java API(SOAP) 빠른 시작을 프로세스에 사용할 수 있습니다. *프로세스 인스턴스*&#x200B;는 호출 API와 같은 호출 방법이나 Workspace 내에서 시작된 특정 프로세스의 발생을 말합니다.

[빠른 시작(SOAP 모드):Java API를 사용하여 프로세스 인스턴스 검색](livecycleprocess-java-api-soap-quick.md#quick-start-soap-mode-searching-for-process-instances-using-the-java-api)

[빠른 시작(SOAP 모드):Java API를 사용하여 프로세스 인스턴스 일시 중단](livecycleprocess-java-api-soap-quick.md#quick-start-soap-mode-suspending-process-instances-using-the-java-api)

[빠른 시작(SOAP 모드):Java API를 사용하여 일시 중단된 프로세스 인스턴스 시작](livecycleprocess-java-api-soap-quick.md#quick-start-soap-mode-starting-suspended-process-instances-using-the-java-api)

[빠른 시작(SOAP 모드):Java API를 사용하여 프로세스 인스턴스 종료](livecycleprocess-java-api-soap-quick.md#quick-start-soap-mode-terminating-process-instances-using-the-java-api)

[빠른 시작(SOAP 모드):Java API를 사용하여 프로세스 데이터 제거](livecycleprocess-java-api-soap-quick.md#quick-start-soap-mode-purging-process-data-using-the-java-api)

[빠른 시작(SOAP 모드):Java API를 사용하여 작업 상태 검색](livecycleprocess-java-api-soap-quick.md#quick-start-soap-mode-retrieving-the-status-of-a-job-using-the-java-api)

AEM Forms 작업은 AEM Forms 강력한 형식의 API를 사용하여 수행할 수 있으며 연결 모드는 SOAP로 설정해야 합니다.

>[!NOTE]
>
>Unix와 같은 다른 운영 체제를 사용하는 경우 AEM Forms으로 프로그래밍에 있는 빠른 시작은 Forms을 기반으로 하며, Windows 특정 경로를 해당 운영 체제에서 지원되는 경로로 바꿉니다. 마찬가지로 다른 J2EE 응용 프로그램 서버를 사용하는 경우 유효한 연결 속성을 지정해야 합니다. ([연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)을 참조하십시오.)

## 빠른 시작(SOAP 모드):Java API {#quick-start-soap-mode-searching-for-process-instances-using-the-java-api}을 사용하여 프로세스 인스턴스 검색

다음 Java 코드 예제에서는 *MortgageLoan - Prebuilt* 프로세스를 기반으로 하는 프로세스 인스턴스를 검색합니다.

```java
 /*
     * This Java Quick Start uses the following JAR files
     * 1. adobe-taskmanager-client.jar
     * 2. adobe-livecycle-client.jar
     * 3. adobe-usermanager-client.jar
     * 4. activation.jar (required for SOAP mode)
     * 5. axis.jar (required for SOAP mode)
     * 6. commons-codec-1.3.jar (required for SOAP mode)
     * 7. commons-collections-3.2.jar  (required for SOAP  mode)
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
     * 20. adobe-workflow-client-sdk.jar
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
     */
 import java.util.*;
 
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 import com.adobe.idp.taskmanager.dsc.client.TaskManagerClientFactory;
 import com.adobe.idp.taskmanager.dsc.client.TaskManagerQueryService;
 import com.adobe.idp.taskmanager.dsc.client.query.ProcessInstanceRow;
 import com.adobe.idp.taskmanager.dsc.client.query.ProcessSearchFilter;
 import com.adobe.idp.workflow.client.ProcessManager;
 
 /**
     * This Java Quick Start searches for all completed processes that are based on the application
     * and tracks the time at which the processes where completed.
     *
     */
 public class SearchingProcesses {
 
     public static void main(String[] args) {
         try{
 
             //Set connection properties required to invoke AEM Forms
             Properties connectionProps = new Properties();
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://'[server]:[port]'");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "tblue");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
 
             //Create a ServiceClientFactory object
             ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps);
             TaskManagerQueryService queryProcess = TaskManagerClientFactory.getQueryManager(myFactory);
 
             ProcessSearchFilter processFilter = new ProcessSearchFilter();
             processFilter.setServiceName("MortgageLoan - Prebuilt");
 
             List allProcesses = queryProcess.processSearch(processFilter);
 
             //Create an Iterator object and iterate through
 //             the List object
            Iterator iter = allProcesses.iterator();
            int i = 0 ;
            long processId=0 ;
            while (iter.hasNext()) {
                ProcessInstanceRow processInstance = (ProcessInstanceRow)iter.next();
 
           if (processInstance.getProcessInstanceStatus() == ProcessInstanceRow.STATUS_RUNNING){
 
             //Display the process d
             processId = processInstance.getProcessInstanceId();
             System.out.println("The process identifier is " +processId);
           }
 
             i++;
            }
         }
 
         catch(Exception e)
         {
             e.printStackTrace();
         }
     }
 
 
 
 
 }
 
```

## 빠른 시작(SOAP 모드):Java API {#quick-start-soap-mode-suspending-process-instances-using-the-java-api}을(를) 사용하여 프로세스 인스턴스 일시 중단

다음 Java 코드 예제에서는 프로세스 인스턴스를 일시 중단합니다. 프로세스 인스턴스를 성공적으로 일시 중단하려면 호출 API를 사용하여 긴 기간 프로세스를 호출할 때 가져올 수 있는 프로세스 호출 식별자가 필요합니다.

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
     * 20. adobe-workflow-client-sdk.jar
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
     */
 import java.util.*;
 
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 import com.adobe.idp.um.api.infomodel.PrincipalSearchFilter;
 import com.adobe.idp.workflow.client.ProcessManager;
 
 
 public class SuspendProcesses {
 
 
     public static void main(String[] args) {
          try{
 
                  //Set connection properties required to invoke AEM Forms
                 Properties connectionProps = new Properties();
                 connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://'[server]:[port]'");
                 connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
                 connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
                 connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "tblue");
                 connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
 
                   //Create a ServiceClientFactory object
                    ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps);
 
                    //Create a ProcessManager object
                    ProcessManager myProcessManager = new ProcessManager(myFactory);
                    myProcessManager.suspendProcess("1");
              }
                catch(Exception e)
                 {
                       e.printStackTrace();
                }
 
 
 
     }
 
 }
 
 
```

## 빠른 시작(SOAP 모드):Java API {#quick-start-soap-mode-starting-suspended-process-instances-using-the-java-api}을(를) 사용하여 일시 중단된 프로세스 인스턴스 시작

다음 Java 코드 예제에서는 일시 중단된 프로세스 인스턴스를 시작합니다.

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
     * 20. adobe-workflow-client-sdk.jar
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
     */
 
 import java.util.*;
 
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 import com.adobe.idp.workflow.client.ProcessManager;
 
 public class StartProcess {
 
     public static void main(String[] args) {
         try{
 
             //Set connection properties required to invoke AEM Forms
             Properties connectionProps = new Properties();
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://'[server]:[port]'");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "tblue");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
 
             //Create a ServiceClientFactory object
             ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps);
 
             //Create a ProcessManager object
             ProcessManager myProcessManager = new ProcessManager(myFactory);
 
             //Start a suspended process instance
              myProcessManager.unSuspendProcess("5fae07190a242fb1010b2229ccad8a7e");
             }
 
         catch(Exception e)
         {
             e.printStackTrace();
         }
     }
 }
 
```

## 빠른 시작(SOAP 모드):Java API {#quick-start-soap-mode-terminating-process-instances-using-the-java-api}을(를) 사용하여 프로세스 인스턴스를 종료하는 중

다음 Java 코드 예제에서는 식별자 값이 756c22860a242fb101ec7a5bc0977fd6인 프로세스 인스턴스를 종료합니다.

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
     * 20. adobe-workflow-client-sdk.jar
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
     */
 
 import java.util.*;
 
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 import com.adobe.idp.workflow.client.ProcessManager;
 
 public class TerminatingProcesses {
 
     public static void main(String[] args) {
         try{
 
             //Set connection properties required to invoke AEM Forms
             Properties connectionProps = new Properties();
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://'[server]:[port]'");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "tblue");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
 
 
             //Create a ServiceClientFactory object
             ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps);
 
             //Create a ProcessManager object
             ProcessManager myProcessManager = new ProcessManager(myFactory);
 
 
             myProcessManager.terminateProcess("sd");
             //Terminate a process instance
         //       myProcessManager.terminateProcess("756c22860a242fb101ec7a5bc0977fd6");
             }
 
         catch(Exception e)
         {
             e.printStackTrace();
         }
     }
 }
 
```

## 빠른 시작(SOAP 모드):Java API {#quick-start-soap-mode-purging-process-data-using-the-java-api}를 사용하여 프로세스 데이터 제거

다음 Java 코드는 *SecureDocument*&#x200B;라는 프로세스에서 데이터를 삭제합니다. *inValue*&#x200B;라는 프로세스 변수가 200보다 큰 프로세스 인스턴스의 데이터를 제거하도록 지정하는 필터가 사용됩니다.

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
     */
 
 import java.util.*;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 import com.adobe.idp.workflow.client.ProcessManager;
 import com.adobe.idp.workflow.dsc.type.*;
 
 public class PurgeProcess
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
 
              //Create a ServiceClientFactory instance
              ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps);
 
            //Create a ProcessManager object
           ProcessManager myProcessManager = new ProcessManager(myFactory);
 
           //Prepare parameters to use in the purge operation
              long age = 10;  // in seconds
              boolean includeChildren = false;// don't include children by default
              int status = 3;   // both completed and terminated by default
              short minor = 0;
              short major = 1;
 
             //Create the conditionFilter object to filter
             //out unwanted instances of the process
             ConditionFilter filter = new ConditionFilter("inValue", ConditionEnum.GREATER_THAN, "200");
 
             //Delete process instances that contain a process
             //variable named inValue whose value
             //is greater than 200
             myProcessManager.purgeProcess(
               "SecureDocument",
               major,
               minor,
               status,
               age,
               filter,
               includeChildren);
       }
     catch (Exception e)
             {
               e.printStackTrace();
              }
         }
 }
 
```

## 빠른 시작(SOAP 모드):Java API {#quick-start-soap-mode-retrieving-the-status-of-a-job-using-the-java-api}을 사용하여 작업 상태 검색

다음 코드 예제에서는 10개의 AEM Forms 작업 상태를 검색합니다.

```java
 /*
     * This Java Quick Start uses the SOAP mode and contains the following JAR files
     * in the class path:
     * 1. adobe-encryption-client.jar
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
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 import com.adobe.idp.jobmanager.client.JobManager;
 import com.adobe.idp.jobmanager.common.JobInstance;
 import com.adobe.idp.jobmanager.common.JobInstanceFilter;
 
 
 public class SearchForJobs {
 
     public static void main(String[] args) {
 
     //This function will upload a ceritificate to AEM Forms trust store
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
         JobManager jobManager= new JobManager(myFactory);
 
         //Specify filter criteria
         JobInstanceFilter jobFilter = new JobInstanceFilter();
         jobFilter.setMaxObjects(10);
 
         //Retrieve the first 10 jobs
         List<JobInstance> allJobs = jobManager.getJobInstances(jobFilter);
 
         //Create an Iterator object and iterate through
         //the List object
         Iterator iter = allJobs.iterator();
         int i = 0 ;
         while (iter.hasNext()) {
             JobInstance JobInstance = (JobInstance)iter.next();
             System.out.println("The status of the job is " +JobInstance.getStatus() +". The identifier value of the job is " +JobInstance.getId()+ ". The service on which the job is based is " +JobInstance.getServiceName());
             i++;
         }
 
       }catch (Exception e) {
              e.printStackTrace();
             }
 
     }
 }
 
 
```

