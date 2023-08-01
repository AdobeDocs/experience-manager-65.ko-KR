---
title: 클라이언트측 사용자 정의
seo-title: Client-side Customization
description: AEM Communities에서 클라이언트측 비헤이비어 또는 모양 사용자 지정
seo-description: Customizing behavior or appearance client-side in AEM Communities
uuid: 57978c39-9a8a-4098-9001-c8bbe7ee786f
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 24b6d1d2-c118-4a25-959f-2783961c4ae3
exl-id: bf34f564-ac93-4c8c-95f7-8690d99d85cb
source-git-commit: c667a1658e43bb5b61daede5f94256dae582a4fc
workflow-type: tm+mt
source-wordcount: '1233'
ht-degree: 0%

---

# 클라이언트측 사용자 정의  {#client-side-customization}

| **[⇐ 기능 기본 사항](essentials.md)** | **[서버측 사용자 지정 ⇒](server-customize.md)** |
|---|---|
|   | **[SCF Handlebars 도우미 ⇒](handlebars-helpers.md)** |

클라이언트측에서 AEM Communities 구성 요소의 모양 및/또는 동작을 사용자 정의하기 위해 몇 가지 접근 방식이 있습니다.

두 가지 주요 접근 방식은 컴포넌트를 오버레이하거나 확장하는 것이다.

