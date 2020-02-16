---
title: 콘솔 사용자 정의
seo-title: 콘솔 사용자 정의
description: AEM 파섹
seo-description: AEM 파섹
uuid: 8ecce9ff-5907-41e1-af3b-a8646352d633
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: 61a4e196-bd53-4ef0-816b-c14401462457
docset: aem65
translation-type: tm+mt
source-git-commit: c13eabdf4938a47ddf64d55b00f845199591b835

---


# 콘솔 사용자 정의 {#customizing-the-consoles}

>[!CAUTION]
>
>이 문서에서는 터치가 활성화된 최신 UI에서 콘솔을 사용자 지정하는 방법에 대해 설명하고 클래식 UI에는 적용되지 않습니다.

AEM에서는 작성 인스턴스의 콘솔(및 [페이지 작성 기능](/help/sites-developing/customizing-page-authoring-touch.md))을 사용자 지정할 수 있도록 하는 다양한 메커니즘을 제공합니다.

* ClientlibsClientlibs를 사용하면 표준 함수, 개체 및 메서드를 재사용하면서 기본 구현을 확장하여 새로운 기능을 구현할 수 있습니다. 사용자 정의할 때 사용자 지정 구성 요소에 필요한 코드를 저장할 수 `/apps.` 있는 예를 들어 사용자 지정 clientlib 아래에 사용자 지정 clientlib을 만들 수 있습니다.

* OverlaysOverlays는 노드 정의를 기반으로 하며, 표준 기능( `/libs`in)을 사용자 정의된 기능(in)과 오버레이할 수 `/apps`있습니다. 오버레이를 만들 때는 소스 병합에서 상속을 허용하므로 원본의 1:1 사본이 필요하지 않습니다.

AEM 콘솔을 확장하는 방법은 여러 가지가 있습니다. 작은 선택 항목은 아래에서 수준 높게 다룹니다.

