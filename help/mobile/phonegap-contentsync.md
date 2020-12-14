---
title: 컨텐츠 동기화를 통한 모바일
seo-title: 컨텐츠 동기화를 통한 모바일
description: AEM과 Adobe PhoneGap Enterprise의 콘텐츠 동기화에 대해 알아보려면 이 페이지를 따르십시오.
seo-description: AEM과 Adobe PhoneGap Enterprise의 콘텐츠 동기화에 대해 알아보려면 이 페이지를 따르십시오.
uuid: c3a82171-e070-4e32-b1ef-26e65ae23d99
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
discoiquuid: 923fc031-1a06-4a9d-94da-a2a4e82c54ee
docset: aem65
translation-type: tm+mt
source-git-commit: 27a054cc5d502d95c664c3b414d0066c6c120b65
workflow-type: tm+mt
source-wordcount: '2989'
ht-degree: 0%

---


# 컨텐트 동기화 포함 모바일{#mobile-with-content-sync}

>[!NOTE]
>
>단일 페이지 애플리케이션 프레임워크 기반 클라이언트측 렌더링(예: 응답)이 필요한 프로젝트에는 SPA 편집기를 사용하는 것이 좋습니다. [추가 정보](/help/sites-developing/spa-overview.md).

>[!NOTE]
>
>이 문서는 AEM Mobile 참조의 권장 시작점인 [AEM Mobile 시작](/help/mobile/getting-started-aem-mobile.md) 안내서의 일부입니다.

컨텐츠 동기화를 사용하여 기본 모바일 애플리케이션에서 사용할 수 있도록 컨텐츠를 패키지화할 수 있습니다. AEM에서 제작한 페이지는 장치가 오프라인 상태일 때도 앱 콘텐츠로 사용할 수 있습니다. 또한 AEM 페이지는 웹 표준을 기반으로 하므로 크로스 플랫폼 방식으로 작동하므로 모든 기본 래퍼에 포함할 수 있습니다. 이 전략을 통해 개발 노력을 줄이고 앱 콘텐츠를 손쉽게 업데이트할 수 있습니다.

>[!NOTE]
>
>AEM 도구를 사용하여 만든 PhoneGap 앱은 콘텐츠 동기화를 통해 AEM 페이지를 컨텐츠로 사용하도록 이미 구성되어 있습니다.

Content Sync 프레임워크는 웹 컨텐츠가 포함된 아카이브 파일을 만듭니다. 컨텐츠는 간단한 페이지, 이미지, PDF 파일 또는 전체 웹 애플리케이션에서부터 무엇이든 될 수 있습니다. 콘텐츠 동기화 API는 모바일 앱 또는 빌드 프로세스의 보관 파일에 대한 액세스를 제공하여 콘텐츠를 검색하고 앱에 포함할 수 있도록 합니다.

다음 단계는 컨텐츠 동기화에 대한 일반적인 사용 사례를 보여줍니다.

1. AEM 개발자는 포함할 컨텐트를 지정하는 컨텐츠 동기화 구성을 만듭니다.
1. Content Sync 프레임워크는 콘텐츠를 수집하고 캐시합니다.
1. 모바일 장치에서 모바일 응용 프로그램이 시작되고 ZIP 파일로 전달되는 서버로부터 콘텐트를 요청합니다.
1. 클라이언트는 ZIP 콘텐트를 로컬 파일 시스템에 압축 해제합니다. ZIP 파일의 폴더 구조는 클라이언트(예: 브라우저)가 서버에서 정상적으로 요청하는 경로를 시뮬레이션합니다.
1. 클라이언트는 포함된 브라우저에서 컨텐츠를 열거나 다른 방법으로 사용합니다.
1. 나중에 클라이언트는 서버의 업데이트된 컨텐츠를 요청합니다. Content Sync 프레임워크는 다운로드 크기와 시간을 줄이기 위해 증분 업데이트를 제공하므로 대역폭이나 데이터 볼륨이 제한되어 있으므로 모바일 장치에 중요합니다.

