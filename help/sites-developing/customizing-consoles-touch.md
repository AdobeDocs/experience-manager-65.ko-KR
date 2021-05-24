---
title: 콘솔 사용자 지정
seo-title: 콘솔 사용자 지정
description: AEM에서는 작성 인스턴스의 콘솔을 사용자 지정할 수 있는 다양한 메커니즘을 제공합니다
seo-description: AEM에서는 작성 인스턴스의 콘솔을 사용자 지정할 수 있는 다양한 메커니즘을 제공합니다
uuid: 8ecce9ff-5907-41e1-af3b-a8646352d633
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: 61a4e196-bd53-4ef0-816b-c14401462457
docset: aem65
exl-id: 6e67f2b3-78b9-45f2-b496-61776b9fd9cc
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '717'
ht-degree: 2%

---

# 콘솔 사용자 지정 {#customizing-the-consoles}

>[!CAUTION]
>
>이 문서에서는 터치가 활성화된 최신 UI에서 콘솔을 사용자 지정하는 방법에 대해 설명하고 클래식 UI에는 적용되지 않습니다.

AEM에서는 작성 인스턴스의 콘솔(및 [페이지 작성 기능](/help/sites-developing/customizing-page-authoring-touch.md))을 사용자 지정할 수 있는 다양한 메커니즘을 제공합니다.

* Clientlibs
Clientlibs를 사용하면 표준 함수, 개체 및 메서드를 재사용하는 동안 기본 구현을 확장하여 새로운 기능을 구현할 수 있습니다. 사용자 지정할 때 `/apps.` 아래에 고유한 clientlib을 만들 수 있습니다. 예를 들어 사용자 지정 구성 요소에 필요한 코드를 보유할 수 있습니다.

* 오버레이
오버레이는 노드 정의를 기반으로 하며 사용자 지정된 고유한 기능(`/apps`에)과 표준 기능(`/libs`에)을 오버레이할 수 있도록 해줍니다. 오버레이를 만들 때 sling 리소스 병합에서 상속을 허용하므로 원본의 1:1 복사본이 필요하지 않습니다.

AEM 콘솔을 확장하는 데 여러 가지 방법으로 사용할 수 있습니다. 작은 선택 항목이 아래에 (높은 수준에서) 표시됩니다.

>[!NOTE]
>
>자세한 내용은 다음을 참조하십시오.
>
>* [clientlibs](/help/sites-developing/clientlibs.md) 사용 및 만들기
>* [오버레이](/help/sites-developing/overlays.md)를 사용하고 만듭니다.
>* [Granite](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html)