>[!NOTE]
>
>자세한 내용은 다음을 참조하십시오.
>
>* clientlibs 사용 및 [만들기](/help/sites-developing/clientlibs.md).
>* 오버레이 [사용 및 만들기](/help/sites-developing/overlays.md).
>* [Granite](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html)
>
>
이 항목에서는 AEM Gems 세션 - [AEM](https://docs.adobe.com/content/ddc/en/gems.html) 6.0 [에 대한 사용자 인터페이스 맞춤화에도 설명되어 있습니다](https://docs.adobe.com/content/ddc/en/gems/user-interface-customization-for-aem-6.html).

>[!CAUTION]
>
>패스에 있는 ***어떤 것도 변경하지*** 않아야 `/libs` 합니다.
>
>이는 다음에 인스턴스를 업그레이드할 때 의 컨텐츠를 `/libs` 덮어쓰게 되기 때문입니다(핫픽스 또는 기능 팩을 적용할 때 덮어쓸 수 있음).
>
>구성 및 기타 변경에 대한 권장 방법은 다음과 같습니다.
>
>1. 필요한 항목(즉, 있는 대로)을 `/libs``/apps`
   >
   >
1. Make any changes within `/apps`
>



예를 들어 구조 내의 다음 위치를 `/libs` 오버레이할 수 있습니다.

* 콘솔(화강암 UI 페이지를 기반으로 하는 모든 콘솔);예를 들면 다음과 같습니다.

   * `/libs/wcm/core/content`

>[!NOTE]
>
>추가 팁 및 도구는 기술 자료 문서, [AEM TouchUI 문제](https://helpx.adobe.com/experience-manager/kb/troubleshooting-aem-touchui-issues.html)해결을 참조하십시오.

## 콘솔에 대한 기본 보기 사용자 정의 {#customizing-the-default-view-for-a-console}

콘솔의 기본 보기(열, 카드, 목록)를 사용자 정의할 수 있습니다.

1. 아래 아래의 필수 항목을 오버레이하여 보기 순서를 변경할 수 있습니다.

   `/libs/wcm/core/content/sites/jcr:content/views`

   첫 번째 항목이 기본값이 됩니다.

   사용할 수 있는 노드는 사용 가능한 보기 옵션과 상호 연관됩니다.

   * `column`
   * `card`
   * `list`

1. 예를 들어 목록에 대한 오버레이에서 다음을 수행합니다.

   `/apps/wcm/core/content/sites/jcr:content/views/list`

   다음 속성을 정의합니다.

   * **이름**: `sling:orderBefore`
   * **유형**: `String`
   * **값**: `column`

### 도구 모음에 새 작업 추가 {#add-new-action-to-the-toolbar}

1. 사용자 정의 작업을 위해 고유한 구성 요소를 만들고 해당 클라이언트 라이브러리를 포함할 수 있습니다. 예를 들어 Twitter로 **홍보** 작업:

   `/apps/wcm/core/clientlibs/sites/js/twitter.js`

   그러면 콘솔에서 도구 모음 항목에 연결할 수 있습니다.

   `/apps/<yourProject>/admin/ext/launches`

   예를 들어 선택 모드에서 다음을 수행합니다.

   `content/jcr:content/body/content/header/items/selection/items/twitter`

### 특정 그룹에 도구 모음 작업 제한 {#restrict-a-toolbar-action-to-a-specific-group}

1. 사용자 정의 렌더링 조건을 사용하여 표준 동작을 오버레이하고 렌더링하기 전에 충족해야 하는 특정 조건을 적용할 수 있습니다.

   예를 들어 그룹에 따라 렌더링 조건을 제어하는 구성 요소를 만듭니다.

   `/apps/myapp/components/renderconditions/group`

1. 사이트 콘솔에서 사이트 만들기 작업에 적용하려면 다음을 수행하십시오.

   `/libs/wcm/core/content/sites`

   오버레이를 만듭니다.

   `/apps/wcm/core/content/sites`

1. 그런 다음 작업에 대한 렌더링 조건을 추가합니다.

   `jcr:content/body/content/header/items/default/items/create/items/createsite/rendercondition`

   이 노드의 속성을 사용하여 특정 작업을 수행할 `groups` 수 있는 권한을 정의할 수 있습니다.예를 들면 `administrators`

### 목록 보기에서 열 사용자 정의 {#customizing-columns-in-the-list-view}

>[!NOTE]
>
>이 기능은 텍스트 필드 열에 최적화되어 있습니다.다른 데이터 유형의 경우 오버레이할 `cq/gui/components/siteadmin/admin/listview/columns/analyticscolumnrenderer` 수 `/apps`있습니다.

목록 보기에서 열을 사용자 정의하려면

1. 사용 가능한 열 목록을 오버레이합니다.

   * 노드에서 다음을 수행합니다.

      ```
             /apps/wcm/core/content/common/availablecolumns
      ```

   * 새 열을 추가하거나 기존 열을 제거합니다.
   자세한 [내용은 오버레이 사용(및 Sling 리소스 합병)](/help/sites-developing/overlays.md) 을 참조하십시오.

1. 원할 경우:

   * 추가 데이터를 연결하려면 [](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/PageInfoProvider.html)
      `pageInfoProviderType` 속성.
   예를 들어 아래 GitHub에서 첨부된 클래스/번들을 참조하십시오.

1. 이제 목록 보기의 열 구성기에서 열을 선택할 수 있습니다.

### 리소스 필터링 {#filtering-resources}

콘솔을 사용할 때 일반적인 사용 사례는 사용자가 리소스(예: 페이지, 구성 요소, 자산 등)에서 선택해야 하는 때입니다. 예를 들어 작성자가 항목을 선택해야 하는 목록 형식을 사용할 수 있습니다.

적절한 크기로 유지하거나 사용 사례와 관련되도록 필터를 사용자 지정 술어의 형태로 구현할 수 있습니다. 자세한 내용은 [이 문서를](/help/sites-developing/customizing-page-authoring-touch.md#filtering-resources) 참조하십시오.
