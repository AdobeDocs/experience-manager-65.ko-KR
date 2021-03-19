---
title: Adobe LiveCycle과 AEM Forms 연결
seo-title: Adobe LiveCycle과 AEM Forms 연결
description: AEM LiveCycle 커넥터를 사용하면 AEM 앱 및 워크플로우 내에서 LiveCycle ES4 다큐멘트 서비스를 시작할 수 있습니다.
seo-description: AEM LiveCycle 커넥터를 사용하면 AEM 앱 및 워크플로우 내에서 LiveCycle ES4 다큐멘트 서비스를 시작할 수 있습니다.
uuid: 7dc9d5ec-7b19-4d93-936d-81ceb45dfffa
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Configuration
discoiquuid: 7e404b45-1302-4dd1-b3c9-3f47fedb5f94
role: 관리자
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '1030'
ht-degree: 0%

---


# Adobe LiveCycle {#connecting-aem-forms-with-adobe-livecycle}과(와) AEM Forms 연결

AEM(Adobe Experience Manager) LiveCycle 커넥터를 사용하면 AEM 웹 앱 및 워크플로우에서 Adobe LiveCycle ES4 다큐멘트 서비스를 원활하게 호출할 수 있습니다. LiveCycle은 클라이언트 응용 프로그램이 Java API를 사용하여 LiveCycle 서비스를 시작할 수 있도록 하는 리치 클라이언트 SDK를 제공합니다. AEM LiveCycle 커넥터는 OSGi 환경 내에서 이러한 API를 사용하는 과정을 간소화합니다.

## Adobe LiveCycle {#connecting-aem-server-to-adobe-livecycle}에 AEM 서버 연결

AEM LiveCycle 커넥터는 [AEM Forms 추가 기능 패키지](/help/forms/using/installing-configuring-aem-forms-osgi.md)의 일부입니다. AEM Forms 추가 기능 패키지를 설치한 후 다음 단계를 수행하여 AEM 웹 콘솔에 LiveCycle 서버의 세부 정보를 추가합니다.

1. AEM 웹 콘솔 구성 관리자에서 Adobe LiveCycle 클라이언트 SDK 구성 구성 요소를 찾습니다.
1. 구성 요소를 클릭하여 구성 서버 URL, 사용자 이름 및 암호를 편집합니다.
1. 설정을 검토하고 **저장**&#x200B;을 클릭합니다.

속성이 자체 설명이지만 중요한 속성은 다음과 같습니다.

* **서버 URL**  - LiveCycle 서버의 URL을 지정합니다. LiveCycle 및 AEM에서 https를 통해 통신하도록 하려면 다음 JVM으로 AEM을 시작하십시오.

   ```java
   argument
    -Djavax.net.ssl.trustStore=<<em>path to LC keystore</em>>
   ```

   옵션을 선택합니다.

* **사용자 이름** - AEM과 LiveCycle 간의 통신을 설정하는 데 사용되는 계정의 사용자 이름을 지정합니다. 계정은 Document Services를 시작할 수 있는 권한이 있는 LiveCycle 사용자 계정입니다.
* **암호** - 암호를 지정합니다.
* **서비스 이름**  - 사용자 이름 및 암호 필드에 제공된 사용자 자격 증명을 사용하여 시작하는 서비스를 지정합니다. 기본적으로 LiveCycle 서비스를 시작하는 동안 자격 증명이 전달되지 않습니다.

## 문서 서비스 {#starting-document-services} 시작

클라이언트 응용 프로그램은 Java API, 웹 서비스, Remoting 및 REST를 사용하여 프로그래밍 방식으로 LiveCycle 서비스를 시작할 수 있습니다. Java 클라이언트의 경우, 애플리케이션은 LiveCycle SDK를 사용할 수 있습니다. LiveCycle SDK는 이러한 서비스를 원격으로 시작할 수 있는 Java API를 제공합니다. 예를 들어 Microsoft Word 문서를 PDF로 변환하기 위해 클라이언트는 GeneratePDF서비스를 시작합니다. 호출 흐름은 다음 단계로 구성됩니다.

1. ServiceClientFactory 인스턴스를 만듭니다.
1. 각 서비스는 클라이언트 클래스를 제공합니다. 서비스를 시작하려면 서비스의 클라이언트 인스턴스를 만듭니다.
1. 서비스를 시작하고 결과를 처리합니다.