>[!NOTE]
>
>Content Sync 핸들러 개발에 대한 지침을 보려면 최신 앱 핸들러에서 [콘텐츠 동기화 핸들러 개발](/help/mobile/contentsync-app-handlers.md)을 참조하십시오.

## 콘텐츠 동기화 콘텐츠 구성 {#configuring-the-content-sync-content}

컨텐츠 동기화 구성을 만들어 클라이언트에 배달되는 ZIP 파일의 컨텐츠를 지정합니다. 원하는 수의 콘텐츠 동기화 구성을 만들 수 있습니다. 각 구성에는 식별을 위한 이름이 있습니다.

컨텐트 동기화 구성을 만들려면 `sling:resourceType` 속성이 `contentsync/config`로 설정된 상태로 `cq:ContentSyncConfig` 노드를 저장소에 추가합니다. `cq:ContentSyncConfig` 노드는 저장소의 어느 곳에나 위치할 수 있지만 AEM 게시 인스턴스의 사용자는 노드에 액세스할 수 있어야 합니다. 따라서 `/content` 아래의 노드를 추가해야 합니다.

콘텐츠 동기화 ZIP 파일의 내용을 지정하려면 cq:ContentSyncConfig 노드에 하위 노드를 추가합니다. 각 하위 노드의 다음 속성은 포함할 컨텐츠 항목과 추가 시 처리되는 방식을 식별합니다.

* `path`:컨텐츠의 위치입니다.
* `type`:컨텐츠 처리에 사용할 구성 유형의 이름입니다. 여러 유형을 사용할 수 있으며 구성 유형에 대해 설명합니다.

콘텐츠 동기화 구성 예를 참조하십시오.

콘텐츠 동기화 구성을 만들면 콘텐츠 동기화 콘솔에 표시됩니다.

>[!NOTE]
>
>Content Sync 프레임워크에서는 자산 및 디자인 관련 파일의 종속성이 Content Sync 패키지에 포함되어 있는지 확인하지 않습니다. ZIP 파일에 필요한 모든 파일을 포함해야 합니다.

### 콘텐트 동기화 다운로드에 대한 액세스 구성 {#configuring-access-to-content-sync-downloads}

콘텐츠 동기화에서 다운로드할 수 있는 사용자 또는 그룹을 지정합니다. 모든 콘텐츠 동기화 캐시에서 다운로드할 수 있는 기본 사용자 또는 그룹을 구성할 수 있으며 기본값을 재정의하고 특정 콘텐츠 동기화 구성에 대한 액세스 권한을 구성할 수 있습니다.

AEM이 설치되면 관리자 그룹의 구성원은 기본적으로 콘텐츠 동기화에서 다운로드할 수 있습니다.

### 컨텐츠 동기화에 대한 기본 액세스 설정 다운로드 {#setting-the-default-access-for-content-sync-downloads}

CQ Content Sync Manager의 요일 서비스는 콘텐츠 동기화에 대한 액세스를 제어합니다. 기본적으로 콘텐츠 동기화에서 다운로드할 수 있는 사용자 또는 그룹을 지정하도록 이 서비스를 구성합니다.

