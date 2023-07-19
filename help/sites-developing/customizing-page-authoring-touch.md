---
title: 페이지 작성 사용자 지정
seo-title: Customizing Page Authoring
description: AEM은 페이지 작성 기능을 사용자 지정할 수 있는 다양한 메커니즘을 제공합니다
seo-description: AEM provides various mechanisms to enable you to customize page authoring functionality
uuid: 9dc72d98-c5ff-4a00-b367-688ccf896526
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: extending-aem
content-type: reference
discoiquuid: 6825dcd6-fa75-4410-b6b2-e7bd4a391224
exl-id: 90594588-db8e-4d4c-a208-22c1c6ea2a2d
source-git-commit: 259f257964829b65bb71b5a46583997581a91a4e
workflow-type: tm+mt
source-wordcount: '1357'
ht-degree: 1%

---

# 페이지 작성 사용자 지정{#customizing-page-authoring}

>[!CAUTION]
>
>이 문서는 최신 터치 지원 UI에서 페이지 작성을 사용자 지정하는 방법에 대해 설명하며, 클래식 UI에는 적용되지 않습니다.

AEM은 페이지 작성 기능 및 [콘솔](/help/sites-developing/customizing-consoles-touch.md))을 참조하십시오.

* Clientlibs

  Clientlib을 사용하면 기본 구현을 확장하여 새로운 기능을 구현하는 동시에 표준 함수, 개체 및 메서드를 재사용할 수 있습니다. 를 사용자 지정할 때 `/apps.` 새 clientlib은 다음 작업을 수행해야 합니다.

   * authoring clientlib에 따라 다름 `cq.authoring.editor.sites.page`
   * 적절한 것의 일부가 되다 `cq.authoring.editor.sites.page.hook` 범주

* 오버레이

  오버레이는 노드 정의를 기반으로 하며, 를 사용하여 표준 기능을 오버레이할 수 있습니다. `/libs`)를 사용하십시오(에서). `/apps`). 오버레이를 만들 때 다음과 같이 원본의 1:1 사본이 필요하지 않습니다. [sling 리소스 병합](/help/sites-developing/sling-resource-merger.md) 상속을 허용합니다.

>[!NOTE]
>
>자세한 내용은 [JS 설명서 세트](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/jsdoc/ui-touch/editor-core/index.html).

여러 가지 방법으로 AEM 인스턴스의 페이지 작성 기능을 확장할 수 있습니다. 선택 내용은 아래에 나와 있습니다(높은 수준에서).

>[!NOTE]
>
>자세한 내용은 다음을 참조하십시오.
>
>* 사용 및 만들기 [clientlibs](/help/sites-developing/clientlibs.md).
>* 사용 및 만들기 [오버레이](/help/sites-developing/overlays.md).
>* [Granite](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/jcr_root/libs/granite/ui/index.html)
>* [AEM 터치 지원 UI의 구조](/help/sites-developing/touch-ui-structure.md) 페이지 작성에 사용되는 구조적 영역에 대한 세부 정보.
>


>[!CAUTION]
>
>본인 ***필수*** 의 아무 것도 변경하지 마십시오. `/libs` 경로.
>
>이는 의 콘텐츠가 `/libs` 는 다음에 인스턴스를 업그레이드할 때 덮어쓰기됩니다(또한 핫픽스 또는 기능 팩을 적용할 때 덮어쓰기될 수도 있음).
>
>구성 및 기타 변경에 권장되는 방법은 다음과 같습니다.
>
>1. 필요한 항목(예:에 존재하는 대로)을 다시 생성합니다. `/libs`) `/apps`
>1. 다음 범위 내에서 변경 `/apps`

## 새 레이어 추가(모드) {#add-new-layer-mode}

