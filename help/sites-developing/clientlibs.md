---
title: 클라이언트측 라이브러리 사용
seo-title: 클라이언트측 라이브러리 사용
description: AEM은 클라이언트측 라이브러리 폴더를 제공합니다. 이 폴더를 통해 저장소에 클라이언트측 코드를 저장하고, 카테고리로 구성하고, 각 코드 카테고리가 클라이언트에게 제공되는 시기와 방법을 정의할 수 있습니다
seo-description: AEM은 클라이언트측 라이브러리 폴더를 제공합니다. 이 폴더를 통해 저장소에 클라이언트측 코드를 저장하고, 카테고리로 구성하고, 각 코드 카테고리가 클라이언트에게 제공되는 시기와 방법을 정의할 수 있습니다
uuid: f12b13cc-6651-4c9a-9c52-19a22bb82b28
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: 3d14837d-41a8-480a-83ba-392e32f84c65
docset: aem65
translation-type: tm+mt
source-git-commit: 5d33b48000cf607eb77c626ec539280cadab378e
workflow-type: tm+mt
source-wordcount: '2889'
ht-degree: 0%

---


# 클라이언트측 라이브러리 사용{#using-client-side-libraries}

최신 웹 사이트에서는 복잡한 JavaScript 및 CSS 코드를 기반으로 하는 클라이언트측 처리에 크게 의존합니다. 이 코드의 제공을 구성하고 최적화하는 것은 복잡한 문제가 될 수 있습니다.

이 문제를 해결하는 데 도움이 되도록 AEM에서는 **클라이언트측 라이브러리 폴더**&#x200B;를 제공하여 보관소에 클라이언트측 코드를 저장하고, 카테고리로 구성하고, 각 코드 카테고리가 클라이언트에 제공될 시기와 방법을 정의할 수 있습니다. 그러면 클라이언트측 라이브러리 시스템은 최종 웹 페이지에서 올바른 링크를 만들어 올바른 코드를 로드합니다.

## AEM {#how-client-side-libraries-work-in-aem}에서 클라이언트측 라이브러리가 작동하는 방식

페이지의 HTML에 클라이언트측 라이브러리(즉, JS 또는 CSS 파일)를 포함하는 표준 방법은 해당 페이지의 JSP에 `<script>` 또는 `<link>` 태그를 단순히 포함시켜 해당 파일의 경로를 포함하는 것입니다. 예,

```xml
...
<head>
   ...
   <script type="text/javascript" src="/etc/clientlibs/granite/jquery/source/1.8.1/jquery-1.8.1.js"></script>
   ...
</head>
...
```

이 방법은 AEM에서 작동하지만 페이지와 구성 요소가 복잡해질 때 문제가 발생할 수 있습니다. 이러한 경우 동일한 JS 라이브러리의 여러 사본이 최종 HTML 출력에 포함될 수 있습니다. 이를 방지하고 클라이언트측 라이브러리 AEM의 논리적 구성을 허용하려면 **클라이언트측 라이브러리 폴더**&#x200B;를 사용합니다.