[오버레이](#overlays) 구성 요소는 기본 구성 요소를 변경하고 구성 요소에 대한 모든 참조에 영향을 줍니다.

[확장](#extensions) 고유하게 이름이 지정되는 구성 요소는 변경 사항의 범위를 제한합니다. &#39;extend&#39;라는 용어는 &#39;override&#39;와 혼용하여 사용됩니다.

## 오버레이 {#overlays}

구성 요소 오버레이는 기본 구성 요소를 수정하고 기본값을 사용하는 모든 인스턴스에 영향을 주는 방법입니다.

오버레이는 /에서 기본 구성 요소의 복사본을 수정하여 수행됩니다&#x200B;**앱** 디렉토리에서 원래 구성 요소를 수정하지 않고&#x200B;**리브** 디렉토리. 구성 요소는 &#39;libs&#39;를 &#39;apps&#39;로 대체한다는 점을 제외하고 동일한 상대 경로로 구성됩니다.

/apps 디렉토리는 요청을 해결하기 위해 가장 먼저 검색한 위치이며, 찾을 수 없는 경우 /libs 디렉토리에 있는 기본 버전이 사용됩니다.

향후 패치 및 업그레이드를 통해 공용 인터페이스를 유지하는 동안 필요한 방식으로 /libs 디렉토리를 변경할 수 있으므로 /libs 디렉토리의 기본 구성 요소는 수정해서는 안 됩니다.

이 은(는) 과(와) 다릅니다. [확장](#extensions) 특정 용도로 수정하여 구성 요소에 고유한 경로를 만들고 /libs 디렉토리의 원래 기본 구성 요소를 수퍼 리소스 유형으로 참조하려는 기본 구성 요소입니다.

주석 구성 요소를 오버레이하는 간단한 예를 보려면 [오버레이 주석 구성 요소 튜토리얼](overlay-comments.md).

## 확장 {#extensions}

구성 요소를 확장(오버라이드)하는 것은 기본값을 사용하는 모든 인스턴스에 영향을 주지 않고 특정 사용을 위해 수정하는 방법입니다. 확장 구성 요소는 /apps 폴더에서 고유하게 이름이 지정되고 /libs 폴더의 기본 구성 요소를 참조하므로 구성 요소의 기본 디자인과 동작이 수정되지 않습니다.

이 은(는) 과(와) 다릅니다. [오버레이](#overlays) sling의 특성이 libs/ 폴더에서 검색하기 전에 apps/ 폴더에 대한 상대 참조를 확인하는 기본 구성 요소이므로 구성 요소의 디자인이나 동작이 전역적으로 수정됩니다.

주석 구성 요소 확장에 대한 간단한 예를 보려면 [주석 구성 요소 확장 튜토리얼](extend-comments.md).

## JavaScript 바인딩 {#javascript-binding}

구성 요소에 대한 HBS 스크립트는 이 기능을 구현하는 JavaScript 개체, 모델 및 뷰에 바인딩되어야 합니다.

값 `data-scf-component` 속성은 다음과 같은 기본값일 수 있습니다. **`social/tally/components/hbs/rating`**&#x200B;또는 과 같은 사용자 지정된 기능을 위한 확장(사용자 지정된) 구성 요소 **weretail/components/hbs/rating**.

구성 요소를 바인딩하려면 전체 구성 요소 스크립트를 &lt;div> 다음 속성을 가진 요소:

* `data-component-id`=&quot;`{{id}}`&quot;

  은 컨텍스트에서 id 속성으로 확인됩니다.

* `data-scf-component`=&quot;*&lt;resourcetype>*

예: 부터 `/apps/weretail/components/hbs/rating/rating.hbs`:

```xml
<div class="we-Rating" data-component-id="`{{id}}`" data-scf-component="weretail/components/hbs/rating">

     <!-- HTML with HBS accessing the rating component -->

</div>
```

## 사용자 정의 속성 {#custom-properties}

구성 요소를 확장하거나 오버레이할 때 수정된 대화 상자에 속성을 추가할 수 있습니다.

구성 요소/리소스에 설정된 모든 속성은 Handlebars 템플릿의 속성 키를 참조하여 액세스할 수 있습니다.

`{{properties.<property_name>}}`

## CSS 스키닝 {#skinning-css}

색상, 글꼴, 이미지, 단추, 링크, 간격 및 위치를 특정 범위로 변경하는 &#39;스키닝&#39;을 통해 웹 사이트의 전체 테마에 맞게 구성 요소를 사용자 정의할 수 있습니다.

스킨십은 프레임워크 스타일을 선택적으로 오버라이드하거나 완전히 새로운 스타일 시트를 작성함으로써 달성할 수 있습니다. SCF 구성 요소는 구성 요소를 구성하는 다양한 요소에 영향을 주는 네임스페이스와 모듈식 및 시맨틱 CSS 클래스를 정의합니다.

구성 요소 스킨을 수행하려면 다음을 수행합니다.

1. 변경할 요소를 식별합니다(예: 작성기 영역, 도구 모음 단추, 메시지 글꼴 등).
1. 이러한 요소에 영향을 주는 CSS 클래스/규칙을 식별합니다.
1. 스타일 시트 파일(.css)을 만듭니다.
1. 클라이언트 라이브러리 폴더에 스타일시트를 포함합니다([clientlibs](#clientlibs-for-scf))을 클릭하여 검색할 수 있도록 설정하고, 템플릿과 페이지에 [ui:includeClientLib](../../help/sites-developing/clientlibs.md).

1. 스타일 시트에서 식별(#2)한 CSS 클래스와 규칙을 재정의하고 스타일을 추가합니다.

이제 사용자 지정 스타일이 기본 프레임워크 스타일을 재정의하고 구성 요소를 새 스킨으로 렌더링합니다.

>[!CAUTION]
>
>접두사가 있는 모든 CSS 클래스 이름 `scf-js` 는 JavaScript 코드에 특정 용도가 있습니다. 이러한 클래스는 구성 요소의 상태에 영향을 주며(예: 숨김에서 표시로 전환), 재정의하거나 제거해서는 안 됩니다.
>
>동안 `scf-js` 클래스는 스타일에 영향을 주지 않습니다. 클래스 이름은 스타일 시트에서 사용할 수 있으며 요소의 상태를 제어하므로 부작용이 있을 수 있습니다.

## JavaScript 확장 {#extending-javascript}

구성 요소 JavaScript 구현을 확장하려면 다음을 수행해야 합니다.

1. jcr:resourceSuperType이 확장 구성 요소의 jcr:resourceType 값(예: social/forum/components/hbs/forum)으로 설정된 앱용 구성 요소를 만듭니다.
1. 기본 SCF 구성 요소의 JavaScript를 검사하여 SCF.registerComponent()를 사용하여 등록해야 하는 메서드를 결정합니다.
1. 확장 구성 요소의 JavaScript를 복사하거나 처음부터 시작합니다.
1. 메서드를 확장합니다.
1. SCF.registerComponent()를 사용하여 모든 메서드를 기본값 또는 사용자 지정된 개체 및 보기로 등록합니다.

### forum.js: Forum의 샘플 확장 - HBS  {#forum-js-sample-extension-of-forum-hbs}

```xml
(function($CQ, _, Backbone, SCF) {
    "use strict";
    var GMForumView = SCF.ForumView.extend({
        viewName: "GMForum",
        showComposer: function(e) {
            SCF.ForumView.prototype.toggleComposer.apply(this);
            var cancel = this.$el.find('.cancel-new-topic');
            cancel.toggle();
        },
        hideComposer: function(e) {
            SCF.ForumView.prototype.toggleComposer.apply(this);
            var cancel = this.$el.find('.cancel-new-topic');
            cancel.toggle();
        }
    });

    SCF.registerComponent('social/forum/components/hbs/post', SCF.Post, SCF.PostView);
    SCF.registerComponent('social/forum/components/hbs/topic', SCF.Topic, SCF.TopicView);
    SCF.registerComponent('social/forum/components/hbs/forum', SCF.Forum, GMForumView );
})($CQ, _, Backbone, SCF);
```

## 스크립트 태그 {#script-tags}

스크립트 태그는 클라이언트측 프레임워크의 고유한 부분입니다. 서버측에서 생성된 마크업을 클라이언트측의 모델 및 보기와 바인딩하는 데 도움이 되는 접착제입니다.

구성 요소를 오버레이하거나 재정의할 때 SCF 스크립트의 스크립트 태그를 제거해서는 안 됩니다. HTML에 JSON을 삽입하기 위해 자동으로 생성된 SCF 스크립트 태그는 속성으로 식별됩니다 `data-scf-json=true`.

## SCF용 Clientlibs {#clientlibs-for-scf}

사용 [클라이언트측 라이브러리](../../help/sites-developing/clientlibs.md) (clientlibs) 는 클라이언트에서 콘텐츠를 렌더링하는 데 사용되는 JavaScript 및 CSS를 구성하고 최적화하는 수단을 제공합니다.

SCF용 clientlib은 범주 이름에 &#39;작성자&#39;가 있는 경우에만 달라지는 두 변형에 대한 매우 구체적인 이름 지정 패턴을 따릅니다.

| Clientlib 변형 | 카테고리 속성에 대한 패턴 |
|--- |--- |
| clientlib 완료 | cq.social.hbs.&lt;component name> |
| 작성자 clientlib | cq.social.author.hbs.&lt;component name> |

### 전체 Clientlibs {#complete-clientlibs}

전체(작성자가 아닌) clientlib에는 종속성이 포함되어 있으며 ui:includeClientLib에 를 포함하기에 편리합니다.

이들 버전은 다음 위치에 있습니다.

* `/etc/clientlibs/social/hbs/&lt;component name&gt;`

예:

* 클라이언트 폴더 노드: `/etc/clientlibs/social/hbs/forum`
* 범주 속성: `cq.social.hbs.forum`

다음 [커뮤니티 구성 요소 안내서](components-guide.md) 각 SCF 구성 요소에 필요한 전체 clientlib을 나열합니다.

[커뮤니티 구성 요소에 대한 Clientlibs](clientlibs.md) 페이지에 clientlib을 추가하는 방법을 설명합니다.

### 작성자 Clientlibs {#author-clientlibs}

작성자 버전 clientlib은 구성 요소를 구현하는 데 필요한 최소 JavaScript로 제거됩니다.

이러한 clientlib은 직접 포함해서는 안 되며, 대신 사이트에 맞게 수작업으로 제작된 다른 clientlib에 포함할 수 있습니다.

이러한 버전은 SCF libs 폴더에 있습니다.

* `/libs/social/&lt;feature&gt;/components/hbs/&lt;component name&gt;/clientlibs`

예:

* 클라이언트 폴더 노드: `/libs/social/forum/hbs/forum/clientlibs`
* 범주 속성: `cq.social.author.hbs.forum`

참고: 작성자 clientlib은 다른 라이브러리를 포함하지 않지만 해당 종속성을 나열합니다. 다른 라이브러리에 포함되면 종속성이 자동으로 가져오지 않으며 종속성도 포함해야 합니다.

의 각 SCF 구성 요소에 대해 나열된 클라이언트 라이브러리에 &quot;author&quot;를 삽입하여 필요한 작성자 클라이언트 라이브러리를 식별할 수 있습니다. [커뮤니티 구성 요소 안내서](components-guide.md).

### 사용 고려 사항 {#usage-considerations}

모든 사이트는 클라이언트 라이브러리를 관리하는 방식이 다릅니다. 다양한 요인은 다음과 같습니다.

* 전체 속도: 사이트가 응답형 사이트일 수 있지만 첫 번째 페이지를 로드하는 데 약간 느릴 수 있습니다. 많은 페이지가 동일한 JavaScript를 사용하는 경우 다양한 JavaScript를 하나의 clientlib에 임베드하고 첫 번째 페이지에서 참조하여 로드할 수 있습니다. 이 단일 다운로드의 JavaScript는 캐시된 상태로 유지되므로 후속 페이지를 위해 다운로드할 데이터의 양이 최소화됩니다.
* 첫 페이지까지 짧은 시간: 첫 페이지를 빠르게 로드하고자 할 수 있습니다. 이 경우 JavaScript는 필요한 경우에만 참조할 수 있도록 여러 개의 작은 파일에 있습니다.
* 첫 번째 페이지 로드와 이후 다운로드 간의 균형.

| **[⇐ 기능 기본 사항](essentials.md)** | **[서버측 사용자 지정 ⇒](server-customize.md)** |
|---|---|
|   | **[SCF Handlebars 도우미 ⇒](handlebars-helpers.md)** |
