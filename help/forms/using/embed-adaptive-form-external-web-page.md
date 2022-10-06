---
title: 외부 웹 페이지에 적응형 양식 임베드
seo-title: Embed adaptive form in external web page
description: 외부 웹 페이지에 적응형 양식을 포함하는 방법을 알아봅니다
seo-description: Learn how to embed an adaptive form in an external HTML web page
uuid: d81032dd-af80-4f4b-a717-ee1b89fd3d3d
products: SG_EXPERIENCEMANAGER/6.3/FORMS
topic-tags: author
discoiquuid: d739c6da-3b41-4452-8728-d7cd1a3ae20b
docset: aem65
feature: Adaptive Forms
exl-id: 2a237f74-fdfc-4e28-841c-f69afb7b99cf
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '970'
ht-degree: 1%

---

# 외부 웹 페이지에 적응형 양식 임베드{#embed-adaptive-form-in-external-web-page}

다음을 수행할 수 있습니다 [AEM Sites 페이지에 적응형 양식 포함](/help/forms/using/embed-adaptive-form-aem-sites.md) 또는 AEM 외부에서 호스팅되는 웹 페이지입니다. 포함된 적응형 양식은 완전히 기능하며 사용자는 페이지를 종료하지 않고 양식을 작성하고 제출할 수 있습니다. 따라서 사용자는 웹 페이지에서 다른 요소의 컨텍스트에 남아 있고 양식과 동시에 상호 작용할 수 있습니다.

## 사전 요구 사항 {#prerequisites}

적응형 양식을 외부 웹 사이트에 포함하기 전에 다음 단계를 수행하십시오

