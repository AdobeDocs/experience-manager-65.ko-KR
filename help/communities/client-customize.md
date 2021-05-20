---
title: 클라이언트측 사용자 지정
seo-title: 클라이언트측 사용자 지정
description: AEM Communities에서 동작 또는 모양 클라이언트측 사용자 지정
seo-description: AEM Communities에서 동작 또는 모양 클라이언트측 사용자 지정
uuid: 57978c39-9a8a-4098-9001-c8bbe7ee786f
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 24b6d1d2-c118-4a25-959f-2783961c4ae3
exl-id: bf34f564-ac93-4c8c-95f7-8690d99d85cb
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1239'
ht-degree: 0%

---

# 클라이언트측 사용자 지정 {#client-side-customization}

| **[⇐ 기능 핵심 사항](essentials.md)** | **[서버 측 사용자 지정 ⇒](server-customize.md)** |
|---|---|
|  | **[SCF Handlebars Helpers ⇒](handlebars-helpers.md)** |

클라이언트측에서 AEM Communities 구성 요소의 모양 및/또는 동작을 사용자 지정하기 위해 몇 가지 방법이 있습니다.

두 가지 주요 접근 방식은 구성 요소를 오버레이하거나 확장하는 것입니다.

[](#overlays) 구성 요소를 오버레이하면 기본 구성 요소가 변경되고 구성 요소에 대한 모든 참조에 영향을 줍니다.

[](#extensions) 구성 요소를 고유하게 명명하고 이름을 바꾸면 변경 범위가 제한됩니다. &#39;extend&#39;라는 용어는 &#39;override&#39;와 교환적으로 사용됩니다.

## 오버레이 {#overlays}

구성 요소 오버레이는 기본 구성 요소를 수정하고 기본값을 사용하는 모든 인스턴스에 영향을 주는 방법입니다.

오버레이는 /**libs** 디렉토리에서 원래 구성 요소를 수정하지 않고 /**apps** 디렉토리에서 기본 구성 요소의 사본을 수정하여 수행됩니다. 구성 요소는 &#39;libs&#39;가 &#39;apps&#39;로 대체된다는 점을 제외하면 동일한 상대 경로로 구성됩니다.

/apps 디렉토리는 요청을 해결하기 위해 검색된 첫 번째 지점이며 찾을 수 없으면 /libs 디렉토리에 있는 기본 버전이 사용됩니다.

공용 인터페이스를 유지 관리하는 동안 필요한 방식으로 /libs 디렉토리를 변경할 수 있도록 향후 패치 및 업그레이드가 가능하므로 /libs 디렉토리에 있는 기본 구성 요소를 수정할 수 없습니다.

이는 특정 사용을 위해 수정해야 하는 기본 구성 요소인 [확장](#extensions)과 다르며, 구성 요소에 고유한 경로를 만들고 /libs 디렉토리의 원래 기본 구성 요소를 슈퍼 리소스 유형으로 참조하는 것에 의존합니다.

주석 구성 요소를 오버레이하는 빠른 예를 보려면 [오버레이 댓글 구성 요소 자습서](overlay-comments.md)를 사용해 보십시오.

## 확장 {#extensions}

구성 요소를 확장(재정의)하는 것은 기본값을 사용하는 모든 인스턴스에 영향을 주지 않고 특정 사용을 위해 수정하는 방법입니다. 확장 구성 요소는 /apps 폴더에서 고유하게 이름을 지정하고 /libs 폴더에서 기본 구성 요소를 참조하므로 구성 요소의 기본 디자인 및 동작이 수정되지 않습니다.

이는 [오버레이](#overlays)와는 다릅니다. 여기서 Sling의 특성은 libs/ 폴더에서 검색하기 전에 apps/ 폴더에 대한 상대 참조를 확인하므로 구성 요소의 디자인이나 동작이 전체적으로 수정됩니다.

주석 구성 요소를 확장하는 빠른 예를 보려면 [주석 구성 요소 확장 자습서](extend-comments.md)를 사용해 보십시오.

## Javascript 바인딩 {#javascript-binding}

구성 요소에 대한 HBS 스크립트는 이 기능을 구현하는 JavaScript 개체, 모델 및 보기에 바인딩되어야 합니다.

`data-scf-component` 속성의 값은 **`social/tally/components/hbs/rating`** 또는 **weretail/components/hbs/rating**&#x200B;과 같은 사용자 지정된 기능을 위한 확장(사용자 지정) 구성 요소일 수 있습니다.

구성 요소를 바인딩하려면 전체 구성 요소 스크립트를 &lt;div> 요소 내에 다음 속성으로 묶어야 합니다.

* `data-component-id`=&quot;{{id}}&quot;

   컨텍스트의 id 속성으로 확인됩니다.

* `data-scf-component`=&quot;*&lt;resourcetype>*

예를 들어 `/apps/weretail/components/hbs/rating/rating.hbs`에서:

```xml
<div class="we-Rating" data-component-id="{{id}}" data-scf-component="weretail/components/hbs/rating">

     <!-- HTML with HBS accessing the rating component -->

</div>
```

## 사용자 정의 속성 {#custom-properties}

구성 요소를 확장하거나 오버레이할 때 수정된 대화 상자에 속성을 추가할 수 있습니다.

구성 요소/리소스에 설정된 모든 속성은 handlebars 템플릿의 속성 키를 참조하여 액세스할 수 있습니다.

`{{properties.<property_name>}}`

## CSS 스키닝 {#skinning-css}

웹 사이트의 전체 테마에 맞게 구성 요소를 사용자 지정하는 것은 색상, 글꼴, 이미지, 단추, 링크, 간격, 특정 범위로 위치를 변경하는 &#39;스키닝&#39;을 통해 수행할 수 있습니다.

프레임워크 스타일을 선택적으로 재정의하거나 완전히 새로운 스타일 시트를 작성하여 스키닝을 수행할 수 있습니다. SCF 구성 요소는 구성 요소를 구성하는 다양한 요소에 영향을 주는 네임스페이스와 모듈식 및 시맨틱 CSS 클래스를 정의합니다.

구성 요소를 스킨하려면

1. 변경할 요소(예: 작성기 영역, 도구 모음 단추, 메시지 글꼴 등)를 식별합니다.
1. 이러한 요소에 영향을 주는 CSS 클래스/규칙을 식별합니다.
1. 스타일시트 파일(.css)을 만듭니다.
1. 사이트의 클라이언트 라이브러리 폴더([clientlibs](#clientlibs-for-scf))에 스타일시트를 포함시키고 이 스타일시트가 [ui:includeClientLib](../../help/sites-developing/clientlibs.md)이 있는 템플릿 및 페이지에 포함되어 있는지 확인합니다.

1. 스타일 시트에서 식별한 CSS 클래스 및 규칙(#2)을 재정의하고 스타일을 추가합니다.

사용자 지정 스타일이 기본 프레임워크 스타일을 재정의하고 구성 요소가 새 스킨으로 렌더링됩니다.

>[!CAUTION]
>
>`scf-js` 접두사가 있는 모든 CSS 클래스 이름은 Javascript 코드에서 특정 사용을 합니다. 이러한 클래스는 구성 요소의 상태에 영향을 주며(예: 숨김에서 가시기로 전환) 무시하거나 제거할 수 없습니다.
>
>`scf-js` 클래스는 스타일에 영향을 주지 않지만 요소의 상태를 제어하므로 부작용이 있을 수 있다는 경고가 있는 스타일시트에 클래스 이름을 사용할 수 있습니다.

## Javascript 확장 {#extending-javascript}

구성 요소 Javascript 구현을 확장하려면 다음을 수행해야 합니다.

1. jcr:resourceSuperType을 확장 구성 요소의 jcr:resourceType 값(예: social/forum/components/hbs/forum)으로 설정한 앱용 구성 요소를 만듭니다.
1. 기본 SCF 구성 요소의 Javascript를 검사하여 SCF.registerComponent()를 사용하여 등록해야 하는 메서드를 확인합니다.
1. 확장 구성 요소의 Javascript를 복사하거나 처음부터 시작합니다.
1. 메서드를 확장합니다.
1. SCF.registerComponent()를 사용하여 기본값이나 사용자 정의된 개체 및 뷰에 모든 메서드를 등록합니다.

### forum.js:포럼 샘플 확장 - HBS {#forum-js-sample-extension-of-forum-hbs}

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

스크립트 태그는 클라이언트측 프레임워크의 고유한 부분입니다. 이 접착제는 서버 측에서 생성된 마크업을 클라이언트 측의 모델 및 뷰와 바인딩하는 데 도움이 되는 풀입니다.

구성 요소를 오버레이하거나 재정의할 때 SCF 스크립트의 스크립트 태그를 제거해서는 안 됩니다. HTML에서 JSON을 주입하기 위해 자동으로 생성된 SCF 스크립트 태그는 `data-scf-json=true` 속성으로 식별됩니다.

## SCF {#clientlibs-for-scf}용 Clientlibs

[클라이언트측 라이브러리](../../help/sites-developing/clientlibs.md)(clientlibs)의 사용은 클라이언트에서 컨텐츠를 렌더링하는 데 사용되는 Javascript 및 CSS를 구성하고 최적화하는 방법을 제공합니다.

SCF용 clientlibs는 카테고리 이름에 &#39;author&#39;가 존재해야만 변하는 두 변형의 매우 특정한 이름 지정 패턴을 따릅니다.

| Clientlib Variant | 범주 등록 정보 패턴 |
|--- |--- |
| complete clientlib | cq.social.hbs.&lt;component name=&quot;&quot;> |
| author clientlib | cq.social.author.hbs.&lt;component name=&quot;&quot;> |

### Clientlibs {#complete-clientlibs} 완료

전체(작성자가 아닌) clientlibs에는 종속성이 포함되며 ui:includeClientLib에 포함되므로 편리합니다.

이러한 버전은 다음과 같습니다.

* `/etc/clientlibs/social/hbs/&lt;component name&gt;`

예:

* 클라이언트 폴더 노드:`/etc/clientlibs/social/hbs/forum`
* 카테고리 속성:`cq.social.hbs.forum`

[커뮤니티 구성 요소 안내서](components-guide.md)는 각 SCF 구성 요소에 필요한 전체 clientlibs를 나열합니다.

[Communities 구성 ](clientlibs.md) 요소용 Clientlibs 페이지에 clientlibs를 추가하는 방법을 설명합니다.

### 작성자 Clientlibs {#author-clientlibs}

작성 버전 clientlibs는 구성 요소를 구현하는 데 필요한 최소한의 Javascript로 제거됩니다.

이러한 clientlibs는 직접 포함해서는 안 되지만, 대신 사이트에 대해 수작업으로 제공되는 다른 clientlibs에 포함할 수 있습니다.

이러한 버전은 SCF libs 폴더에 있습니다.

* `/libs/social/&lt;feature&gt;/components/hbs/&lt;component name&gt;/clientlibs`

예:

* 클라이언트 폴더 노드:`/libs/social/forum/hbs/forum/clientlibs`
* 카테고리 속성:`cq.social.author.hbs.forum`

참고:author clientlibs는 다른 라이브러리를 포함하지 않지만, 해당 종속성을 나열합니다. 다른 라이브러리에 임베드할 때 종속성은 자동으로 가져오지 않고 포함되어 있어야 합니다.

필요한 작성자 clientlibs는 [커뮤니티 구성 요소 안내서](components-guide.md)에서 각 SCF 구성 요소에 나열된 clientlibs에 &quot;author&quot;를 삽입하여 식별할 수 있습니다.

### 사용 고려 사항 {#usage-considerations}

모든 사이트는 클라이언트 라이브러리를 관리하는 방식이 다릅니다. 다양한 요소는 다음과 같습니다.

* 전체 속도:사이트가 응답화되기를 원하지만, 첫 번째 페이지가 약간 느리게 로드되는 것은 허용될 수 있습니다. 많은 페이지에서 동일한 Javascript를 사용하는 경우 다양한 Javascript를 하나의 clientlib에 내장하고 첫 번째 페이지에서 참조하여 로드할 수 있습니다. 이 단일 다운로드의 Javascript는 캐시된 상태로 유지되므로 후속 페이지에 대해 다운로드할 데이터의 양을 최소화합니다.
* 짧은 첫 페이지:첫 번째 페이지가 빠르게 로드되기를 원할 수 있습니다. 이 경우 Javascript는 필요한 경우에만 참조할 수 있는 여러 개의 작은 파일에 있습니다.
* 첫 번째 페이지 로드와 후속 다운로드 간의 균형.

| **[⇐ 기능 핵심 사항](essentials.md)** | **[서버 측 사용자 지정 ⇒](server-customize.md)** |
|---|---|
|  | **[SCF Handlebars Helpers ⇒](handlebars-helpers.md)** |
