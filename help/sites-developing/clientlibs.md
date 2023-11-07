---
title: 클라이언트측 라이브러리 사용
description: AEM은 클라이언트측 코드를 저장소에 저장하고, 범주로 구성하고, 각 코드 범주가 클라이언트에 제공되는 시기와 방법을 정의할 수 있는 클라이언트측 라이브러리 폴더를 제공합니다
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
docset: aem65
exl-id: 408ac30c-60ab-4d6c-855c-d544af8d5cf9
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '2853'
ht-degree: 2%

---

# 클라이언트측 라이브러리 사용{#using-client-side-libraries}

최신 웹 사이트는 복잡한 JavaScript 및 CSS 코드로 구동되는 클라이언트측 처리에 크게 의존합니다. 이 코드의 제공을 구성하고 최적화하는 것은 복잡한 문제가 될 수 있습니다.

이 문제를 해결하기 위해 AEM은 다음을 제공합니다 **클라이언트 측 라이브러리 폴더**&#x200B;를 사용하면 클라이언트측 코드를 저장소에 저장하고, 카테고리로 구성하고, 각 코드 카테고리가 클라이언트에 제공되는 시기와 방법을 정의할 수 있습니다. 그런 다음 클라이언트 측 라이브러리 시스템은 올바른 코드를 로드하기 위해 최종 웹 페이지에 올바른 링크를 생성합니다.

## AEM에서 클라이언트측 라이브러리 작동 방식 {#how-client-side-libraries-work-in-aem}

페이지의 HTML에 클라이언트측 라이브러리(즉, JS 또는 CSS 파일)를 포함하는 표준 방법은 `<script>` 또는 `<link>` 태그에 포함된 모든 태그(해당 파일에 대한 경로 포함) 예:

```xml
...
<head>
   ...
   <script type="text/javascript" src="/etc/clientlibs/granite/jquery/source/1.8.1/jquery-1.8.1.js"></script>
   ...
</head>
...
```

이 접근 방식은 AEM에서 작동하지만 페이지 및 해당 구성 요소가 복잡해질 때 문제가 발생할 수 있습니다. 이러한 경우 동일한 JS 라이브러리의 여러 복사본이 최종 HTML 출력에 포함될 수 있습니다. 이를 방지하고 AEM이 사용하는 클라이언트측 라이브러리의 논리적 구성을 허용하려면 **클라이언트측 라이브러리 폴더**.

