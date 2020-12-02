---
title: AEM Forms 저장소 작업
seo-title: AEM Forms 저장소 작업
description: 'null'
seo-description: 'null'
uuid: 6ead49f9-ca0d-4ee4-86a6-0a9ced6ec4f8
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: d2c95881-6c02-4e34-85af-84607df54287
translation-type: tm+mt
source-git-commit: 67ea825215d1ca7cc2e350ed1c128c3146de45ec
workflow-type: tm+mt
source-wordcount: '9076'
ht-degree: 0%

---


# AEM Forms 리포지토리 작업 {#working-with-aem-forms-repository}

**저장소 서비스 정보**

저장소 서비스는 AEM Forms에 리소스 저장 및 관리 서비스를 제공합니다. 개발자가 *AEM Forms* 응용 프로그램을 만들면 파일 시스템 대신 에셋을 저장소에 배포할 수 있습니다. 자산은 XML 양식, PDF forms(Acrobat 양식 포함), 양식 조각, 이미지, 프로필, 정책, SWF 파일, DDX 파일, XML 스키마, WSDL 파일, 테스트 데이터 등 모든 유형의 자료를 포함할 수 있습니다.

예를 들어, 다음 Forms 응용 프로그램(*Applications/FormsApplication*)을 고려해 보십시오.

![ww_formrepository](assets/ww_ww_formrepository.png)

FormsFolder에 Loan.xdp 파일이 있습니다. 이 양식 디자인에 액세스하려면 전체 경로(버전 포함)를 지정합니다.`Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.

>[!NOTE]
>
>워크벤치를 사용하여 Forms 응용 프로그램을 만드는 방법에 대한 자세한 내용은 [워크벤치 도움말](https://www.adobe.com/go/learn_aemforms_workbench_63)을 참조하십시오.

AEM Forms 저장소에 있는 리소스의 경로는 다음과 같습니다.

`Applications/Application-name/Application-version/Folder.../Filename`

다음 값은 URI 값의 몇 가지 예를 보여 줍니다.

* Applications/AppraisalReport/1.0/Forms/FullForm.xdp
* Applications/AnotherApp/1.1/Assets/picture.jpg
* Applications/SomeApp/2.0/Resources/Data/XSDs/MyData.xsd

>[!NOTE]
>
>웹 브라우저를 사용하여 AEM Forms 저장소를 찾아볼 수 있습니다. 리포지토리를 찾아보려면 다음 URL을 웹 브라우저 `https://[server name]:[server port]/repository`에 입력합니다. 웹 브라우저를 사용하여 AEM Forms 리포지토리로 작업 섹션에 연결된 빠른 시작 결과를 확인할 수 있습니다. 예를 들어 AEM Forms 저장소에 컨텐츠를 추가하는 경우 웹 브라우저에서 컨텐츠를 볼 수 있습니다. ( [빠른 시작(SOAP 모드 참조):Java API](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-writing-a-resource-using-the-java-api)를 사용하여 리소스를 쓰는 중입니다.)

저장소 API는 저장소에서 정보를 저장하고 검색하는 데 사용할 수 있는 여러 가지 작업을 제공합니다. 예를 들어, 애플리케이션 처리의 일부로 리소스가 필요할 때 저장소에 저장된 특정 리소스를 검색하거나 리소스 목록을 가져올 수 있습니다.

>[!NOTE]
>
>저장소 API를 사용하여 콘텐츠 서비스와 상호 작용할 수 없습니다(더 이상 사용되지 않음). 컨텐츠 서비스(더 이상 사용되지 않음)와 상호 작용하려면 문서 관리 API를 사용합니다.

저장소 서비스 API를 사용하여 다음 작업을 수행할 수 있습니다.