클라이언트측 라이브러리 폴더는 `cq:ClientLibraryFolder` 유형의 저장소 노드입니다. [CND 표기법](https://jackrabbit.apache.org/node-type-notation.html)의 정의입니다.

```shell
[cq:ClientLibraryFolder] > sling:Folder
  - dependencies (string) multiple
  - categories (string) multiple
  - embed (string) multiple
  - channels (string) multiple
```

기본적으로 `cq:ClientLibraryFolder` 노드는 `/apps`, `/libs` 및 `/etc` 저장소의 하위 트리(이러한 기본값 및 기타 설정은 [시스템 콘솔](https://localhost:4502/system/console/configMgr)의 **Adobe HTML 라이브러리 관리자** 패널을 통해 제어할 수 있습니다.

각 `cq:ClientLibraryFolder`은 몇 개의 지원 파일과 함께 JS 및/또는 CSS 파일 세트로 채워집니다(아래 참조). `cq:ClientLibraryFolder`의 속성은 다음과 같이 구성됩니다.

* `categories`:이  `cq:ClientLibraryFolder` 가을 내에 JS 및/또는 CSS 파일 세트가 포함되는 카테고리를 식별합니다. 다중 값이 되는 `categories` 속성은 라이브러리 폴더를 두 개 이상의 카테고리에 포함할 수 있도록 합니다(유용할 수 있는 방법은 아래 참조).

* `dependencies`:이 라이브러리 폴더가 종속된 다른 클라이언트 라이브러리 카테고리 목록입니다. 예를 들어, 두 개의 `cq:ClientLibraryFolder` 노드 `F` 및 `G`가 주어지면, `F`의 파일에 제대로 기능하기 위해 `G`의 다른 파일이 필요한 경우, `G`의 `categories` 중 적어도 하나가 `F`의 `dependencies`에 있어야 합니다.

* `embed`:다른 라이브러리의 코드를 임베드하는 데 사용됩니다. 노드 F가 노드 G와 H를 포함하는 경우 결과 HTML은 노드 G 및 H의 컨텐츠가 포함됩니다.
* `allowProxy`:클라이언트 라이브러리가 아래에 있는 경우 이 등록 정보 `/apps`는 프록시 서블릿을 통해 클라이언트 라이브러리에 액세스할 수 있습니다. 아래의 [클라이언트 라이브러리 폴더 찾기 및 프록시 클라이언트 라이브러리 서블릿 사용](/help/sites-developing/clientlibs.md#locating-a-client-library-folder-and-using-the-proxy-client-libraries-servlet)을 참조하십시오.

## 클라이언트측 라이브러리 참조 {#referencing-client-side-libraries}

HTL은 AEM 사이트 개발을 위해 선호되는 기술이므로 AEM에 클라이언트측 라이브러리를 포함하는 데 HTL을 사용해야 합니다. 그러나 JSP를 사용하여 수행할 수도 있습니다.

### HTL {#using-htl} 사용

HTL에서 클라이언트 라이브러리는 AEM에서 제공하는 도우미 템플릿을 통해 로드되며, 이 템플릿은 [ `data-sly-use`](https://helpx.adobe.com/experience-manager/htl/using/block-statements.html#use)를 통해 액세스할 수 있습니다. 이 파일에서 사용할 수 있는 세 가지 템플릿은 [ `data-sly-call`](https://helpx.adobe.com/experience-manager/htl/using/block-statements.html#template-call)를 통해 호출할 수 있습니다.

* **css**  - 참조된 클라이언트 라이브러리의 CSS 파일만 로드합니다.
* **js**  - 참조된 클라이언트 라이브러리의 JavaScript 파일만 로드합니다.
* **all**  - 참조된 클라이언트 라이브러리의 모든 파일(CSS와 JavaScript 모두)을 로드합니다.

각 헬퍼 템플릿에는 원하는 클라이언트 라이브러리를 참조하는 `categories` 옵션이 필요합니다. 이 옵션은 문자열 값의 배열 또는 쉼표로 구분된 값 목록을 포함하는 문자열일 수 있습니다.

자세한 내용 및 사용 예는 [HTML 템플릿 언어 시작하기](https://helpx.adobe.com/experience-manager/htl/using/getting-started.html#loading-client-libraries) 문서를 참조하십시오.

### JSP {#using-jsp} 사용

생성된 HTML 페이지의 클라이언트 라이브러리에 링크를 추가하려면 JSP 코드에 `ui:includeClientLib` 태그를 추가합니다. 라이브러리를 참조하려면 `ui:includeClientLib` 노드의 `categories` 속성 값을 사용합니다.

```
<%@taglib prefix="ui" uri="https://www.adobe.com/taglibs/granite/ui/1.0" %>
<ui:includeClientLib categories="<%= categories %>" />
```

예를 들어 `/etc/clientlibs/foundation/jquery` 노드는 값 `cq.jquery`의 카테고리 속성을 가진 `cq:ClientLibraryFolder` 유형입니다. JSP 파일의 다음 코드가 라이브러리를 참조합니다.

```xml
<ui:includeClientLib categories="cq.jquery"/>
```

생성된 HTML 페이지에는 다음 코드가 포함되어 있습니다.

```xml
<script type="text/javascript" src="/etc/clientlibs/foundation/jquery.js"></script>
```

JS, CSS 또는 테마 라이브러리 필터링을 위한 특성을 비롯한 자세한 내용은 [ui:includeClientLib](/help/sites-developing/taglib.md#lt-ui-includeclientlib)을 참조하십시오.

>[!CAUTION]
>
>`<cq:includeClientLib>`이전에는 클라이언트 라이브러리를 포함하는 데 일반적으로 사용되던 이 값은 AEM 5.6부터 더 이상 사용되지 않습니다. 대신 위에 설명한 대로  [ `<ui:includeClientLib>`](/help/sites-developing/taglib.md#lt-ui-includeclientlib) 사용해야 합니다.

## 클라이언트 라이브러리 폴더 만들기 {#creating-client-library-folders}

`cq:ClientLibraryFolder` 노드를 만들어 JavaScript 및 CSS 스타일 시트 라이브러리를 정의하고 HTML 페이지에서 사용할 수 있도록 합니다. 노드의 `categories` 속성을 사용하여 해당 노드가 속하는 라이브러리 범주를 식별합니다.

노드에는 런타임에 단일 JS 및/또는 CSS 파일로 병합되는 하나 이상의 소스 파일이 포함되어 있습니다. 생성된 파일의 이름은 `.js` 또는 `.css` 파일 이름 확장자를 가진 노드 이름입니다. 예를 들어, `cq.jquery`이라는 라이브러리 노드는 생성된 파일 `cq.jquery.js` 또는 `cq.jquery.css`를 생성합니다.

클라이언트 라이브러리 폴더에는 다음 항목이 포함됩니다.

* 병합할 JS 및/또는 CSS 소스 파일입니다.
* 이미지 파일과 같은 CSS 스타일을 지원하는 리소스입니다.

   **참고:** 하위 폴더를 사용하여 소스 파일을 구성할 수 있습니다.
* 생성된 JS 및/또는 CSS 파일에서 병합할 소스 파일을 식별하는 하나의 `js.txt` 파일 및/또는 하나의 `css.txt` 파일

![clientlibarch](assets/clientlibarch.png)

위젯의 클라이언트 라이브러리와 관련된 요구 사항에 대한 자세한 내용은 [위젯 사용 및 확장](/help/sites-developing/widgets.md)을 참조하십시오.

웹 클라이언트에 `cq:ClientLibraryFolder` 노드에 액세스할 수 있는 권한이 있어야 합니다. 저장소의 보안 영역에서 라이브러리를 표시할 수도 있습니다(아래 다른 라이브러리의 코드 포함 참조).

### /lib {#overriding-libraries-in-lib}에서 라이브러리 재정의

`/apps` 아래에 있는 클라이언트 라이브러리 폴더는 `/libs`에 유사하게 위치한 동일한 이름의 폴더보다 우선합니다. 예를 들어 `/apps/cq/ui/widgets`은 `/libs/cq/ui/widgets`보다 우선합니다. 이러한 라이브러리가 동일한 범주에 속하면 `/apps` 아래 라이브러리가 사용됩니다.

### 클라이언트 라이브러리 폴더 찾기 및 프록시 클라이언트 라이브러리 서블릿 사용 {#locating-a-client-library-folder-and-using-the-proxy-client-libraries-servlet}

이전 버전에서는 클라이언트 라이브러리 폴더가 저장소의 `/etc/clientlibs` 아래에 있었습니다. 이 기능은 여전히 지원되지만 클라이언트 라이브러리가 `/apps` 아래에 있는 것이 좋습니다. 다른 스크립트 근처에 있는 클라이언트 라이브러리를 찾기 위한 것으로, 일반적으로 `/apps` 및 `/libs` 아래에 있습니다.

>[!NOTE]
>
>클라이언트 라이브러리 폴더 아래의 정적 리소스는 *resources*&#x200B;이라는 폴더에 있어야 합니다. 이미지와 같은 정적 리소스를 폴더 *resources*&#x200B;에서 사용하지 않으면 게시 인스턴스에서 참조할 수 없습니다. 다음은 한 예입니다.https://localhost:4503/etc.clientlibs/geometrixx/components/clientlibs/resources/example.gif

>[!NOTE]
>
>컨텐츠 및 구성에서 코드를 보다 잘 격리하기 위해 `/apps` 아래에서 클라이언트 라이브러리를 찾아 `/etc.clientlibs` 속성을 활용하여 노출하는 것이 좋습니다.`allowProxy`

`/apps` 아래의 클라이언트 라이브러리에 액세스하려면 프록시 서버가 사용됩니다. ACL은 클라이언트 라이브러리 폴더에 계속 적용되지만 `allowProxy` 속성이 `true`로 설정된 경우 서블릿은 `/etc.clientlibs/`을 통해 컨텐츠를 읽을 수 있도록 허용합니다.

정적 리소스는 클라이언트 라이브러리 폴더 아래의 리소스 아래에 있는 경우에만 프록시를 통해 액세스할 수 있습니다.

예:

* `/apps/myproject/clientlibs/foo`에 clientlib이 있습니다.
* `/apps/myprojects/clientlibs/foo/resources/icon.png`에 정적 이미지가 있습니다.

그런 다음 `foo`의 `allowProxy` 속성을 true로 설정합니다.

* 그런 다음 `/etc.clientlibs/myprojects/clientlibs/foo.js`을(를) 요청할 수 있습니다.
* 그런 다음 `/etc.clientlibs/myprojects/clientlibs/foo/resources/icon.png`을 통해 이미지를 참조할 수 있습니다

>[!CAUTION]
>
>프록시 클라이언트 라이브러리를 사용하는 경우 AEM Dispatcher 구성을 사용하려면 Extension clientlibs가 있는 URI가 허용되도록 업데이트해야 할 수 있습니다.

>[!CAUTION]
>
>Adobe은 `/apps` 아래에 있는 클라이언트 라이브러리를 찾아 프록시 서블릿을 사용하여 사용할 수 있도록 하는 것이 좋습니다. 그러나 공용 사이트에는 `/apps` 또는 `/libs` 경로 위에 직접 제공되는 항목이 포함되지 않아야 하는 것이 좋습니다.

### 클라이언트 라이브러리 폴더 {#create-a-client-library-folder} 만들기

1. 웹 브라우저에서 CRXDE Lite을 엽니다([https://localhost:4502/crx/de](https://localhost:4502/crx/de)).
1. 클라이언트 라이브러리 폴더를 찾을 폴더를 선택하고 **만들기 > 노드 만들기**&#x200B;를 클릭합니다.
1. 라이브러리 파일의 이름을 입력하고 유형 목록에서 `cq:ClientLibraryFolder`을 선택합니다. **확인**&#x200B;을 클릭한 다음 **모두 저장**&#x200B;을 클릭합니다.
1. 라이브러리가 속한 카테고리 또는 범주를 지정하려면 `cq:ClientLibraryFolder` 노드를 선택하고 다음 속성을 추가한 다음 **모두 저장**&#x200B;을 클릭합니다.

   * 이름:카테고리
   * 유형:문자열
   * 값:범주 이름
   * 다중:선택

1. 어떤 방법으로든 라이브러리 폴더에 소스 파일을 추가합니다. 예를 들어 WebDav 클라이언트를 사용하여 파일을 복사하거나 파일을 만들고 컨텐츠를 수동으로 작성합니다.

   **참고:** 원하는 경우 하위 폴더에서 소스 파일을 구성할 수 있습니다.

1. 클라이언트 라이브러리 폴더를 선택하고 **만들기 > 파일 만들기**&#x200B;를 클릭합니다.
1. 파일 이름 상자에 다음 파일 이름 중 하나를 입력하고 확인을 클릭합니다.

   * **`js.txt`:** 이 파일 이름을 사용하여 JavaScript 파일을 생성합니다.
   * **`css.txt`:** 이 파일 이름을 사용하여 계단식 스타일 시트를 생성합니다.

1. 파일을 열고 다음 텍스트를 입력하여 소스 파일 경로의 루트를 확인합니다.

   `#base=*[root]*`

   * `[root]`*를 TXT 파일의 상대 소스 파일이 포함된 폴더 경로로 바꿉니다. 예를 들어 소스 파일이 TXT 파일과 동일한 폴더에 있는 경우 다음 텍스트를 사용합니다.

   `#base=.`

   다음 코드는 루트를 `cq:ClientLibraryFolder` 노드 아래에 mobile이라는 폴더로 설정합니다.

   `#base=mobile`

1. `#base=[root]` 아래의 줄에 루트에 상대적인 소스 파일의 경로를 입력합니다. 각 파일 이름을 별도의 줄에 배치합니다.
1. **모두 저장**&#x200B;을 클릭합니다.

### 종속성 {#linking-to-dependencies}에 연결

클라이언트 라이브러리 폴더의 코드가 다른 라이브러리를 참조하면 다른 라이브러리를 종속성으로 식별합니다. JSP에서 클라이언트 라이브러리 폴더를 참조하는 `ui:includeClientLib` 태그로 인해 HTML 코드가 생성된 라이브러리 파일에 대한 링크 및 종속성을 포함하도록 됩니다.

종속성은 다른 `cq:ClientLibraryFolder`이어야 합니다. 종속성을 식별하려면 다음 특성을 사용하여 `cq:ClientLibraryFolder` 노드에 속성을 추가하십시오.

* **이름:** 종속성
* **유형:** 문자열[]
* **값:** 현재 라이브러리 폴더가 종속된 cq:ClientLibraryFolder 노드의 categories 속성 값입니다.

예를 들어 / `etc/clientlibs/myclientlibs/publicmain`은 `cq.jquery` 라이브러리에 대한 종속성을 갖습니다. 기본 클라이언트 라이브러리를 참조하는 JSP는 다음 코드를 포함하는 HTML을 생성합니다.

```xml
<script src="/etc/clientlibs/foundation/cq.jquery.js" type="text/javascript">
<script src="/etc/clientlibs/mylibs/publicmain.js" type="text/javascript">
```

### 다른 라이브러리의 코드 포함 {#embedding-code-from-other-libraries}

클라이언트 라이브러리의 코드를 다른 클라이언트 라이브러리에 포함할 수 있습니다. 런타임 시 임베드 라이브러리의 생성된 JS 및 CSS 파일에는 임베드 라이브러리의 코드가 포함되어 있습니다.

포함 코드는 저장소의 보안 영역에 저장된 라이브러리에 대한 액세스를 제공하는 데 유용합니다.

#### 앱별 클라이언트 라이브러리 폴더 {#app-specific-client-library-folders}

모든 응용 프로그램 관련 파일을 응용 프로그램 폴더에 `/app` 아래로 유지하는 것이 좋습니다. 또한 `/app` 폴더에 대한 웹 사이트 방문자의 액세스를 거부하는 것이 좋습니다. 두 가지 모범 사례를 모두 충족하려면 `/app` 아래에 있는 클라이언트 라이브러리를 포함하는 `/etc` 폴더 아래에 클라이언트 라이브러리 폴더를 만드십시오.

categories 속성을 사용하여 포함할 클라이언트 라이브러리 폴더를 식별합니다. 라이브러리를 포함하려면 다음 속성 속성을 사용하여 포함 `cq:ClientLibraryFolder` 노드에 속성을 추가합니다.

* **이름:** 포함
* **유형:** 문자열[]
* **값:** 포함할  `cq:ClientLibraryFolder` 노드의 categories 속성 값.

#### 포함 기능을 사용하여 요청 최소화 {#using-embedding-to-minimize-requests}

경우에 따라 게시 인스턴스에서 일반적인 페이지에 대해 생성된 최종 HTML에 비교적 많은 `<script>` 요소가 포함되어 있습니다. 특히 사이트에서 분석 또는 타깃팅을 위해 클라이언트 컨텍스트 정보를 사용하고 있는 경우입니다. 예를 들어, 최적화되지 않은 프로젝트에서는 페이지에 대한 HTML에서 다음 일련의 `<script>` 요소를 찾을 수 있습니다.

```xml
<script type="text/javascript" src="/etc/clientlibs/granite/jquery.js"></script>
<script type="text/javascript" src="/etc/clientlibs/granite/utils.js"></script>
<script type="text/javascript" src="/etc/clientlibs/granite/jquery/granite.js"></script>
<script type="text/javascript" src="/etc/clientlibs/foundation/jquery.js"></script>
<script type="text/javascript" src="/etc/clientlibs/foundation/shared.js"></script>
<script type="text/javascript" src="/etc/clientlibs/foundation/personalization/kernel.js"></script>
```

이러한 경우 필요한 모든 클라이언트 라이브러리 코드를 하나의 파일로 결합하여 페이지 로드 시 요청이 오고 나가는 횟수를 줄이는 것이 유용할 수 있습니다. 이 작업을 수행하려면 `embed` 노드의 embed 속성을 사용하여 필요한 라이브러리를 앱별 클라이언트 라이브러리에 포함할 수 있습니다.`cq:ClientLibraryFolder`

다음 클라이언트 라이브러리 카테고리는 AEM에 포함됩니다. 특정 사이트의 기능에 필요한 것만 포함해야 합니다. 그러나 **여기에 나열된 순서를 유지해야 합니다**.

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

CSS 파일을 포함할 때 생성된 CSS 코드는 포함 라이브러리에 상대적인 리소스에 대한 경로를 사용합니다. 예를 들어 공개적으로 액세스할 수 있는 라이브러리 `/etc/client/libraries/myclientlibs/publicmain`은 `/apps/myapp/clientlib` 클라이언트 라이브러리를 포함합니다.

![screen_shot_2012-05-29at20122pm](assets/screen_shot_2012-05-29at20122pm.png)

`main.css` 파일에는 다음 스타일이 포함되어 있습니다.

```xml
body {
  padding: 0;
  margin: 0;
  background: url(images/bg-full.jpg) no-repeat center top;
  width: 100%;
}
```

`publicmain` 노드가 생성하는 CSS 파일은 원본 이미지의 URL을 사용하여 다음 스타일을 포함합니다.

```xml
body {
  padding: 0;
  margin: 0;
  background: url(../../../apps/myapp/clientlib/styles/images/bg-full.jpg) no-repeat center top;
  width: 100%;
}
```

### 특정 모바일 그룹용 라이브러리 사용 {#using-a-library-for-specific-mobile-groups}

클라이언트 라이브러리 폴더의 `channels` 속성을 사용하여 라이브러리를 사용하는 모바일 그룹을 식별합니다. `channels` 속성은 같은 범주의 라이브러리가 다른 장치 기능에 대해 디자인된 경우에 유용합니다.

클라이언트 라이브러리 폴더를 장치 그룹과 연결하려면 다음 특성을 사용하여 `cq:ClientLibraryFolder` 노드에 속성을 추가하십시오.

* **이름:** 채널
* **유형:** 문자열[]
* **값:** 모바일 그룹의 이름입니다. 그룹에서 라이브러리 폴더를 제외하려면 이름에 느낌표(&quot;!&quot;)를 붙입니다.

예를 들어 다음 표에는 `cq.widgets` 범주의 각 클라이언트 라이브러리 폴더에 대한 `channels` 속성의 값이 나와 있습니다.

| 클라이언트 라이브러리 폴더 | 채널 속성 값 |
|---|---|
| `/libs/cq/analytics/widgets` | `!touch` |
| `/libs/cq/analytics/widgets/themes/default` | `!touch` |
| `/libs/cq/cloudserviceconfigs/widgets` | `!touch` |
| `/libs/cq/searchpromote/widgets` | `!touch` |
| `/libs/cq/searchpromote/widgets/themes/default` | *[값 없음]* |
| `/libs/cq/touch/widgets` | `touch` |
| `/libs/cq/touch/widgets/themes/default` | `touch` |
| `/libs/cq/ui/widgets` | `!touch` |
| `/libs/cq/ui/widgets/themes/default` | `!touch` |

## 프리프로세서 {#using-preprocessors} 사용

AEM에서는 플러그형 프리프로세서를 지원하고 CSS 및 JavaScript용 [YUI 압축기](https://github.com/yui/yuicompressor#yui-compressor---the-yahoo-javascript-and-css-compressor) 및 AEM 기본 프리프로세서로 설정된 JavaScript용 [Google Closure Compiler(GCC)](https://developers.google.com/closure/compiler/)에 대한 지원을 제공합니다.

플러그형 프리프로세서를 통해 다음을 비롯한 유연한 사용 가능

* 스크립트 소스를 처리할 수 있는 스크립트 프로세서 정의
* 프로세서는 옵션을 사용하여 구성할 수 있습니다.
* 프로세서는 소정에 사용할 수 있지만, 축소 가능한 경우도 사용할 수 있습니다
* clientlib은 사용할 프로세서를 정의할 수 있습니다.

>[!NOTE]
>
>기본적으로 AEM은 YUI 압축기를 사용합니다. 알려진 문제 목록은 [YUI Compressor GitHub 설명서](https://github.com/yui/yuicompressor/issues)를 참조하십시오. 특정 클라이언트용 GCC 압축기로 전환하면 YUI를 사용할 때 발생하는 몇 가지 문제를 해결할 수 있습니다.

>[!CAUTION]
>
>클라이언트 라이브러리에 축소 라이브러리를 배치하지 마십시오. 대신 원시 라이브러리를 제공하고, 인증이 필요한 경우 프리프로세서의 옵션을 사용하십시오.

### 사용량 {#usage}

클라이언트 라이브러리 또는 시스템 전체에 대해 프리프로세서 구성을 구성할 수 있습니다.

* clientlibrary 노드에서 다중 값 속성 `cssProcessor` 및 `jsProcessor`을 추가합니다.

* 또는 **HTML 라이브러리 관리자** OSGi 구성을 통해 시스템 기본 구성을 정의합니다.

clientlib 노드의 프리프로세서 구성이 OSGI 구성에 우선합니다.

### 형식 및 예 {#format-and-examples}

#### 형식 {#format}

```xml
config:= mode ":" processorName options*;
mode:= "default" | "min";
processorName := "none" | <name>;
options := ";" option;
option := name "=" value;
```

#### JS {#yui-compressor-for-css-minification-and-gcc-for-js}용 CSS 미니폴리션을 위한 YUI 압축기

```xml
cssProcessor: ["default:none", "min:yui"]
jsProcessor: ["default:none", "min:gcc;compilationLevel=advanced"]
```

#### Typescript를 Preprocess로 변환한 다음 GCC에서 {#typescript-to-preprocess-and-then-gcc-to-minify-and-obfuscate} 축소 및 난독화

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

GCC 옵션에 대한 자세한 내용은 [GCC 설명서](https://developers.google.com/closure/compiler/docs/compilation_levels)를 참조하십시오.

### 시스템 기본 미니표시자 {#set-system-default-minifier} 설정

AEM에서 YUI가 기본 미니피자로 설정됩니다. GCC로 변경하려면 다음 단계를 따르십시오.

1. [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr)에서 Apache Felix Config Manager로 이동
1. **Adobe Granite HTML 라이브러리 관리자**&#x200B;를 찾아 편집합니다.
1. **Minify** 옵션(아직 활성화되지 않은 경우)을 활성화합니다.
1. 값 **JS 프로세서 기본 구성**&#x200B;을 `min:gcc`로 설정합니다.

   세미콜론(예:)으로 구분하면 옵션을 전달할 수 있습니다.`min:gcc;obfuscate=true`.

1. **저장**&#x200B;을 클릭하여 변경 내용을 저장합니다.

## 디버깅 도구 {#debugging-tools}

AEM은 클라이언트 라이브러리 폴더를 디버깅하고 테스트하는 몇 가지 도구를 제공합니다.

### 포함된 파일 {#see-embedded-files} 참조

포함된 코드의 원본을 추적하거나 포함된 클라이언트 라이브러리가 예상 결과를 생성하는지 확인하기 위해 런타임 시 포함 중인 파일의 이름을 볼 수 있습니다. 파일 이름을 보려면 `debugClientLibs=true` 매개 변수를 웹 페이지의 URL에 추가하십시오. 생성된 라이브러리에는 포함된 코드 대신 `@import` 문이 포함되어 있습니다.

이전 [다른 라이브러리의 코드 포함](/help/sites-developing/clientlibs.md#embedding-code-from-other-libraries) 섹션의 예에서 `/etc/client/libraries/myclientlibs/publicmain` 클라이언트 라이브러리 폴더에 `/apps/myapp/clientlib` 클라이언트 라이브러리 폴더가 포함됩니다. 웹 페이지에 매개 변수를 추가하면 웹 페이지의 소스 코드에 다음 링크가 만들어집니다.

```xml
<link rel="stylesheet" href="/etc/clientlibs/mycientlibs/publicmain.css">
```

`publicmain.css` 파일을 열면 다음 코드가 표시됩니다.

```xml
@import url("/apps/myapp/clientlib/styles/main.css");
```

1. 웹 브라우저의 주소 상자에서 HTML의 URL에 다음 텍스트를 추가합니다.

   `?debugClientLibs=true`
1. 페이지가 로드되면 페이지 소스를 봅니다.
1. 파일을 열고 소스 코드를 보기 위해 링크 요소의 href로 제공되는 링크를 클릭합니다.

### Discover 클라이언트 라이브러리 {#discover-client-libraries}

`/libs/cq/granite/components/dumplibs/dumplibs` 구성 요소는 시스템의 모든 클라이언트 라이브러리 폴더에 대한 정보 페이지를 생성합니다. `/libs/granite/ui/content/dumplibs` 노드에는 구성 요소가 리소스 유형으로 있습니다. 페이지를 열려면 다음 URL을 사용합니다(필요에 따라 호스트 및 포트 변경).

`https://<host>:<port>/libs/granite/ui/content/dumplibs.test.html`

이 정보에는 라이브러리 경로 및 유형(CSS 또는 JS)과 범주 및 종속성 등의 라이브러리 속성 값이 포함됩니다. 페이지의 다음 표는 각 카테고리와 채널의 라이브러리를 보여줍니다.

### 생성된 출력 참조 {#see-generated-output}

`dumplibs` 구성 요소에는 `ui:includeClientLib` 태그에 대해 생성된 소스 코드를 표시하는 테스트 선택기가 포함되어 있습니다. 이 페이지에는 js, css 및 테마 속성의 다양한 조합을 위한 코드가 포함되어 있습니다.

1. 다음 방법 중 하나를 사용하여 [테스트 출력] 페이지를 엽니다.

   * `dumplibs.html` 페이지에서 출력 테스트&#x200B;**텍스트를 보려면**&#x200B;여기를 클릭하십시오.

   * 웹 브라우저에서 다음 URL을 엽니다(필요에 따라 다른 호스트 및 포트 사용).

      * `http://<host>:<port>/libs/granite/ui/content/dumplibs.html`

   기본 페이지에는 categories 속성에 대한 값이 없는 태그에 대한 출력이 표시됩니다.

1. 범주에 대한 출력을 보려면 클라이언트 라이브러리의 `categories` 속성 값을 입력하고 **Submit Query**&#x200B;를 클릭합니다.

## 개발 및 프로덕션에 대한 라이브러리 처리 구성 {#configuring-library-handling-for-development-and-production}

HTML 라이브러리 관리자 서비스는 `cq:ClientLibraryFolder` 태그를 처리하고 런타임에 라이브러리를 생성합니다. 환경, 개발 또는 제작의 유형에 따라 서비스를 구성하는 방법이 결정됩니다.

* 보안 강화:디버깅 사용 안 함
* 성능 향상:공백을 제거하고 라이브러리를 압축합니다.
* 가독성 향상:공백을 포함하고 압축하지 않습니다.

서비스 구성에 대한 자세한 내용은 [AEM HTML 라이브러리 관리자](/help/sites-deploying/osgi-configuration-settings.md#aemhtmllibrarymanager)를 참조하십시오.
