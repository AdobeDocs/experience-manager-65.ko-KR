---
title: 외부 웹 페이지에 적응형 양식 포함
seo-title: 외부 웹 페이지에 적응형 양식 포함
description: 외부 웹 페이지에 적응형 양식을 포함하는 방법을 알아봅니다.
seo-description: 외부 HTML 웹 페이지에 적응형 양식을 포함하는 방법을 알아봅니다.
uuid: d81032dd-af80-4f4b-a717-ee1b89fd3d3d
products: SG_EXPERIENCEMANAGER/6.3/FORMS
topic-tags: author
discoiquuid: d739c6da-3b41-4452-8728-d7cd1a3ae20b
docset: aem65
translation-type: tm+mt
source-git-commit: ade3747ba608164a792a62097b82c55626245891
workflow-type: tm+mt
source-wordcount: '990'
ht-degree: 0%

---


# 외부 웹 페이지에 적응형 양식 포함{#embed-adaptive-form-in-external-web-page}

[적응형 양식을 AEM Sites 페이지](/help/forms/using/embed-adaptive-form-aem-sites.md) 또는 AEM 외부에 호스팅된 웹 페이지에 포함할 수 있습니다. 포함된 적응형 양식이 모든 기능을 갖추고 있으며 사용자는 페이지를 나가지 않고도 양식을 채우고 제출할 수 있습니다. 사용자가 웹 페이지에서 다른 요소의 컨텍스트에 있고 양식과 동시에 상호 작용할 수 있습니다.

## 전제 조건 {#prerequisites}

응용 양식을 외부 웹 사이트에 포함하기 전에 다음 단계를 수행하십시오

