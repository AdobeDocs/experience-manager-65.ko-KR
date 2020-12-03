---
title: 에뮬레이터
seo-title: 에뮬레이터
description: AEM에서는 작성자가 페이지를 볼 환경을 시뮬레이션하는 에뮬레이터로 페이지를 볼 수 있습니다
seo-description: AEM에서는 작성자가 페이지를 볼 환경을 시뮬레이션하는 에뮬레이터로 페이지를 볼 수 있습니다
uuid: ee1496a5-be68-4318-b5ce-b11c41e4485c
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: mobile-web
content-type: reference
discoiquuid: c51fca81-5dfc-4838-9672-acb6de62778b
legacypath: /content/docs/en/aem/6-0/develop/mobile/emulators
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '654'
ht-degree: 0%

---


# 에뮬레이터{#emulators}

>[!NOTE]
>
>단일 페이지 애플리케이션 프레임워크 기반 클라이언트측 렌더링(예: 응답)이 필요한 프로젝트에서는 SPA 편집기를 사용하는 것이 좋습니다. [추가 정보](/help/sites-developing/spa-overview.md).

Adobe Experience Manager(AEM) 작성자는 모바일 장치 또는 이메일 클라이언트와 같이 최종 사용자가 페이지를 보는 환경을 시뮬레이션하는 에뮬레이터에서 페이지를 볼 수 있습니다.

AEM 에뮬레이터 프레임워크:

* 모바일 장치 또는 이메일 클라이언트(뉴스레터를 작성하는 데 사용)와 같은 시뮬레이트된 사용자 인터페이스(UI) 내에서 컨텐츠 작성을 제공합니다.
* 시뮬레이션된 UI에 따라 페이지 컨텐츠를 조정합니다.
* 사용자 정의 에뮬레이터를 만들 수 있습니다.

>[!CAUTION]
>
>이 기능은 클래식 UI에서만 지원됩니다.

## 에뮬레이터 특성 {#emulators-characteristics}

에뮬레이터:

* ExtJS를 기반으로 합니다.
* 페이지 DOM에서 작동합니다.
* 모양은 CSS를 통해 규제됩니다.
* 플러그인(예: 모바일 장치 회전 플러그인)을 지원합니다.
* 작성자에만 활성화됩니다.
* 기본 구성 요소는 `/libs/wcm/emulator/components/base`에 있습니다.

### 에뮬레이터가 내용 {#how-the-emulator-transforms-the-content}을 변환하는 방법

에뮬레이터는 HTML 본문 내용을 에뮬레이터 DIV로 래핑하여 작동합니다. 예를 들어 다음 html 코드를 참조하십시오.

```xml
<body>
<div id="wrapper" class="page mobilecontentpage ">
    <div class="topnav mobiletopnav">
    ...
    </div>
    ...
</div>
</body>
```

는 에뮬레이터를 시작한 후 다음 html 코드로 변형됩니다.

```xml
<body>
 <div id="cq-emulator-toolbar">
 ...
 </div>
 <div id="cq-emulator-wrapper">
  <div id="cq-emulator-device">
   <div class=" android vertical" id="cq-emulator">
    ...
    <div class=" android vertical" id="cq-emulator-content">
     ...
     <div id="wrapper" class="page mobilecontentpage">
     ...
     </div>
     ...
    </div>
   </div>
  </div>
 </div>
 ...
</body>
```

두 개의 div 태그가 추가되었습니다.

* 에뮬레이터를 전체와`cq-emulator`

* 페이지 컨텐츠가 있는 장치의 뷰포트/화면/컨텐츠 영역을 나타내는 id가 `cq-emulator-content`인 div.

새 CSS 클래스는 새로운 에뮬레이터 div에도 할당됩니다.현재 에뮬레이터의 이름을 나타냅니다.

에뮬레이터의 플러그인은 현재 장치 회전에 따라 &quot;vertical&quot; 또는 &quot;horizontal&quot; 클래스를 삽입하는 순환 플러그인의 예와 같이 할당된 CSS 클래스 목록을 추가로 확장할 수 있습니다.

