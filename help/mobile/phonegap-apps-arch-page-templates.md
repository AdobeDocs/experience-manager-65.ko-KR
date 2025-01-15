---
title: 모바일 앱용 콘텐츠 페이지 템플릿
description: 이 페이지를 따라 모바일 앱용 페이지 템플릿에 대해 알아보십시오.
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
exl-id: 7f00d426-4d28-41ee-8c54-636349e48669
solution: Experience Manager
feature: Mobile
role: Admin
source-git-commit: 2dae56dc9ec66f1bf36bbb24d6b0315a5f5040bb
workflow-type: tm+mt
source-wordcount: '2548'
ht-degree: 0%

---

# 모바일 앱용 페이지 템플릿 {#page-templates-for-mobile-apps}

{{ue-over-mobile}}

## 모바일 앱용 페이지 템플릿 {#page-templates-for-mobile-apps-1}

angular 앱에 대해 만드는 페이지 구성 요소는 /libs/mobileapps/components/page/ng-page 구성 요소([로컬 서버의 CRXDE Lite에서 열기](http://localhost:4502/crx/de/index.jsp#/libs/mobileapps/components/angular/ng-page))를 기반으로 합니다. 이 구성 요소에는 구성 요소가 상속하거나 재정의하는 다음 JSP 스크립트가 포함되어 있습니다.

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

`applicationName` 속성을 사용하여 응용 프로그램의 이름을 확인하고 pageContext를 통해 노출합니다.

head.jsp 및 body.jsp를 포함합니다.

### head.jsp {#head-jsp}

앱 페이지의 `<head>` 요소를 씁니다.

앱의 뷰포트 메타 속성을 재정의하려는 경우 재정의하는 파일입니다.

다음 모범 사례를 통해 앱은 헤드에 클라이언트 라이브러리의 css 부분을 포함하는 반면 JS는 닫는 &lt; `body>` 요소에 포함됩니다.

### body.jsp {#body-jsp}

angular 페이지의 본문은 wcmMode의 감지 여부에 따라 다르게 렌더링됩니다(!= WCMMode.DISABLED) - 페이지를 작성용으로 열지 또는 게시된 페이지로 열지를 결정합니다.

**작성자 모드**

작성 모드에서는 각 개별 페이지가 개별적으로 렌더링됩니다. Angular은 페이지 간 라우팅을 처리하지 않으며 페이지의 구성 요소를 포함하는 부분 템플릿을 로드하는 데 사용되는 ng-view도 아닙니다. 대신 페이지 템플릿의 콘텐츠(template.jsp)는 `cq:include` 태그를 통해 서버측에 포함됩니다.

이 전략을 사용하면 작성자 기능(예: 단락 시스템, Sidekick, 디자인 모드에서 구성 요소 추가 및 편집 등)을 수정 없이 사용할 수 있습니다. 앱용 페이지와 같이 클라이언트측 렌더링에 의존하는 페이지는 AEM 작성자 모드에서 잘 작동하지 않습니다.

template.jsp include가 `ng-controller` 지시문을 포함하는 `div` 요소에 래핑됩니다. 이 구조는 DOM 콘텐츠와 컨트롤러의 연결을 가능하게 합니다. 따라서 클라이언트측에서 자체 렌더링하는 페이지는 실패하지만 개별 구성 요소는 제대로 작동합니다(아래 구성 요소에 대한 섹션 참조).

```xml
<div ng-controller="<c:out value="${controllerNameStripped}"/>">
      <cq:include script="template.jsp"/>
</div>
```

**Publish 모드**

게시 모드(예: Content Sync를 사용하여 앱을 내보내는 경우)에서는 모든 페이지가 단일 페이지 앱(SPA)이 됩니다. (SPA에 대해 알아보려면 Angular 자습서(특히 [https://docs.angularjs.org/tutorial/step_07](https://docs.angularjs.org/tutorial/step_07))를 사용하십시오.)

SPA에는 `<html>` 요소를 포함하는 페이지에 HTML 페이지가 하나만 있습니다. 이 페이지를 &quot;레이아웃 템플릿&quot;이라고 합니다. angular 용어에서 &quot;...애플리케이션의 모든 보기에 일반적인 템플릿&quot;입니다. 이 페이지를 &#39;최상위 앱 페이지&#39;로 간주합니다. 규칙상 최상위 앱 페이지는 루트에 가장 가까운 응용 프로그램의 `cq:Page` 노드이며 리디렉션이 아닙니다.

게시 모드에서는 앱의 실제 URI가 변경되지 않으므로 이 페이지의 외부 에셋에 대한 참조는 상대 경로를 사용해야 합니다. 따라서 내보낼 이미지를 렌더링할 때 이 최상위 페이지를 고려하는 특수 이미지 구성 요소가 제공됩니다.

이 레이아웃 템플릿 페이지는 SPA으로서 ng-view 지시문이 있는 div 요소를 생성합니다.

```xml
 <div ng-view ng-class="transition"></div>
```

angular 경로 서비스는 이 요소를 사용하여 현재 페이지(template.jsp에 포함됨)의 작성 가능한 컨텐츠를 포함하여 앱에 있는 모든 페이지의 컨텐츠를 표시합니다.

body.jsp 파일에는 비어 있는 header.jsp 및 footer.jsp가 포함되어 있습니다. 모든 페이지에 정적 콘텐츠를 제공하려는 경우 앱에서 이러한 스크립트를 재정의할 수 있습니다.

마지막으로 Javascript clientlib은 서버에서 생성된 두 개의 특수 JS 파일(*&lt;page name>*.page-app-module.js 및 *&lt;page name>*.angular angular-app-controllers.js)을 포함하는 &lt;body> 요소의 맨 아래에 포함됩니다.

### angular-app-module.js.jsp {#angular-app-module-js-jsp}

이 스크립트는 응용 프로그램의 Angular 모듈을 정의합니다. 이 스크립트의 출력은 다음 특성을 포함하는 ng-page.jsp의 `html` 요소를 통해 템플릿의 나머지 구성 요소가 생성하는 마크업에 연결됩니다.

```xml
ng-app="<c:out value='${applicationName}'/>"
```

이 속성은 이 DOM 요소의 콘텐츠가 다음 Angular에 연결되어야 함을 나타냅니다. 이 모듈은 해당 제어기와 보기(AEM에서 cq:Page 리소스)를 연결합니다.

이 모듈은 또한 `wcmMode` 변수를 범위에 노출하는 `AppController` 최상위 컨트롤러를 정의하고 콘텐츠 동기화 업데이트 페이로드를 가져올 URI를 구성합니다.

마지막으로 이 모듈은 각 하위 페이지(자체 포함)를 반복하고 각 페이지의 경로 조각(angular-route-fragment.js 선택기 및 확장을 통해)의 콘텐츠를 렌더링합니다. 이러한 콘텐츠를 Angular의 $routeProvider에 대한 구성 항목으로 포함합니다. 즉, $routeProvider는 지정된 경로가 요청될 때 렌더링할 콘텐츠를 앱에 알려줍니다.

### angular-route-fragment.js.jsp {#angular-route-fragment-js-jsp}

이 스크립트는 다음 형식을 사용해야 하는 JavaScript 조각을 생성합니다.

```
.when('/<path>', {
    templateUrl: '<path to template>',
    controller: '<controller name>'
})
```

이 코드는 &#39;/&lt;path>&#39;을(를) `templateUrl`의 리소스에서 처리하고 `controller`에 의해 연결됨을 $routeProvider(angular-app-module.js.jsp에 정의됨)에 표시합니다(다음으로 연결됨).

필요한 경우 이 스크립트를 재정의하여 변수가 있는 경로를 포함하여 더 복잡한 경로를 처리할 수 있습니다. 이에 대한 예는 AEM과 함께 설치된 /apps/weretail-app/components/angular/ng-template-page/angular-route-fragment.js.jsp 스크립트에서 확인할 수 있습니다.

```xml
// note the :id suffix on the path
.when('<c:out value="${resource.path}"/>/:id', {
    templateUrl: '<c:out value="${relativeResourcePath}"/>.template.html',
    controller: '<c:out value="${controllerNameStripped}"/>'
})
```

### angular-app-controllers.js.jsp {#angular-app-controllers-js-jsp}

angular에서 컨트롤러는 $scope의 변수를 연결하여 보기에 노출합니다. angular-app-controllers.js.jsp 스크립트는 각 하위 페이지(자체 포함)를 반복하고 각 페이지가 정의하는 컨트롤러 조각을 출력한다는 점에서 angular-app-module.js.jsp에 표시된 패턴을 따릅니다(controller.js.jsp를 통해). 정의하는 모듈을 `cqAppControllers`이라고 하며 페이지 컨트롤러를 사용할 수 있도록 최상위 앱 모듈의 종속성으로 나열해야 합니다.

### controller.js.jsp {#controller-js-jsp}

controller.js.jsp 스크립트는 각 페이지에 대한 컨트롤러 조각을 생성합니다. 이 컨트롤러 조각은 다음 형식을 사용합니다.

```
.controller('<c:out value="${controllerNameStripped}"/>', ['$scope', '$http',
    function($scope, $http) {
        var data = $http.get('<c:out value="${relativeResourcePath}"/>.angular.json' + cacheKiller);

        // component fragments which consume the contents of `data` go here
    }
])
```

`data` 변수에는 Angular `$http.get` 메서드에서 반환된 약속이 할당됩니다. 이 페이지에 포함된 각 구성 요소는 필요한 경우 일부 .json 컨텐츠를 사용할 수 있도록(해당 angular.json.jsp 스크립트를 통해) 설정할 수 있으며, 이 요청이 해결될 때 이 요청의 컨텐츠에 작업을 수행합니다. 이 요청은 파일 시스템에 액세스만 하기 때문에 모바일 장치에서 매우 빠릅니다.

이러한 방식으로 구성 요소를 컨트롤러에 포함하려면 /libs/mobileapps/components/angular/ng 구성 요소를 확장하고 `frameworkType: angular` 속성을 포함해야 합니다.

### template.jsp {#template-jsp}

body.jsp 섹션에 처음 도입된 template.jsp에는 페이지의 parsys가 간단히 포함되어 있습니다. 게시 모드에서 이 콘텐츠는 직접(&lt;page-path>.template.html에서) 참조되며 $routeProvider에 구성된 templateUrl을 통해 SPA에 로드됩니다.

이 스크립트의 parsys는 모든 유형의 구성 요소를 수락하도록 구성할 수 있습니다. 그러나 기존 웹 사이트용으로 빌드된 구성 요소를 처리할 때는(SPA이 아니라) 주의해야 합니다. 예를 들어 기초 이미지 구성 요소는 앱 내의 자산을 참조하도록 디자인되지 않았기 때문에 최상위 앱 페이지에서만 올바르게 작동합니다.

### angular-module-list.js.jsp {#angular-module-list-js-jsp}

이 스크립트는 최상위 Angular 앱 모듈의 Angular 종속성을 출력하기만 합니다. angular-app-module.js.jsp에서 참조합니다.

### header.jsp {#header-jsp}

앱의 맨 위에 정적 콘텐츠를 배치하는 스크립트입니다. 이 컨텐츠는 ng-view의 범위를 벗어난 최상위 페이지에 포함됩니다.

### footer.jsp {#footer-jsp}

앱 하단에 정적 콘텐츠를 배치하는 스크립트. 이 컨텐츠는 ng-view의 범위를 벗어난 최상위 페이지에 포함됩니다.

### js_clientlibs.jsp {#js-clientlibs-jsp}

JavaScript clientlib을 포함하도록 이 스크립트를 재정의합니다.

### css_clientlibs.jsp {#css-clientlibs-jsp}

CSS clientlib을 포함하도록 이 스크립트를 재정의합니다.

## 앱 구성 요소 {#app-components}

앱 구성 요소는 AEM 인스턴스(게시 또는 작성자)에서 작동해야 할 뿐만 아니라 컨텐츠 동기화를 통해 애플리케이션 컨텐츠를 파일 시스템으로 내보낼 때도 작동해야 합니다. 따라서 구성 요소에는 다음 특성이 포함되어야 합니다.

* PhoneGap 애플리케이션의 모든 에셋, 템플릿 및 스크립트를 상대적으로 참조해야 합니다.
* AEM 인스턴스가 작성자 또는 게시 모드에서 작동하는 경우 링크 처리가 달라집니다.

### 상대 Assets {#relative-assets}

PhoneGap 애플리케이션에서 제공된 에셋의 URI는 플랫폼별로 다를 뿐만 아니라 앱의 각 설치에서 고유합니다. 예를 들어 iOS 시뮬레이터에서 실행되는 앱의 다음 URI를 참고하십시오.

`file:///Users/userId/Library/Application%20Support/iPhone%20Simulator/7.0.3/Applications/24BA22ED-7D06-4330-B7EB-F6FC73251CA3/Library/files/www/content/phonegap/weretail/apps/ng-we-retail/en/home.html`

경로의 GUID &#39;24BA22ED-7D06-4330-B7EB-F6FC73251CA3&#39;을 확인하십시오.

PhoneGap 개발자로서 관련 콘텐츠는 www 디렉터리 아래에 있습니다. 앱 자산에 액세스하려면 상대 경로를 사용하십시오.

문제를 종합하기 위해 PhoneGap 애플리케이션은 단일 페이지 앱(SPA) 패턴을 사용하여 기본 URI(해시 제외)가 변경되지 않도록 합니다. 따라서 참조하는 모든 에셋, 템플릿 또는 스크립트는 **최상위 페이지를 기준으로 해야 합니다. **최상위 페이지는 `<name>.angular-app-module.js` 및 `<name>.angular-app-controllers.js`을(를) 통해 Angular 라우팅 및 컨트롤러를 초기화합니다. 이 페이지는 sling:redirect를 *확장하지 *않는 저장소 루트와 가장 가까운 페이지여야 합니다.

상대 경로를 처리하는 데 여러 도우미 메서드를 사용할 수 있습니다.

* FrameworkContentExporterUtils.getTopLevelAppResource
* FrameworkContentExporterUtils.getRelativePathToRootLevel
* FrameworkContentExporterUtils.getPathToAsset

사용 사례를 보려면 /libs/mobileapps/components/angular에 있는 mobileapps 소스를 엽니다.

### 링크 {#links}

링크는 모든 WCM 모드를 지원하려면 `ng-click="go('/path')"` 함수를 사용해야 합니다. 이 함수는 범위 변수의 값에 따라 링크 작업을 올바르게 결정합니다.

```xml
<c:choose><c:when test="${wcmMode}">
    <%-- WCMMode is enabled - page is being rendered in AEM --%>
    $scope.wcmMode = true;
</c:when><c:otherwise>
    <%-- WCMMode is disabled --%>
    $scope.wcmMode = false;
</c:otherwise></c:choose>
```

`$scope.wcmMode == true`에서 일반적인 방법으로 각 탐색 이벤트를 처리하면 URL의 경로 및/또는 페이지 부분이 변경됩니다.

또는 `$scope.wcmMode == false`인 경우 각 탐색 이벤트는 Angular의 ngRoute 모듈에서 내부적으로 확인되는 URL의 해시 부분을 변경합니다.

### 구성 요소 스크립트 세부 정보 {#component-script-details}

![chlimage_1-51](assets/chlimage_1-51.png)

### ng-component.jsp {#ng-component-jsp}

이 스크립트는 편집 모드가 감지되면 구성 요소 콘텐츠 또는 적합한 자리 표시자를 표시합니다.

### template.jsp {#template-jsp-1}

template.jsp 스크립트는 구성 요소의 마크업을 렌더링합니다. 해당 구성 요소가 AEM에서 추출한 JSON 데이터(예: &#39;ng-text&#39;: /libs/mobileapps/components/angular/ng-text/template.jsp)로 구동되는 경우, 이 스크립트는 페이지의 컨트롤러 범위에 의해 노출된 데이터로 마크업을 배선합니다.

그러나 성능 요구 사항에 따라 클라이언트측 템플릿(즉, 데이터 바인딩)이 수행되지 않는 경우가 있습니다. 이 경우 단순히 서버측에서 구성 요소의 마크업을 렌더링하고 페이지 템플릿 콘텐츠에 포함됩니다.

### overhead.jsp {#overhead-jsp}

JSON 데이터 기반 구성 요소(&#39;ng-text&#39;: /libs/mobileapps/components/angular/ng-text 등)에서 overhead.jsp를 사용하여 template.jsp에서 모든 Java 코드를 제거할 수 있습니다. 그런 다음 template.jsp에서 참조되며 요청에 노출하는 모든 변수를 사용할 수 있습니다. 이 전략은 프레젠테이션에서 논리를 분리하는 것을 장려하고 새 구성 요소가 기존 구성 요소에서 파생될 때 복사하여 붙여넣어야 하는 코드의 양을 제한합니다.

### controller.js.jsp {#controller-js-jsp-1}

[AEM 페이지 템플릿](/help/mobile/apps-architecture.md)에 설명된 대로 각 구성 요소는 `data` 약속에 의해 노출된 JSON 콘텐츠를 사용하도록 JavaScript 조각을 출력할 수 있습니다. angular 규칙에 따라 컨트롤러는 범위에 변수를 할당하는 데만 사용해야 합니다.

### angular.json.jsp {#angular-json-jsp}

angular 이 스크립트는 ng-page를 확장하는 각 페이지에 대해 내보내는 페이지 범위의 &quot;&lt;page-name>.page.json&quot; 파일에 조각으로 포함되어 있습니다. 이 파일에서 구성 요소 개발자는 구성 요소에 필요한 JSON 구조를 모두 노출할 수 있습니다. ng-text 예에서 이 구조는 구성 요소의 텍스트 콘텐츠와 구성 요소에 리치 텍스트가 포함되는지 여부를 나타내는 플래그를 간단히 포함합니다.

We.Retail 앱 제품 구성 요소는 보다 복잡한 예(/apps/weretail-app/components/angular/ng-product)입니다.

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

## CLI Assets 다운로드 내용 {#contents-of-the-cli-assets-download}

앱 콘솔에서 CLI 자산을 다운로드하여 특정 플랫폼에 맞게 최적화한 다음 PhoneGap 명령줄 통합(CLI) API를 사용하여 앱을 빌드합니다. 로컬 파일 시스템에 저장하는 ZIP 파일의 내용은 다음과 같은 구조를 갖습니다.

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

현재 OS 설정에 따라 표시되지 않을 수 있는 숨겨진 디렉터리입니다. 포함된 앱 후크를 수정할 계획인 경우 이 디렉터리가 표시되도록 OS를 구성해야 합니다.

### .cordova/hooks/ {#cordova-hooks}

이 디렉터리에 [CLI 후크](https://gist.github.com/jlcarvalho/22402d013bc72f795d45a01836ce735c)가 있습니다. hooks 디렉토리의 폴더에는 작성 중에 정확한 지점에서 실행되는 node.js 스크립트가 있습니다.

### .cordova/hooks/after-platform_add/ {#cordova-hooks-after-platform-add}

after-platform_add 디렉터리에 `copy_AMS_Conifg.js` 파일이 있습니다. 이 스크립트는 Adobe Mobile Services 분석 컬렉션을 지원하는 구성 파일을 복사합니다.

### .cordova/hooks/after-prepare/ {#cordova-hooks-after-prepare}

준비 후 디렉터리에 `copy_resource_files.js` 파일이 있습니다. 이 스크립트는 여러 아이콘 및 스플래시 화면 이미지를 플랫폼별 위치에 복사합니다.

### .cordova/hooks/before_platform_add/ {#cordova-hooks-before-platform-add}

before_platform_add 디렉터리에 `install_plugins.js` 파일이 있습니다. 이 스크립트는 Cordova 플러그인 식별자 목록을 반복하며, 가 감지한 식별자를 아직 사용할 수 없습니다.

이 전략에서는 Maven `content-package:install` 명령이 실행될 때마다 플러그인을 AEM에 번들로 묶고 설치할 필요가 없습니다. 파일을 SCM 시스템에 체크 인하는 대체 전략은 반복적인 번들 결합 및 설치 활동을 필요로 합니다.

### .cordova/훅/기타 후크 {#cordova-hooks-other-hooks}

필요에 따라 다른 후크를 포함합니다. 다음 후크를 사용할 수 있습니다(Phonegap 샘플 hello world 앱에서 제공).

* after_build
* before_build
* after_compile
* before_compile
* 이후 문서
* 이전_문서
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

### 플랫폼/ {#platforms}

이 디렉터리는 프로젝트에서 `phonegap run *<platform>*` 명령을 실행할 때까지 비어 있습니다. 현재 `*<platform>*`은(는) `ios` 또는 `android`일 수 있습니다.

특정 플랫폼용 앱을 빌드하면 해당 디렉터리가 만들어지고 여기에는 플랫폼별 앱 코드가 포함됩니다.

### plugins/ {#plugins}

plugins 디렉터리는 `phonegap run *<platform>*` 명령을 실행한 후 `.cordova/hooks/before_platform_add/install_plugins.js` 파일에 나열된 각 플러그인으로 채워집니다. 디렉터리가 처음에 비어 있습니다.

### www/ {#www}

www 디렉터리에는 앱의 모양과 동작을 구현하는 모든 웹 콘텐츠(HTML, JS 및 CSS 파일)가 포함되어 있습니다. 아래에 설명된 예외를 제외하고 이 콘텐츠는 AEM에서 시작되며 콘텐츠 동기화를 통해 정적 양식으로 내보내집니다.

### www/config.xml {#www-config-xml}

PhoneGap 설명서(`https://docs.phonegap.com`)에서 이 파일을 &#39;전역 구성 파일&#39;로 참조합니다. config.xml에는 앱 이름, 앱 &#39;환경 설정&#39;(예: iOS 웹 보기에서 오버스크롤을 허용하는지 여부) 및 PhoneGap Build에서 사용하는 *only* 플러그 인 종속성과 같은 많은 앱 속성이 포함되어 있습니다.

config.xml 파일은 AEM의 정적 파일이며 Content Sync를 통해 있는 그대로 내보냅니다.

### www/index.html {#www-index-html}

index.html 파일이 앱의 시작 페이지로 리디렉션됩니다.

config.xml 파일에 `content` 요소가 있습니다.

`<content src="content/phonegap/weretail/apps/ng-we-retail/en.html" />`

PhoneGap 설명서(`https://docs.phonegap.com`)에서 이 요소는 &quot;선택적 &lt;content> 요소는 최상위 웹 자산 디렉터리에 있는 앱의 시작 페이지를 정의합니다. 기본값은 프로젝트의 최상위 www 디렉토리에 일반적으로 나타나는 index.html입니다.&quot;

index.html 파일이 없으면 PhoneGap Build가 실패합니다. 따라서 이 파일이 포함됩니다.

### www/res {#www-res}

res 디렉토리에는 스플래시 화면 이미지와 아이콘이 있습니다. `copy_resource_files.js` 스크립트는 `after_prepare` 빌드 단계 동안 플랫폼별 위치에 파일을 복사합니다.

### www/etc {#www-etc}

규칙에 따라 AEM에서 /etc 노드는 정적 clientlib 콘텐츠를 포함합니다. etc 디렉토리에는 Topcoat, AngularJS 및 We.Retail ng-clientlibsall 라이브러리가 포함됩니다.

### www/apps {#www-apps}

앱 디렉토리에는 스플래시 페이지와 관련된 코드가 포함되어 있습니다. AEM 앱의 시작 페이지의 고유한 특징은 사용자 상호 작용 없이 앱을 초기화한다는 것입니다. 따라서 앱의 clientlib 콘텐츠(CSS 및 JS 모두)는 성능을 최대화하기 위해 최소한입니다.

### www/content {#www-content}

콘텐츠 디렉터리에는 앱의 나머지 웹 콘텐츠가 포함되어 있습니다. 콘텐츠는 다음 파일을 포함할 수 있지만 이에 국한되지는 않습니다.

* AEM에서 직접 작성된 HTML 페이지 컨텐츠
* AEM 구성 요소와 연결된 이미지 자산
* 서버측 스크립트가 생성하는 JavaScript 콘텐츠
* 페이지 또는 구성 요소 콘텐츠를 설명하는 JSON 파일

### www/package.json {#www-package-json}

package.json 파일은 **full** Content Sync 다운로드에 포함된 파일을 나열하는 매니페스트 파일입니다. 이 파일에는 콘텐츠 동기화 페이로드가 생성된 타임스탬프(`lastModified`)도 포함되어 있습니다. 이 속성은 AEM에서 앱의 부분 업데이트를 요청할 때 사용됩니다.

### www/package-update.json {#www-package-update-json}

이 페이로드가 전체 앱의 다운로드인 경우 이 매니페스트에는 `package.json`과(와) 같은 정확한 파일 목록이 포함됩니다.

그러나 이 페이로드가 부분 업데이트인 경우 `package-update.json`에는 이 특정 페이로드에 포함된 파일만 포함됩니다.
