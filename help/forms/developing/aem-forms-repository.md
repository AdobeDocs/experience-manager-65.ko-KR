---
title: AEM Forms 저장소 작업
seo-title: Working with AEM Forms Repository
description: Java API 및 웹 서비스 API를 사용하여 폴더 만들기, 쓰기, 목록, 읽기, 업데이트 및 검색 리소스를 포함하도록 AEM Forms 저장소를 관리합니다. 또한 리소스 관계를 만들고 리소스를 잠그고 삭제하는 방법도 알아봅니다.
seo-description: Manage AEM Forms repository to create folders, write, list, read, update resources, and search resources using the Java API and Web Service API. In addition, learn how to create resource relationships, lock and delete resources.
uuid: 6ead49f9-ca0d-4ee4-86a6-0a9ced6ec4f8
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: d2c95881-6c02-4e34-85af-84607df54287
role: Developer
exl-id: a07e51ca-fea0-4719-8071-1b7e805de2ae
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '9117'
ht-degree: 0%

---

# AEM Forms 저장소 작업 {#working-with-aem-forms-repository}

**이 문서의 샘플 및 예제는 JEE 환경의 AEM Forms에 대해서만 적용됩니다.**

**저장소 서비스 정보**

저장소 서비스는 AEM Forms에 리소스 저장 및 관리 서비스를 제공합니다. 개발자가 다음을 만들 때 *AEM Forms* 애플리케이션에서 파일 시스템 대신 저장소에 에셋을 배포할 수 있습니다. 자산에는 XML 양식, PDF forms(Acrobat 양식 포함), 양식 단편, 이미지, 프로필, SWF, 정책 파일, DDX 파일, XML 스키마, WSDL 파일 및 테스트 데이터를 비롯한 모든 유형의 자료가 포함될 수 있습니다.

예를 들어 다음과 같은 Forms 애플리케이션을 고려해 보십시오. *Applications/FormsApplication*:

![ww_ww_formrepository](assets/ww_ww_formrepository.png)

FormsFolder에 Loan.xdp라는 파일이 있습니다. 이 양식 디자인에 액세스하려면 전체 경로(버전 포함)를 지정합니다. `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.

>[!NOTE]
>
>Workbench를 사용하여 Forms 애플리케이션을 만드는 방법에 대한 자세한 내용은 다음을 참조하십시오. [Workbench 도움말](https://www.adobe.com/go/learn_aemforms_workbench_63).

AEM Forms 저장소에 있는 리소스의 경로는 다음과 같습니다.

`Applications/Application-name/Application-version/Folder.../Filename`

다음 값은 URI 값의 몇 가지 예를 보여 줍니다.

* Applications/AppraisalReport/1.0/Forms/FullForm.xdp
* Applications/AnotherApp/1.1/Assets/picture.jpg
* Applications/SomeApp/2.0/Resources/Data/XSDs/MyData.xsd

>[!NOTE]
>
>웹 브라우저를 사용하여 AEM Forms 저장소를 탐색할 수 있습니다. 저장소를 탐색하려면 웹 브라우저에 다음 URL을 입력합니다 `https://[server name]:[server port]/repository`. 웹 브라우저를 사용하여 AEM Forms 저장소를 사용하여 작업 섹션과 연관된 빠른 시작 결과를 확인할 수 있습니다. 예를 들어 AEM Forms 저장소에 컨텐츠를 추가하는 경우 웹 브라우저에서 컨텐츠를 볼 수 있습니다. (참조: [빠른 시작(SOAP 모드): Java API를 사용하여 리소스 쓰기](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-writing-a-resource-using-the-java-api).)

저장소 API는 저장소에서 정보를 저장하고 검색하는 데 사용할 수 있는 여러 작업을 제공합니다. 예를 들어, 리소스 목록을 가져오거나 응용 프로그램 처리의 일부로 리소스가 필요할 때 저장소에 저장된 특정 리소스를 검색할 수 있습니다.

>[!NOTE]
>
>저장소 API를 사용하여 콘텐츠 서비스와 상호 작용할 수 없습니다(더 이상 사용되지 않음). 컨텐츠 서비스(사용 중지)와 상호 작용하려면 Document Management API를 사용합니다.

저장소 서비스 API를 사용하여 다음 작업을 수행할 수 있습니다.