* AEM Forms 서버의 게시 인스턴스에 포함할 적응형 양식을 게시합니다.
* 적응형 양식을 호스팅할 웹 페이지를 만들거나 식별합니다. 웹 페이지에서 [CDN](https://ajax.googleapis.com/ajax/libs/jquery/3.3.1/jquery.min.js)에서 jQuery 파일을 읽을 수 있거나 jQuery의 로컬 복사본이 내장되어 있는지 확인합니다. 적응형 양식을 렌더링하려면 jQuery가 필요합니다.
* AEM 서버와 웹 페이지가 다른 도메인에 있는 경우 [AEM Forms에서 크로스 도메인 사이트](#cross-site)에 적응형 양식을 제공하도록 허용 섹션에 나열된 단계를 수행합니다.

## 응용 양식 {#embed-adaptive-form} 포함

웹 페이지에 JavaScript의 몇 줄을 삽입하여 적응형 양식을 포함할 수 있습니다. 코드의 API는 적응형 양식 리소스를 위해 AEM 서버로 HTTP 요청을 보내고 지정된 양식 컨테이너에 적응형 양식을 삽입합니다.

적응형 양식을 포함하려면 다음을 수행합니다.

1. 다음 코드를 사용하여 웹 사이트에서 웹 페이지를 만듭니다.

   ```html
   <!doctype html>
   <html>
     <head>
       <title>This is the title of the webpage!</title>
       <script src="https://ajax.googleapis.com/ajax/libs/jquery/3.3.1/jquery.min.js"></script>
     </head>
     <body>
     <div class="customafsection"/>
       <p>This section is replaced with the adaptive form.</p>
   
    <script>
    var options = {path:"/content/forms/af/locbasic.html", dataRef:"", themepath:"", CSS_Selector:".customafsection"};
    alert(options.path);
    var loadAdaptiveForm = function(options){
    //alert(options.path);
       if(options.path) {
           // options.path refers to the publish URL of the adaptive form
           // For Example: https:myserver:4503/content/forms/af/ABC, where ABC is the adaptive form
           // Note: If AEM server is running on a context path, the adaptive form URL must contain the context path
           var path = options.path;
           path += "/jcr:content/guideContainer.html";
           $.ajax({
               url  : path ,
               type : "GET",
               data : {
                   // Set the wcmmode to be disabled
                   wcmmode : "disabled"
                   // Set the data reference, if any
                  // "dataRef": options.dataRef
                   // Specify a different theme for the form object
                 //  "themeOverride" : options.themepath
               },
               async: false,
               success: function (data) {
                   // If jquery is loaded, set the inner html of the container
                   // If jquery is not loaded, use APIs provided by document to set the inner HTML but these APIs would not evaluate the script tag in HTML as per the HTML5 spec
                   // For example: document.getElementById().innerHTML
                   if(window.$ && options.CSS_Selector){
                       // HTML API of jquery extracts the tags, updates the DOM, and evaluates the code embedded in the script tag.
                       $(options.CSS_Selector).html(data);
                   }
               },
               error: function (data) {
                   // any error handler
               }
           });
       } else {
           if (typeof(console) !== "undefined") {
               console.log("Path of Adaptive Form not specified to loadAdaptiveForm");
           }
       }
    }(options);
   
    </script>
     </body>
   </html>
   ```

1. 포함된 코드에서:

   * 적응형 양식의 게시 URL 경로를 사용하여 *options.path* 변수의 값을 변경합니다. AEM 서버가 컨텍스트 경로에서 실행 중인 경우 URL에 컨텍스트 경로가 포함되어 있는지 확인합니다. 항상 확장을 포함하여 응용 양식의 전체 이름을 언급하십시오.   예를 들어 위의 코드 및 응용 프로그램은 동일한 AEM 양식 서버에 상주하므로 이 예제에서는 적응형 양식 /content/forms/af/locbasic.html의 컨텍스트 경로를 사용합니다.
   * *options.dataRef*&#x200B;을(를) URL로 전달할 특성으로 바꿉니다. dataref 변수를 사용하여 [적응형 양식](/help/forms/using/prepopulate-adaptive-form-fields.md)을 미리 입력할 수 있습니다.
   * *options.themePath*&#x200B;을 적응형 양식에 구성된 테마 이외의 테마 경로로 바꿉니다. 또는 요청 속성을 사용하여 테마 경로를 지정할 수도 있습니다.
   * CSS_Selector는 적응형 양식이 포함된 양식 컨테이너의 CSS 선택기입니다. 예를 들어 .customafsection css 클래스는 위의 예에서 CSS 선택기입니다.

적응형 양식이 웹 페이지에 포함됩니다. 포함된 응용 양식에서 다음을 관찰합니다.

* 원래 적응형 양식의 머리글과 바닥글은 포함된 양식에 포함되지 않습니다.
* 초안 및 제출된 양식은 Forms Portal의 초안 및 제출 탭에서 사용할 수 있습니다.
* 원래 적응형 양식에 구성된 제출 작업은 포함된 양식으로 유지됩니다.
* 적응형 양식 규칙은 그대로 유지되며 포함된 양식에서 완전히 작동합니다.
* 원래 적응형 양식에 구성된 경험 타깃팅 및 A/B 테스트는 포함된 양식에서 작동하지 않습니다.
* Adobe Analytics이 원래 양식에 구성되어 있으면 분석 데이터가 Adobe Analytics 서버에서 캡처됩니다. 하지만 Forms 분석 보고서에서는 사용할 수 없습니다.

## 샘플 토폴로지 {#sample-topology}

응용 양식을 포함하는 외부 웹 페이지는 일반적으로 비공개 네트워크의 방화벽 뒤에 있는 AEM 서버로 요청을 보냅니다. 요청이 AEM 서버로 안전하게 전달되도록 하려면 역방향 프록시 서버를 설정하는 것이 좋습니다.

디스패처 없이 Apache 2.4 역방향 프록시 서버를 설정하는 방법을 예로 들어보겠습니다. 이 예제에서는 `/forms` 컨텍스트 경로를 사용하여 AEM 서버를 호스팅하고 역방향 프록시에 `/forms`을 매핑합니다. Apache 서버의 `/forms`에 대한 모든 요청이 AEM 인스턴스로 이동됩니다. 이 토폴로지는 `/forms` 경로가 AEM 서버로 사전 설정된 모든 요청에 따라 디스패처 레이어의 규칙 수를 줄이는 데 도움이 됩니다.

1. `httpd.conf` 구성 파일을 열고 다음 코드 줄의 주석을 해제합니다. 또는 이러한 코드 줄을 파일에 추가할 수도 있습니다.

   ```text
   LoadModule proxy_html_module modules/mod_proxy_html.so
   LoadModule proxy_http_module modules/mod_proxy_http.so
   ```

1. `httpd-proxy.conf` 구성 파일에 다음 코드 줄을 추가하여 프록시 규칙을 설정합니다.

   ```text
   ProxyPass /forms https://[AEM_Instance]/forms
   ProxyPassReverse /forms https://[AEM_Instance]/forms
   ```

   규칙에서 `[AEM_Instance]`을(를) AEM 서버 게시 URL로 바꿉니다.

컨텍스트 경로에 AEM 서버를 마운트하지 않으면 Apache 레이어의 프록시 규칙은 다음과 같습니다.

```text
ProxyPass /content https://<AEM_Instance>/content
ProxyPass /etc https://<AEM_Instance>/etc
ProxyPass /etc.clientlibs https://<AEM_Instance>/etc.clientlibs
# CSRF Filter
ProxyPass /libs/granite/csrf/token.json https://<AEM_Instance>/libs/granite/csrf/token.json

ProxyPassReverse /etc https://<AEM_Instance>/etc
ProxyPassReverse /etc.clientlibs https://<AEM_Instance>/etc.clientlibs
# written for thank you page and other URL present in AF during redirect
ProxyPassReverse /content https://<AEM_Instance>/content
```

>[!NOTE]
>
>다른 토폴로지를 설정하는 경우 디스패처 레이어의에 제출, 자동 채우기 및 기타 URL을 허용 목록에 추가하다 추가해야 합니다.

## 우수 사례 {#best-practices}

웹 페이지에 적응형 양식을 포함할 때에는 다음 우수 사례를 고려하십시오.

* 웹 페이지 CSS에 정의된 스타일 규칙이 양식 개체 CSS와 충돌하지 않도록 합니다. 충돌을 방지하기 위해 AEM 클라이언트 라이브러리를 사용하여 적응형 양식 테마에 있는 웹 페이지 CSS를 재사용할 수 있습니다. 응용 양식 테마에서 클라이언트 라이브러리를 사용하는 방법에 대한 자세한 내용은 AEM Forms](../../forms/using/themes.md)의 [테마를 참조하십시오.
* 웹 페이지의 양식 컨테이너에서 전체 창 너비를 사용하도록 설정합니다. 이렇게 하면 모바일 장치용으로 구성된 CSS 규칙이 변경 없이 작동하도록 할 수 있습니다. 양식 컨테이너가 전체 창 너비를 사용하지 않는 경우 사용자 정의 CSS를 작성하여 양식이 다른 모바일 장치에 맞게 조정되어야 합니다.
* `[getData](https://helpx.adobe.com/experience-manager/6-3/forms/javascript-api/GuideBridge.html)` API를 사용하여 클라이언트에서 양식 데이터의 XML 또는 JSON 표현을 가져옵니다.
* `[unloadAdaptiveForm](https://helpx.adobe.com/experience-manager/6-3/forms/javascript-api/GuideBridge.html)` API를 사용하여 HTML DOM에서 적응형 양식을 언로드합니다.
* AEM 서버에서 응답을 보낼 때 액세스 제어 원본 헤더를 설정합니다.

## AEM Forms에서 크로스 도메인 사이트 {#cross-site}에 적응형 양식을 제공할 수 있도록 설정

1. AEM 작성자 인스턴스에서 AEM 웹 콘솔 구성 관리자(`https://'[server]:[port]'/system/console/configMgr`)로 이동합니다.
1. **Apache Sling 레퍼러 필터** 구성을 찾아 엽니다.
1. 허용된 호스트 필드에서 웹 페이지가 있는 도메인을 지정합니다. 이를 통해 주최자가 AEM 서버에 POST 요청을 수행할 수 있습니다. 정규 표현식을 사용하여 일련의 외부 응용 프로그램 도메인을 지정할 수도 있습니다.

