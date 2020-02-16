---
title: 리치 텍스트 편집기 필수
seo-title: 리치 텍스트 편집기 필수
description: 리치 텍스트 편집기 기능 개요
seo-description: 리치 텍스트 편집기 기능 개요
uuid: f96015cc-114b-431a-a5ba-dc195c2a0b83
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 0225a543-0fad-488b-8b0b-8b3512d44fbe
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Rich Text Editor Essentials {#rich-text-editor-essentials}

## 개요 {#overview}

RTE(Rich Text Editor)를 사용하면 마크업이 있는 텍스트를 입력할 수 있습니다.

커뮤니티 구성 요소의 경우 작성 환경의 [리치 텍스트 편집기와](../../help/sites-authoring/rich-text-editor.md)유사하지만 게시 환경에 입력된 텍스트에 영향을 줍니다.

![chlimage_1-410](assets/chlimage_1-410.png)

## 리치 텍스트 편집기 활성화 {#enabling-rich-text-editor}

사용자 생성 콘텐츠(UGC)를 허용하는 커뮤니티 구성 요소를 활성화하여 RTE를 허용할 수 있습니다. 구성 요소가 페이지에 추가되었는지 또는 [함수에](functions.md)포함되었는지에 따라, RTE가 기본적으로 활성화되어 있는지 여부를 지정할 수 있습니다.

활성화되지 않은 경우 [작성자 편집 모드로](sites-console.md#authoring-site-content)전환하고 편집할 구성 요소를 선택한 다음 `Rich Text Editor` 확인란을 선택하면 됩니다.

RTE는 다음 커뮤니티 구성 요소에 사용할 수 있습니다.

* [블로그](blog-feature.md)
* [달력](calendar.md)
* [댓글](comments.md)
* [Filelibrary](file-library.md)
* [포럼](forum.md)
* [메시지](configure-messaging.md)
* [QnA](working-with-qna.md)
* [검토](reviews.md)

## 사용자 정의 {#customization}

CKEditor를 기반으로 구현되므로 리치 텍스트 편집기를 사용자 정의할 [수 있습니다](https://www.ckeditor.com/).

Communities 구성 요소에 대한 현재 구성은 에 `cq.social.  scf   clientlib`있으며

`/libs/clientlibs/social/commons/scf/ckrte.js`

이후 업그레이드가 모든 편집 내용을 덮어쓸 수 있으므로 cq.social.scf clientlib을 수정하는 것은 권장되지 않습니다.

### 사용자 정의 예:인라인 링크 {#example-customization-inline-links}

보안 문제로 인해 하이퍼링크 옵션은 기본적으로 구성원에게 제공되는 리치 텍스트 아이콘 집합에 포함되지 않습니다. UGC에서 허브가 허용되는 경우 재난에 대한 능력은 광범위하다.

도구 모음에 하이퍼링크 옵션을 추가하려면:

* &quot; `links`&quot;이라는 도구 모음 추가
   * `{ name: 'links', items: [ 'Link','Unlink','Anchor' ] }`
* 모두 **[!UICONTROL 저장을 선택합니다.]**

#### /libs/clientlibs/social/commons/scf/ckrte.js {#libs-clientlibs-social-commons-scf-ckrte-js}

```
CKRte.prototype.config = {
    toolbar: [
        { name: "basicstyles",
           items: ["Bold", "Italic", "Underline", "NumberedList", "BulletedList", "Outdent", "Indent", "JustifyLeft", "JustifyCenter", "JustifyRight", "JustifyBlock", "TextColor"]
        },
        { name: 'links',
           items: [ 'Link','Unlink','Anchor' ]
        }
    ],
    autoParagraph: false,
    autoUpdateElement: false,
    removePlugins: "elementspath",
    resize_enabled: false
};
```