* 폴더 만들기. 다음을 참조하십시오 [폴더 만들기](aem-forms-repository.md#creating-folders).
* 리소스 및 해당 속성을 작성합니다. 다음을 참조하십시오 [리소스 쓰기](aem-forms-repository.md#writing-resources).
* 주어진 컬렉션이나 다른 리소스와 관련된 리소스를 나열합니다. 다음을 참조하십시오 [리소스 나열](aem-forms-repository.md#listing-resources).
* 리소스 및 해당 속성을 읽습니다. 다음을 참조하십시오 [리소스 읽기](aem-forms-repository.md#reading-resources).
* 리소스 및 해당 속성을 업데이트합니다. 다음을 참조하십시오 [리소스 업데이트](aem-forms-repository.md#updating-resources).
* 내역, 관련 리소스 및 속성을 포함한 리소스를 검색합니다. 다음을 참조하십시오 [리소스 검색](aem-forms-repository.md#searching-for-resources).
* 리소스 간의 관계를 지정합니다. 다음을 참조하십시오 [리소스 관계 만들기](aem-forms-repository.md#creating-resource-relationships).
* 리소스 잠금 및 잠금 해제, ACL(액세스 제어 목록) 읽기 및 쓰기를 포함하여 리소스 액세스 제어를 관리합니다. 다음을 참조하십시오 [리소스 잠금](aem-forms-repository.md#locking-resources).
* 리소스 및 해당 속성을 삭제합니다. 다음을 참조하십시오 [리소스 삭제](aem-forms-repository.md#deleting-resources).

>[!NOTE]
>
>저장소 API를 사용하면 ECM 저장소를 사용하여 리소스 액세스 제어를 관리하거나 리소스를 검색하거나 리소스 관계를 지정할 수 없습니다.

>[!NOTE]
>
>암호화된 PDF이 저장소에 기록되면 자동화된 관계 추출 기능을 사용할 수 없습니다. 그렇지 않으면 암호화된 PDF을 저장소에 저장하고 나중에 검색할 수 있습니다. 검색자는 저장소에서 검색한 후 PDF의 암호를 해독하도록 선택할 수 있습니다.

>[!NOTE]
>
>저장소 서비스에 대한 자세한 내용은 [AEM Forms에 대한 서비스 참조](https://www.adobe.com/go/learn_aemforms_services_63).

## 폴더 만들기 {#creating-folders}

폴더(리소스 컬렉션)는 개체(파일 또는 리소스)를 구성된 그룹화에 저장하는 데 사용됩니다. 폴더에는 리소스와 하위 폴더라고도 하는 기타 폴더가 포함될 수 있습니다. 리소스는 한 번에 하나의 폴더에만 저장할 수 있습니다.

파일은 폴더에서 ACL(액세스 제어 목록)을 상속하고 하위 폴더는 상위 폴더에서 ACL을 상속합니다. 따라서 하위 폴더를 만들려면 먼저 상위 폴더가 있어야 합니다. IDE를 사용하면 파일별로 상호 작용하지 않고 폴더별로 상호 작용할 수 있습니다. 폴더의 버전을 지정할 수 없으며, 폴더에 데이터 자체가 포함되어 있지 않으므로 그렇게 할 필요가 없습니다. 오히려 데이터가 포함된 리소스의 컨테이너일 뿐입니다. 기본 ACL은 시스템 수준 권한입니다. 즉, 다른 사용자가 특정 폴더에 대한 권한을 부여할 때까지 사용자에게 시스템 수준 권한(읽기, 쓰기, 트래버스, ACL 관리)이 있어야 합니다. ACL은 IDE에서만 작동합니다.

>[!NOTE]
>
>저장소 서비스에 대한 자세한 내용은 [AEM Forms에 대한 서비스 참조](https://www.adobe.com/go/learn_aemforms_services_63).

### 단계 요약 {#summary-of-steps}

폴더를 만들려면 다음 단계를 수행합니다.

1. 프로젝트 파일을 포함합니다.
1. 서비스 클라이언트를 만듭니다.
1. 폴더를 만듭니다.
1. 저장소에 폴더를 작성합니다.

**프로젝트 파일 포함**

개발 프로젝트에 필요한 파일을 포함합니다. Java를 사용하여 클라이언트 응용 프로그램을 만드는 경우 필요한 JAR 파일을 포함합니다. 웹 서비스를 사용하는 경우 프록시 파일을 포함합니다.

**서비스 클라이언트 만들기**

프로그래밍 방식으로 리소스 컬렉션을 만들려면 먼저 연결을 설정하고 자격 증명을 제공해야 합니다. 이 작업은 서비스 클라이언트를 작성하여 수행할 수 있습니다.

**폴더 만들기**

저장소 서비스 메서드를 호출하여 리소스 컬렉션을 만들고 리소스 컬렉션을 해당 UUID, 폴더 이름 및 설명을 포함한 식별 정보로 채웁니다.

**저장소에 폴더 쓰기**

저장소 서비스 메서드를 호출하여 대상 폴더의 URI를 지정하여 리소스 컬렉션을 기록합니다.

**추가 참조**

[Java API를 사용하여 폴더 만들기](aem-forms-repository.md#create-folders-using-the-java-api)

[웹 서비스 API를 사용하여 폴더 만들기](aem-forms-repository.md#create-folders-using-the-web-service-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[저장소 서비스 API 빠른 시작](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### Java API를 사용하여 폴더 만들기 {#create-folders-using-the-java-api}

저장소 서비스 API(Java)를 사용하여 폴더를 만듭니다.

1. 프로젝트 파일 포함

   Java 프로젝트의 클래스 경로에 프로젝트 파일을 포함합니다.

1. 서비스 클라이언트 만들기

   만들기 `ResourceRepositoryClient` 개체를 생성자를 사용하고 `ServiceClientFactory` 연결 속성을 포함하는 개체입니다.

1. 폴더 만들기

   리소스 컬렉션을 만들려면 먼저 `com.adobe.repository.infomodel.bean.RepositoryInfomodelFactoryBean` 개체.

   호출 `repositoryInfomodelFactoryBean` 개체 `newResourceCollection` 메서드를 호출하고 다음 매개 변수를 전달합니다.

   * A `com.adobe.repository.infomodel.Id` 리소스에 할당할 UUID 식별자입니다.
   * A `com.adobe.repository.infomodel.Lid` 리소스에 할당할 UUID 식별자입니다.
   * A `java.lang.String` 리소스 컬렉션의 이름을 포함합니다. (예: `FormsFolder`)

   이 메서드는 `com.adobe.repository.infomodel.bean.ResourceCollection` 새 폴더를 나타내는 개체입니다.

   다음을 사용하여 폴더의 설명 설정 `setDescription` 메서드를 호출하고 다음 매개 변수를 전달합니다.

   * A `String` 리소스 컬렉션을 설명합니다. 이 예에서는 `"test Folder"`가 사용되었습니다 `.`


1. 저장소에 폴더 쓰기

   호출 `ResourceRepositoryClient` 개체 `writeResource` 폴더 및 의 URI에 메서드 및 를 전달합니다. `ResourceCollection` 개체. 예를 들어 폴더에 대한 URI는 다음 값일 수 있습니다 `/Applications/FormsApplication/1.0/`.

   메서드는 새로 만든 의 인스턴스를 반환합니다 `com.adobe.repository.infomodel.bean.Resource` 개체. 예를 들어 를 호출하여 새 리소스의 식별자 값을 검색할 수 있습니다 `com.adobe.repository.infomodel.bean.Resource` 개체 `getId` 메서드를 사용합니다.

**추가 참조**

[폴더 만들기](aem-forms-repository.md#creating-folders)

[빠른 시작(SOAP 모드): Java API를 사용하여 폴더 만들기](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-creating-a-folder-using-the-java-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 웹 서비스 API를 사용하여 폴더 만들기 {#create-folders-using-the-web-service-api}

저장소 서비스 API(웹 서비스)를 사용하여 폴더를 만듭니다.

1. 프로젝트 파일 포함

   * base64를 사용하여 저장소 WSDL을 사용하는 Microsoft .NET 클라이언트 어셈블리를 만듭니다.
   * Microsoft .NET 클라이언트 어셈블리를 참조합니다.

1. 서비스 클라이언트 만들기

   Microsoft .NET 클라이언트 어셈블리를 사용하여 `RepositoryServiceService` 기본 생성자를 호출하여 개체를 작성합니다. 설정 `Credentials` 를 사용하는 속성 `System.Net.NetworkCredential` 사용자 이름과 암호가 포함된 개체입니다.

1. 폴더 만들기

   에 대한 기본 생성자를 사용하여 폴더를 만듭니다. `ResourceCollection` 클래스에서 를 만들고 다음 매개 변수를 전달합니다.

   * An `Id` 개체의 기본 생성자를 호출하여 `Id` 클래스 및 할당됨 `Resource` 개체 `id` 필드.
   * An `Lid` 개체의 기본 생성자를 호출하여 `Lid` 클래스 및 할당됨 `Resource` 개체 `lid` 필드.
   * 에 할당된 리소스 컬렉션의 이름을 포함하는 문자열 `Resource` 개체 `name` 필드. 이 예제에 사용된 이름은 다음과 같습니다. `"testfolder"`.
   * 에 할당된 리소스 컬렉션에 대한 설명이 포함된 문자열 `Resource` 개체 `description` 필드. 이 예제에 사용된 설명은 다음과 같습니다. `"test folder"`.

1. 저장소에 폴더 쓰기

   호출 `RepositoryServiceService` 개체 `writeResource` 메서드, 다음 매개 변수를 전달하십시오.

   * 폴더를 만들 경로입니다.
   * 다음 `ResourceCollection` 폴더를 나타내는 개체입니다.
   * 합격 `null` 다른 두 매개 변수.

**추가 참조**

[폴더 만들기](aem-forms-repository.md#creating-folders)

[Base64 인코딩을 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

## 리소스 쓰기 {#writing-resources}

저장소의 특정 위치에 리소스를 만들 수 있습니다. 기본 파일 크기에는 데이터베이스 제한 및 세션 시간 초과가 적용됩니다. 기본 구성의 경우 파일은 25MB로 제한됩니다. 최대 파일 크기를 늘리거나 줄이려면 데이터베이스 구성을 변경해야 합니다.

리소스를 작성하는 것은 저장소에 데이터를 저장하는 것과 같습니다. 저장소에 리소스를 만들면 저장소 생태계의 모든 클라이언트가 해당 리소스에 액세스할 수 있습니다. XML 스키마, XDP 파일 및 XSD 파일과 같은 리소스를 저장소에 쓸 때 콘텐츠는 MIME 유형을 기반으로 구문 분석됩니다. MIME 유형이 지원되는 경우 파서는 다른 콘텐츠에 대해 암시적 관계가 있는지 확인합니다. 예를 들어 CSS(계단식 스타일 시트)에 공통 CSS를 참조하는 상대 URL이 있는 경우 공통 CSS도 리포지토리에 제출해야 합니다. 두 리소스 간의 관계는 30일의 조정 불가능한 기간 동안 보류 관계로 저장됩니다. 30일 기간 내에 공통 CSS를 저장소에 제출하면 관계가 형성됩니다.

리소스를 만들 때 ACL(액세스 제어 목록)은 상위 폴더에서 상속됩니다. 루트 폴더에는 초기 리소스 또는 폴더가 생성될 때까지 시스템 수준 권한이 있으며, 이 때 리소스 또는 폴더에 기본 ACL 권한이 부여됩니다.

저장소 서비스 Java API 또는 웹 서비스 API를 사용하여 프로그래밍 방식으로 리소스를 작성할 수 있습니다.

>[!NOTE]
>
>저장소 서비스에 대한 자세한 내용은 [AEM Forms에 대한 서비스 참조](https://www.adobe.com/go/learn_aemforms_services_63).

### 단계 요약 {#summary_of_steps-1}

리소스를 작성하려면 다음 단계를 수행합니다.

1. 프로젝트 파일을 포함합니다.
1. 저장소 서비스 클라이언트를 만듭니다.
1. 읽을 리소스의 URI를 지정합니다.
1. 리소스를 읽습니다.

**프로젝트 파일 포함**

개발 프로젝트에 필요한 파일을 포함합니다. Java를 사용하여 클라이언트 응용 프로그램을 만드는 경우 필요한 JAR 파일을 포함합니다. 웹 서비스를 사용하는 경우 프록시 파일을 포함합니다.

**서비스 클라이언트 만들기**

리소스를 프로그래밍 방식으로 읽으려면 먼저 연결을 설정하고 자격 증명을 제공해야 합니다. 이 작업은 서비스 클라이언트를 작성하여 수행할 수 있습니다.

**리소스에 대한 대상 폴더의 URI를 지정합니다.**

읽을 리소스의 URI를 포함하는 문자열을 만듭니다. 구문에는 다음 예제와 같이 슬래시가 포함됩니다. &quot;/*경로*/*폴더*&quot;.

**리소스 만들기**

저장소 서비스 메서드를 호출하여 리소스를 생성하고 리소스를 해당 UUID, 리소스 이름 및 설명을 포함한 식별 정보로 채웁니다.

**리소스 콘텐츠 지정**

저장소 서비스 메서드를 호출하여 리소스 콘텐츠를 만들고 해당 콘텐츠를 리소스에 저장합니다.

**대상 폴더에 리소스 쓰기**

저장소 서비스 메서드를 호출하여 리소스를 쓰고 대상 폴더의 URI를 지정합니다.

**추가 참조**

[Java API를 사용하여 리소스 쓰기](aem-forms-repository.md#write-resources-using-the-java-api)

[웹 서비스 API를 사용하여 리소스 쓰기](aem-forms-repository.md#write-resources-using-the-web-service-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[저장소 서비스 API 빠른 시작](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### Java API를 사용하여 리소스 쓰기 {#write-resources-using-the-java-api}

저장소 서비스 API(Java)를 사용하여 리소스를 작성합니다.

1. 프로젝트 파일 포함

   Java 프로젝트의 클래스 경로에 클라이언트 JAR 파일을 포함합니다.

1. 서비스 클라이언트 만들기

   만들기 `ResourceRepositoryClient` 개체를 생성자를 사용하고 `ServiceClientFactory` 연결 속성을 포함하는 개체입니다.

1. 리소스에 대한 대상 폴더의 URI를 지정합니다.

   리소스에 대한 대상 폴더의 URI를 지정합니다. 이 경우, 리소스가 `testResource` 이(가) 다음 폴더에 저장됩니다. `testFolder`, 폴더의 URI는 입니다. `"/testFolder"`. URI는 `java.lang.String` 개체.

1. 리소스 만들기

   리소스를 만들려면 먼저 `com.adobe.repository.infomodel.bean.RepositoryInfomodelFactoryBean` 개체.

   호출 `RepositoryInfomodelFactoryBean` 개체 `newResource` 메서드, `com.adobe.repository.infomodel.bean.Resource` 개체. 이 예에서는 다음 매개 변수가 제공됩니다.

   * A `com.adobe.repository.infomodel.Id` 개체의 기본 생성자를 호출하여 `Id` 클래스.
   * A `com.adobe.repository.infomodel.Lid` 개체의 기본 생성자를 호출하여 `Lid` 클래스.
   * A `java.lang.String` 리소스의 파일 이름을 포함합니다.

   리소스의 설명을 지정하려면 를 호출합니다 `Resource` 개체 `setDescription` 메서드, 설명이 포함된 문자열 전달 이 예에서 설명은 다음과 같습니다. `"test resource"`.

1. 리소스 콘텐츠 지정

   리소스에 대한 콘텐츠를 만들려면 `RepositoryInfomodelFactoryBean` 개체 `newResourceContent` 메서드, 반환 `com.adobe.repository.infomodel.bean.ResourceContent` 개체. 에 콘텐츠 추가 `ResourceContent` 개체. 이 예에서는 다음 작업을 수행하여 이 작업을 수행합니다.

   * 호출 `ResourceContent` 개체 `setDataDocument` 메서드 및 전달에 `com.adobe.idp.Document` 오브젝트
   * 호출 `ResourceContent` 개체 `setSize` 메서드 및 크기(바이트) `Document` 오브젝트

   를 호출하여 콘텐츠를 리소스에 추가합니다. `Resource` 개체 `setContent` 메서드 및 전달 `ResourceContent` 개체. 자세한 내용은 [AEM Forms API 참조](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

1. 대상 폴더에 리소스 쓰기

   호출 `ResourceRepositoryClient` 개체 `writeResource` 폴더의 URI와 `Resource` 개체.

**추가 참조**

[리소스 쓰기](aem-forms-repository.md#writing-resources)

[빠른 시작(SOAP 모드): Java API를 사용하여 리소스 쓰기](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-writing-a-resource-using-the-java-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 웹 서비스 API를 사용하여 리소스 쓰기 {#write-resources-using-the-web-service-api}

저장소 서비스 API(웹 서비스)를 사용하여 리소스를 작성합니다.

1. 프로젝트 파일 포함

   * base64를 사용하여 저장소 WSDL을 사용하는 Microsoft .NET 클라이언트 어셈블리를 만듭니다.
   * Microsoft .NET 클라이언트 어셈블리를 참조합니다.

1. 서비스 클라이언트 만들기

   Microsoft .NET 클라이언트 어셈블리를 사용하여 `RepositoryServiceService` 기본 생성자를 호출하여 개체를 작성합니다. 설정 `Credentials` 를 사용하는 속성 `System.Net.NetworkCredential` 사용자 이름과 암호가 포함된 개체입니다.

1. 리소스에 대한 대상 폴더의 URI를 지정합니다.

   리소스에 대한 대상 폴더의 URI를 지정합니다. 이 경우, 리소스가 `testResource` 이(가) 다음 폴더에 저장됩니다. `testFolder`, 폴더의 URI는 입니다. `"/testFolder"`. Microsoft .NET Framework와 호환되는 언어(예: C#)를 사용하는 경우 URI를 `System.String` 개체.

1. 리소스 만들기

   리소스를 만들려면 의 기본 생성자를 호출합니다 `Resource` 클래스. 이 예제에서 다음 정보는 `Resource` 개체:

   * A `com.adobe.repository.infomodel.Id` 개체의 기본 생성자를 호출하여 `Id` 클래스 및 할당됨 `Resource` 개체 `id` 필드.
   * A `com.adobe.repository.infomodel.Lid` 개체의 기본 생성자를 호출하여 `Lid` 클래스 및 할당됨 `Resource` 개체 `lid` 필드.
   * 리소스에 할당된 리소스의 파일 이름을 포함하는 문자열 `Resource` 개체 `name` 필드. 이 예제에 사용된 이름은 다음과 같습니다. `"testResource"`.
   * 에 할당된 리소스에 대한 설명이 포함된 문자열 `Resource` 개체 `description` 필드. 이 예제에 사용된 설명은 다음과 같습니다. `"test resource"`.

1. 리소스 콘텐츠 지정

   리소스에 대한 콘텐츠를 만들려면 `ResourceContent` 클래스. 그런 다음 컨텐츠를 `ResourceContent` 개체. 이 예에서는 다음 작업을 수행하여 이 작업을 수행합니다.

   * 할당 `BLOB` 에 대한 문서가 포함된 개체 `ResourceContent` 개체 `dataDocument` 필드.
   * 크기 할당(바이트) `BLOB` 에 대한 오브젝트 `ResourceContent` 개체 `size` 필드.

   을(를) 할당하여 콘텐츠를 리소스에 추가합니다. `ResourceContent` 에 대한 오브젝트 `Resource` 개체 `content` 필드.

1. 대상 폴더에 리소스 쓰기

   호출 `RepositoryServiceService` 개체 `writeResource` 폴더의 URI와 `Resource` 개체. 합격 `null` 다른 두 매개 변수.

**추가 참조**

[리소스 쓰기](aem-forms-repository.md#writing-resources)

[Base64 인코딩을 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

## 리소스 나열 {#listing-resources}

리소스를 나열하여 리소스를 검색할 수 있습니다. 지정된 리소스 컬렉션과 관련된 모든 리소스를 찾기 위해 저장소에 대해 쿼리가 수행됩니다.

리소스를 구성하고 나면 운영 체제에서 수행하는 것처럼 구조의 특정 분기를 확인하여 만든 구조를 검사할 수 있습니다.

리소스 목록은 관계별로 작동합니다. 리소스는 폴더의 멤버입니다. 멤버십은 &quot;member of&quot; 유형의 관계로 표시됩니다. 주어진 폴더에 있는 리소스를 나열할 때 &quot;member of&quot; 관계를 통해 주어진 폴더와 관련된 리소스를 쿼리합니다. 관계는 방향입니다. 관계의 멤버에는 타겟의 멤버인 소스가 있습니다. 소스는 리소스이고 대상은 상위 폴더입니다.

>[!NOTE]
>
>저장소 서비스에 대한 자세한 내용은 [AEM Forms에 대한 서비스 참조](https://www.adobe.com/go/learn_aemforms_services_63).

### 단계 요약 {#summary_of_steps-2}

리소스를 나열하려면 다음 단계를 수행합니다.

1. 프로젝트 파일을 포함합니다.
1. 서비스 클라이언트를 만듭니다.
1. 폴더 경로를 지정합니다.
1. 리소스 목록을 검색합니다.

**프로젝트 파일 포함**

개발 프로젝트에 필요한 파일을 포함합니다. Java를 사용하여 클라이언트 응용 프로그램을 만드는 경우 필요한 JAR 파일을 포함합니다. 웹 서비스를 사용하는 경우 프록시 파일을 포함합니다.

**서비스 클라이언트 만들기**

프로그래밍 방식으로 리소스 컬렉션을 만들려면 먼저 연결을 설정하고 자격 증명을 제공해야 합니다. 이 작업은 서비스 클라이언트를 작성하여 수행할 수 있습니다.

**폴더 경로 지정**

리소스가 포함된 폴더의 경로를 포함하는 문자열을 만듭니다. 구문에는 다음 예제와 같이 슬래시가 포함됩니다. &quot;/*경로*/*폴더*&quot;.

**리소스 목록 검색**

저장소 서비스 메서드를 호출하여 리소스 목록을 검색하고 대상 폴더의 경로를 지정합니다.

**추가 참조**

[Java API를 사용하여 리소스 나열](aem-forms-repository.md#list-resources-using-the-java-api)

[웹 서비스 API를 사용하여 리소스 나열](aem-forms-repository.md#list-resources-using-the-web-service-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[저장소 서비스 API 빠른 시작](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### Java API를 사용하여 리소스 나열 {#list-resources-using-the-java-api}

저장소 서비스 API(Java)를 사용하여 리소스 나열:

1. 프로젝트 파일 포함

   Java 프로젝트의 클래스 경로에 클라이언트 JAR 파일을 포함합니다.

1. 서비스 클라이언트 만들기

   만들기 `ResourceRepositoryClient` 개체를 생성자를 사용하고 `ServiceClientFactory` 연결 속성을 포함하는 개체입니다.

1. 폴더 경로 지정

   쿼리할 리소스 컬렉션의 URI를 지정하십시오. 이 경우 해당 URI는 `"/testFolder"`. URI는 `java.lang.String` 개체.

1. 리소스 목록 검색

   호출 `ResourceRepositoryClient` 개체 `listMembers` 폴더의 URI에 메서드 및 를 전달합니다.

   이 메서드는 `java.util.List` / `com.adobe.repository.infomodel.bean.Resource` 의 소스인 오브젝트 `com.adobe.repository.infomodel.bean.Relation` 유형 `Relation.TYPE_MEMBER_OF` 리소스 컬렉션 URI를 대상으로 사용합니다. 이 과정을 반복할 수 있습니다 `List` 을 클릭하여 각 리소스를 검색합니다. 이 예제에서는 각 리소스의 이름과 설명을 표시합니다.

**추가 참조**

[리소스 나열](aem-forms-repository.md#listing-resources).

[빠른 시작(SOAP 모드): Java API를 사용하여 리소스 나열](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-listing-resources-using-the-java-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 웹 서비스 API를 사용하여 리소스 나열 {#list-resources-using-the-web-service-api}

저장소 서비스 API(웹 서비스)를 사용하여 리소스 나열:

1. 프로젝트 파일 포함

   * 저장소 WSDL을 사용하는 Microsoft .NET 클라이언트 어셈블리를 만듭니다.
   * Microsoft .NET 클라이언트 어셈블리를 참조합니다.

1. 서비스 클라이언트 만들기

   Microsoft .NET 클라이언트 어셈블리를 사용하여 `RepositoryServiceService` 기본 생성자를 호출하여 개체를 작성합니다. 설정 `Credentials` 를 사용하는 속성 `System.Net.NetworkCredential` 사용자 이름과 암호가 포함된 개체입니다.

1. 폴더 경로 지정

   쿼리할 폴더의 URI가 포함된 문자열을 지정합니다. 이 경우 해당 URI는 `"/testFolder"`. Microsoft .NET Framework와 호환되는 언어(예: C#)를 사용하는 경우 URI를 `System.String` 개체.

1. 리소스 목록 검색

   호출 `RepositoryServiceService` 개체 `listMembers` 첫 번째 매개 변수로 폴더의 URI에 를 전달합니다. 합격 `null` 다른 두 매개 변수.

   이 메서드는 캐스팅할 수 있는 개체 배열을 반환합니다. `Resource` 개체. 객체 배열을 반복하여 관련된 각 리소스를 검색할 수 있습니다. 이 예제에서는 각 리소스의 이름과 설명을 표시합니다.

**추가 참조**

[리소스 나열](aem-forms-repository.md#listing-resources).

[Base64 인코딩을 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

## 리소스 읽기 {#reading-resources}

저장소의 특정 위치에서 리소스를 검색하여 해당 콘텐츠 및 메타데이터를 읽을 수 있습니다. 워크플로우가 초기화 양식에 의해 프론트엔딩됩니다. 프로세스에는 양식을 읽는 데 필요한 모든 권한이 있습니다. 시스템은 데이터 양식을 검색하고 저장소에서 컨텐츠를 읽습니다. 저장소는 콘텐츠 및 메타데이터에 대한 액세스 권한을 부여합니다(리소스가 존재하는지 조차 알 수 있음).

저장소에는 다음과 같은 네 가지 권한 유형이 있습니다.

* **횡단**: 리소스를 나열할 수 있습니다. 즉, 리소스 메타데이터를 읽을 수 있지만 리소스 콘텐츠는 읽을 수 없습니다
* **읽기**: 리소스 콘텐츠를 읽을 수 있도록 해줍니다
* **쓰기**: 리소스 컨텐츠를 쓸 수 있습니다.
* **acl(액세스 제어 목록) 관리**: 리소스에서 ACL을 조작할 수 있습니다

사용자는 프로세스를 실행할 권한이 있을 때만 프로세스를 실행할 수 있습니다. IDE 사용자는 저장소와 동기화하려면 트래버스 및 읽기 권한이 필요합니다. 런타임이 시스템 컨텍스트 내에서 발생하므로 ACL은 디자인 타임에만 적용됩니다.

저장소 서비스 Java API 또는 웹 서비스 API를 사용하여 프로그래밍 방식으로 리소스를 읽을 수 있습니다.

>[!NOTE]
>
>저장소 서비스에 대한 자세한 내용은 [AEM Forms에 대한 서비스 참조](https://www.adobe.com/go/learn_aemforms_services_63).

### 단계 요약 {#summary_of_steps-3}

리소스를 읽으려면 다음 단계를 수행합니다.

1. 프로젝트 파일을 포함합니다.
1. 저장소 서비스 클라이언트를 만듭니다.
1. 읽을 리소스의 URI를 지정합니다.
1. 리소스를 읽습니다.

**프로젝트 파일 포함**

개발 프로젝트에 필요한 파일을 포함합니다. Java를 사용하여 클라이언트 응용 프로그램을 만드는 경우 필요한 JAR 파일을 포함합니다. 웹 서비스를 사용하는 경우 프록시 파일을 포함합니다.

**서비스 클라이언트 만들기**

리소스를 프로그래밍 방식으로 읽으려면 먼저 연결을 설정하고 자격 증명을 제공해야 합니다. 이 작업은 서비스 클라이언트를 작성하여 수행할 수 있습니다.

**읽을 리소스의 URI를 지정하십시오.**

읽을 리소스의 URI를 포함하는 문자열을 만듭니다. 구문에는 다음 예제와 같이 슬래시가 포함됩니다. &quot;/*경로*/*리소스*&quot;.

**리소스 읽기**

리소스를 읽을 저장소 서비스 메서드를 호출하고 URI를 지정합니다.

**추가 참조**

[Java API를 사용하여 리소스 읽기](aem-forms-repository.md#read-resources-using-the-java-api)

[웹 서비스 API를 사용하여 리소스 읽기](aem-forms-repository.md#reading-resources-using-the-web-service-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[저장소 서비스 API 빠른 시작](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### Java API를 사용하여 리소스 읽기 {#read-resources-using-the-java-api}

저장소 서비스 API(Java)를 사용하여 리소스를 읽습니다.

1. 프로젝트 파일 포함

   Java 프로젝트의 클래스 경로에 클라이언트 JAR 파일을 포함합니다.

1. 서비스 클라이언트 만들기

   만들기 `ResourceRepositoryClient` 개체를 생성자를 사용하고 `ServiceClientFactory` 연결 속성을 포함하는 개체입니다.

1. 읽을 리소스의 URI를 지정하십시오.

   검색할 리소스의 URI를 나타내는 문자열 값을 지정합니다. 예를 들어 리소스의 이름이 이라고 가정하면 *testResource* 폴더에 있음: *testFolder*, 지정 `/testFolder/testResource`.

1. 리소스 읽기

   호출 `ResourceRepositoryClient` 개체 `readResource` 메서드에서 리소스의 URI를 매개 변수로 전달합니다. 이 메서드는 `Resource` 리소스를 나타내는 인스턴스입니다.

**추가 참조**

[리소스 읽기](aem-forms-repository.md#reading-resources)

[빠른 시작(SOAP 모드): Java API를 사용하여 리소스 읽기](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-reading-a-resource-using-the-java-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 웹 서비스 API를 사용하여 리소스 읽기 {#reading-resources-using-the-web-service-api}

저장소 서비스 API(웹 서비스)를 사용하여 리소스를 읽습니다.

1. 프로젝트 파일 포함

   * 저장소 WSDL을 사용하는 Microsoft .NET 클라이언트 어셈블리를 만듭니다. (참조: [Base64 인코딩을 사용하는 .NET 클라이언트 어셈블리 만들기](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding).)
   * Microsoft .NET 클라이언트 어셈블리를 참조합니다. (참조: [Base64 인코딩을 사용하는 .NET 클라이언트 어셈블리 만들기](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding).)

1. 서비스 클라이언트 만들기

   Microsoft .NET 클라이언트 어셈블리를 사용하여 `RepositoryServiceService` 기본 생성자를 호출하여 개체를 작성합니다. 설정 `Credentials` 를 사용하는 속성 `System.Net.NetworkCredential` 사용자 이름과 암호가 포함된 개체입니다.

1. 읽을 리소스의 URI를 지정하십시오.

   검색할 리소스의 URI를 포함하는 문자열을 지정합니다. 이 경우, 리소스가 `testResource` 이(가) 다음 폴더에 있음: `testFolder`, 해당 URI는 `"/testFolder/testResource"`. Microsoft .NET Framework와 호환되는 언어(예: C#)를 사용하는 경우 URI를 `System.String` 개체.

1. 리소스 읽기

   호출 `RepositoryServiceService` 개체 `readResource` 첫 번째 매개 변수로 리소스의 URI를 전달합니다. 합격 `null` 다른 두 매개 변수.

**추가 참조**

[리소스 읽기](aem-forms-repository.md#reading-resources)

[Base64 인코딩을 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

## 리소스 업데이트 {#updating-resources}

저장소에서 리소스의 콘텐츠를 검색하고 업데이트할 수 있습니다. 리소스를 업데이트할 때 해당 리소스에 대한 액세스 제어는 버전 간에 변경되지 않습니다. 업데이트를 수행할 때 주요 버전을 늘릴 수 있는 옵션이 있습니다. 주 버전 증가를 선택하지 않으면 부 버전이 자동으로 업데이트됩니다.

리소스를 업데이트할 때 지정된 리소스 속성을 기반으로 새 버전이 만들어집니다. 리소스를 업데이트할 때 두 개의 중요한 매개 변수인 대상 URI와 업데이트된 모든 메타데이터가 포함된 리소스 인스턴스를 지정합니다. 지정된 속성(예: 이름)을 변경하지 않는 경우 전달하는 인스턴스에서 속성이 계속 필요합니다. 콘텐츠를 구문 분석할 때 만들어지는 관계는 특정 버전에 추가되며 지정하지 않는 한 전달되지 않습니다.

예를 들어 XDP 파일을 업데이트하고 다른 리소스에 대한 참조가 포함된 경우 이러한 추가 참조도 기록됩니다. form.xdp 버전 1.0에 로고와 스타일 시트, 이렇게 두 개의 외부 참조가 있고, 그 다음 form.xdp를 업데이트하여 이제 로고, 스타일 시트 및 스키마 파일, 이렇게 세 개의 참조가 있다고 가정해 봅시다. 업데이트 중에 저장소는 보류 중인 관계 테이블에 세 번째 관계(스키마 파일에 대한)를 추가합니다. 스키마 파일이 저장소에 있으면 관계가 자동으로 형성됩니다. 그러나 form.xdp 버전 2.0에서 더 이상 로고를 사용하지 않는 경우 form.xdp 버전 2.0은 로고와 관계가 없습니다.

모든 업데이트 작업은 원자적이며 트랜잭션 방식입니다. 예를 들어 두 명의 사용자가 동일한 리소스를 읽고 둘 다 버전 1.0을 버전 2.0으로 업데이트하기로 결정하면 둘 중 하나는 성공하고 둘 중 하나는 실패하며 저장소의 무결성은 유지되고 둘 다 성공 또는 실패를 확인하는 메시지를 받게 됩니다. 트랜잭션이 커밋되지 않으면 데이터베이스 오류가 발생한 경우 롤백되며 애플리케이션 서버에 따라 시간 초과되거나 롤백됩니다.

저장소 서비스 Java API 또는 웹 서비스 API를 사용하여 리소스를 프로그래밍 방식으로 업데이트할 수 있습니다.

>[!NOTE]
>
>저장소 서비스에 대한 자세한 내용은 [AEM Forms에 대한 서비스 참조](https://www.adobe.com/go/learn_aemforms_services_63).

### 단계 요약 {#summary_of_steps-4}

리소스를 업데이트하려면 다음 단계를 수행합니다.

1. 프로젝트 파일을 포함합니다.
1. 저장소 서비스 클라이언트를 만듭니다.
1. 업데이트할 리소스를 검색합니다.
1. 리소스를 업데이트합니다.

**프로젝트 파일 포함**

개발 프로젝트에 필요한 파일을 포함합니다. Java를 사용하여 클라이언트 응용 프로그램을 만드는 경우 필요한 JAR 파일을 포함합니다. 웹 서비스를 사용하는 경우 프록시 파일을 포함합니다.

**서비스 클라이언트 만들기**

리소스를 프로그래밍 방식으로 읽으려면 먼저 연결을 설정하고 자격 증명을 제공해야 합니다. 이 작업은 서비스 클라이언트를 작성하여 수행할 수 있습니다.

**업데이트할 리소스 검색**

리소스를 읽습니다. 자세한 내용은 [리소스 읽기](aem-forms-repository.md#reading-resources).

**리소스 업데이트**

리소스에서 새 정보를 설정하고 Repository Service 메서드를 호출하여 리소스를 업데이트하고, URI, 업데이트된 리소스 및 버전 정보를 업데이트하는 방법을 지정합니다.

**추가 참조**

[Java API를 사용하여 리소스 업데이트](aem-forms-repository.md#update-resources-using-the-java-api)

[웹 서비스 API를 사용하여 리소스 업데이트](aem-forms-repository.md#update-resources-using-the-web-service-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[저장소 서비스 API 빠른 시작](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### Java API를 사용하여 리소스 업데이트 {#update-resources-using-the-java-api}

저장소 서비스 API(Java)를 사용하여 리소스를 업데이트합니다.

1. 프로젝트 파일 포함

   Java 프로젝트의 클래스 경로에 클라이언트 JAR 파일을 포함합니다.

1. 서비스 클라이언트 만들기

   만들기 `ResourceRepositoryClient` 개체를 생성자를 사용하고 `ServiceClientFactory` 연결 속성을 포함하는 개체입니다.

1. 업데이트할 리소스 검색

   리소스를 검색하고 읽을 리소스의 URI를 지정합니다. 이 예에서 리소스의 URI는 입니다. `"/testFolder/testResource"`.

1. 리소스 업데이트

   업데이트 `Resource` 개체 정보. 이 예에서 설명을 업데이트하려면 `Resource` 개체 `setDescription` 메서드, 새 설명 문자열을 매개 변수로 전달합니다.

   그런 다음 를 호출합니다 `ServiceClientFactory` 개체 `updateResource` 메서드를 호출하고 다음 매개 변수를 전달합니다.

   * A `java.lang.String` 리소스의 URI가 포함된 개체입니다.
   * 다음 `Resource` 업데이트된 리소스 정보가 포함된 객체입니다.
   * A `boolean` 주 버전 또는 부 버전을 업데이트할지 여부를 나타내는 값입니다. 이 예에서 값은 `true` 는 메이저 버전이 증가함을 나타내기 위해 전달됩니다.

**추가 참조**

[리소스 업데이트](aem-forms-repository.md#updating-resources)

[빠른 시작(SOAP 모드): Java API를 사용하여 리소스 업데이트](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-updating-a-resource-using-the-java-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 웹 서비스 API를 사용하여 리소스 업데이트 {#update-resources-using-the-web-service-api}

저장소 API(웹 서비스)를 사용하여 리소스를 업데이트합니다.

1. 프로젝트 파일 포함

   * 저장소 WSDL을 사용하는 Microsoft .NET 클라이언트 어셈블리를 만듭니다.
   * Microsoft .NET 클라이언트 어셈블리를 참조합니다.

1. 서비스 클라이언트 만들기

   Microsoft .NET 클라이언트 어셈블리를 사용하여 `RepositoryServiceService` 기본 생성자를 호출하여 개체를 작성합니다. 설정 `Credentials` 를 사용하는 속성 `System.Net.NetworkCredential` 사용자 이름과 암호가 포함된 개체입니다.

1. 업데이트할 리소스 검색

   검색할 리소스의 URI를 지정하고 리소스를 읽습니다. 이 예에서 리소스의 URI는 입니다. `"/testFolder/testResource"`. 자세한 내용은 [리소스 읽기](aem-forms-repository.md#reading-resources).

1. 리소스 업데이트

   업데이트 `Resource` 개체 정보. 이 예에서 설명을 업데이트하려면 새 값을 `Resource` 개체 `description` 필드.

1. 호출 `RepositoryServiceService` 개체 `updateResource` 메서드를 호출하고 다음 매개 변수를 전달합니다.

   * A `System.String` 리소스의 URI가 포함된 개체입니다.
   * 다음 `Resource` 업데이트된 리소스 정보가 포함된 객체입니다.
   * A `boolean` 주 버전 또는 부 버전을 업데이트할지 여부를 나타내는 값입니다. 이 예에서 값은 `true` 는 메이저 버전이 증가함을 나타내기 위해 전달됩니다.
   * 합격 `null` 를 참조하십시오.

**추가 참조**

[리소스 업데이트](aem-forms-repository.md#updating-resources)

[Base64 인코딩을 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

## 리소스 검색 {#searching-for-resources}

기록, 관련 리소스, 등록 정보 등 저장소에서 리소스를 검색하는 데 사용되는 쿼리를 구성할 수 있습니다.

관련 리소스를 검색하여 양식과 해당 조각 간의 종속성을 확인할 수 있습니다. 예를 들어 양식이 있는 경우 사용할 조각이나 외부 리소스를 결정할 수 있습니다. 이미지가 있으면 해당 이미지를 사용하는 양식도 확인할 수 있습니다. 속성을 기반으로 필터링을 사용하여 관련 리소스를 검색할 수도 있습니다. 예를 들어, 지정된 이름의 이미지를 사용하는 모든 양식을 검색하거나 지정된 이름의 양식에서 사용하는 이미지를 찾을 수 있습니다. 리소스 속성을 사용하여 검색할 수도 있습니다. 예를 들어, &#39;%&#39; 및 &#39;_&#39; 와일드카드를 포함할 수 있는 지정된 문자열로 시작하는 이름을 가진 모든 양식 또는 리소스를 찾기 위해 쿼리를 수행할 수 있습니다. 속성을 기반으로 하는 검색은 관계를 기반으로 하지 않습니다. 이러한 검색은 주어진 리소스에 대한 특정 지식을 가지고 있다는 가정을 기반으로 합니다.

**쿼리 문**

A *쿼리* 조건부로 논리적으로 연결된 하나 이상의 문을 포함합니다. A *구문* 왼쪽 피연산자, 연산자 및 오른쪽 피연산자로 구성됩니다. 또한 검색 결과에 사용할 정렬 순서를 지정할 수 있습니다. 다음 *정렬 순서* SQL과 같은 정보를 포함합니다. `ORDER BY` 및 는 검색의 기반이 되는 특성과 오름차순 또는 내림차순을 사용할 것인지 여부를 나타내는 값을 포함하는 요소로 구성됩니다.

저장소 서비스 Java API를 사용하여 프로그래밍 방식으로 리소스를 검색할 수 있습니다. 현재 웹 서비스 API를 사용하여 리소스를 검색할 수 없습니다.

**정렬 동작**

을(를) 호출할 때 정렬 순서가 적용되지 않음 `ResourceRepositoryClient` 개체 `searchProperties` 메서드 및 정렬 순서 지정. 예를 들어 속성 이름이 인 세 개의 사용자 지정 속성으로 리소스를 만든다고 가정합니다. `name`, `secondName`, 및 `asecondName`. 그런 다음 속성 이름에 정렬 순서 요소를 만들고 `ascending` 값: 까지 `true`.

그런 다음 를 호출합니다 `ResourceRepositoryClient` 개체 `searchProperties` 정렬 순서에 따라 메서드 및 를 전달합니다. 다음 세 가지 속성을 갖는 올바른 리소스를 반환합니다. 그러나 속성은 속성 이름별로 정렬되지 않습니다. 추가된 순서대로 반환됩니다. `name`, `secondName`, 및 `asecondName`.

>[!NOTE]
>
>저장소 서비스에 대한 자세한 내용은 [AEM Forms에 대한 서비스 참조](https://www.adobe.com/go/learn_aemforms_services_63).

### 단계 요약 {#summary_of_steps-5}

리소스를 검색하려면 다음 단계를 수행합니다.

1. 프로젝트 파일을 포함합니다.
1. 저장소 서비스 클라이언트를 만듭니다.
1. 검색할 대상 폴더를 지정합니다.
1. 검색에 사용되는 속성을 지정합니다.
1. 검색에 사용되는 쿼리를 만듭니다.
1. 검색 결과에 대한 정렬 순서를 만듭니다.
1. 리소스를 검색합니다.
1. 검색 결과에서 리소스를 검색합니다.

**프로젝트 파일 포함**

개발 프로젝트에 필요한 파일을 포함합니다. Java를 사용하여 클라이언트 응용 프로그램을 만드는 경우 필요한 JAR 파일을 포함합니다. 웹 서비스를 사용하는 경우 프록시 파일을 포함합니다.

**서비스 클라이언트 만들기**

리소스를 프로그래밍 방식으로 읽으려면 먼저 연결을 설정하고 자격 증명을 제공해야 합니다. 이 작업은 서비스 클라이언트를 작성하여 수행할 수 있습니다.

**검색할 대상 폴더 지정**

검색을 수행할 기본 경로를 포함하는 문자열을 만듭니다. 구문에는 다음 예제와 같이 슬래시가 포함됩니다. &quot;/*경로*/*폴더*&quot;.

**검색에 사용되는 속성 지정**

리소스 내에 포함된 속성을 기준으로 검색할 수 있습니다. 검색을 수행할 속성의 값을 지정합니다.

**검색에 사용되는 쿼리 만들기**

문과 조건을 사용하여 쿼리를 구성합니다. 각 문은 검색의 기반이 되는 속성, 사용할 조건 및 검색에 사용할 속성 값을 지정합니다.

**검색 결과에 대한 정렬 순서 만들기**

정렬 순서는 각 요소에 검색에 사용되는 속성 중 하나와 오름차순 또는 내림차순 사용 여부를 나타내는 값이 포함됩니다.

**리소스 검색**

폴더, 쿼리 및 정렬 순서를 사용하여 리소스를 검색합니다. 또한 검색 깊이와 반환할 결과 수의 상한을 나타냅니다.

**검색 결과에서 리소스 검색**

반환된 리소스 목록을 반복하고 추가 처리를 위해 정보를 추출합니다.

**추가 참조**

[Java API를 사용하여 리소스 검색](aem-forms-repository.md#search-for-resources-using-the-java-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[저장소 서비스 API 빠른 시작](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### Java API를 사용하여 리소스 검색 {#search-for-resources-using-the-java-api}

저장소 서비스 API(Java)를 사용하여 리소스를 검색합니다.

1. 프로젝트 파일 포함

   Java 프로젝트의 클래스 경로에 클라이언트 JAR 파일을 포함합니다.

1. 서비스 클라이언트 만들기

   만들기 `ResourceRepositoryClient` 개체를 생성자를 사용하고 `ServiceClientFactory` 연결 속성을 포함하는 개체입니다.

1. 검색할 대상 폴더 지정

   검색을 실행할 기본 경로의 URI를 지정합니다. 이 예에서 리소스의 URI는 입니다. `/testFolder`.

1. 검색에 사용되는 속성 지정

   검색을 수행할 속성에 대한 값을 지정합니다. 속성은 다음 내에 있습니다. `com.adobe.repository.infomodel.bean.Resource` 개체. 이 예에서 검색은 이름 속성에 대해 수행됩니다. 따라서 `java.lang.String` 다음 포함 `Resource` 개체의 이름이 사용됩니다. `testResource` 이 경우.

1. 검색에 사용되는 쿼리 만들기

   쿼리를 만들려면 `com.adobe.repository.query.Query` 개체에 대한 기본 생성자를 호출하여 `Query` 클래스를 만들고 쿼리에 문을 추가합니다.

   문을 만들려면 `com.adobe.repository.query.Query.Statement` 클래스에서 를 만들고 다음 매개 변수를 전달합니다.

   * 리소스 속성 상수를 포함하는 왼쪽 피연산자입니다. 이 예제에서 리소스의 이름은 검색의 기반으로 사용되기 때문에 정적 값입니다 `Resource.ATTRIBUTE_NAME` 를 사용합니다.
   * 속성 검색에 사용되는 조건을 포함하는 연산자입니다. 연산자는 의 정적 상수 중 하나여야 합니다. `Query.Statement` 클래스. 이 예에서 정적 값은 `Query.Statement.OPERATOR_BEGINS_WITH` 를 사용합니다.
   * 검색을 수행할 속성 값을 포함하는 오른쪽 피연산자입니다. 이 예제에서 name 속성은 `String` 값 포함 `"testResource"`가 사용됩니다.

   왼쪽 피연산자의 네임스페이스를 지정하십시오. `Query.Statement` 개체 `setNamespace` 메서드에 포함된 정적 값 중 하나를 전달하는 방법 및 `com.adobe.repository.infomodel.bean.ResourceProperty` 클래스. 이 예에서는 `ResourceProperty.RESERVED_NAMESPACE_REPOSITORY`가 사용되었습니다.

   를 호출하여 쿼리에 각 문을 추가합니다. `Query` 개체 `addStatement` 메서드 및 전달 `Query.Statement` 개체.

1. 검색 결과에 대한 정렬 순서 만들기

   검색 결과에 사용되는 정렬 순서를 지정하려면 `com.adobe.repository.query.sort.SortOrder` 개체에 대한 기본 생성자를 호출하여 `SortOrder` 을 반환하고, 정렬 순서에 요소를 추가합니다.

   정렬 순서에 대한 요소를 만들려면 `com.adobe.repository.query.sort.SortOrder.Element` 클래스. 이 예제에서 리소스의 이름은 검색의 기반으로 사용되기 때문에 정적 값입니다 `Resource.ATTRIBUTE_NAME` 는 첫 번째 매개 변수로 사용되며 오름차순(a `boolean` 값 `true`)가 두 번째 매개 변수로 지정됩니다.

   를 호출하여 정렬 순서에 각 요소를 추가합니다. `SortOrder` 개체 `addSortElement` 메서드 및 전달 `SortOrder.Element` 개체.

1. 리소스 검색

   을 검색하려면 `resources` 속성 속성에 따라 `ResourceRepositoryClient` 개체 `searchProperties` 메서드, 다음 매개 변수를 전달하십시오.

   * A `String` 검색을 실행할 기본 경로를 포함합니다. 이 경우, `"/testFolder"` 를 사용합니다.
   * 검색에 사용되는 쿼리입니다.
   * 검색 깊이. 이 경우, `com.adobe.repository.infomodel.bean.ResourceCollection.DEPTH_INFINITE` 는 기본 경로와 해당 폴더를 모두 사용함을 나타내는 데 사용됩니다.
   * An `int` 페이징되지 않은 결과 세트를 선택할 첫 번째 행을 나타내는 값입니다. 이 예에서는 `0` 이(가) 지정되었습니다.
   * An `int` 반환할 최대 결과 수를 나타내는 값입니다. 이 예에서는 `10` 이(가) 지정되었습니다.
   * 검색에 사용되는 정렬 순서.

   이 메서드는 `java.util.List` / `Resource` 지정된 정렬 순서의 개체입니다.

1. 검색 결과에서 리소스 검색

   검색 결과에 포함된 리소스를 검색하려면 `List` 각 개체를 `Resource` 정보를 추출하기 위해. 이 예제에서는 각 리소스의 이름이 표시됩니다.

**추가 참조**

[리소스 검색](aem-forms-repository.md#searching-for-resources)

[빠른 시작(SOAP 모드): Java API를 사용하여 리소스 검색](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-searching-for-resources-using-the-java-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 리소스 관계 만들기 {#creating-resource-relationships}

저장소에 있는 리소스 간의 관계를 지정할 수 있습니다. 관계에는 세 가지가 있습니다.

* **의존**: 리소스가 다른 리소스에 의존하는 관계입니다. 즉, 저장소에 모든 관련 리소스가 필요합니다.
* **멤버십(파일 시스템)**: 리소스가 주어진 폴더 내에 있는 관계입니다.
* **사용자 정의**: 리소스 간에 지정하는 관계입니다. 예를 들어 한 리소스가 더 이상 사용되지 않고 다른 리소스가 저장소에 도입된 경우, 고유한 대체 관계를 지정할 수 있습니다.

자신만의 사용자 지정 관계를 만들 수 있습니다. 예를 들어, 저장소에 HTML 파일을 저장하고 이미지를 사용하는 경우 HTML 파일을 이미지와 연결할 사용자 지정 관계를 지정할 수 있습니다(일반적으로 XML 파일만 저장소 정의 종속성 관계를 사용하여 이미지와 연결되기 때문). 사용자 지정 관계의 또 다른 예는 트리 구조 대신 주기적 그래프 구조로 다른 저장소 보기를 빌드하려는 경우입니다. 뷰어와 함께 원형 그래프를 정의하여 해당 관계를 트래버스할 수 있습니다. 마지막으로, 두 리소스가 완전히 다른데도 리소스가 다른 리소스를 대체함을 나타낼 수 있습니다. 이 경우 예약된 범위를 벗어나는 관계 유형을 정의하고 이러한 두 리소스 간의 관계를 만들 수 있습니다. 응용 프로그램은 관계를 감지하고 처리할 수 있는 유일한 클라이언트이며 해당 관계를 검색하는 데 사용할 수 있습니다.

저장소 서비스 Java API 또는 웹 서비스 API를 사용하여 리소스 간의 관계를 프로그래밍 방식으로 지정할 수 있습니다.

>[!NOTE]
>
>저장소 서비스에 대한 자세한 내용은 [AEM Forms에 대한 서비스 참조](https://www.adobe.com/go/learn_aemforms_services_63).

### 단계 요약 {#summary_of_steps-6}

두 리소스 간의 관계를 지정하려면 다음 단계를 수행합니다.

1. 프로젝트 파일을 포함합니다.
1. 저장소 서비스 클라이언트를 만듭니다.
1. 연결할 리소스의 URI를 지정합니다.
1. 관계를 만듭니다.

**프로젝트 파일 포함**

개발 프로젝트에 필요한 파일을 포함합니다. Java를 사용하여 클라이언트 응용 프로그램을 만드는 경우 필요한 JAR 파일을 포함합니다. 웹 서비스를 사용하는 경우 프록시 파일을 포함합니다.

**서비스 클라이언트 만들기**

리소스를 프로그래밍 방식으로 읽으려면 먼저 연결을 설정하고 자격 증명을 제공해야 합니다. 이 작업은 서비스 클라이언트를 작성하여 수행할 수 있습니다.

**연결할 리소스의 URI를 지정하십시오.**

연결할 리소스의 URI를 포함하는 문자열을 만듭니다. 구문에는 다음 예제와 같이 슬래시가 포함됩니다. &quot;/*경로*/*리소스*&quot;.

**관계 만들기**

관계 유형을 만들고 지정하려면 저장소 서비스 메서드를 호출하십시오.

**추가 참조**

[Java API를 사용하여 관계 리소스 만들기](aem-forms-repository.md#create-relationship-resources-using-the-java-api)

[웹 서비스 API를 사용하여 관계 리소스 만들기](aem-forms-repository.md#create-relationship-resources-using-the-web-service-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[저장소 서비스 API 빠른 시작](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### Java API를 사용하여 관계 리소스 만들기 {#create-relationship-resources-using-the-java-api}

저장소 서비스 Java API를 사용하여 관계 리소스를 생성하고 다음 작업을 수행합니다.

1. 프로젝트 파일 포함

   Java 프로젝트의 클래스 경로에 클라이언트 JAR 파일을 포함합니다.

1. 서비스 클라이언트 만들기

   만들기 `ResourceRepositoryClient` 개체를 생성자를 사용하고 `ServiceClientFactory` 연결 속성을 포함하는 개체입니다.

1. 연결할 리소스의 URI를 지정하십시오.

   연결할 리소스의 URI를 지정합니다. 이 경우 리소스에 이름이 지정되기 때문입니다 `testResource1` 및 `testResource2` 및 은(는) 다음 폴더에 있습니다. `testFolder`, 해당 URI는 `"/testFolder/testResource1"` 및 `"/testFolder/testResource2"`. URI는 `java.lang.String` 개체. 이 예제에서 리소스는 먼저 저장소에 기록되고 해당 URI가 검색됩니다. 리소스 작성에 대한 자세한 내용은 [리소스 쓰기](aem-forms-repository.md#writing-resources).

1. 관계 만들기

   호출 `ResourceRepositoryClient` 개체 `createRelationship` 메서드, 다음 매개 변수를 전달하십시오.

   * 소스 리소스의 URI입니다.
   * 대상 리소스의 URI입니다.
   * 의 정적 상수 중 하나인 관계의 유형입니다. `com.adobe.repository.infomodel.bean.Relation` 클래스. 이 예에서는 그 값을 특정함으로써 의존 관계를 설정한다 `Relation.TYPE_DEPENDANT_OF`.
   * A `boolean` 대상 리소스가 자동으로 `com.adobe.repository.infomodel.Id`새 head 리소스의 기반 식별자입니다. 이 예제에서는 종속 관계 때문에 값이 `true` 이(가) 지정되었습니다.

   또한 를 호출하여 주어진 리소스에 대한 관련 리소스 목록을 검색할 수 있습니다. `ResourceRepositoryClient` 개체 `getRelated` 메서드 및 다음 매개 변수 전달:

   * 관련 리소스를 검색할 리소스의 URI입니다. 이 예에서 소스 리소스( `"/testFolder/testResource1"`)를 지정합니다.
   * A `boolean` 지정된 리소스가 관계의 원본 리소스인지 여부를 나타내는 값입니다. 이 예에서 값은 `true` 이 경우 이므로 가 지정됩니다.
   * 에서 정적 상수 중 하나인 관계 유형 `Relation` 클래스. 이 예제에서 종속 관계는 앞에서 사용한 것과 동일한 값을 사용하여 지정됩니다. `Relation.TYPE_DEPENDANT_OF`.

   다음 `getRelated` 메서드가 을 반환합니다. `java.util.List` / `Resource` 에 포함된 객체를 캐스팅하여 각 관련 리소스를 검색하기 위해 반복할 수 있는 객체 `List` 끝 `Resource` 그렇게 하잖아요. 이 예에서는 `testResource2` 은(는) 반환된 리소스 목록에 있어야 합니다.

**추가 참조**

[리소스 관계 만들기](aem-forms-repository.md#creating-resource-relationships)

[빠른 시작(SOAP 모드): Java API를 사용하여 리소스 간 관계 만들기](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-creating-relationships-between-resources-using-the-java-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 웹 서비스 API를 사용하여 관계 리소스 만들기 {#create-relationship-resources-using-the-web-service-api}

저장소 API(웹 서비스)를 사용하여 관계 리소스를 만듭니다.

1. 프로젝트 파일 포함

   * 저장소 WSDL을 사용하는 Microsoft .NET 클라이언트 어셈블리를 만듭니다.
   * Microsoft .NET 클라이언트 어셈블리를 참조합니다.

1. 서비스 클라이언트 만들기

   Microsoft .NET 클라이언트 어셈블리를 사용하여 `RepositoryServiceService` 기본 생성자를 호출하여 개체를 작성합니다. 설정 `Credentials` 를 사용하는 속성 `System.Net.NetworkCredential` 사용자 이름과 암호가 포함된 개체입니다.

1. 연결할 리소스의 URI를 지정하십시오.

   연결할 리소스의 URI를 지정합니다. 이 경우 리소스에 이름이 지정되기 때문입니다 `testResource1` 및 `testResource2` 및 은(는) 다음 폴더에 있습니다. `testFolder`, 해당 URI는 `"/testFolder/testResource1"` 및 `"/testFolder/testResource2"`. Microsoft .NET Framework와 호환되는 언어(예: C#)를 사용하는 경우 URI는 `System.String` 개체. 이 예제에서 리소스는 먼저 저장소에 기록되고 해당 URI가 검색됩니다. 리소스 작성에 대한 자세한 내용은 [리소스 쓰기](aem-forms-repository.md#writing-resources).

1. 관계 만들기

   호출 `RepositoryServiceService` 개체 `createRelationship` 메서드, 다음 매개 변수를 전달하십시오.

   * 소스 리소스의 URI입니다.
   * 대상 리소스의 URI입니다.
   * 관계 유형. 이 예에서는 그 값을 특정함으로써 의존 관계를 설정한다 `3`.
   * A `boolean` 관계 유형을 지정했는지 여부를 나타내는 값입니다. 이 예에서 값은 `true` 이(가) 지정되었습니다.
   * A `boolean` 대상 리소스가 자동으로 `Id`새 head 리소스의 기반 식별자입니다. 이 예제에서는 종속 관계 때문에 값이 `true` 이(가) 지정되었습니다.
   * A `boolean` 대상 헤드가 지정되었는지 여부를 나타내는 값입니다. 이 예에서 값은 `true` 이(가) 지정되었습니다.
   * 합격 `null` 을 참조하십시오.

   또한 를 호출하여 주어진 리소스에 대한 관련 리소스 목록을 검색할 수 있습니다. `RepositoryServiceService` 개체 `getRelated` 메서드 및 다음 매개 변수 전달:

   * 관련 리소스를 검색할 리소스의 URI입니다. 이 예에서 소스 리소스( `"/testFolder/testResource1"`)를 지정합니다.
   * A `boolean` 지정된 리소스가 관계의 원본 리소스인지 여부를 나타내는 값입니다. 이 예에서 값은 `true` 이 경우 이므로 가 지정됩니다.
   * A `boolean` 원본 리소스가 지정되었는지 여부를 나타내는 값입니다. 이 예에서 값은 `true` 이(가) 제공됩니다.
   * 관계 유형을 포함하는 정수 배열입니다. 이 예에서 종속 관계는 앞에서 사용했던 것과 동일한 배열 값을 사용하여 지정됩니다. `3`.
   * 합격 `null` 를 참조하십시오.

   다음 `getRelated` 메서드는 캐스팅할 수 있는 개체 배열을 반환합니다. `Resource` 관련된 각 리소스를 검색하기 위해 반복할 수 있는 객체입니다. 이 예에서는 `testResource2` 은(는) 반환된 리소스 목록에 있어야 합니다.

**추가 참조**

[리소스 관계 만들기](aem-forms-repository.md#creating-resource-relationships)

[Base64 인코딩을 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

## 리소스 잠금 {#locking-resources}

특정 사용자의 단독 사용 또는 둘 이상의 사용자 간 공유 사용을 위해 리소스 또는 리소스 집합을 잠글 수 있습니다. 공유 잠금은 리소스에 문제가 발생함을 나타내지만, 이로 인해 다른 사람이 해당 리소스에 대해 작업을 수행할 수 있습니다. 공유 잠금을 신호 메커니즘으로 간주해야 합니다. 단독 잠금은 리소스를 잠근 사용자가 리소스를 변경한다는 것을 의미하며, 잠금은 사용자가 더 이상 리소스에 액세스할 필요가 없고 잠금을 해제할 때까지 다른 사용자가 이 작업을 수행할 수 없도록 합니다. 저장소 관리자가 리소스의 잠금을 해제할 경우 해당 리소스에 대한 모든 배타적 잠금 및 공유 잠금이 자동으로 제거됩니다. 이 유형의 작업은 사용자가 더 이상 사용할 수 없고 리소스 잠금이 해제되지 않은 상황을 위한 것입니다.

자원이 잠기면 다음 그림과 같이 Workbench에 있는 자원 탭을 보면 잠금 아이콘이 나타납니다.

![lr_lr_lockrepository](assets/lr_lr_lockrepository.png)

저장소 서비스 Java API 또는 웹 서비스 API를 사용하여 리소스에 대한 액세스를 프로그래밍 방식으로 제어할 수 있습니다.

>[!NOTE]
>
>저장소 서비스에 대한 자세한 내용은 [AEM Forms에 대한 서비스 참조](https://www.adobe.com/go/learn_aemforms_services_63).

### 단계 요약 {#summary_of_steps-7}

리소스를 잠그고 잠금 해제하려면 다음 단계를 수행합니다.

1. 프로젝트 파일을 포함합니다.
1. 저장소 서비스 클라이언트를 만듭니다.
1. 잠글 리소스의 URI를 지정합니다.
1. 리소스를 잠급니다.
1. 리소스에 대한 잠금을 검색합니다.
1. 리소스 잠금 해제

**프로젝트 파일 포함**

개발 프로젝트에 필요한 파일을 포함합니다. Java를 사용하여 클라이언트 응용 프로그램을 만드는 경우 필요한 JAR 파일을 포함합니다. 웹 서비스를 사용하는 경우 프록시 파일을 포함합니다.

**서비스 클라이언트 만들기**

리소스를 프로그래밍 방식으로 읽으려면 먼저 연결을 설정하고 자격 증명을 제공해야 합니다. 이 작업은 서비스 클라이언트를 작성하여 수행할 수 있습니다.

**잠글 리소스의 URI를 지정하십시오.**

잠글 리소스의 URI를 포함하는 문자열을 만듭니다. 구문에는 다음 예제와 같이 슬래시가 포함됩니다. &quot;/*경로*/*리소스*&quot;.

**리소스 잠금**

URI, 잠금 유형 및 잠금 깊이를 지정하여 리소스를 잠그려면 저장소 서비스 메서드를 호출합니다.

**리소스에 대한 잠금 검색**

저장소 서비스 메서드를 호출하여 리소스에 대한 잠금을 검색하고 URI를 지정합니다.

**리소스 잠금 해제**

URI를 지정하여 리소스의 잠금을 해제하려면 저장소 서비스 메서드를 호출하십시오.

**추가 참조**

[Java API를 사용하여 리소스 잠금](aem-forms-repository.md#lock-resources-using-the-java-api)

[웹 서비스 API를 사용하여 리소스 잠금](aem-forms-repository.md#lock-resources-using-the-web-service-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[저장소 서비스 API 빠른 시작](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### Java API를 사용하여 리소스 잠금 {#lock-resources-using-the-java-api}

저장소 서비스 API(Java)를 사용하여 리소스 잠금:

1. 프로젝트 파일 포함

   Java 프로젝트의 클래스 경로에 클라이언트 JAR 파일을 포함합니다.

1. 서비스 클라이언트 만들기

   만들기 `ResourceRepositoryClient` 개체를 생성자를 사용하고 `ServiceClientFactory` 연결 속성을 포함하는 개체입니다.

1. 잠글 리소스의 URI를 지정하십시오.

   잠글 리소스의 URI를 지정합니다. 이 경우, 리소스가 `testResource` 이(가) 다음 폴더에 있음: `testFolder`, 해당 URI는 `"/testFolder/testResource"`. URI는 `java.lang.String` 개체.

1. 리소스 잠금

   호출 `ResourceRepositoryClient` 개체 `lockResource` 메서드, 다음 매개 변수를 전달하십시오.

   * 리소스의 URI입니다.
   * 잠금 범위입니다. 이 예제에서는 리소스가 배타적으로 사용되도록 잠기므로 잠금 범위가 다음과 같이 지정됩니다. `com.adobe.repository.infomodel.bean.Lock.SCOPE_EXCLUSIVE`.
   * 잠금 깊이입니다. 이 예제에서는 잠금이 특정 리소스에만 적용되고 해당 멤버나 자식은 적용되지 않으므로 잠금 깊이가 로 지정됩니다. `Lock.DEPTH_ZERO`.

   >[!NOTE]
   >
   >의 오버로드된 버전 `lockResource` 4개의 매개 변수가 필요한 메서드에서 예외가 발생합니다. 다음을 사용하십시오. `lockResource` 이 연습에 표시된 대로 매개 변수가 세 개 필요한 메서드입니다.

1. 리소스에 대한 잠금 검색

   호출 `ResourceRepositoryClient` 개체 `getLocks` 메서드에서 리소스의 URI를 매개 변수로 전달합니다. 이 메서드는 반복할 수 있는 Lock 개체 목록을 반환합니다. 이 예제에서 각 Lock 객체의 을 호출하여 각 객체에 대해 잠금 소유자, 깊이 및 범위가 인쇄됩니다 `getOwnerUserId`, `getDepth`, 및 `getType` 메서드를 각각 사용합니다.

1. 리소스 잠금 해제

   호출 `ResourceRepositoryClient` 개체 `unlockResource` 메서드에서 리소스의 URI를 매개 변수로 전달합니다. 자세한 내용은 [AEM Forms API 참조](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

**추가 참조**

[리소스 잠금](aem-forms-repository.md#locking-resources)

[빠른 시작(SOAP 모드): Java API를 사용하여 리소스 잠금](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-locking-a-resource-using-the-java-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 웹 서비스 API를 사용하여 리소스 잠금 {#lock-resources-using-the-web-service-api}

저장소 서비스 API(웹 서비스)를 사용하여 리소스 잠금:

1. 프로젝트 파일 포함

   * Base64를 사용하여 저장소 WSDL을 사용하는 Microsoft .NET 클라이언트 어셈블리를 만듭니다.
   * Microsoft .NET 클라이언트 어셈블리를 참조합니다.

1. 서비스 클라이언트 만들기

   Microsoft .NET 클라이언트 어셈블리를 사용하여 `RepositoryServiceService` 기본 생성자를 호출하여 개체를 작성합니다. 설정 `Credentials` 를 사용하는 속성 `System.Net.NetworkCredential` 사용자 이름과 암호가 포함된 개체입니다.

1. 잠글 리소스의 URI를 지정하십시오.

   잠글 리소스의 URI를 포함하는 문자열을 지정합니다. 이 경우, 리소스가 `testResource` 폴더에 있음 `testFolder`, 해당 URI는 `"/testFolder/testResource"`. Microsoft .NET Framework와 호환되는 언어(예: C#)를 사용하는 경우 URI를 `System.String` 개체.

1. 리소스 잠금

   호출 `RepositoryServiceService` 개체 `lockResource` 메서드, 다음 매개 변수를 전달하십시오.

   * 리소스의 URI입니다.
   * 잠금 범위입니다. 이 예제에서는 리소스가 배타적으로 사용되도록 잠기므로 잠금 범위가 다음과 같이 지정됩니다. `11`.
   * 잠금 깊이입니다. 이 예제에서는 잠금이 특정 리소스에만 적용되고 해당 멤버나 자식은 적용되지 않으므로 잠금 깊이가 로 지정됩니다. `2`.
   * An `int` 잠금이 만료될 때까지의 시간(초)을 나타내는 값입니다. 이 예에서 값은 `1000` 를 사용합니다.
   * 합격 `null` 을 참조하십시오.

1. 리소스에 대한 잠금 검색

   호출 `RepositoryServiceService` 개체 `getLocks` 메서드에서 첫 번째 매개 변수로 리소스의 URI를 전달합니다. `null` (두 번째 매개 변수) 메서드는 다음을 반환합니다. `object` 다음 포함 배열 `Lock` 반복할 수 있는 객체. 이 예제에서는 각 객체에 액세스하여 각 객체에 대해 잠금 소유자, 깊이 및 범위가 인쇄됩니다 `Lock` 개체 `ownerUserId`, `depth`, 및 `type` 각각 필드입니다.

1. 리소스 잠금 해제

   호출 `RepositoryServiceService` 개체 `unlockResource` 메서드에서 첫 번째 매개 변수로 리소스의 URI를 전달합니다. `null` (두 번째 매개 변수)

**추가 참조**

[리소스 잠금](aem-forms-repository.md#locking-resources)

[Base64 인코딩을 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

## 리소스 삭제 {#deleting-resources}

저장소 서비스 SOAP(Java API)를 사용하여 저장소의 지정된 위치에서 리소스를 프로그래밍 방식으로 삭제할 수 있습니다.

리소스를 삭제하면 삭제는 일반적으로 영구적이지만 경우에 따라 ECM 저장소가 기록 메커니즘에 따라 리소스 버전을 저장할 수 있습니다. 따라서 리소스를 삭제할 때는 해당 리소스가 다시 필요하지 않도록 해야 합니다. 리소스를 삭제하는 일반적인 이유에는 데이터베이스에서 사용 가능한 공간을 늘려야 한다는 요구가 포함됩니다. 리소스 버전을 삭제할 수 있지만 이 경우 LID(논리적 식별자) 또는 경로가 아닌 리소스 식별자를 지정해야 합니다. 폴더를 삭제하면 하위 폴더 및 리소스를 포함하여 해당 폴더의 모든 항목이 자동으로 삭제됩니다.

관련 리소스는 삭제되지 않습니다. 예를 들어, logo.gif 파일을 사용하는 양식이 있는 경우 logo.gif를 삭제하면 관계가 보류 중인 관계 테이블에 저장됩니다. 또는 버전 사용 중지의 경우 최신 버전의 개체 상태를 더 이상 사용되지 않음으로 설정합니다.

삭제 작업은 ECM 시스템에서 트랜잭션하기에 안전하지 않습니다. 예를 들어 100개의 리소스를 삭제하려고 할 때 50번째 리소스에서 작업이 실패하면 처음 49개의 인스턴스는 삭제되지만 나머지는 삭제되지 않습니다. 그렇지 않은 경우 기본 동작은 롤백(비약정)입니다.

>[!NOTE]
>
>사용 시 `com.adobe.repository.bindings.dsc.client.ResourceRepositoryClient.deleteResources()` emc Documentum Content Server 및 IBM FileNet P8 Content Manager를 사용하는 메서드에서는 지정된 리소스 중 하나에 대해 삭제가 실패하면 트랜잭션이 롤백되지 않습니다. 즉, 삭제된 파일은 삭제할 수 없습니다.

>[!NOTE]
>
>저장소 서비스에 대한 자세한 내용은 [AEM Forms에 대한 서비스 참조](https://www.adobe.com/go/learn_aemforms_services_63).

### 단계 요약 {#summary_of_steps-8}

리소스를 삭제하려면 다음 단계를 수행합니다.

1. 프로젝트 파일을 포함합니다.
1. 저장소 서비스 클라이언트를 만듭니다.
1. 삭제할 리소스의 URI를 지정합니다.
1. 리소스를 삭제합니다.

**프로젝트 파일 포함**

개발 프로젝트에 필요한 파일을 포함합니다. Java를 사용하여 클라이언트 응용 프로그램을 만드는 경우 필요한 JAR 파일을 포함합니다. 웹 서비스를 사용하는 경우 프록시 파일을 포함합니다.

**서비스 클라이언트 만들기**

리소스를 프로그래밍 방식으로 읽으려면 먼저 연결을 설정하고 자격 증명을 제공해야 합니다. 이 작업은 서비스 클라이언트를 작성하여 수행할 수 있습니다.

**삭제할 리소스의 URI를 지정하십시오.**

삭제할 리소스의 URI를 포함하는 문자열을 만듭니다. 구문에는 다음 예제와 같이 슬래시가 포함됩니다. &quot;/*경로*/*리소스*&quot;. 삭제할 리소스가 폴더인 경우 삭제는 재귀적입니다.

**리소스 삭제**

URI를 지정하여 리소스를 삭제하려면 저장소 서비스 메서드를 호출하십시오.

**추가 참조**

[Java API를 사용하여 리소스 삭제](aem-forms-repository.md#delete-resources-using-the-java-api-soap)

[웹 서비스 API를 사용하여 리소스 삭제](aem-forms-repository.md#delete-resources-using-the-web-service-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[저장소 서비스 API 빠른 시작](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### Java API(SOAP)를 사용하여 리소스 삭제 {#delete-resources-using-the-java-api-soap}

저장소 API(Java)를 사용하여 리소스를 삭제합니다.

1. 프로젝트 파일 포함

   Java 프로젝트의 클래스 경로에 클라이언트 JAR 파일을 포함합니다.

1. 서비스 클라이언트 만들기

   만들기 `ResourceRepositoryClient` 개체를 생성자를 사용하고 `ServiceClientFactory` 연결 속성을 포함하는 개체입니다.

1. 삭제할 리소스의 URI를 지정하십시오.

   검색할 리소스의 URI를 지정합니다. 이 경우 testResourceToBeDeleted라는 리소스가 testFolder라는 폴더에 있으므로 해당 URI는 입니다. `/testFolder/testResourceToBeDeleted`. URI는 `java.lang.String` 개체. 이 예에서 리소스는 먼저 저장소에 기록되고 해당 URI가 검색됩니다. 리소스 작성에 대한 자세한 내용은 [리소스 쓰기](aem-forms-repository.md#writing-resources).

1. 리소스 삭제

   호출 `ResourceRepositoryClient` 개체 `deleteResource` 메서드에서 리소스의 URI를 매개 변수로 전달합니다.

**추가 참조**

[리소스 삭제](aem-forms-repository.md#deleting-resources)

[빠른 시작(SOAP 모드): Java API를 사용하여 리소스 검색](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-searching-for-resources-using-the-java-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 웹 서비스 API를 사용하여 리소스 삭제 {#delete-resources-using-the-web-service-api}

저장소 API(웹 서비스)를 사용하여 리소스를 삭제합니다.

1. 프로젝트 파일 포함

   * Base64를 사용하여 저장소 WSDL을 사용하는 Microsoft .NET 클라이언트 어셈블리를 만듭니다.
   * Microsoft .NET 클라이언트 어셈블리를 참조합니다.

1. 서비스 클라이언트 만들기

   Microsoft .NET 클라이언트 어셈블리를 사용하여 `RepositoryServiceService` 기본 생성자를 호출하여 개체를 작성합니다. 설정 `Credentials` 를 사용하는 속성 `System.Net.NetworkCredential` 사용자 이름과 암호가 포함된 개체입니다.

1. 삭제할 리소스의 URI를 지정하십시오.

   검색할 리소스의 URI를 지정합니다. 이 경우, 리소스가 `testResourceToBeDeleted` 이(가) 다음 폴더에 있음: `testFolder`, 해당 URI는 `"/testFolder/testResourceToBeDeleted"`. 이 예에서 리소스는 먼저 저장소에 기록되고 해당 URI가 검색됩니다. 리소스 작성에 대한 자세한 내용은 [리소스 쓰기](aem-forms-repository.md#writing-resources).

1. 리소스 삭제

   호출 `RepositoryServiceService` 개체 `deleteResources` 방법 및 전달 `System.String` 리소스의 URI를 첫 번째 매개 변수로 포함하는 배열입니다. 합격 `null` (두 번째 매개 변수)

**추가 참조**

[리소스 삭제](aem-forms-repository.md#deleting-resources)

[Base64 인코딩을 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
