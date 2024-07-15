---
title: 앱 구조
description: 이 페이지를 따라 앱 구조를 만드는 방법에 대해 알아보십시오. 이 페이지에서는 JavaScript 및 CSS Clientlib에 대한 정보와 함께 템플릿 및 구성 요소를 구성하는 방법을 설명합니다.
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
exl-id: f37f239f-065b-44f8-acb1-93485b713b49
solution: Experience Manager
feature: Mobile
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '871'
ht-degree: 0%

---

# 앱 구조{#structure-an-app}

>[!NOTE]
>
>Adobe 단일 페이지 애플리케이션 프레임워크 기반 클라이언트측 렌더링(예: React)이 필요한 프로젝트에는 SPA Editor를 사용하는 것이 좋습니다. [자세히 알아보기](/help/sites-developing/spa-overview.md).

AEM Mobile 프로젝트에는 페이지, JavaScript 및 CSS 클라이언트 라이브러리, 재사용 가능한 AEM 구성 요소, 콘텐츠 동기화 구성 및 PhoneGap 앱 쉘 콘텐츠를 비롯한 다양한 콘텐츠 유형 세트가 포함됩니다. [시작 키트](https://github.com/Adobe-Marketing-Cloud-Apps/aem-phonegap-starter-kit)를 기반으로 새 AEM Mobile 앱을 빌드하는 것은 장기적으로 휴대성과 유지 관리를 용이하게 하기 위해 다양한 유형의 콘텐츠를 모두 권장 구조로 가져오는 좋은 방법입니다.

## 페이지 컨텐츠 {#page-content}

애플리케이션의 페이지는 모두 /content/mobileapps 아래에 있어야 AEM Mobile 콘솔에서 인식됩니다.

![chlimage_1-52](assets/chlimage_1-52.png)

AEM 규칙에 따라 앱의 첫 페이지는 앱의 기본 언어(&#39;en&#39;, Geometrixx 및 스타터 키트 사례 모두)로 사용되는 하위 페이지 중 하나로 리디렉션되어야 합니다. 최상위 로케일 페이지는 일반적으로 기본 콘텐츠 동기화 업데이트(contentInit 코드는 /etc/clientlibs/mobile/content-sync/js/contentInit.js에서 찾을 수 있음) 설치를 지원하는 데 필요한 초기화를 처리하는 기초 &#39;splash-page&#39; 구성 요소(/libs/mobileapps/components/splash-page)에서 상속됩니다.

## 템플릿 및 구성 요소 {#templates-and-components}

앱의 템플릿 및 구성 요소 코드는 /apps/&lt;브랜드 이름>/&lt;앱 이름>에 있어야 합니다. 규칙에 따라 /apps/&lt;브랜드 이름>/&lt;앱 이름>에 템플릿과 구성 요소 코드를 배치해야 합니다. 이 패턴은 AEM에서 이미 사이트를 사용하여 작업한 개발자에게 익숙해야 합니다. 일반적으로 /apps/ 가 게시 인스턴스에서 기본적으로 익명 액세스로 잠기므로 뒤에 옵니다. 따라서 원시 JSP 코드는 잠재적 공격자로부터 멀리 숨겨집니다.

템플릿 자체의 `allowedPaths` 속성 노드를 사용하고 값을 &#39;/content/mobileapps(/)로 설정하여 앱별 템플릿을 표시만 하도록 구성할 수 있습니다.&amp;ast;)?&#39; - 또는 템플릿을 단일 앱에만 사용할 수 있어야 하는 경우 보다 구체적인 요구 사항 `allowedParents` 및 `allowedChildren` 속성은 새 페이지가 만들어지는 위치에 따라 작성자가 사용할 수 있는 템플릿을 세밀하게 제어하는 데에도 사용할 수 있습니다.

angular 앱 페이지 구성 요소를 처음부터 만들 때는 해당 `sling:resourceSuperType` 속성을 &#39;mobileapps/components/page/ng-page&#39;로 설정하는 것이 좋습니다. 이렇게 하면 작성 및 렌더링을 위한 페이지가 단일 페이지 앱으로 설정되고 구성 요소가 변경해야 할 수 있는 모든 .jsp 파일을 오버레이할 수 있습니다. ng-page에는 UI 프레임워크가 전혀 포함되어 있지 않으므로 일반적으로 개발자는 &quot;template.jsp&quot;(/libs/mobileapps/components/angular/ng-page/template.jsp에서 오버레이됨)를 오버레이합니다.

AngularJS를 사용하려는 작성 가능한 페이지 구성 요소에는 동일한 방식으로 오버레이하고 사용자 정의할 수 있는 /libs/mobileapps/components/angular/ng-component에 동등한 `sling:resourceSuperType` 구성 요소가 있습니다.

## JavaScript 및 CSS Clientlibs {#javascript-and-css-clientlibs}

클라이언트 라이브러리에서는 개발자가 저장소에 배치할 위치에 사용할 수 있는 몇 가지 옵션이 있습니다. 다음 패턴은 지침을 위해 제공되지만 어려운 요구 사항은 아닙니다.

clientside 코드가 독립적일 수 있고 응용 프로그램의 특정 구성 요소와 관련이 없는 경우(다른 응용 프로그램에서 재사용될 수 있음), Adobe은 /etc/clientlibs/&lt;brand name>/&lt;lib name>에 저장하는 것을 권장합니다. 반면 clientlib이 단일 앱에 고유한 경우 앱 디자인 노드의 하위 노드인 /etc/designs/phonegap/&lt;brand name>/&lt;app name>/clientlibs로 중첩할 수 있습니다. 이 clientlib의 범주를 다른 lib과 함께 사용하지 마십시오. 대신 필요에 따라 다른 lib을 임베드하십시오. 이 패턴을 사용하면 개발자가 클라이언트 라이브러리를 앱에 추가할 때마다 새로운 Content Sync 구성을 추가하지 않아도 됩니다. 대신 앱 디자인 clientlib의 &#39;embed&#39; 속성을 업데이트하면 됩니다. 예를 들어 /content/phonegap/geometrixx-outdoors/en/jcr:content/pge-app/app-config/clientlibs-all에서 Geometrixx clientlibs-all Content Sync 구성 노드를 살펴보십시오.

클라이언트측 코드가 특정 구성 요소에 밀접하게 연결되어 있는 경우 /apps/에서 구성 요소의 위치 아래에 중첩된 클라이언트 라이브러리에 해당 코드를 배치하고 해당 범주를 앱의 &#39;design&#39; clientlib에 포함하십시오.

## PhoneGap 구성 {#phonegap-configuration}

각 AEM Mobile 앱에는 PhoneGap [명령줄 인터페이스](https://github.com/phonegap/phonegap-cli) 및 `https://build.phonegap.com/`의 PhoneGap Build에서 사용하는 구성 파일을 호스팅하여 웹 콘텐츠를 실행 가능한 응용 프로그램으로 변환하는 디렉터리가 포함되어 있습니다. 예를 들어 Geometrixx 샘플에서 이 디렉터리(/content/phonegap/geometrixx-outdoors/shell/jcr:content/pge-app/app-content)는 셸의 일부로 위치합니다. 여기에는 장치 API 및 앱 자체의 구성을 처리하는 플러그인과 같이 공중으로 업데이트할 수 없는 콘텐츠만 포함되어 있으므로 디자인 결정이 내려졌습니다.

이 디렉터리에는 플러그인을 설치하고 플랫폼별 위치에 리소스 파일을 배치하고 빌드의 일부로 실행해야 하는 기타 작업에 사용할 수 있는 [Cordova 후크](https://cordova.apache.org/docs/en/dev/guide/appdev/hooks/index.html#Hooks%20Guide)도 있습니다. 참고: 빌드의 일부로 각 플러그인을 다운로드하는 대신 Kitchen Sink 앱의 패턴을 따라 나머지 앱 프로젝트와 함께 플러그인 소스 코드<!-- THIS URL IS 404 (https://github.com/blefebvre/aem-phonegap-kitchen-sink/tree/master/content/src/main/content/jcr_root/content/phonegap/kitchen-sink/shell/_jcr_content/pge-app/app-content/phonegap/plugins) -->을(를) 포함할 수 있습니다.

## 다음 단계 {#the-next-steps}

앱의 구조에 대해 알아본 후 [앱 콘솔을 사용하여 앱 만들기 및 편집](/help/mobile/phonegap-apps-console.md)을 참조하세요.
