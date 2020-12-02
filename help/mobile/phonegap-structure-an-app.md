---
title: 앱 구조
seo-title: 앱 구조
description: 앱의 구조를 만드는 방법에 대해 알려면 이 페이지를 따르십시오. 이 페이지에서는 JavaScript 및 CSS Clientlibs에 대한 정보와 함께 템플릿 및 구성 요소를 구조화하는 방법을 설명합니다.
seo-description: 앱의 구조를 만드는 방법에 대해 알려면 이 페이지를 따르십시오. 이 페이지에서는 JavaScript 및 CSS Clientlibs에 대한 정보와 함께 템플릿 및 구성 요소를 구조화하는 방법을 설명합니다.
uuid: bf0e8b0c-a075-4847-b56d-de458715027c
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
discoiquuid: c614a7ff-0d13-4407-bda0-c0a402a13dcd
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '973'
ht-degree: 0%

---


# 앱 구조화{#structure-an-app}

>[!NOTE]
>
>단일 페이지 애플리케이션 프레임워크 기반 클라이언트측 렌더링(예: 응답)이 필요한 프로젝트에서는 SPA 편집기를 사용하는 것이 좋습니다. [추가 정보](/help/sites-developing/spa-overview.md).

AEM Mobile 프로젝트에는 페이지, JavaScript 및 CSS 클라이언트 라이브러리, 재사용 가능한 AEM 구성 요소, Content Sync 구성 및 PhoneGap 앱 셸 컨텐츠 등 다양한 유형의 컨텐츠 세트가 포함되어 있습니다. 새로운 AEM Mobile 앱을 [Starter Kit](https://github.com/Adobe-Marketing-Cloud-Apps/aem-phonegap-starter-kit)에 따라 만드는 것은 이식성과 장기적으로 유지 관리 기능을 간소화할 수 있도록 다양한 유형의 컨텐츠를 Adobe의 권장 구조로 가져오는 좋은 방법입니다.

## 페이지 컨텐츠 {#page-content}

애플리케이션의 페이지는 모두 AEM Mobile 콘솔에서 인식할 수 있도록 /content/mobileapps 아래에 위치해야 합니다.

![chlimage_1-52](assets/chlimage_1-52.png)

AEM 규칙으로 인해 앱의 첫 페이지는 앱의 기본 언어(&#39;en&#39;, Geometrixx 및 Starter Kit 케이스 모두에서)로 사용되는 1차 하위 페이지로 리디렉션되어야 합니다. 최상위 로케일 페이지는 일반적으로 기초 &#39;splash-page&#39; 구성 요소(/libs/mobileapps/components/splash-page)에서 상속됩니다. 이 구성 요소는 오버에어 컨텐츠 동기화 업데이트 설치를 지원하는 데 필요한 초기화를 처리합니다(contentInit 코드는 /etc/clientlibs/mobile/content-sync/js/contentInit.js에 있음).

## 템플릿 및 구성 요소 {#templates-and-components}

앱에 대한 템플릿 및 구성 요소 코드는 /apps/&lt;브랜드 이름>/&lt;앱 이름>에 있어야 합니다. 규칙에 따라 /apps/&lt;브랜드 이름>/&lt;앱 이름>에 템플릿 및 구성 요소 코드를 삽입해야 합니다. 이 패턴은 AEM에서 Site를 사용하여 이미 작업한 개발자에게 익숙해야 합니다. 게시 인스턴스의 경우 기본적으로 익명 액세스가 가능하도록 /apps/가 잠겨져 있기 때문에 그 뒤에 옵니다. 따라서 Raw JSP 코드는 잠재적 침입자로부터 숨겨집니다.

앱 특정 템플릿은 템플릿 자체의 `allowedPaths` 속성 노드를 사용하고 해당 값을 &#39;/content/mobileapps(/)로 설정하여 제공할 수만 있도록 구성할 수 있습니다.&amp;ast;)?&#39; - 또는 템플릿을 단일 앱에서만 사용할 수 있어야 하는 경우 더욱 구체적으로 적용할 수 있습니다. 또한 `allowedParents` 및 `allowedChildren` 속성을 활용하여 새 페이지를 만드는 위치를 기반으로 작성자가 사용할 수 있는 템플릿을 세부적으로 제어할 수 있습니다.

새 앱 페이지 구성 요소를 처음부터 만들 때는 `sling:resourceSuperType` 속성을 &#39;mobileapps/components/angular/ng-page&#39;로 설정하는 것이 좋습니다. 이렇게 하면 작성 및 렌더링이 모두 단일 페이지 앱으로 설정되며 구성 요소가 변경해야 할 수 있는 모든 .jsp 파일을 오버레이할 수 있습니다. ng-page에는 UI 프레임워크가 전혀 포함되어 있지 않으므로 개발자는 일반적으로 &#39;template.jsp&#39;(/libs/mobileapps/components/angular/ng-page/template.jsp에서 오버레이됩니다.)

AngularJS를 활용하고자 하는 작성 가능한 페이지 구성 요소에는 /libs/mobileapps/components/angular/ng-component에 상응하는 `sling:resourceSuperType` 구성 요소가 있으며 이러한 구성 요소는 동일한 방식으로 오버레이되어 사용자 정의할 수 있습니다.

## JavaScript 및 CSS Clientlibs {#javascript-and-css-clientlibs}

클라이언트 라이브러리와 관련하여 개발자는 보관소에 배치할 수 있는 몇 가지 옵션을 사용할 수 있습니다. 다음 패턴은 안내를 위해 제공되지만 어려운 조건은 아닙니다.

클라이언트 측 코드가 자체적으로 설 수 있고 응용 프로그램의 특정 구성 요소와 관련이 없는 경우(즉, 다른 응용 프로그램에서 다시 사용할 수 있음) /etc/clientlibs/&lt;brand name>/&lt;lib name>에 저장하는 것이 좋습니다. 반면 clientlib이 단일 앱에만 해당되는 경우 앱 디자인 노드의 자식으로 중첩할 수 있습니다./etc/designs/phonegap/&lt;brand name>/&lt;app name>/clientlibs. 이 clientlib의 범주는 다른 libs에서 사용할 수 없으며 필요한 경우 다른 libs를 포함하는 데 사용해야 합니다. 이 패턴에 따라 개발자는 클라이언트 라이브러리가 앱에 추가될 때마다 새로운 컨텐츠 동기화 구성을 추가해야 하는 것을 방지할 수 있습니다. 대신 앱의 design clientlib의 &#39;embed&#39; 속성을 간단히 업데이트합니다. 예를 들어 /content/phonegap/geometrixx-outdoors/en/jcr:content/page-app/app-config/clientlibs-all의 Geometrixx clientlibs-all Content Sync 구성 노드를 살펴보십시오.

클라이언트 측 코드가 특정 구성 요소와 긴밀하게 연결된 경우, 해당 코드를 /apps/의 구성 요소 위치 아래에 중첩된 클라이언트 라이브러리에 배치하고, 앱의 &#39;design&#39; clientlib에 이 코드를 포함시킵니다.

## PhoneGap 구성 {#phonegap-configuration}

각 AEM Mobile 앱에는 웹 콘텐츠를 실행 가능한 애플리케이션으로 전환하기 위해 PhoneGap [명령줄 인터페이스](https://github.com/phonegap/phonegap-cli) 및 [PhoneGap 빌드](https://build.phonegap.com/)에서 사용하는 구성 파일을 호스팅하는 디렉토리가 포함되어 있습니다. 예를 들어 Geometrixx 샘플에서 이 디렉터리(/content/phonegap/geometrixx-outdoors/shell/jcr:content/page-app/app-content)는 셸의 일부로 위치합니다.장치 API와 관련된 플러그인 및 앱 자체의 구성과 같이 무선 기능에서 업데이트할 수 없는 컨텐츠만 포함되어 있기 때문에 디자인 결정을 내렸습니다.

또한 이 디렉토리에서 플러그인 설치, 플랫폼 특정 위치에 리소스 파일 배치 및 빌드의 일부로 실행해야 하는 기타 작업에 사용할 수 있는 [Cordova 후크](https://cordova.apache.org/docs/en/edge/guide_appdev_hooks_index.md.html#Hooks%20Guide)의 수도 찾을 수 있습니다. 참고:빌드의 일부로 각 플러그인을 다운로드하는 대신 Kitchen Sink 앱의 패턴을 따르고 [include plugin source code](https://github.com/blefebvre/aem-phonegap-kitchen-sink/tree/master/content/src/main/content/jcr_root/content/phonegap/kitchen-sink/shell/_jcr_content/pge-app/app-content/phonegap/plugins)와 나머지 앱 프로젝트를 함께 수행할 수 있습니다.

## 다음 단계 {#the-next-steps}

앱의 구조에 대해 알게 되면 [앱 콘솔을 사용하여 앱 제작 및 편집을 참조하십시오](/help/mobile/phonegap-apps-console.md).
