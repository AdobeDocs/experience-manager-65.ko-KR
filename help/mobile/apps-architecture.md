---
title: 모바일 앱용 페이지 템플릿
description: 페이지 템플릿에 대한 자세한 내용을 보려면 이 페이지를 따르십시오. 앱에 대해 만드는 페이지 구성 요소는 /libs/mobileapps/components/angular/ng-page 구성 요소를 기반으로 합니다.
uuid: c53901c9-5974-4c6b-ac61-1c094a93c9d6
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-on-demand-services-app
discoiquuid: cfc7ad16-965e-4075-bc4d-5630abeaba55
exl-id: 397def36-45b2-47a7-b103-99ca22b6dae1
source-git-commit: f4b6eb2ded17ec641f23a1fc3b977ce77169c8a1
workflow-type: tm+mt
source-wordcount: '2666'
ht-degree: 0%

---

# 모바일 앱용 페이지 템플릿 {#page-templates-for-mobile-apps}

>[!NOTE]
>
>단일 페이지 애플리케이션 프레임워크 기반 클라이언트측 렌더링(예: React)이 필요한 프로젝트에 SPA 편집기를 사용하는 것이 좋습니다. [자세히 알아보기](/help/sites-developing/spa-overview.md).

## 모바일 앱용 페이지 템플릿 {#page-templates-for-mobile-apps-1}

