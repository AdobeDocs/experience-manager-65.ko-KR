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
exl-id: f37f239f-065b-44f8-acb1-93485b713b49
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '973'
ht-degree: 0%

---

# 앱 구조{#structure-an-app}

>[!NOTE]
>
>단일 페이지 애플리케이션 프레임워크 기반 클라이언트측 렌더링(예: React)이 필요한 프로젝트에 SPA 편집기를 사용하는 것이 좋습니다. [추가 정보](/help/sites-developing/spa-overview.md).

AEM Mobile 프로젝트에는 페이지, JavaScript 및 CSS 클라이언트 라이브러리, 재사용 가능한 AEM 구성 요소, 컨텐츠 동기화 구성 및 PhoneGap 앱 셸 컨텐츠를 포함한 다양한 컨텐츠 유형 세트가 포함되어 있습니다. 새 AEM Mobile 앱을 [Starter Kit](https://github.com/Adobe-Marketing-Cloud-Apps/aem-phonegap-starter-kit)을 기반으로 지정하는 것은 장기적으로 휴대성과 유지 관리 기능을 모두 간소화하기 위해 다양한 유형의 컨텐츠를 Adobe의 권장 구조에 가져오는 좋은 방법입니다.

## 페이지 컨텐츠 {#page-content}

AEM Mobile 콘솔에서 응용 프로그램을 인식하려면 응용 프로그램의 모든 페이지가 /content/mobileapps 아래에 있어야 합니다.

![chlimage_1-52](assets/chlimage_1-52.png)

AEM 규칙을 통해 앱의 첫 번째 페이지는 앱의 기본 언어(Geometrixx 및 시작 키트 케이스 둘 다에서 &#39;en&#39;)로 사용되는 1차 하위 구성요소로 리디렉션되어야 합니다. 최상위 로케일 페이지는 일반적으로 기본 &#39;splash-page&#39; 구성 요소(/libs/mobileapps/components/splash-page)에서 상속되며, 이 구성 요소는 과도한 Content Sync 업데이트(contentInit 코드는 /etc/clientlibs/mobile/content-sync/js/contentInit.js)의 설치를 지원하는 데 필요한 초기화를 처리합니다.

## 템플릿 및 구성 요소 {#templates-and-components}

앱에 대한 템플릿 및 구성 요소 코드는 /apps/&lt;브랜드 이름>/&lt;앱 이름>에 있어야 합니다. 규칙에 따라 /apps/&lt;브랜드 이름>/&lt;앱 이름>에 템플릿 및 구성 요소 코드를 배치해야 합니다. 이 패턴은 AEM에서 사이트에서 이미 작업한 개발자에게 익숙해야 합니다. 게시 인스턴스에서 기본적으로 /apps/ 가 익명 액세스를 위해 잠기면 일반적으로 그 뒤에 옵니다. 따라서 원시 JSP 코드가 잠재적인 공격자들로부터 숨겨집니다.

앱 관련 템플릿은 템플릿 자체의 `allowedPaths` 속성 노드를 사용하고 해당 값을 &#39;/content/mobileapps(/)로 설정하여 표시할 수만 사용하도록 구성할 수 있습니다.&amp;ast;)?&#39; - 또는 템플릿을 단일 앱에만 사용할 수 있어야 하는 경우 더 구체적인 항목을 사용할 수 있습니다. `allowedParents` 및 `allowedChildren` 속성을 활용하여 새 페이지를 만드는 위치를 기반으로 작성자가 사용할 수 있는 템플릿을 매우 세밀하게 제어할 수도 있습니다.

처음부터 새 앱 페이지 구성 요소를 만들 때는 `sling:resourceSuperType` 속성을 &#39;mobileapps/components/angular/ng-page&#39;로 설정하는 것이 좋습니다. 페이지를 단일 페이지 앱으로 작성 및 렌더링할 수 있도록 설정하고, 구성 요소를 변경해야 할 수 있는 모든 .jsp 파일을 오버레이할 수 있습니다. ng-page에는 UI 프레임워크가 전혀 포함되지 않으므로 개발자는 일반적으로 &#39;template.jsp&#39;(/libs/mobileapps/components/angular/ng-page/template.jsp에서 오버레이됨)를 오버레이합니다.

AngularJS를 활용하려는 작성 가능한 페이지 구성 요소는 /libs/mobileapps/components/angular/ng-component에 동일한 방식으로 오버레이하고 사용자 지정할 수 있는 동일한 `sling:resourceSuperType` 구성 요소가 있습니다.

## JavaScript 및 CSS Clientlibs {#javascript-and-css-clientlibs}

클라이언트 라이브러리와 관련하여 개발자가 저장소에 배치할 수 있는 몇 가지 옵션이 있습니다. 다음 패턴은 지침을 위해 제공되지만, 어려운 요구 사항은 아닙니다.

clientside 코드가 자체적으로 실행될 수 있고 애플리케이션의 특정 구성 요소와 관련이 없는 경우(즉, 다른 애플리케이션에서 재사용할 수 있는 경우) /etc/clientlibs/&lt;brand name>/&lt;lib name>에 저장하는 것이 좋습니다. 반면 clientlib이 단일 앱에만 해당하는 경우 앱 디자인 노드의 하위로 중첩할 수 있습니다./etc/designs/phonegap/&lt;brand name>/&lt;app name>/clientlibs. 이 clientlib의 카테고리는 다른 libs에서 사용할 수 없으며 필요에 따라 다른 libs를 포함하는 데 사용해야 합니다. 이 패턴을 수행하면 개발자가 클라이언트 라이브러리가 앱에 추가될 때마다 새 컨텐츠 동기화 구성을 추가할 필요가 없고 앱 디자인 clientlib의 &#39;embed&#39; 속성을 업데이트하기만 하면 됩니다. 예를 들어, /content/phonegap/geometrixx-outdoors/en/jcr:content/page-app/app-config/clientlibs-all에서 clientlibs-all Content Sync 구성 노드를 살펴봅니다.

클라이언트 측 코드가 특정 구성 요소와 밀접하게 연결된 경우 해당 코드를 /apps/의 구성 요소 위치 아래에 중첩된 클라이언트 라이브러리에 배치하고 이 코드를 앱의 &#39;design&#39; clientlib에 포함하십시오.

## PhoneGap 구성 {#phonegap-configuration}

각 AEM Mobile 앱에는 PhoneGap [명령줄 인터페이스](https://github.com/phonegap/phonegap-cli) 및 [PhoneGap 빌드](https://build.phonegap.com/)에서 사용하는 구성 파일을 호스트하는 디렉토리가 있습니다. 예를 들어 Geometrixx 샘플에서 이 디렉토리(/content/phonegap/geometrixx-outdoors/shell/jcr:content/page-app/app-content)는 Shell의 일부로 위치합니다.장치 API를 처리하는 플러그인 및 앱 자체의 구성과 같이, 공중에 떠서 업데이트할 수 없는 콘텐츠만 포함된다는 사실로 인해 디자인이 결정했습니다.

또한 이 디렉토리에는 플러그인을 설치하고, 플랫폼별 위치에 리소스 파일을 배치하고, 빌드의 일부로 실행해야 하는 기타 작업에 사용할 수 있는 [Cordova 후크](https://cordova.apache.org/docs/en/edge/guide_appdev_hooks_index.md.html#Hooks%20Guide)가 여러 개 있습니다. 참고:빌드의 일부로 각 플러그인을 다운로드하는 대신, Kitchen Sink 앱의 패턴을 따르고 [플러그인 소스 코드](https://github.com/blefebvre/aem-phonegap-kitchen-sink/tree/master/content/src/main/content/jcr_root/content/phonegap/kitchen-sink/shell/_jcr_content/pge-app/app-content/phonegap/plugins)를 나머지 앱 프로젝트에서 포함할 수 있습니다.

## 다음 단계 {#the-next-steps}

앱의 구조에 대해 알려면 [앱 콘솔을 사용하여 앱 만들기 및 편집](/help/mobile/phonegap-apps-console.md)을 참조하십시오.
