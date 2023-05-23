---
title: 프로그래밍 방식으로 엔드포인트 관리
seo-title: Programmatically Managing Endpoints
description: Endpoint Registry 서비스를 사용하여 EJB 끝점 추가, SOAP 끝점 추가, 감시 폴더 끝점 추가, 이메일 끝점 추가, 원격 끝점 추가, 작업 관리자 끝점 추가, 끝점 수정, 끝점 제거 및 끝점 커넥터 정보 검색을 수행할 수 있습니다.
seo-description: Use the Endpoint Registry service to add EJB endpoints, add SOAP endpoint, add Watched Folder endpoints, add Email endpoints, add  Remoting endpoints, add Task Manager endpoints, modify endpoints, remove endpoints, and retrieve endpoint connector information.
uuid: 5dc50946-3323-4c5d-a43b-31c1c980bd04
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 076889a7-9c9f-4b6f-a45b-67a9b3923c36
role: Developer
exl-id: b94dcca2-136b-4b7d-b5ce-544804575876
source-git-commit: 0c7dba43dad8608b4a5de271e1e44942c950fb16
workflow-type: tm+mt
source-wordcount: '10805'
ht-degree: 1%

---

# 프로그래밍 방식으로 엔드포인트 관리 {#programmatically-managing-endpoints}

**이 문서의 샘플 및 예제는 JEE 환경의 AEM Forms에 대해서만 적용됩니다.**

**Endpoint Registry Service 정보**

Endpoint Registry 서비스는 끝점을 프로그래밍 방식으로 관리하는 기능을 제공합니다. 예를 들어 서비스에 다음 유형의 끝점을 추가할 수 있습니다.

* EJB
* SOAP
* 감시 폴더
* 이메일
* (AEM Forms에서 더 이상 사용되지 않음) 원격
* 작업 관리자

>[!NOTE]
>
>SOAP, EJB 및 (JEE에서는 AEM Forms에서 더 이상 사용되지 않음) 원격 끝점은 활성화된 각 서비스에 대해 자동으로 만들어집니다. SOAP 및 EJB 끝점은 모든 서비스 작업에 SOAP 및 EJB를 활성화합니다.

원격 끝점을 사용하면 Flex 클라이언트가 끝점이 추가된 AEM Forms 서비스에서 작업을 호출할 수 있습니다. 끝점과 이름이 같은 Flex 대상이 만들어지고 Flex 클라이언트는 이 대상을 가리키는 RemoteObject를 만들어 관련 서비스에서 작업을 호출할 수 있습니다.

이메일, 작업 관리자 및 감시 폴더 엔드포인트는 서비스의 특정 작업만 노출합니다. 이러한 끝점을 추가하려면 호출할 메서드를 선택하고, 구성 매개 변수를 설정하고, 입력 및 출력 매개 변수 매핑을 지정하는 두 번째 구성 단계가 필요합니다.

TaskManager 끝점을 다음 그룹으로 구성할 수 있습니다. *카테고리*. 그런 다음 이러한 범주는 TaskManager를 통해 작업 영역에 노출되며 최종 사용자는 범주화된 TaskManager 끝점을 볼 수 있습니다. Workspace 내에서 최종 사용자는 탐색 창에 이러한 카테고리를 볼 수 있습니다. 각 카테고리 내의 끝점은 작업 공간의 프로세스 시작 페이지에 프로세스 카드로 표시됩니다.

Endpoint Registry 서비스를 사용하여 다음 작업을 수행할 수 있습니다.

