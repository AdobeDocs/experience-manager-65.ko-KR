---
title: CustomToolbars를 사용하여 HTML Forms 렌더링
description: Forms 서비스를 사용하여 HTML 양식으로 렌더링되는 도구 모음을 사용자 지정할 수 있습니다. Java API 및 웹 서비스 API를 사용하여 사용자 지정 도구 모음으로 HTML 양식을 렌더링할 수 있습니다.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
exl-id: 0b992b1c-3878-447a-bccc-7034aa3e98bc
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Document Services,APIs & Integrations
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '2328'
ht-degree: 0%

---

# CustomToolbars를 사용하여 HTML Forms 렌더링 {#rendering-html-forms-with-customtoolbars}

**이 문서의 샘플 및 예제는 JEE 환경의 AEM Forms에 대해서만 적용됩니다.**

## 사용자 지정 도구 모음으로 HTML Forms 렌더링 {#rendering-html-forms-with-custom-toolbars}

Forms 서비스를 사용하면 HTML 양식으로 렌더링되는 도구 모음을 사용자 지정할 수 있습니다. 기본 CSS 스타일을 재정의하여 모양을 변경하고 Java 스크립트를 재정의하여 동적 동작을 추가하도록 도구 모음을 사용자 지정할 수 있습니다. fscmenu.xml이라는 XML 파일을 사용하여 도구 모음을 사용자 지정합니다. 기본적으로 Forms 서비스는 내부적으로 지정된 URI 위치에서 이 파일을 검색합니다.

>[!NOTE]
>
>이 URI 위치는 adobe-forms-dsc.jar 파일에 있는 adobe-forms-core.jar 파일에 있습니다. adobe-forms-dsc.jar 파일은 C:\Adobe\Adobe_Experience_Manager_forms\ 폴더에 있습니다(C:\은 설치 디렉토리). Win RAR과 같은 파일 추출 도구를 사용하여 adobe를 열 수 있습니다.

이 위치에서 fscmenu.xml을 복사하고 요구 사항에 맞게 수정한 다음 사용자 지정 URI 위치에 배치할 수 있습니다. 그런 다음 Forms 서비스 API를 사용하여 지정된 위치에서 fscmenu.xml 파일을 사용하여 Forms 서비스를 생성하는 런타임 옵션을 설정합니다. 이러한 작업을 수행하면 Forms 서비스에서 사용자 지정 도구 모음이 있는 HTML 양식을 렌더링합니다.

fscmenu.xml 파일 외에 다음 파일도 가져와야 합니다.

* fscmenu.js
* fscattachments.js
* fscmenu.css
* fscmenu-v.css
* fscmenu-ie.css
* fscdialog.css

fscJS는 각 노드와 연결된 Java 스크립트입니다. 다음에 대해 하나를 제공해야 합니다. `div#fscmenu` 노드 및 (선택 사항) `ul#fscmenuItem` 노드. JS 파일은 핵심 도구 모음 기능을 구현하며 기본 파일이 작동합니다.

fscCSS는 특정 노드와 연결된 스타일 시트입니다. CSS 파일의 스타일은 도구 모음 모양을 지정합니다. *fscVCSS* 은 렌더링된 HTML 양식의 왼쪽에 표시되는 세로 도구 모음의 스타일시트입니다. *fscIECSS* 는 Internet Explorer에서 렌더링되는 HTML 양식에 사용되는 스타일시트입니다.

위의 모든 파일이 fscmenu.xml 파일에서 참조되는지 확인합니다. 즉, fscmenu.xml 파일에서 이러한 파일을 가리키는 URI 위치를 지정하여 Forms 서비스가 해당 파일을 찾을 수 있도록 합니다. 기본적으로 이러한 파일은 내부 키워드로 시작하는 URI 위치에서 사용할 수 있습니다 `FSWebRoot` 또는 `ApplicationWebRoot`.

도구 모음을 사용자 지정하려면 외부 키워드를 사용하여 키워드를 바꿉니다 `FSToolBarURI`. 이 키워드는 런타임에 Forms 서비스로 전달되는 URI를 나타냅니다(이 접근 방식은 이 섹션의 뒷부분에 표시됨).

