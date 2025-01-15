---
title: 에뮬레이터
description: AEM을 사용하면 작성자가 최종 사용자가 페이지를 볼 환경을 시뮬레이션하는 에뮬레이터에서 페이지를 볼 수 있습니다
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: mobile-web
content-type: reference
legacypath: /content/docs/en/aem/6-0/develop/mobile/emulators
exl-id: 009b7e2c-ac37-4acc-a656-0a34d3853dfd
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 2dae56dc9ec66f1bf36bbb24d6b0315a5f5040bb
workflow-type: tm+mt
source-wordcount: '609'
ht-degree: 0%

---

# 에뮬레이터{#emulators}

{{ue-over-mobile}}

Adobe Experience Manager(AEM)를 사용하면 작성자가 최종 사용자가 페이지를 볼 환경을 시뮬레이션하는 에뮬레이터에서 페이지를 볼 수 있습니다. 예를 들어 모바일 디바이스나 이메일 클라이언트에서 페이지를 볼 수 있습니다.

AEM 에뮬레이터 프레임워크:

* 모바일 장치나 이메일 클라이언트(뉴스레터 작성에 사용)와 같은 시뮬레이션된 UI(사용자 인터페이스) 내에서 콘텐츠 작성을 제공합니다.
* 시뮬레이션된 UI에 따라 페이지 콘텐츠를 조정합니다.
* 사용자 지정 에뮬레이터를 만들 수 있습니다.

>[!CAUTION]
>
>이 기능은 클래식 UI에서만 지원됩니다.

## 에뮬레이터 특성 {#emulators-characteristics}

에뮬레이터:

* ExtJS를 기반으로 합니다.
* 페이지 DOM에서 작동합니다.
* 해당 모양은 CSS를 통해 조절됩니다.
* 플러그인을 지원합니다(예: 모바일 디바이스 회전 플러그인).
* 은(는) 작성자에서만 활성화됩니다.
* 기본 구성 요소는 `/libs/wcm/emulator/components/base`에 있습니다.

### 에뮬레이터가 콘텐츠를 변환하는 방법 {#how-the-emulator-transforms-the-content}

에뮬레이터는 HTML 본문 컨텐츠를 에뮬레이터 DIV에 래핑하여 작동합니다. 예를 들어 다음 html 코드는

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

는 에뮬레이터를 시작한 후 다음 html 코드로 변환됩니다.

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

* 에뮬레이터를 전체적으로 포함하는 ID가 `cq-emulator`인 div 및

* 페이지 콘텐츠가 있는 장치의 뷰포트/화면/콘텐츠 영역을 나타내는 id `cq-emulator-content`의 div입니다.

새 CSS 클래스도 새 에뮬레이터 div에 할당됩니다. 이 div는 현재 에뮬레이터의 이름을 나타냅니다.

에뮬레이터의 플러그인은 회전 플러그인의 예에서와 같이 할당된 CSS 클래스 목록을 추가로 확장하여 현재 디바이스 회전에 따라 &quot;수직&quot; 또는 &quot;수평&quot; 클래스를 삽입할 수 있습니다.

이러한 방식으로, 에뮬레이터 div의 ID 및 CSS 클래스에 해당하는 CSS 클래스를 가짐으로써 에뮬레이터의 전체 모양을 제어할 수 있습니다.

>[!NOTE]
>
>프로젝트 HTML은 위의 예제와 같이 본문 콘텐츠를 단일 div로 래핑하는 것이 좋습니다. 본문 컨텐츠에 여러 태그가 포함된 경우 예기치 않은 결과가 발생할 수 있습니다.

### 모바일 에뮬레이터 {#mobile-emulators}

기존 모바일 에뮬레이터는

* /libs/wcm/mobile/components/emulators 아래에 있습니다.
* 다음 위치의 JSON 서블릿을 통해 사용할 수 있습니다.

  http://localhost:4502/bin/wcm/mobile/emulators.json

페이지 구성 요소가 모바일 페이지 구성 요소(`/libs/wcm/mobile/components/page`)를 사용하는 경우 에뮬레이터 기능은 다음 메커니즘을 통해 페이지에 자동으로 통합됩니다.

* 모바일 페이지 구성 요소 `head.jsp`에는 장치 그룹의 연결된 에뮬레이터 초기화 구성 요소(작성자 모드에서만)와 장치 그룹의 렌더링 CSS가 포함되어 있습니다.

  `deviceGroup.drawHead(pageContext);`

* `DeviceGroup.drawHead(pageContext)` 메서드가 에뮬레이터의 init 구성 요소를 포함합니다. 즉, 에뮬레이터 구성 요소의 `init.html.jsp`을(를) 호출합니다. 에뮬레이터 구성 요소에 자체 `init.html.jsp`이(가) 없고 모바일 기본 에뮬레이터( `wcm/mobile/components/emulators/base)`)에 의존하는 경우 모바일 기본 에뮬레이터의 init 스크립트가 호출됩니다( `/libs/wcm/mobile/components/emulators/base/init.html.jsp`).

* 모바일 기본 에뮬레이터의 init 스크립트는 JavaScript을 통해 다음을 정의합니다.

   * 페이지에 대해 정의된 모든 에뮬레이터에 대한 구성(emulatorConfigs)
   * 다음을 통해 페이지에서 에뮬레이터의 기능을 통합하는 에뮬레이터 관리자:

     `emulatorMgr.launch(config)`;

     에뮬레이터 관리자는 다음으로 정의됩니다.

     `/libs/wcm/emulator/widgets/source/EmulatorManager.js`

#### 사용자 지정 모바일 에뮬레이터 만들기 {#creating-a-custom-mobile-emulator}

사용자 지정 모바일 에뮬레이터를 만들려면:

1. `/apps/myapp/components/emulators` 아래에서 `myemulator` 구성 요소를 만듭니다(노드 형식: `cq:Component`).

1. `sling:resourceSuperType` 속성을 `/libs/wcm/mobile/components/emulators/base`(으)로 설정

1. 에뮬레이터 모양: 이름 = `css`, 노드 유형 = `cq:ClientLibrary`에 대해 `cq.wcm.mobile.emulator` 범주가 있는 CSS 클라이언트 라이브러리를 정의하십시오.

   예를 들어 `/libs/wcm/mobile/components/emulators/iPhone/css` 노드를 참조할 수 있습니다.

1. 필요한 경우 JS 클라이언트 라이브러리를 정의하여 특정 플러그인을 정의합니다(예: name = js, node type = cq:ClientLibrary).

   예를 들어 `/libs/wcm/mobile/components/emulators/base/js` 노드를 참조할 수 있습니다.

1. 에뮬레이터가 플러그인으로 정의된 특정 기능(예: 터치 스크롤)을 지원하는 경우 에뮬레이터 아래에 구성 노드를 만드십시오. 이름 = `cq:emulatorConfig`, 노드 유형 = `nt:unstructured`.

   * 이름 = `canRotate`, 유형 = `Boolean`, 값 = `true`: 순환 기능을 포함합니다.

   * 이름 = `touchScrolling`, 유형 = `Boolean`, 값 = `true`: 터치 스크롤 기능을 포함합니다.

   고유한 플러그인을 정의하여 더 많은 기능을 추가할 수 있습니다.