이렇게 하면 에뮬레이터의 전체 모양을 에뮬레이터의 ID 및 CSS 클래스에 해당하는 CSS 클래스가 있어 제어할 수 있습니다.

>[!NOTE]
>
>위 예제와 같이 프로젝트 HTML이 본문 컨텐츠를 단일 div로 래핑하는 것이 좋습니다. 본문 컨텐츠에 여러 태그가 포함되어 있는 경우 예측할 수 없는 결과가 발생할 수 있습니다.

### 모바일 에뮬레이터 {#mobile-emulators}

기존 모바일 에뮬레이터:

* /libs/wcm/mobile/components/에뮬레이터 아래에 있습니다.
* JSON 서블릿을 통해 사용 가능:

   http://localhost:4502/bin/wcm/mobile/emulators.json

페이지 구성 요소가 모바일 페이지 구성 요소( `/libs/wcm/mobile/components/page`)에 의존하는 경우 에뮬레이터 기능은 다음 메커니즘을 통해 페이지에 자동으로 통합됩니다.

* 모바일 페이지 구성 요소 `head.jsp`에는 장치 그룹의 관련 에뮬레이터 init 구성 요소(작성자 모드에서만)와 장치 그룹의 렌더링 CSS가 다음을 통해 포함됩니다.

   `deviceGroup.drawHead(pageContext);`

* `DeviceGroup.drawHead(pageContext)` 메서드에는 에뮬레이터의 init 구성 요소가 포함되어 있습니다. 즉, 에뮬레이터 구성 요소의 `init.html.jsp`을 호출합니다. 에뮬레이터 구성 요소에 자체 `init.html.jsp`이 없고 모바일 기반 에뮬레이터를 사용하는 경우( `wcm/mobile/components/emulators/base)`) 모바일 기본 에뮬레이터의 init 스크립트가 호출됩니다( `/libs/wcm/mobile/components/emulators/base/init.html.jsp`).

* 모바일 기본 에뮬레이터의 init 스크립트는 Javascript를 통해 정의합니다.

   * 페이지에 대해 정의된 모든 에뮬레이터의 구성(에뮬레이터구성)
   * 에뮬레이터의 기능을 다음 기능을 통해 페이지에 통합하는 에뮬레이터 관리자

      `emulatorMgr.launch(config)`;

      에뮬레이터 관리자는

      `/libs/wcm/emulator/widgets/source/EmulatorManager.js`

#### 사용자 지정 모바일 에뮬레이터 만들기 {#creating-a-custom-mobile-emulator}

사용자 정의 모바일 에뮬레이터를 만들려면:

1. `/apps/myapp/components/emulators` 아래에서 구성 요소 `myemulator`(노드 유형:`cq:Component`).

1. `sling:resourceSuperType` 속성을 `/libs/wcm/mobile/components/emulators/base`로 설정합니다.

1. 에뮬레이터 모양에 대해 범주 `cq.wcm.mobile.emulator`으로 CSS 클라이언트 라이브러리를 정의합니다.name = `css`, 노드 유형 = `cq:ClientLibrary`

   예를 들어 노드 `/libs/wcm/mobile/components/emulators/iPhone/css`을 참조할 수 있습니다.

1. 필요한 경우 JS 클라이언트 라이브러리를 정의합니다. 예를 들어 특정 플러그인을 정의합니다.name = js, node type = cq:ClientLibrary

   예를 들어 노드 `/libs/wcm/mobile/components/emulators/base/js`을 참조할 수 있습니다.

1. 에뮬레이터가 플러그인으로 정의된 특정 기능(터치 스크롤링 등)을 지원하는 경우 에뮬레이터 아래에 구성 노드를 만듭니다.name = `cq:emulatorConfig`, node type = `nt:unstructured`, 플러그인을 정의하는 속성을 추가합니다.

   * 이름 = `canRotate`, 유형 = `Boolean`, 값 = `true`:를 클릭하여 회전 기능을 포함할 수 있습니다.

   * 이름 = `touchScrolling`, 유형 = `Boolean`, 값 = `true`:를 클릭하여 터치 스크롤 기능을 포함할 수 있습니다.

   고유한 플러그인을 정의하여 더 많은 기능을 추가할 수 있습니다.

