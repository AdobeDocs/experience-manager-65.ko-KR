---
title: 사용자 관리자 Java API 빠른 시작(SOAP)
seo-title: 사용자 관리자 Java API 빠른 시작(SOAP)
description: User Manager API를 사용하여 사용자를 추가, 삭제, 그룹 생성, 사용자 및 그룹 관리, 역할 및 권한 관리, 프로그래밍 방식으로 사용자 동기화, 환경 설정 노드 프로그래밍 방식으로 관리
seo-description: User Manager API를 사용하여 사용자를 추가, 삭제, 그룹 생성, 사용자 및 그룹 관리, 역할 및 권한 관리, 프로그래밍 방식으로 사용자 동기화, 환경 설정 노드 프로그래밍 방식으로 관리
uuid: 0a2aa4ab-9329-485f-a30e-47bb471ce1b5
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: e0c20fd2-b084-4f61-936c-5282826a8d3d
translation-type: tm+mt
source-git-commit: 07889ead2ae402b5fb738ca08c7efe076ef33e44
workflow-type: tm+mt
source-wordcount: '529'
ht-degree: 0%

---


# 사용자 관리자 Java API 빠른 시작(SOAP) {#user-manager-java-api-quick-start-soap}

Java API 빠른 시작(SOAP)은 사용자 관리자 API에 사용할 수 있습니다.

