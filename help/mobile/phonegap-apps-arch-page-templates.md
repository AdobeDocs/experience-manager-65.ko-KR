---
title: 모바일 앱용 페이지 템플릿
seo-title: 모바일 앱용 페이지 템플릿
description: 모바일 앱용 페이지 템플릿에 대해 알려면 이 페이지를 따르십시오.
seo-description: 모바일 앱용 페이지 템플릿에 대해 알려면 이 페이지를 따르십시오.
uuid: ef469796-10f5-44f4-a5c7-25025ca192b0
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
discoiquuid: f45d8a9b-14d6-468f-a44c-3933e962922c
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 모바일 앱용 페이지 템플릿 {#page-templates-for-mobile-apps}

>[!NOTE]
>
>단일 페이지 애플리케이션 프레임워크 기반 클라이언트측 렌더링(예: 응답)이 필요한 프로젝트에 SPA 편집기를 사용하는 것이 좋습니다. [추가 정보](/help/sites-developing/spa-overview.md).

## 모바일 앱용 페이지 템플릿 {#page-templates-for-mobile-apps-1}

앱에 대해 만드는 페이지 구성 요소는 /libs/mobileapps/components/angular/ng-page 구성 요소를 기반으로 합니다(로컬 서버의 CRXDE Lite에서[열기](http://localhost:4502/crx/de/index.jsp#/libs/mobileapps/components/angular/ng-page)). 이 구성 요소에는 구성 요소가 상속하거나 덮어쓰는 다음 JSP 스크립트가 포함되어 있습니다.

* ng-page.jsp
* head.jsp
* body.jsp
* angular-app-module.js.jsp
* angular-route-fragment.js.jsp
* angular-app-controllers.js.jsp
* controller.js.jsp
* template.jsp
* angular-module-list.js.jsp
* header.jsp
* footer.jsp
* js_clientlibs.jsp
* css_clientlibs.jsp

### ng-page.jsp {#ng-page-jsp}

속성을 사용하여 응용 프로그램의 이름을 결정하고 pageContext를 통해 `applicationName` 표시합니다.

head.jsp 및 body.jsp를 포함합니다.

### head.jsp {#head-jsp}

앱 페이지의 `<head>` 요소를 기록합니다.

앱의 뷰포트 메타 속성을 재정의하려면 재정의하는 파일입니다.

다음의 우수 사례를 통해 앱은 클라이언트 라이브러리의 css 부분을 헤드에 포함시키고 JS는 닫는 &lt; `body>` 요소에 포함됩니다.

### body.jsp {#body-jsp}

각진 페이지의 본문은 wcmMode가 감지되었는지에 따라 다르게 렌더링됩니다(!= WCMMode.DISABLED)를 사용하여 페이지를 작성용으로 열었는지 또는 게시된 페이지로 열었는지 확인합니다.

**작성자 모드**

작성 모드에서는 각 개별 페이지가 별도로 렌더링됩니다. Angular는 페이지 간 라우팅을 처리하지 않으며 페이지의 구성 요소가 포함된 부분 템플릿을 로드하는 데 사용되는 Ng-View도 아닙니다. 대신 페이지 템플릿(template.jsp)의 컨텐츠는 `cq:include` 태그를 통해 서버측에 포함됩니다.

이 전략을 사용하면 작성 기능(예: 단락 시스템에서 구성 요소 추가 및 편집, 사이드 킥이나 디자인 모드 등)을 사용할 수 있습니다. to function without modification. 앱용 페이지와 같은 클라이언트 측 렌더링을 사용하는 페이지는 AEM 작성자 모드에서 제대로 작동하지 않습니다.

template.jsp에 포함된 요소는 `div` 지시문을 포함하는 `ng-controller` 요소로 래핑됩니다. 이 구조를 사용하면 DOM 컨텐츠를 컨트롤러와 연결할 수 있습니다. 따라서 클라이언트측에서 렌더링되는 페이지는 실패하더라도 이를 수행하는 개별 구성 요소는 제대로 작동합니다(아래 구성 요소의 섹션 참조).

```xml
<div ng-controller="<c:out value="${controllerNameStripped}"/>">
      <cq:include script="template.jsp"/>
</div>
```

**게시 모드**

게시 모드(예: 콘텐츠 동기화를 사용하여 앱을 내보낼 때)에서 모든 페이지는 단일 페이지 앱(SPA)이 됩니다. (SPA에 대한 자세한 내용은 Angular 튜토리얼(특히 https://docs.angularjs.org/tutorial/step_07)을 [참조하십시오](https://docs.angularjs.org/tutorial/step_07).)

SPA에는 HTML 페이지가 하나만 있습니다( `<html>` 요소가 포함된 페이지). 이 페이지를 &quot;레이아웃 템플릿&quot;이라고 합니다. 각 용어로, &quot;...응용 프로그램의 모든 보기에 공통으로 사용되는 템플릿입니다.&quot; 이 페이지를 &#39;최상위 앱 페이지&#39;로 간주합니다. 최상위 앱 페이지는 루트에 가장 근접한 애플리케이션의 `cq:Page` 노드이며 리디렉션이 아닙니다.

앱의 실제 URI가 게시 모드에서 변경되지 않으므로 이 페이지의 외부 자산에 대한 참조는 상대 경로를 사용해야 합니다. 따라서 내보내기를 위해 이미지를 렌더링할 때 이 최상위 페이지를 고려하도록 특수 이미지 구성 요소가 제공됩니다.

SPA로서 이 레이아웃 템플릿 페이지는 ng-view 지시문을 사용하여 div 요소를 생성합니다.

```xml
 <div ng-view ng-class="transition"></div>
```

Angular Route 서비스는 이 요소를 사용하여 현재 페이지의 작성 가능한 컨텐츠(template.jsp에 포함)를 비롯하여 앱의 모든 페이지의 컨텐츠를 표시합니다.

body.jsp 파일은 비어 있는 header.jsp 및 footer.jsp를 포함합니다. 모든 페이지에 정적 콘텐츠를 제공하려는 경우 앱에서 이러한 스크립트를 재정의할 수 있습니다.

마지막으로, javascript clientlibs는 서버에서 생성된 두 개의 특수 JS 파일을 포함하여 &lt;body> 요소의 아래쪽에 포함됩니다.&lt; *&lt;page name>*.angular-app-module.js 및 *&lt;page name>*.angular-app-controllers.js.

### angular-app-module.js.jsp {#angular-app-module-js-jsp}

이 스크립트는 응용 프로그램의 각도 모듈을 정의합니다. 이 스크립트의 출력은 다음 속성을 포함하는 ng-page.jsp의 `html` 요소를 통해 템플릿 구성 요소의 나머지 부분이 생성하는 마크업에 연결됩니다.

```xml
ng-app="<c:out value='${applicationName}'/>"
```

이 속성은 이 DOM 요소의 컨텐츠를 다음 모듈에 연결해야 함을 Angular로 나타냅니다. 이 모듈은 뷰(AEM에서는 cq:Page 리소스)를 해당 컨트롤러와 연결합니다.

또한 이 모듈은 변수를 범위에 `AppController` `wcmMode` 노출하는 이름이 지정된 최상위 수준의 컨트롤러를 정의하고 컨텐츠 동기화 업데이트 페이로드를 가져올 URI를 구성합니다.

마지막으로, 이 모듈은 각 하위 페이지(자체 포함)를 반복하여 각 페이지의 경로 분리(angular-route-fragment.js 선택기 및 익스텐션을 통해)를 Angular의 $routeProvider에 대한 구성 항목으로 포함하여 렌더링합니다. 즉, $routeProvider는 주어진 경로를 요청할 때 렌더링할 콘텐츠를 앱에 알려줍니다.

### angular-route-fragment.js.jsp {#angular-route-fragment-js-jsp}

이 스크립트는 다음 양식을 가져와야 하는 JavaScript 조각을 생성합니다.

```
.when('/<path>', {
    templateUrl: '<path to template>',
    controller: '<controller name>'
})
```

이 코드는 $routeProvider(angular-app-module.js.jsp에 정의됨)에 &#39;/&lt;path>&#39;가 다음 리소스에서 처리되고 `templateUrl`유선 연결이 `controller` 될 것임을 나타냅니다.

필요한 경우 이 스크립트를 재정의하여 변수가 있는 경로를 포함하여 보다 복잡한 경로를 처리할 수 있습니다. 이러한 예제는 AEM과 함께 설치되는 /apps/weretail-app/components/angular/ng-template-page/angular-route-fragment.js.jsp 스크립트에서 확인할 수 있습니다.

```xml
// note the :id suffix on the path
.when('<c:out value="${resource.path}"/>/:id', {
    templateUrl: '<c:out value="${relativeResourcePath}"/>.template.html',
    controller: '<c:out value="${controllerNameStripped}"/>'
})
```

### angular-app-controllers.js.jsp {#angular-app-controllers-js-jsp}

각도에서 컨트롤러는 $scope의 변수를 연결하여 뷰에 표시합니다. angular-app-controllers.js.jsp 스크립트는 angular-app-module.js.jsp로 표시된 패턴을 따르고 각 하위 페이지(자체 포함)를 반복하여 각 페이지가 정의하는 컨트롤러 조각을 출력합니다(controller.js.jsp를 통해). 정의하는 모듈은 호출되며 페이지 컨트롤러를 사용할 수 있도록 최상위 앱 모듈의 종속성이 `cqAppControllers` 되어야 합니다.

### controller.js.jsp {#controller-js-jsp}

controller.js.jsp 스크립트는 각 페이지에 대한 컨트롤러 조각을 생성합니다. 이 컨트롤러 조각은 다음 양식을 사용합니다.

```
.controller('<c:out value="${controllerNameStripped}"/>', ['$scope', '$http',
    function($scope, $http) {
        var data = $http.get('<c:out value="${relativeResourcePath}"/>.angular.json' + cacheKiller);

        // component fragments which consume the contents of `data` go here
    }
])
```

이 `data` 변수에는 각도 `$http.get` 방법으로 반환된 약속이 지정됩니다. 원하는 경우 이 페이지에 포함된 각 구성 요소는 일부 .json 컨텐츠를 사용 가능하도록(angular.json.jsp 스크립트를 통해) 만들고 이 요청이 해결될 때 해당 요청의 컨텐츠에 따라 작동할 수 있습니다. 모바일 디바이스에서 간단하게 파일 시스템에 액세스할 수 있으므로 요청이 매우 빨라집니다.

구성 요소가 이러한 방식으로 컨트롤러의 일부분이 되도록 하려면 /libs/mobileapps/components/angular/ng-component 구성 요소를 확장하고 `frameworkType: angular` 속성을 포함해야 합니다.

### template.jsp {#template-jsp}

body.jsp 섹션에 처음 도입된 template.jsp는 페이지의 parsys만 포함합니다. 게시 모드에서 이 컨텐츠는 직접(&lt;page-path>.template.html)에 참조되고 $routeProvider에 구성된 templateUrl을 통해 SPA로 로드됩니다.

이 스크립트의 parsys는 모든 유형의 구성 요소를 허용하도록 구성할 수 있습니다. 그러나 SPA가 아닌 기존 웹 사이트에 맞게 제작된 구성 요소를 처리할 때는 주의해야 합니다. 예를 들어, 기본 이미지 구성 요소는 앱 내에 있는 자산을 참조하도록 설계되지 않았으므로 최상위 앱 페이지에서만 올바르게 작동합니다.

### angular-module-list.js.jsp {#angular-module-list-js-jsp}

이 스크립트는 최상위 수준 Angular 앱 모듈의 Angular 종속성을 출력합니다. angular-app-module.js.jsp에서 참조합니다.

### header.jsp {#header-jsp}

앱 맨 위에 정적 콘텐츠를 배치하는 스크립트입니다. 이 컨텐츠는 ng-view 범위를 벗어나는 최상위 페이지에 포함됩니다.

### footer.jsp {#footer-jsp}

앱 하단에 정적 컨텐츠를 배치하는 스크립트입니다. 이 컨텐츠는 ng-view 범위를 벗어나는 최상위 페이지에 포함됩니다.

### js_clientlibs.jsp {#js-clientlibs-jsp}

JavaScript clientlibs를 포함하도록 이 스크립트를 재정의합니다.

### css_clientlibs.jsp {#css-clientlibs-jsp}

CSS 클라이언트를 포함하려면 이 스크립트를 재정의합니다.

## 앱 구성 요소 {#app-components}

앱 구성 요소는 AEM 인스턴스(게시 또는 작성자)에서만 작동될 수 있을 뿐만 아니라 컨텐츠 동기화를 통해 애플리케이션 컨텐츠를 파일 시스템으로 내보낼 때에도 작동해야 합니다. 따라서 구성 요소에는 다음 특성이 포함되어야 합니다.

* PhoneGap 애플리케이션의 모든 에셋, 템플릿 및 스크립트는 상대적으로 참조되어야 합니다.
* AEM 인스턴스가 작성 또는 게시 모드에서 작동 중이면 링크 처리가 달라집니다.

### 상대 자산 {#relative-assets}

PhoneGap 응용 프로그램에서 지정된 자산의 URI는 플랫폼별로 다를 뿐만 아니라 응용 프로그램의 각 설치 시 고유합니다. 예를 들어 iOS 시뮬레이터에서 실행 중인 앱의 다음 URI를 참조하십시오.

`file:///Users/userId/Library/Application%20Support/iPhone%20Simulator/7.0.3/Applications/24BA22ED-7D06-4330-B7EB-F6FC73251CA3/Library/files/www/content/phonegap/weretail/apps/ng-we-retail/en/home.html`

경로에 GUID &#39;24BA22ED-7D06-4330-B7EB-F6FC73251CA3&#39;가 있습니다.

PhoneGap 개발자는 관심이 있는 컨텐츠가 www 디렉토리 아래에 있습니다. 앱 자산에 액세스하려면 상대 경로를 사용하십시오.

이 문제를 해결하기 위해 PhoneGap 응용 프로그램은 단일 페이지 앱(SPA) 패턴을 사용하므로 기본 URI(해시 제외)는 변경되지 않습니다. 따라서 참조한 모든 에셋, 템플릿 또는 스크립트는 최상위 페이지에 상대적이어야 합니다. **최상위 수준 페이지는 `<name>.angular-app-module.js` 및 에 따라 각 라우팅 및 컨트롤러를 초기화합니다 `<name>.angular-app-controllers.js`. 이 페이지는 *sling:redirect를 확장하지 않는 *저장소의 루트에 가장 가까운 페이지여야 합니다.

상대 경로를 처리하는 데 몇 가지 도우미 메서드를 사용할 수 있습니다.

* FrameworkContentExporterUtils.getTopLevelAppResource
* FrameworkContentExporterUtils.get 파섹
* FrameworkContentExporterUtils.getPathToAsset

사용 예를 보려면 /libs/mobileapps/components/angular에 있는 mobileapps 소스를 엽니다.

### 링크 {#links}

링크는 모든 WCM 모드를 지원하려면 `ng-click="go('/path')"` 함수를 사용해야 합니다. 이 함수는 범위 변수의 값에 따라 달라져서 링크 작업을 올바르게 결정합니다.

```xml
<c:choose><c:when test="${wcmMode}">
    <%-- WCMMode is enabled - page is being rendered in AEM --%>
    $scope.wcmMode = true;
</c:when><c:otherwise>
    <%-- WCMMode is disabled --%>
    $scope.wcmMode = false;
</c:otherwise></c:choose>
```

일반적으로 각 탐색 이벤트를 처리할 `$scope.wcmMode == true` 때 URL의 경로 및/또는 페이지 부분이 변경되도록 합니다.

또는 각 탐색 이벤트가 URL의 해시 부분이 변경되면 Angular `$scope.wcmMode == false`의 ngRoute 모듈로 내부적으로 해결됩니다.

### 구성 요소 스크립트 세부 사항 {#component-script-details}

![chlimage_1-51](assets/chlimage_1-51.png)

### ng-component.jsp {#ng-component-jsp}

이 스크립트는 편집 모드가 감지되면 구성 요소 컨텐츠나 적절한 자리 표시자를 표시합니다.

### template.jsp {#template-jsp-1}

template.jsp 스크립트는 구성 요소의 마크업을 렌더링합니다. 해당 구성 요소가 AEM에서 추출한 JSON 데이터에 의해 구동되는 경우(예: &#39;ng-text&#39;):/libs/mobileapps/components/angular/ng-text/template.jsp), 그러면 이 스크립트는 페이지의 컨트롤러 범위에 의해 노출된 데이터와 함께 마크업을 연결하는 책임을 집니다.

그러나 성능 요구 사항에 따라 클라이언트측 템플릿(데이터 바인딩)을 수행할 필요가 없는 경우가 있습니다. 이 경우 구성 요소의 마크업을 서버 측에서 렌더링하면 페이지 템플릿 컨텐츠에 포함됩니다.

### 간접비.jsp {#overhead-jsp}

JSON 데이터를 기반으로 하는 구성 요소(예: &#39;ng-text&#39;):/libs/mobileapps/components/angular/ng-text), overhead.jsp를 사용하여 template.jsp에서 모든 Java 코드를 제거할 수 있습니다. 그런 다음 template.jsp에서 참조되며 요청에 표시되는 모든 변수를 사용할 수 있습니다. 이 전략을 사용하면 논리와 프레젠테이션을 분리할 수 있으며, 새 구성 요소가 기존 구성 요소에서 파생될 때 복사하여 붙여넣어야 하는 코드의 양을 제한할 수 있습니다.

### controller.js.jsp {#controller-js-jsp-1}

AEM 페이지 [템플릿에서 설명한](/help/mobile/apps-architecture.md)바와 같이, 각 구성 요소는 JavaScript 조각을 출력하여 `data` 약속에 의해 노출된 JSON 컨텐츠를 사용할 수 있습니다. 각 규칙 다음에 따라, 컨트롤러는 범위에 변수를 할당하는 데에만 사용해야 합니다.

### angular.json.jsp {#angular-json-jsp}

이 스크립트는 페이지 전체 &#39;&lt;page-name>.angular.json&#39; 파일에서 ng-page를 확장하는 각 페이지에 대해 내보낸 조각으로 포함됩니다. 이 파일에서 구성 요소 개발자는 구성 요소에 필요한 모든 JSON 구조를 표시할 수 있습니다. &#39;ng-text&#39; 예에서 이 구조에는 구성 요소의 텍스트 컨텐츠와 구성 요소에 리치 텍스트가 포함되어 있는지 여부를 나타내는 플래그가 포함되어 있습니다.

We.Retail 앱 제품 구성 요소는 보다 복잡한 예입니다(/apps/weretail-app/components/angular/ng-product).

```xml
{
    "content-par/ng-product": {
        "items": [{
            "name": "Cajamara",
            "description": "Bike",
            "summaryHTML": "",
            "price": "$610.00",
            "SKU": "eqsmcj",
            "numberOfLikes": "0",
            "numberOfComments": "0"
        }]
    },
    "content-par/ng-product/ng-image": {
        "items": [{
            "hasContent": true,
            "imgSrc": "home/products/eq/eqsm/eqsmcj/jcr_content/content-par/ng-product/ng-image.img.jpg/1377771306985.jpg",
            "description": "",
            "alt": "Cajamara",
            "title": "Cajamara",
            "hasLink": false,
            "linkPath": "",
            "attributes": [{
                "attributeName": "class",
                "attributeValue": "cq-dd-image"
            }]
        }]
    }
}
```

## CLI 자산 다운로드 컨텐츠 {#contents-of-the-cli-assets-download}

Apps 콘솔에서 CLI 에셋을 다운로드하여 특정 플랫폼에 맞게 최적화한 다음 PhoneGap 명령줄 통합(CLI) API를 사용하여 앱을 빌드합니다. 로컬 파일 시스템에 저장하는 ZIP 파일의 내용은 다음 구조를 갖습니다.

```xml
.cordova/
  |- hooks/
     |- after_prepare/
     |- before_platform_add/
     |- Other Hooks
plugins/
www/
  |- config.xml
  |- index.html
  |- res/
  |- etc/
  |- apps/
  |- content/
  |- package.json
  |- package-update.json
```

### .cordova {#cordova}

이 디렉토리는 현재 OS 설정에 따라 표시되지 않을 수 있습니다. 포함된 앱 후크를 수정할 계획이면 이 디렉토리가 표시되도록 OS를 구성해야 합니다.

### .cordova/hooks/ {#cordova-hooks}

이 디렉토리에는 CLI 후크가 [들어](https://devgirl.org/2013/11/12/three-hooks-your-cordovaphonegap-project-needs/)있습니다. hooks 디렉토리의 폴더에는 빌드 동안 정확히 실행되는 node.js 스크립트가 포함되어 있습니다.

### .cordova/hooks/after-platform_add/ {#cordova-hooks-after-platform-add}

after-platform_add 디렉토리에는 `copy_AMS_Conifg.js` 파일이 포함되어 있습니다. 이 스크립트는 구성 파일을 복사하여 Adobe Mobile Services 분석 컬렉션을 지원합니다.

### .cordova/hooks/after-prepare/ {#cordova-hooks-after-prepare}

사후 준비 디렉토리에는 `copy_resource_files.js` 파일이 포함되어 있습니다. 이 스크립트는 다양한 아이콘 및 시작 화면 이미지를 플랫폼별 위치로 복사합니다.

### .cordova/hooks/before_platform_add/ {#cordova-hooks-before-platform-add}

before_platform_add 디렉토리에는 `install_plugins.js` 파일이 포함되어 있습니다. 이 스크립트는 Cordova 플러그인 식별자 목록을 반복하므로 감지한 플러그인 식별자는 아직 사용할 수 없습니다.

이 전략은 Maven `content-package:install` 명령이 실행될 때마다 플러그인을 번들로 설치하고 AEM에 설치할 필요가 없습니다. SCM 시스템에 파일을 체크 인하기 위한 대체 전략은 반복적인 번들로 묶어서 작업을 설치해야 합니다.

### .cordova/hooks/기타 후크 {#cordova-hooks-other-hooks}

필요에 따라 다른 후크를 포함합니다. 다음 후크를 사용할 수 있습니다(Phonegap 샘플 hello world 앱에서 제공).

* after_build
* before_build
* after_compile
* before_compile
* after_docs
* before_docs
* after_emulate
* before_emulate
* after_platform_add
* before_platform_add
* after_platform_ls
* before_platform_ls
* after_platform_rm
* before_platform_rm
* after_plugin_add
* before_plugin_add
* after_plugin_ls
* before_plugin_ls
* after_plugin_rm
* before_plugin_rm
* after_prepare
* before_prepare
* after_run
* before_run

### platforms/ {#platforms}

이 디렉토리는 프로젝트에서 `phonegap run *<platform>*` 명령을 실행할 때까지 비어 있습니다. 현재, `*<platform>*` 은 `ios` 또는 `android`일 수 있습니다.

특정 플랫폼용 앱을 빌드하면 해당 디렉토리가 만들어지고 플랫폼별 앱 코드가 포함됩니다.

### plugins/ {#plugins}

plugins 디렉토리는 `.cordova/hooks/before_platform_add/install_plugins.js` `phonegap run *<platform>*` 명령을 실행한 후 파일에 나열된 각 플러그인으로 채워집니다. 디렉토리는 처음에 비어 있습니다.

### www/ {#www}

www 디렉토리에는 앱의 모양과 동작을 구현하는 모든 웹 컨텐츠(HTML, JS 및 CSS 파일)가 포함되어 있습니다. 아래에 설명된 예외를 제외하고, 이 컨텐츠는 AEM에서 생성되어 콘텐츠 동기화를 통해 정적 양식으로 내보내집니다.

### www/config.xml {#www-config-xml}

PhoneGap [설명서는](https://docs.phonegap.com) 이 파일을 &#39;전역 구성 파일&#39;이라고 합니다. config.xml에는 앱 이름, 앱 &#39;preferences&#39;(예: iOS 웹뷰가 오버스크롤을 허용하는지 여부) 및 PhoneGap 빌드에 *의해서만* 사용되는 플러그인 종속성이 포함됩니다.

config.xml 파일은 AEM의 정적 파일이며 컨텐츠 동기화를 통해 있는 그대로 내보냅니다.

### www/index.html {#www-index-html}

index.html 파일은 앱의 시작 페이지로 리디렉션됩니다.

config.xml 파일에는 `content` 요소가 포함되어 있습니다.

`<content src="content/phonegap/weretail/apps/ng-we-retail/en.html" />`

PhoneGap [설명서에서](https://docs.phonegap.com)이 요소는 &quot;선택적 &lt;content> 요소는 최상위 웹 자산 디렉토리에서 앱의 시작 페이지를 정의합니다. 기본값은 index.html로, 프로젝트의 최상위 www 디렉토리에 일반적으로 표시됩니다.&quot;

index.html 파일이 없으면 PhoneGap 빌드가 실패합니다. 따라서 이 파일이 포함됩니다.

### www/res {#www-res}

res 디렉토리에는 시작 화면 이미지와 아이콘이 포함되어 있습니다. 이 `copy_resource_files.js` 스크립트는 `after_prepare` 빌드 단계 동안 파일을 플랫폼별 위치에 복사합니다.

### www/etc {#www-etc}

규칙별로, AEM에서 /etc 노드에는 정적 clientlib 컨텐츠가 포함됩니다. etc 디렉토리에는 Topcoat, AngularJS 및 We.Retail ng-clientsall 라이브러리가 포함되어 있습니다.

### www/apps {#www-apps}

앱 디렉토리에는 시작 페이지와 관련된 코드가 포함되어 있습니다. AEM 앱의 시작 페이지의 고유한 특징은 사용자 상호 작용 없이 앱을 초기화한다는 것입니다. 따라서 앱의 clientlib 컨텐츠(CSS 및 JS 모두)는 성능을 최대화하기 위해 최소한으로 사용됩니다.

### www/content {#www-content}

콘텐츠 디렉토리에는 앱의 나머지 웹 콘텐츠가 포함되어 있습니다. 컨텐츠는 다음 파일을 포함할 수 있지만 이에 제한되지 않습니다.

* AEM에서 직접 작성되는 HTML 페이지 컨텐츠
* AEM 구성 요소와 연결된 이미지 자산
* 서버측 스크립트가 생성하는 JavaScript 컨텐츠
* 페이지 또는 구성 요소 컨텐츠를 설명하는 JSON 파일

### www/package.json {#www-package-json}

package.json 파일은 **전체** 컨텐츠 동기화 다운로드에 포함된 파일을 나열하는 매니페스트 파일입니다. 이 파일에는 컨텐츠 동기화 페이로드가 생성된 타임스탬프( `lastModified`)도 포함되어 있습니다. 이 속성은 AEM에서 앱의 부분 업데이트를 요청할 때 사용됩니다.

### www/package-update.json {#www-package-update-json}

이 페이로드가 전체 앱의 다운로드인 경우 이 매니페스트에는 파일의 정확한 목록이 포함되어 `package.json`있습니다.

그러나 이 페이로드가 부분 업데이트인 경우 `package-update.json` 이 특정 페이로드에 포함된 파일만 포함합니다.