페이지를 편집할 때 다양한 옵션이 있습니다 [모드](/help/sites-authoring/author-environment-tools.md#page-modes) 사용 가능. 이러한 모드는 를 사용하여 구현됩니다 [레이어](/help/sites-developing/touch-ui-structure.md#layer). 이를 통해 동일한 페이지 콘텐츠에 대해 서로 다른 유형의 기능에 액세스할 수 있습니다. 표준 레이어는 편집, 미리보기, 주석 달기, 개발자 및 타겟팅입니다.

### 레이어 예: Live Copy 상태 {#layer-example-live-copy-status}

표준 AEM 인스턴스는 MSM 계층을 제공합니다. 관련 데이터에 액세스합니다. [다중 사이트 관리](/help/sites-administering/msm.md) 레이어에서 강조 표시됩니다.

작업을 보려면 다음을 편집할 수 있습니다. [We.Retail 언어 사본](/help/sites-developing/we-retail-globalized-site-structure.md) 페이지(또는 다른 라이브 카피 페이지)를 선택하고 **Live Copy 상태** 모드.

MSM 레이어 정의(참조용)는에서 찾을 수 있습니다.

`/libs/wcm/msm/content/touch-ui/authoring/editor/js/msm.Layer.js`

### 코드 샘플 {#code-sample}

MSM 보기의 새 레이어인 새 레이어(모드)를 만드는 방법을 보여주는 샘플 패키지입니다.

GITHUB의 코드

GitHub에서 이 페이지의 코드를 확인할 수 있습니다

* [GitHub에서 aem 작성-새 레이어 모드 프로젝트 열기](https://github.com/Adobe-Marketing-Cloud/aem-authoring-new-layer-mode)
* 다음으로 프로젝트 다운로드 [ZIP 파일](https://github.com/Adobe-Marketing-Cloud/aem-authoring-new-layer-mode/archive/master.zip)

## 자산 브라우저에 새 선택 범주 추가 {#add-new-selection-category-to-asset-browser}

에셋 브라우저에는 다양한 유형/카테고리(예: 이미지, 문서 등)의 에셋이 표시됩니다. 자산은 이러한 자산 카테고리로 필터링할 수도 있습니다.

### 코드 샘플 {#code-sample-1}

`aem-authoring-extension-assetfinder-flickr` 는 에셋 파인더에 새 그룹을 추가하는 방법을 보여 주는 샘플 패키지입니다. 이 예는에 연결합니다. [Flickr](https://www.flickr.com)의 공개 스트림과 사이드 패널에 표시합니다.

GITHUB의 코드

GitHub에서 이 페이지의 코드를 확인할 수 있습니다

* [GitHub에서 aem-authoring-extension-assetfinder-flickr 프로젝트 열기](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-assetfinder-flickr)
* 다음으로 프로젝트 다운로드 [ZIP 파일](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-assetfinder-flickr/archive/master.zip)

## 리소스 필터링 {#filtering-resources}

페이지를 작성할 때 리소스(예: 페이지, 구성 요소, 에셋 등)에서 선택해야 하는 경우가 많습니다. 예를 들어 작성자가 항목을 선택해야 하는 목록 형식을 취할 수 있습니다.

목록을 적절한 크기로 유지하고 사용 사례와 관련이 있도록 맞춤형 술어 형식으로 필터를 구현할 수 있습니다. 예를 들어 [`pathbrowser`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/granite-ui/api/index.html) [Granite](/help/sites-developing/touch-ui-concepts.md#granite-ui) 구성 요소를 사용하여 사용자가 특정 리소스에 대한 경로를 선택할 수 있습니다. 제공된 경로는 다음과 같은 방식으로 필터링될 수 있습니다.

* 를 구현하여 사용자 지정 술어 구현 [`com.day.cq.commons.predicate.AbstractNodePredicate`](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/commons/predicate/package-summary.html) 인터페이스.
* 술어 이름을 지정하고, 을 사용할 때 해당 이름을 참조합니다. `pathbrowser`.

사용자 지정 술어 만들기에 대한 자세한 내용은 [이 문서](/help/sites-developing/implementing-custom-predicate-evaluator.md).

>[!NOTE]
>
>를 구현하여 사용자 정의 술어 구현 `com.day.cq.commons.predicate.AbstractNodePredicate` 인터페이스는 클래식 UI에서도 작동합니다.
>
>다음을 참조하십시오 [이 기술 자료 문서](https://helpx.adobe.com/experience-manager/using/creating-custom-cq-tree.html) 클래식 UI에서 사용자 지정 술어를 구현하는 방법의 예입니다.

## 구성 요소 도구 모음에 새 작업 추가 {#add-new-action-to-a-component-toolbar}

각 구성 요소(일반적으로)에는 해당 구성 요소에서 수행할 수 있는 작업 범위에 대한 액세스를 제공하는 도구 모음이 있습니다.

### 코드 샘플 {#code-sample-2}

`aem-authoring-extension-toolbar-screenshot` 는 구성 요소를 렌더링하기 위해 사용자 지정 도구 모음 작업을 만드는 방법을 보여 주는 샘플 패키지입니다.

GITHUB의 코드

GitHub에서 이 페이지의 코드를 확인할 수 있습니다

* [GitHub에서 aem 작성-확장 도구 모음-스크린샷 프로젝트 열기](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-toolbar-screenshot)
* 다음으로 프로젝트 다운로드 [ZIP 파일](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-toolbar-screenshot/archive/master.zip)

## 새로운 즉석 편집기 추가 {#add-new-in-place-editor}

### 표준 즉석 편집기 {#standard-in-place-editor}

표준 AEM 설치에서

1. `/libs/cq/gui/components/authoring/editors/clientlibs/core/js/editors/editorExample.js`

   사용 가능한 다양한 편집기에 대한 정의를 보관합니다.

1. 편집기와 이를 사용할 수 있는 각 리소스 유형(구성 요소에서와 같이) 간에 연결이 있습니다.

   * `cq:inplaceEditing`

     예:

      * `/libs/foundation/components/text/cq:editConfig`
      * `/libs/foundation/components/image/cq:editConfig`

         * 속성: `editorType`

           해당 구성 요소에 대해 즉석 편집이 트리거될 때 사용할 인라인 편집기 유형을 정의합니다. 예: `text`, `textimage`, `image`, `title`.

1. 편집기의 추가 구성 세부 정보는 `config` 구성은 물론 추가 구성이 포함된 노드 `plugin` 필요한 플러그인 구성 세부 정보를 포함할 노드입니다.

   다음은 이미지 구성 요소의 이미지 자르기 플러그인에 대한 종횡비를 정의하는 예입니다. 매우 제한된 화면 크기의 가능성 때문에 자르기 대상 비율이 전체 화면 편집기로 이동되었으며 해당 편집기에서만 볼 수 있습니다.

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
   >AEM 자르기 비율에서 다음을 통해 설정합니다. `ratio` 속성은 다음과 같이 정의됩니다. **높이/폭**. 이것은 종래의 폭/높이 정의와 다르며, 레거시 호환성을 위해 수행됩니다. 사용자가 를 정의한 경우 작성 사용자가 차이를 알지 못합니다. `name` 속성이 UI에 표시되므로 명확하게 알 수 있습니다.

#### 새로운 즉석 편집기 만들기 {#creating-a-new-in-place-editor}

새로운 즉석 편집기를 구현하려면(clientlib 내에서):

>[!NOTE]
>
>예를 들어 다음을 참조하십시오.
>`/libs/cq/gui/components/authoring/editors/clientlibs/core/js/editors/editorExample.js`

1. 구현:

   * `setUp`
   * `tearDown`

1. 편집기 등록(생성자 포함):

   * `editor.register`

1. 편집기와 이를 사용할 수 있는 모든 리소스 유형(구성 요소에서와 같이) 간의 연결을 제공합니다.

#### 새로운 즉석 편집기를 만들기 위한 코드 샘플 {#code-sample-for-creating-a-new-in-place-editor}

`aem-authoring-extension-inplace-editor` 는 AEM에서 새로운 즉석 편집기를 만드는 방법을 보여 주는 샘플 패키지입니다.

GITHUB의 코드

GitHub에서 이 페이지의 코드를 확인할 수 있습니다

* [GitHub에서 aem-authoring-extension-inplace-editor 프로젝트 열기](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-inplace-editor)
* 다음으로 프로젝트 다운로드 [ZIP 파일](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-inplace-editor/archive/master.zip)

#### 여러 즉석 편집기 구성 {#configuring-multiple-in-place-editors}

구성 요소에 여러 개의 즉석 편집기가 있도록 구성할 수 있습니다. 여러 즉석 편집기가 구성된 경우 적절한 콘텐츠를 선택하고 적절한 편집기를 열 수 있습니다. 다음을 참조하십시오. [여러 즉석 편집기 구성](/help/sites-developing/multiple-inplace-editors.md) 설명서 를 참조하십시오.

## 새 페이지 작업 추가 {#add-a-new-page-action}

페이지 도구 모음에 새 페이지 작업을 추가하려면(예: ) **사이트로 돌아가기** (콘솔) 작업.

### 코드 샘플 {#code-sample-3}

`aem-authoring-extension-header-backtosites` 는 사이트 콘솔로 다시 이동하기 위해 사용자 지정 헤더 막대 작업을 만드는 방법을 보여 주는 샘플 패키지입니다.

GITHUB의 코드

GitHub에서 이 페이지의 코드를 확인할 수 있습니다

* [GitHub에서 aem-authoring-extension-header-backtosites 프로젝트 열기](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-header-backtosites)
* 다음으로 프로젝트 다운로드 [ZIP 파일](https://github.com/Adobe-Marketing-Cloud/aem-authoring-extension-header-backtosites/archive/master.zip)

## 활성화 요청 워크플로 사용자 지정 {#customizing-the-request-for-activation-workflow}

기본 워크플로우 **활성화 요청**:

* 콘텐츠 작성자는 적절한 메뉴에 자동으로 표시됩니다. **이(가) 다음을 포함하지 않음** 적절한 복제 권한이지만 **다음을 포함** DAM 사용자 및 작성자의 멤버십.

* 그렇지 않으면 복제 권한이 제거되어 아무 것도 표시되지 않습니다.

이러한 활성화 시 사용자 지정된 비헤이비어를 만들려면 **활성화 요청** 워크플로:

1. 위치 `/apps` 오버레이 **사이트** 마법사:

   `/libs/wcm/core/content/common/managepublicationwizard`

   >[!NOTE]
   >
   >이 인스턴스 자체는 의 일반 인스턴스를 무시합니다.
   >
   >`/libs/cq/gui/content/common/managepublicationwizard`

1. 업데이트 [워크플로 모델](/help/sites-developing/workflows-models.md) 필요에 따라 관련 구성/스크립트를 작성합니다.
1. 에 대한 권한 제거 [`replicate` 작업](/help/sites-administering/security.md#actions) 모든 관련 페이지에 대한 모든 적절한 사용자로부터; 모든 사용자가 페이지를 게시(또는 복제)하려고 할 때 이 워크플로가 기본 작업으로 트리거되도록 하기 위한 것입니다.
