---
title: 페이지 작성 사용자 정의
seo-title: 페이지 작성 사용자 정의
description: AEM에서는 페이지 작성 기능을 사용자 지정할 수 있도록 다양한 메커니즘을 제공합니다
seo-description: AEM에서는 페이지 작성 기능을 사용자 지정할 수 있도록 다양한 메커니즘을 제공합니다
uuid: 9dc72d98-c5ff-4a00-b367-688ccf896526
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: 6825dcd6-fa75-4410-b6b2-e7bd4a391224
translation-type: tm+mt
source-git-commit: 5128a08d4db21cda821de0698b0ac63ceed24379

---


# 페이지 작성 사용자 정의{#customizing-page-authoring}

>[!CAUTION]
>
>이 문서에서는 터치가 활성화된 최신 UI에서 페이지 작성을 사용자 지정하는 방법에 대해 설명하고 클래식 UI에는 적용되지 않습니다.

AEM에서는 작성 인스턴스의 페이지 작성 기능(및 [콘솔](/help/sites-developing/customizing-consoles-touch.md))을 사용자 지정할 수 있도록 하는 다양한 메커니즘을 제공합니다.

* Clientlibs

   Clientlibs를 사용하면 표준 함수, 개체 및 메서드를 재사용하는 동안 기본 구현을 확장하여 새로운 기능을 구현할 수 있습니다. 사용자 정의할 때 새 clientlib의 필수 조건 아래에 `/apps.` 사용자 자신의 clientlib을 만들 수 있습니다.

   * authoring clientlib에 따라 다름 `cq.authoring.editor.sites.page`
   * 해당 `cq.authoring.editor.sites.page.hook` 카테고리에 속함

* 오버레이

   Overlays는 노드 정의를 기반으로 하며, 표준 기능(in `/libs`)을 사용자 정의된 기능(in)과 오버레이할 수 `/apps`있습니다. 오버레이를 만들 때는 [슬링 리소스 병합에서](/help/sites-developing/sling-resource-merger.md) 상속을 허용하므로 원본의 1:1 사본이 필요하지 않습니다.

>[!NOTE]
>
>자세한 내용은 JS [설명서 세트를](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/jsdoc/ui-touch/editor-core/index.html)참조하십시오.

AEM 인스턴스에서 페이지 작성 기능을 확장하는 데 여러 가지 방법으로 사용할 수 있습니다. 선택 항목은 아래에서 수준 높은 순서로 표시됩니다.

