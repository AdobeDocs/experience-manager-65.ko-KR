---
title: SPA(Single Page Applications)
seo-title: SPA(Single Page Applications)
description: 이 페이지에 따라 단일 페이지 애플리케이션에 대해 알아보십시오. 즉, 데스크탑 또는 모바일 애플리케이션과 동일하게 수행되는 애플리케이션을 만들 수 있습니다.
seo-description: 이 페이지에 따라 단일 페이지 애플리케이션에 대해 알아보십시오. 즉, 데스크탑 또는 모바일 애플리케이션과 동일하게 수행되는 애플리케이션을 만들 수 있습니다.
uuid: d1865e79-6e7c-4149-95c0-556e61478b01
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
discoiquuid: a5b5e40e-2457-45fe-9632-baf5008fe8bf
exl-id: daf7bf39-a105-46eb-ab7b-1c59484949e2
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1015'
ht-degree: 1%

---

# SPA(Single Page Applications){#single-page-applications}

>[!NOTE]
>
>단일 페이지 애플리케이션 프레임워크 기반 클라이언트측 렌더링(예: React)이 필요한 프로젝트에 SPA 편집기를 사용하는 것이 좋습니다. [추가 정보](/help/sites-developing/spa-overview.md).

[SPA(Single-Page Applications](https://en.wikipedia.org/wiki/Single-page_application) )은 웹 기술을 사용하여 원활한 경험을 구축할 수 있는 가장 효과적인 패턴으로 널리 간주되어 중요한 규모에 도달했습니다. SPA 패턴을 따르면 데스크탑 또는 모바일 애플리케이션과 동일하게 수행되지만 개방형 웹 표준의 기본 설정으로 인해 많은 장치 플랫폼 및 양식 요소에 도달하는 애플리케이션을 만들 수 있습니다.

일반적으로 SPA은 일반적으로 전체 HTML 페이지 **를 한 번만 로드하고(CSS, JS 및 지원 글꼴 컨텐츠 포함) 앱에서 상태 변경이 발생할 때마다 필요한 항목만 정확히 로드하므로 기존 페이지 기반 웹 사이트보다 성능이 더 우수합니다.** 이 상태 변경에 필요한 사항은 선택한 기술 세트에 따라 달라질 수 있지만, 일반적으로 기존 &#39;view&#39;를 대체하기 위한 단일 HTML 조각 및 새 보기를 연결하고 필요한 모든 클라이언트 측 템플릿 렌더링을 수행하는 JS 코드 블록 실행이 포함되어 있습니다. 템플릿 캐싱 메커니즘을 지원하거나 Adobe PhoneGap을 사용하는 경우 템플릿 컨텐츠에 대한 오프라인 액세스를 통해 이 상태 변경 속도를 더 향상시킬 수 있습니다.

AEM 6.1은 AEM 앱을 통해 SPA의 빌드 및 관리를 지원합니다. 이 문서에서는 SPA의 개념 및 [AngularJS](https://angularjs.org/)를 활용하여 브랜드를 앱스토어와 Google Play에 가져오는 방법을 소개합니다.

## AEM 앱의 SPA {#spa-in-aem-apps}

AEM 앱의 단일 페이지 애플리케이션 프레임워크를 사용하면 AngularJS 앱의 고성능 기능을 사용할 수 있을 뿐만 아니라 작성자(또는 기타 기술 담당자가 아닌 경우)가 웹 사이트 관리를 위해 전통적으로 예약된 터치에 적합한 드래그 앤 드롭 편집기 환경을 통해 앱 컨텐츠를 만들고 관리할 수 있습니다. AEM으로 사이트가 이미 만들어졌습니까? AEM 앱을 사용하면 콘텐츠, 구성 요소, 워크플로우, 자산 및 권한을 쉽게 재사용할 수 있습니다.

## AngularJS 응용 프로그램 모듈 {#angularjs-application-module}

AEM 앱은 앱의 최상위 모듈 통합을 포함하여 AngularJS 구성의 대부분을 처리합니다. 기본적으로 이 모듈의 이름은 &#39;AEMAngularApp&#39;이며, 이 모듈의 생성을 담당하는 스크립트는 /libs/mobileapps/components/angular/ng-page/angular-app-module.js.jsp에서 찾을 수 있습니다.

앱의 초기화 부분에는 앱이 종속되는 AngularJS 모듈을 지정하는 작업이 포함됩니다. 앱에서 사용하는 모듈 목록은 /libs/mobileapps/components/angular/ng-page/angular-module-list.js.jsp에 있는 스크립트에 의해 지정되며, 앱에 필요한 추가 AngularJS 모듈을 가져올 수 있도록 자체 앱의 페이지 구성 요소에 의해 오버레이될 수 있습니다. 예를 들어, 위의 스크립트를 Geometrixx 구현(/apps/geometrixx-outdoors-app/components/angular/ng-geometrixx-page/angular-module-list.js.jsp)과 비교합니다.

앱의 개별 상태 간 탐색을 지원하기 위해 angular-앱 모듈 스크립트는 최상위 앱 페이지의 모든 하위 페이지를 반복하여 &#39;경로&#39; 세트를 생성하고 Angular의 $routeProvider 서비스에서 각 경로를 구성합니다. 이것이 실제로 어떻게 보이는지에 대한 예를 보려면 Geometrixx Outdoors 앱 샘플에서 생성한 angular-앱 모듈 스크립트를 살펴보십시오.(링크에는 로컬 인스턴스가 필요합니다.) [http://localhost:4502/content/phonegap/conference-app/en/home.angular-app-module.js](http://localhost:4502/content/phonegap/conference-app/en/home.angular-app-module.js)

생성된 AEMngularApp으로 를 확장하면 다음과 같이 지정된 일련의 경로를 찾을 수 있습니다.

```xml
$routeProvider
.when('/content/phonegap/geometrixx-outdoors/en/home/products/:id', {
    templateUrl: 'home/products.template.html',
    controller: 'contentphonegapgeometrixxoutdoorsenhomeproducts'
})
```

위의 샘플에서는 특히 경로의 일부로 매개 변수 전달의 예를 보여줍니다. 이 예에서는 지정된 패턴(/content/phonegap/geometrixx-outdoors/en/home/products/:id)을 충족하는 경로가 요청되면 home/products.template.html 템플릿에서 처리되고 &#39;contentphonegapgeometrioutdoors&#39; 컨트롤러를 사용하라는 메시지가 표시됩니다.

이 경로가 요청될 때 로드할 템플릿은 templateUrl 속성에 의해 지정됩니다. 이 템플릿에는 페이지에 포함된 AEM 구성 요소의 HTML과 응용 프로그램의 클라이언트 측 배선에 필요한 AngularJS 지시어가 포함됩니다. Geometrixx 구성 요소에 있는 AngularJS 지시문의 예는 스와이프 회전판의 template.jsp(/apps/geometrixx-outdoors-app/components/swipe-carousel/template.jsp) 중 45행을 살펴봅니다.

## 페이지 컨트롤러 {#page-controllers}

angular의 고유한 단어에서는 &quot;Controller는 Angular 범위를 늘리는 데 사용되는 JavaScript 생성자 함수입니다.&quot; ([source](https://docs.angularjs.org/guide/controller)) AEM 앱의 각 페이지는 `angular`의 `frameworkType`를 지정하는 컨트롤러에 의해 증강 가능한 컨트롤러에 자동으로 연결되어 있습니다. 이 구성 요소가 페이지에 추가될 때마다 이 중요한 속성이 페이지에 포함되어 있는지 확인하는 cq:template 노드를 포함하여 ng-text 구성 요소를 예(/libs/mobileapps/components/angular/ng-text)로 살펴봅니다.

보다 복잡한 컨트롤러 예를 보려면 ng-template-page controller.jsp 스크립트(/apps/geometrixx-outdoors-app/components/angular/ng-template-page)를 엽니다. 특히 실행 시 생성되는 javascript 코드가 다음과 같이 렌더링됩니다.

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

위의 예에서는 `$routeParams` 서비스에서 매개 변수를 가져온 다음 JSON 데이터가 저장된 디렉토리 구조로 마사지하도록 하겠습니다. 이러한 방식으로 sku `id`를 처리하여 수천 개의 개별 제품에 대한 제품 데이터를 렌더링할 수 있는 단일 제품 템플릿을 제공할 수 있습니다. 대규모 제품 데이터베이스의 각 항목에 대해 개별 경로를 필요로 하는 훨씬 더 확장 가능한 모델입니다.

또한 두 가지 구성 요소가 작업 중입니다.ng-product는 위의 `$http` 호출에서 추출하는 데이터로 범위를 늘립니다. 이 페이지에는 응답 이미지도 있으며 응답에서 검색한 값으로 범위를 늘립니다. angular의 `$http` 서비스를 통해 각 구성 요소는 요청이 완료되고 생성된 약속이 이행될 때까지 참으면서 기다립니다.

## 다음 단계 {#the-next-steps}

단일 페이지 애플리케이션에 대해 학습한 후에는 [PhoneGap CLI를 사용하여 앱 개발](/help/mobile/phonegap-apps-pg-cli.md)을 참조하십시오.
