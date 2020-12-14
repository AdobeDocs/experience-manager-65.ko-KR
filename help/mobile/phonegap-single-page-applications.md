---
title: SPA(Single Page Applications)
seo-title: SPA(Single Page Applications)
description: 단일 페이지 애플리케이션에 대해 알아보려면 이 페이지를 따르십시오. 즉, 데스크톱 또는 모바일 응용 프로그램과 동일하게 작동하는 응용 프로그램을 만들 수 있습니다.
seo-description: 단일 페이지 애플리케이션에 대해 알아보려면 이 페이지를 따르십시오. 즉, 데스크톱 또는 모바일 응용 프로그램과 동일하게 작동하는 응용 프로그램을 만들 수 있습니다.
uuid: d1865e79-6e7c-4149-95c0-556e61478b01
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
discoiquuid: a5b5e40e-2457-45fe-9632-baf5008fe8bf
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '1015'
ht-degree: 1%

---


# SPA(Single Page Applications){#single-page-applications}

>[!NOTE]
>
>단일 페이지 애플리케이션 프레임워크 기반 클라이언트측 렌더링(예: 응답)이 필요한 프로젝트에는 SPA 편집기를 사용하는 것이 좋습니다. [추가 정보](/help/sites-developing/spa-overview.md).

[SPA(Single-Page Applications](https://en.wikipedia.org/wiki/Single-page_application) )는 웹 기술을 사용하여 매끄러운 경험을 제작할 수 있는 가장 효과적인 패턴으로 널리 알려져 있습니다. SPA 패턴을 따르면 데스크탑 또는 모바일 애플리케이션과 동일하게 수행하지만 개방형 웹 표준의 기본 요소로 인해 다양한 디바이스 플랫폼과 폼 팩터에 이르는 애플리케이션을 제작할 수 있습니다.

일반적으로 SPA은 전체 HTML 페이지 **를 한 번만 로드하고(CSS, JS 및 지원 글꼴 컨텐츠 포함) 앱에서 상태가 변경될 때마다 필요한 부분만 로드하므로 일반적인 페이지 기반 웹 사이트보다 성능이 더 좋은 것으로 보입니다.** 이러한 상태 변경에 필요한 것은 선택한 기술 집합에 따라 다를 수 있지만, 일반적으로 기존 &#39;보기&#39;를 대체할 단일 HTML 조각 및 JS 코드 블록을 실행하여 새 보기를 연결하고 필요한 클라이언트측 템플릿 렌더링을 수행할 수 있습니다. 템플릿 캐싱 메커니즘을 지원하거나 Adobe PhoneGap을 사용하는 경우 템플릿 컨텐츠에 대한 오프라인 액세스를 지원함으로써 이러한 상태 변경 속도를 더욱 향상시킬 수 있습니다.

AEM 6.1은 AEM Apps를 통해 SPA의 구축 및 관리를 지원합니다. 이 문서에서는 SPA의 개념 및 [AngularJS](https://angularjs.org/)를 활용하여 App Store 및 Google Play에 브랜드를 가져오는 방법에 대해 설명합니다.

## AEM 앱의 SPA {#spa-in-aem-apps}

AEM Apps의 단일 페이지 애플리케이션 프레임워크를 사용하면 AngularJS 앱의 높은 성능을 경험할 수 있을 뿐만 아니라 작성자(또는 기타 기술 지식이 없는 직원)가 웹 사이트 관리용으로 예약되어 온 터치에 최적화된 드래그 앤 드롭 편집기 환경을 통해 앱 컨텐츠를 만들고 관리할 수 있습니다. AEM으로 사이트를 구축한 경우 AEM Apps를 사용하면 컨텐츠, 구성 요소, 워크플로우, 에셋 및 권한을 손쉽게 재활용할 수 있습니다.

## AngularJS 응용 프로그램 모듈 {#angularjs-application-module}

AEM 앱은 앱의 최상위 수준 모듈을 통합하는 등 AngularJS 구성의 상당 부분을 처리합니다. 기본적으로 이 모듈의 이름은 &#39;AEMAngularApp&#39;이며 이 모듈의 생성 작업을 담당하는 스크립트는 /libs/mobileapps/components/angular/ng-page/angular-app-module.js.jsp에서 찾을 수 있습니다.

앱 초기화의 일부에는 앱이 종속되는 AngularJS 모듈을 지정하는 작업이 포함됩니다. 앱에서 사용하는 모듈 목록은 /libs/mobileapps/components/angular/ng-page/angular-module-list.js.jsp에 있는 스크립트에 의해 지정되며, 자신의 앱 페이지 구성 요소에 의해 오버레이되어 앱에 필요한 추가 AngularJS 모듈을 가져올 수 있습니다. 예를 들어 위의 스크립트를 Geometrixx 구현(/apps/geometrixx-outdoors-app/components/angular/ng-geometrixx-page/angular-module-list.js.jsp)과 비교합니다.

앱의 개별 상태 간 탐색을 지원하기 위해 각 앱 모듈 스크립트는 최상위 앱 페이지의 모든 하위 페이지를 반복하여 &#39;경로&#39; 세트를 생성하고 각 경로를 Angular의 $routeProvider 서비스에 구성합니다. 이러한 방식이 실제로 어떻게 보이는지 예를 보려면 Geometrixx Outdoors 앱 샘플에서 생성된 각단-앱 모듈 스크립트를 살펴보십시오.(링크는 로컬 인스턴스가 필요) [http://localhost:4502/content/phonegap/conference-app/en/home.angular-app-module.js](http://localhost:4502/content/phonegap/conference-app/en/home.angular-app-module.js)

생성된 AEMAngularApp으로 검색하면 다음과 같이 지정된 일련의 경로를 찾을 수 있습니다.

```xml
$routeProvider
.when('/content/phonegap/geometrixx-outdoors/en/home/products/:id', {
    templateUrl: 'home/products.template.html',
    controller: 'contentphonegapgeometrixxoutdoorsenhomeproducts'
})
```

특히 위의 샘플에서는 매개 변수를 경로의 일부로 전달하는 예를 보여 줍니다. 이 예에서는 지정된 패턴(/content/phonegap/geometrixx-outdoors/en/home/products/:id)을 충족하는 경로가 요청된 경우 home/products.template.html 템플릿으로 처리되어야 하며 &#39;contentphonegapgeometrioutdoors&#39; outdoors&#39; 컨트롤러를 사용해야 합니다.

이 경로가 요청될 때 로드할 템플릿은 templateUrl 속성에 의해 지정됩니다. 이 템플릿에는 페이지에 포함된 AEM 구성 요소의 HTML과 애플리케이션의 클라이언트 측 배선에 필요한 AngularJS 지시어가 포함됩니다. Geometrixx 구성 요소의 AngularJS 지시문의 예를 보려면 스와이프 회전판의 template.jsp(/apps/geometrixx-outdoors-app/components/swipe-carousel/template.jsp)의 45행을 확인하십시오.

## 페이지 컨트롤러 {#page-controllers}

Angular의 자체 단어에서 &quot;컨트롤러는 각 범위를 증가시키는 데 사용되는 JavaScript 생성자 함수입니다.&quot; ([source](https://docs.angularjs.org/guide/controller)) AEM App의 각 페이지는 `angular`의 `frameworkType`를 지정하는 모든 컨트롤러가 추가할 수 있는 컨트롤러에 자동으로 연결됩니다. 이 구성 요소가 페이지에 추가될 때마다 이 중요한 속성이 포함되어 있는지 확인할 수 있는 cq:template 노드를 포함하여 ng-text 구성 요소를 예(/libs/mobileapps/components/angular/ng-text)로 봅니다.

좀 더 복잡한 컨트롤러 예를 보려면, ng-template-page controller.jsp 스크립트(/apps/geometrixx-outdoors-app/components/angular/ng-template-page)를 여십시오. 특히 실행 시 생성되는 javascript 코드는 다음과 같이 렌더링됩니다.

```xml
// Controller for page 'products'
.controller('contentphonegapgeometrixxoutdoorsenhomeproducts', ['$scope', '$http', '$routeParams',
    function($scope, $http, $routeParams) {
        var sku = $routeParams.id;
        var productPath = '/' + sku.substring(0, 2) + '/' + sku.substring(0, 4) + '/' + sku;
        var data = $http.get('home/products' + productPath + '.angular.json' + cacheKiller);

        /* ng-product component controller (path: content-par/ng-product) */
        data.then(function(response) {
            $scope.contentparngproduct = response.data["content-par/ng-product"].items;
        });

        /* ng-image component controller (path: content-par/ng-product/ng-image) */
        data.then(function(response) {
            $scope.contentparngproductngimage = response.data["content-par/ng-product/ng-image"].items;
        });
    }
])
```

위의 예에서 `$routeParams` 서비스에서 매개 변수를 가져온 다음 JSON 데이터가 저장되어 있는 디렉토리 구조에 매개 변수를 정렬하는 것을 확인할 수 있습니다. 이러한 방식으로 sku `id`를 처리함으로써 잠재적으로 수천 개의 고유 제품에 대한 제품 데이터를 렌더링할 수 있는 단일 제품 템플릿을 제공할 수 있습니다. 대규모 제품 데이터베이스의 각 항목에 대한 개별 경로가 필요한 훨씬 확장 가능한 모델입니다.

여기에는 두 가지 구성 요소도 있습니다.ng-product는 위의 `$http` 호출에서 추출되는 데이터로 범위를 늘립니다. 이 페이지에는 응답에서 검색하는 값으로 범위가 확장되는 ng-이미지도 있습니다. Angular의 `$http` 서비스를 통해 각 구성 요소는 요청이 완료되고 생성된 약속이 이행될 때까지 참을성 있게 기다립니다.

## 다음 단계 {#the-next-steps}

단일 페이지 애플리케이션에 대해 알게 되면 [PhoneGap CLI를 사용하여 앱 개발](/help/mobile/phonegap-apps-pg-cli.md)을 참조하십시오.
