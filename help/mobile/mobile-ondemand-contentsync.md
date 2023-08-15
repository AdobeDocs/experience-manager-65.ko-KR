---
title: 콘텐츠 동기화가 있는 모바일
description: 콘텐츠 동기화에 대해 알아보려면 이 페이지를 따르십시오. Adobe Experience Manager(AEM)에서 작성된 페이지는 장치가 오프라인 상태인 경우에도 앱 콘텐츠로 사용할 수 있습니다. 또한 AEM 페이지는 웹 표준을 기반으로 하므로 플랫폼 간에 작동하므로 기본 래퍼에 포함할 수 있습니다. 이 전략을 사용하면 개발 노력을 줄이고 앱 콘텐츠를 쉽게 업데이트할 수 있습니다.
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-on-demand-services-app
exl-id: a6e59334-09e2-4bb8-b445-1868035da556
source-git-commit: 50d29c967a675db92e077916fb4adef6d2d98a1a
workflow-type: tm+mt
source-wordcount: '2974'
ht-degree: 0%

---

# 콘텐츠 동기화가 있는 모바일{#mobile-with-content-sync}

>[!NOTE]
>
>Adobe 단일 페이지 애플리케이션 프레임워크 기반 클라이언트측 렌더링(예: React)이 필요한 프로젝트에는 SPA Editor를 사용하는 것이 좋습니다. [자세히 알아보기](/help/sites-developing/spa-overview.md).

기본 모바일 애플리케이션에서 사용할 수 있도록 컨텐츠 동기화를 사용하여 컨텐츠를 패키징합니다. Adobe Experience Manager(AEM)에서 작성된 페이지는 장치가 오프라인 상태인 경우에도 앱 콘텐츠로 사용할 수 있습니다. 또한 AEM 페이지는 웹 표준을 기반으로 하므로 플랫폼 간에 작동하므로 기본 래퍼에 포함할 수 있습니다. 이 전략을 사용하면 개발 노력을 줄이고 앱 콘텐츠를 쉽게 업데이트할 수 있습니다.

컨텐츠 동기화 프레임워크는 웹 컨텐츠를 포함하는 아카이브 파일을 만듭니다. 컨텐츠는 간단한 페이지, 이미지 및 PDF 파일 또는 전체 웹 애플리케이션에서 사용할 수 있습니다. 콘텐츠 동기화 API는 콘텐츠를 검색하고 앱에 포함할 수 있도록 모바일 앱 또는 빌드 프로세스에서 보관 파일에 대한 액세스를 제공합니다.

다음 단계는 Content Sync의 일반적인 사용 사례를 보여 줍니다.

1. AEM 개발자는 포함할 콘텐츠를 지정하는 콘텐츠 동기화 구성을 만듭니다.
1. 콘텐츠 동기화 프레임워크는 콘텐츠를 수집하고 캐시합니다.
1. 모바일 디바이스에서 모바일 애플리케이션이 시작되고 ZIP 파일로 제공되는 서버의 콘텐츠를 요청합니다.
1. 클라이언트가 ZIP 콘텐츠를 로컬 파일 시스템에 압축을 풉니다. ZIP 파일의 폴더 구조는 클라이언트(예: 브라우저)가 일반적으로 서버에서 요청하는 경로를 시뮬레이션합니다.
1. 클라이언트가 포함된 브라우저에서 콘텐츠를 열거나 다른 방식으로 사용합니다.
1. 나중에 클라이언트가 서버에서 업데이트된 콘텐츠를 요청합니다. Content Sync 프레임워크는 다운로드 크기와 시간을 줄이기 위해 증분 업데이트를 제공합니다. 이 업데이트는 제한된 대역폭 또는 데이터 볼륨으로 인해 모바일 장치에 중요할 수 있습니다.

## 콘텐츠 동기화 핸들러 개발 {#developing-the-content-sync-handlers}

Content Sync Handler 개발에 대한 몇 가지 지침은 다음과 같습니다.

