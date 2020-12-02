---
title: 클라이언트측 사용자 정의
seo-title: 클라이언트측 사용자 정의
description: AEM Communities의 동작 또는 모양 클라이언트측 사용자 정의
seo-description: AEM Communities의 동작 또는 모양 클라이언트측 사용자 정의
uuid: 57978c39-9a8a-4098-9001-c8bbe7ee786f
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 24b6d1d2-c118-4a25-959f-2783961c4ae3
translation-type: tm+mt
source-git-commit: f375b40c084ee363757b78c602091f38524b8b03
workflow-type: tm+mt
source-wordcount: '1239'
ht-degree: 0%

---


# 클라이언트측 사용자 지정 {#client-side-customization}

| **[Feature ⇐ Essentials](essentials.md)** | **[서버측 맞춤화 =](server-customize.md)** |
|---|---|
|  | **[SCF 핸들바르를 돕는 사람 =](handlebars-helpers.md)** |

클라이언트측에서 AEM Communities 구성 요소의 모양 및/또는 동작을 사용자 정의하려면 몇 가지 방법이 있습니다.

두 가지 주요 방법은 구성 요소를 오버레이하거나 확장하는 것입니다.

[구성 ](#overlays) 요소 오버레이는 기본 구성 요소를 변경하고 구성 요소에 대한 모든 참조에 영향을 줍니다.

[구성 요소](#extensions) 를 고유한 이름으로 확장하면 변경 범위가 제한됩니다. &#39;extend&#39;라는 용어는 &#39;override&#39;와 혼용적으로 사용됩니다.

## 오버레이 {#overlays}

구성 요소 오버레이는 기본 구성 요소를 수정하고 기본값을 사용하는 모든 인스턴스에 영향을 주는 방법입니다.

오버레이는 /**libs** 디렉토리에서 원래 구성 요소를 수정하지 않고 /**apps** 디렉토리에서 기본 구성 요소의 사본을 수정하여 수행됩니다. 구성 요소는 &#39;libs&#39;가 &#39;apps&#39;로 대체된다는 점을 제외하고 동일한 상대 경로로 구성됩니다.

/apps 디렉토리는 요청을 해결하기 위해 검색된 첫 번째 위치입니다. 찾을 수 없는 경우, /libs 디렉토리에 있는 기본 버전이 사용됩니다.

/libs 디렉토리의 기본 구성 요소는 이후 패치 및 업그레이드는 공용 인터페이스를 유지하는 동안 필요한 방식으로 /libs 디렉토리를 변경할 수 있으므로 수정해서는 안 됩니다.

이는 특정 사용을 위해 수정 작업을 수행하는 기본 구성 요소인 [확장](#extensions)과 다릅니다. 여기서 구성 요소에 대한 고유한 경로를 만들고 /libs 디렉토리의 원래 기본 구성 요소를 슈퍼 리소스 유형으로 참조하기 때문입니다.

주석 구성 요소 오버레이의 빠른 예를 보려면 [오버레이 댓글 구성 요소 자습서](overlay-comments.md)를 시도해 보십시오.

## 확장 {#extensions}

구성 요소 확장(재정의)은 기본값을 사용하는 모든 인스턴스에 영향을 주지 않고 특정 사용을 수정하는 방법입니다. 확장 구성 요소는 /apps 폴더에서 고유하게 이름이 지정되고 /libs 폴더의 기본 구성 요소를 참조하므로 구성 요소의 기본 디자인 및 동작은 수정되지 않습니다.

이는 Sling의 특성이 libs/ 폴더에서 검색하기 전에 apps/ 폴더에 대한 상대 참조를 확인하는 기본 구성 요소인 [오버레이](#overlays)와 다르므로 구성 요소의 디자인 또는 동작이 전체적으로 수정됩니다.

주석 구성 요소를 확장하는 빠른 예를 보려면 [주석 구성 요소 확장 자습서](extend-comments.md)를 시도해 보십시오.

## Javascript 바인딩 {#javascript-binding}

구성 요소에 대한 HBS 스크립트는 JavaScript 객체, 모델 및 뷰에 바인딩되어야 하며 이 기능은 구현됩니다.

`data-scf-component` 속성의 값은 **`social/tally/components/hbs/rating`** 같은 기본값이거나, 사용자 지정된 기능을 위해 **weretail/components/hbs/rating**&#x200B;과 같은 확장(사용자 지정된) 구성 요소일 수 있습니다.

구성 요소를 바인딩하려면 전체 구성 요소 스크립트를 &lt;div> 요소 내에 다음 특성을 포함해야 합니다.

* `data-component-id`=&quot;{{id}}&quot;

   resolves to id property from the context

* `data-scf-component`=&quot;*&lt;resourcetype>*

예를 들어 `/apps/weretail/components/hbs/rating/rating.hbs`에서:

```xml
<div class="we-Rating" data-component-id="{{id}}" data-scf-component="weretail/components/hbs/rating">

     <!-- HTML with HBS accessing the rating component -->

</div>
```

## 사용자 정의 속성 {#custom-properties}

구성 요소를 확장하거나 오버레이할 때 수정된 대화 상자에 속성을 추가할 수 있습니다.

All properties set on a component/resource can be accessed by referencing the property keys in the handlebars template:

`{{properties.<property_name>}}`

## CSS 스키닝 {#skinning-css}

색상, 글꼴, 이미지, 버튼, 링크, 간격 및 특정 범위로 위치를 변경하는 &#39;스키닝&#39;을 통해 웹 사이트의 전체 테마에 맞게 구성 요소를 사용자 정의할 수 있습니다.

프레임워크 스타일을 선택적으로 덮어쓰거나 완전히 새로운 스타일 시트를 작성하여 스키닝을 수행할 수 있습니다. SCF 구성 요소는 구성 요소를 구성하는 다양한 요소에 영향을 주는 네임스페이스된, 모듈형 및 의미 체계 CSS 클래스를 정의합니다.

구성 요소의 스킨을 지정하려면

1. 변경할 요소(예: 컴포저 영역, 도구 모음 단추, 메시지 글꼴 등)를 식별합니다.
1. 이러한 요소에 영향을 주는 CSS 클래스/규칙을 식별합니다.
1. 스타일시트 파일(.css)을 만듭니다.
1. 사이트의 클라이언트 라이브러리 폴더([clientlibs](#clientlibs-for-scf))에 스타일시트를 포함시키고 해당 스타일시트가 [ui:includeClientLib](../../help/sites-developing/clientlibs.md)이 있는 템플릿 및 페이지에서 포함되었는지 확인합니다.

1. 스타일 시트에서 식별한 CSS 클래스 및 규칙을 재정의하고 스타일을 추가합니다.

이제 사용자 정의 스타일이 기본 프레임워크 스타일을 덮어쓰고 구성 요소가 새 스킨으로 렌더링됩니다.

>[!CAUTION]
>
>`scf-js`으로 접두사가 붙은 모든 CSS 클래스 이름에는 javascript 코드에서 특정 용도가 사용됩니다. 이러한 클래스는 구성 요소의 상태(예: 숨김에서 표시로 전환)에 영향을 주며, 무시하거나 제거할 수 없습니다.
>
>`scf-js` 클래스는 스타일에 영향을 주지 않지만, 요소의 상태를 제어하므로 부작용이 있을 수 있다는 주의해야 하는 사항이 있는 스타일시트에서 클래스 이름을 사용할 수 있습니다.

## Javascript {#extending-javascript} 확장

구성 요소 Javascript 구현을 확장하려면 다음을 수행해야 합니다.

1. 확장 구성 요소의 jcr:resourceSuperType 값으로 설정된 jcr:resourceType을 사용하여 앱에 사용할 구성 요소를 만듭니다(예: social/forum/components/hbs/forum).
1. 기본 SCF 구성 요소의 Javascript를 검사하여 SCF.registerComponent()를 사용하여 등록해야 하는 메서드를 결정합니다.
1. 확장 구성 요소의 Javascript를 복사하거나 처음부터 다시 시작합니다.
1. 메서드를 확장합니다.
1. SCF.registerComponent()를 사용하여 모든 메서드를 기본값이나 사용자 지정된 개체 및 보기로 등록합니다.

### forum.js:포럼 확장 샘플 - HBS {#forum-js-sample-extension-of-forum-hbs}

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

스크립트 태그는 클라이언트측 프레임워크의 기본적인 부분입니다. 서버 측에서 생성된 마크업을 클라이언트 쪽의 모델 및 뷰와 바인딩하는 데 도움이 되는 풀입니다.

구성 요소를 오버레이하거나 덮어쓸 때 SCF 스크립트의 스크립트 태그를 제거하지 말아야 합니다. HTML에서 JSON을 삽입하기 위해 자동으로 만들어진 SCF 스크립트 태그는 `data-scf-json=true` 속성으로 식별됩니다.

## SCF {#clientlibs-for-scf}용 Clientlibs

[클라이언트측 라이브러리](../../help/sites-developing/clientlibs.md)(clientlibs)를 사용하면 클라이언트에서 컨텐츠를 렌더링하는 데 사용되는 Javascript 및 CSS를 구성하고 최적화할 수 있습니다.

SCF용 Clientlibs는 두 가지 변형에 대해 매우 특정한 이름 지정 패턴을 따르며, 이 패턴은 범주 이름에 &#39;author&#39;가 있는 경우에만 달라집니다.

| Clientlib Variant | 카테고리 속성 패턴 |
|--- |--- |
| complete clientlib | cq.social.hbs.&lt;component name=&quot;&quot;> |
| author clientlib | cq.social.author.hbs.&lt;component name=&quot;&quot;> |

### Complete Clientlibs {#complete-clientlibs}

전체(작성자가 아님) 클라이언트에는 종속성이 포함되며 ui:includeClientLib에 포함하기에 편리합니다.

이러한 버전은

* `/etc/clientlibs/social/hbs/&lt;component name&gt;`

예:

* 클라이언트 폴더 노드:`/etc/clientlibs/social/hbs/forum`
* 카테고리 속성:`cq.social.hbs.forum`

[커뮤니티 구성 요소 안내서](components-guide.md)에는 각 SCF 구성 요소에 필요한 전체 clientlibs가 나열됩니다.

[Clientlibs for Communities ](clientlibs.md) Component페이지에 clientlibs를 추가하는 방법을 설명합니다.

### Author Clientlibs {#author-clientlibs}

작성 버전 clientlibs는 구성 요소를 구현하는 데 필요한 최소한의 Javascript로 제거됩니다.

이러한 clientlibs는 직접 포함되어서는 안 되지만 대신 다른 clientlibs에 임베드할 수 있습니다. 다른 clientlibs는 사이트를 위해 수작업으로 제작됩니다.

다음 버전은 SCF libs 폴더에서 찾을 수 있습니다.

* `/libs/social/&lt;feature&gt;/components/hbs/&lt;component name&gt;/clientlibs`

예:

* 클라이언트 폴더 노드:`/libs/social/forum/hbs/forum/clientlibs`
* 카테고리 속성:`cq.social.author.hbs.forum`

참고:author clientlibs never embed other libraries, they do list their dependencies. 다른 라이브러리에 포함할 경우 종속성은 자동으로 가져오지 않고 포함되어 있어야 합니다.

필요한 작성자 clientlibs는 [커뮤니티 구성 요소 안내서](components-guide.md)의 각 SCF 구성 요소에 대해 나열된 clientlibs에 &quot;author&quot;를 삽입하여 식별할 수 있습니다.

### 사용 고려 사항 {#usage-considerations}

모든 사이트는 클라이언트 라이브러리를 관리하는 방식이 서로 다릅니다. 다양한 요소는 다음과 같습니다.

* 전체 속도:사이트가 응답하기 위한 것일 수도 있지만 첫 페이지의 로드 속도가 약간 느려도 가능합니다. 많은 페이지가 동일한 Javascript를 사용하는 경우, 다양한 Javascripts를 하나의 clientlib에 내장하고 첫 번째 페이지에서 참조하여 로드할 수 있습니다. 이 단일 다운로드에서 Javascript는 캐시되어 이후 페이지에 대해 다운로드할 데이터의 양을 최소화합니다.
* 짧은 첫 페이지:첫 페이지가 빨리 로드되기를 바라는 것일 수도 있습니다. 이 경우 Javascript는 필요한 경우에만 참조할 수 있도록 여러 개의 작은 파일에 있습니다.
* 첫 번째 페이지 로드와 후속 다운로드 간의 균형.

| **[Feature ⇐ Essentials](essentials.md)** | **[서버측 맞춤화 =](server-customize.md)** |
|---|---|
|  | **[SCF 핸들바르를 돕는 사람 =](handlebars-helpers.md)** |

