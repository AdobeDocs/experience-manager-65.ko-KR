---
title: SPA (Single Page Applications)
description: 이 페이지를 따라 단일 페이지 애플리케이션에 대해 알아보십시오. 즉, 데스크탑 또는 모바일 애플리케이션과 동일하게 수행되는 애플리케이션을 만들 수 있습니다.
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
exl-id: daf7bf39-a105-46eb-ab7b-1c59484949e2
solution: Experience Manager
feature: Mobile
role: Admin
source-git-commit: 2dae56dc9ec66f1bf36bbb24d6b0315a5f5040bb
workflow-type: tm+mt
source-wordcount: '930'
ht-degree: 0%

---

# SPA (Single Page Applications){#single-page-applications}

{{ue-over-mobile}}

[단일 페이지 애플리케이션](https://en.wikipedia.org/wiki/Single-page_application)(SPA)이 웹 기술을 사용하여 원활한 경험을 구축하는 데 가장 효과적인 패턴으로 널리 간주되는 중요한 대규모에 도달했습니다. SPA 패턴을 따라 데스크탑 또는 모바일 애플리케이션과 동일하게 수행되지만 개방형 웹 표준에서의 기반 때문에 다양한 디바이스 플랫폼 및 폼 팩터에 도달하는 애플리케이션을 만들 수 있습니다.

일반적으로 SPA은 전체 HTML 페이지 **한 번만**(CSS, JS 및 지원 글꼴 콘텐츠 포함)을 로드한 다음 앱에서 상태가 변경될 때마다 필요한 항목만 로드하므로 기존 페이지 기반 웹 사이트보다 성능이 향상됩니다. 이 상태 변경에 필요한 사항은 선택한 기술 세트에 따라 다를 수 있지만, 일반적으로 기존 &#39;보기&#39;를 대체할 단일 HTML 조각과 새 보기를 연결하고 필요할 수 있는 모든 클라이언트측 템플릿 렌더링을 수행하는 JS 코드 블록 실행을 포함합니다. 템플릿 캐싱 메커니즘을 지원하거나 Adobe PhoneGap을 사용하는 경우 템플릿 콘텐츠에 대한 오프라인 액세스를 통해 이 상태 변경 속도를 더욱 향상시킬 수 있습니다.

AEM 6.1은 AEM 앱을 통해 SPA의 구축 및 관리를 지원합니다. 이 문서에서는 SPA에 포함된 개념과 [AngularJS](https://angularjs.org/)을(를) 사용하여 브랜드를 App Store 및 Google Play으로 가져오는 방법에 대해 소개합니다.

## AEM 앱의 SPA {#spa-in-aem-apps}

AEM Apps의 단일 페이지 애플리케이션 프레임워크를 사용하면 AngularJS 앱의 고성능을 활성화하면서도 작성자(또는 기타 비기술 담당자)는 전통적으로 웹 사이트 관리에 예약되어 있던 터치 최적화, 드래그 앤 드롭 편집기 환경을 통해 앱의 콘텐츠를 만들고 관리할 수 있습니다. AEM으로 사이트가 이미 구축되어 있습니까? AEM 앱에서는 콘텐츠, 구성 요소, 워크플로우, 에셋 및 권한을 쉽게 재사용할 수 있습니다.

## AngularJS 애플리케이션 모듈 {#angularjs-application-module}

AEM Apps는 앱의 최상위 모듈을 구성하는 등 AngularJS 구성의 대부분을 처리합니다. 기본적으로 이 모듈의 이름은 &#39;AEMAngularApp&#39;이며 해당 생성을 담당하는 스크립트는 /libs/mobileapps/components/angular/ng-page/angular-app-module.js.jsp에서 찾을 수 있습니다(및 오버레이됨).

앱 초기화의 일부에는 앱이 종속된 AngularJS 모듈을 지정하는 작업이 포함됩니다. 앱에서 사용하는 모듈 목록은 /libs/mobileapps/components/angular/ng-page/angular-module-list.js.jsp에 있는 스크립트에 의해 지정되며 앱의 페이지 구성 요소에 의해 오버레이되어 앱에 필요한 추가 AngularJS 모듈을 가져올 수 있습니다. 예를 들어 위의 스크립트를 Geometrixx 구현(/apps/geometrixx-outdoors-app/components/angular/ng-geometrixx-page/angular-module-list.js.jsp에 있음)과 비교합니다.

앱의 고유한 상태 간 탐색을 지원하기 위해 angular-앱-모듈 스크립트는 최상위 앱 페이지의 모든 하위 페이지를 반복하여 &#39;경로&#39; 집합을 생성하고 Angular의 $routeProvider 서비스에서 각 경로를 구성합니다. 실제 모습의 예를 보려면 Geometrixx Outdoors 앱 샘플에서 생성된 angular 앱 모듈 스크립트를 참조하십시오. (링크는 로컬 인스턴스가 필요) [http://localhost:4502/content/phonegap/conference-app/en/home.angular-app-module.js](http://localhost:4502/content/phonegap/conference-app/en/home.angular-app-module.js)

생성된 AEMAngularApp을 자세히 살펴보면 다음과 같이 일련의 경로가 지정됩니다.

```xml
$routeProvider
.when('/content/phonegap/geometrixx-outdoors/en/home/products/:id', {
    templateUrl: 'home/products.template.html',
    controller: 'contentphonegapgeometrixxoutdoorsenhomeproducts'
})
```

특히 위의 샘플은 경로의 일부로서 파라미터를 전달하는 예를 예시한다. 이 예에서는 지정된 패턴(/content/phonegap/geometrixx-outdoors/en/home/products/:id)을 충족하는 경로가 요청되면 home/products.template.html 템플릿으로 처리하고 &#39;contentphonegapgeometrixxoutdoorsenhomeproducts&#39; 컨트롤러를 사용해야 함을 나타냅니다.

이 경로가 요청될 때 로드할 템플릿은 templateUrl 속성에 의해 지정됩니다. 이 템플릿에는 페이지에 포함된 AEM 구성 요소의 HTML과 애플리케이션의 클라이언트측 배선에 필요한 AngularJS 지시문이 포함되어 있습니다. Geometrixx 구성 요소의 AngularJS 지시문 예제를 보려면 스와이프-캐러셀의 template.jsp(/apps/geometrixx-outdoors-app/components/swipe-carousel/template.jsp)의 45행을 살펴보십시오.

## 페이지 컨트롤러 {#page-controllers}

angular 자신의 표현으로, &quot;컨트롤러는 Angular 범위를 확장하는 데 사용되는 JavaScript 생성자 함수입니다.&quot; ([source](https://docs.angularjs.org/guide/controller)) AEM 앱의 각 페이지는 `angular`의 `frameworkType`을(를) 지정하는 모든 컨트롤러에 의해 추가될 수 있는 컨트롤러까지 자동으로 배선됩니다. angular 예로서 ng-text 구성 요소(/libs/mobileapps/components/template/ng-text)를 살펴봅니다. cq:template 노드는 이 구성 요소가 페이지에 추가될 때마다 이 중요한 속성을 포함하도록 합니다.

보다 복잡한 컨트롤러 예제의 경우 ng-template-page controller.jsp 스크립트( /apps/geometrixx-outdoors-app/components/angular/ng-template-page에서)를 엽니다. 특히 중요한 것은 실행 시 생성되는 JavaScript 코드이며, 이는 다음과 같이 렌더링됩니다.

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

위의 예에서는 `$routeParams` 서비스의 매개 변수를 가져온 다음 JSON 데이터가 저장된 디렉터리 구조로 마스터합니다. 이러한 방식으로 SKU `id`을(를) 처리하면 잠재적으로 수천 개의 개별 제품에 대한 제품 데이터를 렌더링할 수 있는 단일 제품 템플릿을 제공할 수 있습니다. 이는 (잠재적으로) 대규모 제품 데이터베이스의 각 항목에 대한 개별 경로가 필요한 훨씬 확장 가능한 모델입니다.

여기에는 두 가지 구성 요소도 있습니다. ng-product는 위의 `$http` 호출에서 추출한 데이터로 범위를 늘립니다. 또한 이 페이지에는 ng-image가 있으며, 이는 또한 응답에서 검색하는 값으로 범위를 늘립니다. angular의 `$http` 서비스를 통해 각 구성 요소는 요청이 완료되고 만들어진 약속이 이행될 때까지 인내심을 가지고 기다립니다.

## 다음 단계 {#the-next-steps}

단일 페이지 애플리케이션에 대한 자세한 내용은 [PhoneGap CLI를 사용하여 앱 개발](/help/mobile/phonegap-apps-pg-cli.md)을 참조하십시오.