* 처리기는 다음을 구현해야 합니다. *com.day.cq.contentsync.handler.ContentUpdateHandler* (작업을 수행하는 클래스를 직접 확장하거나 확장)
* 처리기는 확장할 수 있습니다. *com.adobe.cq.mobile.platform.impl.contentsync.handler.AbstractSlingResourceUpdateHandler*
* 처리기는 ContentSync 캐시를 업데이트하는 경우에만 true를 보고해야 합니다. true를 잘못 보고하면 업데이트가 실제로 발생하지 않았을 때 AEM에서 업데이트를 만듭니다.
* 처리기는 콘텐츠가 변경된 경우에만 캐시를 업데이트해야 합니다. 흰색이 필요하지 않은 경우 캐시에 쓰지 마십시오. 따라서 불필요한 업데이트가 생성됩니다.

>[!NOTE]
>
>사용 *ContentSync 디버그 로깅* 패키지의 OSGI 로거 구성을 통해 *com.day.cq.contentsync*. 그러면 어떤 핸들러가 실행되었는지, 캐시가 업데이트되었는지, 캐시 업데이트가 보고되었는지 여부를 추적할 수 있습니다.

## 컨텐츠 동기화 컨텐츠 구성 {#configuring-the-content-sync-content}

콘텐츠 동기화 구성을 만들어 클라이언트에 제공되는 ZIP 파일의 콘텐츠를 지정합니다. 콘텐츠 동기화 구성을 원하는 수만큼 만들 수 있습니다. 각 구성에는 식별을 위한 이름이 있습니다.

콘텐츠 동기화 구성을 만들려면 `cq:ContentSyncConfig` 노드를 리포지토리에 추가합니다. `sling:resourceType` 속성이 로 설정됨 `contentsync/config`. 다음 `cq:ContentSyncConfig` 노드는 저장소의 어디에나 있을 수 있지만, AEM 게시 인스턴스의 사용자는 노드에 액세스할 수 있어야 합니다. 따라서 아래에 노드를 추가해야 합니다. `/content`.

콘텐츠 동기화 ZIP 파일의 콘텐츠를 지정하려면 cq:ContentSyncConfig 노드에 하위 노드를 추가합니다. 각 하위 노드의 다음 속성은 포함할 콘텐츠 항목과 이 항목을 추가할 때 처리되는 방법을 식별합니다.

* `path`: 콘텐츠의 위치입니다.
* `type`: 콘텐츠 처리에 사용할 구성 유형의 이름입니다. 몇 가지 유형을 사용할 수 있으며 섹션에 설명되어 있습니다 *구성 유형*.

다음을 참조하십시오 *콘텐츠 동기화 구성 예* 추가 정보.

콘텐츠 동기화 구성을 만들면 콘텐츠 동기화 콘솔에 표시됩니다.

>[!NOTE]
>
>Content Sync 프레임워크는 자산 및 디자인 관련 파일의 종속성이 Content Sync 패키지에 포함되어 있는지 확인하지 않습니다. ZIP 파일에 모든 필수 파일을 포함해야 합니다.

### 콘텐츠 동기화 다운로드에 대한 액세스 구성 {#configuring-access-to-content-sync-downloads}

콘텐츠 동기화에서 다운로드할 수 있는 사용자 또는 그룹을 지정합니다. 모든 Content Sync 캐시에서 다운로드할 수 있는 기본 사용자 또는 그룹을 구성할 수 있으며, 기본값을 재정의하고 특정 Content Sync 구성에 대한 액세스를 구성할 수 있습니다.

AEM이 설치되면 기본적으로 관리자 그룹의 구성원은 Content Sync에서 다운로드할 수 있습니다.

#### 콘텐츠 동기화 다운로드에 대한 기본 액세스 설정 {#setting-the-default-access-for-content-sync-downloads}