클라이언트측 라이브러리 폴더는 유형의 저장소 노드입니다 `cq:ClientLibraryFolder`. 의 정의입니다 [CND 표기법](https://jackrabbit.apache.org/node-type-notation.html) 은(는)

```shell
[cq:ClientLibraryFolder] > sling:Folder
  - dependencies (string) multiple
  - categories (string) multiple
  - embed (string) multiple
  - channels (string) multiple
```

기본적으로, `cq:ClientLibraryFolder` 노드를 내의 어디에나 배치할 수 있습니다. `/apps`, `/libs` 및 `/etc` 저장소의 하위 트리(이러한 기본값 및 기타 설정은 **Adobe Granite HTML 라이브러리 관리자** 패널 [시스템 콘솔](https://localhost:4502/system/console/configMgr)).

각 `cq:ClientLibraryFolder` 는 몇 개의 지원 파일과 함께 JS 및/또는 CSS 파일 세트로 채워집니다(아래 참조). 의 속성 `cq:ClientLibraryFolder` 는 다음과 같이 구성됩니다.

* `categories`: 이 내에서 JS 및/또는 CSS 파일 세트가 포함되는 범주를 식별합니다. `cq:ClientLibraryFolder` 가을. 다음 `categories` 속성이 다중 값이면 라이브러리 폴더가 두 개 이상의 카테고리에 속할 수 있습니다(이 기능이 유용할 수 있는 방법은 아래 참조).

* `dependencies`: 이 라이브러리 폴더가 종속된 다른 클라이언트 라이브러리 범주 목록입니다. 예를 들어, 다음 두 가지를 고려할 경우 `cq:ClientLibraryFolder` 노드 `F` 및 `G`에 파일이 있는 경우 `F` 에는 다른 파일이 필요합니다. `G` 제대로 작동하려면 다음 중 하나 이상을 `categories` / `G` 다음 중 하나여야 합니다. `dependencies` / `F`.

* `embed`: 다른 라이브러리의 코드를 포함하는 데 사용됩니다. 노드 F가 노드 G 및 H를 임베드하면 결과 HTML은 노드 G 및 H로부터의 콘텐츠의 집중이 될 것이다.
* `allowProxy`: 클라이언트 라이브러리가 아래에 있는 경우 `/apps`, 이 속성을 사용하면 프록시 서블릿을 통해 액세스할 수 있습니다. 다음을 참조하십시오 [클라이언트 라이브러리 폴더 찾기 및 프록시 클라이언트 라이브러리 서블릿 사용](/help/sites-developing/clientlibs.md#locating-a-client-library-folder-and-using-the-proxy-client-libraries-servlet) 아래요.

## 클라이언트측 라이브러리 참조 {#referencing-client-side-libraries}

HTL은 AEM 사이트 개발을 위한 기본 기술이므로 AEM에 클라이언트측 라이브러리를 포함시키는 데 HTL을 사용해야 합니다. 그러나 JSP를 사용하여 그렇게 하는 것도 가능합니다.

### HTL 사용 {#using-htl}

HTL에서 클라이언트 라이브러리는 를 통해 액세스할 수 있는 AEM에서 제공하는 도우미 템플릿을 통해 로드됩니다. [`data-sly-use`](https://helpx.adobe.com/experience-manager/htl/using/block-statements.html#use). 이 파일에는 을 통해 호출할 수 있는 세 가지 템플릿이 있습니다. [`data-sly-call`](https://helpx.adobe.com/experience-manager/htl/using/block-statements.html#template-call):

* **css** - 참조된 클라이언트 라이브러리의 CSS 파일만 로드합니다.
* **js** - 참조된 클라이언트 라이브러리의 JavaScript 파일만 로드합니다.
* **모두** - 참조된 클라이언트 라이브러리의 모든 파일을 로드합니다(CSS 및 JavaScript 모두).

각 도우미 템플릿에는 원하는 클라이언트 라이브러리를 참조하기 위한 `categories` 옵션이 필요합니다. 해당 옵션은 문자열 값의 배열이거나 쉼표로 구분된 값 목록을 포함하는 문자열일 수 있습니다.

자세한 내용 및 사용 예는 문서를 참조하십시오 [HTML 템플릿 언어 시작하기](https://helpx.adobe.com/experience-manager/htl/using/getting-started.html#loading-client-libraries).

### JSP 사용 {#using-jsp}

추가 `ui:includeClientLib` 를 JSP 코드에 태깅하여 생성된 HTML 페이지에서 클라이언트 라이브러리에 대한 링크를 추가합니다. 라이브러리를 참조하려면 의 값을 사용합니다. `categories` 의 속성 `ui:includeClientLib` 노드.

```
<%@taglib prefix="ui" uri="https://www.adobe.com/taglibs/granite/ui/1.0" %>
<ui:includeClientLib categories="<%= categories %>" />
```

예를 들어 `/etc/clientlibs/foundation/jquery` 노드가 유형임 `cq:ClientLibraryFolder` 값의 카테고리 속성 포함 `cq.jquery`. JSP 파일의 다음 코드는 라이브러리를 참조합니다.

```xml
<ui:includeClientLib categories="cq.jquery"/>
```

생성된 HTML 페이지에는 다음 코드가 포함되어 있습니다.

```xml
<script type="text/javascript" src="/etc/clientlibs/foundation/jquery.js"></script>
```

JS, CSS 또는 테마 라이브러리를 필터링하기 위한 속성을 포함한 전체 정보는 [ui:includeClientLib](/help/sites-developing/taglib.md#lt-ui-includeclientlib).

>[!CAUTION]
>
>`<cq:includeClientLib>`과거에는 클라이언트 라이브러리를 포함하는 데 일반적으로 사용되었던 가 AEM 5.6 이후 더 이상 사용되지 않습니다. [`<ui:includeClientLib>`](/help/sites-developing/taglib.md#lt-ui-includeclientlib) 위에 자세히 설명된 대로 대신 를 사용해야 합니다.

## 클라이언트 라이브러리 폴더 만들기 {#creating-client-library-folders}

만들기 `cq:ClientLibraryFolder` 노드를 사용하여 JavaScript 및 CSS(Cascading Style Sheet) 라이브러리를 정의하고 HTML 페이지에서 사용할 수 있습니다. 사용 `categories` 노드가 속한 라이브러리 범주를 식별하기 위한 노드의 속성입니다.

노드에는 런타임 시 단일 JS 및/또는 CSS 파일에 병합되는 하나 이상의 소스 파일이 포함되어 있습니다. 생성된 파일의 이름은 다음 중 하나를 사용하는 노드 이름입니다. `.js` 또는 `.css` 파일 이름 확장명. 예를 들어, 라는 라이브러리 노드가 `cq.jquery` 라는 이름의 생성된 파일이 생성됩니다. `cq.jquery.js` 또는 `cq.jquery.css`.

클라이언트 라이브러리 폴더에는 다음 항목이 포함되어 있습니다.

* 병합할 JS 및/또는 CSS 소스 파일입니다.
* 이미지 파일과 같이 CSS 스타일을 지원하는 리소스입니다.

  **참고:** 하위 폴더를 사용하여 소스 파일을 구성할 수 있습니다.
* 1개 `js.txt` 파일 및/또는 하나 `css.txt` 생성된 JS 및/또는 CSS 파일에서 병합할 소스 파일을 식별하는 파일입니다.

![clientlibarch](assets/clientlibarch.png)

위젯의 클라이언트 라이브러리와 관련된 요구 사항에 대한 자세한 내용은 을 참조하십시오. [위젯 사용 및 확장](/help/sites-developing/widgets.md).

웹 클라이언트에게 액세스 권한이 있어야 함 `cq:ClientLibraryFolder` 노드. 저장소의 보안 영역에서 라이브러리를 노출할 수도 있습니다(아래 다른 라이브러리의 코드 포함 참조).

### /lib에서 라이브러리 재정의 {#overriding-libraries-in-lib}

아래에 있는 클라이언트 라이브러리 폴더 `/apps` 에서 유사한 이름이 같은 폴더보다 우선합니다. `/libs`. 예를 들어, `/apps/cq/ui/widgets` 보다 우선함 `/libs/cq/ui/widgets`. 이러한 라이브러리가 동일한 카테고리에 속하는 경우 아래 라이브러리가 표시됩니다. `/apps` 를 사용합니다.

### 클라이언트 라이브러리 폴더 찾기 및 프록시 클라이언트 라이브러리 서블릿 사용 {#locating-a-client-library-folder-and-using-the-proxy-client-libraries-servlet}

이전 버전에서는 클라이언트 라이브러리 폴더가 아래에 있었습니다 `/etc/clientlibs` 저장소에서 입니다. 이는 여전히 지원되지만 클라이언트 라이브러리는 이제 아래에 있는 것이 좋습니다. `/apps`. 이는 일반적으로 아래에 있는 다른 스크립트 근처에서 클라이언트 라이브러리를 찾기 위한 것입니다 `/apps` 및 `/libs`.

>[!NOTE]
>
>클라이언트 라이브러리 폴더 아래의 정적 리소스는 다음 폴더에 있어야 합니다. *리소스*. 폴더 아래에 이미지와 같은 정적 리소스가 없는 경우 *리소스*&#x200B;게시 인스턴스에서 참조할 수 없습니다. 다음은 예입니다. https://localhost:4503/etc.clientlibs/geometrixx/components/clientlibs/resources/example.gif

>[!NOTE]
>
>콘텐츠 및 구성에서 코드를 보다 잘 분리하려면 `/apps` 다음을 통해 노출 `/etc.clientlibs` 를 사용하여 `allowProxy` 속성.

클라이언트 라이브러리의 경우 `/apps` 액세스하기 위해 프록시 서블릿 이 사용됩니다. ACL은 여전히 클라이언트 라이브러리 폴더에 적용되지만 서블릿을 통해 콘텐츠를 읽을 수 있습니다. `/etc.clientlibs/` 다음과 같은 경우 `allowProxy` 속성이 로 설정되어 있습니다. `true`.

정적 리소스는 클라이언트 라이브러리 폴더 아래의 리소스 아래에 있는 경우 프록시를 통해서만 액세스할 수 있습니다.

예:

* 에 clientlib이 있습니다. `/apps/myproject/clientlibs/foo`
* 에 정적 이미지가 있습니다. `/apps/myprojects/clientlibs/foo/resources/icon.png`

그리고 다음을 설정합니다. `allowProxy` 속성 `foo` true로 설정합니다.

* 그런 다음 을 요청할 수 있습니다. `/etc.clientlibs/myprojects/clientlibs/foo.js`
* 그런 다음 를 통해 이미지를 참조할 수 있습니다. `/etc.clientlibs/myprojects/clientlibs/foo/resources/icon.png`

>[!CAUTION]
>
>프록시화된 클라이언트 라이브러리를 사용할 때 AEM Dispatcher 구성을 업데이트하여 확장 clientlib의 URI가 허용되도록 할 수 있습니다.

>[!CAUTION]
>
>Adobe은 클라이언트 라이브러리를 `/apps` 및 프록시 서블릿을 사용하여 사용할 수 있도록 설정. 그러나 우수 사례를 사용하려면 공용 사이트에 를 통해 직접 제공되는 항목이 포함되어 있지 않아야 합니다. `/apps` 또는 `/libs` 경로.

### 클라이언트 라이브러리 폴더 만들기 {#create-a-client-library-folder}

1. 웹 브라우저에서 CRXDE Lite 열기([https://localhost:4502/crx/de](https://localhost:4502/crx/de)).
1. 클라이언트 라이브러리 폴더를 찾을 폴더를 선택하고 **만들기 > 노드 만들기**.
1. 라이브러리 파일의 이름을 입력하고 유형(Type) 목록에서 `cq:ClientLibraryFolder`. 클릭 **확인** 그런 다음 을 클릭합니다. **모두 저장**.
1. 라이브러리가 속한 범주를 지정하려면 `cq:ClientLibraryFolder` 노드를 클릭하고 다음 속성을 추가한 다음 **모두 저장**:

   * 이름: 카테고리
   * 유형: 문자열
   * 값: 카테고리 이름
   * 다중: 선택

1. 어떤 방법으로든 라이브러리 폴더에 소스 파일을 추가합니다. 예를 들어 WebDav 클라이언트를 사용하여 파일을 복사하거나 파일을 만들고 콘텐츠를 수동으로 작성합니다.

   **참고:** 원하는 경우 하위 폴더에 소스 파일을 구성할 수 있습니다.

1. 클라이언트 라이브러리 폴더를 선택하고 **만들기 > 파일 만들기**.
1. 파일 이름 상자에 다음 파일 이름 중 하나를 입력하고 확인을 클릭합니다.

   * **`js.txt`:** 이 파일 이름을 사용하여 JavaScript 파일을 생성합니다.
   * **`css.txt`:** 이 파일 이름을 사용하여 계단식 스타일 시트를 생성합니다.

1. 파일을 열고 다음 텍스트를 입력하여 소스 파일의 경로 루트를 식별합니다.

   `#base=*[root]*`

   바꾸기 * `[root]`* TXT 파일을 기준으로 소스 파일이 포함된 폴더의 경로 예를 들어 소스 파일이 TXT 파일과 동일한 폴더에 있는 경우 다음 텍스트를 사용합니다.

   `#base=.`

   다음 코드는 루트를 모바일 이라는 폴더 아래에 설정합니다. `cq:ClientLibraryFolder` 노드:

   `#base=mobile`

1. 아래 줄에 표시 `#base=[root]`를 클릭하고 루트를 기준으로 소스 파일의 경로를 입력합니다. 각 파일 이름을 별도의 줄에 지정합니다.
1. **모두 저장**&#x200B;을 클릭합니다.

### 종속성에 연결 {#linking-to-dependencies}

클라이언트 라이브러리 폴더의 코드가 다른 라이브러리를 참조하면 다른 라이브러리를 종속성으로 식별합니다. JSP에서 `ui:includeClientLib` 클라이언트 라이브러리 폴더를 참조하는 태그로 인해 HTML 코드에 생성된 라이브러리 파일에 대한 링크와 종속성이 포함됩니다.

종속성은 다른 항목이어야 합니다. `cq:ClientLibraryFolder`. 종속성을 식별하려면 속성을 `cq:ClientLibraryFolder` 다음 속성을 가진 노드:

* **이름:** 종속성
* **유형:** 문자열[]
* **값:** 현재 라이브러리 폴더가 종속된 cq:ClientLibraryFolder 노드의 categories 속성 값입니다.

예: / `etc/clientlibs/myclientlibs/publicmain` 에 대한 종속성이 있습니다. `cq.jquery` 라이브러리입니다. 주 클라이언트 라이브러리를 참조하는 JSP는 다음 코드를 포함하는 HTML을 생성합니다.

```xml
<script src="/etc/clientlibs/foundation/cq.jquery.js" type="text/javascript">
<script src="/etc/clientlibs/mylibs/publicmain.js" type="text/javascript">
```

### 다른 라이브러리의 코드 포함 {#embedding-code-from-other-libraries}

클라이언트 라이브러리의 코드를 다른 클라이언트 라이브러리에 포함할 수 있습니다. 런타임 시 포함 라이브러리의 생성된 JS 및 CSS 파일은 포함 라이브러리의 코드를 포함합니다.

포함 코드는 저장소의 보안 영역에 저장된 라이브러리에 대한 액세스를 제공하는 데 유용합니다.

#### 앱별 클라이언트 라이브러리 폴더 {#app-specific-client-library-folders}

모든 애플리케이션 관련 파일을 아래의 애플리케이션 폴더에 보관하는 것이 좋습니다. `/apps`. 또한 웹 사이트 방문자가에 대한 액세스를 거부하는 것이 좋습니다. `/apps` 폴더를 삭제합니다. 두 모범 사례를 모두 충족하려면 아래에 클라이언트 라이브러리 폴더를 만듭니다 `/apps`에 설명된 대로 프록시 서블릿을 통해 액세스할 수 있도록 합니다 [클라이언트 라이브러리 폴더 찾기 및 프록시 클라이언트 라이브러리 서블릿 사용](/help/sites-developing/clientlibs.md#locating-a-client-library-folder-and-using-the-proxy-client-libraries-servlet).

포함할 클라이언트 라이브러리 폴더를 식별하려면 categories 속성을 사용합니다. 라이브러리를 포함하려면 포함에 속성을 추가하십시오 `cq:ClientLibraryFolder` 노드, 다음 속성 사용:

* **이름:** 임베드
* **유형:** 문자열[]
* **값:** 의 categories 속성 값 `cq:ClientLibraryFolder` 포함할 노드입니다.

#### 포함을 사용하여 요청 최소화 {#using-embedding-to-minimize-requests}

경우에 따라 게시 인스턴스에 의해 일반 페이지에 대해 생성된 최종 HTML에 비교적 많은 수의 가 포함되어 있을 수 있습니다. `<script>` 요소(특히 사이트에서 분석 또는 타겟팅에 클라이언트 컨텍스트 정보를 사용하는 경우) 예를 들어 최적화되지 않은 프로젝트에서는 다음 시리즈를 찾을 수 있습니다. `<script>` 페이지의 HTML 요소:

```xml
<script type="text/javascript" src="/etc/clientlibs/granite/jquery.js"></script>
<script type="text/javascript" src="/etc/clientlibs/granite/utils.js"></script>
<script type="text/javascript" src="/etc/clientlibs/granite/jquery/granite.js"></script>
<script type="text/javascript" src="/etc/clientlibs/foundation/jquery.js"></script>
<script type="text/javascript" src="/etc/clientlibs/foundation/shared.js"></script>
<script type="text/javascript" src="/etc/clientlibs/foundation/personalization/kernel.js"></script>
```

이러한 경우 페이지 로드 시 앞뒤 요청 수가 줄어들도록 필요한 모든 클라이언트 라이브러리 코드를 단일 파일에 결합하는 것이 유용할 수 있습니다. 이렇게 하려면 다음 작업을 수행할 수 있습니다. `embed` 의 embed 속성을 사용하여 앱별 클라이언트 라이브러리에 필요한 라이브러리 `cq:ClientLibraryFolder` 노드.

AEM에는 다음 클라이언트 라이브러리 범주가 포함됩니다. 특정 사이트의 기능에 필요한 항목만 포함해야 합니다. 그러나 **여기에 나열된 순서를 유지해야 합니다.**:

1. `browsermap.standard`
1. `browsermap`
1. `jquery-ui`
1. `cq.jquery.ui`
1. `personalization`
1. `personalization.core`
1. `personalization.core.kernel`
1. `personalization.clientcontext.kernel`
1. `personalization.stores.kernel`
1. `personalization.kernel`
1. `personalization.clientcontext`
1. `personalization.stores`
1. `cq.collab.comments`
1. `cq.collab.feedlink`
1. `cq.collab.ratings`
1. `cq.collab.toggle`
1. `cq.collab.forum`
1. `cq.cleditor`

#### CSS 파일의 경로 {#paths-in-css-files}

CSS 파일을 포함할 때 생성된 CSS 코드는 포함 라이브러리에 상대적인 리소스에 대한 경로를 사용합니다. 예: 공개적으로 액세스할 수 있는 라이브러리 `/etc/client/libraries/myclientlibs/publicmain` 다음을 포함 `/apps/myapp/clientlib` 클라이언트 라이브러리:

![screen_shot_2012-05-29at20122pm](assets/screen_shot_2012-05-29at20122pm.png)

다음 `main.css` 파일에는 다음 스타일이 포함되어 있습니다.

```xml
body {
  padding: 0;
  margin: 0;
  background: url(images/bg-full.jpg) no-repeat center top;
  width: 100%;
}
```

다음에 해당하는 CSS 파일 `publicmain` 는 원본 이미지의 URL을 사용하여 다음 스타일을 포함합니다.

```xml
body {
  padding: 0;
  margin: 0;
  background: url(../../../apps/myapp/clientlib/styles/images/bg-full.jpg) no-repeat center top;
  width: 100%;
}
```

### 특정 모바일 그룹에 라이브러리 사용 {#using-a-library-for-specific-mobile-groups}

사용 `channels` 라이브러리를 사용하는 모바일 그룹을 식별하기 위한 클라이언트 라이브러리 폴더의 속성입니다. 다음 `channels` 속성은 동일한 카테고리의 라이브러리가 다른 디바이스 기능에 맞게 디자인된 경우 유용합니다.

클라이언트 라이브러리 폴더를 장치 그룹에 연결하려면 속성을 `cq:ClientLibraryFolder` 다음 속성을 가진 노드:

* **이름:** 채널
* **유형:** 문자열[]
* **값:** 모바일 그룹의 이름입니다. 그룹에서 라이브러리 폴더를 제외하려면 이름 앞에 느낌표(&quot;!&quot;)를 붙입니다.

예를 들어 다음 표에는 `channels` 의 각 클라이언트 라이브러리 폴더에 대한 속성 `cq.widgets` 범주:

| 클라이언트 라이브러리 폴더 | 채널 속성 값 |
|---|---|
| `/libs/cq/analytics/widgets` | `!touch` |
| `/libs/cq/analytics/widgets/themes/default` | `!touch` |
| `/libs/cq/cloudserviceconfigs/widgets` | `!touch` |
| `/libs/cq/touch/widgets` | `touch` |
| `/libs/cq/touch/widgets/themes/default` | `touch` |
| `/libs/cq/ui/widgets` | `!touch` |
| `/libs/cq/ui/widgets/themes/default` | `!touch` |

<!-- Search&Promote is end of life as of September 1, 2022 | `/libs/cq/searchpromote/widgets` | `!touch` | -->
<!-- Search&Promote is end of life as of September 1, 2022 | `/libs/cq/searchpromote/widgets/themes/default` |*[no value]* -->

## 전처리기 사용 {#using-preprocessors}

AEM을 통해 플러그 가능한 프로세서 및 [YUI 압축기](https://github.com/yui/yuicompressor#yui-compressor---the-yahoo-javascript-and-css-compressor) CSS 및 JavaScript용 및 [GCC(Google Closure Compiler)](https://developers.google.com/closure/compiler/) YUI가 AEM 기본 전처리기로 설정된 JavaScript용

플러그 가능한 프리프로세서는 다음을 포함하여 유연하게 사용할 수 있습니다.

* 스크립트 소스를 처리할 수 있는 스크립트 프로세서 정의
* 옵션으로 프로세서 구성 가능
* 프로세서는 축소되지 않은 경우에도 사용할 수 있습니다.
* clientlib은 사용할 프로세서를 정의할 수 있습니다

>[!NOTE]
>
>기본적으로 AEM은 YUI Compressor를 사용합니다. 다음을 참조하십시오. [YUI 압축기 GitHub 설명서](https://github.com/yui/yuicompressor/issues) 알려진 문제 목록 특정 클라이언트 라이브러리에 대해 GCC 압축기로 전환하면 YUI 사용 시 관찰되는 몇 가지 문제를 해결할 수 있습니다.

>[!CAUTION]
>
>축소된 라이브러리를 클라이언트 라이브러리에 배치하지 마십시오. 대신 원시 라이브러리를 제공하고, 축소가 필요한 경우 사전 프로세서의 옵션을 사용합니다.

### 사용 {#usage}

클라이언트 라이브러리 또는 시스템 전체에 대해 프로세서 구성을 구성할 수 있습니다.

* 다중 값 속성 추가 `cssProcessor` 및 `jsProcessor` clientlibrary 노드에서

* 또는 다음을 통해 시스템 기본 구성 정의 **HTML 라이브러리 관리자** OSGi 구성

clientlib 노드의 전처리기 구성이 OSGI 구성보다 우선합니다.

### 형식 및 예 {#format-and-examples}

#### 형식 {#format}

```xml
config:= mode ":" processorName options*;
mode:= "default" | "min";
processorName := "none" | <name>;
options := ";" option;
option := name "=" value;
```

#### CSS용 YUI 압축기 축소 및 JS용 GCC {#yui-compressor-for-css-minification-and-gcc-for-js}

```xml
cssProcessor: ["default:none", "min:yui"]
jsProcessor: ["default:none", "min:gcc;compilationLevel=advanced"]
```

#### 사전 처리할 Typescript를 입력한 다음 축소 및 난독화할 GCC {#typescript-to-preprocess-and-then-gcc-to-minify-and-obfuscate}

```xml
jsProcessor: [
   "default:typescript",
   "min:typescript",
   "min:gcc;obfuscate=true"
]
```

#### 추가 GCC 옵션 {#additional-gcc-options}

```xml
failOnWarning (defaults to "false")
languageIn (defaults to "ECMASCRIPT5")
languageOut (defaults to "ECMASCRIPT5")
compilationLevel (defaults to "simple") (can be "whitespace", "simple", "advanced")
```

GCC 옵션에 대한 자세한 내용은 [GCC 설명서](https://developers.google.com/closure/compiler/docs/compilation_levels).

### 시스템 기본 축소기 설정 {#set-system-default-minifier}

AEM에서 YUI가 기본 축소기로 설정됩니다. GCC로 변경하려면 다음 단계를 따르십시오.

1. 의 Apache Felix 구성 관리자로 이동합니다. [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr)
1. 찾기 및 편집 **Adobe Granite HTML 라이브러리 관리자**.
1. 활성화 **축소** 옵션(아직 활성화되지 않은 경우)
1. 값 설정 **JS 프로세서 기본 구성** 끝 `min:gcc`.

   예를 들어 옵션을 세미콜론으로 구분하면 전달할 수 있습니다. `min:gcc;obfuscate=true`.

1. 클릭 **저장** 변경 내용을 저장합니다.

## 디버깅 도구 {#debugging-tools}

AEM은 클라이언트 라이브러리 폴더를 디버깅하고 테스트하기 위한 몇 가지 도구를 제공합니다.

### 임베드된 파일 참조 {#see-embedded-files}

포함된 코드의 원본을 추적하거나 포함된 클라이언트 라이브러리가 예상 결과를 생성하도록 하려면 런타임 시 포함된 파일의 이름을 볼 수 있습니다. 파일 이름을 보려면 `debugClientLibs=true` 매개 변수를 웹 페이지의 URL에 추가합니다. 생성된 라이브러리에는 다음이 포함됩니다. `@import` 포함된 코드 대신 문을 사용하십시오.

앞의 예에서 [다른 라이브러리의 코드 포함](/help/sites-developing/clientlibs.md#embedding-code-from-other-libraries) 섹션, `/etc/client/libraries/myclientlibs/publicmain` 클라이언트 라이브러리 폴더는 `/apps/myapp/clientlib` 클라이언트 라이브러리 폴더입니다. 웹 페이지에 매개 변수를 추가하면 웹 페이지의 소스 코드에 다음과 같은 링크가 만들어집니다.

```xml
<link rel="stylesheet" href="/etc/clientlibs/mycientlibs/publicmain.css">
```

열기 `publicmain.css` 파일에는 다음 코드가 표시됩니다.

```xml
@import url("/apps/myapp/clientlib/styles/main.css");
```

1. 웹 브라우저의 주소 상자에서 HTML URL에 다음 텍스트를 추가합니다.

   `?debugClientLibs=true`
1. 페이지가 로드되면 페이지 소스를 봅니다.
1. 링크 요소에 대해 href로 제공된 링크를 클릭하여 파일을 열고 소스 코드를 봅니다.

### 클라이언트 라이브러리 검색 {#discover-client-libraries}

다음 `/libs/cq/granite/components/dumplibs/dumplibs` 구성 요소는 시스템의 모든 클라이언트 라이브러리 폴더에 대한 정보 페이지를 생성합니다. 다음 `/libs/granite/ui/content/dumplibs` 노드에는 구성 요소가 리소스 유형으로 있습니다. 페이지를 열려면 다음 URL을 사용합니다(필요에 따라 호스트 및 포트 변경).

`https://<host>:<port>/libs/granite/ui/content/dumplibs.test.html`

정보에는 라이브러리 경로 및 유형(CSS 또는 JS)과 라이브러리 속성의 값(예: 범주 및 종속성)이 포함됩니다. 페이지의 후속 테이블에는 각 카테고리 및 채널의 라이브러리가 표시됩니다.

### 생성된 출력 보기 {#see-generated-output}

다음 `dumplibs` 구성 요소에는 용으로 생성된 소스 코드를 표시하는 테스트 선택기가 포함되어 있습니다. `ui:includeClientLib` 태그 사이에 코드를 삽입하지 마십시오. 이 페이지에는 js, css 및 테마 속성의 다양한 조합에 대한 코드가 포함되어 있습니다.

1. 다음 방법 중 하나를 사용하여 테스트 출력 페이지를 엽니다.

   * 다음에서 `dumplibs.html` 페이지에서 **출력 테스트를 위해 여기를 클릭하십시오.** 텍스트를 입력하십시오.

   * 웹 브라우저에서 다음 URL을 엽니다(필요에 따라 다른 호스트 및 포트 사용).

      * `http://<host>:<port>/libs/granite/ui/content/dumplibs.html`

   기본 페이지에는 categories 속성에 대한 값이 없는 태그의 출력이 표시됩니다.

1. 범주에 대한 출력을 보려면 클라이언트 라이브러리의 값을 입력합니다. `categories` 속성 및 클릭 **쿼리 제출**.

## 개발 및 프로덕션을 위한 라이브러리 처리 구성 {#configuring-library-handling-for-development-and-production}

HTML 라이브러리 관리자 서비스 프로세스 `cq:ClientLibraryFolder` 는 런타임 시 라이브러리를 태깅하고 생성합니다. 환경 유형, 개발 또는 프로덕션에 따라 서비스를 구성하는 방법이 결정됩니다.

* 보안 강화: 디버깅 비활성화
* 성능 향상: 공백을 제거하고 라이브러리를 압축합니다.
* 가독성 개선: 공백을 포함하고 압축하지 마십시오.

서비스 구성에 대한 자세한 내용은 [AEM HTML 라이브러리 관리자](/help/sites-deploying/osgi-configuration-settings.md#aemhtmllibrarymanager).