>
>
이 항목에서는 [AEM Gems](https://docs.adobe.com/content/ddc/en/gems.html) 세션 - [AEM 6.0용 사용자 인터페이스 사용자 지정에서도 다룹니다.](https://docs.adobe.com/content/ddc/en/gems/user-interface-customization-for-aem-6.html)

>[!CAUTION]
>
>***은 `/libs` 경로에서 아무 것도 변경하지 않아야 합니다.***
>
>이는 다음 번에 인스턴스를 업그레이드할 때 `/libs` 컨텐츠를 덮어쓰게 되기 때문입니다(핫픽스 또는 기능 팩을 적용할 때 덮어쓸 수 있음).
>
>구성 및 기타 변경에 대해 권장되는 방법은 다음과 같습니다.
>
>1. `/apps` 아래에 필요한 항목(즉, `/libs`에 있는 항목)을 다시 만듭니다.
   >
   >
1. `/apps` 내에서 변경

>



예를 들어 `/libs` 구조 내에서 다음 위치를 오버레이할 수 있습니다.

* 콘솔(Granite UI 페이지를 기반으로 하는 모든 콘솔);예:

   * `/libs/wcm/core/content`

>[!NOTE]
>
>추가 팁 및 도구는 기술 자료 문서 [AEM TouchUI 문제 해결](https://helpx.adobe.com/experience-manager/kb/troubleshooting-aem-touchui-issues.html) 을 참조하십시오.

## 콘솔 {#customizing-the-default-view-for-a-console}에 대한 기본 보기 사용자 지정

콘솔에 대한 기본 보기(열, 카드, 목록)를 사용자 지정할 수 있습니다.

1. 아래의 필수 항목을 오버레이하여 보기 순서를 변경할 수 있습니다.

   `/libs/wcm/core/content/sites/jcr:content/views`

   첫 번째 항목이 기본값입니다.

   사용 가능한 노드는 사용 가능한 보기 옵션과 상호 연결됩니다.

   * `column`
   * `card`
   * `list`

1. 예를 들어, 목록에 대한 오버레이에서 다음을 수행합니다.

   `/apps/wcm/core/content/sites/jcr:content/views/list`

   다음 속성을 정의합니다.

   * **이름**: `sling:orderBefore`
   * **유형**: `String`
   * **값**:  `column`

### 도구 모음 {#add-new-action-to-the-toolbar}에 새 작업 추가

1. 자체 구성 요소를 작성하고 사용자 지정 작업을 위해 해당 클라이언트 라이브러리를 포함할 수 있습니다. 예를 들어 **Twitter** 작업을 다음 위치에 프로모션합니다.

   `/apps/wcm/core/clientlibs/sites/js/twitter.js`

   그런 다음 콘솔의 도구 모음 항목에 연결할 수 있습니다.

   `/apps/<yourProject>/admin/ext/launches`

   예를 들어 선택 모드에서 다음을 수행합니다.

   `content/jcr:content/body/content/header/items/selection/items/twitter`

### 도구 모음 작업을 특정 그룹 {#restrict-a-toolbar-action-to-a-specific-group}으로 제한

1. 사용자 지정 렌더링 조건을 사용하여 표준 작업을 오버레이하고 렌더링하기 전에 충족해야 하는 특정 조건을 적용할 수 있습니다.

   예를 들어 그룹에 따라 렌더링 조건을 제어하는 구성 요소를 만듭니다.

   `/apps/myapp/components/renderconditions/group`

1. 사이트 콘솔의 사이트 만들기 작업에 적용하려면 다음을 수행하십시오.

   `/libs/wcm/core/content/sites`

   오버레이를 만듭니다.

   `/apps/wcm/core/content/sites`

1. 그런 다음 작업에 대한 렌더링 조건을 추가합니다.

   `jcr:content/body/content/header/items/default/items/create/items/createsite/rendercondition`

   이 노드의 속성을 사용하여 특정 작업을 수행할 수 있는 `groups` 을 정의할 수 있습니다.예: `administrators`

### 목록 보기에서 열 사용자 지정 {#customizing-columns-in-the-list-view}

>[!NOTE]
>
>이 기능은 텍스트 필드 열에 최적화되었습니다.다른 데이터 유형의 경우 `/apps`에 `cq/gui/components/siteadmin/admin/listview/columns/analyticscolumnrenderer`을 오버레이할 수 있습니다.

목록 보기에서 열을 사용자 정의하려면

1. 사용 가능한 열 목록을 오버레이합니다.

   * 노드에서 다음을 수행합니다.

      ```
             /apps/wcm/core/content/common/availablecolumns
      ```

   * 새 열을 추가하거나 기존 열을 제거합니다.
   자세한 내용은 [오버레이 사용(및 Sling Resource Merger)](/help/sites-developing/overlays.md)을 참조하십시오.

1. 원할 경우:

   * 추가 데이터를 연결하려면 [PageInforProvider](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/PageInfoProvider.html)를
      `pageInfoProviderType` 속성.

   예를 들어 아래의 (GitHub에서) 첨부된 클래스/번들을 참조하십시오.

1. 이제 목록 뷰의 열 구성자에서 열을 선택할 수 있습니다.

### 리소스 필터링 {#filtering-resources}

콘솔을 사용할 때 일반적인 사용 사례는 리소스(예: 페이지, 구성 요소, 자산 등)에서 사용자가 선택해야 하는 때입니다. 예를 들어 작성자가 항목을 선택해야 하는 목록 형태를 취할 수 있습니다.

목록을 적절한 크기로 유지하거나 사용 사례와 관련이 있도록 사용자 지정 설명 형태로 필터를 구현할 수 있습니다. 자세한 내용은 [이 문서](/help/sites-developing/customizing-page-authoring-touch.md#filtering-resources)를 참조하십시오.