Day CQ Content Sync Manager 서비스는 콘텐츠 동기화에 대한 액세스를 제어합니다. 기본적으로 Content Sync에서 다운로드할 수 있는 사용자 또는 그룹을 지정하도록 이 서비스를 구성합니다.

다음과 같은 경우 [웹 콘솔을 사용한 서비스 구성](/help/sites-deploying/configuring-osgi.md#osgi-configuration-with-the-web-console), 사용자 또는 그룹의 이름을 대체 캐시 승인 가능 속성의 값으로 입력합니다.

다음과 같은 경우 [저장소에서 구성](/help/sites-deploying/configuring-osgi.md#osgi-configuration-in-the-repository), 서비스에 대한 다음 정보 사용:

* PID: com.day.cq.contentsync.impl.ContentSyncManagerImpl
* 속성 이름: contentsync.fallback.authorizable

#### 콘텐츠 동기화 캐시에 대한 다운로드 액세스 재정의 {#overriding-download-access-for-a-content-sync-cache}

특정 Content Sync 구성에 대한 다운로드 액세스를 구성하려면 다음 속성을 `cq:ContentSyncConfig` 노드:

* 이름: 승인 가능
* 유형: 문자열
* 값: 다운로드할 수 있는 사용자 또는 그룹의 이름입니다.

예를 들어 앱을 사용하면 사용자가 Content Sync에서 직접 업데이트를 설치할 수 있습니다. 모든 사용자가 업데이트를 다운로드할 수 있도록 하려면 승인 가능 속성의 값을 로 설정합니다 `everyone`.

다음과 같은 경우 `cq:ContentSyncConfig` 노드에는 승인 가능 속성이 없습니다. 일별 CQ Content Sync Manager 서비스의 대체 캐시 승인 가능 속성에 대해 구성된 기본 사용자 또는 그룹이 다운로드할 수 있는 사용자를 결정합니다.

### 콘텐츠 동기화 캐시를 업데이트하기 위한 사용자 구성 {#configuring-the-user-for-updating-a-content-sync-cache}

사용자가 Content Sync 캐시에 대한 업데이트를 수행할 때 특정 사용자 계정이 사용자를 대신하여 해당 작업을 수행합니다. 익명 사용자는 기본적으로 모든 Content Sync 캐시를 업데이트합니다.

기본 사용자를 재정의하고 특정 Content Sync 캐시를 업데이트하는 사용자 또는 그룹을 지정할 수 있습니다.

기본 사용자를 재정의하려면 cq:ContentSyncConfig 노드에 다음 속성을 추가하여 특정 Content Sync 구성에 대한 업데이트를 수행하는 사용자 또는 그룹을 지정합니다.

* 이름: `updateuser`
* 유형: `String`
* 값: 갱신을 수행할 수 있는 사용자 또는 그룹의 이름입니다.

다음과 같은 경우 `cq:ContentSyncConfig` 노드에 없음 `updateuser` 속성, 기본값 `anonymous` 사용자가 캐시를 업데이트합니다.

### 구성 유형 {#configuration-types}

처리는 간단한 JSON 렌더링부터 참조된 에셋을 포함한 페이지의 완전한 렌더링까지 다양할 수 있습니다. 이 섹션에는 사용 가능한 구성 유형 및 특정 매개 변수가 나열되어 있습니다.

**복사** - 파일 및 폴더를 복사합니다.

* **경로** - 경로가 단일 파일을 가리키면 파일만 복사됩니다. 폴더를 가리키면(페이지 노드 포함) 아래의 모든 파일과 폴더가 복사됩니다.

**콘텐츠** 표준을 사용하여 콘텐츠 렌더링 [Sling 요청 처리](/help/sites-developing/the-basics.md#sling-request-processing).

* **경로** - 출력해야 하는 리소스의 경로.
* **확장** - 요청에 사용해야 하는 확장명. 일반적인 예는 다음과 같습니다 *html* 및 *json*&#x200B;다른 확장 프로그램도 가능합니다.

* **선택기** - 점으로 구분된 선택적 선택기. 일반적인 예는 다음과 같습니다 *터치* 페이지의 모바일 버전을 렌더링하거나 *무한대* JSON 출력용.

**clientlib** - JavaScript 또는 CSS 클라이언트 라이브러리를 패키징합니다.

* **경로** - 클라이언트 라이브러리의 루트에 대한 경로입니다.
* **확장** - 클라이언트 라이브러리 유형. 다음 중 하나로 설정해야 합니다. *js* 또는 *css* 지금이요.

**assets**

자산의 원본 렌디션을 수집합니다.

* **경로** - /content/dam 아래의 자산 폴더 경로.

**이미지** - 이미지를 수집합니다.

* **경로** - 이미지 리소스 경로.

이미지 유형은 zip 파일에 We Retail 로고를 포함하는 데 사용됩니다.

**페이지** - AEM 페이지를 렌더링하고 참조된 자산을 수집합니다.

* **경로** - 페이지 경로.
* **확장** - 요청에 사용해야 하는 확장명. 페이지의 경우 거의 항상 다음과 같습니다. *html*, 그러나 다른 기능은 여전히 가능합니다.

* **선택기** - 점으로 구분된 선택적 선택기. 일반적인 예는 다음과 같습니다 *터치* 페이지의 모바일 버전을 렌더링하는 경우.

* **깊이** - 하위 페이지를 포함해야 하는지 여부를 결정하는 부울 속성(선택 사항). 기본값은 입니다. *맞아.*

* **includeImages** - 이미지를 포함해야 하는지 여부를 결정하는 선택적 부울 속성. 기본값은 입니다. *true*.

  기본적으로 기본/구성 요소/이미지 리소스 유형의 이미지 구성 요소만 포함할 것으로 간주됩니다. 다음을 구성하여 더 많은 리소스 유형을 추가할 수 있습니다. **일별 CQ WCM 페이지 업데이트 핸들러** 웹 콘솔에서 게시할 수 있습니다.

**다시 작성** - 다시 작성 노드는 내보낸 페이지에서 링크가 다시 작성되는 방식을 정의합니다. 다시 작성된 링크는 zip 파일에 포함된 파일이나 서버의 리소스를 가리킬 수 있습니다.

다음 `rewrite` 노드는 다음 아래에 있어야 합니다. `page` 노드.

다음 `rewrite` 노드에는 다음 속성 중 하나 이상이 있을 수 있습니다.

* `clientlibs`: clientlibs 경로를 재작성합니다.

* `images`: 이미지 경로를 재작성합니다.
* `links`: 링크 경로를 재작성합니다.

각 속성은 다음 값 중 하나를 가질 수 있습니다.

* `REWRITE_RELATIVE`: 파일 시스템에서 페이지 .html 파일에 대한 상대적 위치로 경로를 재작성합니다.

* `REWRITE_EXTERNAL`: AEM을 사용하여 서버의 리소스를 가리키도록 경로를 재작성합니다. [Externalizer 서비스](/help/sites-developing/externalizer.md).

AEM 서비스가 호출되었습니다. **PathRewriterTransformerFactory** 다시 작성할 특정 html 속성을 구성할 수 있습니다. 이 서비스는 웹 콘솔에서 구성할 수 있으며 의 각 속성에 대한 구성을 갖습니다. `rewrite` 노드: `clientlibs`, `images`, 및 `links`.

이 기능은 AEM 5.5에 추가되었습니다.

### 콘텐츠 동기화 구성 예 {#example-content-sync-configuration}

아래 목록은 콘텐츠 동기화에 대한 예제 구성을 보여 줍니다.

```xml
+ weretail_go [cq:ContentSyncConfig]
  - sling:resourceType = "contentsync/config"

  + etc.designs.default [nt:unstructured]
    - path = "/etc/designs/default"
    - type = "copy"

  + etc.designs.mobile [nt:unstructured]
    - path = "/etc/designs/mobile"
    - type = "copy"

  + events.plist [nt:unstructured]
    - path = "/content/weretail_mobile/en/events/jcr:content/par/events"
    - type = "content"
    - extension = "plist"

  + events.touch.html [nt:unstructured]
    - path = "/content/weretail_mobile/en/events"
    - type = "pages"
    - extension = "html"
    - selector = "touch"

  + logo [nt:unstructured]
    - path = "/etc/designs/mobile/jcr:content/mobilecontentpage/logo"
    - type = "logo"

  + manifest [nt:unstructured]
    - indexPage = "/content/weretail_mobile/en/events.touch.html"
    - metadataPlist = "/content/weretail_mobile/en/events/_jcr_content/par/events.plist"

  + ...
```

**etc.designs.default 및 etc.designs.mobile** - 구성의 처음 두 항목이 명확합니다. 여러 모바일 페이지를 포함시키려면 /etc/designs 아래에 관련 디자인 파일이 필요합니다. 또한 추가 처리가 필요하지 않으므로 복사가 충분합니다.

**events.plist** - 이 항목은 좀 특별합니다. 서론에서 언급했듯이 애플리케이션은 이벤트 위치의 마커가 포함된 맵 보기를 제공해야 합니다. 필요한 위치 정보는 PLIST 형식의 별도 파일로 제공됩니다. 이를 위해 인덱스 페이지에서 사용되는 이벤트 목록 구성 요소에 plist.jsp라는 스크립트가 있습니다. 이 스크립트는 구성 요소의 리소스를 `.plist` 확장명. 평소대로 구성 요소 경로는 경로 속성에 지정되며 유형은 을 사용하려고 하므로 content로 설정됩니다 [Sling 요청 처리](/help/sites-developing/the-basics.md#sling-request-processing).

**events.touch.html** - 다음은 앱에 표시될 실제 페이지입니다. path 속성은 이벤트의 루트 페이지로 설정됩니다. 딥 속성의 기본값이 true이므로, 해당 페이지 아래의 모든 이벤트 페이지도 포함됩니다. 페이지를 구성 유형으로 사용하므로 페이지의 이미지 또는 다운로드 구성 요소에서 참조할 수 있는 모든 이미지 또는 기타 파일이 포함됩니다. 또한 터치 선택기를 설정하면 모바일 버전의 페이지가 제공됩니다. 기능 팩의 구성에는 이러한 종류의 항목이 더 포함되어 있지만 여기서는 간결성을 위해 생략되었습니다.

**로고** - 로고 구성 유형은 지금까지 언급되지 않았으며 빌드-인 유형 중 어느 것도 아닙니다. 그러나 Content Sync 프레임워크는 어느 정도 확장 가능하며 그 예는 다음 섹션에서 다룹니다.

**매니페스트** - 예를 들어 콘텐츠의 시작 페이지와 같이 zip 파일에 일종의 메타데이터를 포함하는 것이 바람직합니다. 그러나 이러한 정보를 하드코딩하면 나중에 쉽게 변경할 수 없습니다. Content Sync 프레임워크는 구성에서 이름으로 식별되고 구성 유형이 필요하지 않은 매니페스트 노드를 찾아 이 사용 사례를 지원합니다. 특정 노드에 정의된 모든 속성은 매니페스트라고도 하며 zip 파일의 루트에 있는 파일에 추가됩니다.

이 예제에서 이벤트 목록 페이지는 초기 페이지로 가정됩니다. 이 정보는 **indexPage** 및 속성은 언제든지 쉽게 변경될 수 있습니다. 두 번째 속성은 의 경로를 정의합니다 *events.plist* 파일. 나중에 볼 수 있듯이 클라이언트 애플리케이션은 이제 매니페스트를 읽고 그에 따라 작동할 수 있습니다.

구성이 설정되면 콘텐츠는 브라우저나 다른 HTTP 클라이언트를 통해 다운로드할 수 있습니다. 또는 iOS용으로 개발하는 경우 전용 WAppKitSync 클라이언트 라이브러리를 사용할 수 있습니다. 다운로드 위치는 구성의 경로 및 *.zip* 확장(예: 로컬 AEM 인스턴스로 작업하는 경우): *http://localhost:4502/content/weretail_go.zip*

### 콘텐츠 동기화 콘솔 {#the-content-sync-console}

콘텐츠 동기화 콘솔에는 저장소의 모든 콘텐츠 동기화 구성(유형의 모든 노드)이 나열됩니다 `cq:ContentSyncConfig`) 각 구성에 대해 및 를 사용하여 다음을 수행할 수 있습니다.

* 캐시를 업데이트합니다.
* 캐시를 지웁니다.
* 전체 zip 다운로드.
* 현재와 특정 날짜 및 시간 사이의 차이점 zip을 다운로드합니다.

개발 및 문제 해결에 유용할 수 있습니다.

콘솔은 다음 위치에서 액세스할 수 있습니다.

`http://localhost:4502/libs/cq/contentsync/content/console.html`

이는 다음과 같습니다.

![chlimage_1-50](assets/chlimage_1-50.png)

### Content Sync 프레임워크 확장 {#extending-the-content-sync-framework}

구성 옵션의 수는 이미 광범위하지만 특정 사용 사례의 모든 요구 사항을 다루지는 않을 수 있습니다. 이 섹션에서는 Content Sync 프레임워크의 확장 지점 및 사용자 지정 구성 유형을 만드는 방법에 대해 설명합니다.

각 구성 유형에는 *컨텐츠 업데이트 핸들러*: 특정 유형에 등록된 OSGi 구성 요소 팩터리입니다. 이러한 처리기는 콘텐츠를 수집하고 처리한 다음 Content Sync 프레임워크에서 유지 관리하는 캐시에 추가합니다. 다음 인터페이스 또는 추상 기본 클래스를 구현합니다.

* `com.day.cq.contentsync.handler.ContentUpdateHandler` - 모든 업데이트 처리기가 구현해야 하는 인터페이스
* `com.day.cq.contentsync.handler.AbstractSlingResourceUpdateHandler` - Sling을 사용하여 리소스 렌더링을 간소화하는 추상 클래스

클래스를 OSGi 구성 요소 팩토리로 등록하고 번들의 OSGi 컨테이너에 배포합니다. 다음을 사용하여 이 작업을 수행할 수 있습니다. [Maven SCR 플러그인](https://felix.apache.org/documentation/subprojects/apache-felix-maven-scr-plugin/apache-felix-maven-scr-plugin-use.html) JavaDoc 태그 또는 주석 사용. 다음 예제는 JavaDoc 버전을 보여 줍니다.

```java
/*
 * @scr.component metatype="no"
 * factory="com.day.cq.contentsync.handler.ContentUpdateHandler/customtype"
 */
public class CustomTypeUpdateHandler implements ContentUpdateHandler {
    // add your code here
}

/*
 * @scr.component metatype="no" inherit="true"
 * factory="com.day.cq.contentsync.handler.ContentUpdateHandler/othertype"
 */
public class OtherTypeUpdateHandler extends AbstractSlingResourceUpdateHandler {
    // add your code here
}
```

다음 사항에 주목하십시오. *공장* 정의에는 슬래시로 구분된 공통 인터페이스와 사용자 정의 유형이 포함됩니다. 이 전략을 사용하면 콘텐츠 동기화 프레임워크는 구성 항목에서 사용자 지정 유형을 인식하므로 사용자 지정 클래스의 인스턴스를 찾고 만들 수 있습니다. 다음 섹션에서는 사용자 지정 업데이트 처리기의 구체적인 예를 제공합니다.

>[!CAUTION]
>
>AbstractSlingResourceUpdateHandler 기본 클래스를 기반으로 빌드하는 경우 *상속* 정의. 그렇지 않으면 OSGi 컨테이너는 기본 클래스에서 선언되는 필수 참조를 설정하지 않습니다.

### 사용자 지정 업데이트 처리기 구현 {#implementing-a-custom-update-handler}

모든 We.Retail 모바일 페이지에는 zip 파일에 포함되어야 하는 로고가 왼쪽 상단 모서리에 있습니다. 그러나 캐시 최적화를 위해 AEM은 저장소의 이미지 파일 실제 위치를 참조하지 않으므로 를 사용하지 못할 수 있습니다. **복사** 구성 유형. 대신 당신이 해야 할 일은 우리의 것을 제공하는 것입니다 **로고** AEM에서 요청한 위치에서 이미지를 사용할 수 있도록 하는 구성 유형입니다. 다음 코드 목록은 로고 업데이트 처리기의 전체 구현을 보여 줍니다.

#### LogoUpdateHandler.java {#logoupdatehandler-java}

```java
package com.day.cq.wcm.apps.weretail.impl;

import javax.jcr.Node;
import javax.jcr.RepositoryException;
import javax.jcr.Session;

import org.apache.sling.api.resource.Resource;
import org.apache.sling.api.resource.ResourceResolver;
import org.apache.sling.jcr.resource.JcrResourceResolverFactory;

import com.day.cq.commons.jcr.JcrUtil;
import com.day.cq.contentsync.config.ConfigEntry;
import com.day.cq.contentsync.handler.ContentUpdateHandler;
import com.day.cq.wcm.foundation.Image;
import com.day.text.Text;

/**
 * The <code>LogoUpdateHandler</code> is used to update the content sync cache
 * with a page logo added using a logo component.
 *
 * @scr.component metatype="no"
 * factory="com.day.cq.contentsync.handler.ContentUpdateHandler/logo"
 */
public class LogoUpdateHandler implements ContentUpdateHandler {

    private static final Logger log = LoggerFactory.getLogger(LogoUpdateHandler.class);

    /** @scr.reference policy="static" */
    protected JcrResourceResolverFactory resolverFactory;

    public boolean updateCacheEntry(ConfigEntry configEntry, Long lastUpdated, String configCacheRoot, Session admin, Session session) {
        ResourceResolver resolver = resolverFactory.getResourceResolver(admin);
        Resource resource = resolver.getResource(configEntry.getContentPath());

        Image img = new Image(resource);
        img.setItemName(Image.NN_FILE, "image");
        img.setItemName(Image.PN_REFERENCE, "imageReference");
        img.setSelector("img");

        try {
            if(img.getLastModified() == null || lastUpdated < img.getLastModified().getTime().getTime()) {
                String src = img.getSrc();
                String parentPath = configCacheRoot + Text.getRelativeParent(src, 1);

                Node parent = JcrUtil.createPath(parentPath, "sling:Folder", admin);
                Node image = resolver.getResource(resource.getPath() + "/image").adaptTo(Node.class);
                JcrUtil.copy(image, parent, Text.getName(src));

                admin.save();

                return true;
            }
        } catch (RepositoryException e) {
            log.error("Unexpected error while updating logo: ", e);
        }

        return false;
    }
}
```

다음 `LogoUpdateHandler` 클래스는 `ContentUpdateHandler` 인터페이스 `updateCacheEntry(ConfigEntry, Long, String, Session, Session)` 메서드, 여러 인수를 사용합니다.

* A `ConfigEntry` 이 처리기가 호출되는 구성 항목 및 해당 속성에 대한 액세스를 제공하는 인스턴스입니다.
* A `lastUpdated` 콘텐츠 동기화가 캐시를 마지막으로 업데이트한 시간을 나타내는 타임스탬프입니다. 해당 타임스탬프 후에 수정되지 않은 콘텐츠는 핸들러가 업데이트하면 안 됩니다.
* A `configCacheRoot` 캐시의 루트 경로를 지정하는 인수 업데이트된 모든 파일은 이 경로 아래에 저장해야 zip 파일에 추가할 수 있습니다.
* 모든 캐시 관련 저장소 작업에 사용해야 하는 관리 세션입니다.
* 특정 사용자의 컨텍스트에서 콘텐츠를 업데이트하여 일종의 개인화된 콘텐츠를 제공하는 데 사용할 수 있는 사용자 세션입니다.

사용자 지정 처리기를 구현하려면 먼저 구성 항목에 지정된 리소스를 기반으로 Image 클래스의 인스턴스를 만듭니다. 이는 페이지의 실제 로고 구성 요소와 동일한 절차를 따릅니다. 이미지의 대상 경로가 페이지에서 참조된 경로와 동일한지 확인합니다.

그런 다음 마지막 업데이트 이후 리소스가 수정되었는지 확인합니다. 사용자 지정 구현은 캐시의 불필요한 업데이트를 방지하고 아무것도 변경되지 않으면 false를 반환해야 합니다. 리소스가 수정된 경우 이미지를 캐시 루트에 상대적인 예상 대상 위치에 복사합니다. 마지막으로, `true` 는 캐시가 업데이트되었음을 프레임워크에 표시하기 위해 반환됩니다.

## 클라이언트에서 컨텐츠 사용 {#using-the-content-on-the-client}

Content Sync에서 제공하는 모바일 앱에서 콘텐츠를 사용하려면 HTTP 또는 HTTPS 연결을 통해 콘텐츠를 요청해야 합니다. 그 결과, 검색된 콘텐츠(ZIP 파일에 압축됨)가 추출되어 모바일 디바이스에 로컬로 저장될 수 있습니다. 콘텐츠는 데이터뿐만 아니라 논리, 즉 완전한 웹 애플리케이션을 의미하므로 모바일 사용자는 네트워크 연결 없이도 검색된 웹 애플리케이션 및 해당 데이터를 실행할 수 있습니다.

Content Sync는 지능적인 방식으로 콘텐츠를 제공합니다. 마지막으로 성공한 데이터 동기화 이후의 데이터 변경만 제공되므로 데이터 전송에 필요한 시간을 줄일 수 있습니다. 응용 프로그램을 처음 실행할 때는 1970년 1월 01일 이후 데이터 변경이 요청되지만, 나중에 마지막으로 성공한 동기화 이후 변경된 데이터만 요청됩니다. AEM은 iOS용 클라이언트 통신 프레임워크를 사용하여 데이터 통신 및 전송을 단순화하므로 iOS 기반 웹 애플리케이션을 활성화하는 데 최소한의 기본 코드가 필요합니다.

전송된 모든 데이터를 동일한 디렉토리 구조로 추출할 수 있으므로 데이터를 추출할 때 추가 단계(예: 종속성 확인)가 필요하지 않습니다. iOS이 있는 경우 모든 데이터는 iOS 앱의 Documents 폴더 내에 있는 하위 폴더에 저장됩니다.

iOS 기반 AEM Mobile 앱의 일반적인 실행 경로:

* 사용자가 iOS 장치에서 앱을 시작합니다.
* 앱에서 AEM 백엔드에 연결을 시도하고 마지막 실행 이후 데이터 변경 사항을 요청합니다.
* 서버는 해당 데이터를 검색하여 파일에 넣습니다.
* 데이터는 클라이언트 장치로 반환되어 문서 폴더로 추출됩니다.
* UIWebView 구성 요소 시작/새로 고침

이전에 연결을 설정할 수 없었던 경우 다운로드한 데이터가 표시됩니다.

### 추가 리소스 {#additional-resources}

관리자 및 작성자의 역할과 책임에 대해 알아보려면 아래 리소스를 참조하십시오.

* [AEM Mobile On-demand Services용 AEM 컨텐츠 작성](/help/mobile/mobile-apps-ondemand.md)
* [AEM Mobile On-demand Services을 사용할 컨텐츠 관리](/help/mobile/aem-mobile.md)
