---
title: 페이지 작성 사용자 지정
seo-title: Customizing Page Authoring
description: AEM에서는 페이지 작성 기능을 사용자 지정할 수 있는 다양한 메커니즘을 제공합니다
seo-description: AEM provides various mechanisms to enable you to customize page authoring functionality
uuid: 9dc72d98-c5ff-4a00-b367-688ccf896526
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: 6825dcd6-fa75-4410-b6b2-e7bd4a391224
exl-id: 90594588-db8e-4d4c-a208-22c1c6ea2a2d
source-git-commit: 273836ad0afd6466eac437bf7711e7dbabc1d5e9
workflow-type: tm+mt
source-wordcount: '1383'
ht-degree: 2%

---

# 페이지 작성 사용자 지정{#customizing-page-authoring}

>[!CAUTION]
>
>이 문서에서는 터치가 활성화된 최신 UI에서 페이지 작성을 사용자 지정하는 방법에 대해 설명하고 클래식 UI에는 적용되지 않습니다.

AEM에서는 작성 인스턴스의 [콘솔](/help/sites-developing/customizing-consoles-touch.md))을 사용자 지정할 수 있도록 해주는 다양한 메커니즘을 제공합니다.

* Clientlibs

   Clientlibs를 사용하면 표준 함수, 개체 및 메서드를 재사용하는 동안 기본 구현을 확장하여 새로운 기능을 구현할 수 있습니다. 사용자 지정할 때 `/apps.` 아래에 고유한 clientlib을 만들 수 있습니다. 새 clientlib은 다음을 수행해야 합니다.

   * authoring clientlib `cq.authoring.editor.sites.page`에 따라 다름
   * 해당 `cq.authoring.editor.sites.page.hook` 카테고리의 일부가 됩니다.

* 오버레이

   오버레이는 노드 정의를 기반으로 하며 사용자 지정된 고유한 기능(`/apps`에)과 표준 기능(`/libs`에)을 오버레이할 수 있도록 해줍니다. 오버레이를 만들 때 [sling resource merger](/help/sites-developing/sling-resource-merger.md)은 상속을 허용하므로 원본의 1:1 복사본이 필요하지 않습니다.

>[!NOTE]
>
>자세한 내용은 [JS 설명서 set](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/jsdoc/ui-touch/editor-core/index.html)을 참조하십시오.

여러 가지 방법으로 AEM 인스턴스에서 페이지 작성 기능을 확장하는 데 사용할 수 있습니다. 선택 사항은 아래에 (높은 수준에서) 표시됩니다.

>[!NOTE]
>
>자세한 내용은 다음을 참조하십시오.
>
>* [clientlibs](/help/sites-developing/clientlibs.md) 사용 및 만들기
>* [오버레이](/help/sites-developing/overlays.md)를 사용하고 만듭니다.
>* [Granite](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/index.html)
>* [AEM 터치 지원 ](/help/sites-developing/touch-ui-structure.md) UI의 구조 를 참조하십시오.