이러한 JS 및 CSS 파일의 절대 위치를 지정할 수도 있습니다(예: https://www.mycompany.com/scripts/misc/fscmenu.js). 이 경우에는 를 사용할 필요가 없습니다 `FSToolBarURI` 키워드.

>[!NOTE]
>
>이러한 파일을 참조하는 방식을 혼합하지 않는 것이 좋습니다. 즉, 다음 중 하나를 사용하여 모든 URI를 참조해야 합니다. `FSToolBarURI` 키워드 또는 절대 위치입니다.

adobe-forms를 열어 JS 및 CSS 파일을 가져올 수 있습니다.&lt;appserver>.ear 파일입니다. 이 파일 내에서 adobe-forms-res.war를 엽니다. 이 모든 파일은 WAR 파일에 있습니다. Adobe-forms-&lt;appserver>.ear 파일은 AEM forms 설치 폴더에 있습니다(C:\ 는 설치 디렉토리). adobe-forms를 열 수 있습니다.&lt;appserver>WinRAR과 같은 파일 추출 도구를 사용하는 .ear.

다음 XML 구문은 fscmenu.xml 파일의 예를 보여 줍니다.

```html
 <div id="fscmenu" fscJS="FSToolBarURI/scripts/fscmenu.js" fscCSS="FSToolBarURI/fscmenu.css" fscVCSS="FSToolBarURI/fscmenu-v.css" fscIECSS="FSToolBarURI/fscmenu-ie.css">
         <ul class="fscmenuItem" id="Home">
             <li>
                 <a href="#" fscTarget="_top" tabindex="1">Home</a>
             </li>
         </ul>
         <ul class="fscmenuItem" id="Upload" fscJS="FSToolBarURI/scripts/fscattachments.js" fscCSS="FSToolBarURI/fscdialog.css">
             <li>
                 <a tabindex="2">Upload Attachments</a>
                 <ul class="fscmenuPopup" id="fscUploadAttachments">
                     <li>
                         <a href="javascript:doUploadDialog();" tabindex="3">Add ...</a>
                     </li>
                     <li>
                         <a href="javascript:doDeleteDialog();" tabindex="4">Delete ...</a>
                     </li>
                 </ul>
             </li>
         </ul>
         <ul class="fscmenuItem" id="Download">
             <li>
                 <a tabindex="100">Download Attachments</a>
                 <ul class="fscmenuPopup">
                     <li>
                         <a tabindex="101">None available</a>
                     </li>
                 </ul>
             </li>
         </ul>
     </div>
```

>[!NOTE]
>
>굵은 텍스트는 참조해야 하는 CSS 및 JS 파일에 대한 URI를 나타냅니다.

다음 항목에서는 도구 모음을 사용자 지정하는 방법을 설명합니다.

* 값 변경 `fscJS`, `fscCSS`, `fscVCSS`, `fscIECSS` 이 섹션에 설명된 방법 중 하나를 사용하여 참조된 파일의 사용자 지정 위치를 반영하도록 fscmenu.xml 파일에 있는 속성(예: `fscJS="FSToolBarURI/scripts/fscmenu.js"`).
* 모든 CSS 및 JS 파일을 지정해야 합니다. 파일이 수정되지 않은 경우 사용자 지정 위치에 기본 파일을 제공합니다. 이 섹션에 설명된 대로 다양한 파일을 열어 기본 파일을 가져올 수 있습니다.
* 모든 파일에 대한 절대 참조(예: https://www.example.com/scripts/custom-vertical-fscmenu.css)를 제공할 수 있습니다.
* 가 만드는 JS 및 CSS 파일 `div#fscmenu` 노드는 도구 모음 기능에 필수적입니다. 개인 `ul#fscmenuItem` 노드에 지원되는 JS 또는 CSS 파일이 있거나 없을 수 있습니다.

**로컬 값 변경**

도구 모음 사용자 지정의 일부로 도구 모음의 로케일 값을 변경할 수 있습니다. 즉, 다른 언어로 표시할 수 있습니다. 다음 그림은 프랑스어로 표시되는 사용자 지정 도구 모음을 보여 줍니다.

>[!NOTE]
>
>두 개 이상의 언어로 사용자 지정 도구 모음을 만들 수 없습니다. 도구 모음은 로케일 설정에 따라 다른 XML 파일을 사용할 수 없습니다.

도구 모음의 로케일 값을 변경하려면 fscmenu.xml 파일에 표시할 언어가 포함되어 있는지 확인합니다. 다음 XML 구문은 프랑스어 도구 모음을 표시하는 데 사용되는 fscmenu.xml 파일을 보여 줍니다.

```html
 <div id="fscmenu" fscJS="FSToolBarURI/scripts/fscmenu.js" fscCSS="FSToolBarURI/fscmenu.css" fscVCSS="FSToolBarURI/fscmenu-v.css" fscIECSS="FSToolBarURI/fscmenu-ie.css">
         <ul class="fscmenuItem" id="Home">
             <li>
                 <a href="#" fscTarget="_top" tabindex="1">Accueil</a>
             </li>
         </ul>
         <ul class="fscmenuItem" id="Upload" fscJS="FSToolBarURI/scripts/fscattachments.js" fscCSS="FSToolBarURI/fscdialog.css">
             <li>
                 <a tabindex="2">Télécharger les pièces jointes</a>
                 <ul class="fscmenuPopup" id="fscUploadAttachments">
                     <li>
                         <a href="javascript:doUploadDialog();" tabindex="3">Ajouter...</a>
                     </li>
                     <li>
                         <a href="javascript:doDeleteDialog();" tabindex="4">Supprimer...</a>
                     </li>
                 </ul>
             </li>
         </ul>
         <ul class="fscmenuItem" id="Download">
             <li>
                 <a tabindex="100">Télécharger les pièces jointes</a>
                 <ul class="fscmenuPopup">
                     <li>
                         <a tabindex="101">Aucune disponible</a>
                     </li>
                 </ul>
             </li>
         </ul>
     </div>
```

>[!NOTE]
>
>이 섹션과 연관된 빠른 시작은 이 XML 파일을 사용하여 이전 그림과 같이 프랑스어 사용자 정의 도구 모음을 표시합니다.

또한 `HTMLRenderSpec` 개체 `setLocale` 메서드 및 로케일 값을 지정하는 문자열 값 전달 예를 들어 를 전달합니다 `fr_FR` 프랑스어를 지정합니다. Forms 서비스는 현지화된 도구 모음과 함께 번들로 제공됩니다.

>[!NOTE]
>
>사용자 지정 도구 모음을 사용하는 HTML 양식을 렌더링하기 전에 HTML 양식이 렌더링되는 방법을 알아야 합니다. (참조: [Forms을 HTML으로 렌더링](/help/forms/developing/rendering-forms-html.md).)

Forms 서비스에 대한 자세한 내용은 [AEM Forms에 대한 서비스 참조](https://www.adobe.com/go/learn_aemforms_services_63).

### 단계 요약 {#summary-of-steps}

사용자 지정 도구 모음이 포함된 HTML 양식을 렌더링하려면 다음 작업을 수행합니다.

1. 프로젝트 파일을 포함합니다.
1. Forms Java API 개체를 만듭니다.
1. 사용자 지정 fscmenu XML 파일을 참조합니다.
1. HTML 양식 렌더링
1. 양식 데이터 스트림을 클라이언트 웹 브라우저에 작성합니다.

**프로젝트 파일 포함**

개발 프로젝트에 필요한 파일을 포함합니다. Java를 사용하여 클라이언트 응용 프로그램을 만드는 경우 필요한 JAR 파일을 포함합니다. 웹 서비스를 사용하는 경우 프록시 파일을 포함합니다.

**Forms Java API 개체 만들기**

Forms 서비스에서 지원하는 작업을 프로그래밍 방식으로 수행하려면 먼저 Forms 클라이언트 개체를 만들어야 합니다.

**사용자 지정 fscmenu XML 파일 참조**

사용자 지정 도구 모음이 포함된 HTML 양식을 렌더링하려면 도구 모음을 설명하는 fscmenu XML 파일을 참조하십시오. 이 단원에서는 fscmenu XML 파일의 두 가지 예를 제공합니다. 또한 fscmenu.xml 파일이 참조된 모든 파일의 위치를 올바르게 지정하는지 확인합니다. 이 섹션의 앞부분에서 언급했듯이 `FSToolBarURI` 키워드 또는 절대 위치.

**HTML 양식 렌더링**

HTML 양식을 렌더링하려면 Designer에서 작성하여 XDP 파일로 저장한 양식 디자인을 지정합니다. HTML 변환 유형도 선택합니다. 예를 들어 Internet Explorer 5.0 이상의 동적 HTML을 렌더링하는 HTML 변환 유형을 지정할 수 있습니다.

HTML 양식을 렌더링하려면 다른 양식 유형을 렌더링하기 위한 URI 값과 같은 값도 필요합니다.

**클라이언트 웹 브라우저에 양식 데이터 스트림 작성**

Forms 서비스에서 HTML 양식을 렌더링할 때 사용자가 HTML 양식을 볼 수 있도록 클라이언트 웹 브라우저에 작성해야 하는 양식 데이터 스트림을 반환합니다.

**추가 참조**

[Java API를 사용하여 사용자 지정 도구 모음으로 HTML 양식 렌더링](#render-an-html-form-with-a-custom-toolbar-using-the-java-api)

[웹 서비스 API를 사용하여 사용자 지정 도구 모음으로 HTML 양식 렌더링](#rendering-an-html-form-with-a-custom-toolbar-using-the-web-service-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Forms 서비스 API 빠른 시작](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[대화형 PDF forms 렌더링](/help/forms/developing/rendering-interactive-pdf-forms.md)

[Forms을 HTML으로 렌더링](/help/forms/developing/rendering-forms-html.md)

[Forms을 렌더링하는 웹 애플리케이션 만들기](/help/forms/developing/creating-web-applications-renders-forms.md)

### Java API를 사용하여 사용자 지정 도구 모음으로 HTML 양식 렌더링 {#render-an-html-form-with-a-custom-toolbar-using-the-java-api}

Forms 서비스 API(Java)를 사용하여 사용자 지정 도구 모음이 포함된 HTML 양식을 렌더링합니다.

1. 프로젝트 파일 포함

   Java 프로젝트의 클래스 경로에 adobe-forms-client.jar과 같은 클라이언트 JAR 파일을 포함합니다.

1. Forms Java API 개체 만들기

   * 만들기 `ServiceClientFactory` 연결 속성을 포함하는 개체입니다.
   * 만들기 `FormsServiceClient` 개체를 생성자를 사용하고 `ServiceClientFactory` 개체.

1. 사용자 지정 fscmenu XML 파일 참조

   * 만들기 `HTMLRenderSpec` 개체를 만들 때 사용됩니다.
   * 도구 모음으로 HTML 양식을 렌더링하려면 `HTMLRenderSpec` 개체 `setHTMLToolbar` 방법 및 전달 `HTMLToolbar` 열거형 값입니다. 예를 들어 세로 HTML 도구 모음을 표시하려면 를 전달합니다 `HTMLToolbar.Vertical`.
   * 다음을 호출하여 fscmenu XML 파일의 위치를 지정합니다. `HTMLRenderSpec` 개체 `setToolbarURI` 메서드 및 XML 파일의 URI 위치를 지정하는 문자열 값 전달
   * 해당하는 경우 `HTMLRenderSpec` 개체 `setLocale` 메서드 및 로케일 값을 지정하는 문자열 값 전달 기본값은 영어입니다.

   >[!NOTE]
   >
   >이 섹션과 연결된 빠른 시작은 이 값을 로 설정합니다. `fr_FR`*.*

1. HTML 양식 렌더링

   호출 `FormsServiceClient` 개체 `renderHTMLForm` 메서드를 실행하고 다음 값을 전달합니다.

   * 파일 이름 확장명을 포함하여 양식 디자인 이름을 지정하는 문자열 값입니다. Forms 애플리케이션의 일부인 양식 디자인을 참조하는 경우 다음과 같은 전체 경로를 지정해야 합니다. `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * A `TransformTo` HTML 환경 설정 유형을 지정하는 열거형 값입니다. 예를 들어, Internet Explorer 5.0 이상의 동적 HTML과 호환되는 HTML 양식을 렌더링하려면 다음을 지정합니다 `TransformTo.MSDHTML`.
   * A `com.adobe.idp.Document` 양식과 병합할 데이터가 포함된 개체입니다. 데이터를 병합하지 않으려면 비워 둡니다. `com.adobe.idp.Document` 개체.
   * 다음 `HTMLRenderSpec` HTML 런타임 옵션을 저장하는 개체입니다.
   * 다음을 지정하는 문자열 값 `HTTP_USER_AGENT` 헤더 값(예: ) `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322)`.
   * A `URLSpec` HTML 양식을 렌더링하는 데 필요한 URI 값을 저장하는 개체입니다.
   * A `java.util.HashMap` 첨부 파일을 저장하는 객체입니다. 이는 선택적 매개 변수이며 다음을 지정할 수 있습니다. `null` 양식에 파일을 첨부하지 않으려면.

   다음 `renderHTMLForm` 메서드가 을 반환합니다. `FormsResult` 클라이언트 웹 브라우저에 작성해야 하는 양식 데이터 스트림이 포함된 개체입니다.

1. 클라이언트 웹 브라우저에 양식 데이터 스트림 작성

   * 만들기 `com.adobe.idp.Document` 를 호출하여 개체 `FormsResult` 개체 &#39;s `getOutputContent` 메서드를 사용합니다.
   * 의 콘텐츠 유형 가져오기 `com.adobe.idp.Document` 개체 `getContentType` 메서드를 사용합니다.
   * 설정 `javax.servlet.http.HttpServletResponse` 를 호출하여 객체의 콘텐츠 유형 `setContentType` 메서드와 의 콘텐츠 유형 전달 `com.adobe.idp.Document` 개체.
   * 만들기 `javax.servlet.ServletOutputStream` 를 호출하여 양식 데이터 스트림을 클라이언트 웹 브라우저에 작성하는 데 사용되는 개체 `javax.servlet.http.HttpServletResponse` 개체 `getOutputStream` 메서드를 사용합니다.
   * 만들기 `java.io.InputStream` 를 호출하여 개체 `com.adobe.idp.Document` 개체 `getInputStream` 메서드를 사용합니다.
   * 바이트 배열을 만들고 `InputStream` 개체 `read` 메서드에서 바이트 배열을 인수로 전달합니다.
   * 호출 `javax.servlet.ServletOutputStream` 개체 `write` 클라이언트 웹 브라우저에 양식 데이터 스트림을 전송하는 방법입니다. 바이트 배열을 로 전달 `write` 메서드를 사용합니다.

**추가 참조**

[빠른 시작(SOAP 모드): Java API를 사용하여 사용자 지정 도구 모음으로 HTML 양식 렌더링](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-rendering-an-html-form-with-a-custom-toolbar-using-the-java-api)

[AEM Forms Java 라이브러리 파일 포함](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[연결 속성 설정](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### 웹 서비스 API를 사용하여 사용자 지정 도구 모음으로 HTML 양식 렌더링 {#rendering-an-html-form-with-a-custom-toolbar-using-the-web-service-api}

Forms 서비스 API(웹 서비스)를 사용하여 사용자 지정 도구 모음이 포함된 HTML 양식을 렌더링합니다.

1. 프로젝트 파일 포함

   * Forms 서비스 WSDL을 사용하는 Java 프록시 클래스를 만듭니다.
   * 클래스 경로에 Java 프록시 클래스를 포함합니다.

1. Forms Java API 개체 만들기

   만들기 `FormsService` 개체로 설정하고 인증 값을 설정합니다.

1. 사용자 지정 fscmenu XML 파일 참조

   * 만들기 `HTMLRenderSpec` 개체를 만들 때 사용됩니다.
   * 도구 모음으로 HTML 양식을 렌더링하려면 `HTMLRenderSpec` 개체 `setHTMLToolbar` 방법 및 전달 `HTMLToolbar` 열거형 값입니다. 예를 들어 세로 HTML 도구 모음을 표시하려면 를 전달합니다 `HTMLToolbar.Vertical`.
   * 다음을 호출하여 fscmenu XML 파일의 위치를 지정합니다. `HTMLRenderSpec` 개체 `setToolbarURI` 메서드 및 XML 파일의 URI 위치를 지정하는 문자열 값 전달
   * 해당하는 경우 `HTMLRenderSpec` 개체 `setLocale` 메서드 및 로케일 값을 지정하는 문자열 값 전달 기본값은 영어입니다.

   >[!NOTE]
   >
   >이 섹션과 연결된 빠른 시작은 이 값을 로 설정합니다. `fr_FR`*.*

1. HTML 양식 렌더링

   호출 `FormsService` 개체 `renderHTMLForm` 메서드를 실행하고 다음 값을 전달합니다.

   * 파일 이름 확장명을 포함하여 양식 디자인 이름을 지정하는 문자열 값입니다. Forms 애플리케이션의 일부인 양식 디자인을 참조하는 경우 다음과 같은 전체 경로를 지정해야 합니다. `Applications/FormsApplication/1.0/FormsFolder/Loan.xdp`.
   * A `TransformTo` HTML 환경 설정 유형을 지정하는 열거형 값입니다. 예를 들어, Internet Explorer 5.0 이상의 동적 HTML과 호환되는 HTML 양식을 렌더링하려면 다음을 지정합니다 `TransformTo.MSDHTML`.
   * A `BLOB` 양식과 병합할 데이터가 포함된 개체입니다. 데이터를 병합하지 않으려면 를 전달합니다. `null`.
   * 다음 `HTMLRenderSpec` HTML 런타임 옵션을 저장하는 개체입니다.
   * 다음을 지정하는 문자열 값 `HTTP_USER_AGENT` 헤더 값(예: ) `Mozilla/4.0 (compatible; MSIE 6.0; Windows NT 5.1; SV1; .NET CLR 1.1.4322`). 이 값을 설정하지 않으려는 경우 빈 문자열을 전달할 수 있습니다.
   * A `URLSpec` HTML 양식을 렌더링하는 데 필요한 URI 값을 저장하는 개체입니다.
   * A `java.util.HashMap` 첨부 파일을 저장하는 객체입니다. 이 매개 변수는 선택 사항이며 다음을 지정할 수 있습니다 `null` 양식에 파일을 첨부하지 않으려는 경우.
   * 비어 있음 `com.adobe.idp.services.holders.BLOBHolder` 로 채워지는 개체 `renderHTMLForm` 메서드를 사용합니다. 이 매개 변수 값은 렌더링된 양식을 저장합니다.
   * 비어 있음 `com.adobe.idp.services.holders.BLOBHolder` 로 채워지는 개체 `renderHTMLForm` 메서드를 사용합니다. 이 매개 변수는 출력 XML 데이터를 저장합니다.
   * 비어 있음 `javax.xml.rpc.holders.LongHolder` 로 채워지는 개체 `renderHTMLForm` 메서드를 사용합니다. 이 인수는 양식의 페이지 수를 저장합니다.
   * 비어 있음 `javax.xml.rpc.holders.StringHolder` 로 채워지는 개체 `renderHTMLForm` 메서드를 사용합니다. 이 인수는 로케일 값을 저장합니다.
   * 비어 있음 `javax.xml.rpc.holders.StringHolder` 로 채워지는 개체 `renderHTMLForm` 메서드를 사용합니다. 이 인수는 사용되는 HTML 렌더링 값을 저장합니다.
   * 비어 있음 `com.adobe.idp.services.holders.FormsResultHolder` 이 작업의 결과를 포함할 개체입니다.

   다음 `renderHTMLForm` 메서드는 `com.adobe.idp.services.holders.FormsResultHolder` 클라이언트 웹 브라우저에 작성해야 하는 양식 데이터 스트림을 사용하여 마지막 인수 값으로 전달되는 개체입니다.

1. 클라이언트 웹 브라우저에 양식 데이터 스트림 작성

   * 만들기 `FormResult` 의 값을 가져와서 개체 `com.adobe.idp.services.holders.FormsResultHolder` 개체 `value` 데이터 구성원입니다.
   * 만들기 `BLOB` 를 호출하여 양식 데이터를 포함하는 개체 `FormsResult` 개체 `getOutputContent` 메서드를 사용합니다.
   * 의 콘텐츠 유형 가져오기 `BLOB` 개체 `getContentType` 메서드를 사용합니다.
   * 설정 `javax.servlet.http.HttpServletResponse` 를 호출하여 객체의 콘텐츠 유형 `setContentType` 메서드와 의 콘텐츠 유형 전달 `BLOB` 개체.
   * 만들기 `javax.servlet.ServletOutputStream` 를 호출하여 양식 데이터 스트림을 클라이언트 웹 브라우저에 작성하는 데 사용되는 개체 `javax.servlet.http.HttpServletResponse` 개체 `getOutputStream` 메서드를 사용합니다.
   * 바이트 배열을 만들고 `BLOB` 개체 `getBinaryData` 메서드를 사용합니다. 이 작업은 의 콘텐츠를 할당합니다. `FormsResult` 개체를 바이트 배열에 추가합니다.
   * 호출 `javax.servlet.http.HttpServletResponse` 개체 `write` 클라이언트 웹 브라우저에 양식 데이터 스트림을 전송하는 방법입니다. 바이트 배열을 로 전달 `write` 메서드를 사용합니다.

**추가 참조**

[Base64 인코딩을 사용하여 AEM Forms 호출](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