[빠른 시작(SOAP 모드):Java API를 사용하여 사용자 추가](user-manager-java-api-quick.md#quick-start-soap-mode-adding-users-using-the-java-api)

[빠른 시작(SOAP 모드):Java API를 사용하여 사용자 삭제](user-manager-java-api-quick.md#quick-start-soap-mode-deleting-users-using-the-java-api)

[빠른 시작(SOAP 모드):Java API를 사용하여 그룹 만들기](user-manager-java-api-quick.md#quick-start-soap-mode-creating-groups-using-the-java-api)

[빠른 시작(SOAP 모드):Java API를 사용하여 사용자 및 그룹 관리](user-manager-java-api-quick.md#quick-start-soap-mode-managing-users-and-groups-using-the-java-api)

[빠른 시작(SOAP 모드):Java API를 사용하여 역할 및 권한 관리](user-manager-java-api-quick.md#quick-start-soap-mode-managing-roles-and-permissions-using-the-java-api)

[빠른 시작(SOAP 모드):Java API를 사용하여 프로그래밍 방식으로 사용자 동기화](user-manager-java-api-quick.md#quick-start-soap-mode-programmatically-synchronizing-users-using-the-java-api)

[빠른 시작(SOAP 모드):Java API를 사용하여 프로그래밍 방식으로 환경 설정 노드 관리](user-manager-java-api-quick.md#quick-start-soap-mode-programmatically-managing-the-preferences-nodes-using-the-java-api)

AEM Forms 작업은 AEM Forms 강력한 형식의 API를 사용하여 수행할 수 있으며 연결 모드는 SOAP로 설정해야 합니다.

>[!NOTE]
>
>AEM 양식을 사용한 프로그래밍에 있는 빠른 시작은 Unix와 같은 다른 운영 체제를 사용하는 경우 문서를 기반으로 하며 Windows 특정 경로를 해당 운영 체제에서 지원되는 경로로 바꿉니다. 마찬가지로 다른 J2EE 응용 프로그램 서버를 사용하는 경우 유효한 연결 속성을 지정해야 합니다. [연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)을 참조하십시오.

## 빠른 시작(SOAP 모드):Java API {#quick-start-soap-mode-adding-users-using-the-java-api}을(를) 사용하여 사용자 추가

다음 코드 예제에서는 Wendy Blue라는 사용자를 AEM Forms에 추가합니다. ([사용자 추가](/help/forms/developing/users.md#adding-users)를 참조하십시오.)

```java
 /*
     * This Java Quick Start uses the SOAP mode and contains the following JAR files
     * in the class path:
     * 1. adobe-livecycle-client.jar
     * 2. adobe-usermanager-client.jar
    * 3. activation.jar (required for SOAP mode)
    * 4. axis.jar (required for SOAP mode)
    * 5. commons-codec-1.3.jar (required for SOAP mode)
    * 6. commons-collections-3.2.jar  (required for SOAP mode)
    * 7. commons-discovery.jar (required for SOAP mode)
    * 8. commons-logging.jar (required for SOAP mode)
    * 9. dom3-xml-apis-2.5.0.jar (required for SOAP mode)
    * 10. jaxen-1.1-beta-9.jar (required for SOAP mode)
    * 11. jaxrpc.jar (required for SOAP mode)
    * 12. log4j.jar (required for SOAP mode)
    * 13. mail.jar (required for SOAP mode)
    * 14. saaj.jar (required for SOAP mode)
    * 15. wsdl4j.jar (required for SOAP mode)
    * 16. xalan.jar (required for SOAP mode)
    * 17. xbean.jar (required for SOAP mode)
    * 18. xercesImpl.jar (required for SOAP mode)
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
 import com.adobe.livecycle.usermanager.client.DirectoryManagerServiceClient;
 import com.adobe.idp.um.api.infomodel.impl.*;
 import com.adobe.idp.um.api.infomodel.*;
 
 public class AddUser {
 
     public static void main(String[] args) {
         try {
             //Set connection properties required to invoke AEM Forms
                Properties connectionProps = new Properties();
                connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://'[server]:[port]'");
      connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
                connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
                connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
                connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
 
             //Create a ServiceClientFactory object
             ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps);
 
             //Create an DirectoryManagerServiceClient object
             DirectoryManagerServiceClient dmClient = new DirectoryManagerServiceClient(myFactory);
 
             //Create a User object and populate its attributes
             UserImpl u = new UserImpl();
             u.setDomainName("DefaultDom");
             u.setUserid("wblue");
             u.setCanonicalName("wblue");
             u.setPrincipalType("USER");
             u.setGivenName("Wendy");
             u.setFamilyName("Blue");
             u.setLocale(Locale.CANADA);
             u.setTimezone(TimeZone.getDefault());
             u.setDisabled(false);
 
             //Add the User to the system using the DirectoryManagerServiceClient
             dmClient.createLocalUser(u,"password");
 
             //Ensure that the user was added
             //Create a PrincipalSearchFilter to find the user by ID
             PrincipalSearchFilter psf = new PrincipalSearchFilter();
             psf.setUserId("wblue");
             List<User> principalList = dmClient.findPrincipals(psf);
             Iterator<User> pit = principalList.iterator();
             if(pit.hasNext()){
                 User theUser = pit.next();
                 System.out.println("User ID: " + theUser.getUserid());
                 System.out.println("User name: " + theUser.getGivenName() +" "+ theUser.getFamilyName());
                 System.out.println("User Domain: " + theUser.getDomainName());
                 System.out.println("is user disabled?: " + theUser.isDisabled());
             }
 
         }catch (Exception e) {
             e.printStackTrace();
         }
 ;
     }
 
 }
 
 
```

## 빠른 시작(SOAP 모드):Java API {#quick-start-soap-mode-deleting-users-using-the-java-api}을(를) 사용하여 사용자 삭제

다음 코드 예제에서는 AEM Forms에서 Wendy Blue라는 사용자를 삭제합니다. ([사용자 삭제](/help/forms/developing/users.md#deleting-users)를 참조하십시오.)

```java
 /*
     * This Java Quick Start uses the SOAP mode and contains the following JAR files
     * in the class path:
     * 1. adobe-livecycle-client.jar
     * 2. adobe-usermanager-client.jar
    * 3. activation.jar (required for SOAP mode)
    * 4. axis.jar (required for SOAP mode)
    * 5. commons-codec-1.3.jar (required for SOAP mode)
    * 6. commons-collections-3.2.jar  (required for SOAP mode)
    * 7. commons-discovery.jar (required for SOAP mode)
    * 8. commons-logging.jar (required for SOAP mode)
    * 9. dom3-xml-apis-2.5.0.jar (required for SOAP mode)
    * 10. jaxen-1.1-beta-9.jar (required for SOAP mode)
    * 11. jaxrpc.jar (required for SOAP mode)
    * 12. log4j.jar (required for SOAP mode)
    * 13. mail.jar (required for SOAP mode)
    * 14. saaj.jar (required for SOAP mode)
    * 15. wsdl4j.jar (required for SOAP mode)
    * 16. xalan.jar (required for SOAP mode)
    * 17. xbean.jar (required for SOAP mode)
    * 18. xercesImpl.jar (required for SOAP mode)
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
 import com.adobe.idp.um.api.infomodel.PrincipalSearchFilter;
 import com.adobe.idp.um.api.infomodel.User;
 import com.adobe.livecycle.usermanager.client.DirectoryManagerServiceClient;
 
 public class DeleteUser {
 
     public static void main(String[] args) {
         try {
             //Set connection properties required to invoke AEM Forms
             Properties connectionProps = new Properties();
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://'[server]:[port]'");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL, ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, ServiceClientFactoryProperties.DSC_JBOSS_SERVER_TYPE);
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
 
             // Create a ServiceClientFactory object
             ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps);
 
             // Create a DirectoryManagerServiceClient object
             DirectoryManagerServiceClient dm = new DirectoryManagerServiceClient(myFactory);
 
             //Find the target user by the user ID value
             PrincipalSearchFilter psf = new PrincipalSearchFilter();
             psf.setUserId("wblue");
             List<User> principalList = dm.findPrincipals(psf);
             Iterator<User> pit = principalList.iterator();
 
             //Delete the user
             while(pit.hasNext()){
                 User targetUser = pit.next();
                 dm.deleteLocalUser(targetUser.getOid());
             }
         } catch (Exception e) {
             e.printStackTrace();
         }
     }
 }
 
```

## 빠른 시작(SOAP 모드):Java API {#quick-start-soap-mode-managing-users-and-groups-using-the-java-api}을 사용하여 사용자 및 그룹 관리

다음 코드 예제에서는 로컬 사용자와 사용자가 속한 로컬 그룹을 찾습니다. ([사용자 및 그룹 관리](/help/forms/developing/users.md#managing-users-and-groups)를 참조하십시오.)

```java
 /*
     * This Java Quick Start uses the SOAP mode and contains the following JAR files
     * in the class path:
     * 1. adobe-livecycle-client.jar
     * 2. adobe-usermanager-client.jar
    * 3. activation.jar (required for SOAP mode)
    * 4. axis.jar (required for SOAP mode)
    * 5. commons-codec-1.3.jar (required for SOAP mode)
    * 6. commons-collections-3.2.jar  (required for SOAP mode)
    * 7. commons-discovery.jar (required for SOAP mode)
    * 8. commons-logging.jar (required for SOAP mode)
    * 9. dom3-xml-apis-2.5.0.jar (required for SOAP mode)
    * 10. jaxen-1.1-beta-9.jar (required for SOAP mode)
    * 11. jaxrpc.jar (required for SOAP mode)
    * 12. log4j.jar (required for SOAP mode)
    * 13. mail.jar (required for SOAP mode)
    * 14. saaj.jar (required for SOAP mode)
    * 15. wsdl4j.jar (required for SOAP mode)
    * 16. xalan.jar (required for SOAP mode)
    * 17. xbean.jar (required for SOAP mode)
    * 18. xercesImpl.jar (required for SOAP mode)
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
     * For complete details about the location of the AEM FOrms JAR files,
     * see "Including AEM Forms Java library files" in Programming
     * with AEM Forms
     */
 import java.util.*;
 
 import com.adobe.idp.um.api.infomodel.*;
 import com.adobe.livecycle.usermanager.client.DirectoryManagerServiceClient;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 
 public class ManageUsersAndGroupsTest
 {
     public static void main(String[] args) {
         try {
             //Set connection properties required to invoke AEM Forms
             Properties connectionProps = new Properties();
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://'[server]:[port]'");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
             connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
 
             //Create a ServiceClientFactory object
             ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps);
 
             // Create an DirectoryManagerServiceClient object
             DirectoryManagerServiceClient dirClient = new DirectoryManagerServiceClient(myFactory);
 
             // Find a local user
             PrincipalSearchFilter psf = new PrincipalSearchFilter();
             psf.setUserId("wblue");
             List principalList = dirClient.findPrincipals(psf);
             Iterator pit = principalList.iterator();
             String oid = "";
             User testUser = null;
             if (pit.hasNext())
             {
                 // Obtain the principal’s object identifier
                 testUser = (User)(pit.next());
             }
 
             // Find the local group
             Set groupMemberships = testUser.getGroupMemberships();
             Iterator git = groupMemberships.iterator();
             Group localGroup = null;
             if (git.hasNext())
             {
                 // Obtain the group to which the user belongs
                 localGroup = (Group)(git.next());
             }
 
             // Determine the domain and the group to which the local user belongs
             String verifyCanonicalName = testUser.getCanonicalName();
             Domain verifyDomain = dirClient.findDomain(testUser.getDomainName());
             String verifyDomainName = verifyDomain.getDomainName();
             Group verifyGroup = dirClient.getDomainAsGroup(verifyDomainName);
             String verifyGroupName = verifyGroup.getCanonicalName();
 
             // Print the uniquely identifying information about the user
             System.out.println("User name: " + verifyCanonicalName);
             System.out.println("Group name: " + verifyGroupName);
             System.out.println("Domain names should match: " + verifyDomainName + ", "+ testUser.getDomainName());
 
         }
         catch (Exception e)
         {
             System.out.println("Error occurred: " + e.getMessage());
         }
     }
 }
 
 
 
```

## 빠른 시작(SOAP 모드):Java API {#quick-start-soap-mode-managing-roles-and-permissions-using-the-java-api}을(를) 사용하여 역할 및 권한 관리

다음 코드 예제에서는 Services 사용자 역할을 주체에 할당하고 주체가 보유한 역할을 인쇄한 다음 주체로부터 역할을 제거합니다. 이 빠른 시작을 위해 두 개의 서비스가 호출됩니다.DirectoryManager 서비스 및 AuthorizationManager 서비스.([역할 및 권한 관리](/help/forms/developing/users.md#managing-roles-and-permissions) 참조)

```java
 /*
     * This Java Quick Start uses the SOAP mode and contains the following JAR files
     * in the class path:
     * 1. adobe-livecycle-client.jar
     * 2. adobe-usermanager-client.jar
    * 3. activation.jar (required for SOAP mode)
    * 4. axis.jar (required for SOAP mode)
    * 5. commons-codec-1.3.jar (required for SOAP mode)
    * 6. commons-collections-3.2.jar  (required for SOAP mode)
    * 7. commons-discovery.jar (required for SOAP mode)
    * 8. commons-logging.jar (required for SOAP mode)
    * 9. dom3-xml-apis-2.5.0.jar (required for SOAP mode)
    * 10. jaxen-1.1-beta-9.jar (required for SOAP mode)
    * 11. jaxrpc.jar (required for SOAP mode)
    * 12. log4j.jar (required for SOAP mode)
    * 13. mail.jar (required for SOAP mode)
    * 14. saaj.jar (required for SOAP mode)
    * 15. wsdl4j.jar (required for SOAP mode)
    * 16. xalan.jar (required for SOAP mode)
    * 17. xbean.jar (required for SOAP mode)
    * 18. xercesImpl.jar (required for SOAP mode)
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
 
 import com.adobe.idp.um.api.infomodel.*;
 import com.adobe.livecycle.usermanager.client.AuthorizationManagerServiceClient;
 import com.adobe.livecycle.usermanager.client.DirectoryManagerServiceClient;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 
 public class ManageRolesAndPermissionsTest
 {
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
 
             // Create an AuthorizationManagerServiceClient object
             AuthorizationManagerServiceClient amClient = new AuthorizationManagerServiceClient(myFactory);
 
             // Retrieve a principal
             DirectoryManagerServiceClient dirClient = new DirectoryManagerServiceClient(myFactory);
             PrincipalSearchFilter psf = new PrincipalSearchFilter();
             psf.setUserId("wblue");
             List principalList = dirClient.findPrincipals(psf);
             Iterator pit = principalList.iterator();
             String oid = "";
             if (pit.hasNext())
             {
                 // Obtain the principal’s object identifier
                 oid = ((User)pit.next()).getOid();
                 String[] principalOids = new String[1];
                 principalOids[0] = oid;
 
                 //Obtain the roles to be assigned
                 RoleSearchFilter rsf = new RoleSearchFilter();
                 rsf.setRoleName("Services User");
                 List roleList = amClient.findRoles(rsf);
                 Iterator rit = roleList.iterator();
                 String roleId1 = "";
                 if (rit.hasNext())
                 {
                     // Obtain the role identifier
                     roleId1 = ((Role)rit.next()).getId();
 
                     // Assign the role to the principal
                     amClient.assignRole(roleId1, principalOids);
                 }
                 else
                 {
                     System.out.println("Role not found");
                 }
 
                 // Determine which roles the principal has
                 Set roleSet = amClient.findRolesForPrincipal(oid);
 
                 // Print the roles the principal has
                 Iterator it = roleSet.iterator();
                 Role r = null;
                 System.out.println("Roles:");
                 while (it.hasNext())
                 {
                     r = ((Role)it.next());
                     System.out.println(r.getName());
                 }
 
                 // Remove a role from the principal
                 //amClient.unassignRole(roleId1, principalOids);
             }
             else
             {
                 System.out.println("Principal not found");
             }
 
         }catch (Exception e) {
             e.printStackTrace();
         }
     }
 }
 
 
 
```

## 빠른 시작(SOAP 모드):Java API {#quick-start-soap-mode-programmatically-synchronizing-users-using-the-java-api}을 사용하여 프로그래밍 방식으로 사용자를 동기화합니다.

다음 Java 코드 예제에서는 사용자 관리 API를 사용하여 사용자를 동기화합니다. ([프로그래밍 방식으로 사용자 동기화](/help/forms/developing/users.md#programmatically-synchronizing-users)를 참조하십시오.)

```java
 /*
     * This Java Quick Start uses the SOAP mode and contains the following JAR files
     * in the class path:
     * 1. adobe-livecycle-client.jar
     * 2. adobe-usermanager-client.jar
    * 3. activation.jar (required for SOAP mode)
    * 4. axis.jar (required for SOAP mode)
    * 5. commons-codec-1.3.jar (required for SOAP mode)
    * 6. commons-collections-3.2.jar  (required for SOAP mode)
    * 7. commons-discovery.jar (required for SOAP mode)
    * 8. commons-logging.jar (required for SOAP mode)
    * 9. dom3-xml-apis-2.5.0.jar (required for SOAP mode)
    * 10. jaxen-1.1-beta-9.jar (required for SOAP mode)
    * 11. jaxrpc.jar (required for SOAP mode)
    * 12. log4j.jar (required for SOAP mode)
    * 13. mail.jar (required for SOAP mode)
    * 14. saaj.jar (required for SOAP mode)
    * 15. wsdl4j.jar (required for SOAP mode)
    * 16. xalan.jar (required for SOAP mode)
    * 17. xbean.jar (required for SOAP mode)
    * 18. xercesImpl.jar (required for SOAP mode)
     * 19. adobe-usermanager-util-client.jar
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
 import com.adobe.livecycle.usermanager.client.DirectoryManagerServiceClient;
 import com.adobe.idp.um.api.DirectoryManager;
 import com.adobe.idp.um.api.infomodel.DirectorySyncInfo;
 import com.adobe.idp.um.dsc.util.client.UserManagerUtilServiceClient;
 
 public class SynchDomain {
 
     public static void main(String[] args) {
         try {
 
             //Set connection properties required to invoke AEM Forms
                Properties connectionProps = new Properties();
                connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://'[server]:[port]'");
      connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
                connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
                connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
                connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
 
             //Create a UserManagerUtilServiceClient object
             ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps);
             UserManagerUtilServiceClient umutil = new  UserManagerUtilServiceClient(myFactory);
 
             //Specify the set of enterprise domains to synchronize
             Set<String> domainNames = new HashSet<String>();
             domainNames.add("adobe3");
 
             //Perform the synchronization operation on the set of enterprise domains specified above
             umutil.scheduleSynchronization(domainNames);
 
             //In case the synchronization needs to be performed on all the registered enterprise domains use this method umutil.scheduleSynchronization();
 
             DirectoryManager dm = new DirectoryManagerServiceClient(myFactory);
             Map<String, DirectorySyncInfo> synchStatus = dm.getDirectorySyncStatus(domainNames);
 
             String domainName = "adobe3";
             DirectorySyncInfo di = synchStatus.get(domainName);
             if(di.getSyncStatus() == DirectorySyncInfo.SYNCSTATUS_COMPLETED){
                          System.out.println("Directory synch for domain     "+domainName+" is complete");
 
             }
 
         }catch (Exception e) {
             e.printStackTrace();
         }
     }
 
 }
 
 
 
```

## 빠른 시작(SOAP 모드):Java API {#quick_start_soap_mode_adding_users_using_the_java_api-1}을(를) 사용하여 사용자 추가

다음 코드 예제에서는 Wendy Blue라는 사용자를 AEM Forms에 추가합니다. ([사용자 추가](/help/forms/developing/users.md#adding-users)를 참조하십시오.)

```java
 /*
     * This Java Quick Start uses the SOAP mode and contains the following JAR files
     * in the class path:
     * 1. adobe-livecycle-client.jar
     * 2. adobe-usermanager-client.jar
    * 3. activation.jar (required for SOAP mode)
    * 4. axis.jar (required for SOAP mode)
    * 5. commons-codec-1.3.jar (required for SOAP mode)
    * 6. commons-collections-3.2.jar  (required for SOAP mode)
    * 7. commons-discovery.jar (required for SOAP mode)
    * 8. commons-logging.jar (required for SOAP mode)
    * 9. dom3-xml-apis-2.5.0.jar (required for SOAP mode)
    * 10. jaxen-1.1-beta-9.jar (required for SOAP mode)
    * 11. jaxrpc.jar (required for SOAP mode)
    * 12. log4j.jar (required for SOAP mode)
    * 13. mail.jar (required for SOAP mode)
    * 14. saaj.jar (required for SOAP mode)
    * 15. wsdl4j.jar (required for SOAP mode)
    * 16. xalan.jar (required for SOAP mode)
    * 17. xbean.jar (required for SOAP mode)
    * 18. xercesImpl.jar (required for SOAP mode)
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
 import com.adobe.livecycle.usermanager.client.DirectoryManagerServiceClient;
 import com.adobe.idp.um.api.infomodel.impl.*;
 import com.adobe.idp.um.api.infomodel.*;
 
 public class AddUser {
 
     public static void main(String[] args) {
         try {
             //Set connection properties required to invoke AEM Forms
                Properties connectionProps = new Properties();
                connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://'[server]:[port]'");
      connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
                connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
                connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
                connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
 
             //Create a ServiceClientFactory object
             ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps);
 
             //Create an DirectoryManagerServiceClient object
             DirectoryManagerServiceClient dmClient = new DirectoryManagerServiceClient(myFactory);
 
             //Create a User object and populate its attributes
             UserImpl u = new UserImpl();
             u.setDomainName("DefaultDom");
             u.setUserid("wblue");
             u.setCanonicalName("wblue");
             u.setPrincipalType("USER");
             u.setGivenName("Wendy");
             u.setFamilyName("Blue");
             u.setLocale(Locale.CANADA);
             u.setTimezone(TimeZone.getDefault());
             u.setDisabled(false);
 
             //Add the User to the system using the DirectoryManagerServiceClient
             dmClient.createLocalUser(u,"password");
 
             //Ensure that the user was added
             //Create a PrincipalSearchFilter to find the user by ID
             PrincipalSearchFilter psf = new PrincipalSearchFilter();
             psf.setUserId("wblue");
             List<User> principalList = dmClient.findPrincipals(psf);
             Iterator<User> pit = principalList.iterator();
             if(pit.hasNext()){
                 User theUser = pit.next();
                 System.out.println("User ID: " + theUser.getUserid());
                 System.out.println("User name: " + theUser.getGivenName() +" "+ theUser.getFamilyName());
                 System.out.println("User Domain: " + theUser.getDomainName());
                 System.out.println("is user disabled?: " + theUser.isDisabled());
             }
 
         }catch (Exception e) {
             e.printStackTrace();
         }
 ;
     }
 
 }
 
 
```

## 빠른 시작(SOAP 모드):Java API {#quick-start-soap-mode-creating-groups-using-the-java-api}을 사용하여 그룹 만들기

다음 코드 예제에서는 AEM Forms에 AdobeGroup이라는 그룹을 만듭니다. ([그룹 만들기](/help/forms/developing/users.md#creating-groups)를 참조하십시오.)

```java
 /*
     * This Java Quick Start uses the SOAP mode and contains the following JAR files
     * in the class path:
     * 1. adobe-livecycle-client.jar
     * 2. adobe-usermanager-client.jar
    * 3. activation.jar (required for SOAP mode)
    * 4. axis.jar (required for SOAP mode)
    * 5. commons-codec-1.3.jar (required for SOAP mode)
    * 6. commons-collections-3.2.jar  (required for SOAP mode)
    * 7. commons-discovery.jar (required for SOAP mode)
    * 8. commons-logging.jar (required for SOAP mode)
    * 9. dom3-xml-apis-2.5.0.jar (required for SOAP mode)
    * 10. jaxen-1.1-beta-9.jar (required for SOAP mode)
    * 11. jaxrpc.jar (required for SOAP mode)
    * 12. log4j.jar (required for SOAP mode)
    * 13. mail.jar (required for SOAP mode)
    * 14. saaj.jar (required for SOAP mode)
    * 15. wsdl4j.jar (required for SOAP mode)
    * 16. xalan.jar (required for SOAP mode)
    * 17. xbean.jar (required for SOAP mode)
    * 18. xercesImpl.jar (required for SOAP mode)
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
 import java.util.List;
 import java.util.Properties;
 
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
 import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
 import com.adobe.idp.um.api.infomodel.Group;
 import com.adobe.idp.um.api.infomodel.Principal;
 import com.adobe.idp.um.api.infomodel.PrincipalSearchFilter;
 import com.adobe.idp.um.api.infomodel.PrincipalReference;
 import com.adobe.idp.um.api.infomodel.impl.GroupImpl;
 import com.adobe.livecycle.usermanager.client.DirectoryManagerServiceClient;
 
 public class AddGroup {
 
     public static void main(String[] args) {
          try {
 
          //Set connection properties that are required to invoke AEM Forms
          Properties connectionProps = new Properties();
                 connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://'[server]:[port]'");
      connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
                 connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
                 connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
                 connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");
 
                  //Create a ServiceClientFactory object
                  ServiceClientFactory myFactory = ServiceClientFactory.createInstance(connectionProps);
 
                  //Create an DirectoryManagerServiceClient object
                  DirectoryManagerServiceClient dmClient = new DirectoryManagerServiceClient(myFactory);
 
                  //Specify the group and domain name
                  String groupName = "AdobeGroup";
                  String domainName = "TestDomain";
 
                  //Check whether the group exists
                  String groupOid = checkGroupExist(groupName, domainName,dmClient);
 
                  //The group exists
                  if(groupOid != null){
                      System.out.println("The group exists");
                      return;
                  }
 
                  //The group does not exist
                  String groupCanonicalName = groupName;
 
                  GroupImpl group = new GroupImpl();
                  group.setCanonicalName(groupCanonicalName);
                  group.setDomainName(domainName);
                  group.setGroupType(Group.GROUPTYPE_PRINCIPALS);
                  group.setLocal(true);
                  group.setPrincipalType(Principal.PRINCIPALTYPE_GROUP);
 
                  groupOid = dmClient.createLocalGroup(group);
                  System.out.println("Sample group created with name "+groupName);
 
          }catch (Exception e) {
                 e.printStackTrace();
             }
 
         }
 
     /**
         * Search for a group located in the specified domain
         */
        private static String checkGroupExist(String groupName, String domainName, DirectoryManagerServiceClient directoryManager){
          try {
          PrincipalSearchFilter psf = new PrincipalSearchFilter();
            psf.setCommonName(groupName);
            psf.setSpecificDomainName(domainName);
 
            //By default the filter causes like search unless you are using the absolute version
            //Setting this ensures that search is exact
            psf.setMatchExactCriteria(true);
 
            //By default search returns obsolete groups also. Set this to ensure that
            //only active groups are returned
            psf.setRetrieveOnlyActive();
 
            //PrincipalReference are lightweight group objects and searching for them is better performance.
            //If you do not require any other group attribute then use this
            //mode of search
            List<PrincipalReference> result = directoryManager.findPrincipalReferences(psf);
            if(result.isEmpty()){
          System.out.println("Sample group with name "+groupName +" does not exist");
                return null;
            }else{
                String oid = result.get(0).getOid();
                System.out.println("Sample group with name "+groupName +" already exists");
                return oid;
            }
          }catch (Exception e) {
                e.printStackTrace();
            }
          return "";
        }
 }
```

## 빠른 시작(SOAP 모드) 환경 설정 노드 관리 {#quick-start-soap-mode-managing-preferences-nodes}

사용자 관리 API를 사용하여 환경 설정 노드를 관리하는 다음 Java 코드 모델입니다. ( [환경 설정 노드 프로그래밍 방식으로 관리](/help/forms/developing/programmatically-preferences-nodes.md#programmatically-managing-the-preferences-nodes) 참조)

```java
/*
 * This Java Quick Start uses the SOAP mode and contains the following JAR files
 * in the class path:
 * 1. adobe-livecycle-client.jar
 * 2. adobe-usermanager-client.jar
    * 3. activation.jar (required for SOAP mode)
    * 4. axis.jar (required for SOAP mode)
    * 5. commons-codec-1.3.jar (required for SOAP mode)
    * 6. commons-collections-3.2.jar  (required for SOAP mode)
    * 7. commons-discovery.jar (required for SOAP mode)
    * 8. commons-logging.jar (required for SOAP mode)
    * 9. dom3-xml-apis-2.5.0.jar (required for SOAP mode)
    * 10. jaxen-1.1-beta-9.jar (required for SOAP mode)
    * 11. jaxrpc.jar (required for SOAP mode)
    * 12. log4j.jar (required for SOAP mode)
    * 13. mail.jar (required for SOAP mode)
    * 14. saaj.jar (required for SOAP mode)
    * 15. wsdl4j.jar (required for SOAP mode)
    * 16. xalan.jar (required for SOAP mode)
    * 17. xbean.jar (required for SOAP mode)
    * 18. xercesImpl.jar (required for SOAP mode)
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
import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
import com.adobe.idp.um.api.UMException;
import com.adobe.livecycle.usermanager.client.PreferenceManagerServiceClient;

public class ManagePreferences {

    public static void main(String[] args) {
    //Set connection properties required to invoke AEM Forms
        Properties connectionProps = new Properties();
    connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://'[server]:[port]'");
    connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
    connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
    connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
    connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");

    //Create a PreferenceManagerServiceClient object
    ServiceClientFactory factory = ServiceClientFactory.createInstance(connectionProps);
    PreferenceManagerServiceClient pmutil = new  PreferenceManagerServiceClient(factory);

    //get the preference map for a particular node
    String path = "/Adobe/LiveCycle/Config/UM/CommonNameOrder";
    Map<String, String> map;
    try {
        map = pmutil.getPreferences(path);
        for(String str:map.keySet()) {
            //assert on the key as "ReverseOrder"
            //assert on the value[map.get(str)] as "false”
        }
    } catch (UMException e) {
        e.printStackTrace();
    }

    // set preferences by editing a particular key/value pair of a Node.
    String path = "/Adobe/LiveCycle/Config/UM/CommonNameOrder";
    Map<String, String> map = new HashMap<String, String>();
    map.put("ReverseOrder", "true");
    try {
        pmutil.setPreferences(path, map);
        Map<String, String> map1 = pmutil.getPreferences(path);
        for(String str:map1.keySet()) {
            //assert on the key as "ReverseOrder"
            //assert on the value[map.get(str)] as "true"
        }
    } catch (UMException e) {
        e.printStackTrace();
    }
    }
}
```

## 빠른 시작(SOAP 모드):Java API {#quick-start-soap-mode-programmatically-managing-the-preferences-nodes-using-the-java-api}을 사용하여 프로그래밍 방식으로 환경 설정 노드 관리

사용자 관리 API를 사용하여 환경 설정 노드를 관리하는 다음 Java 코드 모델([환경 설정 노드 프로그래밍 방식 관리](/help/forms/developing/programmatically-preferences-nodes.md#programmatically-managing-the-preferences-nodes) 참조)

```java
/*
 * This Java Quick Start uses the SOAP mode and contains the following JAR files
 * in the class path:
 * 1. adobe-livecycle-client.jar
 * 2. adobe-usermanager-client.jar
 *
 * These JAR files are located in the following path:
 * <install directory>/Adobe/Adobe_Experience_Manager_forms/sdk/client-libs/common
 *
 * <install directory>/Adobe/Adobe_Experience_Manager_forms/sdk/client-libs/jboss
 *
 * <install directory>/Adobe/Adobe_Experience_Manager_forms/jboss/bin/client
 *
 * If you want to invoke a remote AEM Forms instance and there is a
 * firewall between the client application and AEM FOrms, then it is
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
 * see "Including AEM FOrms library files" in Programming
 * with AEM FOrms
 */

import java.util.*;
import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;
import com.adobe.idp.dsc.clientsdk.ServiceClientFactoryProperties;
import com.adobe.idp.um.api.UMException;
import com.adobe.livecycle.usermanager.client.PreferenceManagerServiceClient;

public class ManagePreferences {

    public static void main(String[] args) {
    //Set connection properties required to invoke AEM Forms
        Properties connectionProps = new Properties();
    connectionProps.setProperty(ServiceClientFactoryProperties.DSC_DEFAULT_SOAP_ENDPOINT, "https://'[server]:[port]'");
    connectionProps.setProperty(ServiceClientFactoryProperties.DSC_TRANSPORT_PROTOCOL,ServiceClientFactoryProperties.DSC_SOAP_PROTOCOL);
    connectionProps.setProperty(ServiceClientFactoryProperties.DSC_SERVER_TYPE, "JBoss");
    connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_USERNAME, "administrator");
    connectionProps.setProperty(ServiceClientFactoryProperties.DSC_CREDENTIAL_PASSWORD, "password");

    //Create a PreferenceManagerServiceClient object
    ServiceClientFactory factory = ServiceClientFactory.createInstance(connectionProps);
    PreferenceManagerServiceClient pmutil = new  PreferenceManagerServiceClient(factory);

    //get the preference map for a particular node
    String path = "/Adobe/LiveCycle/Config/UM/CommonNameOrder";
    Map<String, String> map;
    try {
        map = pmutil.getPreferences(path);
        for(String str:map.keySet()) {
            //assert on the key as "ReverseOrder"
            //assert on the value[map.get(str)] as "false"
        }
    } catch (UMException e) {
        e.printStackTrace();
    }

    // set preferences by editing a particular key/value pair of a Node.
    String path = "/Adobe/LiveCycle/Config/UM/CommonNameOrder";
    Map<String, String> map = new HashMap<String, String>();
    map.put("ReverseOrder", "true");
    try {
        pmutil.setPreferences(path, map);
        Map<String, String> map1 = pmutil.getPreferences(path);
        for(String str:map1.keySet()) {
            //assert on the key as "ReverseOrder"
            //assert on the value[map.get(str)] as "true"
        }
    } catch (UMException e) {
        e.printStackTrace();
    }
}
}
```