* 폴더를 만듭니다. [폴더 만들기](aem-forms-repository.md#creating-folders)를 참조하십시오.
* 리소스 및 속성 작성 [리소스 쓰기](aem-forms-repository.md#writing-resources)를 참조하십시오.
* 주어진 컬렉션 또는 다른 리소스와 관련된 리소스를 나열합니다. [리소스 목록](aem-forms-repository.md#listing-resources)을 참조하십시오.
* 리소스 및 속성 보기 [리소스 읽기](aem-forms-repository.md#reading-resources)를 참조하십시오.
* 리소스 및 해당 속성을 업데이트합니다. [리소스 업데이트](aem-forms-repository.md#updating-resources)를 참조하십시오.
* 작업 내역, 관련 리소스 및 속성을 비롯한 리소스를 검색합니다. [리소스 검색](aem-forms-repository.md#searching-for-resources)을 참조하십시오.
* 리소스 간의 관계를 지정합니다. [리소스 관계 만들기](aem-forms-repository.md#creating-resource-relationships)를 참조하십시오.
* 리소스 잠금 및 잠금 해제, ACL(액세스 제어 목록) 읽기 및 쓰기 등 리소스 액세스 제어를 관리합니다. [리소스 잠금](aem-forms-repository.md#locking-resources)을 참조하십시오.
* 리소스 및 해당 속성을 삭제합니다. [리소스 삭제](aem-forms-repository.md#deleting-resources)를 참조하십시오.

>[!NOTE]
>
>저장소 API를 사용하면 ECM 저장소를 사용하여 리소스 액세스 제어를 관리하거나, 리소스를 검색하거나, 리소스 관계를 지정할 수 없습니다.

>[!NOTE]
>
>암호화된 PDF가 저장소에 기록되면 자동화된 관계 추출 기능을 사용할 수 없습니다. 그렇지 않으면 암호화된 PDF를 저장소에 저장하고 나중에 검색할 수 있습니다. 검색기에서 검색한 PDF의 암호를 해독하도록 선택할 수 있습니다.

>[!NOTE]
>
>저장소 서비스에 대한 자세한 내용은 [AEM Forms에 대한 서비스 참조](https://www.adobe.com/go/learn_aemforms_services_63)를 참조하십시오.

## 폴더 만들기 {#creating-folders}

폴더(리소스 컬렉션)는 개체(파일 또는 리소스)를 체계적인 그룹으로 저장하는 데 사용됩니다. 폴더에는 하위 폴더라고도 하는 리소스 및 기타 폴더가 포함될 수 있습니다. 리소스는 한 번에 한 폴더에만 저장할 수 있습니다.

파일은 폴더에서 ACL(액세스 제어 목록)을 상속하고 하위 폴더는 상위 폴더에서 ACL을 상속합니다. 따라서 하위 폴더를 만들려면 상위 폴더가 있어야 합니다. IDE를 사용하면 파일별로 상호 작용하지 않고 폴더별로 상호 작용할 수 있습니다. 폴더 버전을 지정할 수 없으며 그렇게 할 필요가 없습니다.폴더에는 데이터 자체가 없습니다. 오히려 데이터가 포함된 리소스의 컨테이너일 뿐입니다. 기본 ACL은 시스템 수준 권한이므로 특정 폴더에 대한 권한을 부여할 때까지 사용자는 시스템 수준 권한(읽기, 쓰기, 트래버스, ACL 관리)을 가져야 합니다. ACL은 IDE에서만 작동합니다.

>[!NOTE]
>
>저장소 서비스에 대한 자세한 내용은 [AEM Forms에 대한 서비스 참조](https://www.adobe.com/go/learn_aemforms_services_63)를 참조하십시오.

### {#summary-of-steps} 단계 요약

폴더를 만들려면 다음 단계를 수행하십시오.

1. 프로젝트 파일 포함
1. 서비스 클라이언트를 만듭니다.
1. 폴더를 만듭니다.
1. 저장소에 폴더를 작성합니다.

**프로젝트 파일 포함**

개발 프로젝트에 필요한 파일을 포함합니다. Java를 사용하여 클라이언트 응용 프로그램을 만드는 경우 필요한 JAR 파일을 포함합니다. 웹 서비스를 사용하는 경우 프록시 파일을 포함하십시오.

**서비스 클라이언트 만들기**

프로그래밍 방식으로 리소스 컬렉션을 만들려면 먼저 연결을 설정하고 자격 증명을 제공해야 합니다. 이는 서비스 클라이언트를 만들어 완료합니다.

**폴더 만들기**

Repository service 메서드를 호출하여 리소스 컬렉션을 만들고 UUID, 폴더 이름 및 설명을 비롯한 식별 정보로 리소스 컬렉션을 채웁니다.

**저장소에 폴더 쓰기**

저장소 서비스 메서드를 호출하여 대상 폴더의 URI를 지정하여 리소스 컬렉션을 작성합니다.

**참고 항목**

[Java API를 사용하여 폴더 만들기](aem-forms-repository.md#create-folders-using-the-java-api)

[웹 서비스 API를 사용하여 폴더 만들기](aem-forms-repository.md#create-folders-using-the-web-service-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[저장소 서비스 API 빠른 시작](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### Java API {#create-folders-using-the-java-api}를 사용하여 폴더 만들기

저장소 서비스 API(Java)를 사용하여 폴더를 만듭니다.

1. 프로젝트 파일 포함

   Java 프로젝트의 클래스 경로에 프로젝트 파일을 포함합니다.

1. 서비스 클라이언트 만들기

   생성자를 사용하여 `ResourceRepositoryClient` 개체를 만들고 연결 속성이 포함된 `ServiceClientFactory` 개체를 전달합니다.

1. 폴더 만들기

   리소스 컬렉션을 만들려면 먼저 `com.adobe.repository.infomodel.bean.RepositoryInfomodelFactoryBean` 개체를 만들어야 합니다.

   `repositoryInfomodelFactoryBean` 개체의 `newResourceCollection` 메서드를 호출하고 다음 매개 변수를 전달합니다.

   * 리소스에 할당될 `com.adobe.repository.infomodel.Id` UUID 식별자입니다.
   * 리소스에 할당될 `com.adobe.repository.infomodel.Lid` UUID 식별자입니다.
   * 리소스 컬렉션의 이름을 포함하는 `java.lang.String` 예, `FormsFolder`.

   이 메서드는 새 폴더를 나타내는 `com.adobe.repository.infomodel.bean.ResourceCollection` 개체를 반환합니다.

   `setDescription` 메서드를 사용하여 폴더 설명을 설정하고 다음 매개 변수를 전달합니다.

   * 리소스 컬렉션을 설명하는 `String` 이 예에서 `"test Folder"`은 `.`에 사용됩니다.


1. 저장소에 폴더 쓰기

   `ResourceRepositoryClient` 개체의 `writeResource` 메서드를 호출하고 폴더의 URI와 `ResourceCollection` 개체를 전달합니다. 예를 들어 폴더에 대한 URI는 다음 값 `/Applications/FormsApplication/1.0/`일 수 있습니다.

   이 메서드는 새로 만든 `com.adobe.repository.infomodel.bean.Resource` 개체의 인스턴스를 반환합니다. 예를 들어 `com.adobe.repository.infomodel.bean.Resource` 개체의 `getId` 메서드를 호출하여 새 리소스의 식별자 값을 검색할 수 있습니다.

**참고 항목**

[폴더 만들기](aem-forms-repository.md#creating-folders)

[빠른 시작(SOAP 모드):Java API를 사용하여 폴더 만들기](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-creating-a-folder-using-the-java-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 웹 서비스 API {#create-folders-using-the-web-service-api}를 사용하여 폴더 만들기

저장소 서비스 API(웹 서비스)를 사용하여 폴더를 만듭니다.

1. 프로젝트 파일 포함

   * base64를 사용하여 저장소 WSDL을 사용하는 Microsoft .NET 클라이언트 어셈블리를 만듭니다.
   * Microsoft .NET 클라이언트 어셈블리를 참조하십시오.

1. 서비스 클라이언트 만들기

   Microsoft .NET 클라이언트 어셈블리를 사용하여 기본 생성자를 호출하여 `RepositoryServiceService` 개체를 만듭니다. 사용자 이름과 암호를 포함하는 `System.Net.NetworkCredential` 개체를 사용하여 `Credentials` 속성을 설정합니다.

1. 폴더 만들기

   `ResourceCollection` 클래스에 대한 기본 생성자를 사용하여 폴더를 만들고 다음 매개 변수를 전달합니다.

   * `Id` 클래스에 대한 기본 생성자를 호출하고 `Resource` 개체의 `id` 필드에 할당하여 만든 `Id` 개체
   * `Lid` 클래스에 대한 기본 생성자를 호출하고 `Resource` 개체의 `lid` 필드에 할당하여 만든 `Lid` 개체
   * `Resource` 개체의 `name` 필드에 할당된 리소스 컬렉션의 이름을 포함하는 문자열. 이 예에서 사용되는 이름은 `"testfolder"`입니다.
   * `Resource` 개체의 `description` 필드에 지정된 리소스 컬렉션의 설명을 포함하는 문자열. 이 예에서 사용되는 설명은 `"test folder"`입니다.

1. 저장소에 폴더 쓰기

   `RepositoryServiceService` 개체의 `writeResource` 메서드를 호출하고 다음 매개 변수를 전달합니다.

   * 폴더를 만들 경로입니다.
   * 폴더를 나타내는 `ResourceCollection` 개체
   * 다른 두 매개 변수에 대해 `null`을 전달합니다.

**참고 항목**

[폴더 만들기](aem-forms-repository.md#creating-folders)

[Base64 인코딩을 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

## 리소스를 쓰는 중 {#writing-resources}

저장소의 지정된 위치에 리소스를 만들 수 있습니다. 자연어 파일 크기는 데이터베이스 제한 및 세션 시간 초과를 따릅니다. 기본 구성의 경우 파일은 25MB로 제한됩니다. 최대 파일 크기를 늘리거나 줄이려면 데이터베이스 구성을 변경해야 합니다.

리소스를 쓰는 것은 저장소에 데이터를 저장하는 것과 같습니다. 저장소에 리소스를 작성하면 저장소 에코시스템의 모든 클라이언트에서 액세스할 수 있게 됩니다. 저장소에 XML 스키마, XDP 파일 및 XSD 파일과 같은 리소스를 작성할 때 MIME 형식을 기반으로 컨텐츠가 파싱됩니다. MIME 유형이 지원되는 경우 파서는 다른 컨텐츠와 묵시적 관계가 있는지 확인합니다. 예를 들어, CSS(Cascading Style Sheet)에 공통 CSS를 참조하는 상대 URL이 있는 경우 일반 CSS도 저장소에 제출해야 합니다. 두 리소스 간의 관계는 조정 불가능한 기간 30일 동안 보류 중인 관계로 저장됩니다. 30일 기간 내에 일반 CSS를 저장소에 제출하면 관계가 만들어집니다.

리소스를 만들면 상위 폴더에서 ACL(액세스 제어 목록)이 상속됩니다. 루트 폴더에는 초기 리소스 또는 폴더를 만들 때까지 시스템 수준 권한이 있으며, 리소스 또는 폴더에 기본 ACL 권한이 부여됩니다.

저장소 서비스 Java API 또는 웹 서비스 API를 사용하여 프로그래밍 방식으로 리소스를 작성할 수 있습니다.

>[!NOTE]
>
>저장소 서비스에 대한 자세한 내용은 [AEM Forms에 대한 서비스 참조](https://www.adobe.com/go/learn_aemforms_services_63)를 참조하십시오.

### {#summary_of_steps-1} 단계 요약

리소스를 작성하려면 다음 단계를 따르십시오.

1. 프로젝트 파일 포함
1. 저장소 서비스 클라이언트를 만듭니다.
1. 읽을 리소스의 URI를 지정합니다.
1. 리소스를 확인합니다.

**프로젝트 파일 포함**

개발 프로젝트에 필요한 파일을 포함합니다. Java를 사용하여 클라이언트 응용 프로그램을 만드는 경우 필요한 JAR 파일을 포함합니다. 웹 서비스를 사용하는 경우 프록시 파일을 포함하십시오.

**서비스 클라이언트 만들기**

프로그래밍 방식으로 리소스를 읽을 수 있으려면 먼저 연결을 설정하고 자격 증명을 제공해야 합니다. 이는 서비스 클라이언트를 만들어 완료합니다.

**리소스에 대한 대상 폴더의 URI 지정**

읽을 리소스의 URI가 포함된 문자열을 만듭니다. 구문에는 다음과 같이 슬래시가 포함됩니다.&quot;/*path*/*folder*&quot;

**리소스 만들기**

Repository service 메서드를 호출하여 리소스를 만들고 UUID, 리소스 이름 및 설명을 비롯한 식별 정보로 리소스를 채웁니다.

**리소스 컨텐츠 지정**

Repository service 메서드를 호출하여 리소스 컨텐츠를 만들고 해당 컨텐츠를 리소스에 저장합니다.

**대상 폴더에 리소스 쓰기**

Repository service 메서드를 호출하여 리소스를 작성하고 대상 폴더의 URI를 지정합니다.

**참고 항목**

[Java API를 사용하여 리소스 쓰기](aem-forms-repository.md#write-resources-using-the-java-api)

[웹 서비스 API를 사용하여 리소스 작성](aem-forms-repository.md#write-resources-using-the-web-service-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[저장소 서비스 API 빠른 시작](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### Java API {#write-resources-using-the-java-api}를 사용하여 리소스 쓰기

Repository service API(Java)를 사용하여 리소스를 작성합니다.

1. 프로젝트 파일 포함

   Java 프로젝트의 클래스 경로에 클라이언트 JAR 파일을 포함합니다.

1. 서비스 클라이언트 만들기

   생성자를 사용하여 `ResourceRepositoryClient` 개체를 만들고 연결 속성이 포함된 `ServiceClientFactory` 개체를 전달합니다.

1. 리소스에 대한 대상 폴더의 URI 지정

   리소스에 대한 대상 폴더의 URI를 지정합니다. 이 경우 이름이 `testResource`인 리소스가 `testFolder`인 폴더에 저장되므로 폴더의 URI는 `"/testFolder"`입니다. URI는 `java.lang.String` 개체로 저장됩니다.

1. 리소스 만들기

   리소스를 만들려면 먼저 `com.adobe.repository.infomodel.bean.RepositoryInfomodelFactoryBean` 개체를 만들어야 합니다.

   `RepositoryInfomodelFactoryBean` 개체의 `newResource` 메서드를 호출하여 `com.adobe.repository.infomodel.bean.Resource` 개체를 만듭니다. 이 예에서 다음 매개 변수가 제공됩니다.

   * `Id` 클래스에 대한 기본 생성자를 호출하여 생성되는 `com.adobe.repository.infomodel.Id` 개체입니다.
   * `Lid` 클래스에 대한 기본 생성자를 호출하여 생성되는 `com.adobe.repository.infomodel.Lid` 개체입니다.
   * 리소스의 파일 이름을 포함하는 `java.lang.String`

   리소스의 설명을 지정하려면 `Resource` 개체의 `setDescription` 메서드를 호출하고 설명이 포함된 문자열을 전달합니다. 이 예에서 설명은 `"test resource"`입니다.

1. 리소스 컨텐츠 지정

   리소스에 대한 내용을 만들려면 `RepositoryInfomodelFactoryBean` 개체의 `newResourceContent` 메서드를 호출하고 `com.adobe.repository.infomodel.bean.ResourceContent` 개체를 반환합니다. `ResourceContent` 개체에 컨텐츠를 추가합니다. 이 예에서는 다음 작업을 수행하여 수행됩니다.

   * `ResourceContent` 개체의 `setDataDocument` 메서드를 호출하고 `com.adobe.idp.Document` 개체를 전달합니다.
   * `ResourceContent` 개체의 `setSize` 메서드를 호출하고 `Document` 개체의 크기(바이트)를 전달합니다.

   `Resource` 개체의 `setContent` 메서드를 호출하고 `ResourceContent` 개체를 전달하여 리소스를 추가합니다. 자세한 내용은 [AEM Forms API 참조](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)를 참조하십시오.

1. 대상 폴더에 리소스 쓰기

   `ResourceRepositoryClient` 개체의 `writeResource` 메서드를 호출하고 `Resource` 개체와 함께 폴더의 URI를 전달합니다.

**참고 항목**

[리소스 작성](aem-forms-repository.md#writing-resources)

[빠른 시작(SOAP 모드):Java API를 사용하여 리소스 쓰기](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-writing-a-resource-using-the-java-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 웹 서비스 API {#write-resources-using-the-web-service-api}를 사용하여 리소스 쓰기

Repository service API(웹 서비스)를 사용하여 리소스를 작성합니다.

1. 프로젝트 파일 포함

   * base64를 사용하여 저장소 WSDL을 사용하는 Microsoft .NET 클라이언트 어셈블리를 만듭니다.
   * Microsoft .NET 클라이언트 어셈블리를 참조하십시오.

1. 서비스 클라이언트 만들기

   Microsoft .NET 클라이언트 어셈블리를 사용하여 기본 생성자를 호출하여 `RepositoryServiceService` 개체를 만듭니다. 사용자 이름과 암호를 포함하는 `System.Net.NetworkCredential` 개체를 사용하여 `Credentials` 속성을 설정합니다.

1. 리소스에 대한 대상 폴더의 URI 지정

   리소스에 대한 대상 폴더의 URI를 지정합니다. 이 경우 이름이 `testResource`인 리소스가 `testFolder`인 폴더에 저장되므로 폴더의 URI는 `"/testFolder"`입니다. Microsoft .NET Framework(예: C#)와 호환되는 언어를 사용하는 경우 URI를 `System.String` 개체에 저장합니다.

1. 리소스 만들기

   리소스를 만들려면 `Resource` 클래스에 대한 기본 생성자를 호출합니다. 이 예에서 다음 정보는 `Resource` 개체에 저장됩니다.

   * `Id` 클래스에 대한 기본 생성자를 호출하고 `Resource` 개체의 `id` 필드에 할당하여 만든 `com.adobe.repository.infomodel.Id` 개체입니다.
   * `Lid` 클래스에 대한 기본 생성자를 호출하고 `Resource` 개체의 `lid` 필드에 할당하여 만든 `com.adobe.repository.infomodel.Lid` 개체입니다.
   * 리소스의 파일 이름이 들어 있는 문자열로서, `Resource` 개체의 `name` 필드에 할당됩니다. 이 예에서 사용되는 이름은 `"testResource"`입니다.
   * `Resource` 개체의 `description` 필드에 할당된 리소스의 설명을 포함하는 문자열. 이 예에서 사용되는 설명은 `"test resource"`입니다.

1. 리소스 컨텐츠 지정

   리소스에 대한 컨텐츠를 만들려면 `ResourceContent` 클래스에 대한 기본 생성자를 불러옵니다. 그런 다음 `ResourceContent` 개체에 컨텐츠를 추가합니다. 이 예에서는 다음 작업을 수행하여 수행됩니다.

   * 문서를 포함하는 `BLOB` 개체를 `ResourceContent` 개체의 `dataDocument` 필드에 할당합니다.
   * `BLOB` 개체의 크기(바이트)를 `ResourceContent` 개체의 `size` 필드에 할당합니다.

   `ResourceContent` 개체를 `Resource` 개체의 `content` 필드에 할당하여 리소스를 추가합니다.

1. 대상 폴더에 리소스 쓰기

   `RepositoryServiceService` 개체의 `writeResource` 메서드를 호출하고 `Resource` 개체와 함께 폴더의 URI를 전달합니다. 다른 두 매개 변수에 대해 `null`을 전달합니다.

**참고 항목**

[리소스 작성](aem-forms-repository.md#writing-resources)

[Base64 인코딩을 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

## 리소스 목록 {#listing-resources}

리소스를 나열하여 리소스를 찾을 수 있습니다. 저장소에 대해 쿼리가 수행되어 주어진 리소스 수집과 관련된 모든 리소스를 찾습니다.

리소스를 구성한 후에는 운영 체제에서와 마찬가지로 구조의 특정 분기를 보고 생성한 구조를 검사할 수 있습니다.

목록 리소스는 관계별로 작동합니다.리소스는 폴더의 구성원입니다. 멤버십은 &quot;member of&quot; 유형의 관계로 표시됩니다. 지정된 폴더에 리소스를 나열할 때 &quot;member of&quot; 관계(해당)가 해당 폴더와 관련된 리소스를 쿼리하는 것입니다. 관계는 방향입니다.관계의 구성원은 타겟의 멤버인 소스를 가집니다. 소스는 자원이다.대상은 상위 폴더입니다.

>[!NOTE]
>
>저장소 서비스에 대한 자세한 내용은 [AEM Forms에 대한 서비스 참조](https://www.adobe.com/go/learn_aemforms_services_63)를 참조하십시오.

### {#summary_of_steps-2} 단계 요약

리소스를 나열하려면 다음 단계를 따르십시오.

1. 프로젝트 파일 포함
1. 서비스 클라이언트를 만듭니다.
1. 폴더 경로를 지정합니다.
1. 리소스 목록을 검색합니다.

**프로젝트 파일 포함**

개발 프로젝트에 필요한 파일을 포함합니다. Java를 사용하여 클라이언트 응용 프로그램을 만드는 경우 필요한 JAR 파일을 포함합니다. 웹 서비스를 사용하는 경우 프록시 파일을 포함하십시오.

**서비스 클라이언트 만들기**

프로그래밍 방식으로 리소스 컬렉션을 만들려면 먼저 연결을 설정하고 자격 증명을 제공해야 합니다. 이는 서비스 클라이언트를 만들어 완료합니다.

**폴더 경로 지정**

리소스를 포함하는 폴더의 경로를 포함하는 문자열을 만듭니다. 구문에는 다음과 같이 슬래시가 포함됩니다.&quot;/*path*/*folder*&quot;

**리소스 목록 검색**

Repository service 메서드를 호출하여 리소스 목록을 검색하여 대상 폴더의 경로를 지정합니다.

**참고 항목**

[Java API를 사용하여 리소스 나열](aem-forms-repository.md#list-resources-using-the-java-api)

[웹 서비스 API를 사용하는 리소스 목록](aem-forms-repository.md#list-resources-using-the-web-service-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[저장소 서비스 API 빠른 시작](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### Java API {#list-resources-using-the-java-api}를 사용하여 리소스를 나열합니다.

Repository service API(Java)를 사용하여 리소스를 나열합니다.

1. 프로젝트 파일 포함

   Java 프로젝트의 클래스 경로에 클라이언트 JAR 파일을 포함합니다.

1. 서비스 클라이언트 만들기

   생성자를 사용하여 `ResourceRepositoryClient` 개체를 만들고 연결 속성이 포함된 `ServiceClientFactory` 개체를 전달합니다.

1. 폴더 경로 지정

   쿼리할 리소스 컬렉션의 URI를 지정합니다. 이 경우 URI는 `"/testFolder"`입니다. URI는 `java.lang.String` 개체로 저장됩니다.

1. 리소스 목록 검색

   `ResourceRepositoryClient` 개체의 `listMembers` 메서드를 호출하고 폴더의 URI를 전달합니다.

   이 메서드는 `Relation.TYPE_MEMBER_OF` 유형의 `com.adobe.repository.infomodel.bean.Relation`의 소스인 `com.adobe.repository.infomodel.bean.Resource` 개체의 `java.util.List`을 반환하고 리소스 수집 URI를 대상으로 합니다. 이 `List`을 반복하여 각 리소스를 검색할 수 있습니다. 이 예에서는 각 리소스의 이름과 설명이 표시됩니다.

**참고 항목**

[리소스 나열을 참조하십시오](aem-forms-repository.md#listing-resources).

[빠른 시작(SOAP 모드):Java API를 사용하여 리소스 나열](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-listing-resources-using-the-java-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 웹 서비스 API {#list-resources-using-the-web-service-api}를 사용하여 리소스를 나열합니다.

Repository service API(웹 서비스)를 사용하여 리소스를 나열합니다.

1. 프로젝트 파일 포함

   * 저장소 WSDL을 사용하는 Microsoft .NET 클라이언트 어셈블리를 만듭니다.
   * Microsoft .NET 클라이언트 어셈블리를 참조하십시오.

1. 서비스 클라이언트 만들기

   Microsoft .NET 클라이언트 어셈블리를 사용하여 기본 생성자를 호출하여 `RepositoryServiceService` 개체를 만듭니다. 사용자 이름과 암호를 포함하는 `System.Net.NetworkCredential` 개체를 사용하여 `Credentials` 속성을 설정합니다.

1. 폴더 경로 지정

   쿼리할 폴더의 URI가 포함된 문자열을 지정합니다. 이 경우 URI는 `"/testFolder"`입니다. Microsoft .NET Framework(예: C#)와 호환되는 언어를 사용하는 경우 URI를 `System.String` 개체에 저장합니다.

1. 리소스 목록 검색

   `RepositoryServiceService` 개체의 `listMembers` 메서드를 호출하고 폴더의 URI를 첫 번째 매개 변수로 전달합니다. 다른 두 매개 변수에 대해 `null`을 전달합니다.

   이 메서드는 `Resource` 개체에 캐스팅할 수 있는 개체 배열을 반환합니다. 객체 배열을 반복하여 관련 리소스를 각각 검색할 수 있습니다. 이 예에서는 각 리소스의 이름과 설명이 표시됩니다.

**참고 항목**

[리소스 나열을 참조하십시오](aem-forms-repository.md#listing-resources).

[Base64 인코딩을 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

## 리소스 {#reading-resources} 읽기

저장소의 지정된 위치에서 해당 컨텐츠와 메타데이터를 읽기 위해 리소스를 검색할 수 있습니다. 워크플로우는 초기화 양식으로 미리 끝납니다. 이 프로세스에는 양식을 읽는 데 필요한 모든 권한이 있습니다. 시스템은 데이터 양식을 검색하고 저장소에서 컨텐츠를 읽습니다. 보관소는 컨텐츠와 메타데이터에 대한 액세스 권한을 부여합니다(리소스가 존재함을 아는 기능).

저장소에는 다음과 같은 네 가지 권한 유형이 있습니다.

* **트래버스**:리소스를 나열할 수 있습니다.즉, 리소스 메타데이터를 읽는 대신 리소스 컨텐츠를 읽는 것입니다.
* **읽기**:리소스 컨텐츠를 읽을 수 있도록 허용
* **쓰기**:리소스 컨텐츠를 작성할 수 있도록 허용
* **ACL(액세스 제어 목록 관리)**:리소스 ACL을 조작할 수 있도록 함

사용자는 프로세스를 실행할 권한이 있는 경우에만 프로세스를 실행할 수 있습니다. IDE 사용자는 탐색과 읽기 권한이 있어야 보관소와 동기화할 수 있습니다. 런타임이 시스템 컨텍스트 내에서 발생하므로 ACL은 디자인 시에만 적용됩니다.

저장소 서비스 Java API 또는 웹 서비스 API를 사용하여 프로그래밍 방식으로 리소스를 읽을 수 있습니다.

>[!NOTE]
>
>저장소 서비스에 대한 자세한 내용은 [AEM Forms에 대한 서비스 참조](https://www.adobe.com/go/learn_aemforms_services_63)를 참조하십시오.

### {#summary_of_steps-3} 단계 요약

리소스를 읽으려면 다음 단계를 따르십시오.

1. 프로젝트 파일 포함
1. 저장소 서비스 클라이언트를 만듭니다.
1. 읽을 리소스의 URI를 지정합니다.
1. 리소스를 확인합니다.

**프로젝트 파일 포함**

개발 프로젝트에 필요한 파일을 포함합니다. Java를 사용하여 클라이언트 응용 프로그램을 만드는 경우 필요한 JAR 파일을 포함합니다. 웹 서비스를 사용하는 경우 프록시 파일을 포함하십시오.

**서비스 클라이언트 만들기**

프로그래밍 방식으로 리소스를 읽을 수 있으려면 먼저 연결을 설정하고 자격 증명을 제공해야 합니다. 이는 서비스 클라이언트를 만들어 완료합니다.

**읽을 리소스의 URI 지정**

읽을 리소스의 URI가 포함된 문자열을 만듭니다. 구문에는 다음과 같이 슬래시가 포함됩니다.&quot;/*path*/*resource*&quot;

**리소스 보기**

Repository service 메서드를 호출하여 리소스를 읽고 URI를 지정합니다.

**참고 항목**

[Java API를 사용하여 리소스 읽기](aem-forms-repository.md#read-resources-using-the-java-api)

[웹 서비스 API를 사용한 리소스 읽기](aem-forms-repository.md#reading-resources-using-the-web-service-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[저장소 서비스 API 빠른 시작](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### Java API {#read-resources-using-the-java-api}를 사용하여 리소스 읽기

Repository service API(Java)를 사용하여 리소스를 확인합니다.

1. 프로젝트 파일 포함

   Java 프로젝트의 클래스 경로에 클라이언트 JAR 파일을 포함합니다.

1. 서비스 클라이언트 만들기

   생성자를 사용하여 `ResourceRepositoryClient` 개체를 만들고 연결 속성이 포함된 `ServiceClientFactory` 개체를 전달합니다.

1. 읽을 리소스의 URI 지정

   검색할 리소스의 URI를 나타내는 문자열 값을 지정합니다. 예를 들어 리소스 이름이 *testFolder*&#x200B;이라는 폴더에 있는 &lt;a0/>testResource *이라고 가정할 경우 `/testFolder/testResource`를 지정합니다.*

1. 리소스 보기

   `ResourceRepositoryClient` 개체의 `readResource` 메서드를 호출하고 리소스의 URI를 매개 변수로 전달합니다. 이 메서드는 리소스를 나타내는 `Resource` 인스턴스를 반환합니다.

**참고 항목**

[읽기 리소스](aem-forms-repository.md#reading-resources)

[빠른 시작(SOAP 모드):Java API를 사용하여 리소스 읽기](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-reading-a-resource-using-the-java-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 웹 서비스 API {#reading-resources-using-the-web-service-api}를 사용하여 리소스를 읽는 중

Repository service API(웹 서비스)를 사용하여 리소스를 확인합니다.

1. 프로젝트 파일 포함

   * 저장소 WSDL을 사용하는 Microsoft .NET 클라이언트 어셈블리를 만듭니다. (Base64 인코딩](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)을 사용하는 .NET 클라이언트 어셈블리 만들기를 참조하십시오.)[
   * Microsoft .NET 클라이언트 어셈블리를 참조하십시오. (Base64 인코딩](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)을 사용하는 .NET 클라이언트 어셈블리 만들기를 참조하십시오.)[

1. 서비스 클라이언트 만들기

   Microsoft .NET 클라이언트 어셈블리를 사용하여 기본 생성자를 호출하여 `RepositoryServiceService` 개체를 만듭니다. 사용자 이름과 암호를 포함하는 `System.Net.NetworkCredential` 개체를 사용하여 `Credentials` 속성을 설정합니다.

1. 읽을 리소스의 URI 지정

   검색할 리소스의 URI가 포함된 문자열을 지정합니다. 이 경우 이름이 `testResource`인 리소스가 이름이 `testFolder`인 폴더에 있으므로 해당 URI는 `"/testFolder/testResource"`입니다. Microsoft .NET Framework(예: C#)와 호환되는 언어를 사용하는 경우 URI를 `System.String` 개체에 저장합니다.

1. 리소스 보기

   `RepositoryServiceService` 개체의 `readResource` 메서드를 호출하고 리소스의 URI를 첫 번째 매개 변수로 전달합니다. 다른 두 매개 변수에 대해 `null`을 전달합니다.

**참고 항목**

[읽기 리소스](aem-forms-repository.md#reading-resources)

[Base64 인코딩을 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

## 리소스 {#updating-resources} 업데이트

저장소의 리소스 컨텐츠를 검색하고 업데이트할 수 있습니다. 리소스를 업데이트하면 버전 간에 이러한 리소스에 대한 액세스 제어가 변경되지 않습니다. 업데이트를 수행할 때 주 버전을 늘릴 수 있습니다. 주 버전을 증가시키지 않으면 부 버전이 자동으로 업데이트됩니다.

리소스를 업데이트하면 지정된 리소스 속성을 기반으로 새 버전이 만들어집니다. 리소스를 업데이트할 때 두 가지 중요한 매개 변수를 지정합니다.대상 URI와 업데이트된 모든 메타데이터를 포함하는 리소스 인스턴스. 지정된 속성(예: 이름)을 변경하지 않는 경우 전달된 인스턴스에서도 속성이 여전히 필요합니다. 컨텐츠를 구문 분석할 때 생성되는 관계는 특정 버전에 추가되며 지정된 경우를 제외하고 전달되지 않습니다.

예를 들어 XDP 파일을 업데이트한 후 다른 리소스에 대한 참조가 포함되어 있으면 이러한 추가 참조도 기록됩니다. form.xdp 버전 1.0에 다음 두 개의 외부 참조가 있다고 가정합니다.로고 및 스타일 시트를 업데이트하면 form.xdp를 업데이트하여 다음과 같은 세 가지 참조가 만들어집니다.로고, 스타일 시트 및 스키마 파일. 업데이트 중에 리포지토리는 보류 중인 관계 테이블에 세 번째 관계(스키마 파일에)를 추가합니다. 저장소 내에 스키마 파일이 있으면 관계가 자동으로 만들어집니다. 그러나 form.xdp 버전 2.0이 더 이상 로고를 사용하지 않는 경우 form.xdp 버전 2.0은 로고와 관련이 없습니다.

모든 업데이트 작업은 원자적 및 트랜잭션 작업입니다. 예를 들어 두 사용자가 동일한 리소스를 읽고 버전 1.0을 버전 2.0으로 모두 업데이트하기로 한 경우, 그 중 하나는 성공하고 하나는 실패하게 되며, 저장소의 무결성은 유지되며, 둘 다 성공 또는 실패를 확인하는 메시지를 받게 됩니다. 트랜잭션이 커밋되지 않으면 데이터베이스 실패 시 롤백되고 응용 프로그램 서버에 따라 시간 초과나 롤백됩니다.

저장소 서비스 Java API 또는 웹 서비스 API를 사용하여 프로그래밍 방식으로 리소스를 업데이트할 수 있습니다.

>[!NOTE]
>
>저장소 서비스에 대한 자세한 내용은 [AEM Forms에 대한 서비스 참조](https://www.adobe.com/go/learn_aemforms_services_63)를 참조하십시오.

### {#summary_of_steps-4} 단계 요약

리소스를 업데이트하려면 다음 단계를 따르십시오.

1. 프로젝트 파일 포함
1. 저장소 서비스 클라이언트를 만듭니다.
1. 업데이트할 리소스를 검색합니다.
1. 리소스를 업데이트합니다.

**프로젝트 파일 포함**

개발 프로젝트에 필요한 파일을 포함합니다. Java를 사용하여 클라이언트 응용 프로그램을 만드는 경우 필요한 JAR 파일을 포함합니다. 웹 서비스를 사용하는 경우 프록시 파일을 포함하십시오.

**서비스 클라이언트 만들기**

프로그래밍 방식으로 리소스를 읽을 수 있으려면 먼저 연결을 설정하고 자격 증명을 제공해야 합니다. 이는 서비스 클라이언트를 만들어 완료합니다.

**업데이트할 리소스 검색**

리소스를 확인합니다. 자세한 내용은 [리소스 읽기](aem-forms-repository.md#reading-resources)를 참조하십시오.

**리소스 업데이트**

리소스의 새 정보를 설정하고 저장소 서비스 방법을 호출하여 리소스를 업데이트하며 URI, 업데이트된 리소스 및 버전 정보를 업데이트하는 방법을 지정합니다.

**참고 항목**

[Java API를 사용하여 리소스 업데이트](aem-forms-repository.md#update-resources-using-the-java-api)

[웹 서비스 API를 사용하여 리소스 업데이트](aem-forms-repository.md#update-resources-using-the-web-service-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[저장소 서비스 API 빠른 시작](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### Java API {#update-resources-using-the-java-api}를 사용하여 리소스 업데이트

Repository service API(Java)를 사용하여 리소스를 업데이트합니다.

1. 프로젝트 파일 포함

   Java 프로젝트의 클래스 경로에 클라이언트 JAR 파일을 포함합니다.

1. 서비스 클라이언트 만들기

   생성자를 사용하여 `ResourceRepositoryClient` 개체를 만들고 연결 속성이 포함된 `ServiceClientFactory` 개체를 전달합니다.

1. 업데이트할 리소스 검색

   리소스를 검색하고 읽을 리소스의 URI를 지정합니다. 이 예에서 리소스의 URI는 `"/testFolder/testResource"`입니다.

1. 리소스 업데이트

   `Resource` 개체 정보를 업데이트합니다. 이 예에서 설명을 업데이트하려면 `Resource` 개체의 `setDescription` 메서드를 호출하고 새 설명 문자열을 매개 변수로 전달합니다.

   그런 다음 `ServiceClientFactory` 개체의 `updateResource` 메서드를 호출하고 다음 매개 변수를 전달합니다.

   * 리소스의 URI를 포함하는 `java.lang.String` 개체입니다.
   * 업데이트된 리소스 정보가 포함된 `Resource` 개체입니다.
   * 주 버전을 업데이트할지 또는 부 버전을 업데이트할지 여부를 나타내는 `boolean` 값. 이 예에서, `true` 값이 전달되어 주 버전이 증가함을 나타냅니다.

**참고 항목**

[리소스 업데이트](aem-forms-repository.md#updating-resources)

[빠른 시작(SOAP 모드):Java API를 사용하여 리소스 업데이트](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-updating-a-resource-using-the-java-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 웹 서비스 API {#update-resources-using-the-web-service-api}를 사용하여 리소스 업데이트

저장소 API(웹 서비스)를 사용하여 리소스를 업데이트합니다.

1. 프로젝트 파일 포함

   * 저장소 WSDL을 사용하는 Microsoft .NET 클라이언트 어셈블리를 만듭니다.
   * Microsoft .NET 클라이언트 어셈블리를 참조하십시오.

1. 서비스 클라이언트 만들기

   Microsoft .NET 클라이언트 어셈블리를 사용하여 기본 생성자를 호출하여 `RepositoryServiceService` 개체를 만듭니다. 사용자 이름과 암호를 포함하는 `System.Net.NetworkCredential` 개체를 사용하여 `Credentials` 속성을 설정합니다.

1. 업데이트할 리소스 검색

   검색할 리소스의 URI를 지정하고 리소스를 읽습니다. 이 예에서 리소스의 URI는 `"/testFolder/testResource"`입니다. 자세한 내용은 [리소스 읽기](aem-forms-repository.md#reading-resources)를 참조하십시오.

1. 리소스 업데이트

   `Resource` 개체 정보를 업데이트합니다. 이 예에서 설명을 업데이트하려면 `Resource` 개체의 `description` 필드에 새 값을 할당합니다.

1. `RepositoryServiceService` 개체의 `updateResource` 메서드를 호출하고 다음 매개 변수를 전달합니다.

   * 리소스의 URI를 포함하는 `System.String` 개체입니다.
   * 업데이트된 리소스 정보가 포함된 `Resource` 개체입니다.
   * 주 버전을 업데이트할지 또는 부 버전을 업데이트할지 여부를 나타내는 `boolean` 값. 이 예에서, `true` 값이 전달되어 주 버전이 증가함을 나타냅니다.
   * 나머지 두 매개 변수에 대해 `null`을(를) 전달합니다.

**참고 항목**

[리소스 업데이트](aem-forms-repository.md#updating-resources)

[Base64 인코딩을 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

## 리소스 {#searching-for-resources} 검색

내역, 관련 리소스 및 속성을 포함하여 저장소에서 리소스를 검색하는 데 사용되는 쿼리를 만들 수 있습니다.

관련 리소스를 검색하여 양식과 조각 간의 종속성을 확인할 수 있습니다. 예를 들어 양식이 있는 경우 어떤 조각 또는 외부 리소스를 사용할지 결정할 수 있습니다. 이미지가 있는 경우 해당 이미지를 사용하는 양식도 확인할 수 있습니다. 속성을 기반으로 하는 필터링을 사용하여 관련 리소스를 검색할 수도 있습니다. 예를 들어, 지정된 이름의 이미지를 사용하는 모든 양식을 검색하거나, 지정된 이름의 양식에 사용된 이미지를 찾을 수 있습니다. 리소스 속성을 사용하여 검색할 수도 있습니다. 예를 들어 쿼리를 수행하여 이름이 &#39;%&#39; 및 &#39;_&#39; 와일드카드를 포함할 수 있는 지정된 문자열로 시작하는 모든 양식 또는 리소스를 찾을 수 있습니다. 속성을 기반으로 하는 검색은 관계를 기반으로 하지 않습니다.이러한 검색은 주어진 리소스에 대한 특정 지식이 있다는 가정을 기반으로 합니다.

**쿼리 문**

*쿼리*&#x200B;에는 논리적으로 조건에 연결된 하나 이상의 문이 포함되어 있습니다. *문*&#x200B;은 왼쪽 피연산자, 연산자 및 오른쪽 피연산자로 구성됩니다. 또한 검색 결과에 사용할 정렬 순서를 지정할 수 있습니다. *정렬 순서*&#x200B;에는 SQL `ORDER BY` 절에 상응하는 정보가 들어 있으며, 검색이 시작된 속성이 포함된 요소와 오름차순 또는 내림차순 사용 여부를 나타내는 값으로 구성됩니다.

저장소 서비스 Java API를 사용하여 프로그래밍 방식으로 리소스를 검색할 수 있습니다. 지금은 웹 서비스 API를 사용하여 리소스를 검색할 수 없습니다.

**정렬 동작**

`ResourceRepositoryClient` 개체의 `searchProperties` 메서드를 호출하고 정렬 순서를 지정하면 정렬 순서가 적용되지 않습니다. 예를 들어, 특성 이름이 `name`, `secondName` 및 `asecondName`인 세 개의 사용자 지정 속성을 가진 리소스를 만든다고 가정합니다. 그런 다음 속성 이름에 정렬 순서 요소를 만들고 `ascending` 값을 `true`로 설정합니다.

그런 다음 `ResourceRepositoryClient` 개체의 `searchProperties` 메서드를 호출하고 정렬 순서를 전달합니다. 검색은 세 개의 속성을 가진 올바른 리소스를 반환합니다. 하지만 속성은 속성 이름별로 정렬되지 않습니다. 추가된 순서대로 반환됩니다.`name`, `secondName` 및 `asecondName`.

>[!NOTE]
>
>저장소 서비스에 대한 자세한 내용은 [AEM Forms에 대한 서비스 참조](https://www.adobe.com/go/learn_aemforms_services_63)를 참조하십시오.

### {#summary_of_steps-5} 단계 요약

리소스를 검색하려면 다음 단계를 따르십시오.

1. 프로젝트 파일 포함
1. 저장소 서비스 클라이언트를 만듭니다.
1. 검색할 대상 폴더를 지정합니다.
1. 검색에 사용되는 속성을 지정합니다.
1. 검색에 사용되는 쿼리를 만듭니다.
1. 검색 결과에 대한 정렬 순서를 만듭니다.
1. 리소스를 검색합니다.
1. 검색 결과에서 리소스를 검색합니다.

**프로젝트 파일 포함**

개발 프로젝트에 필요한 파일을 포함합니다. Java를 사용하여 클라이언트 응용 프로그램을 만드는 경우 필요한 JAR 파일을 포함합니다. 웹 서비스를 사용하는 경우 프록시 파일을 포함하십시오.

**서비스 클라이언트 만들기**

프로그래밍 방식으로 리소스를 읽을 수 있으려면 먼저 연결을 설정하고 자격 증명을 제공해야 합니다. 이는 서비스 클라이언트를 만들어 완료합니다.

**검색에 사용할 대상 폴더 지정**

검색을 수행할 기본 경로를 포함하는 문자열을 만듭니다. 구문에는 다음과 같이 슬래시가 포함됩니다.&quot;/*path*/*folder*&quot;

**검색에 사용되는 속성 지정**

리소스 내에 포함된 속성을 기반으로 검색을 할 수 있습니다. 검색을 수행할 속성 값을 지정합니다.

**검색에 사용되는 쿼리 만들기**

문과 조건을 사용하여 쿼리를 생성합니다. 각 문은 검색을 기준으로 할 속성, 사용할 조건 및 검색에 사용할 속성 값을 지정합니다.

**검색 결과에 대한 정렬 순서 만들기**

정렬 순서는 요소로 구성되며, 각 요소에는 검색에 사용되는 속성 중 하나와 오름차순 또는 내림차순 사용 여부를 나타내는 값이 포함됩니다.

**리소스 검색**

폴더, 쿼리 및 정렬 순서를 사용하여 리소스를 검색합니다. 또한 검색 깊이와 반환할 결과 수에 대한 상한을 표시합니다.

**검색 결과에서 리소스 검색**

반환된 리소스 목록을 반복하고 추가 처리를 위해 정보를 추출합니다.

**참고 항목**

[Java API를 사용하여 리소스 검색](aem-forms-repository.md#search-for-resources-using-the-java-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[저장소 서비스 API 빠른 시작](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### Java API {#search-for-resources-using-the-java-api}를 사용하여 리소스 검색

Repository service API(Java)를 사용하여 리소스를 검색합니다.

1. 프로젝트 파일 포함

   Java 프로젝트의 클래스 경로에 클라이언트 JAR 파일을 포함합니다.

1. 서비스 클라이언트 만들기

   생성자를 사용하여 `ResourceRepositoryClient` 개체를 만들고 연결 속성이 포함된 `ServiceClientFactory` 개체를 전달합니다.

1. 검색에 사용할 대상 폴더 지정

   검색을 실행할 기본 경로의 URI를 지정합니다. 이 예에서 리소스의 URI는 `/testFolder`입니다.

1. 검색에 사용되는 속성 지정

   검색을 수행할 속성의 값을 지정합니다. 특성이 `com.adobe.repository.infomodel.bean.Resource` 개체 내에 있습니다. 이 예에서는 name 속성에 대해 검색이 수행됩니다.따라서 `Resource` 개체의 이름을 포함하는 `java.lang.String`이(가) 사용됩니다. 이 경우 `testResource`입니다.

1. 검색에 사용되는 쿼리 만들기

   쿼리를 만들려면 `Query` 클래스에 대한 기본 생성자를 호출하여 `com.adobe.repository.query.Query` 개체를 만들고 쿼리에 문을 추가합니다.

   문을 만들려면 `com.adobe.repository.query.Query.Statement` 클래스에 대한 생성자를 호출하고 다음 매개 변수를 전달합니다.

   * 리소스 속성 상수가 들어 있는 왼쪽 피연산자입니다. 이 예에서 리소스 이름이 검색 기준으로 사용되므로 정적 값 `Resource.ATTRIBUTE_NAME`이 사용됩니다.
   * 속성 검색에 사용되는 조건을 포함하는 연산자입니다. 연산자는 `Query.Statement` 클래스에 있는 정적 상수 중 하나여야 합니다. 이 예에서 정적 값 `Query.Statement.OPERATOR_BEGINS_WITH`이 사용됩니다.
   * 검색을 수행할 속성 값을 포함하는 오른쪽 피연산자입니다. 이 예에서 이름 속성인 `"testResource"` 값이 포함된 `String`이 사용됩니다.

   `Query.Statement` 개체의 `setNamespace` 메서드를 호출하고 `com.adobe.repository.infomodel.bean.ResourceProperty` 클래스에 포함된 정적 값 중 하나를 전달하여 왼쪽 피연산자의 네임스페이스를 지정합니다. 이 예에서 `ResourceProperty.RESERVED_NAMESPACE_REPOSITORY`이 사용됩니다.

   `Query` 개체의 `addStatement` 메서드를 호출하고 `Query.Statement` 개체를 전달하여 각 문을 쿼리에 추가합니다.

1. 검색 결과에 대한 정렬 순서 만들기

   검색 결과에 사용되는 정렬 순서를 지정하려면 `SortOrder` 클래스에 대한 기본 생성자를 호출하여 `com.adobe.repository.query.sort.SortOrder` 개체를 만들고 정렬 순서에 요소를 추가합니다.

   정렬 순서에 대한 요소를 만들려면 `com.adobe.repository.query.sort.SortOrder.Element` 클래스에 대한 생성자 중 하나를 호출합니다. 이 예에서 리소스 이름이 검색 기준으로 사용되기 때문에 정적 값 `Resource.ATTRIBUTE_NAME`은 첫 번째 매개 변수로 사용되고 오름차순(`boolean` 값: `true`)은 두 번째 매개 변수로 지정됩니다.

   `SortOrder` 개체의 `addSortElement` 메서드를 호출하고 `SortOrder.Element` 개체를 전달하여 정렬 순서에 각 요소를 추가합니다.

1. 리소스 검색

   속성 속성을 기준으로 `resources`을 검색하려면 `ResourceRepositoryClient` 개체의 `searchProperties` 메서드를 호출하고 다음 매개 변수를 전달합니다.

   * 검색을 실행할 기본 경로를 포함하는 `String` 이 경우 `"/testFolder"`이 사용됩니다.
   * 검색에 사용되는 쿼리입니다.
   * 검색 깊이 이 경우, `com.adobe.repository.infomodel.bean.ResourceCollection.DEPTH_INFINITE`은 기본 경로와 모든 해당 폴더를 사용할 것임을 나타내는 데 사용됩니다.
   * 호출되지 않은 결과 집합을 선택할 첫 번째 행을 나타내는 `int` 값. 이 예에서 `0`이(가) 지정되었습니다.
   * 반환할 최대 결과 수를 나타내는 `int` 값. 이 예에서 `10`이(가) 지정되었습니다.
   * 검색에 사용되는 정렬 순서.

   이 메서드는 지정된 정렬 순서에서 `Resource` 개체의 `java.util.List`을 반환합니다.

1. 검색 결과에서 리소스 검색

   검색 결과에 포함된 리소스를 검색하려면 `List`을 반복하여 각 개체를 `Resource`에 캐스팅하여 해당 정보를 추출합니다. 이 예에서 각 리소스의 이름이 표시됩니다.

**참고 항목**

[리소스 검색](aem-forms-repository.md#searching-for-resources)

[빠른 시작(SOAP 모드):Java API를 사용하여 리소스 검색](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-searching-for-resources-using-the-java-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## 리소스 관계 만들기 {#creating-resource-relationships}

저장소의 리소스 간 관계를 지정할 수 있습니다. 세 가지 종류의 관계가 있다.

* **의존성**:리소스가 다른 리소스에 의존하는 관계, 즉 모든 관련 리소스가 저장소에 필요합니다.
* **회원(파일 시스템)**:특정 폴더 내에 리소스가 있는 관계.
* **사용자 지정**:리소스 간에 지정하는 관계. 예를 들어, 한 리소스가 더 이상 사용되지 않고 다른 리소스가 저장소에 도입된 경우 고유한 대체 관계를 지정할 수 있습니다.

자신만의 사용자 지정 관계를 만들 수 있습니다. 예를 들어, 저장소에 HTML 파일을 저장하고 이미지를 사용하는 경우, HTML 파일을 이미지와 연결하는 사용자 지정 관계를 지정할 수 있습니다(일반적으로 XML 파일만 저장소 정의 종속 관계를 사용하여 이미지와 연결되어 있음). 사용자 지정 관계의 또 다른 예는 트리 구조 대신 순환 그래프 구조를 사용하여 저장소의 다른 보기를 빌드하려는 경우입니다. 뷰어와 함께 원형 그래프를 정의하여 이러한 관계를 탐색할 수 있습니다. 마지막으로 두 리소스가 완전히 다른 경우에도 리소스가 다른 리소스를 대체한다고 표시할 수 있습니다. 이 경우 예약 범위를 벗어나는 관계 유형을 정의하고 두 리소스 간의 관계를 만들 수 있습니다. 귀하의 응용 프로그램은 관계를 감지하고 처리할 수 있는 유일한 클라이언트가 될 것이며 이 관계를 검색하는 데 사용될 수 있습니다.

저장소 서비스 Java API 또는 웹 서비스 API를 사용하여 리소스 간의 관계를 프로그래밍 방식으로 지정할 수 있습니다.

>[!NOTE]
>
>저장소 서비스에 대한 자세한 내용은 [AEM Forms에 대한 서비스 참조](https://www.adobe.com/go/learn_aemforms_services_63)를 참조하십시오.

### {#summary_of_steps-6} 단계 요약

두 리소스 간의 관계를 지정하려면 다음 단계를 수행합니다.

1. 프로젝트 파일 포함
1. 저장소 서비스 클라이언트를 만듭니다.
1. 관련된 리소스의 URI를 지정합니다.
1. 관계를 만듭니다.

**프로젝트 파일 포함**

개발 프로젝트에 필요한 파일을 포함합니다. Java를 사용하여 클라이언트 응용 프로그램을 만드는 경우 필요한 JAR 파일을 포함합니다. 웹 서비스를 사용하는 경우 프록시 파일을 포함하십시오.

**서비스 클라이언트 만들기**

프로그래밍 방식으로 리소스를 읽을 수 있으려면 먼저 연결을 설정하고 자격 증명을 제공해야 합니다. 이는 서비스 클라이언트를 만들어 완료합니다.

**연결할 리소스의 URI 지정**

관련된 리소스의 URI가 포함된 문자열을 만듭니다. 구문에는 다음과 같이 슬래시가 포함됩니다.&quot;/*path*/*resource*&quot;

**관계 만들기**

Repository service 메서드를 호출하여 관계 유형을 만들고 지정합니다.

**참고 항목**

[Java API를 사용하여 관계 리소스 만들기](aem-forms-repository.md#create-relationship-resources-using-the-java-api)

[웹 서비스 API를 사용하여 관계 리소스 만들기](aem-forms-repository.md#create-relationship-resources-using-the-web-service-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[저장소 서비스 API 빠른 시작](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### Java API {#create-relationship-resources-using-the-java-api}를 사용하여 관계 리소스 만들기

저장소 서비스 Java API를 사용하여 관계 리소스를 만드는 경우 다음 작업을 수행합니다.

1. 프로젝트 파일 포함

   Java 프로젝트의 클래스 경로에 클라이언트 JAR 파일을 포함합니다.

1. 서비스 클라이언트 만들기

   생성자를 사용하여 `ResourceRepositoryClient` 개체를 만들고 연결 속성이 포함된 `ServiceClientFactory` 개체를 전달합니다.

1. 연결할 리소스의 URI 지정

   관련된 리소스의 URI를 지정합니다. 이 경우 리소스의 이름은 `testResource1` 및 `testResource2`이며 이름이 `testFolder`인 폴더에 있으므로 해당 URI는 `"/testFolder/testResource1"` 및 `"/testFolder/testResource2"`입니다. URI는 `java.lang.String` 개체로 저장됩니다. 이 예에서 리소스는 먼저 저장소에 기록되고 해당 URI가 검색됩니다. 리소스 작성에 대한 자세한 내용은 [리소스 쓰기](aem-forms-repository.md#writing-resources)를 참조하십시오.

1. 관계 만들기

   `ResourceRepositoryClient` 개체의 `createRelationship` 메서드를 호출하고 다음 매개 변수를 전달합니다.

   * 소스 리소스의 URI입니다.
   * 대상 리소스의 URI입니다.
   * 관계 유형. `com.adobe.repository.infomodel.bean.Relation` 클래스에 있는 정적 상수 중 하나입니다. 이 예에서는 `Relation.TYPE_DEPENDANT_OF` 값을 지정하여 종속 관계가 설정됩니다.
   * 대상 리소스를 새 헤드 리소스의 `com.adobe.repository.infomodel.Id` 기반 식별자로 자동으로 업데이트할지 여부를 나타내는 `boolean` 값. 이 예에서는 종속 관계로 인해 `true` 값이 지정됩니다.

   `ResourceRepositoryClient` 개체의 `getRelated` 메서드를 호출하고 다음 매개 변수를 전달하여 해당 리소스에 대한 관련 리소스 목록을 검색할 수도 있습니다.

   * 관련 리소스를 검색할 리소스의 URI입니다. 이 예에서 소스 리소스( `"/testFolder/testResource1"`)가 지정됩니다.
   * 지정한 리소스가 관계의 소스 리소스인지 여부를 나타내는 `boolean` 값. 이 예에서 값 `true`은(는) 대/소문자이므로 지정됩니다.
   * 관계 유형 - `Relation` 클래스에 있는 정적 상수 중 하나입니다. 이 예에서는 앞서 사용한 것과 동일한 값을 사용하여 종속 관계를 지정합니다.`Relation.TYPE_DEPENDANT_OF`.

   `getRelated` 메서드는 관련된 각 리소스를 검색할 수 있도록 반복할 수 있는 `Resource` 개체의 `java.util.List`을 반환합니다. 이렇게 하면 `List`에 포함된 개체를 `Resource`로 캐스팅합니다. 이 예에서 `testResource2`은 반환된 리소스 목록에 있어야 합니다.

**참고 항목**

[리소스 관계 만들기](aem-forms-repository.md#creating-resource-relationships)

[빠른 시작(SOAP 모드):Java API를 사용하여 리소스 간 관계 만들기](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-creating-relationships-between-resources-using-the-java-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 웹 서비스 API {#create-relationship-resources-using-the-web-service-api}를 사용하여 관계 리소스 만들기

Repository API(웹 서비스)를 사용하여 관계 리소스를 만듭니다.

1. 프로젝트 파일 포함

   * 저장소 WSDL을 사용하는 Microsoft .NET 클라이언트 어셈블리를 만듭니다.
   * Microsoft .NET 클라이언트 어셈블리를 참조하십시오.

1. 서비스 클라이언트 만들기

   Microsoft .NET 클라이언트 어셈블리를 사용하여 기본 생성자를 호출하여 `RepositoryServiceService` 개체를 만듭니다. 사용자 이름과 암호를 포함하는 `System.Net.NetworkCredential` 개체를 사용하여 `Credentials` 속성을 설정합니다.

1. 연결할 리소스의 URI 지정

   관련된 리소스의 URI를 지정합니다. 이 경우 리소스의 이름은 `testResource1` 및 `testResource2`이며 이름이 `testFolder`인 폴더에 있으므로 해당 URI는 `"/testFolder/testResource1"` 및 `"/testFolder/testResource2"`입니다. Microsoft .NET Framework(예: C#)와 호환되는 언어를 사용하는 경우 URI가 `System.String` 개체로 저장됩니다. 이 예에서 리소스는 먼저 저장소에 기록되고 해당 URI가 검색됩니다. 리소스 작성에 대한 자세한 내용은 [리소스 쓰기](aem-forms-repository.md#writing-resources)를 참조하십시오.

1. 관계 만들기

   `RepositoryServiceService` 개체의 `createRelationship` 메서드를 호출하고 다음 매개 변수를 전달합니다.

   * 소스 리소스의 URI입니다.
   * 대상 리소스의 URI입니다.
   * 관계 유형. 이 예에서는 `3` 값을 지정하여 종속 관계가 설정됩니다.
   * 관계 유형이 지정되었는지 여부를 나타내는 `boolean` 값. 이 예에서 값 `true`이(가) 지정되었습니다.
   * 대상 리소스를 새 헤드 리소스의 `Id` 기반 식별자로 자동으로 업데이트할지 여부를 나타내는 `boolean` 값. 이 예에서는 종속 관계로 인해 `true` 값이 지정됩니다.
   * 대상 헤드가 지정되었는지 여부를 나타내는 `boolean` 값. 이 예에서 값 `true`이(가) 지정되었습니다.
   * 마지막 매개 변수에 `null`을(를) 전달합니다.

   `RepositoryServiceService` 개체의 `getRelated` 메서드를 호출하고 다음 매개 변수를 전달하여 해당 리소스에 대한 관련 리소스 목록을 검색할 수도 있습니다.

   * 관련 리소스를 검색할 리소스의 URI입니다. 이 예에서 소스 리소스( `"/testFolder/testResource1"`)가 지정됩니다.
   * 지정한 리소스가 관계의 소스 리소스인지 여부를 나타내는 `boolean` 값. 이 예에서 값 `true`은(는) 대/소문자이므로 지정됩니다.
   * 소스 리소스를 지정했는지 여부를 나타내는 `boolean` 값. 이 예에서 값 `true`이 제공됩니다.
   * 관계 유형을 포함하는 정수 배열. 이 예에서는 앞서 사용된 것과 동일한 값을 배열에 사용하여 종속 관계가 지정됩니다.`3`.
   * 나머지 두 매개 변수에 대해 `null`을(를) 전달합니다.

   `getRelated` 메서드는 관련된 각 리소스를 검색할 수 있도록 반복할 수 있는 `Resource` 개체에 캐스팅할 수 있는 개체 배열을 반환합니다. 이 예에서 `testResource2`은 반환된 리소스 목록에 있어야 합니다.

**참고 항목**

[리소스 관계 만들기](aem-forms-repository.md#creating-resource-relationships)

[Base64 인코딩을 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

## 리소스 잠금 {#locking-resources}

특정 사용자가 단독으로 사용하거나 두 명 이상의 사용자 간에 공유하기 위해 리소스 또는 리소스 세트를 잠글 수 있습니다. 공유 잠금은 리소스에서 어떤 일이 발생한다는 의미이지만 다른 사람이 해당 리소스에 대해 작업을 수행하는 것을 막지 않습니다. 공유 잠금은 신호 메커니즘으로 간주되어야 합니다. 배타적 잠금은 리소스를 잠근 사용자가 리소스를 변경하게 되며, 잠금은 사용자가 더 이상 리소스에 액세스할 필요가 없고 잠금을 해제하기 전까지 다른 사람이 그렇게 할 수 없도록 합니다. 저장소 관리자가 리소스를 잠금 해제하면 해당 리소스에 대한 모든 배타적 및 공유 잠금이 자동으로 제거됩니다. 이 유형의 작업은 사용자가 더 이상 사용할 수 없고 리소스의 잠금을 해제하지 않은 경우에 사용됩니다.

리소스가 잠기면 다음 그림과 같이 워크벤치에 있는 리소스 탭을 볼 때 잠금 아이콘이 표시됩니다.

![lr_lockrepository](assets/lr_lr_lockrepository.png)

저장소 서비스 Java API 또는 웹 서비스 API를 사용하여 리소스에 대한 액세스를 프로그래밍 방식으로 제어할 수 있습니다.

>[!NOTE]
>
>저장소 서비스에 대한 자세한 내용은 [AEM Forms에 대한 서비스 참조](https://www.adobe.com/go/learn_aemforms_services_63)를 참조하십시오.

### {#summary_of_steps-7} 단계 요약

리소스를 잠그고 잠금 해제하려면 다음 단계를 따르십시오.

1. 프로젝트 파일 포함
1. 저장소 서비스 클라이언트를 만듭니다.
1. 잠글 리소스의 URI를 지정합니다.
1. 리소스를 잠급니다.
1. 리소스에 대한 잠금을 검색합니다.
1. 리소스 잠금 해제

**프로젝트 파일 포함**

개발 프로젝트에 필요한 파일을 포함합니다. Java를 사용하여 클라이언트 응용 프로그램을 만드는 경우 필요한 JAR 파일을 포함합니다. 웹 서비스를 사용하는 경우 프록시 파일을 포함하십시오.

**서비스 클라이언트 만들기**

프로그래밍 방식으로 리소스를 읽을 수 있으려면 먼저 연결을 설정하고 자격 증명을 제공해야 합니다. 이는 서비스 클라이언트를 만들어 완료합니다.

**잠글 리소스의 URI 지정**

잠글 리소스의 URI가 포함된 문자열을 만듭니다. 구문에는 다음과 같이 슬래시가 포함됩니다.&quot;/*path*/*resource*&quot;

**리소스 잠금**

Repository service 메서드를 호출하여 리소스를 잠그고 URI, 잠금 유형 및 잠금 깊이를 지정합니다.

**리소스에 대한 잠금 검색**

Repository service 메서드를 호출하여 리소스에 대한 잠금을 검색하여 URI를 지정합니다.

**리소스 잠금 해제**

Repository service 메서드를 호출하여 리소스의 잠금을 해제하며 URI를 지정합니다.

**참고 항목**

[Java API를 사용하여 리소스 잠금](aem-forms-repository.md#lock-resources-using-the-java-api)

[웹 서비스 API를 사용하여 리소스 잠금](aem-forms-repository.md#lock-resources-using-the-web-service-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[저장소 서비스 API 빠른 시작](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### Java API {#lock-resources-using-the-java-api}를 사용하여 리소스 잠금

Repository service API(Java)를 사용하여 리소스 잠금:

1. 프로젝트 파일 포함

   Java 프로젝트의 클래스 경로에 클라이언트 JAR 파일을 포함합니다.

1. 서비스 클라이언트 만들기

   생성자를 사용하여 `ResourceRepositoryClient` 개체를 만들고 연결 속성이 포함된 `ServiceClientFactory` 개체를 전달합니다.

1. 잠글 리소스의 URI 지정

   잠글 리소스의 URI를 지정합니다. 이 경우 이름이 `testResource`인 리소스가 이름이 `testFolder`인 폴더에 있으므로 해당 URI는 `"/testFolder/testResource"`입니다. URI는 `java.lang.String` 개체로 저장됩니다.

1. 리소스 잠금

   `ResourceRepositoryClient` 개체의 `lockResource` 메서드를 호출하고 다음 매개 변수를 전달합니다.

   * 리소스의 URI입니다.
   * 잠금 범위 이 예에서 리소스는 독점적으로 사용할 수 있도록 잠기므로 잠금 범위는 `com.adobe.repository.infomodel.bean.Lock.SCOPE_EXCLUSIVE`으로 지정됩니다.
   * 잠금 깊이입니다. 이 예에서 잠금은 특정 리소스에만 적용되며 해당 멤버 또는 하위 리소스만 적용되지 않으므로 잠금 깊이는 `Lock.DEPTH_ZERO`으로 지정됩니다.

   >[!NOTE]
   >
   >4개의 매개 변수가 필요한 오버로드된 `lockResource` 메서드 버전에서는 예외가 발생합니다. 이 연습에서 보듯이 세 개의 매개 변수가 필요한 `lockResource` 메서드를 사용해야 합니다.

1. 리소스에 대한 잠금 검색

   `ResourceRepositoryClient` 개체의 `getLocks` 메서드를 호출하고 리소스의 URI를 매개 변수로 전달합니다. 이 메서드는 반복할 수 있는 List of Lock 객체를 반환합니다. 이 예에서 각 Lock 개체의 `getOwnerUserId`, `getDepth` 및 `getType` 메서드를 각각 호출하여 각 개체에 대해 잠금 소유자, 깊이 및 범위가 인쇄됩니다.

1. 리소스 잠금 해제

   `ResourceRepositoryClient` 개체의 `unlockResource` 메서드를 호출하고 리소스의 URI를 매개 변수로 전달합니다. 자세한 내용은 [AEM Forms API 참조](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)를 참조하십시오.

**참고 항목**

[리소스 잠금](aem-forms-repository.md#locking-resources)

[빠른 시작(SOAP 모드):Java API를 사용하여 리소스 잠금](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-locking-a-resource-using-the-java-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 웹 서비스 API {#lock-resources-using-the-web-service-api}를 사용하여 리소스 잠금

Repository service API(웹 서비스)를 사용하여 리소스 잠금:

1. 프로젝트 파일 포함

   * Base64를 사용하여 저장소 WSDL을 사용하는 Microsoft .NET 클라이언트 어셈블리를 만듭니다.
   * Microsoft .NET 클라이언트 어셈블리를 참조하십시오.

1. 서비스 클라이언트 만들기

   Microsoft .NET 클라이언트 어셈블리를 사용하여 기본 생성자를 호출하여 `RepositoryServiceService` 개체를 만듭니다. 사용자 이름과 암호를 포함하는 `System.Net.NetworkCredential` 개체를 사용하여 `Credentials` 속성을 설정합니다.

1. 잠글 리소스의 URI 지정

   잠글 리소스의 URI가 포함된 문자열을 지정합니다. 이 경우 이름이 `testResource`인 리소스가 `testFolder` 폴더에 있으므로 해당 URI는 `"/testFolder/testResource"`입니다. Microsoft .NET Framework(예: C#)와 호환되는 언어를 사용하는 경우 URI를 `System.String` 개체에 저장합니다.

1. 리소스 잠금

   `RepositoryServiceService` 개체의 `lockResource` 메서드를 호출하고 다음 매개 변수를 전달합니다.

   * 리소스의 URI입니다.
   * 잠금 범위 이 예에서 리소스는 독점적으로 사용할 수 있도록 잠기므로 잠금 범위는 `11`으로 지정됩니다.
   * 잠금 깊이입니다. 이 예에서 잠금은 특정 리소스에만 적용되며 해당 멤버 또는 하위 리소스만 적용되지 않으므로 잠금 깊이는 `2`으로 지정됩니다.
   * 잠금이 만료될 때까지 시간(초)을 나타내는 `int` 값. 이 예에서 `1000`의 값이 사용됩니다.
   * 마지막 매개 변수에 `null`을(를) 전달합니다.

1. 리소스에 대한 잠금 검색

   `RepositoryServiceService` 개체의 `getLocks` 메서드를 호출하고 리소스의 URI를 첫 번째 매개 변수로 전달하며 두 번째 매개 변수에는 `null`를 전달합니다. 이 메서드는 반복할 수 있는 `Lock` 개체를 포함하는 `object` 배열을 반환합니다. 이 예에서 각 `Lock` 개체의 `ownerUserId`, `depth` 및 `type` 필드에 각각 액세스하여 잠금 소유자, 깊이 및 범위가 각 개체에 대해 인쇄됩니다.

1. 리소스 잠금 해제

   `RepositoryServiceService` 개체의 `unlockResource` 메서드를 호출하고 리소스의 URI를 첫 번째 매개 변수로 전달하며 두 번째 매개 변수에는 `null`를 전달합니다.

**참고 항목**

[리소스 잠금](aem-forms-repository.md#locking-resources)

[Base64 인코딩을 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

## 리소스 {#deleting-resources} 삭제

저장소 서비스 Java API(SOAP)를 사용하여 저장소의 지정된 위치에서 프로그래밍 방식으로 리소스를 삭제할 수 있습니다.

리소스를 삭제할 때 삭제는 일반적으로 영구적입니다. 일부 경우 ECM 리포지토리는 작업 내역 메커니즘에 따라 리소스 버전을 저장할 수 있습니다. 따라서 리소스를 삭제할 때 해당 리소스가 다시는 필요하지 않은지 확인하는 것이 중요합니다. 리소스를 삭제하는 일반적인 이유는 데이터베이스의 사용 가능한 공간을 늘려야 하는 것입니다. 리소스 버전을 삭제할 수 있지만 삭제할 경우 리소스 식별자를 지정해야 하며, 리소스 식별자(LID)나 경로가 아닙니다. 폴더를 삭제하면 하위 폴더와 리소스를 비롯한 해당 폴더의 모든 내용이 자동으로 삭제됩니다.

관련 리소스는 삭제되지 않습니다. 예를 들어 logo.gif 파일을 사용하는 양식이 있고 logo.gif를 삭제하는 경우 관계는 보류 중인 관계 테이블에 저장됩니다. 버전 사용 중단의 대안으로 최신 버전의 개체 상태를 더 이상 사용되지 않도록 설정합니다.

삭제 작업은 ECM 시스템에서 트랜잭션 보안이 아닙니다. 예를 들어 100개의 리소스를 삭제하려고 시도했지만 50번째 리소스에서 작업이 실패하는 경우 처음 49개의 인스턴스가 삭제되지만 나머지 인스턴스는 삭제되지 않습니다. 그렇지 않으면 기본 동작은 롤백(비약정)입니다.

>[!NOTE]
>
>ECM 저장소(EMC Documentum Content Server 및 IBM FileNet P8 Content Manager)에서 `com.adobe.repository.bindings.dsc.client.ResourceRepositoryClient.deleteResources()` 메서드를 사용할 때, 지정된 리소스 중 하나에 대한 삭제가 실패할 경우 트랜잭션이 롤백되지 않으므로 삭제된 파일은 삭제할 수 없습니다.

>[!NOTE]
>
>저장소 서비스에 대한 자세한 내용은 [AEM Forms에 대한 서비스 참조](https://www.adobe.com/go/learn_aemforms_services_63)를 참조하십시오.

### {#summary_of_steps-8} 단계 요약

리소스를 삭제하려면 다음 단계를 따르십시오.

1. 프로젝트 파일 포함
1. 저장소 서비스 클라이언트를 만듭니다.
1. 삭제할 리소스의 URI를 지정합니다.
1. 리소스를 삭제합니다.

**프로젝트 파일 포함**

개발 프로젝트에 필요한 파일을 포함합니다. Java를 사용하여 클라이언트 응용 프로그램을 만드는 경우 필요한 JAR 파일을 포함합니다. 웹 서비스를 사용하는 경우 프록시 파일을 포함하십시오.

**서비스 클라이언트 만들기**

프로그래밍 방식으로 리소스를 읽을 수 있으려면 먼저 연결을 설정하고 자격 증명을 제공해야 합니다. 이는 서비스 클라이언트를 만들어 완료합니다.

**삭제할 리소스의 URI를 지정합니다.**

삭제할 리소스의 URI가 포함된 문자열을 만듭니다. 구문에는 다음과 같이 슬래시가 포함됩니다.&quot;/*path*/*resource*&quot; 삭제할 리소스가 폴더인 경우 삭제는 재귀적입니다.

**리소스 삭제**

Repository service 메서드를 호출하여 리소스를 삭제하고 URI를 지정합니다.

**참고 항목**

[Java API를 사용하여 리소스 삭제](aem-forms-repository.md#delete-resources-using-the-java-api-soap)

[웹 서비스 API를 사용하여 리소스 삭제](aem-forms-repository.md#delete-resources-using-the-web-service-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[저장소 서비스 API 빠른 시작](/help/forms/developing/repository-service-api-quick-starts.md#repository-service-api-quick-starts)

### Java API(SOAP) {#delete-resources-using-the-java-api-soap}을(를) 사용하여 리소스를 삭제합니다.

저장소 API(Java)를 사용하여 리소스를 삭제합니다.

1. 프로젝트 파일 포함

   Java 프로젝트의 클래스 경로에 클라이언트 JAR 파일을 포함합니다.

1. 서비스 클라이언트 만들기

   생성자를 사용하여 `ResourceRepositoryClient` 개체를 만들고 연결 속성이 포함된 `ServiceClientFactory` 개체를 전달합니다.

1. 삭제할 리소스의 URI를 지정합니다.

   검색할 리소스의 URI를 지정합니다. 이 경우 testResourceToBeDeleted라는 리소스가 testFolder라는 폴더에 있으므로 해당 URI는 `/testFolder/testResourceToBeDeleted`입니다. URI는 `java.lang.String` 개체로 저장됩니다. 이 예에서 리소스는 처음으로 저장소에 기록되고 해당 URI가 검색됩니다. 리소스 작성에 대한 자세한 내용은 [리소스 쓰기](aem-forms-repository.md#writing-resources)를 참조하십시오.

1. 리소스 삭제

   `ResourceRepositoryClient` 개체의 `deleteResource` 메서드를 호출하고 리소스의 URI를 매개 변수로 전달합니다.

**참고 항목**

[리소스 삭제](aem-forms-repository.md#deleting-resources)

[빠른 시작(SOAP 모드):Java API를 사용하여 리소스 검색](/help/forms/developing/repository-service-api-quick-starts.md#quick-start-soap-mode-searching-for-resources-using-the-java-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 웹 서비스 API {#delete-resources-using-the-web-service-api}를 사용하여 리소스 삭제

저장소 API(웹 서비스)를 사용하여 리소스를 삭제합니다.

1. 프로젝트 파일 포함

   * Base64를 사용하여 저장소 WSDL을 사용하는 Microsoft .NET 클라이언트 어셈블리를 만듭니다.
   * Microsoft .NET 클라이언트 어셈블리를 참조하십시오.

1. 서비스 클라이언트 만들기

   Microsoft .NET 클라이언트 어셈블리를 사용하여 기본 생성자를 호출하여 `RepositoryServiceService` 개체를 만듭니다. 사용자 이름과 암호를 포함하는 `System.Net.NetworkCredential` 개체를 사용하여 `Credentials` 속성을 설정합니다.

1. 삭제할 리소스의 URI를 지정합니다.

   검색할 리소스의 URI를 지정합니다. 이 경우 이름이 `testResourceToBeDeleted`인 리소스가 이름이 `testFolder`인 폴더에 있으므로 해당 URI는 `"/testFolder/testResourceToBeDeleted"`입니다. 이 예에서 리소스는 처음으로 저장소에 기록되고 해당 URI가 검색됩니다. 리소스 작성에 대한 자세한 내용은 [리소스 쓰기](aem-forms-repository.md#writing-resources)를 참조하십시오.

1. 리소스 삭제

   `RepositoryServiceService` 개체의 `deleteResources` 메서드를 호출하고 리소스의 URI가 포함된 `System.String` 배열을 첫 번째 매개 변수로 전달합니다. 두 번째 매개 변수에 `null`을(를) 전달합니다.

**참고 항목**

[리소스 삭제](aem-forms-repository.md#deleting-resources)

[Base64 인코딩을 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
