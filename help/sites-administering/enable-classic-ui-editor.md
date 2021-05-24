---
title: 편집자
seo-title: 편집자
description: 클래식 UI 편집기로 다시 전환하는 방법을 알아봅니다.
seo-description: 클래식 UI 편집기로 다시 전환하는 방법을 알아봅니다.
uuid: ca8b07e7-014f-428e-82bd-87f3aae12f6e
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: 54903f3a-1e7e-4083-a2c9-b2ea4555d7fc
docset: aem65
exl-id: 8540e1f0-22d7-4f48-85d9-7c44eb7185df
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '111'
ht-degree: 7%

---

# 편집자{#editor}

기본적으로 편집기에서 클래식 UI로 전환하는 기능이 비활성화됩니다.

**페이지 정보** 메뉴에서 **클래식 UI에서 열기** 옵션을 다시 활성화하려면 다음 단계를 수행합니다.

1. CRXDE Lite을 사용하여 다음 노드를 찾습니다.

   `/libs/wcm/core/content/editor/jcr:content/content/items/content/header/items/headerbar/items/pageinfopopover/items/list/items/classicui`

   예

   ` [https://localhost:4502/crx/de/index.jsp#/libs/wcm/core/content/editor/jcr%3Acontent/content/items/content/header/items/headerbar/items/pageinfopopover/items/list/items/classicui](https://localhost:4502/crx/de/index.jsp#/libs/wcm/core/content/editor/jcr%3Acontent/content/items/content/header/items/headerbar/items/pageinfopopover/items/list/items/classicui)`

1. **오버레이 노드** 옵션을 사용하여 오버레이를 만듭니다.예:

   * **경로**: `/apps/wcm/core/content/editor/jcr:content/content/items/content/header/items/headerbar/items/pageinfopopover/items/list/items/classicui`
   * **오버레이 위치**: `/apps/`
   * **일치 노드 유형**:활성(확인란 선택)

1. 겹쳐진 노드에 다음 다중 값 텍스트 속성을 추가합니다.

   `sling:hideProperties = ["granite:hidden"]`

1. 페이지를 편집할 때 **클래식 UI에서 열기** 옵션은 **페이지 정보** 메뉴에서 다시 사용할 수 있습니다.

   ![](assets/syui-03-2019-02-27-15-19-48.png)
