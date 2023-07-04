---
title: 편집기
seo-title: Editor
description: 클래식 UI 편집기로 다시 전환하는 방법에 대해 알아봅니다.
seo-description: Learn how to switch back to the Classic UI Editor.
uuid: ca8b07e7-014f-428e-82bd-87f3aae12f6e
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
discoiquuid: 54903f3a-1e7e-4083-a2c9-b2ea4555d7fc
docset: aem65
exl-id: 8540e1f0-22d7-4f48-85d9-7c44eb7185df
source-git-commit: ab6399d2d3b4ea0e77a017a34b953864ecadb10c
workflow-type: tm+mt
source-wordcount: '108'
ht-degree: 6%

---

# 편집기{#editor}

편집기에서 클래식 UI로 전환하는 기능이 기본적으로 비활성화되었습니다.

옵션을 다시 활성화하려면 **클래식 UI에서 열기** 다음에서 **페이지 정보** 메뉴를 보려면 다음 단계를 따르십시오.

1. CRXDE Lite을 사용하여 다음 노드를 찾습니다.

   `/libs/wcm/core/content/editor/jcr:content/content/items/content/header/items/headerbar/items/pageinfopopover/items/list/items/classicui`

   예

   ` [https://localhost:4502/crx/de/index.jsp#/libs/wcm/core/content/editor/jcr%3Acontent/content/items/content/header/items/headerbar/items/pageinfopopover/items/list/items/classicui](https://localhost:4502/crx/de/index.jsp#/libs/wcm/core/content/editor/jcr%3Acontent/content/items/content/header/items/headerbar/items/pageinfopopover/items/list/items/classicui)`

1. 를 사용하여 오버레이 만들기 **오버레이 노드** 옵션(예: )

   * **경로**: `/apps/wcm/core/content/editor/jcr:content/content/items/content/header/items/headerbar/items/pageinfopopover/items/list/items/classicui`
   * **오버레이 위치**: `/apps/`
   * **노드 유형 일치**: 활성(확인란 선택)

1. 중첩된 노드에 다음 다중 값 텍스트 속성을 추가합니다.

   `sling:hideProperties = ["granite:hidden"]`

1. 다음 **클래식 UI에서 열기** 옵션은에서 다시 사용할 수 있습니다. **페이지 정보** 페이지를 편집할 때 메뉴 아래의 제품에서 사용할 수 있습니다.

   ![페이지 정보에서 클래식 UI로 열기 옵션](assets/syui-03-2019-02-27-15-19-48.png)