* EJB 엔드포인트를 추가합니다. (참조: [EJB 끝점 추가](programmatically-endpoints.md#adding-ejb-endpoints).)
* SOAP 끝점 추가. (참조: [SOAP 끝점 추가](programmatically-endpoints.md#adding-soap-endpoints).)
* 감시 폴더 엔드포인트 추가(참조 [감시 폴더 엔드포인트 추가](programmatically-endpoints.md#adding-watched-folder-endpoints).)
* 이메일 엔드포인트를 추가합니다. (참조: [이메일 엔드포인트 추가](programmatically-endpoints.md#adding-email-endpoints).)
* 원격 엔드포인트를 추가합니다. (참조: [원격 끝점 추가](programmatically-endpoints.md#adding-remoting-endpoints).)
* TaskManager 끝점 추가(참조) [TaskManager 끝점 추가](programmatically-endpoints.md#adding-taskmanager-endpoints).)
* 엔드포인트 수정(참조 [엔드포인트 수정](programmatically-endpoints.md#modifying-endpoints).)
* 엔드포인트 제거(참조 [엔드포인트 제거](programmatically-endpoints.md#removing-endpoints).)
* 끝점 커넥터 정보 검색(참조) [끝점 커넥터 정보 검색](programmatically-endpoints.md#retrieving-endpoint-connector-information).)

## EJB 끝점 추가 {#adding-ejb-endpoints}

AEM Forms Java API를 사용하여 프로그래밍 방식으로 EJB 끝점을 서비스에 추가할 수 있습니다. 서비스에 EJB 끝점을 추가하면 클라이언트 애플리케이션이 EJB 모드를 사용하여 서비스를 호출할 수 있습니다. 즉, AEM Forms을 호출하는 데 필요한 연결 속성을 설정할 때 EJB 모드를 선택할 수 있습니다. (참조: [연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).)

>[!NOTE]
>
>웹 서비스를 사용하여 EJB 끝점을 추가할 수 없습니다.

>[!NOTE]
>
>일반적으로 EJB 끝점은 기본적으로 서비스에 추가되지만, 프로그래밍 방식으로 배포되거나 EJB 끝점이 제거되어 다시 추가해야 하는 프로세스에 EJB 끝점을 추가할 수 있습니다.

### 단계 요약 {#summary-of-steps}

서비스에 EJB 끝점을 추가하려면 다음 작업을 수행하십시오.

1. 프로젝트 파일을 포함합니다.
1. 만들기 `EndpointRegistry Client` 개체.
1. EJB 끝점 속성을 설정합니다.
1. EJB 엔드포인트를 만듭니다.
1. 끝점을 활성화합니다.

**프로젝트 파일 포함**

개발 프로젝트에 필요한 파일을 포함합니다. 프로젝트의 클래스 경로에 다음 JAR 파일을 추가해야 합니다.

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar (AEM Forms이 JBoss 애플리케이션 서버에 배포된 경우 필요)
* jbossall-client.jar(AEM Forms이 JBoss 애플리케이션 서버에 배포된 경우 필수)

이러한 JAR 파일의 위치에 대한 자세한 내용은 [AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**EndpointRegistry 클라이언트 개체 만들기**

EJB 끝점을 프로그래밍 방식으로 추가하려면 먼저 `EndpointRegistryClient` 개체.

**EJB 엔드포인트 속성 설정**

서비스에 대한 EJB 끝점을 생성하려면 다음 값을 지정합니다.

* **커넥터 식별자**: 만들 끝점의 유형을 지정합니다. EJB 끝점을 만들려면 다음을 지정합니다 `EJB`.
* **설명**: 끝점 설명을 지정합니다.
* **이름**: 끝점의 이름을 지정합니다.
* **서비스 식별자**: 끝점이 속한 서비스를 지정합니다.
* **작업 이름**: 끝점을 사용하여 호출되는 작업의 이름을 지정합니다. EJB 끝점을 생성할 때 와일드카드 문자( `*`). 그러나 모든 서비스 작업을 호출하는 대신 특정 작업을 지정하려면 와일드카드 문자( `*`).

**EJB 엔드포인트 만들기**

EJB 끝점 속성을 설정한 후에는 서비스에 대한 EJB 끝점을 만들 수 있습니다.

**끝점 활성화**

새 끝점을 만든 후에는 이를 활성화해야 합니다. 끝점을 활성화한 후 이 끝점을 사용하여 서비스를 호출할 수 있습니다. 끝점을 활성화하면 관리 콘솔 내에서 볼 수 있습니다.

**추가 참조**

[Java API를 사용하여 EJB 엔드포인트 추가](programmatically-endpoints.md#adding-an-ejb-endpoint-using-the-java-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Java API를 사용하여 EJB 엔드포인트 추가 {#adding-an-ejb-endpoint-using-the-java-api}

Java API를 사용하여 EJB 엔드포인트 추가:

1. 프로젝트 파일을 포함합니다.

   Java 프로젝트의 클래스 경로에 adobe-livecycle-client.jar과 같은 클라이언트 JAR 파일을 포함합니다. (

1. EndpointRegistry 클라이언트 개체를 만듭니다.

   * 만들기 `ServiceClientFactory` 연결 속성을 포함하는 개체입니다.
   * 만들기 `EndpointRegistryClient` 개체를 생성자를 사용하고 `ServiceClientFactory` 개체.

1. EJB 끝점 속성을 설정합니다.

   * 만들기 `CreateEndpointInfo` 개체를 만들 때 사용됩니다.
   * 다음을 호출하여 커넥터 식별자 값 지정 `CreateEndpointInfo` 개체 `setConnectorId` 메서드 및 문자열 값 전달 `EJB`.
   * 를 호출하여 끝점에 대한 설명을 지정하십시오. `CreateEndpointInfo` 개체 `setDescription` 메서드 및 끝점을 설명하는 문자열 값 전달
   * 를 호출하여 끝점의 이름을 지정합니다. `CreateEndpointInfo` 개체 `setName` 메서드 및 이름을 지정하는 문자열 값 전달
   * 를 호출하여 끝점이 속한 서비스를 지정하십시오. `CreateEndpointInfo` 개체 `setServiceId` 메서드 및 서비스 이름을 지정하는 문자열 값 전달
   * 를 호출하여 호출되는 작업을 지정합니다. `CreateEndpointInfo` 개체 `setOperationName` 메서드, 작업 이름을 지정하는 문자열 값 전달 SOAP 및 EJB 끝점의 경우 와일드카드 문자( `*`) - 모든 작업을 암시합니다.

1. EJB 엔드포인트를 만듭니다.

   를 호출하여 끝점을 만듭니다. `EndpointRegistryClient` 개체 `createEndpoint` 메서드 및 전달 `CreateEndpointInfo` 개체. 이 메서드는 `Endpoint` 새 EJB 끝점을 나타내는 개체입니다.

1. 끝점을 활성화합니다.

   를 호출하여 끝점을 활성화합니다. `EndpointRegistryClient` 개체의 활성화 메서드 및 전달 `Endpoint` 에서 반환한 개체 `createEndpoint` 메서드를 사용합니다.

**추가 참조**

[단계 요약](programmatically-endpoints.md#summary-of-steps)

[QuickStart: Java API를 사용하여 EJB 엔드포인트 추가](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-an-ejb-endpoint-using-the-java-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## SOAP 끝점 추가 {#adding-soap-endpoints}

AEM Forms Java API를 사용하여 프로그래밍 방식으로 SOAP 끝점을 서비스에 추가할 수 있습니다. SOAP 끝점을 추가하면 클라이언트 응용 프로그램이 SOAP 모드를 사용하여 서비스를 호출할 수 있습니다. 즉, AEM Forms을 호출하는 데 필요한 연결 속성을 설정할 때 SOAP 모드를 선택할 수 있습니다.

>[!NOTE]
>
>웹 서비스를 사용하여 SOAP 끝점을 추가할 수 없습니다.

>[!NOTE]
>
>일반적으로 SOAP 끝점은 기본적으로 서비스에 추가되지만, SOAP 끝점은 프로그래밍 방식으로 배포되거나 SOAP 끝점이 제거되어 다시 추가되어야 하는 프로세스에 추가할 수 있습니다.

### 단계 요약 {#summary_of_steps-1}

서비스에 SOAP 끝점을 추가하려면 다음 작업을 수행하십시오.

1. 프로젝트 파일을 포함합니다.
1. 만들기 `EndpointRegistryClient` 개체.
1. SOAP 끝점 특성을 설정합니다.
1. SOAP 끝점을 만듭니다.
1. 끝점을 활성화합니다.

**프로젝트 파일 포함**

개발 프로젝트에 필요한 파일을 포함합니다. Java를 사용하여 클라이언트 응용 프로그램을 만드는 경우 필요한 JAR 파일을 포함합니다. 웹 서비스를 사용하는 경우 프록시 파일을 포함해야 합니다.

프로젝트의 클래스 경로에 다음 JAR 파일을 추가해야 합니다.

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar (AEM Forms이 JBoss 애플리케이션 서버에 배포된 경우 필요)
* jbossall-client.jar(AEM Forms이 JBoss 애플리케이션 서버에 배포된 경우 필수)

이러한 JAR 파일은 SOAP 끝점을 만드는 데 필요합니다. 그러나 SOAP 끝점을 사용하여 서비스를 호출하는 경우 추가 JAR 파일이 필요합니다. AEM Forms JAR 파일에 대한 자세한 내용은 [AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**EndpointRegistry 클라이언트 개체 만들기**

SOAP 끝점을 서비스에 프로그래밍 방식으로 추가하려면 다음을 만들어야 합니다. `EndpointRegistryClient` 개체.

**SOAP 끝점 특성 설정**

서비스에 SOAP 끝점을 추가하려면 다음 값을 지정하십시오.

* **커넥터 식별자 값**: 만들 끝점의 유형을 지정합니다. SOAP 끝점을 만들려면 `SOAP`.
* **설명**: 끝점 설명을 지정합니다.
* **이름**: 끝점 이름을 지정합니다.
* **서비스 식별자 값**: 끝점이 속한 서비스를 지정합니다.
* **작업 이름**: 끝점을 사용하여 호출되는 작업의 이름을 지정합니다. SOAP 끝점을 만들 때 와일드카드 문자( `*`). 그러나 모든 서비스 작업을 호출하는 대신 특정 작업을 지정하려면 와일드카드 문자( `*`).

**SOAP 끝점 만들기**

SOAP 끝점 특성을 설정한 후 SOAP 끝점을 만들 수 있습니다.

**끝점 활성화**

새 끝점을 만든 후에는 이를 활성화해야 합니다. 끝점이 활성화되면 서비스를 호출하는 데 사용할 수 있습니다. 끝점을 활성화하면 관리 콘솔 내에서 볼 수 있습니다.

**추가 참조**

[Java API를 사용하여 SOAP 끝점 추가](programmatically-endpoints.md#add-a-soap-endpoint-using-the-java-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Java API를 사용하여 SOAP 끝점 추가 {#add-a-soap-endpoint-using-the-java-api}

Java API를 사용하여 SOAP 끝점을 서비스에 추가합니다.

1. 프로젝트 파일을 포함합니다.

   Java 프로젝트의 클래스 경로에 adobe-livecycle-client.jar과 같은 클라이언트 JAR 파일을 포함합니다.

1. EndpointRegistry 클라이언트 개체를 만듭니다.

   * 만들기 `ServiceClientFactory` 연결 속성을 포함하는 개체입니다.
   * 만들기 `EndpointRegistryClient` 개체를 생성자를 사용하고 `ServiceClientFactory` 개체.

1. SOAP 끝점 특성을 설정합니다.

   * 만들기 `CreateEndpointInfo` 개체를 만들 때 사용됩니다.
   * 다음을 호출하여 커넥터 식별자 값 지정 `CreateEndpointInfo` 개체 `setConnectorId` 메서드 및 문자열 값 전달 `SOAP`.
   * 를 호출하여 끝점에 대한 설명을 지정하십시오. `CreateEndpointInfo` 개체 `setDescription` 메서드 및 끝점을 설명하는 문자열 값 전달
   * 를 호출하여 끝점의 이름을 지정합니다. `CreateEndpointInfo` 개체 `setName` 메서드 및 이름을 지정하는 문자열 값 전달
   * 를 호출하여 끝점이 속한 서비스를 지정하십시오. `CreateEndpointInfo` 개체 `setServiceId` 메서드 및 서비스 이름을 지정하는 문자열 값 전달
   * 를 호출하여 호출되는 작업을 지정합니다. `CreateEndpointInfo` 개체 `setOperationName` 메서드 및 작업 이름을 지정하는 문자열 값 전달 SOAP 및 EJB 끝점의 경우 와일드카드 문자( `*`) - 모든 작업을 암시합니다.

1. SOAP 끝점을 만듭니다.

   를 호출하여 끝점을 만듭니다. `EndpointRegistryClient` 개체 `createEndpoint` 메서드 및 전달 `CreateEndpointInfo` 개체. 이 메서드는 `Endpoint` 새 SOAP 끝점을 나타내는 개체입니다.

1. 끝점을 활성화합니다.

   를 호출하여 끝점을 활성화합니다. `EndpointRegistryClient` 개체의 활성화 메서드를 호출하고 `Endpoint` 에서 반환한 개체 `createEndpoint` 메서드를 사용합니다.

**추가 참조**

[단계 요약](programmatically-endpoints.md#summary-of-steps)

[QuickStart: Java API를 사용하여 SOAP 끝점 추가](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-a-soap-endpoint-using-the-java-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 감시 폴더 엔드포인트 추가 {#adding-watched-folder-endpoints}

AEM Forms Java API를 사용하여 감시 폴더 엔드포인트를 서비스에 프로그래밍 방식으로 추가할 수 있습니다. 감시 폴더 엔드포인트를 추가하면 사용자는 폴더에 파일(예: PDF 파일)을 배치할 수 있습니다. 파일이 폴더에 배치되면 구성된 서비스가 호출되고 파일이 조작됩니다. 이 서비스는 지정된 작업을 수행한 후 수정된 파일을 지정된 출력 폴더에 저장합니다. 감시 폴더는 고정된 비율 간격으로 또는 매주 월요일, 수요일 및 금요일 정오와 같이 cron schedule로 스캔되도록 구성됩니다.

감시 폴더 엔드포인트를 서비스에 프로그래밍 방식으로 추가하려면 다음과 같은 단기 프로세스를 고려하십시오. *EncryptDocument*. (참조: [AEM Forms 프로세스 이해](/help/forms/developing/aem-forms-processes.md#understanding-aem-forms-processes).)

![aw_aw_encryptdocumentprocess](assets/aw_aw_encryptdocumentprocess.png)

이 프로세스는 보안되지 않은 PDF 문서를 입력 값으로 받아들인 다음 보안되지 않은 PDF 문서를 `EncryptPDFUsingPassword` 작업. PDF 문서는 암호로 암호화되며, 암호로 암호화된 PDF 문서는 본 과정의 출력값이다. 입력 값(보안되지 않은 PDF 문서)의 이름은 입니다. `InDoc` 및 데이터 유형은 입니다. `com.adobe.idp.Document`. 출력 값(암호로 암호화된 PDF 문서)의 이름은 입니다. `SecuredDoc` 및 데이터 유형은 입니다. `com.adobe.idp.Document`.

>[!NOTE]
>
>웹 서비스를 사용하여 감시 폴더 끝점을 추가할 수 없습니다.

### 단계 요약 {#summary_of_steps-2}

감시 폴더 엔드포인트를 서비스에 추가하려면 다음 작업을 수행하십시오.

1. 프로젝트 파일을 포함합니다.
1. 만들기 `EndpointRegistryClient` 개체.
1. 감시 폴더 끝점 특성을 설정합니다.
1. 구성 값을 지정합니다.
1. 입력 매개 변수 값을 정의합니다.
1. 출력 매개 변수 값을 정의합니다.
1. 감시 폴더 엔드포인트를 만듭니다.
1. 끝점을 활성화합니다.

**프로젝트 파일 포함**

개발 프로젝트에 필요한 파일을 포함합니다. Java를 사용하여 클라이언트 응용 프로그램을 만드는 경우 필요한 JAR 파일을 포함합니다. 웹 서비스를 사용하는 경우 프록시 파일을 포함해야 합니다.

프로젝트의 클래스 경로에 다음 JAR 파일을 추가해야 합니다.

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar (AEM Forms이 JBoss 애플리케이션 서버에 배포된 경우 필요)
* jbossall-client.jar(AEM Forms이 JBoss 애플리케이션 서버에 배포된 경우 필수)

이러한 JAR 파일의 위치에 대한 자세한 내용은 [AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**EndpointRegistry 클라이언트 개체 만들기**

감시 폴더 끝점을 프로그래밍 방식으로 추가하려면 `EndpointRegistryClient` 개체.

**감시 폴더 끝점 특성 설정**

서비스에 대한 감시 폴더 엔드포인트를 만들려면 다음 값을 지정합니다.

* **커넥터 식별자**: 생성된 끝점의 유형을 지정합니다. 감시 폴더 엔드포인트를 만들려면 다음을 지정합니다. `WatchedFolder`.
* **설명**: 끝점에 대한 설명을 지정합니다.
* **이름**: 끝점의 이름을 지정합니다.
* **서비스 식별자**: 끝점이 속한 서비스를 지정합니다. 예를 들어 이 섹션에 도입된 프로세스에 감시 폴더 엔드포인트를 추가하려면(Workbench를 사용하여 활성화하면 프로세스가 서비스 됨) 다음을 지정합니다. `EncryptDocument`.
* **작업 이름**: 끝점을 사용하여 호출되는 작업의 이름을 지정합니다. 일반적으로 Workbench에서 만든 프로세스에서 시작된 서비스에 대한 감시 폴더 엔드포인트를 만들 때 작업의 이름은 입니다. `invoke`.

**구성 값 지정**

감시 폴더 끝점을 서비스에 프로그래밍 방식으로 추가할 때는 감시 폴더 끝점에 대한 구성 값을 지정해야 합니다. 이러한 구성 값은 관리 콘솔을 사용하여 감시 폴더 엔드포인트가 추가되는 경우 관리자가 지정합니다.

다음 목록은 감시 폴더 끝점을 서비스에 프로그래밍 방식으로 추가할 때 설정되는 구성 값을 지정합니다.

* **url**: 감시 폴더 위치를 지정합니다. 클러스터된 환경에서 이 값은 클러스터의 모든 컴퓨터에서 액세스할 수 있는 공유 네트워크 폴더를 가리켜야 합니다.
* **비동기**: 호출 유형을 비동기 또는 동기식으로 식별합니다. 임시 및 동기 프로세스는 동기적으로만 호출할 수 있습니다. 기본값은 true입니다. 비동기식이 권장됩니다.
* **크론식**: 석영에서 입력 디렉터리의 폴링을 예약하는 데 사용됩니다.
* **purgeDuration**: 필수 속성입니다. 결과 폴더의 파일과 폴더가 이 값보다 오래되면 삭제됩니다. 이 값은 일 단위로 측정됩니다. 이 속성은 결과 폴더가 꽉 차지 않도록 하는 데 유용합니다. -1일 값은 결과 폴더를 삭제하지 않음을 나타냅니다. 기본값은 -1입니다.
* **repeatInterval**: 감시 폴더에서 입력을 검색하는 간격(초)입니다. 제한이 설정되지 않은 경우 이 값은 평균 작업을 처리하는 시간보다 길어야 합니다. 그렇지 않으면 시스템이 오버로드될 수 있습니다. 기본값은 5입니다.
* **repeatCount**: 감시 폴더가 폴더 또는 디렉터리를 스캔한 횟수입니다. -1 값은 무한 스캔을 나타냅니다. 기본값은 -1입니다.
* **throttleOn**: 주어진 시간에 처리할 수 있는 감시 폴더 작업 수를 제한합니다. 최대 작업 수는 batchSize 값에 의해 결정됩니다.
* **userName**: 감시 폴더에서 대상 서비스를 호출할 때 사용되는 사용자 이름입니다. 이 값은 필수입니다. 기본값은 Superadmin입니다.
* **domainName**: 사용자의 도메인입니다. 이 값은 필수입니다. 기본값은 DefaultDom입니다.
* **batchSize**: 스캔당 선택할 파일 또는 폴더 수입니다. 이 값을 사용하여 시스템의 오버로드를 방지하십시오. 한 번에 너무 많은 파일을 검색하면 충돌이 발생할 수 있습니다. 기본값은 2입니다.
* **waitTime**: 만든 후 폴더 또는 파일을 스캔하기 전에 대기하는 시간(밀리초)입니다. 예를 들어, 대기 시간이 36,000,000밀리초(1시간)이고, 파일이 1분 전에 생성된 경우, 이 파일은 59분 이상 경과한 후 선택됩니다. 이 속성은 파일 또는 폴더가 입력 폴더에 완전히 복사되도록 하는 데 유용합니다. 예를 들어 처리할 대형 파일이 있고 파일을 다운로드하는 데 10분이 걸리는 경우 대기 시간을 10&amp;ast;60 &amp;ast;1000밀리초로 설정합니다. 이 설정은 감시 폴더가 10분 동안 기다리지 않은 경우 파일을 검색하지 못하게 합니다. 기본값은 0입니다.
* **exclude파일 패턴**: 감시 폴더가 스캔하고 가져올 파일 및 폴더를 결정하는 데 사용하는 패턴입니다. 이 패턴을 가진 모든 파일 또는 폴더는 처리를 위해 검사되지 않습니다. 이 설정은 입력이 여러 파일이 포함된 폴더인 경우 유용합니다. 폴더의 내용은 감시 폴더에서 선택할 이름이 있는 폴더로 복사할 수 있습니다. 이 단계에서는 폴더가 입력 폴더로 완전히 복사되기 전에 감시 폴더가 처리할 폴더를 선택하지 못하도록 합니다. 예를 들어 excludeFilePattern 값이 `data*`, 일치하는 모든 파일 및 폴더 `data*` 가져오지 않았습니다. 여기에는 다음과 같은 파일 및 폴더가 포함됩니다. `data1`, `data2`등. 또한 패턴을 와일드카드 패턴으로 보완하여 파일 패턴을 지정할 수 있습니다. 감시 폴더는 다음과 같은 와일드카드 패턴을 지원하도록 정규 표현식을 수정합니다. `*.*` 및 `*.pdf`. 이러한 와일드카드 패턴은 정규 표현식에서 지원되지 않습니다.
* **include파일 패턴**: 감시 폴더가 스캔하고 가져올 폴더 및 파일을 결정하는 데 사용하는 패턴입니다. 예를 들어 이 값이 `*`, 일치하는 모든 파일 및 폴더 `input*` 가져왔습니다. 여기에는 다음과 같은 파일 및 폴더가 포함됩니다. `input1`, `input2`등. 기본값은 `*`입니다. 이 값은 모든 파일과 폴더를 나타냅니다. 또한 패턴을 와일드카드 패턴으로 보완하여 파일 패턴을 지정할 수 있습니다. 감시 폴더는 다음과 같은 와일드카드 패턴을 지원하도록 정규 표현식을 수정합니다. `*.*` 및 `*.pdf`. 이러한 와일드카드 패턴은 정규 표현식에서 지원되지 않습니다. 이 값은 필수입니다.
* **결과 폴더 이름**: 저장된 결과가 저장되는 폴더입니다. 이 위치는 절대 또는 상대 디렉토리 경로일 수 있습니다. 결과가 이 폴더에 표시되지 않으면 실패 폴더를 확인하십시오. 읽기 전용 파일은 처리되지 않으며 실패 폴더에 저장됩니다. 기본값은 `result/%Y/%M/%D/`입니다. 감시 폴더 내의 결과 폴더입니다.
* **preserveFolderName**: 성공적으로 스캔 및 픽업한 후 파일이 저장되는 위치입니다. 이 위치는 절대, 상대 또는 null 디렉터리 경로일 수 있습니다. 기본값은 `preserve/%Y/%M/%D/`입니다.
* **failureFolderName**: 오류 파일이 저장되는 폴더입니다. 이 위치는 항상 감시 폴더를 기준으로 합니다. 읽기 전용 파일은 처리되지 않으며 실패 폴더에 저장됩니다. 기본값은 `failure/%Y/%M/%D/`입니다.
* **preserveOnFailure**: 서비스에서 작업을 실행하지 못하는 경우 입력 파일을 유지합니다. 기본값은 true입니다.
* **overwriteDuplicateFile**: true로 설정하면 결과 폴더 및 유지 폴더의 파일이 덮어쓰기됩니다. false로 설정하면 숫자 인덱스 접미사가 있는 파일과 폴더가 이름에 사용됩니다. 기본값은 false입니다.

**입력 매개 변수 값 정의**

감시 폴더 엔드포인트를 만들 때 입력 매개 변수 값을 정의해야 합니다. 즉, 감시 폴더에 의해 호출되는 작업에 전달되는 입력 값을 설명해야 합니다. 예를 들어 이 항목에 소개된 프로세스를 고려하십시오. 라는 입력 값이 한 개 있습니다. `InDoc` 및 해당 데이터 유형은 입니다. `com.adobe.idp.Document`. 이 프로세스에 대한 감시 폴더 엔드포인트를 만들 때(프로세스가 활성화된 후 서비스가 됨) 입력 매개변수 값을 정의해야 합니다.

감시 폴더 엔드포인트에 필요한 입력 매개변수 값을 정의하려면 다음 값을 지정합니다.

**입력 매개 변수 이름**: 입력 매개 변수의 이름입니다. 입력 값의 이름은 프로세스에 대해 Workbench에 지정됩니다. 입력 값이 서비스 작업(Workbench에서 생성된 프로세스가 아닌 서비스)에 속하는 경우 입력 이름은 component.xml 파일에 지정됩니다. 예를 들어 이 섹션에 소개된 프로세스의 입력 매개변수는 다음과 같습니다 `InDoc`.

**매핑 유형**: 서비스 작업을 호출하는 데 필요한 입력 값을 구성하는 데 사용됩니다. 매핑 유형에는 두 가지가 있습니다.

* `Literal`: 감시 폴더 엔드포인트는 필드에 입력한 값을 표시되는 대로 사용합니다. 모든 기본 Java 유형이 지원됩니다. 예를 들어 API에서 String, long, int 및 Boolean과 같은 입력을 사용하는 경우 문자열은 적절한 유형으로 변환되고 서비스가 호출됩니다.
* `Variable`: 입력한 값은 감시 폴더가 입력을 선택하는 데 사용하는 파일 패턴입니다. 예를 들어 매핑 유형으로 변수를 선택하고 입력 문서가 PDF 파일이어야 하는 경우 다음을 지정할 수 있습니다 `*.pdf`를 매핑 값으로 사용하십시오.

**매핑 값**: 매핑 유형의 값을 지정합니다. 예를 들어 `Variable` 매핑 유형, 다음을 지정할 수 있습니다 `*.pdf` 를 파일 패턴으로 사용하십시오.

**데이터 유형**: 입력 값의 데이터 유형을 지정합니다. 예를 들어, 이 섹션에서 소개된 프로세스의 입력 값의 데이터 유형은 다음과 같습니다. `com.adobe.idp.Document`.

**출력 매개 변수 값 정의**

감시 폴더 엔드포인트를 만들 때 출력 매개 변수 값을 정의해야 합니다. 즉, 감시 폴더 끝점에 의해 호출되는 서비스에서 반환되는 출력 값을 설명해야 합니다. 예를 들어 이 항목에 소개된 프로세스를 고려하십시오. 라는 출력 값이 있습니다. `SecuredDoc` 및 해당 데이터 유형은 입니다. `com.adobe.idp.Document`. 이 프로세스에 대한 감시 폴더 엔드포인트를 만들 때(프로세스가 활성화된 후 서비스가 됨) 출력 매개 변수 값을 정의해야 합니다.

감시 폴더 끝점에 필요한 출력 매개 변수 값을 정의하려면 다음 값을 지정합니다.

**출력 매개 변수 이름**: 출력 매개 변수의 이름입니다. 프로세스 출력 값의 이름은 Workbench에 지정됩니다. 출력 값이 서비스 작업(Workbench에서 생성된 프로세스가 아닌 서비스)에 속하는 경우 출력 이름은 component.xml 파일에 지정됩니다. 예를 들어 이 섹션에 소개된 프로세스에 대한 출력 매개변수의 이름은 입니다. `SecuredDoc`.

**매핑 유형**: 서비스 및 작업의 출력을 구성하는 데 사용됩니다. 다음 옵션을 사용할 수 있습니다.

* 서비스가 단일 개체(단일 문서)를 반환하는 경우 패턴은 다음과 같습니다. `%F.pdf` 소스 대상은 sourcefilename.pdf입니다. 예를 들어 이 섹션에 도입된 프로세스는 단일 문서를 반환합니다. 결과적으로 매핑 유형은 다음과 같이 정의할 수 있습니다. `%F.pdf` ( `%F` 은(는) 주어진 파일 이름을 사용함을 의미합니다. 패턴 `%E` 입력 문서의 확장명을 지정합니다.
* 서비스가 목록을 반환하는 경우 패턴은 다음과 같습니다. `Result\%F\`: 소스 대상은 Result\sourcefilename\source1(출력 1) 및 Result\sourcefilename\source2(출력 2)입니다.
* 서비스가 맵을 반환하는 경우 패턴은 다음과 같습니다. `Result\%F\`원본 대상은 Result\sourcefilename\file1 및 Result\sourcefilename\file2입니다. 맵에 둘 이상의 오브젝트가 있는 경우 패턴은 다음과 같습니다. `Result\%F.pdf` 원본 대상은 Result\sourcefilename1.pdf(출력 1), Result\sourcefilenam2.pdf(출력 2) 등입니다.

**데이터 유형**: 반환 값의 데이터 유형을 지정합니다. 예를 들어 이 섹션에 소개된 프로세스의 반환 값에 대한 데이터 유형은 다음과 같습니다 `com.adobe.idp.Document`.

**감시 폴더 엔드포인트 만들기**

끝점의 속성, 구성 값을 설정하고 입력 및 출력 매개 변수 값을 정의한 후에는 감시 폴더 끝점을 만들어야 합니다.

**끝점 활성화**

감시 폴더 엔드포인트를 만든 후에는 이를 활성화해야 합니다. 끝점이 활성화되면 서비스를 호출하는 데 사용할 수 있습니다. 끝점을 활성화하면 관리 콘솔 내에서 볼 수 있습니다.

**추가 참조**

[Java API를 사용하여 감시 폴더 엔드포인트 추가](programmatically-endpoints.md#add-a-watched-folder-endpoint-using-the-java-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Java API를 사용하여 감시 폴더 엔드포인트 추가 {#add-a-watched-folder-endpoint-using-the-java-api}

AEM Forms Java API를 사용하여 감시 폴더 엔드포인트 추가:

1. 프로젝트 파일을 포함합니다.

   Java 프로젝트의 클래스 경로에 adobe-livecycle-client.jar과 같은 클라이언트 JAR 파일을 포함합니다.

1. EndpointRegistry 클라이언트 개체를 만듭니다.

   * 만들기 `ServiceClientFactory` 연결 속성을 포함하는 개체입니다.
   * 만들기 `EndpointRegistryClient` 개체를 생성자를 사용하고 `ServiceClientFactory` 개체.

1. 감시 폴더 끝점 특성을 설정합니다.

   * 만들기 `CreateEndpointInfo` 개체를 만들 때 사용됩니다.
   * 다음을 호출하여 커넥터 식별자 값 지정 `CreateEndpointInfo` 개체 `setConnectorId` 메서드 및 문자열 값 전달 `WatchedFolder`.
   * 를 호출하여 끝점에 대한 설명을 지정하십시오. `CreateEndpointInfo` 개체 `setDescription` 메서드 및 끝점을 설명하는 문자열 값 전달
   * 를 호출하여 끝점의 이름을 지정합니다. `CreateEndpointInfo` 개체 `setName` 메서드 및 이름을 지정하는 문자열 값 전달
   * 를 호출하여 끝점이 속한 서비스를 지정하십시오. `CreateEndpointInfo` 개체 `setServiceId` 메서드 및 서비스 이름을 지정하는 문자열 값 전달
   * 를 호출하여 호출되는 작업을 지정합니다. `CreateEndpointInfo` 개체 `setOperationName` 메서드 및 작업 이름을 지정하는 문자열 값 전달 일반적으로 Workbench에서 만든 프로세스에서 시작된 서비스에 대한 감시 폴더 끝점을 만들 때 작업의 이름은 호출됩니다.

1. 구성 값을 지정합니다.

   감시 폴더 끝점에 대해 설정할 각 구성 값에 대해 `CreateEndpointInfo` 개체 `setConfigParameterAsText` 메서드를 사용합니다. 예를 들어, `url` 구성 값, 호출 `CreateEndpointInfo` 개체 `setConfigParameterAsText` 메서드를 실행하고 다음 문자열 값을 전달하십시오.

   * 구성 값의 이름을 지정하는 문자열 값입니다. 를 설정할 때 `url` 구성 값, 지정 `url`.
   * 구성 값의 값을 지정하는 문자열 값입니다. 를 설정할 때 `url` 구성 값에서 감시 폴더 위치를 지정합니다.

   >[!NOTE]
   >
   >EncryptDocument 서비스에 대해 설정된 모든 구성 값을 보려면 다음 위치에 있는 Java 코드 예를 참조하십시오. [QuickStart: Java API를 사용하여 감시 폴더 엔드포인트 추가](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-a-watched-folder-endpoint-using-the-java-api).

1. 입력 매개 변수 값을 정의합니다.

   다음을 호출하여 입력 매개 변수 값 정의 `CreateEndpointInfo` 개체 `setInputParameterMapping` 메서드를 실행하고 다음 값을 전달합니다.

   * 입력 매개 변수의 이름을 지정하는 문자열 값입니다. 예를 들어 EncryptDocument 서비스에 대한 입력 매개 변수의 이름은 입니다. `InDoc`.
   * 입력 매개 변수의 데이터 형식을 지정하는 문자열 값입니다. (예: `InDoc` 입력 매개 변수: `com.adobe.idp.Document`.
   * 매핑 유형을 지정하는 문자열 값입니다. 예를 들어 다음을 지정할 수 있습니다 `variable`.
   * 매핑 유형 값을 지정하는 문자열 값입니다. 예를 들어 &amp;ast;.pdf를 파일 패턴으로 지정할 수 있습니다.

   >[!NOTE]
   >
   >호출 `setInputParameterMapping` 정의할 각 입력 매개 변수 값에 대한 메서드입니다. EncryptDocument 프로세스에는 입력 매개 변수가 하나만 있으므로 이 메서드를 한 번 호출해야 합니다.

1. 출력 매개 변수 값을 정의합니다.

   다음을 호출하여 출력 매개 변수 값 정의 `CreateEndpointInfo` 개체 `setOutputParameterMapping` 메서드를 실행하고 다음 값을 전달합니다.

   * 출력 매개 변수의 이름을 지정하는 문자열 값입니다. 예를 들어 EncryptDocument 서비스에 대한 출력 매개 변수의 이름은 입니다. `SecuredDoc`.
   * 출력 매개 변수의 데이터 형식을 지정하는 문자열 값입니다. (예: `SecuredDoc` 출력 매개 변수: `com.adobe.idp.Document`.
   * 매핑 유형을 지정하는 문자열 값입니다. 예를 들어 다음을 지정할 수 있습니다 `%F.pdf`.

1. 감시 폴더 엔드포인트를 만듭니다.

   를 호출하여 끝점을 만듭니다. `EndpointRegistryClient` 개체 `createEndpoint` 메서드 및 전달 `CreateEndpointInfo` 개체. 이 메서드는 `Endpoint` 감시 폴더 끝점을 나타내는 개체입니다.

1. 끝점을 활성화합니다.

   를 호출하여 끝점을 활성화합니다. `EndpointRegistryClient` 개체 `enable` 메서드 및 전달 `Endpoint` 에서 반환한 개체 `createEndpoint` 메서드를 사용합니다.

**추가 참조**

[단계 요약](programmatically-endpoints.md#summary-of-steps)

[QuickStart: Java API를 사용하여 감시 폴더 엔드포인트 추가](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-a-watched-folder-endpoint-using-the-java-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 감시 폴더 구성 값 상수 파일 {#watched-folder-configuration-values-constant-file}

다음 [QuickStart: Java API를 사용하여 감시 폴더 엔드포인트 추가](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-a-watched-folder-endpoint-using-the-java-api) 는 빠른 시작을 컴파일하기 위해 Java 프로젝트의 일부여야 하는 상수 파일을 사용합니다. 이 상수 파일은 감시 폴더 끝점을 추가할 때 설정해야 하는 구성 값을 나타냅니다. 다음 Java 코드는 상수 파일을 나타냅니다.

```java
 /**
     * This class contains constants that can be used when setting Watched Folder
     * configuration values
     */

 public final class WatchedFolderEndpointConfigConstants {

         public static final String PROPERTY_FILEPROVIDER_URL = "url";
         public static final String PROPERTY_PROPERTY_ASYNCHRONOUS = "asynchronous";
         public static final String PROPERTY_CRON_EXPRESSION = "cronExpression";
         public static final String PROPERTY_PURGE_DURATION = "purgeDuration";
         public static final String PROPERTY_REPEAT_INTERVAL = "repeatInterval";
         public static final String PROPERTY_REPEAT_COUNT = "repeatCount";
         public static final String PROPERTY_THROTTLE = "throttleOn";
         public static final String PROPERTY_USERNAMER = "userName";
         public static final String PROPERTY_DOMAINNAME = "domainName";
         public static final String PROPERTY_FILEPROVIDER_BATCH_SIZE = "batchSize";
         public static final String PROPERTY_FILEPROVIDER_WAIT_TIME = "waitTime";
         public static final String PROPERTY_EXCLUDE_FILE_PATTERN = "excludeFilePattern";
         public static final String PROPERTY_INCLUDE_FILE_PATTERN = "excludeFilePattern";
         public static final String PROPERTY_FILEPROVIDER_RESULT_FOLDER_NAME =  "resultFolderName";
         public static final String PROPERTY_FILEPROVIDER_PRESERVE_FOLDER_NAME = "preserveFolderName";
         public static final String PROPERTY_FILEPROVIDER_FAILURE_FOLDER_NAME = "failureFolderName";
         public static final String PROPERTY_FILEPROVIDER_PRESERVE_ON_FAILURE = "preserveOnFailure";
         public static final String PROPERTY_FILEPROVIDER_OVERWRITE_DUPLICATE_FILENAME = "overwriteDuplicateFilename";
        }
```

## 이메일 엔드포인트 추가 {#adding-email-endpoints}

AEM Forms Java API를 사용하여 이메일 엔드포인트를 서비스에 프로그래밍 방식으로 추가할 수 있습니다. 이메일 엔드포인트를 추가하면 사용자가 하나 이상의 첨부 파일이 있는 이메일 메시지를 지정된 이메일 계정에 보낼 수 있습니다. 그런 다음 서비스 구성 작업이 호출되고 파일이 조작됩니다. 서비스는 지정된 작업을 수행한 후 수정된 파일을 첨부 파일로 하여 보낸 사람에게 전자 메일 메시지를 보냅니다.

이메일 엔드포인트를 서비스에 프로그래밍 방식으로 추가하려면 다음과 같은 단기 프로세스를 고려하십시오. *MyApplication\EncryptDocument*. 단기 프로세스에 대한 자세한 내용은 [AEM Forms 프로세스 이해](/help/forms/developing/aem-forms-processes.md#understanding-aem-forms-processes).

![ae_ae_encryptdocumentprocess](assets/ae_ae_encryptdocumentprocess.png)

이 프로세스는 보안되지 않은 PDF 문서를 입력 값으로 받아들인 다음 보안되지 않은 PDF 문서를 `EncryptPDFUsingPassword` 작업. 이 프로세스는 암호로 PDF 문서를 암호화하고 암호로 암호화된 PDF 문서를 출력 값으로 반환합니다. 입력 값(보안되지 않은 PDF 문서)의 이름은 입니다. `InDoc` 및 데이터 유형은 입니다. `com.adobe.idp.Document`. 출력 값(암호로 암호화된 PDF 문서)의 이름은 입니다. `SecuredDoc` 및 데이터 유형은 입니다. `com.adobe.idp.Document`.

>[!NOTE]
>
>웹 서비스를 사용하여 이메일 엔드포인트를 추가할 수 없습니다.

### 단계 요약 {#summary_of_steps-3}

서비스에 이메일 엔드포인트를 추가하려면 다음 작업을 수행하십시오.

1. 프로젝트 파일을 포함합니다.
1. 만들기 `EndpointRegistryClient` 개체.
1. 이메일 엔드포인트 속성을 설정합니다.
1. 구성 값을 지정합니다.
1. 입력 매개 변수 값을 정의합니다.
1. 출력 매개 변수 값을 정의합니다.
1. 이메일 엔드포인트를 만듭니다.
1. 끝점을 활성화합니다.

**프로젝트 파일 포함**

개발 프로젝트에 필요한 파일을 포함합니다. Java를 사용하여 클라이언트 응용 프로그램을 만드는 경우 필요한 JAR 파일을 포함합니다. 웹 서비스를 사용하는 경우 프록시 파일을 포함해야 합니다.

프로젝트의 클래스 경로에 다음 JAR 파일을 추가해야 합니다.

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar (AEM Forms이 JBoss 애플리케이션 서버에 배포된 경우 필요)
* jbossall-client.jar(AEM Forms이 JBoss 애플리케이션 서버에 배포된 경우 필수)

이러한 JAR 파일의 위치에 대한 자세한 내용은 [AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**EndpointRegistry 클라이언트 개체 만들기**

이메일 엔드포인트를 프로그래밍 방식으로 추가하려면 먼저 `EndpointRegistryClient` 개체.

**이메일 엔드포인트 속성 설정**

서비스에 대한 이메일 엔드포인트를 만들려면 다음 값을 지정합니다.

* **커넥터 식별자 값**: 생성된 끝점의 유형을 지정합니다. 이메일 엔드포인트를 만들려면 다음을 지정합니다. `Email`.
* **설명**: 끝점에 대한 설명을 지정합니다.
* **이름**: 끝점의 이름을 지정합니다.
* **서비스 식별자 값**: 끝점이 속한 서비스를 지정합니다. 예를 들어 이 섹션에 도입된 프로세스에 이메일 엔드포인트를 추가하려면(Workbench를 사용하여 활성화하면 프로세스가 서비스 됨) 다음을 지정합니다. `EncryptDocument`.
* **작업 이름**: 끝점을 사용하여 호출되는 작업의 이름을 지정합니다. 일반적으로 Workbench에서 만든 프로세스에서 시작된 서비스에 대한 이메일 엔드포인트를 만들 때 작업의 이름은 입니다. `invoke`.

**구성 값 지정**

서비스에 이메일 엔드포인트를 프로그래밍 방식으로 추가할 때 이메일 엔드포인트에 대한 구성 값을 지정해야 합니다. 이러한 구성 값은 관리 콘솔을 사용하여 이메일 엔드포인트가 추가되는 경우 관리자가 지정합니다.

>[!NOTE]
>
>모니터링되는 이메일 계정은 이메일 엔드포인트에만 사용되는 특수 계정입니다. 이 계정은 일반 사용자의 이메일 계정이 아닙니다. 일반 사용자의 이메일 계정은 이메일 공급자가 메시지를 완료한 후 받은 편지함에서 이메일 메시지를 삭제하므로 이메일 공급자가 사용하는 계정으로 구성하지 않아야 합니다.

다음 구성 값은 서비스에 이메일 엔드포인트를 프로그래밍 방식으로 추가할 때 설정됩니다.

* **크론식**: cron 표현식을 사용하여 이메일을 예약해야 하는 경우 cron 표현식입니다.
* **repeatCount**: 이메일 끝점이 폴더 또는 디렉터리를 스캔한 횟수입니다. -1 값은 무한 스캔을 나타냅니다. 기본값은 -1입니다.
* **repeatInterval**: 받는 사람이 받는 메일을 확인하는 데 사용하는 검색 속도(초)입니다. 기본값은 10입니다.
* **startDelay**: 스케줄러가 시작된 후 스캔을 기다리는 시간입니다. 기본 시간은 0입니다.
* **batchSize**: 최적의 성능을 위해 받는 사람이 스캔당 처리하는 이메일 메시지 수입니다. -1 값은 모든 이메일을 나타냅니다. 기본값은 2입니다.
* **userName**: 이메일에서 대상 서비스를 호출할 때 사용되는 사용자 이름입니다. 기본값은 `SuperAdmin`입니다.
* **domainName**: 필수 구성 값입니다. 기본값은 `DefaultDom`입니다.
* **도메인 패턴**: 공급자가 허용하는 수신 이메일의 도메인 패턴을 지정합니다. 예를 들어 다음과 같습니다. `adobe.com` 가 사용되고 adobe.com에서의 이메일만 처리되며 다른 도메인의 이메일은 무시됩니다.
* **파일 패턴**: 공급자가 허용하는 수신 파일 첨부 파일 패턴을 지정합니다. 특정 파일 확장명(&amp;ast;.dat, &amp;ast;.xml)이 있는 파일, 특정 이름(데이터)이 있는 파일 및 이름과 확장명이 복합 표현식(&amp;ast;)이 있는 파일이 여기에 포함됩니다.[dD][aA]&#39;port&#39;). 기본값은 `*`입니다.
* **recipientSucceededJob**: 성공적인 작업을 나타내는 메시지가 전송되는 이메일 주소입니다. 기본적으로 성공적인 작업 메시지는 항상 보낸 사람에게 전송됩니다. 입력한 경우 `sender`, 전자 메일 결과가 보낸 사람에게 전송됩니다. 최대 100명의 수신자가 지원됩니다. 전자 메일 주소를 사용하여 각 주소를 쉼표로 구분하여 추가 수신자를 지정하십시오. 이 옵션을 끄려면 이 값을 비워 둡니다. 경우에 따라 프로세스를 트리거하고 결과에 대한 이메일 알림을 원하지 않을 수 있습니다. 기본값은 `sender`입니다.
* **recipientFailedJob**: 실패한 작업을 나타내는 메시지가 전송되는 이메일 주소입니다. 기본적으로 실패한 작업 메시지는 항상 보낸 사람에게 전송됩니다. 입력한 경우 `sender`, 전자 메일 결과가 보낸 사람에게 전송됩니다. 최대 100명의 수신자가 지원됩니다. 전자 메일 주소를 사용하여 각 주소를 쉼표로 구분하여 추가 수신자를 지정하십시오. 이 옵션을 끄려면 이 값을 비워 둡니다. 기본값은 `sender`입니다.
* **inboxHost**: 이메일 공급자가 스캔할 받은 편지함 호스트 이름 또는 IP 주소입니다.
* **inboxPort**: 이메일 서버가 사용하는 포트입니다. POP3의 기본값은 110이고 IMAP의 기본값은 143입니다. SSL이 활성화된 경우 POP3의 기본값은 995이고 IMAP의 기본값은 993입니다.
* **inboxProtocol**: 받은 편지함을 검색하는 데 사용할 이메일 엔드포인트에 대한 이메일 프로토콜입니다. 옵션은 다음과 같습니다 `IMAP` 또는 `POP3`. 받은 편지함 호스트 메일 서버는 이러한 프로토콜을 지원해야 합니다.
* **inboxTimeOut**: 이메일 공급자가 받은 편지함 응답을 기다리는 시간(초)입니다. 기본값은 60입니다.
* **inboxUser**: 이메일 계정에 로그인하는 데 필요한 사용자 이름입니다. 이메일 서버 및 구성에 따라 이메일의 사용자 이름 부분만 될 수도 있고 전체 이메일 주소일 수도 있습니다.
* **inboxPassword**: 받은 편지함 사용자의 암호입니다.
* **inboxSSLEnabled**: 결과 또는 오류에 대한 알림 메시지를 보낼 때 이메일 공급자가 SSL을 사용하도록 하려면 이 값을 설정하십시오. IMAP 또는 POP3 호스트가 SSL을 지원하는지 확인합니다.
* **smtpHost**: 이메일 공급자가 결과 및 오류 메시지를 보내는 메일 서버의 호스트 이름입니다.
* **smtpPort**: SMTP 포트의 기본값은 25입니다.
* **smtpUser**: 결과 및 오류에 대한 이메일 알림을 전송할 때 사용할 이메일 공급자에 대한 사용자 계정입니다.
* **smtpPassword**: SMTP 계정의 암호입니다. 일부 메일 서버에는 SMTP 암호가 필요하지 않습니다.
* **charSet**: 이메일 공급자가 사용하는 문자 집합입니다. 기본값은 `UTF-8`입니다.
* **smtpSSLEnabled**: 결과 또는 오류에 대한 알림 메시지를 보낼 때 이메일 공급자가 SSL을 사용하도록 하려면 이 값을 설정하십시오. SMTP 호스트가 SSL을 지원하는지 확인합니다.
* **failedJobFolder**: SMTP 메일 서버가 작동하지 않을 때 결과를 저장할 디렉터리를 지정합니다.
* **비동기**: 동기식으로 설정하면 모든 입력 문서가 처리되고 단일 응답이 반환됩니다. 비동기식으로 설정하면 처리되는 각 입력 문서에 대한 응답이 전송됩니다. 예를 들어 이 주제에 도입된 프로세스에 대해 이메일 엔드포인트가 생성되고, 이메일 메시지가 여러 개의 비보안 PDF 문서가 포함된 엔드포인트의 받은 편지함으로 전송됩니다. 모든 PDF 문서가 암호로 암호화되고 끝점이 동기식으로 구성된 경우 모든 보안 PDF 문서가 첨부된 단일 응답 이메일 메시지가 전송됩니다. 끝점이 비동기식으로 구성된 경우 보안 설정된 각 PDF 문서에 대해 별도의 응답 이메일 메시지가 전송됩니다. 각 이메일 메시지에는 하나의 PDF 문서가 첨부 파일로 포함되어 있습니다. 기본값은 비동기입니다.

**입력 매개 변수 값 정의**

이메일 엔드포인트를 만들 때 입력 매개 변수 값을 정의해야 합니다. 즉, 이메일 엔드포인트에서 호출하는 작업에 전달되는 입력 값을 설명해야 합니다. 예를 들어 이 항목에 소개된 프로세스를 고려하십시오. 라는 입력 값이 한 개 있습니다. `InDoc` 및 해당 데이터 유형은 입니다. `com.adobe.idp.Document`. 이 프로세스에 대한 이메일 엔드포인트를 만들 때(프로세스가 활성화된 후 서비스가 됨) 입력 매개변수 값을 정의해야 합니다.

이메일 엔드포인트에 필요한 입력 매개변수 값을 정의하려면 다음 값을 지정합니다.

**입력 매개 변수 이름**: 입력 매개 변수의 이름입니다. 입력 값의 이름은 프로세스에 대해 Workbench에 지정됩니다. 입력 값이 서비스 작업(Workbench에서 생성된 프로세스가 아닌 Forms 서비스)에 속하는 경우 입력 이름이 component.xml 파일에 지정됩니다. 예를 들어 이 섹션에 소개된 프로세스의 입력 매개변수는 다음과 같습니다 `InDoc`.

**매핑 유형**: 서비스 작업을 호출하는 데 필요한 입력 값을 구성하는 데 사용됩니다. 두 가지 유형의 매핑 유형은 다음과 같습니다.

* `Literal`: 이메일 엔드포인트는 필드에 입력한 값을 표시되는 대로 사용합니다. 모든 기본 Java 유형이 지원됩니다. 예를 들어 API에서 String, long, int 및 Boolean과 같은 입력을 사용하는 경우 문자열이 적절한 유형으로 변환되고 서비스가 호출됩니다.
* `Variable`: 입력한 값은 이메일 엔드포인트가 입력을 선택하는 데 사용하는 파일 패턴입니다. 예를 들어 매핑 유형으로 변수를 선택하고 입력 문서가 PDF 파일이어야 하는 경우 다음을 지정할 수 있습니다 `*.pdf` 를 매핑 값으로 사용하십시오.

**매핑 값**: 매핑 유형의 값을 지정합니다. 예를 들어 변수 매핑 유형을 선택하는 경우 `*.pdf` 를 파일 패턴으로 사용하십시오.

**데이터 유형**: 입력 값의 데이터 유형을 지정합니다. 예를들어, 이 섹션에 소개된 프로세스의 입력 값 데이터 형식은 com.adobe.idp.Document입니다.

**출력 매개 변수 값 정의**

이메일 엔드포인트를 만들 때 출력 매개 변수 값을 정의해야 합니다. 즉, 이메일 엔드포인트에서 호출하는 서비스에서 반환되는 출력 값을 설명해야 합니다. 예를 들어 이 항목에 소개된 프로세스를 고려하십시오. 라는 출력 값이 있습니다. `SecuredDoc` 및 해당 데이터 유형은 입니다. `com.adobe.idp.Document`. 이 프로세스에 대한 이메일 엔드포인트를 만들 때(프로세스가 활성화된 후 서비스가 됨) 출력 매개 변수 값을 정의해야 합니다.

이메일 엔드포인트에 필요한 출력 매개변수 값을 정의하려면 다음 값을 지정합니다.

**출력 매개 변수 이름**: 출력 매개 변수의 이름입니다. 프로세스 출력 값의 이름은 Workbench에 지정됩니다. 출력 값이 서비스 작업(Workbench에서 생성된 프로세스가 아닌 서비스)에 속하는 경우 출력 이름은 component.xml 파일에 지정됩니다. 예를 들어 이 섹션에 소개된 프로세스에 대한 출력 매개변수의 이름은 입니다. `SecuredDoc`.

**매핑 유형**: 서비스 및 작업의 출력을 구성하는 데 사용됩니다. 다음 옵션을 사용할 수 있습니다.

* 서비스가 단일 개체(단일 문서)를 반환하는 경우 패턴은 다음과 같습니다. `%F.pdf` 소스 대상은 sourcefilename.pdf입니다. 예를 들어 이 섹션에 도입된 프로세스는 단일 문서를 반환합니다. 결과적으로 매핑 유형은 다음과 같이 정의할 수 있습니다. `%F.pdf` ( `%F` 은(는) 주어진 파일 이름을 사용함을 의미합니다. 패턴 `%E` 입력 문서의 확장명을 지정합니다.
* 서비스가 목록을 반환하는 경우 패턴은 다음과 같습니다. `Result\%F\`: 소스 대상은 Result\sourcefilename\source1(출력 1) 및 Result\sourcefilename\source2(출력 2)입니다.
* 서비스가 맵을 반환하는 경우 패턴은 다음과 같습니다. `Result\%F\`원본 대상은 Result\sourcefilename\file1 및 Result\sourcefilename\file2입니다. 맵에 둘 이상의 오브젝트가 있는 경우 패턴은 다음과 같습니다. `Result\%F.pdf` 원본 대상은 Result\sourcefilename1.pdf(출력 1), Result\sourcefilenam2.pdf(출력 2) 등입니다.

**데이터 유형**: 반환 값의 데이터 유형을 지정합니다. 예를 들어 이 섹션에 소개된 프로세스의 반환 값에 대한 데이터 유형은 다음과 같습니다 `com.adobe.idp.Document`.

**이메일 엔드포인트 만들기**

이메일 엔드포인트 속성 및 구성 값을 설정하고 입력 및 출력 매개 변수 값을 정의한 후에는 이메일 엔드포인트를 만들어야 합니다.

**끝점 활성화**

이메일 엔드포인트를 만든 후에는 이를 활성화해야 합니다. 끝점이 활성화되면 서비스를 호출하는 데 사용할 수 있습니다. 끝점을 활성화하면 관리 콘솔 내에서 볼 수 있습니다.

**추가 참조**

[Java API를 사용하여 이메일 엔드포인트 추가](programmatically-endpoints.md#add-an-email-endpoint-using-the-java-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Java API를 사용하여 이메일 엔드포인트 추가 {#add-an-email-endpoint-using-the-java-api}

Java API를 사용하여 이메일 엔드포인트 추가:

1. 프로젝트 파일을 포함합니다.

   Java 프로젝트의 클래스 경로에 adobe-livecycle-client.jar과 같은 클라이언트 JAR 파일을 포함합니다.

1. EndpointRegistry 클라이언트 개체를 만듭니다.

   * 만들기 `ServiceClientFactory` 연결 속성을 포함하는 개체입니다.
   * 만들기 `EndpointRegistryClient` 개체를 생성자를 사용하고 `ServiceClientFactory` 개체.

1. 이메일 엔드포인트 속성을 설정합니다.

   * 만들기 `CreateEndpointInfo` 개체를 만들 때 사용됩니다.
   * 다음을 호출하여 커넥터 식별자 값 지정 `CreateEndpointInfo` 개체 `setConnectorId` 메서드 및 문자열 값 전달 `Email`.
   * 를 호출하여 끝점에 대한 설명을 지정하십시오. `CreateEndpointInfo` 개체 `setDescription` 메서드 및 끝점을 설명하는 문자열 값 전달
   * 를 호출하여 끝점의 이름을 지정합니다. `CreateEndpointInfo` 개체 `setName` 메서드 및 이름을 지정하는 문자열 값 전달
   * 를 호출하여 끝점이 속한 서비스를 지정하십시오. `CreateEndpointInfo` 개체 `setServiceId` 메서드 및 서비스 이름을 지정하는 문자열 값 전달
   * 를 호출하여 호출되는 작업을 지정합니다. `CreateEndpointInfo` 개체 `setOperationName` 메서드 및 작업 이름을 지정하는 문자열 값 전달 일반적으로 Workbench에서 만든 프로세스에서 시작된 서비스에 대한 이메일 엔드포인트를 만들 때 작업의 이름은 호출됩니다.

1. 구성 값을 지정합니다.

   이메일 엔드포인트에 대해 설정할 각 구성 값에 대해 `CreateEndpointInfo` 개체 `setConfigParameterAsText` 메서드를 사용합니다. 예를 들어, `smtpHost` 구성 값, 호출 `CreateEndpointInfo` 개체 `setConfigParameterAsText` 메서드를 실행하고 다음 값을 전달합니다.

   * 구성 값의 이름을 지정하는 문자열 값입니다. 를 설정할 때 `smtpHost` 구성 값, 지정 `smtpHost`.
   * 구성 값의 값을 지정하는 문자열 값입니다. 를 설정할 때 `smtpHost` 구성 값을 사용하려면 SMTP 서버의 이름을 지정하는 문자열 값을 지정하십시오.

   >[!NOTE]
   >
   >이 섹션에 소개된 EncryptDocument 서비스에 대해 설정된 모든 구성 값을 보려면 다음 위치에 있는 Java 코드 예를 참조하십시오. [빠른 시작: Java API를 사용하여 이메일 엔드포인트 추가](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-an-email-endpoint-using-the-java-api).

1. 입력 매개 변수 값을 정의합니다.

   다음을 호출하여 입력 매개 변수 값 정의 `CreateEndpointInfo` 개체 `setInputParameterMapping` 메서드를 실행하고 다음 값을 전달합니다.

   * 입력 매개 변수의 이름을 지정하는 문자열 값입니다. 예를 들어 EncryptDocument 서비스에 대한 입력 매개 변수의 이름은 입니다. `InDoc`.
   * 입력 매개 변수의 데이터 형식을 지정하는 문자열 값입니다. (예: `InDoc` 입력 매개 변수: `com.adobe.idp.Document`.
   * 매핑 유형을 지정하는 문자열 값입니다. 예를 들어 다음을 지정할 수 있습니다 `variable`.
   * 매핑 유형 값을 지정하는 문자열 값입니다. 예를 들어 &amp;ast;.pdf를 파일 패턴으로 지정할 수 있습니다.

   >[!NOTE]
   >
   >호출 `setInputParameterMapping` 정의할 각 입력 매개 변수 값에 대한 메서드입니다. EncryptDocument 프로세스에는 입력 매개 변수가 하나만 있으므로 이 메서드를 한 번 호출해야 합니다.

1. 출력 매개 변수 값을 정의합니다.

   다음을 호출하여 출력 매개 변수 값 정의 `CreateEndpointInfo` 개체 `setOutputParameterMapping` 메서드 및 다음 값 전달:

   * 출력 매개 변수의 이름을 지정하는 문자열 값입니다. 예를 들어 EncryptDocument 서비스에 대한 출력 매개 변수의 이름은 입니다. `SecuredDoc`.
   * 출력 매개 변수의 데이터 형식을 지정하는 문자열 값입니다. (예: `SecuredDoc` 출력 매개 변수: `com.adobe.idp.Document`.
   * 매핑 유형을 지정하는 문자열 값입니다. 예를 들어 다음을 지정할 수 있습니다 `%F.pdf`.

1. 이메일 엔드포인트를 만듭니다.

   를 호출하여 끝점을 만듭니다. `EndpointRegistryClient` 개체 `createEndpoint` 메서드 및 전달 `CreateEndpointInfo` 개체. 이 메서드는 `Endpoint` 이메일 끝점을 나타내는 개체입니다.

1. 끝점을 활성화합니다.

   를 호출하여 끝점을 활성화합니다. `EndpointRegistryClient` 개체 `enable` 메서드 및 전달 `Endpoint` 에서 반환한 개체 `createEndpoint` 메서드를 사용합니다.

**추가 참조**

[단계 요약](programmatically-endpoints.md#summary-of-steps)

[QuickStart: Java API를 사용하여 감시 폴더 엔드포인트 추가](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-a-watched-folder-endpoint-using-the-java-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 이메일 구성 값 상수 파일 {#email-configuration-values-constant-file}

다음 [빠른 시작: Java API를 사용하여 이메일 엔드포인트 추가](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-an-email-endpoint-using-the-java-api) 는 빠른 시작을 컴파일하기 위해 Java 프로젝트의 일부여야 하는 상수 파일을 사용합니다. 이 상수 파일은 이메일 엔드포인트를 추가할 때 설정해야 하는 구성 값을 나타냅니다. 다음 Java 코드는 상수 파일을 나타냅니다.

```java
 /**
     * This class contains constants that can be used when setting email endpoint
     * configuration values
     */
 public class EmailEndpointConfigConstants {

     public static final String PROPERTY_EMAILPROVIDER_CRON_EXPRESSION = "cronExpression";
     public static final String PROPERTY_EMAILPROVIDER_REPREAT_COUNT = "repeatCount";
     public static final String PROPERTY_EMAILPROVIDER_REPREAT_INTERVAL = "repeatInterval";
     public static final String PROPERTY_EMAILPROVIDER_START_DELAY = "startDelay";
     public static final String PROPERTY_EMAILPROVIDER_BATCH_SIZE = "batchSize";
     public static final String PROPERTY_EMAILPROVIDER_USERNAME = "userName";
     public static final String PROPERTY_EMAILPROVIDER_DOMAINNAME = "domainName";
     public static final String PROPERTY_EMAILPROVIDER_DOMAINPATTERN = "domainPattern";
     public static final String PROPERTY_EMAILPROVIDER_FILEPATTERN = "filePattern";
     public static final String PROPERTY_EMAILPROVIDER_RECIPIENT_SUCCESSFUL_JOB = "recipientSuccessfulJob";
     public static final String PROPERTY_EMAILPROVIDER_RECIPIENT_FAILED_JOB = "recipientFailedJob";
     public static final String PROPERTY_EMAILPROVIDER_INBOX_HOST = "inboxHost";
     public static final String PROPERTY_EMAILPROVIDER_INBOX_PORT = "inboxPort";
     public static final String PROPERTY_EMAILPROVIDER_PROTOCOL = "inboxProtocol";
     public static final String PROPERTY_EMAILPROVIDER_INBOX_TIMEOUT = "inboxTimeOut";
     public static final String PROPERTY_EMAILPROVIDER_INBOX_USER = "inboxUser";
     public static final String PROPERTY_EMAILPROVIDER_INBOX_PASSWORD = "inboxPassword";
     public static final String PROPERTY_EMAILPROVIDER_INBOX_SSL = "inboxSSLEnabled";
     public static final String PROPERTY_EMAILPROVIDER_SMTP_HOST = "smtpHost";
     public static final String PROPERTY_EMAILPROVIDER_SMTP_PORT = "smtpPort";
     public static final String PROPERTY_EMAILPROVIDER_SMTP_USER = "smtpUser";
     public static final String PROPERTY_EMAILPROVIDER_SMTP_PASSWORD = "smtpPassword";
     public static final String PROPERTY_EMAILPROVIDER_CHARSET = "charSet";
     public static final String PROPERTY_EMAILPROVIDER_SMTP_SSL = "smtpSSLEnabled";
     public static final String PROPERTY_EMAILPROVIDER_FAILED_FOLDER = "failedJobFolder";
     public static final String PROPERTY_EMAILPROVIDER_ASYNCHRONOUS = "asynchronous";
 }
```

## 원격 끝점 추가 {#adding-remoting-endpoints}

>[!NOTE]
>
>LiveCycle Remoting API는 JEE의 AEM Forms에서 더 이상 사용되지 않습니다.

AEM Forms Java API를 사용하여 원격 끝점을 서비스에 프로그래밍 방식으로 추가할 수 있습니다. 원격 끝점을 추가하면 Flex 응용 프로그램에서 원격을 사용하여 서비스를 호출할 수 있습니다. (참조: [(AEM Forms에서 더 이상 사용되지 않는 기능)AEM Forms 원격을 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-remoting.md#invoking-aem-forms-using-remoting).)

원격 끝점을 서비스에 프로그래밍 방식으로 추가하려면 다음 이름의 단기 프로세스를 고려하십시오. *EncryptDocument*.

![ar_ar_encryptdocumentprocess](assets/ar_ar_encryptdocumentprocess.png)

이 프로세스는 보안되지 않은 PDF 문서를 입력 값으로 받아들인 다음 보안되지 않은 PDF 문서를 `EncryptPDFUsingPassword` 작업. PDF 문서는 암호로 암호화되며, 암호로 암호화된 PDF 문서는 본 과정의 출력값이다. 입력 값(보안되지 않은 PDF 문서)의 이름은 입니다. `InDoc` 및 데이터 유형은 입니다. `com.adobe.idp.Document`. 출력 값(암호로 암호화된 PDF 문서)의 이름은 입니다. `SecuredDoc` 및 데이터 유형은 입니다. `com.adobe.idp.Document`.

원격 끝점을 서비스에 추가하는 방법을 보여 주기 위해 이 섹션에서는 원격 끝점을 EncryptDocument라는 서비스에 추가합니다.

>[!NOTE]
>
>웹 서비스를 사용하여 원격 끝점을 추가할 수 없습니다.

### 단계 요약 {#summary_of_steps-4}

서비스에서 끝점을 제거하려면 다음 작업을 수행하십시오.

1. 프로젝트 파일을 포함합니다.
1. 만들기 `EndpointRegistryClient` 개체.
1. 원격 끝점 특성을 설정합니다.
1. 원격 끝점을 만듭니다.
1. 끝점을 활성화합니다.

**프로젝트 파일 포함**

개발 프로젝트에 필요한 파일을 포함합니다. Java를 사용하여 클라이언트 응용 프로그램을 만드는 경우 필요한 JAR 파일을 포함합니다. 웹 서비스를 사용하는 경우 프록시 파일을 포함해야 합니다.

프로젝트의 클래스 경로에 다음 JAR 파일을 추가해야 합니다.

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar (AEM Forms이 JBoss 애플리케이션 서버에 배포된 경우 필요)
* jbossall-client.jar(AEM Forms이 JBoss 애플리케이션 서버에 배포된 경우 필수)

이러한 JAR 파일의 위치에 대한 자세한 내용은 [AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**EndpointRegistry 클라이언트 개체 만들기**

원격 끝점을 프로그래밍 방식으로 추가하려면 `EndpointRegistryClient` 개체.

**원격 끝점 특성 설정**

서비스에 대한 원격 끝점을 만들려면 다음 값을 지정합니다.

* **커넥터 식별자 값**: 생성된 끝점의 유형을 지정합니다. 원격 끝점을 만들려면 `Remoting`.
* **설명**: 끝점에 대한 설명을 지정합니다.
* **이름**: 끝점의 이름을 지정합니다.
* **서비스 식별자 값**: 끝점이 속한 서비스를 지정합니다. 예를 들어 이 섹션에 도입된 프로세스에 원격 끝점을 추가하려면(Workbench 내에서 활성화되면 프로세스가 서비스 됨) 다음을 지정합니다. `EncryptDocument`.
* **작업 이름**: 끝점을 사용하여 호출되는 작업의 이름을 지정합니다. 원격 끝점을 만들 때 와일드카드 문자(&amp;ast;)를 지정합니다.

**원격 끝점 만들기**

원격 끝점 특성을 설정한 후에는 서비스에 대한 원격 끝점을 만들 수 있습니다.

**끝점 활성화**

새 끝점을 만든 후에는 이를 활성화해야 합니다. 원격 끝점이 활성화되면 Flex 클라이언트가 서비스를 호출할 수 있습니다.

**추가 참조**

[Java API를 사용하여 원격 끝점 추가](programmatically-endpoints.md#add-a-remoting-endpoint-using-the-java-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Java API를 사용하여 원격 끝점 추가 {#add-a-remoting-endpoint-using-the-java-api}

Java API를 사용하여 원격 엔드포인트 추가:

1. 프로젝트 파일을 포함합니다.

   Java 프로젝트의 클래스 경로에 adobe-livecycle-client.jar과 같은 클라이언트 JAR 파일을 포함합니다.

1. EndpointRegistry 클라이언트 개체를 만듭니다.

   * 만들기 `ServiceClientFactory` 연결 속성을 포함하는 개체입니다.
   * 만들기 `EndpointRegistryClient` 개체를 생성자를 사용하고 `ServiceClientFactory` 개체.

1. 원격 끝점 특성을 설정합니다.

   * 만들기 `CreateEndpointInfo` 개체를 만들 때 사용됩니다.
   * 다음을 호출하여 커넥터 식별자 값 지정 `CreateEndpointInfo` 개체 `setConnectorId` 메서드 및 문자열 값 전달 `Remoting`.
   * 를 호출하여 끝점에 대한 설명을 지정하십시오. `CreateEndpointInfo` 개체 `setDescription` 메서드 및 끝점을 설명하는 문자열 값 전달
   * 를 호출하여 끝점의 이름을 지정합니다. `CreateEndpointInfo` 개체 `setName` 메서드 및 이름을 지정하는 문자열 값 전달
   * 를 호출하여 끝점이 속한 서비스를 지정하십시오. `CreateEndpointInfo` 개체 `setServiceId` 메서드 및 서비스 이름을 지정하는 문자열 값 전달
   * 에서 호출하는 작업을 지정합니다. `CreateEndpointInfo` 개체 `setOperationName` 메서드 및 작업 이름을 지정하는 문자열 값 전달 원격 끝점의 경우 와일드카드 문자(&amp;ast;)를 지정합니다.

1. 원격 끝점을 만듭니다.

   를 호출하여 끝점을 만듭니다. `EndpointRegistryClient` 개체 `createEndpoint` 메서드 및 전달 `CreateEndpointInfo` 개체. 이 메서드는 `Endpoint` 새 원격 끝점을 나타내는 개체입니다.

1. 끝점을 활성화합니다.

   를 호출하여 끝점을 활성화합니다. `EndpointRegistryClient` 개체 `enable` 메서드 및 전달 `Endpoint` 에서 반환한 개체 `createEndpoint` 메서드를 사용합니다.

**추가 참조**

[단계 요약](programmatically-endpoints.md#summary-of-steps)

[QuickStart: Java API를 사용하여 원격 끝점 추가](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-a-remoting-endpoint-using-the-java-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## TaskManager 끝점 추가 {#adding-taskmanager-endpoints}

AEM Forms Java API를 사용하여 프로그래밍 방식으로 TaskManager 끝점을 서비스에 추가할 수 있습니다. TaskManager 끝점을 서비스에 추가하면 Workspace 사용자가 서비스를 호출할 수 있습니다. 즉, 작업 영역에서 작업하는 사용자는 해당 TaskManager 끝점이 있는 프로세스를 호출할 수 있습니다.

>[!NOTE]
>
>웹 서비스를 사용하여 TaskManager 끝점을 추가할 수 없습니다.

### 단계 요약 {#summary_of_steps-5}

TaskManager 끝점을 서비스에 추가하려면 다음 작업을 수행하십시오.

1. 프로젝트 파일을 포함합니다.
1. 만들기 `EndpointRegistryClient` 개체.
1. 끝점에 대한 범주를 만듭니다.
1. TaskManager 끝점 특성을 설정합니다.
1. TaskManager 끝점을 만듭니다.
1. 끝점을 활성화합니다.

**프로젝트 파일 포함**

개발 프로젝트에 필요한 파일을 포함합니다. Java를 사용하여 클라이언트 응용 프로그램을 만드는 경우 필요한 JAR 파일을 포함합니다. 웹 서비스를 사용하는 경우 프록시 파일을 포함해야 합니다.

프로젝트의 클래스 경로에 다음 JAR 파일을 추가해야 합니다.

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar (AEM Forms이 JBoss 애플리케이션 서버에 배포된 경우 필요)
* jbossall-client.jar(AEM Forms이 JBoss 애플리케이션 서버에 배포된 경우 필수)

이러한 JAR 파일의 위치에 대한 자세한 내용은 [AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**EndpointRegistry 클라이언트 개체 만들기**

프로그래밍 방식으로 TaskManager 끝점을 추가하려면 먼저 `EndpointRegistryClient` 개체.

**끝점에 대한 범주 만들기**

범주는 작업 영역 내에서 서비스를 구성하는 데 사용됩니다. 즉, 작업 영역 사용자는 작업 영역 내에서 범주를 선택하여 TaskManager 끝점이 있는 서비스를 호출할 수 있습니다. TaskManager 끝점을 만들 때 기존 범주를 참조하거나 프로그래밍 방식으로 새 범주를 만들 수 있습니다.

>[!NOTE]
>
>이 섹션에서는 TaskManager 끝점을 서비스에 추가하는 과정에서 새 범주를 만듭니다.

**TaskManager 끝점 특성 설정**

서비스에 대한 TaskManager 끝점을 만들려면 다음 값을 지정하십시오.

* **커넥터 식별자**: 생성된 끝점의 유형을 지정합니다. TaskManager 끝점을 만들려면 다음을 지정하십시오 `TaskManagerConnector`.
* **설명**: 끝점에 대한 설명을 지정합니다.
* **이름**: 끝점의 이름을 지정합니다.
* **서비스 식별자**: 끝점이 속한 서비스를 지정합니다.
* **범주**: TaskManager 끝점과 연결된 범주 식별자 값을 지정합니다.
* **작업 이름**: 일반적으로 Workbench에서 생성된 프로세스에서 비롯된 서비스에 대한 TaskManager 끝점을 생성할 때 작업의 이름은 입니다. `invoke`.

**TaskManager 끝점 만들기**

TaskManager 끝점 특성을 설정한 후에는 서비스에 대한 TaskManager 끝점을 만들 수 있습니다.

**끝점 활성화**

새 끝점을 만든 후에는 이를 활성화해야 합니다. 끝점이 활성화되면 Workspace 내에서 서비스를 호출하는 데 사용할 수 있습니다. 끝점을 활성화하면 관리 콘솔 내에서 볼 수 있습니다.

**추가 참조**

[Java API를 사용하여 TaskManager 끝점 추가](programmatically-endpoints.md#add-a-taskmanager-endpoint-using-the-java-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Java API를 사용하여 TaskManager 끝점 추가 {#add-a-taskmanager-endpoint-using-the-java-api}

Java API를 사용하여 TaskManager 끝점 추가:

1. 프로젝트 파일을 포함합니다.

   Java 프로젝트의 클래스 경로에 adobe-livecycle-client.jar과 같은 클라이언트 JAR 파일을 포함합니다.

1. EndpointRegistry 클라이언트 개체를 만듭니다.

   * 만들기 `ServiceClientFactory` 연결 속성을 포함하는 개체입니다.
   * 만들기 `EndpointRegistryClient` 개체를 생성자를 사용하고 `ServiceClientFactory` 개체.

1. 끝점에 대한 범주를 만듭니다.

   * 만들기 `CreateEndpointCategoryInfo` 개체, 개체, 개체, 개체 또는 개체의 생성자를 사용하고 다음 값을

      * 범주의 식별자 값을 지정하는 문자열 값
      * 범주에 대한 설명을 지정하는 문자열 값
   * 를 호출하여 범주를 만듭니다. `EndpointRegistryClient` 개체 `createEndpointCategory` 메서드 및 전달 `CreateEndpointCategoryInfo` 개체. 이 메서드는 `EndpointCategory` 새 카테고리를 나타내는 개체입니다.


1. TaskManager 끝점 특성을 설정합니다.

   * 만들기 `CreateEndpointInfo` 개체를 만들 때 사용됩니다.
   * 다음을 호출하여 커넥터 식별자 값 지정 `CreateEndpointInfo` 개체 `setConnectorId` 메서드 및 문자열 값 전달 `TaskManagerConnector`.
   * 를 호출하여 끝점에 대한 설명을 지정하십시오. `CreateEndpointInfo` 개체 `setDescription` 메서드 및 끝점을 설명하는 문자열 값 전달
   * 를 호출하여 끝점의 이름을 지정합니다. `CreateEndpointInfo` 개체 `setName` 메서드 및 이름을 지정하는 문자열 값 전달
   * 를 호출하여 끝점이 속한 서비스를 지정하십시오. `CreateEndpointInfo` 개체 `setServiceId` 메서드 및 서비스 이름을 지정하는 문자열 값 전달
   * 를 호출하여 끝점이 속한 범주를 지정합니다. `CreateEndpointInfo` 개체 `setCategoryId` 메서드 및 카테고리 식별자 값을 지정하는 문자열 값 전달 다음을 호출할 수 있습니다. `EndpointCategory` 개체 `getId` 이 범주의 식별자 값을 가져오는 방법.
   * 를 호출하여 호출되는 작업을 지정합니다. `CreateEndpointInfo` 개체 `setOperationName` 메서드 및 작업 이름을 지정하는 문자열 값 전달 일반적으로 를 만들 때 `TaskManager` Workbench에서 생성된 프로세스에서 시작된 서비스의 끝점입니다. 작업의 이름은 입니다. `invoke`.

1. TaskManager 끝점을 만듭니다.

   를 호출하여 끝점을 만듭니다. `EndpointRegistryClient` 개체 `createEndpoint` 메서드 및 전달 `CreateEndpointInfo` 개체. 이 메서드는 `Endpoint` 새 TaskManager 끝점을 나타내는 개체입니다.

1. 끝점을 활성화합니다.

   를 호출하여 끝점을 활성화합니다. `EndpointRegistryClient` 개체 `enable` 메서드 및 전달 `Endpoint` 에서 반환한 개체 `createEndpoint` 메서드를 사용합니다.

**추가 참조**

[단계 요약](programmatically-endpoints.md#summary-of-steps)

[QuickStart: Java API를 사용하여 TaskManager 끝점 추가](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-adding-a-taskmanager-endpoint-using-the-java-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 엔드포인트 수정 {#modifying-endpoints}

AEM Forms Java API를 사용하여 기존 끝점을 프로그래밍 방식으로 수정할 수 있습니다. 끝점을 수정하면 끝점의 동작을 변경할 수 있습니다. 예를 들어 감시 폴더로 사용되는 폴더를 지정하는 감시 폴더 엔드포인트를 생각해 보십시오. 감시 폴더 끝점에 속하는 구성 값을 프로그래밍 방식으로 수정할 수 있으므로 다른 폴더가 감시 폴더로 작동합니다. 감시 폴더 끝점에 속하는 구성 값에 대한 자세한 내용은 [감시 폴더 엔드포인트 추가](programmatically-endpoints.md#adding-watched-folder-endpoints).

엔드포인트 수정 방법을 보여 주기 위해 이 섹션에서는 감시 폴더로 동작하는 폴더를 변경하여 감시 폴더 엔드포인트를 수정합니다.

>[!NOTE]
>
>웹 서비스를 사용하여 끝점을 수정할 수 없습니다.

### 단계 요약 {#summary_of_steps-6}

끝점을 수정하려면 다음 작업을 수행합니다.

1. 프로젝트 파일을 포함합니다.
1. 만들기 `EndpointRegistryClient` 개체.
1. 끝점을 검색합니다.
1. 새 구성 값을 지정합니다.

**프로젝트 파일 포함**

개발 프로젝트에 필요한 파일을 포함합니다. Java를 사용하여 클라이언트 응용 프로그램을 만드는 경우 필요한 JAR 파일을 포함합니다. 웹 서비스를 사용하는 경우 프록시 파일을 포함해야 합니다.

프로젝트의 클래스 경로에 다음 JAR 파일을 추가해야 합니다.

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar (AEM Forms이 JBoss 애플리케이션 서버에 배포된 경우 필요)
* jbossall-client.jar(AEM Forms이 JBoss 애플리케이션 서버에 배포된 경우 필수)

이러한 JAR 파일의 위치에 대한 자세한 내용은 [AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**EndpointRegistry 클라이언트 개체 만들기**

끝점을 프로그래밍 방식으로 수정하려면 `EndpointRegistryClient` 개체.

**수정할 엔드포인트 검색**

끝점을 수정하려면 먼저 끝점을 검색해야 합니다. 끝점을 검색하려면 끝점에 액세스할 수 있는 사용자로 연결해야 합니다. 관리자로 연결하는 것이 좋습니다. (참조: [연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)).

엔드포인트 목록을 검색하여 엔드포인트를 검색할 수 있습니다. 그런 다음 목록을 반복하여 제거할 특정 끝점을 검색할 수 있습니다. 예를 들어 끝점에 해당하는 서비스와 끝점 유형을 확인하여 끝점을 찾을 수 있습니다. 끝점을 찾으면 수정할 수 있습니다.

**새 구성 값 지정**

끝점을 수정할 때 새 구성 값을 지정합니다. 예를 들어 감시 폴더 엔드포인트를 수정하려면 수정하려는 값뿐만 아니라 모든 감시 폴더 엔드포인트 구성 값을 재설정합니다. 감시 폴더 끝점에 속하는 구성 값에 대한 자세한 내용은 [감시 폴더 엔드포인트 추가](programmatically-endpoints.md#adding-watched-folder-endpoints).

>[!NOTE]
>
>이메일 엔드포인트에 속하는 구성 값에 대한 자세한 내용은 [이메일 엔드포인트 추가](programmatically-endpoints.md#adding-email-endpoints).

>[!NOTE]
>
>끝점에 의해 호출되는 서비스는 수정할 수 없습니다. 서비스를 수정하려고 하면 예외가 발생합니다. 지정된 끝점과 연결된 서비스를 수정하려면 끝점을 제거하고 새 끝점을 만듭니다. (참조: [엔드포인트 제거](programmatically-endpoints.md#removing-endpoints).)

**추가 참조**

[Java API를 사용하여 엔드포인트 수정](programmatically-endpoints.md#modifying-an-endpoint-using-the-java-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Java API를 사용하여 엔드포인트 수정 {#modifying-an-endpoint-using-the-java-api}

Java API를 사용하여 끝점을 수정합니다.

1. 프로젝트 파일을 포함합니다.

   Java 프로젝트의 클래스 경로에 adobe-livecycle-client.jar과 같은 클라이언트 JAR 파일을 포함합니다.

1. EndpointRegistry 클라이언트 개체를 만듭니다.

   * 만들기 `ServiceClientFactory` 연결 속성을 포함하는 개체입니다.
   * 만들기 `EndpointRegistryClient` 개체를 생성자를 사용하고 `ServiceClientFactory` 개체.

1. 수정할 끝점을 검색합니다.

   * 연결 속성에 지정된 현재 사용자가 액세스할 수 있는 모든 끝점 목록을 `EndpointRegistryClient` 개체 `getEndpoints` 방법 및 전달 `PagingFilter` 필터 역할을 하는 개체입니다. 다음을 전달할 수 있습니다. `(PagingFilter)null` 값을 반환하여 모든 끝점을 반환합니다. 이 메서드는 `java.util.List` 각 요소가 다음에 있는 개체 `Endpoint` 개체. 에 대한 자세한 내용 `PagingFilter` 개체, 참조 [AEM Forms API 참조](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).
   * 다음을 반복합니다. `java.util.List` 종단점이 있는지 확인하는 개체입니다. 끝점이 존재하는 경우 각 요소는 `EndPoint` 인스턴스.
   * 를 호출하여 끝점에 해당하는 서비스를 확인합니다. `EndPoint` 개체 `getServiceId` 메서드를 사용합니다. 이 메서드는 서비스 이름을 지정하는 문자열 값을 반환합니다.
   * 를 호출하여 끝점의 유형을 확인합니다. `EndPoint` 개체 `getConnectorId` 메서드를 사용합니다. 이 메서드는 끝점의 유형을 지정하는 문자열 값을 반환합니다. 예를 들어 끝점이 감시 폴더 끝점인 경우 이 메서드는 를 반환합니다 `WatchedFolder`.

1. 새 구성 값을 지정합니다.

   * 만들기 `ModifyEndpointInfo` 해당 생성자를 호출하여 개체를 작성합니다.
   * 설정할 각 구성 값에 대해 `ModifyEndpointInfo` 개체 `setConfigParameterAsText` 메서드를 사용합니다. 예를 들어 URL 구성 값을 설정하려면 `ModifyEndpointInfo` 개체 `setConfigParameterAsText` 메서드를 실행하고 다음 값을 전달합니다.

      * 구성 값의 이름을 지정하는 문자열 값입니다. 예를 들어, `url` 구성 값, 지정 `url`.
      * 구성 값의 값을 지정하는 문자열 값입니다. 에 대한 값을 정의하려면 `url` 구성 값에서 감시 폴더 위치를 지정합니다.
   * 호출 `EndpointRegistryClient` 개체 `modifyEndpoint` 메서드 및 전달 `ModifyEndpointInfo` 개체.


**추가 참조**

[단계 요약](programmatically-endpoints.md#summary-of-steps)

[QuickStart: Java API를 사용하여 엔드포인트 수정](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-modifying-an-endpoint-using-the-java-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 엔드포인트 제거 {#removing-endpoints}

AEM Forms Java API를 사용하여 프로그래밍 방식으로 서비스에서 끝점을 제거할 수 있습니다. 끝점을 제거한 후에는 끝점이 활성화한 호출 메서드를 사용하여 서비스를 호출할 수 없습니다. 예를 들어 서비스에서 SOAP 끝점을 제거하면 SOAP 모드를 사용하여 서비스를 호출할 수 없습니다.

서비스에서 끝점을 제거하는 방법을 보여 주기 위해 이 섹션에서는 라는 서비스에서 EJB 끝점을 제거합니다. *EncryptDocument*.

>[!NOTE]
>
>웹 서비스를 사용하여 끝점을 제거할 수 없습니다.

### 단계 요약 {#summary_of_steps-7}

서비스에서 끝점을 제거하려면 다음 작업을 수행하십시오.

1. 프로젝트 파일을 포함합니다.
1. 만들기 `EndpointRegistryClient` 개체.
1. 끝점을 검색합니다.
1. 끝점을 제거합니다.

**프로젝트 파일 포함**

개발 프로젝트에 필요한 파일을 포함하십시오. Java를 사용하여 클라이언트 응용 프로그램을 만드는 경우 필요한 JAR 파일을 포함합니다. 웹 서비스를 사용하는 경우 프록시 파일을 포함해야 합니다.

프로젝트의 클래스 경로에 다음 JAR 파일을 추가해야 합니다.

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar (AEM Forms이 JBoss 애플리케이션 서버에 배포된 경우 필요)
* jbossall-client.jar(AEM Forms이 JBoss 애플리케이션 서버에 배포된 경우 필수)

이러한 JAR 파일의 위치에 대한 자세한 내용은 [AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**EndpointRegistry 클라이언트 개체 만들기**

끝점을 프로그래밍 방식으로 제거하려면 `EndpointRegistryClient` 개체.

**제거할 엔드포인트 검색**

끝점을 제거하려면 먼저 끝점을 검색해야 합니다. 끝점을 검색하려면 끝점에 액세스할 수 있는 사용자로 연결해야 합니다. 관리자로 연결하는 것이 좋습니다. (참조: [연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)).

엔드포인트 목록을 검색하여 엔드포인트를 검색할 수 있습니다. 그런 다음 목록을 반복하여 제거할 특정 끝점을 검색할 수 있습니다. 예를 들어 끝점에 해당하는 서비스와 끝점 유형을 확인하여 끝점을 찾을 수 있습니다. 끝점을 찾으면 제거할 수 있습니다.

**끝점 제거**

새 끝점을 만든 후에는 이를 활성화해야 합니다. 끝점이 활성화되면 서비스를 호출하는 데 사용할 수 있습니다. 끝점을 활성화하면 관리 콘솔 내에서 볼 수 있습니다.

**추가 참조**

[Java API를 사용하여 엔드포인트 제거](programmatically-endpoints.md#removing-an-endpoint-using-the-java-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Java API를 사용하여 엔드포인트 제거 {#removing-an-endpoint-using-the-java-api}

Java API를 사용하여 엔드포인트 제거:

1. 프로젝트 파일을 포함합니다.

   Java 프로젝트의 클래스 경로에 adobe-livecycle-client.jar과 같은 클라이언트 JAR 파일을 포함합니다.

1. EndpointRegistry 클라이언트 개체를 만듭니다.

   * 만들기 `ServiceClientFactory` 연결 속성을 포함하는 개체입니다.
   * 만들기 `EndpointRegistryClient` 개체를 생성자를 사용하고 `ServiceClientFactory` 개체.

1. 제거할 끝점을 검색합니다.

   * 를 호출하여 현재 사용자(연결 속성에 지정됨)가 액세스할 수 있는 모든 끝점 목록을 검색합니다. `EndpointRegistryClient` 개체 `getEndpoints` 방법 및 전달 `PagingFilter` 필터 역할을 하는 개체입니다. 다음을 전달할 수 있습니다. `(PagingFilter)null` 를 클릭하여 모든 끝점을 반환합니다. 이 메서드는 `java.util.List` 각 요소가 다음에 있는 개체 `Endpoint` 개체.
   * 다음을 반복합니다. `java.util.List` 종단점이 있는지 확인하는 개체입니다. 끝점이 존재하는 경우 각 요소는 `EndPoint` 인스턴스.
   * 를 호출하여 끝점에 해당하는 서비스를 확인합니다. `EndPoint` 개체 `getServiceId` 메서드를 사용합니다. 이 메서드는 서비스 이름을 지정하는 문자열 값을 반환합니다.
   * 를 호출하여 끝점의 유형을 확인합니다. `EndPoint` 개체 `getConnectorId` 메서드를 사용합니다. 이 메서드는 끝점의 유형을 지정하는 문자열 값을 반환합니다. 예를 들어 끝점이 EJB 끝점인 경우 이 메서드는 를 반환합니다 `EJB`.

1. 끝점을 제거합니다.

   를 호출하여 끝점을 제거합니다. `EndpointRegistryClient` 개체 `remove` 메서드 및 전달 `EndPoint` 제거할 끝점을 나타내는 개체입니다.

**추가 참조**

[단계 요약](programmatically-endpoints.md#summary-of-steps)

[QuickStart: Java API를 사용하여 엔드포인트 제거](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-removing-an-endpoint-using-the-java-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 끝점 커넥터 정보 검색 {#retrieving-endpoint-connector-information}

AEM Forms API를 사용하여 Endpoint Connectors에 대한 정보를 프로그래밍 방식으로 검색할 수 있습니다. 커넥터를 사용하면 엔드포인트가 다양한 호출 방법을 사용하여 서비스를 호출할 수 있습니다. 예를 들어 감시 폴더 커넥터를 사용하면 엔드포인트가 감시 폴더를 사용하여 서비스를 호출할 수 있습니다. Endpoint Connectors에 대한 정보를 프로그래밍 방식으로 검색하여 필요한 구성 값 및 선택 사항 같은 커넥터와 연결된 구성 값을 검색할 수 있습니다.

끝점 커넥터에 대한 정보를 검색하는 방법을 보여 주기 위해 이 섹션에서는 감시 폴더 커넥터에 대한 정보를 검색합니다. (참조: [감시 폴더 엔드포인트 추가](programmatically-endpoints.md#adding-watched-folder-endpoints).)

>[!NOTE]
>
>웹 서비스를 사용하여 끝점에 대한 정보를 검색할 수 없습니다.

>[!NOTE]
>
>이 항목에서는 `ConnectorRegistryClient` 끝점 커넥터에 대한 정보를 검색하는 API입니다. (참조: [AEM Forms API 참조](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).)

### 단계 요약 {#summary_of_steps-8}

끝점 커넥터 정보를 검색하려면 다음 작업을 수행합니다.

1. 프로젝트 파일을 포함합니다.
1. 만들기 `ConnectorRegistryClient` 개체.
1. 커넥터 유형을 지정합니다.
1. 구성 값을 검색합니다.

**프로젝트 파일 포함**

개발 프로젝트에 필요한 파일을 포함하십시오. Java를 사용하여 클라이언트 응용 프로그램을 만드는 경우 필요한 JAR 파일을 포함합니다. 웹 서비스를 사용하는 경우 프록시 파일을 포함해야 합니다.

프로젝트의 클래스 경로에 다음 JAR 파일을 추가해야 합니다.

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-utilities.jar (AEM Forms이 JBoss 애플리케이션 서버에 배포된 경우 필요)
* jbossall-client.jar(AEM Forms이 JBoss 애플리케이션 서버에 배포된 경우 필수)

AEM Forms이 JBoss가 아닌 지원되는 J2EE 애플리케이션 서버에 배포된 경우 adobe-utilities.jar 및 jbossall-client.jar을 AEM Forms이 배포된 J2EE 애플리케이션 서버에 관련된 JAR 파일로 바꿉니다. 모든 AEM Forms JAR 파일의 위치에 대한 자세한 내용은 [AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**ConnectorRegistry 클라이언트 개체 만들기**

끝점 커넥터 정보를 프로그래밍 방식으로 검색하려면 `ConnectorRegistryClient` 개체.

**커넥터 유형 지정**

정보를 검색할 커넥터 유형을 지정합니다. 다음 유형의 커넥터가 있습니다.

* **EJB**: 클라이언트 애플리케이션이 EJB 모드를 사용하여 서비스를 호출할 수 있도록 합니다.
* **SOAP**: 클라이언트 응용 프로그램에서 SOAP 모드를 사용하여 서비스를 호출할 수 있습니다.
* **감시 폴더**: 감시 폴더가 서비스를 호출할 수 있도록 합니다.
* **이메일**: 이메일 메시지에서 서비스를 호출할 수 있습니다.
* **원격**: Flex 클라이언트 애플리케이션이 서비스를 호출할 수 있도록 합니다.
* **작업 관리자 커넥터**: Workspace 사용자가 Workspace 내에서 서비스를 호출할 수 있도록 합니다.

**구성 값 검색**

커넥터 유형을 지정한 후 지원되는 구성 값과 같은 커넥터에 대한 정보를 검색할 수 있습니다. 예를 들어, 어떤 커넥터에 대해 어떤 구성 값이 필수인지 그리고 어떤 구성 값이 선택 사항인지 결정할 수 있습니다.

**추가 참조**

[Java API를 사용하여 엔드포인트 커넥터 정보 검색](programmatically-endpoints.md#retrieve-endpoint-connector-information-using-the-java-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Java API를 사용하여 엔드포인트 커넥터 정보 검색 {#retrieve-endpoint-connector-information-using-the-java-api}

Java API를 사용하여 끝점 커넥터 정보 검색:

1. 프로젝트 파일을 포함합니다. .

   Java 프로젝트의 클래스 경로에 adobe-livecycle-client.jar과 같은 클라이언트 JAR 파일을 포함합니다.

1. ConnectorRegistry 클라이언트 개체를 만듭니다.

   * 만들기 `ServiceClientFactory` 연결 속성을 포함하는 개체입니다.
   * 만들기 `ConnectorRegistryClient` 개체를 생성자를 사용하고 `ServiceClientFactory` 개체.

1. 커넥터 유형을 지정합니다.

   다음을 호출하여 커넥터 유형 지정 `ConnectorRegistryClient` 개체 `getEndpointDefinition` 메서드 및 커넥터 유형을 지정하는 문자열 값 전달 예를 들어 감시 폴더 커넥터 유형을 지정하려면 문자열 값을 전달합니다 `WatchedFolder`. 이 메서드는 `Endpoint` 커넥터 유형에 해당하는 개체입니다.

1. 구성 값을 검색합니다.

   * 를 호출하여 이 끝점 내에 연결된 구성 값을 검색합니다. `Endpoint` 개체 `getConfigParameters` 메서드를 사용합니다. 이 메서드는 배열의 `ConfigParameter` 개체.
   * 배열 내의 각 요소를 검색하여 각 구성 값에 대한 정보를 검색합니다. 각 요소는 `ConfigParameter` 개체. 예를 들어 를 호출하여 구성 값이 필요한지 또는 선택 사항인지 여부를 확인할 수 있습니다. `ConfigParameter` 개체 `isRequired` 메서드를 사용합니다. 구성 값이 필요한 경우 이 메서드는 를 반환합니다 `true`.

**추가 참조**

[단계 요약](programmatically-endpoints.md#summary-of-steps)

[QuickStart: Java API를 사용하여 엔드포인트 커넥터 정보 검색](/help/forms/developing/endpoint-registry-java-api-quick.md#quickstart-retrieving-endpoint-connector-information-using-the-java-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)
