---
title: 편집기
description: 클래식 UI 편집기로 다시 전환하는 방법에 대해 알아봅니다.
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: operations
content-type: reference
docset: aem65
exl-id: 8540e1f0-22d7-4f48-85d9-7c44eb7185df
solution: Experience Manager, Experience Manager Sites
feature: Administering
role: Admin
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: c45915cf-e157-4af7-a80d-97b905bcb3a5
    internal-label: Experience Manager Sites
feature_v2:
  - id: 5ef752af-d616-5b23-8312-06964e46b208
    internal-label: Administering
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '110'
ht-degree: 3%
---

# 편집기{#editor}

편집기에서 클래식 UI로 전환하는 기능이 기본적으로 비활성화되었습니다.

**페이지 정보** 메뉴에서 **클래식 UI에서 열기** 옵션을 다시 사용하려면 다음 단계를 따르십시오.

1. CRXDE Lite을 사용하여 다음 노드를 찾습니다.

   `/libs/wcm/core/content/editor/jcr:content/content/items/content/header/items/headerbar/items/pageinfopopover/items/list/items/classicui`

   예

   ` [https://localhost:4502/crx/de/index.jsp#/libs/wcm/core/content/editor/jcr%3Acontent/content/items/content/header/items/headerbar/items/pageinfopopover/items/list/items/classicui](https://localhost:4502/crx/de/index.jsp#/libs/wcm/core/content/editor/jcr%3Acontent/content/items/content/header/items/headerbar/items/pageinfopopover/items/list/items/classicui)`

1. **오버레이 노드** 옵션을 사용하여 오버레이를 만듭니다. 예:

   * **경로**: `/apps/wcm/core/content/editor/jcr:content/content/items/content/header/items/headerbar/items/pageinfopopover/items/list/items/classicui`
   * **오버레이 위치**: `/apps/`
   * **노드 유형 일치**: 활성(확인란 선택)

1. 중첩된 노드에 다음 다중 값 텍스트 속성을 추가합니다.

   `sling:hideProperties = ["granite:hidden"]`

1. 페이지를 편집할 때 **페이지 정보** 메뉴에서 **클래식 UI에서 열기** 옵션을 다시 사용할 수 있습니다.

   ![페이지 정보에서 클래식 UI로 열기 옵션](assets/syui-03-2019-02-27-15-19-48.png)