>[!NOTE]
>
>자세한 내용은 다음을 참조하십시오.
>
>* clientlibs 사용 및 [만들기](/help/sites-developing/clientlibs.md).
>* 오버레이 [사용 및 만들기](/help/sites-developing/overlays.md).
>* [Granite](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/index.html)
>* [AEM Touch-Enabled UI의 구조를](/help/sites-developing/touch-ui-structure.md) 참조하십시오.
>
>
이 항목에서는 AEM Gems 세션 - [AEM](https://docs.adobe.com/content/ddc/en/gems.html) 6.0 [에 대한 사용자 인터페이스 맞춤화에도 설명되어 있습니다](https://helpx.adobe.com/experience-manager/kt/eseminars/gems/aem-user-interface-customization-for-aem6.html).

>[!CAUTION]
>
>패스에 있는 ***어떤 것도 변경하지*** 않아야 `/libs` 합니다.
>
>이는 다음에 인스턴스를 업그레이드할 때 의 컨텐츠를 `/libs` 덮어쓰게 되기 때문입니다(핫픽스 또는 기능 팩을 적용할 때 덮어쓸 수 있음).
>
>구성 및 기타 변경에 대한 권장 방법은 다음과 같습니다.
>
>1. 필요한 항목(즉, 있는 대로)을 `/libs``/apps`
>1. Make any changes within `/apps`


## 새 레이어 추가(모드) {#add-new-layer-mode}

페이지를 편집할 때 다양한 [모드를](/help/sites-authoring/author-environment-tools.md#page-modes) 사용할 수 있습니다. 이러한 모드는 [레이어를](/help/sites-developing/touch-ui-structure.md#layer)사용하여 구현됩니다. 이러한 기능을 사용하면 동일한 페이지 컨텐츠에 대해 서로 다른 유형의 기능에 액세스할 수 있습니다. 표준 레이어는 다음과 같습니다.편집, 미리 보기, 주석 달기, 개발자 및 타깃팅

### 레이어 예:Live Copy 상태 {#layer-example-live-copy-status}

표준 AEM 인스턴스는 MSM 레이어를 제공합니다. 이렇게 하면 [다중 사이트 관리와](/help/sites-administering/msm.md) 관련된 데이터에 액세스하고 레이어에서 강조 표시됩니다.

We.Retail 언어 복사 [페이지(또는 기타 Live](/help/sites-developing/we-retail-globalized-site-structure.md) Copy 페이지)를 편집하고 Live Copy 상태 **모드를 선택할 수 있습니다** .

MSM 레이어 정의(참조용)는

`/libs/wcm/msm/content/touch-ui/authoring/editor/js/msm.Layer.js`

### 코드 샘플 {#code-sample}

MSM 보기에 대한 새 레이어인 새 레이어(모드)를 만드는 방법을 보여주는 샘플 패키지입니다.

GITHUB에 대한 코드

GitHub에서 이 페이지의 코드를 찾을 수 있습니다

* [GitHub에서 aem-authoring-new-layer-mode 프로젝트 열기](https://github.com/Adobe-Marketing-Cloud/aem-authoring-new-layer-mode)
* 프로젝트를 ZIP [파일로 다운로드](https://github.com/Adobe-Marketing-Cloud/aem-authoring-new-layer-mode/archive/master.zip)

## 자산 브라우저에 새 선택 범주 추가 {#add-new-selection-category-to-asset-browser}

자산 브라우저는 다양한 유형/범주(예: 이미지, 문서 등)의 자산을 표시합니다. 이러한 자산 카테고리로 자산을 필터링할 수도 있습니다.

### 코드 샘플 {#code-sample-1}

`aem-authoring-extension-assetfinder-flickr` 는 자산 파인더에 새 그룹을 추가하는 방법을 보여주는 샘플 패키지입니다. 이 예는 Flickr [의](https://www.flickr.com)공개 스트림에 연결하여 사이드 패널에 표시합니다.

GITHUB에 대한 코드

GitHub에서 이 페이지의 코드를 찾을 수 있습니다

* [GitHub에서 aem-authoring-extension-assets-flickr 프로젝트 열기](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-assetfinder-flickr)
* 프로젝트를 ZIP [파일로 다운로드](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-assetfinder-flickr/archive/master.zip)

## 리소스 필터링 {#filtering-resources}

페이지를 작성할 때 리소스(예: 페이지, 구성 요소, 자산 등)에서 선택해야 하는 경우가 많습니다. 예를 들어 작성자가 항목을 선택해야 하는 목록 형식을 사용할 수 있습니다.

적절한 크기로 유지하거나 사용 사례와 관련되도록 필터를 사용자 지정 술어의 형태로 구현할 수 있습니다. 예를 들어 [ [`pathbrowser`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html) 화강암 [](/help/sites-developing/touch-ui-concepts.md#granite-ui) ] 구성 요소를 사용하여 사용자가 특정 리소스의 경로를 선택할 수 있는 경우 표시된 경로를 다음과 같이 필터링할 수 있습니다.

* 인터페이스를 구현하여 사용자 지정 조건자를 구현합니다. [`com.day.cq.commons.predicate.AbstractNodePredicate`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/commons/predicate/package-summary.html)
* 조건자의 이름을 지정하고, 조건자를 사용할 때 해당 이름을 `pathbrowser`참조하십시오.

사용자 지정 설명 만들기에 대한 자세한 내용은 [이 문서를](/help/sites-developing/implementing-custom-predicate-evaluator.md)참조하십시오.

>[!NOTE]
>
>인터페이스를 구현하여 사용자 지정 설명 구현은 클래식 UI에서도 작동합니다. `com.day.cq.commons.predicate.AbstractNodePredicate`
>
>클래식 UI에서 사용자 지정 설명 구현의 예는 [이 기술 자료 문서를](https://helpx.adobe.com/experience-manager/using/creating-custom-cq-tree.html) 참조하십시오.

## 구성 요소 도구 모음에 새 작업 추가 {#add-new-action-to-a-component-toolbar}

각 구성 요소(일반적으로)에는 해당 구성 요소에서 수행할 수 있는 작업 범위에 대한 액세스를 제공하는 도구 모음이 있습니다.

### 코드 샘플 {#code-sample-2}

`aem-authoring-extension-toolbar-screenshot` 은 구성 요소를 렌더링하기 위한 사용자 정의 도구 모음 작업을 만드는 방법을 보여주는 샘플 패키지입니다.

GITHUB에 대한 코드

GitHub에서 이 페이지의 코드를 찾을 수 있습니다

* [GitHub에서 aem-authoring-extension-toolbar-스크린샷 프로젝트 열기](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-toolbar-screenshot)
* 프로젝트를 ZIP [파일로 다운로드](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-toolbar-screenshot/archive/master.zip)

## 새 즉석 편집기 추가 {#add-new-in-place-editor}

### 표준 즉석 편집기 {#standard-in-place-editor}

표준 AEM 설치:

1. `/libs/cq/gui/components/authoring/editors/clientlibs/core/js/editors/editorExample.js`

   사용 가능한 다양한 편집기의 정의를 보관합니다.

1. 편집기와 각 리소스 유형(구성 요소에서와 마찬가지로) 간에 이 리소스를 사용할 수 있습니다.

   * `cq:inplaceEditing`

      예:

      * `/libs/foundation/components/text/cq:editConfig`
      * `/libs/foundation/components/image/cq:editConfig`

         * 속성: `editorType`

            해당 구성 요소에 대해 즉석 편집이 트리거될 때 사용할 인라인 편집기 유형을 정의합니다.예: `text``textimage`, `image`3 `title`.

1. 편집기의 추가 구성 세부 사항은 구성이 포함된 `config` 노드 및 필요한 플러그인 구성 세부 사항을 포함하는 추가 `plugin` 노드를 사용하여 구성할 수 있습니다.

   다음은 이미지 구성 요소의 이미지 자르기 플러그인에 대한 종횡비를 정의하는 예입니다. 화면 크기가 매우 제한되어 있기 때문에 자르기 적용 비율이 전체 화면 편집기로 이동되었으며 여기에서 볼 수만 있습니다.

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
   >AEM 자르기 비율에서는 `ratio` 속성에 의해 설정된 대로 **높이/폭으로**&#x200B;정의됩니다. 이것은 종래의 폭/높이 정의와 다르며, 레거시 호환성을 위해 수행됩니다. The authoring users will not be aware of any difference provided you define the `name` property clearly since this is what is displayed in the UI.

#### 새 즉석 편집기 만들기 {#creating-a-new-in-place-editor}

새 즉석 편집기를 구현하려면(clientlib 내에서):

>[!NOTE]
>
>예를 들면 다음을 참조하십시오.
>`/libs/cq/gui/components/authoring/editors/clientlibs/core/js/editors/editorExample.js`

1. 구현:

   * `setUp`
   * `tearDown`

1. 편집기 등록(생성자 포함):

   * `editor.register`

1. 편집기와 이를 사용할 수 있는 모든 리소스 유형(구성 요소에서처럼) 간의 연결을 제공합니다.

#### 새 즉석 편집기를 만들기 위한 코드 샘플 {#code-sample-for-creating-a-new-in-place-editor}

`aem-authoring-extension-inplace-editor` 는 AEM에서 새 즉석 편집기를 만드는 방법을 보여주는 샘플 패키지입니다.

GITHUB에 대한 코드

GitHub에서 이 페이지의 코드를 찾을 수 있습니다

* [GitHub에서 aem-authoring-extension-inplace-editor 프로젝트 열기](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-inplace-editor)
* 프로젝트를 ZIP [파일로 다운로드](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-inplace-editor/archive/master.zip)

#### 여러 즉석 편집기 구성 {#configuring-multiple-in-place-editors}

구성 요소에 여러 즉석 편집기가 있도록 구성 요소를 구성할 수 있습니다. 여러 즉석 편집기가 구성된 경우 적절한 컨텐츠를 선택하고 적절한 편집기를 열 수 있습니다. 자세한 [내용은 여러 즉석 편집기](/help/sites-developing/multiple-inplace-editors.md) 구성 설명서를 참조하십시오.

## 새 페이지 작업 추가 {#add-a-new-page-action}

페이지 도구 모음에 새 페이지 작업을 추가하려면(예: 사이트에 **돌아가기** (콘솔) 작업).

### 코드 샘플 {#code-sample-3}

`aem-authoring-extension-header-backtosites` 는 사이트 콘솔로 다시 이동할 사용자 정의 헤더 막대 작업을 만드는 방법을 보여주는 샘플 패키지입니다.

GITHUB에 대한 코드

GitHub에서 이 페이지의 코드를 찾을 수 있습니다

* [GitHub에서 aem-authoring-extension-header-backtosites 프로젝트 열기](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-header-backtosites)
* 프로젝트를 ZIP [파일로 다운로드](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-header-backtosites/archive/master.zip)

## 활성화 요청 워크플로우 사용자 정의 {#customizing-the-request-for-activation-workflow}

즉시 사용 가능한 워크플로우인 **활성화**&#x200B;요청은 컨텐츠 작성자에게 적절한 복제 권한이 없을 때 자동으로 트리거됩니다.

활성화 요청 워크플로우를 오버레이하면 활성화 **요청을 수행할 수** 있습니다.

1. 오버레이에서 사이트 `/apps` 마법사를 **** 사용합니다.

   `/libs/wcm/core/content/common/managepublicationwizard`

   >[!NOTE]
   >
   >이 자체는 다음과 같은 일반적인 인스턴스를 무시합니다.
   >
   >`/libs/cq/gui/content/common/managepublicationwizard`

1. 필요에 따라 [워크플로우 모델](/help/sites-developing/workflows-models.md) 및 관련 구성/스크립트를 업데이트합니다.
1. 모든 관련 페이지에 대한 모든 적절한 사용자로부터 [ 작업에 `replicate`](/help/sites-administering/security.md#actions) 대한 권한을 제거합니다.사용자가 페이지를 게시(또는 복제하려고 할 때 이 워크플로우를 기본 작업으로 트리거하도록 합니다.

