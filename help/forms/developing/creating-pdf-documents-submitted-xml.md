---
title: SubmittedXML 데이터를 사용하여 PDF 문서 만들기
seo-title: Creating PDF Documents with SubmittedXML Data
description: Forms 서비스를 사용하여 사용자가 대화형 양식에 입력한 양식 데이터를 검색합니다. 양식 데이터를 다른 AEM Forms 서비스 작업에 전달하고 데이터를 사용하여 PDF 문서를 만듭니다.
seo-description: Use the Forms service to retrieve the form data that the user entered into an interactive form. Pass the form data to another AEM Forms service operation and create a PDF document using the data.
uuid: 2676c614-8988-451b-ac7c-bd07731a3f5f
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 62490230-a24e-419d-95bb-c0bb04a03f96
role: Developer
exl-id: d9d5b94a-9d10-4d90-9e10-5142f30ba4a3
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1320'
ht-degree: 0%

---

# 제출된 XML 데이터를 사용하여 PDF 문서 만들기 {#creating-pdf-documents-with-submittedxml-data}

**이 문서의 샘플 및 예제는 JEE 환경의 AEM Forms용입니다.**

## 제출된 XML 데이터를 사용하여 PDF 문서 만들기 {#creating-pdf-documents-with-submitted-xml-data}

사용자가 대화형 양식을 채울 수 있도록 하는 웹 기반 응용 프로그램을 사용하려면 데이터를 서버에 다시 제출해야 합니다. Forms 서비스를 사용하여 사용자가 대화형 양식에 입력한 양식 데이터를 검색할 수 있습니다. 그런 다음 양식 데이터를 다른 AEM Forms 서비스 작업에 전달하고 데이터를 사용하여 PDF 문서를 만들 수 있습니다.

>[!NOTE]
>
>이 컨텐츠를 읽기 전에 제출된 양식 처리에 대한 이해를 높이는 것이 좋습니다. 양식 디자인과 제출된 XML 데이터 간의 관계와 같은 개념은 제출된 Forms 처리에서 다룹니다.

세 개의 AEM Forms 서비스를 포함하는 다음 워크플로우를 고려하십시오.

* 사용자가 웹 기반 애플리케이션에서 Forms 서비스로 XML 데이터를 제출합니다.
* Forms 서비스는 제출된 양식을 처리하고 양식 필드를 추출하는 데 사용됩니다. 양식 데이터를 처리할 수 있습니다. 예를 들어 데이터를 엔터프라이즈 데이터베이스에 제출할 수 있습니다.
* 양식 데이터는 비대화형 PDF 문서를 만들기 위해 출력 서비스로 전송됩니다.
* 비대화형 PDF 문서는 Content Services에 저장됩니다(더 이상 사용되지 않음).

다음 다이어그램은 이 워크플로우의 시각적 표현을 제공합니다.

![cd_cd_finsrv_architecture_xml_pdf1](assets/cd_cd_finsrv_architecture_xml_pdf1.png)

사용자가 클라이언트 웹 브라우저에서 양식을 제출하면 비대화형 PDF 문서는 Content Services에 저장됩니다(더 이상 사용되지 않음). 다음 그림은 컨텐츠 서비스에 저장된 PDF 문서를 보여줍니다(더 이상 사용되지 않음).

![cd_cd_cs_gui](assets/cd_cd_cs_gui.png)

### 단계 요약 {#summary-of-steps}

제출된 XML 데이터를 사용하여 비대화형 PDF 문서를 만들고 Content Services의 PDF 문서에 저장하려면 다음 작업을 수행하십시오.

1. 프로젝트 파일을 포함합니다.
1. Forms, 출력 및 문서 관리 개체를 만듭니다.
1. Forms 서비스를 사용하여 양식 데이터를 검색합니다.
1. 출력 서비스를 사용하여 비대화형 PDF 문서를 만듭니다.
1. 문서 관리 서비스를 사용하여 PDF 양식을 콘텐츠 서비스(더 이상 사용되지 않음)에 저장합니다.

**프로젝트 파일 포함**

개발 프로젝트에 필요한 파일을 포함합니다. Java를 사용하여 클라이언트 응용 프로그램을 만드는 경우 필요한 JAR 파일을 포함하십시오. 웹 서비스를 사용하는 경우 프록시 파일을 포함해야 합니다.

**Forms, 출력 및 문서 관리 개체 만들기**

Forms 서비스 API 작업을 프로그래밍 방식으로 수행하려면 먼저 Forms 클라이언트 API 개체를 만드십시오. 마찬가지로, 이 워크플로우는 출력 및 문서 관리 서비스를 호출하므로 출력 클라이언트 API 개체와 Document Management 클라이언트 API 개체를 모두 만듭니다.

