---
title: 리치 텍스트 편집기 핵심 사항
description: 마크업으로 텍스트를 입력할 수 있는 리치 텍스트 편집기의 기본 사항과 기능에 대해 알아봅니다.
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 821e32f4-da8d-4bbb-936a-0844b8a24cdd
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '237'
ht-degree: 3%

---

# 리치 텍스트 편집기 핵심 사항 {#rich-text-editor-essentials}

## 개요 {#overview}

리치 텍스트 편집기(RTE)를 사용하면 마크업이 있는 텍스트를 입력할 수 있습니다.

커뮤니티 구성 요소의 경우 [작성 환경의 리치 텍스트 편집기](../../help/sites-authoring/rich-text-editor.md)와 유사하지만 게시 환경에 입력된 텍스트에 영향을 줍니다.

![리치 텍스트 편집기](assets/rich-text-editor.png)

## 리치 텍스트 편집기 활성화 {#enabling-rich-text-editor}

UGC(사용자 생성 컨텐츠)를 허용하는 커뮤니티 구성 요소를 활성화하여 RTE를 허용할 수 있습니다. 구성 요소가 페이지에 추가되거나 [function](functions.md) 내에 포함된 경우 기본적으로 RTE가 활성화되거나 활성화되지 않을 수 있습니다.

활성화되지 않은 경우 [작성자 편집 모드](sites-console.md#authoring-site-content)를 입력하고 편집할 구성 요소를 선택한 다음 `Rich Text Editor` 확인란을 선택하면 됩니다.

RTE는 다음 커뮤니티 구성 요소에 사용할 수 있습니다.

* [블로그](blog-feature.md)
* [달력](calendar.md)
* [댓글](comments.md)
* [파일 라이브러리](file-library.md)
* [포럼](forum.md)
* [메시지](configure-messaging.md)
* [QnA](working-with-qna.md)
* [리뷰](reviews.md)

## 사용자 지정 {#customization}

구현은 [CKEditor](https://ckeditor.com/)을 기반으로 하므로 서식 있는 텍스트 편집기를 사용자 지정할 수 있습니다.

커뮤니티 구성 요소에 대한 현재 구성은 저장소의 `cq.social.  scf   clientlib`에 있습니다.

`/libs/clientlibs/social/commons/scf/ckrte.js`

향후 업그레이드가 편집 내용을 재정의할 수 있으므로 cq.social.scf clientlib을 수정하지 않는 것이 좋습니다.

### 예제 사용자 정의: 인라인 링크 {#example-customization-inline-links}

보안상의 문제로 인해 하이퍼링크 옵션은 기본적으로 구성원에게 제공되는 서식 있는 텍스트 아이콘 집합에 포함되지 않습니다. UGC에서 href가 허용되었을 때, 장난을 할 수 있는 능력은 광범위하다.

도구 모음에 하이퍼링크 옵션을 추가하려면 다음을 수행합니다.

* 이름이 &quot; `links`&quot;인 도구 모음 추가
   * `{ name: 'links', items: [ 'Link','Unlink','Anchor' ] }`
* **[!UICONTROL 모두 저장]** 선택

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
