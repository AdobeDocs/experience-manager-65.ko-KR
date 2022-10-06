---
title: 리치 텍스트 편집기 핵심 사항
seo-title: Rich Text Editor Essentials
description: 리치 텍스트 편집기 기능 개요
seo-description: Rich text Editor feature overview
uuid: f96015cc-114b-431a-a5ba-dc195c2a0b83
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: 0225a543-0fad-488b-8b0b-8b3512d44fbe
exl-id: 821e32f4-da8d-4bbb-936a-0844b8a24cdd
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '230'
ht-degree: 3%

---

# 리치 텍스트 편집기 핵심 사항 {#rich-text-editor-essentials}

## 개요 {#overview}

리치 텍스트 편집기(RTE)가 마크업으로 텍스트를 입력하는 기능을 제공합니다.

커뮤니티 구성 요소의 경우 [작성 환경의 리치 텍스트 편집기](../../help/sites-authoring/rich-text-editor.md)이 변수는 게시 환경에 입력한 텍스트에 영향을 줍니다.

![리치 텍스트 편집기](assets/rich-text-editor.png)

## 리치 텍스트 편집기 활성화 {#enabling-rich-text-editor}

RTE를 허용하도록 사용자 생성 콘텐츠(UGC)를 허용하는 커뮤니티 구성 요소를 활성화할 수 있습니다. 구성 요소가 페이지에 추가되었는지 또는 페이지에 포함되었는지 여부에 따라 [함수](functions.md), RTE는 기본적으로 활성화되어 있거나 활성화되지 않을 수 있습니다.

활성화되지 않은 경우 를 입력합니다. [편집 모드 작성](sites-console.md#authoring-site-content)을 클릭하고 편집할 구성 요소를 선택한 다음 `Rich Text Editor` 확인란을 선택합니다.

RTE는 다음 커뮤니티 구성 요소에 사용할 수 있습니다.

* [블로그](blog-feature.md)
* [달력](calendar.md)
* [댓글](comments.md)
* [Filelibrary](file-library.md)
* [포럼](forum.md)
* [메시지](configure-messaging.md)
* [QnA](working-with-qna.md)
* [검토](reviews.md)

## 사용자 지정 {#customization}

구현이 다음을 기반으로 하므로 리치 텍스트 편집기의 사용자 지정이 가능합니다 [CKEditor](https://www.ckeditor.com/).

커뮤니티 구성 요소에 대한 현재 구성은 `cq.social.  scf   clientlib`( 의 저장소에 있음)

`/libs/clientlibs/social/commons/scf/ckrte.js`

향후 업그레이드하면 편집 내용이 무시될 수 있으므로 cq.social.scf clientlib을 수정하지 않는 것이 좋습니다.

### 사용자 지정 예: 인라인 링크 {#example-customization-inline-links}

보안 문제로 인해 하이퍼링크 옵션은 기본적으로 구성원에게 제공되는 리치 텍스트 아이콘 세트에 포함되지 않습니다. UGC에서 해커가 허용될 때 해악 능력이 광범위하다.

도구 모음에 하이퍼링크 옵션을 추가하려면

* 이름이 &quot;&quot;인 도구 모음 추가 `links`&quot;
   * `{ name: 'links', items: [ 'Link','Unlink','Anchor' ] }`
* 선택 **[!UICONTROL 모두 저장]**

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