* AEM Forms 서버의 게시 인스턴스에 포함할 적응형 양식을 게시합니다.
* 웹 사이트에서 적응형 양식을 호스팅할 웹 페이지를 만들거나 식별합니다. 웹 페이지가 [CDN에서 jQuery 파일 읽기](https://ajax.googleapis.com/ajax/libs/jquery/3.3.1/jquery.min.js) 또는 jQuery의 로컬 복사본이 들어 있습니다. 적응형 양식을 렌더링하려면 jQuery가 필요합니다.
* AEM 서버와 웹 페이지가 다른 도메인에 있는 경우 다음 섹션에 나열된 단계를 수행합니다. [AEM Forms에서 도메인 간 사이트에 적응형 양식을 제공할 수 있도록 설정](#cross-site).

## 적응형 양식 포함 {#embed-adaptive-form}

웹 페이지에 JavaScript 몇 줄을 삽입하여 적응형 양식을 포함할 수 있습니다. 코드의 API는 적응형 양식 리소스를 위해 AEM 서버에 HTTP 요청을 보내고 지정된 양식 컨테이너에 적응형 양식을 삽입합니다.

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

   * 의 값 변경 *options.path* 적응형 양식의 게시 URL 경로가 있는 변수입니다. AEM 서버가 컨텍스트 경로에서 실행 중인 경우 URL에 컨텍스트 경로가 포함되어 있는지 확인하십시오. 확장을 포함하여 항상 적응형 양식의 전체 이름을 언급하십시오.   예를 들어 위의 코드 및 적응형 은 동일한 AEM Forms 서버에 상주하므로 이 예제에서는 적응형 양식의 컨텍스트 경로 /content/forms/af/locbasic.html 를 사용합니다.
   * 바꾸기 *options.dataRef* 를 사용하십시오. dataref 변수를 사용하여 다음을 수행할 수 있습니다 [적응형 양식 미리 채우기](/help/forms/using/prepopulate-adaptive-form-fields.md).
   * 바꾸기 *options.themePath* 적응형 양식에 구성된 테마가 아닌 테마 경로를 사용합니다. 또는 요청 속성을 사용하여 테마 경로를 지정할 수 있습니다.
   * CSS_Selector는 적응형 양식이 포함된 양식 컨테이너의 CSS 선택기입니다. 예를 들어 .customafsection css 클래스는 위의 예에서 CSS 선택기입니다.

적응형 양식은 웹 페이지에 포함됩니다. 포함된 적응형 양식에서 다음을 관찰합니다.

* 원래 적응형 양식의 머리글 및 바닥글은 포함된 양식에 포함되지 않습니다.
* 초안 및 제출된 양식은 Forms Portal의 초안 및 제출 탭에서 사용할 수 있습니다.
* 원본 적응형 양식에 구성된 제출 작업은 포함된 양식에 유지됩니다.
* 적응형 양식 규칙은 포함된 양식에서 유지되고 완전히 작동합니다.
* 원래 적응형 양식에 구성된 경험 타깃팅 및 A/B 테스트가 포함된 양식에서 작동하지 않습니다.
* Adobe Analytics이 원래 양식에 구성된 경우 Analytics 데이터가 Adobe Analytics 서버에 캡처됩니다. 하지만 Forms 분석 보고서에서는 사용할 수 없습니다.

## 예제 토폴로지 {#sample-topology}

적응형 양식을 포함하는 외부 웹 페이지는 일반적으로 개인 네트워크의 방화벽 뒤에 있는 AEM 서버에 요청을 보냅니다. 요청이 AEM 서버로 안전하게 전달되도록 하려면 역방향 프록시 서버를 설정하는 것이 좋습니다.

디스패처 없이 Apache 2.4 역방향 프록시 서버를 설정하는 방법을 예제를 살펴보겠습니다. 이 예에서는 다음을 사용하여 AEM 서버를 호스팅합니다. `/forms` 컨텍스트 경로 및 맵 `/forms` 역방향 프록시용. 그러면 모든 요청이 `/forms` Apache 서버에서 AEM 인스턴스로 이동합니다. 이 토폴로지는 사전 설정된 모든 요청과 같이 디스패처 레이어의 규칙 수를 줄이는 데 도움이 됩니다. `/forms` AEM 서버로 라우팅합니다.

1. 를 엽니다. `httpd.conf` 구성 파일을 구성하고 다음 코드 줄의 주석을 해제합니다. 또는 파일에 이러한 코드 행을 추가할 수 있습니다.

   ```text
   LoadModule proxy_html_module modules/mod_proxy_html.so
   LoadModule proxy_http_module modules/mod_proxy_http.so
   ```

1. 다음 코드 행을 `httpd-proxy.conf` 구성 파일.

   ```text
   ProxyPass /forms https://[AEM_Instance]/forms
   ProxyPassReverse /forms https://[AEM_Instance]/forms
   ```

   바꾸기 `[AEM_Instance]` AEM 서버 게시 URL을 사용하여 규칙에 매핑해야 합니다.

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
>다른 토폴로지를 설정하는 경우 Dispatcher 레이어의에 제출, 미리 채우기 및 기타 URL을 추가해야 허용 목록에 추가하다 합니다.

## 우수 사례 {#best-practices}

웹 페이지에 적응형 양식을 포함할 때에는 다음 우수 사례를 고려하십시오.

* 웹 페이지 CSS에 정의된 스타일 규칙이 양식 개체 CSS와 충돌하지 않도록 합니다. 충돌을 방지하기 위해 AEM 클라이언트 라이브러리를 사용하여 적응형 양식 테마에서 웹 페이지 CSS를 다시 사용할 수 있습니다. 적응형 양식 테마에서 클라이언트 라이브러리를 사용하는 방법에 대한 자세한 내용은 [AEM Forms의 테마](../../forms/using/themes.md).
* 웹 페이지의 양식 컨테이너에 전체 창 너비를 사용하도록 합니다. 이렇게 하면 모바일 장치에 대해 구성된 CSS 규칙이 변경 없이 작동합니다. 양식 컨테이너가 전체 창 너비를 취하지 않는 경우 양식이 다른 모바일 장치에 적용되도록 사용자 지정 CSS를 작성해야 합니다.
* 사용 `[getData](https://helpx.adobe.com/experience-manager/6-3/forms/javascript-api/GuideBridge.html)` 클라이언트에서 양식 데이터의 XML 또는 JSON 표현을 가져오는 API입니다.
* 사용 `[unloadAdaptiveForm](https://helpx.adobe.com/experience-manager/6-3/forms/javascript-api/GuideBridge.html)` HTML DOM에서 적응형 양식을 언로드하기 위한 API입니다.
* AEM 서버에서 응답을 보낼 때 액세스 제어 원본 헤더를 설정합니다.

## 도메인 간 사이트에 적응형 양식을 제공할 수 있도록 AEM Forms 활성화 {#cross-site}

1. AEM 게시 인스턴스에서 AEM Web Console 구성 관리자로 이동합니다. `https://'[server]:[port]'/system/console/configMgr`.
1. 을(를) 찾아 엽니다. **Apache Sling 레퍼러 필터** 구성.
1. 허용된 호스트 필드에서 웹 페이지가 있는 도메인을 지정합니다. 이렇게 하면 호스트가 AEM 서버에 POST 요청을 수행할 수 있습니다. 정규 표현식을 사용하여 일련의 외부 애플리케이션 도메인을 지정할 수도 있습니다.