웹 콘솔[을(를) 사용하여 서비스를 구성하는 경우 사용자 또는 그룹의 이름을 폴백 캐시 승인 가능 속성의 값으로 입력합니다.](/help/sites-deploying/configuring-osgi.md#osgi-configuration-with-the-web-console)

[리포지토리](/help/sites-deploying/configuring-osgi.md#osgi-configuration-in-the-repository)에서 구성하는 경우 서비스에 대한 다음 정보를 사용하십시오.

* PID:com.day.cq.contentsync.impl.ContentSyncManagerImpl
* 속성 이름:contentsync.fallback.authorizable

#### 콘텐트 동기화 캐시에 대한 다운로드 액세스 재정의 {#overriding-download-access-for-a-content-sync-cache}

특정 콘텐츠 동기화 구성에 대한 다운로드 액세스를 구성하려면 `cq:ContentSyncConfig` 노드에 다음 속성을 추가하십시오.

* 이름:작성 가능
* 유형:문자열
* 값:다운로드할 수 있는 사용자 또는 그룹의 이름입니다.

예를 들어 사용자가 앱을 통해 Content Sync에서 바로 업데이트를 설치할 수 있습니다. 모든 사용자가 업데이트를 다운로드할 수 있도록 하려면 authorizable 속성의 값을 `everyone`으로 설정합니다.

`cq:ContentSyncConfig` 노드에 인증 가능한 속성이 없는 경우 Day CQ Content Sync Manager 서비스의 Fallback Cache Authorizable 속성에 대해 구성된 기본 사용자 또는 그룹이 다운로드할 수 있는 사람을 결정합니다.

### 콘텐트 동기화 캐시 업데이트를 위한 사용자 구성 {#configuring-the-user-for-updating-a-content-sync-cache}

사용자가 컨텐츠 동기화 캐시에 대한 업데이트를 수행하는 경우 특정 사용자 계정은 사용자를 대신하여 작업을 수행합니다. 익명 사용자는 기본적으로 모든 콘텐츠 동기화 캐시를 업데이트합니다.

기본 사용자를 재정의하고 특정 컨텐츠 동기화 캐시를 업데이트하는 사용자 또는 그룹을 지정할 수 있습니다.

기본 사용자를 재정의하려면 cq:ContentSyncConfig 노드에 다음 속성을 추가하여 특정 콘텐츠 동기화 구성에 대한 업데이트를 수행하는 사용자 또는 그룹을 지정합니다.

* 이름:updateuser
* 유형:문자열
* 값:업데이트를 수행할 수 있는 사용자 또는 그룹의 이름입니다.

cq:ContentSyncConfig 노드에 업데이트 사용자 속성이 없으면 기본 익명 사용자가 캐시를 업데이트합니다.

### 구성 유형 {#configuration-types}

처리 범위는 간단한 JSON을 렌더링하는 것부터 참조된 자산을 포함한 페이지의 완전한 렌더링 범위까지 가능합니다. 이 섹션에는 사용 가능한 구성 유형과 특정 매개 변수가 나와 있습니다.

**복사** 간단히 파일 및 폴더 복사

* **경로**  - 경로가 단일 파일을 가리키면 파일만 복사됩니다. 폴더(페이지 노드 포함)를 가리키면 아래 모든 파일과 폴더가 복사됩니다.

**컨텐츠** 표준 Sling 요청 처리를 사용하여 컨텐츠를 렌더링합니다.

* **경로**  - 출력해야 하는 리소스의 경로입니다.
* **확장**  - 요청에 사용해야 하는 확장입니다. 일반적인 예로는 *html* 및 *json*&#x200B;이지만 다른 확장명은 사용할 수 있습니다.

* **선택기**  - 선택적인 선택기는 점으로 구분됩니다. 일반적인 예는 페이지의 모바일 버전을 렌더링하는 경우 *touch*, JSON 출력의 경우 *infinity*&#x200B;입니다.

**clientlib** Javascript 또는 CSS 클라이언트 라이브러리를 패키지화합니다.

* **경로**  - 클라이언트 라이브러리의 루트에 대한 경로입니다.
* **확장**  - 클라이언트 라이브러리의 유형입니다. 지금은 *js* 또는 *css*&#x200B;로 설정해야 합니다.

* **includeFolders** - Type은 문자열 배열이며, 사용자가 클라이언트 라이브러리에서 스캔하여 파일을 가져올 추가 폴더(예: 사용자 정의 글꼴)를 지정할 수 있도록 합니다.

**자산**

자산의 원본 표현물을 수집합니다.

* **경로**  - /content/dam 아래 자산 폴더의 경로입니다.
* **표현물**  - 유형은 기본 이미지 대신 사용할 표현물을 지정할 수 있는 문자열 배열입니다. 다음 목록은 일부 기본 변환을 요약하지만 워크플로우에서 만든 변환을 사용할 수도 있습니다.

   * *원본*
   * *cq5dam.thumbnail.48.48.png*
   * *cq5dam.thumbnail.319.319.png*
   * *cq5dam.thumbnail.140.100.png*
   * *cq5dam.web.1280.1280.png*

**이미지** 이미지를 수집합니다.

* **경로**  - 이미지 리소스에 대한 경로입니다.

이미지 유형은 zip 파일에 We.Retail 로고를 포함하는 데 사용됩니다.

**페이지** AEM 페이지를 렌더링하고 참조된 자산을 수집합니다.

* **경로**  - 페이지의 경로입니다.
* **확장**  - 요청에 사용해야 하는 확장입니다. 페이지의 경우 거의 항상 *html*&#x200B;이지만 다른 페이지는 여전히 사용할 수 있습니다.

* **선택기**  - 선택적인 선택기는 점으로 구분됩니다. 일반적인 예는 페이지의 모바일 버전을 렌더링하기 위한 *touch*&#x200B;입니다.

* **deep**  - 하위 페이지를 포함할지 여부를 결정하는 선택적 부울 속성입니다. 기본값은 *true입니다.*

* **includeImages**  - 이미지를 포함해야 하는지 여부를 결정하는 선택적 부울 속성입니다. 기본값은 *true*입니다.
기본적으로 리소스 유형의 foundation/components/image가 있는 이미지 구성 요소만 포함으로 간주됩니다. 웹 콘솔에서 **Day CQ WCM 페이지 업데이트 처리기**&#x200B;를 구성하여 리소스 유형을 더 추가할 수 있습니다.

**다시** 쓰기다시 작성 노드는 내보낸 페이지에서 링크가 재작성되는 방식을 정의합니다. 새로 작성된 링크는 zip 파일에 포함된 파일이나 서버의 리소스를 가리킬 수 있습니다.

`rewrite` 노드는 `page` 노드 아래에 있어야 합니다.

`rewrite` 노드에는 다음 속성 중 하나 이상을 사용할 수 있습니다.

* `clientlibs`:clientlibs 경로를 다시 작성합니다.

* `images`:이미지 경로를 다시 작성합니다.
* `links`:링크 경로를 다시 작성합니다.

각 속성에는 다음 값 중 하나를 사용할 수 있습니다.

* `REWRITE_RELATIVE`:파일 시스템의 페이지 .html 파일에 대한 상대 위치로 경로를 다시 작성합니다.

* `REWRITE_EXTERNAL`:aem Externalizer 서비스를 사용하여 서버의 리소스를 가리키면 경로를  [다시 씁니다](/help/sites-developing/externalizer.md).

**PathRewriterTransformerFactory**&#x200B;라는 AEM 서비스를 사용하면 다시 작성할 특정 html 특성을 구성할 수 있습니다. 이 서비스는 웹 콘솔에서 구성할 수 있으며 `rewrite` 노드의 각 속성에 대한 구성이 있습니다.`clientlibs`, `images` 및 `links`.

이 기능은 AEM 5.5에서 추가되었습니다.

### 콘텐츠 동기화 구성 예 {#example-content-sync-configuration}

아래 목록은 콘텐츠 동기화에 대한 예제 구성을 보여줍니다.

```java
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

**etc.designs.default and etc.designs.** mobile구성의 처음 두 항목은 매우 명백해야 합니다. 모바일 페이지를 여러 개 포함할 예정이므로 /etc/designs 아래에 관련 디자인 파일이 필요합니다. 추가 처리가 필요하지 않으므로 복사본으로도 충분합니다.

**events.** plist이 항목은 약간 특별합니다. 소개에서 언급했듯이 응용 프로그램은 이벤트 위치의 마커가 포함된 맵 보기를 제공해야 합니다. 필요한 위치 정보를 PLIST 형식으로 별도의 파일로 제공할 예정입니다. 이를 위해 인덱스 페이지에서 사용되는 이벤트 목록 구성 요소에는 plist.jsp라는 스크립트가 있습니다. 이 스크립트는 구성 요소의 리소스가 .plist 확장명으로 요청될 때 실행됩니다. 일반적으로 구성 요소 경로는 path 속성에 지정되고 유형은 컨텐츠로 설정됩니다. Sling 요청 처리를 활용하려고 합니다.

**events.touch.** htmlNext는 앱에 표시될 실제 페이지가 표시됩니다. path 속성은 이벤트의 루트 페이지로 설정됩니다. 딥 속성의 기본값은 true이므로 해당 페이지 아래의 모든 이벤트 페이지도 포함됩니다. 페이지를 구성 유형으로 사용하여 이미지의 참조나 페이지의 다운로드 구성 요소에서 참조할 수 있는 이미지나 기타 파일을 포함할 수 있습니다. 또한 터치 선택기를 설정하면 페이지의 모바일 버전이 제공됩니다. Feature Pack의 구성에는 이러한 유형의 항목이 더 많이 포함되어 있지만 여기서는 간단히 볼 수 없습니다.

**로고** 지금까지 로고 구성 유형에 대해 언급되지 않았으며 내장 유형이 아닙니다. 그러나 Content Sync 프레임워크는 어느 정도까지 확장할 수 있으며 이러한 프레임워크의 예는 다음 섹션에서 다룹니다.

**매니페스트콘텐츠** 의 시작 페이지와 같이, zip 파일에 메타데이터의 종류를 포함하는 것이 바람직합니다. 그러나 이러한 정보를 하드코딩하면 나중에 쉽게 변경할 수 없습니다. Content Sync 프레임워크는 구성에서 단순히 이름으로 식별되고 구성 유형이 필요 없는 매니페스트 노드를 찾아 이러한 사용 사례를 지원합니다. 특정 노드에 정의된 모든 속성이 매니페스트라고도 하며 zip 파일의 루트에 있는 파일에 추가됩니다.

이 예에서 이벤트 목록 페이지는 초기 페이지여야 합니다. 이 정보는 **indexPage** 속성에 제공되므로 언제든지 쉽게 변경할 수 있습니다. 두 번째 속성은 *events.plist* 파일의 경로를 정의합니다. 나중에 볼 수 있듯이 클라이언트 응용 프로그램은 이제 매니페스트를 읽고 그에 따라 작동할 수 있습니다.

구성이 설정되면 브라우저나 다른 HTTP 클라이언트를 사용하여 컨텐츠를 다운로드할 수 있고 iOS용으로 개발 중인 경우 전용 WAppKitSync 클라이언트 라이브러리를 사용할 수 있습니다. 다운로드 위치는 로컬 AEM 인스턴스 작업 시 구성 경로와 *.zip* 확장명으로 구성됩니다.*https://localhost:4502/content/weretail_go.zip*

### 콘텐츠 동기화 콘솔 {#the-content-sync-console}

컨텐츠 동기화 콘솔에는 저장소의 모든 컨텐츠 동기화 구성(유형 `cq:ContentSyncConfig`)이 나열되며 각 구성에 대해 다음을 수행할 수 있습니다.

* 캐시를 업데이트합니다.
* 캐시를 지웁니다.
* 전체 zip을 다운로드합니다.
* 지금, 특정 날짜 및 시간 사이의 diff zip을 다운로드합니다.

개발 및 문제 해결에 사용할 수 있습니다.

다음 위치에서 콘솔에 액세스할 수 있습니다.

`https://localhost:4502/libs/cq/contentsync/content/console.html`

다음과 같습니다.

![chlimage_1](assets/chlimage_1.png)

### Content Sync 프레임워크 {#extending-the-content-sync-framework} 확장

구성 옵션 수는 이미 매우 광범위하지만 특정 사용 사례의 요구 사항을 모두 충족하지는 않을 수 있습니다. 이 섹션에서는 Content Sync 프레임워크의 확장 지점 및 사용자 정의 구성 유형을 만드는 방법에 대해 설명합니다.

각 구성 유형에 대해 해당 특정 유형에 대해 등록된 OSGi 구성 요소 팩터리인 *컨텐트 업데이트 핸들러*&#x200B;가 있습니다. 이러한 핸들러는 내용을 수집하고 처리하여 Content Sync 프레임워크에서 유지 관리하는 캐시에 추가합니다. 다음 인터페이스 또는 추상 기본 클래스를 구현합니다.

* `com.day.cq.contentsync.handler.ContentUpdateHandler` - 모든 업데이트 핸들러에서 구현해야 하는 인터페이스
* `com.day.cq.contentsync.handler.AbstractSlingResourceUpdateHandler` - Sling을 사용하여 리소스 렌더링을 간소화하는 추상 클래스

클래스를 OSGi 구성 요소 팩터리로 등록하고 번들의 OSGi 컨테이너에 배포합니다. JavaDoc 태그나 주석을 사용하여 [Maven SCR 플러그인](https://felix.apache.org/site/apache-felix-maven-scr-plugin.html)을 사용하여 수행할 수 있습니다. 다음 예는 JavaDoc 버전을 보여 줍니다.

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

*factory* 정의에는 공통 인터페이스와 사용자 정의 유형이 슬래시로 구분되어 있습니다. 이 전략을 사용하면 구성 항목에서 사용자 지정 유형을 인식하므로 Content Sync 프레임워크에서 사용자 지정 클래스의 인스턴스를 찾고 만들 수 있습니다. 다음 섹션에서는 사용자 지정 업데이트 핸들러의 구체적인 예를 보여 줍니다.

>[!CAUTION]
>
>AbstractSlingResourceUpdateHandler 기본 클래스를 기반으로 빌드할 때 *inherit* 정의를 추가해야 합니다. 그렇지 않으면 OSGi 컨테이너가 기본 클래스에서 선언되는 필수 참조를 설정하지 않습니다.

### 사용자 지정 업데이트 처리기 구현 {#implementing-a-custom-update-handler}

모든 We.Retail 모바일 페이지에는 물론, zip 파일에 포함시키고자 하는 로고가 왼쪽 위에 있습니다. 그러나 캐시 최적화의 경우, AEM은 저장소에서 이미지 파일의 실제 위치를 참조하지 않으므로 단순히 **copy** 구성 유형을 사용해서는 안 됩니다. 대신 AEM에서 요청한 위치에서 이미지를 사용할 수 있도록 하는 고유한 **로고** 구성 유형을 제공해야 합니다. 다음 코드 샘플에서는 로고 업데이트 핸들러의 전체 구현을 보여 줍니다.

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

`LogoUpdateHandler` 클래스는 많은 인수를 사용하는 `ContentUpdateHandler` 인터페이스의 `updateCacheEntry(ConfigEntry, Long, String, Session, Session)` 메서드를 구현합니다.

* 이 핸들러가 호출되는 구성 항목과 해당 속성에 대한 액세스 권한을 제공하는 `ConfigEntry` 인스턴스입니다.
* 콘텐츠 동기화가 마지막으로 캐시를 업데이트한 시간을 나타내는 `lastUpdated` 타임스탬프 해당 타임스탬프 이후에 수정되지 않은 콘텐츠는 핸들러가 업데이트할 수 없습니다.
* 캐시의 루트 경로를 지정하는 `configCacheRoot` 인수입니다. zip 파일에 추가하려면 업데이트된 모든 파일을 이 경로 아래에 저장해야 합니다.
* 모든 캐시 관련 저장소 작업에 사용해야 하는 관리 세션입니다.
* 특정 사용자의 컨텍스트에서 컨텐츠를 업데이트하여 일종의 개인화된 컨텐츠를 제공하는 데 사용할 수 있는 사용자 세션입니다.

사용자 지정 핸들러를 구현하려면 먼저 구성 항목에 지정된 리소스를 기반으로 Image 클래스의 인스턴스를 만듭니다. 이것은 기본적으로 페이지에서 실제 로고 구성 요소가 수행하는 절차와 동일합니다. 이미지의 대상 경로가 페이지에서 참조한 경로와 동일한지 확인합니다.

그런 다음 마지막 업데이트 이후 리소스가 수정되었는지 확인합니다. 사용자 지정 구현에서는 캐시가 불필요한 업데이트를 하지 않아야 하며 변경되지 않으면 false를 반환해야 합니다. 리소스가 수정된 경우 캐시 루트에 상대적인 예상 대상 위치에 이미지를 복사합니다. 마지막으로 `true`이(가) 캐시가 업데이트되었음을 나타내는 프레임워크로 반환됩니다.

## 클라이언트 {#using-the-content-on-the-client}의 컨텐츠 사용

콘텐츠 동기화에서 제공하는 모바일 앱에서 콘텐츠를 사용하려면 HTTP 또는 HTTPS 연결을 통해 콘텐츠를 요청해야 합니다. 따라서 검색된 컨텐츠(ZIP 파일에 압축)는 모바일 장치에서 추출하여 로컬에 저장할 수 있습니다. 컨텐츠는 데이터뿐만 아니라 논리, 즉 전체 웹 애플리케이션을 참조합니다.따라서 모바일 사용자는 네트워크 연결 없이도 검색 가능한 웹 애플리케이션과 해당 데이터를 실행할 수 있습니다.

컨텐츠 싱크는 지능적인 방식으로 컨텐츠를 전달합니다.마지막으로 성공한 데이터 동기화 이후 변경된 데이터만 제공되므로 데이터 전송 시간을 줄일 수 있습니다. 애플리케이션 데이터 변경 작업은 1970년 1월 1일 이후 처음 실행되며 이후에 마지막으로 동기화한 이후 변경된 데이터만 요청됩니다. AEM은 iOS용 클라이언트 통신 프레임워크를 사용하여 데이터 통신 및 전송을 단순화하여 iOS 기반 웹 애플리케이션을 활성화하는 데 최소한의 기본 코드가 필요합니다.

전송된 모든 데이터는 동일한 디렉토리 구조로 추출할 수 있으며, 데이터를 추출할 때 추가 단계(예: 종속성 검사)는 필요하지 않습니다. iOS의 경우 모든 데이터가 iOS 앱의 Documents 폴더 내의 하위 폴더에 저장됩니다.

iOS 기반 AEM Mobile 앱의 일반적인 실행 경로:

* 사용자가 iOS 장치에서 앱을 시작합니다.
* 앱이 AEM 백 엔드에 연결하려고 시도하고 마지막 실행 이후 데이터 변경을 요청합니다.
* 서버는 문제의 데이터를 검색하여 파일로 압축합니다.
* 데이터는 문서 폴더에 추출되는 클라이언트 장치로 반환됩니다.
* UIWebView 구성 요소 시작/새로 고침.

이전에 다운로드한 데이터를 사용하여 연결을 설정할 수 없는 경우 데이터가 표시됩니다.

### {#getting-ahead} 앞에 가져오기

관리자 및 개발자의 역할 및 책임을 살펴보려면 아래 리소스를 참조하십시오.

* [AEM을 사용한 Adobe PhoneGap Enterprise 저작](/help/mobile/phonegap.md)
* [AEM에서 Adobe PhoneGap Enterprise용 컨텐츠 관리](/help/mobile/administer-phonegap.md)