**Forms 서비스를 사용하여 양식 데이터 검색**

Forms 서비스에 제출된 양식 데이터를 검색합니다. 비즈니스 요구 사항을 충족하기 위해 제출된 데이터를 처리할 수 있습니다. 예를 들어 엔터프라이즈 데이터베이스에 양식 데이터를 저장할 수 있습니다. 그러나 비대화형 PDF 문서를 만들기 위해 양식 데이터가 출력 서비스에 전달됩니다.

**출력 서비스를 사용하여 비대화형 PDF 문서를 만듭니다.**

출력 서비스를 사용하여 양식 디자인 및 XML 양식 데이터를 기반으로 하는 비대화형 PDF 문서를 만듭니다. 워크플로우에서 양식 데이터는 Forms 서비스에서 검색됩니다.

**문서 관리 서비스를 사용하여 PDF 양식을 Content Services(사용 중지)에 저장합니다**

문서 관리 서비스 API를 사용하여 PDF 문서를 Content Services에 저장합니다(더 이상 사용되지 않음).

**추가 참조**

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Forms 서비스 API 빠른 시작](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

### Java API를 사용하여 제출된 XML 데이터로 PDF 문서 만들기 {#create-a-pdf-document-with-submitted-xml-data-using-the-java-api}

Forms, 출력 및 문서 관리 API(Java)를 사용하여 제출된 XML 데이터를 사용하여 PDF 문서를 만듭니다.

1. 프로젝트 파일 포함

   Java 프로젝트의 클래스 경로에 adobe-forms-client.jar, adobe-output-client.jar 및 adobe-contentservices-client.jar 등의 클라이언트 JAR 파일을 포함합니다.

1. Forms, 출력 및 문서 관리 개체 만들기

   * 만들기 `ServiceClientFactory` 연결 속성을 포함하는 객체입니다.
   * 만들기 `FormsServiceClient` 생성자를 사용하여 객체를 전달하고 `ServiceClientFactory` 개체.
   * 만들기 `OutputClient` 생성자를 사용하여 객체를 전달하고 `ServiceClientFactory` 개체.
   * 만들기 `DocumentManagementServiceClientImpl` 생성자를 사용하여 객체를 전달하고 `ServiceClientFactory` 개체.

1. Forms 서비스를 사용하여 양식 데이터 검색

   * 를 호출합니다 `FormsServiceClient` 개체 `processFormSubmission` 메서드를 사용하여 다음 값을 전달합니다.

      * 다음 `com.adobe.idp.Document` 양식 데이터를 포함하는 객체입니다.
      * 모든 관련 HTTP 헤더를 포함하여 환경 변수를 지정하는 문자열 값입니다. 에 대해 하나 이상의 값을 지정하여 처리할 콘텐츠 유형을 지정합니다. `CONTENT_TYPE` 환경 변수 입니다. 예를 들어 XML 데이터를 처리하려면 이 매개 변수에 다음 문자열 값을 지정합니다. `CONTENT_TYPE=text/xml`.
      * 를 지정하는 문자열 값 `HTTP_USER_AGENT` 헤더 값(예: ) `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`.
      * A `RenderOptionsSpec` 런타임 옵션을 저장하는 개체입니다.

      다음 `processFormSubmission` 메서드 반환 `FormsResult` 양식 제출 결과가 포함된 객체입니다.

   * 를 호출하여 Forms 서비스가 양식 데이터 처리를 완료했는지 여부를 결정합니다 `FormsResult` 개체 `getAction` 메서드를 사용합니다. 이 메서드가 값을 반환하는 경우 `0`: 데이터를 처리할 준비가 되었습니다.
   * 양식 데이터를 검색하려면 `com.adobe.idp.Document` 객체를 호출하여 `FormsResult` 개체 `getOutputContent` 메서드를 사용합니다. 이 개체에는 출력 서비스로 전송할 수 있는 양식 데이터가 포함되어 있습니다.
   * 만들기 `java.io.InputStream` 객체를 호출하여 `java.io.DataInputStream` 생성자 및 전달 `com.adobe.idp.Document` 개체.
   * 만들기 `org.w3c.dom.DocumentBuilderFactory` 정적 `org.w3c.dom.DocumentBuilderFactory` 개체 `newInstance` 메서드를 사용합니다.
   * 만들기 `org.w3c.dom.DocumentBuilder` 객체를 호출하여 `org.w3c.dom.DocumentBuilderFactory` 개체 `newDocumentBuilder` 메서드를 사용합니다.
   * 만들기 `org.w3c.dom.Document` 객체를 호출하여 `org.w3c.dom.DocumentBuilder` 개체 `parse` 메서드 및 전달 `java.io.InputStream` 개체.
   * XML 문서 내에서 각 노드의 값을 검색합니다. 이 작업을 수행하는 한 가지 방법은 두 개의 매개 변수를 허용하는 사용자 지정 메서드를 만드는 것입니다. a `org.w3c.dom.Document` 객체 및 검색할 값이 있는 노드의 이름입니다. 이 메서드는 노드의 값을 나타내는 문자열 값을 반환합니다. 이 프로세스를 따르는 코드 예제에서 이 사용자 지정 메서드는 라고 합니다 `getNodeText`. 이 메서드의 본문이 표시됩니다.


1. 출력 서비스를 사용하여 비대화형 PDF 문서를 만듭니다.

   를 호출하여 PDF 문서 만들기 `OutputClient` 개체 `generatePDFOutput` 메서드 및 다음 값 전달:

   * A `TransformationFormat` 열거형 값. PDF 문서를 생성하려면 `TransformationFormat.PDF`.
   * 양식 디자인의 이름을 지정하는 문자열 값입니다. 양식 디자인이 Forms 서비스에서 검색한 양식 데이터와 호환되는지 확인합니다.
   * 양식 디자인이 있는 컨텐츠 루트를 지정하는 문자열 값입니다.
   * A `PDFOutputOptionsSpec` PDF 런타임 옵션이 포함된 객체입니다.
   * A `RenderOptionsSpec` 렌더링 런타임 옵션이 포함된 객체입니다.
   * 다음 `com.adobe.idp.Document` 폼 디자인과 병합할 데이터가 포함된 XML 데이터 소스를 포함하는 개체입니다. 이 개체가 `FormsResult` 개체 `getOutputContent` 메서드를 사용합니다.
   * 다음 `generatePDFOutput` 메서드 반환 `OutputResult` 작업 결과가 포함된 객체입니다.
   * 비대화형 PDF 문서를 호출하여 검색합니다. `OutputResult` 개체 `getGeneratedDoc` 메서드를 사용합니다. 이 메서드는 `com.adobe.idp.Document` 비대화형 PDF 문서를 나타내는 인스턴스입니다.

1. 문서 관리 서비스를 사용하여 콘텐츠 서비스(사용 중지)에 PDF 양식을 저장합니다

   을 호출하여 컨텐츠를 추가합니다 `DocumentManagementServiceClientImpl` 개체 `storeContent` 메서드 및 다음 값 전달:

   * 컨텐츠가 추가되는 저장소를 지정하는 문자열 값입니다. 기본 저장소는 다음과 같습니다. `SpacesStore`. 이 값은 필수 매개 변수입니다.
   * 컨텐츠가 추가되는 공간의 정규화된 경로를 지정하는 문자열 값입니다(예: `/Company Home/Test Directory`). 이 값은 필수 매개 변수입니다.
   * 새 컨텐츠를 나타내는 노드 이름(예: `MortgageForm.pdf`). 이 값은 필수 매개 변수입니다.
   * 노드 유형을 지정하는 문자열 값입니다. PDF 파일과 같은 새 컨텐츠를 추가하려면 `{https://www.alfresco.org/model/content/1.0}content`. 이 값은 필수 매개 변수입니다.
   * A `com.adobe.idp.Document` 컨텐츠를 나타내는 개체입니다. 이 값은 필수 매개 변수입니다.
   * 인코딩 값을 지정하는 문자열 값(예: `UTF-8`). 이 값은 필수 매개 변수입니다.
   * An `UpdateVersionType` 버전 정보를 처리하는 방법을 지정하는 열거형 값(예: `UpdateVersionType.INCREMENT_MAJOR_VERSION` 컨텐츠 버전을 증가시킵니다. ) 이 값은 필수 매개 변수입니다.
   * A `java.util.List` 컨텐츠와 관련된 측면을 지정하는 인스턴스입니다. 이 값은 선택적 매개 변수이며 `null`.
   * A `java.util.Map` 컨텐트 속성을 저장하는 객체입니다.

   다음 `storeContent` 메서드 반환 `CRCResult` 컨텐츠를 설명하는 개체입니다. 사용 `CRCResult` 예를 들어 컨텐츠의 고유 식별자 값을 가져올 수 있습니다. 이 작업을 수행하려면 `CRCResult` 개체 `getNodeUuid` 메서드를 사용합니다.

**추가 참조**

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)