앱에 대해 만드는 페이지 구성 요소는 /libs/mobileapps/components/angular/ng-page 구성 요소([로컬 서버에서 CRXDE Lite으로 열기](http://localhost:4502/crx/de/index.jsp#/libs/mobileapps/components/angular/ng-page)). 이 구성 요소에는 구성 요소가 상속하거나 재지정하는 다음 JSP 스크립트가 포함되어 있습니다.

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

응용 프로그램의 이름을 `applicationName` 및 는 pageContext를 통해 노출합니다.

head.jsp 및 body.jsp를 포함합니다.

### head.jsp {#head-jsp}

에 대한 쓰기 `<head>` 앱 페이지의 요소.

앱의 뷰포트 메타 속성을 재정의하려면 재정의하는 파일입니다.

다음의 우수 사례를 통해 앱은 클라이언트 라이브러리의 css 부분을 헤드에 포함하고 JS는 닫기 &lt; `body>` 요소를 생성하지 않습니다.

### body.jsp {#body-jsp}

angular 페이지의 본문은 wcmMode가 검색되는지(!)에 따라 다르게 렌더링됩니다.= WCMMode.DISABLED) 를 사용하여 페이지를 열었는지 아니면 게시된 페이지로 열었는지 확인합니다.

**작성자 모드**

작성 모드에서는 각 개별 페이지가 별도로 렌더링됩니다. Angular은 페이지 간 라우팅을 처리하지 않으며 페이지의 구성 요소가 포함된 부분 템플릿을 로드하는 데 사용되는 ng-view도 아닙니다. 대신 페이지 템플릿(template.jsp)의 컨텐츠는 `cq:include` 태그에 가깝게 포함했습니다.

이 전략은 작성 기능을 활성화합니다(예: 단락 시스템에서 구성 요소 추가 및 편집, 사이드 킥이나 디자인 모드 등). 변경하지 마십시오. 앱용 페이지와 같이 클라이언트 측 렌더링을 사용하는 페이지는 AEM 작성자 모드에서 제대로 작동하지 않습니다.

template.jsp 포함 파일은 `div` 를 포함하는 요소 `ng-controller` 지시문 이 구조를 사용하면 DOM 컨텐츠를 컨트롤러와 연결할 수 있습니다. 따라서 클라이언트측에서 렌더링되는 페이지가 실패하더라도 개별 구성 요소가 제대로 작동합니다(아래 구성 요소의 섹션 참조).

```xml
<div ng-controller="<c:out value="${controllerNameStripped}"/>">
      <cq:include script="template.jsp"/>
</div>
```

**게시 모드**

게시 모드(예: 컨텐츠 동기화를 사용하여 앱을 내보내는 경우)에서 모든 페이지는 단일 페이지 앱(SPA)이 됩니다. (SPA에 대해 알아보려면 특히 Angular 자습서를 사용하십시오 [https://docs.angularjs.org/tutorial/step_07](https://docs.angularjs.org/tutorial/step_07))

SPA(페이지를 포함하는 페이지)에는 하나의 HTML 페이지만 있습니다 `<html>` 요소를 생성하지 않습니다. 이 페이지를 &quot;레이아웃 템플릿&quot;이라고 합니다. angular 용어에서 &quot;...애플리케이션의 모든 보기에 공통인 템플릿입니다.&quot; 이 페이지를 &#39;최상위 앱 페이지&#39;로 간주합니다. 규칙에 따라 최상위 앱 페이지는 `cq:Page` 루트와 가장 가까운 응용 프로그램의 노드(리디렉션이 아님)입니다.

앱의 실제 URI가 게시 모드에서 변경되지 않으므로 이 페이지의 외부 자산에 대한 참조는 상대 경로를 사용해야 합니다. 따라서 내보내기를 위해 이미지를 렌더링할 때 이 최상위 페이지를 고려하는 특수 이미지 구성 요소가 제공됩니다.

SPA로서, 이 레이아웃 템플릿 페이지는 단순히 ng-view 지시어가 있는 div 요소를 생성합니다.

```xml
 <div ng-view ng-class="transition"></div>
```

angular 경로 서비스는 이 요소를 사용하여 현재 페이지(template.jsp에 포함됨)의 작성 가능한 내용을 포함하여 앱의 모든 페이지의 내용을 표시합니다.

body.jsp 파일에는 비어 있는 header.jsp 및 footer.jsp가 포함되어 있습니다. 모든 페이지에서 정적 콘텐츠를 제공하려는 경우 앱에서 이러한 스크립트를 재정의할 수 있습니다.

마지막으로 Javascript clientlibs 는 &lt;body> 서버에서 생성된 두 개의 특수 JS 파일을 포함하는 요소: *&lt;page name=&quot;&quot;>*.angular-app-module.js 및 *&lt;page name=&quot;&quot;>*.angular-app-controller.js.

### angular-app-module.js.jsp {#angular-app-module-js-jsp}

이 스크립트는 응용 프로그램의 Angular 모듈을 정의합니다. 이 스크립트의 출력은 나머지 템플릿 구성 요소가 `html` 다음 속성을 포함하는 ng-page.jsp의 요소입니다.

```xml
ng-app="<c:out value='${applicationName}'/>"
```

이 속성은 이 DOM 요소의 컨텐츠가 다음 모듈에 연결되어야 함을 Angular에 표시합니다. 이 모듈은 해당 컨트롤러와 보기를 연결합니다(AEM에서 cq:Page 리소스).

또한 이 모듈은 이름이 인 최상위 컨트롤러를 정의합니다 `AppController` 이 `wcmMode` 변수를 범위로 설정하고, Content Sync 업데이트 페이로드를 가져올 URI를 구성합니다.

마지막으로 이 모듈은 각 하위 페이지(자신 포함)를 반복하여 각 페이지의 경로 연결 관리 컨텐츠를 렌더링합니다(angular-route-fragment.js 선택기 및 확장을 통해). 이를 Angular의 \$routeProvider에 대한 구성 항목으로 포함합니다. 즉, \$routeProvider는 지정된 경로가 요청될 때 렌더링할 콘텐츠를 앱에 알려줍니다.

### angular-route-fragment.js.jsp {#angular-route-fragment-js-jsp}

이 스크립트는 다음 양식을 사용해야 하는 JavaScript 조각을 생성합니다.

```
.when('/<path>', {
    templateUrl: '<path to template>',
    controller: '<controller name>'
})
```

이 코드는 &#39;/( angular-app-module.js.jsp에 정의됨)에 있는 $routeProvider를 나타냅니다.&lt;path>&#39; 은(는) 의 리소스에 의해 처리됩니다. `templateUrl`, 및에 의해 유선 `controller` (다음 단계로 넘어갈게요)

필요한 경우 이 스크립트를 무시하여 변수가 있는 경로를 포함하여 더 복잡한 경로를 처리할 수 있습니다. 이 예는 AEM과 함께 설치된 /apps/geometrixx-outdoors-app/components/angular/ng-template-page/angular-route-fragment.js.jsp 스크립트에서 확인할 수 있습니다.

```xml
// note the :id suffix on the path
.when('<c:out value="${resource.path}"/>/:id', {
    templateUrl: '<c:out value="${relativeResourcePath}"/>.template.html',
    controller: '<c:out value="${controllerNameStripped}"/>'
})
```

### angular-app-controllers.js.jsp {#angular-app-controllers-js-jsp}

angular에서 컨트롤러가 \$범위의 변수를 연결하여 보기에 표시합니다. angular-app-controllers.js.jsp 스크립트는 각 하위 페이지(자신 포함)를 반복하고 각 페이지가 정의하는 컨트롤러 조각을 출력한다는 점에서 angular-app-module.js.jsp로 표시된 패턴을 따릅니다(controller.js.jsp를 통해). 정의하는 모듈을 라고 합니다 `cqAppControllers` 페이지 컨트롤러를 사용할 수 있도록 및 를 최상위 앱 모듈의 종속으로 나열해야 합니다.

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

다음 사항에 유의하십시오. `data` 변수에는 Angular이 반환한 약속이 할당됩니다 `$http.get` 메서드를 사용합니다. 이 페이지에 포함된 각 구성 요소는 원하는 경우 일부 .json 컨텐츠를 해당 angular.json.jsp 스크립트를 통해 사용할 수 있도록 설정하고, 이 컨텐츠가 확인될 때 이 요청의 내용에 대해 작업할 수 있습니다. 요청은 파일 시스템에 액세스하므로 모바일 장치에서 매우 빠릅니다.

구성 요소가 이러한 방식으로 컨트롤러의 일부가 되려면 /libs/mobileapps/components/angular/ng-component 구성 요소를 확장하고 다음을 포함해야 합니다 `frameworkType: angular` 속성을 사용합니다.

### template.jsp {#template-jsp}

body.jsp 섹션에 처음 도입된 template.jsp에는 페이지의 parsys가 포함되어 있습니다. 게시 모드에서 이 컨텐츠는 직접 참조됩니다(다음 위치) &lt;page-path>.template.html)을 설정하고 \$routeProvider에 구성된 templateUrl을 통해 SPA에 로드됩니다.

이 스크립트의 parsys는 모든 유형의 구성 요소를 수락하도록 구성할 수 있습니다. 그러나 기존 웹 사이트용으로 만들어진 구성 요소를 처리할 때에는 주의해야 합니다(SPA과 대조적으로). 예를 들어, 기초 이미지 구성 요소는 앱 내에 있는 자산을 참조하도록 설계되지 않았으므로 최상위 앱 페이지에서만 올바르게 작동합니다.

### angular-module-list.js.jsp {#angular-module-list-js-jsp}

이 스크립트는 최상위 Angular 앱 모듈의 Angular 종속성을 출력하기만 하면 됩니다. angular-app-module.js.jsp에서 참조됩니다.

### header.jsp {#header-jsp}

앱 맨 위에 정적 콘텐츠를 배치하는 스크립트입니다. 이 컨텐츠는 ng-view 범위를 벗어나는 최상위 페이지에 포함됩니다.

### footer.jsp {#footer-jsp}

앱 하단에 정적 콘텐츠를 배치하는 스크립트입니다. 이 컨텐츠는 ng-view 범위를 벗어나는 최상위 페이지에 포함됩니다.

### js_clientlibs.jsp {#js-clientlibs-jsp}

JavaScript clientlibs를 포함하려면 이 스크립트를 재정의합니다.

### css_clientlibs.jsp {#css-clientlibs-jsp}

CSS clientlibs를 포함하려면 이 스크립트를 재정의합니다.

## 앱 구성 요소 {#app-components}

앱 구성 요소는 AEM 인스턴스(게시 또는 작성자)에서만 작동할 뿐만 아니라, 애플리케이션 컨텐츠를 Content Sync를 통해 파일 시스템으로 내보내는 경우에도 작동해야 합니다. 따라서 구성 요소에는 다음 특성이 포함되어야 합니다.

* PhoneGap 응용 프로그램의 모든 자산, 템플릿 및 스크립트는 상대적으로 참조되어야 합니다.
* AEM 인스턴스가 작성자 또는 게시 모드에서 작동 중이면 링크 처리가 다릅니다.

### 상대 자산 {#relative-assets}

PhoneGap 애플리케이션에서 제공된 자산의 URI는 플랫폼별로 다를 뿐만 아니라 앱 설치 시 고유합니다. 예를 들어 iOS 시뮬레이터에서 실행 중인 앱의 다음 URI를 확인합니다.

`file:///Users/userId/Library/Application%20Support/iPhone%20Simulator/7.0.3/Applications/24BA22ED-7D06-4330-B7EB-F6FC73251CA3/Library/files/www/content/phonegap/geometrixx/apps/ng-geometrixx-outdoors/en/home.html`

경로에 GUID &#39;24BA22ED-7D06-4330-B7EB-F6FC73251CA3&#39;을 참고하십시오.

PhoneGap 개발자로서 관심이 있는 컨텐츠는 www 디렉토리 아래에 있습니다. 앱 자산에 액세스하려면 상대 경로를 사용합니다.

이 문제를 해결하려면 PhoneGap 응용 프로그램에서 단일 페이지 앱(SPA) 패턴을 사용하여 기본 URI(해시 제외)가 변경되지 않습니다. 따라서 참조하는 모든 자산, 템플릿 또는 스크립트 **는 최상위 페이지에 상대적이어야 합니다.** 최상위 레벨 페이지는 다음을 기준으로 Angular 라우팅 및 컨트롤러를 초기화합니다 `*<name>*.angular-app-module.js` 및 `*<name>*.angular-app-controllers.js`. 이 페이지는 *sling:redirect를 확장하지 *않는 *저장소의 루트에 가장 가까운 페이지여야 합니다.

상대 경로를 처리하는 데 몇 가지 도우미 방법을 사용할 수 있습니다.

* FrameworkContentExporterUtils.getTopLevelAppResource
* FrameworkContentExporterUtils.getRelativePathToRootLevel
* FrameworkContentExporterUtils.getPathToAsset

사용 예를 보려면 /libs/mobileapps/components/angular에 있는 mobileapps 소스를 엽니다.

### 링크 {#links}

링크는 `ng-click="go('/path')"` 모든 WCM 모드를 지원하는 함수입니다. 이 함수는 링크 작업을 올바르게 결정하기 위해 범위 변수의 값에 따라 달라집니다.

```xml
<c:choose><c:when test="${wcmMode}">
    <%-- WCMMode is enabled - page is being rendered in AEM --%>
    $scope.wcmMode = true;
</c:when><c:otherwise>
    <%-- WCMMode is disabled --%>
    $scope.wcmMode = false;
</c:otherwise></c:choose>
```

When `$scope.wcmMode == true` 변수는 URL의 경로 및/또는 페이지 부분을 변경하도록 일반적인 방법으로 각 탐색 이벤트를 처리합니다.

또는, `$scope.wcmMode == false`로 지정하는 경우, 각 탐색 이벤트는 Angular의 ngRoute 모듈에서 내부적으로 해결된 URL의 해시 부분을 변경합니다.

### 구성 요소 스크립트 세부 사항 {#component-script-details}

![chlimage_1-36](assets/chlimage_1-36.png)

#### ng-component.jsp {#ng-component-jsp}

이 스크립트는 편집 모드가 감지되면 구성 요소 컨텐츠나 적절한 자리 표시자를 표시합니다.

#### template.jsp {#template-jsp-1}

template.jsp 스크립트는 구성 요소의 마크업을 렌더링합니다. 해당 구성 요소가 AEM에서 추출된 JSON 데이터(예: &#39;ng-text&#39;)에 의해 구동되는 경우: /libs/mobileapps/components/angular/ng-text/template.jsp) 그러면 이 스크립트는 페이지의 컨트롤러 범위에 의해 노출된 데이터로 마크업을 배선합니다.

그러나 성능 요구 사항에 따라 클라이언트 측 템플릿(데이터 바인딩)을 수행할 필요가 없는 경우가 있습니다. 이 경우 구성 요소의 마크업을 서버 측에서 렌더링하면 해당 마크업이 페이지 템플릿 컨텐츠에 포함됩니다.

#### overhead.jsp {#overhead-jsp}

JSON 데이터(예: &#39;ng-text&#39;)로 구동되는 구성 요소에서, /libs/mobileapps/components/angular/ng-text), overhead.jsp를 사용하여 template.jsp에서 모든 Java 코드를 제거할 수 있습니다. 그런 다음 template.jsp에서 참조되며 요청에 표시하는 모든 변수를 사용할 수 있습니다. 이 전략은 논리를 프레젠테이션과 분리하도록 권장하며, 새 구성 요소가 기존 구성 요소에서 파생될 때 복사하여 붙여넣어야 하는 코드의 양을 제한합니다.

#### controller.js.jsp {#controller-js-jsp-1}

AEM 페이지 템플릿에 설명된 대로, 각 구성 요소는 JavaScript 조각을 출력하여 페이지에 의해 노출된 JSON 컨텐츠를 사용할 수 있습니다 `data` 약속 다음 Angular 규칙을 따르면, 컨트롤러에 변수를 범위에 지정하는 데만 사용해야 합니다.

#### angular.json.jsp {#angular-json-jsp}

이 스크립트는 페이지 전체에 있는 조각으로 포함됩니다.&lt;page-name>ng-page를 확장하는 각 페이지에 대해 내보내는 .angular.json&#39; 파일입니다. 이 파일에서 구성 요소 개발자는 구성 요소에 필요한 JSON 구조를 노출할 수 있습니다. ng-text 예에서는 이 구조가 구성 요소의 텍스트 컨텐츠와 구성 요소에 리치 텍스트가 포함되어 있는지 여부를 나타내는 플래그를 단순히 포함합니다.

Geometrixx outdoors 앱 제품 구성 요소는 보다 복잡한 예입니다(/apps/geometrixx-outdoors-app/components/angular/ng-product).

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

Apps 콘솔에서 CLI 자산을 다운로드하여 특정 플랫폼용으로 최적화한 다음 PhoneGap CLI(명령줄 통합) API를 사용하여 앱을 빌드합니다. 로컬 파일 시스템에 저장하는 ZIP 파일의 내용은 다음 구조를 갖습니다.

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

현재 OS 설정에 따라 표시되지 않을 수 있는 숨겨진 디렉토리입니다. 포함된 앱 후크를 수정할 계획이 있는 경우 이 디렉토리가 표시되도록 OS를 구성해야 합니다.

#### .cordova/hooks/ {#cordova-hooks}

이 디렉토리에는 다음이 포함됩니다. [CLI 후크](https://devgirl.org/2013/11/12/three-hooks-your-cordovaphonegap-project-needs/). 후크 디렉토리의 폴더에 빌드 중에 정확한 지점에서 실행되는 node.js 스크립트가 있습니다.

#### .cordova/hooks/after-platform_add/ {#cordova-hooks-after-platform-add}

after-platform_add 디렉토리에는 `copy_AMS_Conifg.js` 파일. 이 스크립트는 Adobe Mobile Services Analytics 컬렉션을 지원하도록 구성 파일을 복사합니다.

#### .cordova/hooks/after-prepare/ {#cordova-hooks-after-prepare}

사후 준비 디렉토리에는 `copy_resource_files.js` 파일. 이 스크립트는 많은 아이콘 및 시작 화면 이미지를 플랫폼별 위치에 복사합니다.

#### .cordova/hooks/before_platform_add/ {#cordova-hooks-before-platform-add}

before_platform_add 디렉토리에는 가 포함됩니다. `install_plugins.js` 파일. 이 스크립트는 Cordova 플러그인 식별자 목록을 반복하며 감지된 항목을 아직 사용할 수 없습니다.

이 전략은 Maven을 사용할 때마다 플러그인을 AEM에 번들로 설치하고 설치할 필요가 없습니다 `content-package:install` 명령이 실행됩니다. 파일을 SCM 시스템에 체크 인하는 다른 전략은 반복적인 번들 및 설치 활동을 필요로 합니다.

#### .cordova/hooks/기타 후크 {#cordova-hooks-other-hooks}

필요에 따라 다른 후크를 포함하십시오. Phonegap 샘플 hello world 앱에서 제공하는 대로 다음 후크를 사용할 수 있습니다.

* after_build
* before_build
* after_compile
* before_compile
* after_docs
* before_docs
* after_emulation
* before_emulation
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

#### 플랫폼/ {#platforms}

이 디렉토리는 사용자가 `phonegap run <platform>` 프로젝트에 대한 명령. 현재, `<platform>` 다음 중 하나를 수행할 수 있습니다. `ios` 또는 `android`.

특정 플랫폼용 앱을 빌드하면 해당 디렉토리가 만들어지고 플랫폼별 앱 코드가 포함되어 있습니다.

#### plugins/ {#plugins}

플러그인 디렉토리는 `.cordova/hooks/before_platform_add/install_plugins.js` 실행 후 파일 `phonegap run <platform>` 명령. 디렉터리가 처음에 비어 있습니다.

#### www/ {#www}

www 디렉토리에는 앱의 모양과 동작을 구현하는 모든 웹 컨텐츠(HTML, JS 및 CSS 파일)가 포함되어 있습니다. 아래에 설명된 예외를 제외하고 이 컨텐츠는 AEM에서 생성되며 컨텐츠 동기화를 통해 정적 양식으로 내보내집니다.

#### www/config.xml {#www-config-xml}

다음 [PhoneGap 설명서](https://docs.phonegap.com) 는 이 파일을 &#39;글로벌 구성 파일&#39;로 참조합니다. config.xml에는 앱 이름, 앱 &#39;환경 설정&#39;(예: iOS webview에서 오버스크롤을 허용하는지 여부) 및 다음과 같은 플러그인 종속성이 포함되어 있습니다 *전용* PhoneGap 빌드에 의해 사용됩니다.

config.xml 파일은 AEM의 정적 파일이며 컨텐츠 동기화를 통해 있는 그대로 내보냅니다.

#### www/index.html {#www-index-html}

index.html 파일이 앱의 시작 페이지로 리디렉션됩니다.

config.xml 파일에 `content` 요소:

`<content src="content/phonegap/geometrixx/apps/ng-geometrixx-outdoors/en.html" />`

in [PhoneGap 설명서](https://docs.phonegap.com)로 지정하는 경우 이 요소는 &quot;선택 사항&quot;으로 설명되어 있습니다 &lt;content> 요소는 최상위 웹 자산 디렉터리에서 앱의 시작 페이지를 정의합니다. 기본값은 index.html이며, 이 값은 대개 프로젝트의 최상위 www 디렉터리에 나타납니다.&quot;

index.html 파일이 없으면 PhoneGap 빌드가 실패합니다. 따라서 이 파일이 포함됩니다.

#### www/res {#www-res}

res 디렉토리에는 스플래시 화면 이미지와 아이콘이 있습니다. 다음 `copy_resource_files.js` 스크립트는 `after_prepare` 빌드 단계.

#### www/etc {#www-etc}

규칙에 따라 AEM에서 /etc 노드에는 정적 clientlib 콘텐츠가 포함됩니다. etc 디렉토리에는 Tocoat, AngularJS 및 Geometrixx ng-clientlibsall 라이브러리가 있습니다.

#### www/apps {#www-apps}

apps 디렉토리에는 시작 페이지와 관련된 코드가 있습니다. AEM 앱의 시작 페이지의 고유한 특성은 사용자 상호 작용 없이 앱을 초기화한다는 것입니다. 따라서 앱의 clientlib 콘텐츠(CSS 및 JS 모두)는 성능을 최대화하기 위해 최소한으로 설정됩니다.

#### www/content {#www-content}

컨텐츠 디렉토리에는 앱의 나머지 웹 컨텐츠가 포함되어 있습니다. 컨텐츠에는 다음 파일이 포함될 수 있지만 이에 제한되지 않습니다.

* AEM에서 직접 작성된 HTML 페이지 컨텐츠
* AEM 구성 요소와 연관된 이미지 자산
* 서버측 스크립트가 생성하는 JavaScript 컨텐츠
* 페이지 또는 구성 요소 컨텐츠를 설명하는 JSON 파일

#### www/package.json {#www-package-json}

package.json 파일은 **full** 콘텐츠 동기화 다운로드가 포함됩니다. 이 파일에는 콘텐츠 동기화 페이로드가 생성된 타임스탬프도 포함되어 있습니다(`lastModified`). 이 속성은 AEM에서 앱의 부분 업데이트를 요청할 때 사용됩니다.

#### www/package-update.json {#www-package-update-json}

이 페이로드가 전체 앱의 다운로드인 경우 이 매니페스트에는 파일의 정확한 목록이 포함됩니다. `package.json`.

그러나 이 페이로드가 부분 업데이트인 경우 `package-update.json` 이 특정 페이로드에 포함된 파일만 포함합니다.