>
>이 항목에서는 [AEM Gems](https://docs.adobe.com/content/ddc/en/gems.html) 세션 - [AEM 6.0용 사용자 인터페이스 사용자 지정에서도 다룹니다.](https://helpx.adobe.com/experience-manager/kt/eseminars/gems/aem-user-interface-customization-for-aem6.html)

>[!CAUTION]
>
>***은 `/libs` 경로에서 아무 것도 변경하지 않아야 합니다.***
>
>이는 다음 번에 인스턴스를 업그레이드할 때 `/libs` 컨텐츠를 덮어쓰게 되기 때문입니다(핫픽스 또는 기능 팩을 적용할 때 덮어쓸 수 있음).
>
>구성 및 기타 변경에 대해 권장되는 방법은 다음과 같습니다.
>
>1. `/apps` 아래에 필요한 항목(즉, `/libs`에 있는 항목)을 다시 만듭니다.
>1. `/apps` 내에서 변경


## 새 레이어 추가(모드) {#add-new-layer-mode}

페이지를 편집할 때 다양한 [모드](/help/sites-authoring/author-environment-tools.md#page-modes)를 사용할 수 있습니다. 이러한 모드는 [레이어](/help/sites-developing/touch-ui-structure.md#layer)를 사용하여 구현됩니다. 이렇게 하면 동일한 페이지 컨텐츠에 대해 서로 다른 유형의 기능에 액세스할 수 있습니다. 표준 레이어는 다음과 같습니다. 편집, 미리 보기, 주석 달기, 개발자 및 타깃팅.

### 레이어 예: Live Copy 상태 {#layer-example-live-copy-status}

표준 AEM 인스턴스는 MSM 레이어를 제공합니다. 이렇게 하면 [다중 사이트 관리](/help/sites-administering/msm.md)와 관련된 데이터에 액세스하고 계층에서 강조 표시됩니다.

실행 중인 Live Copy를 보려면 [We.Retail 언어 복사](/help/sites-developing/we-retail-globalized-site-structure.md) 페이지(또는 다른 Live Copy 페이지)를 편집하고 **Live Copy 상태** 모드를 선택할 수 있습니다.

다음에서 MSM 레이어 정의(참조용)를 찾을 수 있습니다.

`/libs/wcm/msm/content/touch-ui/authoring/editor/js/msm.Layer.js`

### 코드 샘플 {#code-sample}

MSM 보기의 새 레이어인 새 레이어(모드)를 만드는 방법을 보여 주는 샘플 패키지입니다.

GITHUB의 코드

GitHub에서 이 페이지의 코드를 찾을 수 있습니다

* [GitHub에서 aem-authoring-new-layer-mode 프로젝트 열기](https://github.com/Adobe-Marketing-Cloud/aem-authoring-new-layer-mode)
* 프로젝트를 [ZIP 파일](https://github.com/Adobe-Marketing-Cloud/aem-authoring-new-layer-mode/archive/master.zip)로 다운로드합니다

## 자산 브라우저에 새 선택 카테고리 추가 {#add-new-selection-category-to-asset-browser}

자산 브라우저에는 다양한 유형/카테고리의 자산(예: 이미지, 문서 등)이 표시됩니다. 이러한 자산 카테고리로 자산을 필터링할 수도 있습니다.

### 코드 샘플 {#code-sample-1}

`aem-authoring-extension-assetfinder-flickr` 는 자산 파인더에 새 그룹을 추가하는 방법을 보여주는 샘플 패키지입니다. 이 예는 [Flickr](https://www.flickr.com)의 공개 스트림에 연결하여 사이드 패널에 표시합니다.

GITHUB의 코드

GitHub에서 이 페이지의 코드를 찾을 수 있습니다

* [GitHub에서 aem-authoring-extension-assetfinder-flickr 프로젝트를 엽니다.](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-assetfinder-flickr)
* 프로젝트를 [ZIP 파일](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-assetfinder-flickr/archive/master.zip)로 다운로드합니다

## 리소스 필터링 {#filtering-resources}

페이지를 작성할 때 리소스(예: 페이지, 구성 요소, 자산 등)에서 선택해야 합니다. 예를 들어 작성자가 항목을 선택해야 하는 목록 형태를 취할 수 있습니다.

목록을 적절한 크기로 유지하거나 사용 사례와 관련이 있도록 사용자 지정 설명 형태로 필터를 구현할 수 있습니다. 예를 들어 [`pathbrowser`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html) [Granite](/help/sites-developing/touch-ui-concepts.md#granite-ui) 구성 요소를 사용하여 사용자가 특정 리소스에 대한 경로를 선택할 수 있는 경우, 제공된 경로는 다음과 같은 방법으로 필터링할 수 있습니다.

* [`com.day.cq.commons.predicate.AbstractNodePredicate`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/commons/predicate/package-summary.html) 인터페이스를 구현하여 사용자 지정 설명을 구현합니다.
* 조건자의 이름을 지정하고 `pathbrowser` 사용 시 해당 이름을 참조합니다.

사용자 지정 술어 만들기에 대한 자세한 내용은 [이 문서](/help/sites-developing/implementing-custom-predicate-evaluator.md)를 참조하십시오.

>[!NOTE]
>
>`com.day.cq.commons.predicate.AbstractNodePredicate` 인터페이스를 구현하여 사용자 지정 설명을 구현하는 것은 클래식 UI에서도 작동합니다.
>
>클래식 UI에서 사용자 지정 설명을 구현하는 예는 [이 기술 자료 문서](https://helpx.adobe.com/experience-manager/using/creating-custom-cq-tree.html)를 참조하십시오.

## 구성 요소 도구 모음에 새 작업 추가 {#add-new-action-to-a-component-toolbar}

각 구성 요소(일반적으로)에는 해당 구성 요소에서 수행할 수 있는 다양한 작업에 액세스할 수 있는 도구 모음이 있습니다.

### 코드 샘플 {#code-sample-2}

`aem-authoring-extension-toolbar-screenshot` 는 구성 요소를 렌더링하기 위해 사용자 지정 도구 모음 작업을 만드는 방법을 보여주는 샘플 패키지입니다.

GITHUB의 코드

GitHub에서 이 페이지의 코드를 찾을 수 있습니다

* [GitHub에서 aem-authoring-extension-toolbar-screens 프로젝트 열기](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-toolbar-screenshot)
* 프로젝트를 [ZIP 파일](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-toolbar-screenshot/archive/master.zip)로 다운로드합니다

## 새 즉석 편집기 추가 {#add-new-in-place-editor}

### 표준 즉석 편집기 {#standard-in-place-editor}

표준 AEM 설치에서

1. `/libs/cq/gui/components/authoring/editors/clientlibs/core/js/editors/editorExample.js`

   사용 가능한 다양한 편집기에 대한 정의를 포함합니다.

1. 편집기를 사용할 수 있는 각 리소스 유형(구성 요소에서처럼) 간에 연결이 있습니다.

   * `cq:inplaceEditing`

      예:

      * `/libs/foundation/components/text/cq:editConfig`
      * `/libs/foundation/components/image/cq:editConfig`

         * 속성: `editorType`

            해당 구성 요소에 대해 즉석 편집이 트리거될 때 사용할 인라인 편집기의 유형을 정의합니다. 예 `text`, `textimage`, `image`, `title`.

1. 편집기의 추가 구성 세부 사항은 필요한 플러그인 구성 세부 사항을 포함하도록 구성을 포함하는 `config` 노드 및 추가 `plugin` 노드를 사용하여 구성할 수 있습니다.

   다음은 이미지 구성 요소의 이미지 자르기 플러그인에 대한 종횡비를 정의하는 예입니다. 매우 제한된 화면 크기이기 때문에 자르기 예상 비율이 전체 화면 편집기로 이동되었으며 거기에서만 볼 수 있습니다.

   ```xml
   <cq:inplaceEditing
           jcr:primaryType="cq:InplaceEditingConfig"
           active="{Boolean}true"
           editorType="image">
           <config jcr:primaryType="nt:unstructured">
               <plugins jcr:primaryType="nt:unstructured">
                   <crop jcr:primaryType="nt:unstructured">
                       <aspectRatios jcr:primaryType="nt:unstructured">
                           <_x0031_6-10
                               jcr:primaryType="nt:unstructured"
                               name="16 : 10"
                               ratio="0.625"/>
                       </aspectRatios>
                   </crop>
               </plugins>
           </config>
   </cq:inplaceEditing>
   ```

   >[!CAUTION]
   >
   >AEM에서 자르기 비율은 `ratio` 속성에 의해 설정된 대로 **height/width**&#x200B;로 정의됩니다. 이것은 종래의 폭/높이 정의와 다르며, 레거시 호환성을 위해 수행됩니다. `name` 속성을 명확히 정의한 경우 이 속성이 UI에 표시되므로 작성 사용자가 차이를 알지 못합니다.

#### 새 즉석 편집기 만들기 {#creating-a-new-in-place-editor}

clientlib 내에서 새로운 즉석 편집기를 구현하려면 다음을 수행하십시오.

>[!NOTE]
>
>예를 들어 다음을 참조하십시오.
>`/libs/cq/gui/components/authoring/editors/clientlibs/core/js/editors/editorExample.js`

1. 구현:

   * `setUp`
   * `tearDown`

1. 편집기를 등록합니다(생성자 포함).

   * `editor.register`

1. 편집기를 사용할 수 있는 모든 리소스 유형(구성 요소에서처럼) 간의 연결을 제공합니다.

#### 새 즉석 편집기를 만들기 위한 코드 샘플 {#code-sample-for-creating-a-new-in-place-editor}

`aem-authoring-extension-inplace-editor` 는 AEM에서 새 즉석 편집기를 만드는 방법을 보여주는 샘플 패키지입니다.

GITHUB의 코드

GitHub에서 이 페이지의 코드를 찾을 수 있습니다

* [GitHub에서 aem-authoring-extension-inplace-editor 프로젝트를 엽니다.](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-inplace-editor)
* 프로젝트를 [ZIP 파일](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-inplace-editor/archive/master.zip)로 다운로드합니다

#### 여러 즉석 편집기 구성 {#configuring-multiple-in-place-editors}

여러 즉석 편집기가 있도록 구성 요소를 구성할 수 있습니다. 여러 즉석 편집기가 구성된 경우 적절한 컨텐츠를 선택하고 적절한 편집기를 열 수 있습니다. 자세한 내용은 [여러 즉석 편집기 구성](/help/sites-developing/multiple-inplace-editors.md) 설명서를 참조하십시오.

## 새 페이지 작업 추가 {#add-a-new-page-action}

페이지 도구 모음에 새 페이지 작업을 추가하려면, 예를 들어 **Back to Sites** (콘솔) 작업을 수행합니다.

### 코드 샘플 {#code-sample-3}

`aem-authoring-extension-header-backtosites` 는 사이트 콘솔로 다시 이동하는 사용자 지정 헤더 막대 작업을 만드는 방법을 보여주는 샘플 패키지입니다.

GITHUB의 코드

GitHub에서 이 페이지의 코드를 찾을 수 있습니다

* [GitHub에서 aem-authoring-extension-header-backtosites 프로젝트를 엽니다.](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-header-backtosites)
* 프로젝트를 [ZIP 파일](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-header-backtosites/archive/master.zip)로 다운로드합니다

## 활성화 요청 워크플로우 사용자 정의 {#customizing-the-request-for-activation-workflow}

즉시 사용 가능한 워크플로우 **활성화 요청**:

* 컨텐츠 작성자 **에 적절한 복제 권한이 없지만**&#x200B;에 DAM-사용자 및 작성자의&#x200B;**멤버십이 있으면 적절한 메뉴에 자동으로 표시됩니다.**

* 복제 권한이 제거되므로 표시되지 않습니다.

이러한 활성화에서 사용자 지정된 동작을 갖도록 하려면 **활성화 요청** 워크플로우를 오버레이할 수 있습니다.

1. `/apps`에서 **사이트** 마법사를 오버레이합니다.

   `/libs/wcm/core/content/common/managepublicationwizard`

   >[!NOTE]
   >
   >이 자체는 다음과 같은 공통 인스턴스를 무시합니다.
   >
   >`/libs/cq/gui/content/common/managepublicationwizard`

1. 필요에 따라 [워크플로우 모델](/help/sites-developing/workflows-models.md) 및 관련 구성/스크립트를 업데이트합니다.
1. 모든 관련 페이지에 대한 적절한 사용자에서 [ `replicate` 작업](/help/sites-administering/security.md#actions)에 대한 권한을 제거합니다. 사용자가 페이지를 게시(또는 복제하려고 할 때 이 워크플로우를 기본 작업으로 트리거하도록 합니다.