AEM LiveCycle 커넥터는 표준 OSGi 수단을 사용하여 액세스할 수 있는 OSGi 서비스로 이러한 클라이언트 인스턴스를 노출하여 흐름을 단순화합니다. LiveCycle 커넥터는 다음과 같은 기능을 제공합니다.

* OSGi 서비스로 된 클라이언트 인스턴스:OSGI 번들로 패키지된 클라이언트는 [문서 서비스 목록](/help/forms/using/aem-livecycle-connector.md#p-document-services-list-p) 섹션에 나열됩니다. 각 클라이언트 jar는 클라이언트 인스턴스를 OSGi 서비스 레지스트리에 OSGi 서비스로 등록합니다.
* 사용자 자격 증명 전파:LiveCycle 서버에 연결하는 데 필요한 연결 세부 사항은 중앙 위치에서 관리됩니다.
* ServiceClientFactory 서비스:프로세스를 시작하기 위해 클라이언트 응용 프로그램은 ServiceClientFactory 인스턴스에 액세스할 수 있습니다.

### OSGi 서비스 레지스트리 {#starting-via-service-references-from-osgi-service-registry}의 서비스 참조를 통해 시작

AEM 내에서 노출된 서비스를 시작하려면 다음 단계를 수행하십시오.

1. 추가적인 종속성을 결정합니다. maven pom.xml 파일에서 필요한 클라이언트 jar에 종속성을 추가합니다. 최소한 adobe-livecycle-client 및 adobe-usermanager-client jar에 종속성을 추가합니다.

   ```xml
   <dependency>
     <groupId>com.adobe.livecycle</groupId>
     <artifactId>adobe-livecycle-client</artifactId>
     <version>11.0.0</version>
   </dependency>
   <dependency>
     <groupId>com.adobe.livecycle</groupId>
     <artifactId>adobe-usermanager-client</artifactId>
     <version>11.0.0</version>
   </dependency>
   <dependency>
     <groupId>com.adobe.livecycle</groupId>
     <artifactId>adobe-cq-integration-api</artifactId>
     <version>11.0.0</version>
   </dependency>
   ```

   서비스를 시작하려면 서비스에 대한 해당 Maven 종속성을 추가하십시오. 종속성 목록은 [문서 서비스 목록](/help/forms/using/aem-livecycle-connector.md#p-document-services-list-p)을 참조하십시오. 예를 들어 PDF 생성 서비스의 경우 다음 종속성을 추가합니다.

   ```xml
   <dependency>
     <groupId>com.adobe.livecycle</groupId>
     <artifactId>adobe-generatepdf-client</artifactId>
     <version>11.0.0</version>
   </dependency>
   ```

1. 서비스 참조를 얻습니다. 서비스 인스턴스에 대한 핸들을 가져옵니다. Java 클래스를 작성하는 경우 선언적 서비스 주석을 사용할 수 있습니다.

   ```java
   import com.adobe.livecycle.generatepdf.client.GeneratePdfServiceClient;
   import com.adobe.livecycle.generatepdf.client.CreatePDFResult;
   import com.adobe.idp.Document;
   
   @Reference
   GeneratePdfServiceClient generatePDF;
   ...
   
   Resource r = resourceResolver.getResource("/path/tp/docx");
   Document sourceDoc = new Document(r.adaptTo(InputStream.class));
   CreatePDFResult result = generatePDF.createPDF2(
                       sourceDoc,
                       extension, //inputFileExtension
                       null, //fileTypeSettings
                       null, //pdfSettings
                       null, //securitySettings
                       settingsDoc, //settingsDoc
                       null //xmpDoc
               );
   ```

   위의 코드 조각은 문서를 PDF로 변환하기 위해 GeneratePdfServiceClient의 createPDF API를 시작합니다. 다음 코드를 사용하여 JSP에서 비슷한 호출을 수행할 수 있습니다. 주요 차이점은 다음 코드는 Sling ScriptHelper를 사용하여 GeneratePdfServiceClient에 액세스한다는 것입니다.

   ```jsp
   <%@ page import="com.adobe.livecycle.generatepdf.client.GeneratePdfServiceClient" %>
   <%@ page import="com.adobe.livecycle.generatepdf.client.CreatePDFResult" %>
   <%@ page import="com.adobe.idp.Document" %>
   
   GeneratePdfServiceClient generatePDF = sling.getService(GeneratePdfServiceClient.class);
   Document sourceDoc = ...
   CreatePDFResult result = generatePDF.createPDF2(
                       sourceDoc,
                       extension, //inputFileExtension
                       null, //fileTypeSettings
                       null, //pdfSettings
                       null, //securitySettings
                       settingsDoc, //settingsDoc
                       null //xmpDoc
               );
   ```

### ServiceClientFactory를 통해 시작 {#starting-via-serviceclientfactory}

경우에 따라 ServiceClientFactory 클래스가 필요합니다. 예를 들어 프로세스를 호출하려면 ServiceClientFactory가 필요합니다.

```java
import com.adobe.livecycle.dsc.clientsdk.ServiceClientFactoryProvider;
import com.adobe.idp.dsc.clientsdk.ServiceClientFactory;

@Reference
ServiceClientFactoryProvider scfProvider;

...
ServiceClientFactory scf = scfProvider.getDefaultServiceClientFactory();
...
```

## RunAs 지원 {#runas-support}

LiveCycle의 거의 모든 문서 서비스에는 인증이 필요합니다. 다음 옵션을 사용하여 코드에 명시적 자격 증명을 제공하지 않고 이러한 서비스를 시작할 수 있습니다.

### 허용 목록에 추가하다 구성 {#allowlist-configuration}

LiveCycle 클라이언트 SDK 구성에는 서비스 이름에 대한 설정이 포함됩니다. 이 구성은 호출 논리가 즉시 관리자 자격 증명을 사용하는 서비스 목록입니다. 예를 들어 DirectoryManager 서비스(사용자 관리 API의 일부)를 이 목록에 추가하는 경우 클라이언트 코드는 서비스를 직접 사용할 수 있으며 호출 레이어가 LiveCycle 서버로 전송된 요청의 일부로 구성된 자격 증명을 자동으로 전달합니다

### RunAsManager {#runasmanager}

통합의 일부로 새 서비스 RunAsManager가 제공됩니다. LiveCycle 서버를 호출할 때 사용할 자격 증명을 프로그래밍 방식으로 제어할 수 있습니다.

```java
import com.adobe.livecycle.dsc.clientsdk.security.PasswordCredential;
import com.adobe.livecycle.dsc.clientsdk.security.PrivilegedAction;
import com.adobe.livecycle.dsc.clientsdk.security.RunAsManager;
import com.adobe.idp.dsc.registry.component.ComponentRegistry;

@Reference
private RunAsManager runAsManager;

List<Component> components = runAsManager.doPrivileged(new PrivilegedAction<List<Component>>() {
            public List<Component> run() {
                return componentRegistry.getComponents();
            }
        });
assertNotNull(components);
```

다른 자격 증명을 전달하려면 PasswordCredential 인스턴스를 가져오는 오버로드된 메서드를 사용할 수 있습니다.

```java
PasswordCredential credential = new PasswordCredential("administrator","password");
List<Component> components = runAsManager.doPrivileged(new PrivilegedAction<List<Component>>() {
    public List<Component> run() {
        return componentRegistry.getComponents();
    }
},credential);
```

### InvocationRequest 속성 {#invocationrequest-property}

프로세스를 호출하거나 ServiceClientFactory 클래스를 직접 사용하고 InvocationRequest를 만드는 경우 호출 레이어에서 구성된 자격 증명을 사용하도록 지정할 수 있습니다.

```java
import com.adobe.idp.dsc.InvocationResponse
import com.adobe.idp.dsc.InvocationRequest
import com.adobe.livecycle.dsc.clientsdk.ServiceClientFactoryProvider
import com.adobe.idp.dsc.clientsdk.ServiceClientFactory
import com.adobe.livecycle.dsc.clientsdk.InvocationProperties

ServiceClientFactoryProvider scfp = sling.getService(ServiceClientFactoryProvider.class)
ServiceClientFactory serviceClientFactory = scfp.getDefaultServiceClientFactory()
InvocationRequest ir = serviceClientFactory.createInvocationRequest("sample/LetterSubmissionProcess", "invoke", new HashMap(), true);

//Here we are invoking the request with system user
ir.setProperty(InvocationProperties.INVOKER_TYPE,InvocationProperties.INVOKER_TYPE_SYSTEM)

InvocationResponse response = serviceClientFactory.getServiceClient().invoke(ir);
```

## 문서 서비스 목록 {#document-services-list}

### Adobe LiveCycle 클라이언트 SDK API 번들 {#adobe-livecycle-client-sdk-api-bundle}

다음 서비스를 사용할 수 있습니다.

* com.adobe.idp.um.api.AuthenticationManager
* com.adobe.idp.um.api.DirectoryManager
* com.adobe.idp.um.api.AuthorizationManager
* com.adobe.idp.dsc.registry.service.ServiceRegistry
* com.adobe.idp.dsc.registry.component.ComponentRegistry

#### 마비된종속성 {#maven-dependencies}

```xml
<dependency>
  <groupId>com.adobe.livecycle</groupId>
  <artifactId>adobe-livecycle-client</artifactId>
  <version>11.0.0</version>
</dependency>
<dependency>
  <groupId>com.adobe.livecycle</groupId>
  <artifactId>adobe-usermanager-client</artifactId>
  <version>11.0.0</version>
</dependency>
```

### Adobe LiveCycle 클라이언트 SDK 번들 {#adobe-livecycle-client-sdk-bundle}

다음 서비스를 사용할 수 있습니다.

* com.adobe.livecycle.dsc.clientsdk.security.RunAsManager
* com.adobe.livecycle.dsc.clientsdk.ServiceClientFactoryProvider

#### 마비된종속성 {#maven-dependencies-1}

```xml
<dependency>
  <groupId>com.adobe.livecycle</groupId>
  <artifactId>adobe-livecycle-cq-integration-api</artifactId>
  <version>1.1.10</version>
</dependency>
```

### Adobe LiveCycle TaskManager 클라이언트 번들 {#adobe-livecycle-taskmanager-client-bundle}

다음 서비스를 사용할 수 있습니다.

* com.adobe.idp.taskmanager.dsc.client.task.TaskManager
* com.adobe.idp.taskmanager.dsc.client.TaskManagerQueryService
* com.adobe.idp.taskmanager.dsc.client.queuemanager.QueueManager
* com.adobe.idp.taskmanager.dsc.client.emailsettings.EmailSettingService
* com.adobe.idp.taskmanager.dsc.client.endpoint.TaskManagerEndpointClient
* com.adobe.idp.taskmanager.dsc.client.userlist.UserlistService

#### 마비된종속성 {#maven-dependencies-2}

```xml
<dependency>
  <groupId>com.adobe.livecycle</groupId>
  <artifactId>adobe-taskmanager-client</artifactId>
  <version>11.0.0</version>
</dependency>
```

### Adobe LiveCycle Workflow 클라이언트 번들 {#adobe-livecycle-workflow-client-bundle}

다음 서비스를 사용할 수 있습니다.

* com.adobe.idp.workflow.client.WorkflowServiceClient

#### 마비된종속성 {#maven-dependencies-3}

```xml
<dependency>
  <groupId>com.adobe.livecycle</groupId>
  <artifactId>adobe-workflow-client-sdk</artifactId>
  <version>11.0.0</version>
</dependency>
```

### Adobe LiveCycle PDF Generator 클라이언트 번들 {#adobe-livecycle-pdf-generator-client-bundle}

다음 서비스를 사용할 수 있습니다.

* com.adobe.livecycle.generatepdf.client.GeneratePdfServiceClient

#### 마비된종속성 {#maven-dependencies-4}

```xml
<dependency>
  <groupId>com.adobe.livecycle</groupId>
  <artifactId>adobe-generatepdf-client</artifactId>
  <version>11.0.0</version>
</dependency>
```

### Adobe LiveCycle Application Manager 클라이언트 번들 {#adobe-livecycle-application-manager-client-bundle}

다음 서비스를 사용할 수 있습니다.

* com.adobe.idp.applicationmanager.service.ApplicationManager
* com.adobe.livecycle.applicationmanager.client.ApplicationManager
* com.adobe.livecycle.design.service.DesigntimeService

#### 마비된종속성 {#maven-dependencies-5}

```xml
<dependency>
  <groupId>com.adobe.livecycle</groupId>
  <artifactId>adobe-applicationmanager-client-sdk</artifactId>
  <version>11.0.0</version>
</dependency>
```

### Adobe LiveCycle 어셈블러 클라이언트 번들 {#adobe-livecycle-assembler-client-bundle}

다음 서비스를 사용할 수 있습니다.

* com.adobe.livecycle.assembler.client.AssemblerServiceClient

#### 마비된종속성 {#maven-dependencies-6}

```xml
<dependency>
  <groupId>com.adobe.livecycle</groupId>
  <artifactId>adobe-assembler-client</artifactId>
  <version>11.0.0</version>
</dependency>
```

### Adobe LiveCycle 양식 데이터 통합 클라이언트 번들 {#adobe-livecycle-form-data-integration-client-bundle}

다음 서비스를 사용할 수 있습니다.

* com.adobe.livecycle.formdataintegration.client.FormDataIntegrationClient

#### 마비된종속성 {#maven-dependencies-7}

```xml
<dependency>
  <groupId>com.adobe.livecycle</groupId>
  <artifactId>adobe-formdataintegration-client</artifactId>
  <version>11.0.0</version>
</dependency>
```

### Adobe LiveCycle Forms 클라이언트 번들 {#adobe-livecycle-forms-client-bundle}

다음 서비스를 사용할 수 있습니다.

* com.adobe.livecycle.formsservice.client.FormsServiceClient

#### 마비된종속성 {#maven-dependencies-8}

```xml
<dependency>
  <groupId>com.adobe.livecycle</groupId>
  <artifactId>adobe-forms-client</artifactId>
  <version>11.0.0</version>
</dependency>
```

### Adobe LiveCycle Output 클라이언트 번들 {#adobe-livecycle-output-client-bundle}

다음 서비스를 사용할 수 있습니다.

* com.adobe.livecycle.output.client.OutputClient

#### 마비된종속성 {#maven-dependencies-9}

```xml
<dependency>
  <groupId>com.adobe.livecycle</groupId>
  <artifactId>adobe-output-client</artifactId>
  <version>11.0.0</version>
</dependency>
```

### Adobe LiveCycle Reader Extensions 클라이언트 번들 {#adobe-livecycle-reader-extensions-client-bundle}

다음 서비스를 사용할 수 있습니다.

* com.adobe.livecycle.readerextensions.client.ReaderExtensionsServiceClient

#### 마비된종속성 {#maven-dependencies-10}

```xml
<dependency>
  <groupId>com.adobe.livecycle</groupId>
  <artifactId>adobe-reader-extensions-client</artifactId>
  <version>11.0.0</version>
</dependency>
```

### Adobe Rights Manager 클라이언트 번들 {#adobe-livecycle-rights-manager-client-bundle}

다음 서비스를 사용할 수 있습니다.

* com.adobe.livecycle.rightsmanagement.client.DocumentManager
* com.adobe.livecycle.rightsmanagement.client.EventManager
* com.adobe.livecycle.rightsmanagement.client.ExternalUserManager
* com.adobe.livecycle.rightsmanagement.client.LicenseManager
* com.adobe.livecycle.rightsmanagement.client.WatermarkManager
* com.adobe.livecycle.rightsmanagement.client.PolicyManager
* com.adobe.livecycle.rightsmanagement.client.AbstractPolicyManager

#### 마비된종속성 {#maven-dependencies-11}

```xml
<dependency>
  <groupId>com.adobe.livecycle</groupId>
  <artifactId>adobe-rightsmanagement-client</artifactId>
  <version>11.0.0</version>
</dependency>
```

### Adobe LiveCycle 서명 클라이언트 번들 {#adobe-livecycle-signatures-client-bundle}

다음 서비스를 사용할 수 있습니다.

* com.adobe.livecycle.signatures.client.SignatureServiceClientInterface

#### 마비된종속성 {#maven-dependencies-12}

```xml
<dependency>
  <groupId>com.adobe.livecycle</groupId>
  <artifactId>adobe-signatures-client</artifactId>
  <version>11.0.0</version>
</dependency>
```

### Adobe LiveCycle Truststore 클라이언트 번들 {#adobe-livecycle-truststore-client-bundle}

다음 서비스를 사용할 수 있습니다.

* com.adobe.truststore.dsc.TrustConfigurationService
* com.adobe.truststore.dsc.CRLService
* com.adobe.truststore.dsc.CredentialService
* com.adobe.truststore.dsc.CertificateService

#### 마비된종속성 {#maven-dependencies-13}

```xml
<dependency>
  <groupId>com.adobe.livecycle</groupId>
  <artifactId>adobe-truststore-client</artifactId>
  <version>11.0.0</version>
</dependency>
```

### Adobe 리포지토리 클라이언트 번들 {#adobe-livecycle-repository-client-bundle}

다음 서비스를 사용할 수 있습니다.

* com.adobe.repository.bindings.ResourceRepository
* com.adobe.repository.bindings.ResourceSynchronizer

#### 마비된종속성 {#maven-dependencies-14}

```xml
<dependency>
  <groupId>com.adobe.livecycle</groupId>
  <artifactId>adobe-repository-client</artifactId>
  <version>11.0.0</version>
</dependency>
```
