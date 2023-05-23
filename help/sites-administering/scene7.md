---
title: Adobe Experience Manager과 Dynamic Media Classic 통합
description: Adobe Experience Manager을 Dynamic Media Classic과 통합하는 방법을 알아봅니다.
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
exl-id: f244cfb5-5550-4f20-92f0-bb296e2bf76e
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: tm+mt
source-wordcount: '5484'
ht-degree: 1%

---

# Adobe Experience Manager과 Dynamic Media Classic 통합 {#integrating-with-dynamic-media-classic-scene}

Adobe Dynamic Media Classic은 리치 미디어 자산을 웹, 모바일, 이메일 및 인터넷에 연결된 디스플레이와 인쇄로 관리, 향상, 게시 및 전달하기 위한 호스팅 솔루션입니다.

Dynamic Media Classic을 사용하려면 Dynamic Media Classic과 Adobe Experience Manager Assets가 서로 상호 작용할 수 있도록 클라우드 구성을 구성해야 합니다. 이 문서에서는 Experience Manager 및 Dynamic Media Classic을 구성하는 방법에 대해 설명합니다.

페이지에서 모든 Dynamic Media Classic 구성 요소를 사용하고 비디오 작업에 대한 자세한 내용은 을 참조하십시오. [Dynamic Media Classic 사용](../assets/scene7.md).

>[!NOTE]
>
>* Dynamic Media Classic의 DHTML 뷰어 플랫폼은 2014년 1월 31일에 공식적으로 사용이 종료되었습니다. 자세한 내용은 [DHTML 뷰어 지원 중단 FAQ](../sites-administering/dhtml-viewer-endoflifefaqs.md).
>* Experience Manager에서 작동하도록 Dynamic Media Classic을 구성하기 전에 다음을 참조하십시오. [우수 사례](#best-practices-for-integrating-scene-with-aem) Dynamic Media Classic과 Experience Manager 통합
>* Experience Manager의 일부 기능은 3.x API를 사용하고 다른 기능은 4.x API를 사용하므로 Dynamic Media Classic을 사용자 지정 프록시 구성과 함께 사용하는 경우 HTTP 클라이언트 프록시 구성을 모두 구성해야 합니다. 3.x은(는) [http://localhost:4502/system/console/configMgr/com.day.commons.httpclient](http://localhost:4502/system/console/configMgr/com.day.commons.httpclient) 및 4.x는 [http://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator](http://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator).
>


## Experience Manager/Dynamic Media Classic 통합 대 Dynamic Media {#aem-scene-integration-versus-dynamic-media}

Experience Manager 사용자는 Dynamic Media에서 사용할 두 가지 솔루션 중에서 선택할 수 있습니다. 다음 중 하나를 사용할 수 있습니다.

* Experience Manager 인스턴스를 Dynamic Media Classic과 통합합니다.
* Experience Manager에 통합된 Dynamic Media을 사용합니다.

선택할 솔루션을 결정하려면 다음 기준을 사용하십시오.

* 다음 중 하나입니까? **기존** 게시 및 전달을 위해 자산이 Dynamic Media Classic에 있지만 이러한 자산을 사이트(WCM) 작성 또는 Experience Manager Assets과 통합하려는 Dynamic Media Classic 고객 이 경우 [Experience Manager/Dynamic Media Classic 지점 간 통합](#aem-scene-point-to-point-integration) 이 문서에 설명되어 있습니다.

* 다음과 같은 경우 **신규** 리치 미디어 제공 요구 사항이 있는 Experience Manager 고객이 [Dynamic Media 옵션](#aem-dynamic-media). 이 옵션은 기존 S7 계정이 없고 해당 시스템에 많은 자산이 저장된 경우에 가장 적합합니다.

* 경우에 따라 두 솔루션을 모두 사용합니다. 다음 [이중 사용 시나리오](/help/sites-administering/scene7.md#dual-use-scenario) 은 해당 시나리오를 설명합니다.

### Experience Manager/Dynamic Media Classic 지점 간 통합 {#aem-scene-point-to-point-integration}

이 솔루션에서 에셋으로 작업할 때 다음 중 하나를 수행합니다.

* 에셋을 Dynamic Media Classic에 직접 업로드한 다음 를 통해 액세스합니다. **Dynamic Media Classic** 페이지 작성 또는
* Experience Manager Assets에 업로드한 다음 Dynamic Media Classic에 자동 게시를 활성화합니다. 다음을 통해 액세스합니다 **에셋** 페이지 작성용 컨텐츠 브라우저

이 통합에 사용하는 구성 요소는 **Dynamic Media Classic** 구성 요소 영역 [디자인 모드](/help/sites-authoring/author-environment-tools.md#page-modes).

### Dynamic Media Experience Manager {#aem-dynamic-media}

Experience Manager Dynamic Media은 Experience Manager 플랫폼 내에서 직접 Dynamic Media Classic 기능을 통합하는 것입니다.

이 솔루션에서 에셋으로 작업할 때 다음 워크플로를 따릅니다.

1. 단일 이미지 및 비디오 에셋을 Experience Manager에 바로 업로드할 수 있습니다.
1. Experience Manager 내에서 직접 비디오를 인코딩합니다.
1. Experience Manager 내에서 직접 이미지 기반 세트를 작성합니다.
1. 해당하는 경우 이미지 또는 비디오에 인터랙티브를 추가합니다.

Dynamic Media에 사용하는 구성 요소는 **[!UICONTROL Dynamic Media]** 구성 요소 영역 [디자인 모드](/help/sites-authoring/author-environment-tools.md#page-modes). 여기에는 다음이 포함됩니다.

* **[!UICONTROL Dynamic Media]** - **[!UICONTROL Dynamic Media]** 구성 요소는 편리하게도 이미지를 추가하는지 아니면 비디오를 추가하는지에 따라 사용 가능한 선택 사항이 달라집니다. 이 구성 요소는 이미지 사전 설정, 이미지 세트와 같은 이미지 기반 뷰어, 스핀 세트, 혼합 미디어 세트 및 비디오를 지원합니다. 또한 뷰어는 응답형이며 화면 크기는 화면 크기에 따라 자동으로 변경됩니다. 모든 뷰어는 HTML 5 뷰어입니다.

* **[!UICONTROL 대화형 미디어]** - **[!UICONTROL 대화형 미디어]** 구성 요소는 회전 배너, 대화형 이미지 및 대화형 비디오와 같은 에셋용입니다. 이러한 에셋은 핫스팟 또는 이미지 맵과 같은 상호 작용성이 있습니다. 이 구성 요소는 편리합니다. 즉, 이미지를 추가하는지 아니면 비디오를 추가하는지에 따라 다양한 옵션이 제공됩니다. 또한 뷰어는 응답형이며 화면 크기는 화면 크기에 따라 자동으로 변경됩니다. 모든 뷰어는 HTML 5 뷰어입니다.

### 이중 사용 시나리오 {#dual-use-scenario}

기본적으로 Experience Manager의 Dynamic Media 및 Dynamic Media Classic 통합 기능을 동시에 사용할 수 있습니다. 다음 사용 사례 표에서는 특정 영역을 켜거나 끌 때를 설명합니다.

Dynamic Media 및 Dynamic Media Classic을 동시에 사용하려면

1. 구성 [Dynamic Media Classic](#creating-a-cloud-configuration-for-scene) Cloud Services.
1. 사용 사례에 해당하는 특정 지침을 따르십시오.

   <table>
    <tbody>
    <tr>
    <td> </td>
    <td> </td>
    <td><strong>Dynamic Media</strong></td>
    <td> </td>
    <td><strong>Dynamic Media Classic 통합</strong></td>
    <td> </td>
    </tr>
    <tr>
    <td><strong>다음 작업을 수행하는 경우</strong></td>
    <td><strong>사용 사례 워크플로</strong></td>
    <td><strong>이미징/비디오</strong></td>
    <td><strong>Dynamic Media 구성 요소</strong></td>
    <td><strong>S7 컨텐츠 브라우저 및 구성 요소</strong></td>
    <td><strong>자산에서 S7로 자동 업로드</strong></td>
    </tr>
    <tr>
    <td>Sites 및 Dynamic Media의 새로운 기능</td>
    <td>에셋을 업로드하고 Experience Manager Experience Manager Dynamic Media 구성 요소를 사용하여 Sites 페이지에 에셋을 작성합니다</td>
    <td><p>사용</p> <p>(3단계 참조)</p> </td>
    <td><a href="/help/assets/adding-dynamic-media-assets-to-pages.md">사용</a></td>
    <td>끔</td>
    <td>끔</td>
    </tr>
    <tr>
    <td>소매 및 Sites 및 Dynamic Media의 새로운 기능</td>
    <td>관리 및 전달을 위해 Experience Manager에 비제품 자산을 업로드합니다. 제품 에셋을 Dynamic Media Classic에 업로드하고 Experience Manager 및 구성 요소의 Dynamic Media Classic 콘텐츠 브라우저를 사용하여 Sites의 제품 세부 사항 페이지를 작성합니다.</td>
    <td><p>사용</p> <p>(3단계 참조)</p> </td>
    <td><a href="/help/assets/adding-dynamic-media-assets-to-pages.md">사용</a></td>
    <td><a href="/help/assets/scene7.md#scene-content-browser">사용</a></td>
    <td>끔</td>
    </tr>
    <tr>
    <td>Assets 및 Dynamic Media의 새로운 기능</td>
    <td>에셋을 Experience Manager Assets에 업로드하고 Dynamic Media에서 게시된 URL/포함 코드를 사용합니다.</td>
    <td><p>사용</p> <p>(3단계 참조)</p> </td>
    <td>끔</td>
    <td>끔</td>
    <td>끔</td>
    </tr>
    <tr>
    <td>Dynamic Media 및 템플릿 처음 사용</td>
    <td>이미징 및 비디오에 Dynamic Media을 사용합니다. Dynamic Media Classic에서 이미지 템플릿을 작성하고 Dynamic Media Classic 콘텐츠 파인더를 사용하여 사이트 페이지에 템플릿을 포함합니다.</td>
    <td><p>사용</p> <p>(3단계 참조)</p> </td>
    <td><a href="/help/assets/adding-dynamic-media-assets-to-pages.md">사용</a></td>
    <td><a href="/help/assets/scene7.md#scene-content-browser">사용</a></td>
    <td>끔</td>
    </tr>
    <tr>
    <td>기존 Dynamic Media Classic 고객 및 Sites를 처음 사용하는 고객</td>
    <td>에셋을 Dynamic Media Classic에 업로드하고 Dynamic Media Classic 콘텐츠 브라우저 Experience Manager 를 사용하여 Sites 페이지에서 에셋을 검색하고 작성합니다</td>
    <td>끔</td>
    <td>끔</td>
    <td><a href="/help/assets/scene7.md#scene-content-browser">사용</a></td>
    <td>끔</td>
    </tr>
    <tr>
    <td>Sites 및 Assets를 처음 사용하는 기존 Dynamic Media Classic 고객</td>
    <td>자산을 DAM에 업로드하고 게재를 위해 Dynamic Media Classic에 자동으로 게시합니다. Experience Manager Dynamic Media Classic 콘텐츠 브라우저를 사용하여 Sites 페이지에서 에셋을 검색하고 작성할 수 있습니다.</td>
    <td>끔</td>
    <td>끔</td>
    <td><a href="/help/assets/scene7.md#scene-content-browser">사용</a></td>
    <td><p><a href="#configuringautouploadingfromaemassets">사용</a></p> <p>(4단계 참조)</p> </td>
    </tr>
    <tr>
    <td>기존 Dynamic Media Classic 고객 및 Assets 신규 고객</td>
    <td><p>Experience Manager에 에셋을 업로드하고 Dynamic Media을 사용하여 다운로드/공유를 위한 렌디션을 생성합니다. 게재를 위해 Experience Manager 에셋을 Dynamic Media Classic에 자동으로 게시합니다.</p> <p><strong>중요 사항:</strong> 중복 처리가 발생하고 Experience Manager에서 생성된 렌디션이 Dynamic Media Classic에 동기화되지 않음</p> </td>
    <td><p>사용</p> <p>(3단계 참조)</p> </td>
    <td>끔</td>
    <td>끔</td>
    <td><p><a href="#configuringautouploadingfromaemassets">사용</a></p> <p>(4단계 참조)</p> </td>
    </tr>
    </tbody>
    </table>

1. (선택 사항, 사용 사례 표 참조) - [Dynamic Media 클라우드 구성](/help/assets/config-dynamic.md) 및 [Dynamic Media 서버 활성화](/help/assets/config-dynamic.md).
1. (선택 사항, 사용 사례 테이블 참조) - 자산에서 Dynamic Media Classic으로 자동 업로드를 활성화하려면 다음을 추가해야 합니다.

   1. Dynamic Media Classic에 자동 업로드를 설정합니다.
   1. 추가 **Dynamic Media Classic 업로드** 모든 Dynamic Media 워크플로우 단계 이후 단계 *의 끝 부분에* **Dam 자산 업데이트** 워크플로우 ( `https://<server>:<host>/cf#/etc/workflow/models/dam/update_asset.html)`
   1. (선택 사항) MIME 유형별로 Dynamic Media Classic 에셋 업로드를 제한합니다. [https://&lt;server>:&lt;port>/system/console/configMgr/com.day.cq.dam.scene7.impl.Scene7AssetMimeTypeServiceImpl](http://localhost:4502/system/console/configMgr/com.day.cq.dam.scene7.impl.Scene7AssetMimeTypeServiceImpl). 이 목록에 없는 에셋 MIME 유형은 Dynamic Media Classic 서버에 업로드되지 않습니다.
   1. (선택 사항) Dynamic Media Classic 구성에서 비디오를 설정합니다. Dynamic Media 및 Dynamic Media Classic 중 하나 또는 모두에 대해 비디오 인코딩을 동시에 활성화할 수 있습니다. 동적 변환은 Experience Manager 인스턴스에서 로컬로 미리 보기 및 재생에 사용되는 반면, Dynamic Media Classic 비디오 변환은 Dynamic Media Classic 서버에서 생성 및 저장됩니다. Dynamic Media 및 Dynamic Media Classic 모두에 대한 비디오 인코딩 서비스를 설정할 때 [비디오 처리 프로필](/help/assets/video-profiles.md) Dynamic Media Classic 자산 폴더로 이동합니다.
   1. (선택 사항) [Dynamic Media Classic에서 보안 미리 보기 구성](/help/sites-administering/scene7.md#configuring-the-state-published-unpublished-of-assets-pushed-to-scene).

#### 제한 사항 {#limitations}

Dynamic Media Classic과 Dynamic Media이 모두 활성화되어 있으면 다음과 같은 제한 사항이 있습니다.

* 에셋을 선택하여 Dynamic Media Classic에 수동으로 업로드하고, Experience Manager 페이지에서 Dynamic Media Classic 구성 요소로 드래그하면 작동하지 않습니다.
* Experience Manager-Dynamic Media Classic 동기화된 에셋은 에셋에서 에셋을 편집할 때 자동으로 Dynamic Media Classic으로 업데이트되지만 롤백 작업은 새 업로드를 트리거하지 않습니다. 따라서 Dynamic Media Classic은 롤백 직후 최신 버전을 받지 않습니다. 롤백이 완료된 후 다시 편집하는 것이 해결 방법입니다.
* Dynamic Media 자산이 Dynamic Media Classic 시스템과 상호 작용하지 않도록 한 사용 사례에는 Dynamic Media을 사용하고 다른 사용 사례에는 Dynamic Media Classic 통합을 사용해야 합니까? 그렇다면 Dynamic Media Classic 구성을 Dynamic Media 폴더에 적용하지 마십시오. 또한 Dynamic Media 구성(처리 프로필)을 Dynamic Media Classic 폴더에 적용하지 마십시오.

## Dynamic Media Classic과 Experience Manager 통합을 위한 우수 사례 {#best-practices-for-integrating-scene-with-aem}

Dynamic Media Classic을 Experience Manager과 통합할 때 다음 영역에서 준수해야 하는 몇 가지 중요한 모범 사례가 있습니다.

* 통합 테스트 추진
* Dynamic Media Classic에서 직접 에셋을 업로드하는 것은 특정 시나리오에 권장됩니다

다음을 참조하십시오 [알려진 제한 사항](#known-limitations-and-design-implications).

### 통합 테스트 드라이브 {#test-driving-your-integration}

Adobe은 루트 폴더가 전체 회사가 아닌 하위 폴더만 가리키도록 하여 통합을 테스트하는 것을 권장합니다.

>[!CAUTION]
>
>기존 Dynamic Media Classic 회사 계정에서 자산을 가져오는 경우 Experience Manager에 표시되는 데 시간이 오래 걸릴 수 있습니다. Dynamic Media Classic에 너무 많은 에셋이 없는 폴더를 지정해야 합니다(예: 루트 폴더에 에셋이 너무 많아 시스템 충돌이 발생할 수 있음).

### Experience Manager Assets과 Dynamic Media Classic의 자산 업로드 {#uploading-assets-from-aem-assets-versus-from-scene}

에셋(디지털 에셋 관리) 기능을 사용하거나 Dynamic Media Classic 컨텐츠 브라우저를 통해 Experience Manager에서 직접 Dynamic Media Classic에 액세스하여 에셋을 업로드할 수 있습니다. 다음 요소에 따라 선택할 수 있습니다.

* Experience Manager Assets에서 아직 지원하지 않는 Dynamic Media Classic 자산 유형은 Dynamic Media Classic 컨텐츠 브라우저를 통해 Dynamic Media Classic에서 Experience Manager 웹 사이트에 직접 추가해야 합니다. 예를 들어 이미지 템플릿입니다.
* Experience Manager Assets과 Dynamic Media Classic에서 모두 지원되는 에셋 유형의 경우, 업로드 방법은 다음에 따라 결정됩니다.

   * 현재 에셋 위치 및
   * 공통 저장소에서 이러한 파일을 관리하는 것의 중요성

자산이 이미 Dynamic Media Classic에 있고 공통 저장소에서 관리하는 것은 중요하지 않다고 가정합니다. 이 경우 에셋을 Experience Manager Assets으로 내보내고 게재를 위해 Dynamic Media Classic으로 다시 동기화하는 것은 불필요한 왕복 이동입니다. Adobe은 자산을 단일 저장소에 보관하고 게재를 위해 Dynamic Media Classic과 동기화하는 것을 권장합니다.

## Dynamic Media Classic 통합 구성 {#configuring-scene-integration}

Dynamic Media Classic에 에셋을 업로드하도록 Experience Manager 를 구성할 수 있습니다. CQ 대상 폴더의 에셋은 Experience Manager에서 Dynamic Media Classic 회사 계정으로 (자동 또는 수동으로) 업로드할 수 있습니다.

>[!NOTE]
>
>Adobe Dynamic Media Classic 에셋을 가져오려면 지정된 대상 폴더만 사용하는 것이 좋습니다. 대상 폴더 외부에 있는 디지털 에셋은 Dynamic Media Classic 구성이 활성화된 페이지의 Dynamic Media Classic 구성 요소에서만 사용할 수 있습니다. 또한 Dynamic Media Classic의 주문형 폴더에 배치됩니다. 온디맨드 폴더는 Experience Manager과 동기화되지 않지만 에셋은 Dynamic Media Classic 콘텐츠 브라우저에서 검색할 수 있습니다.

**Dynamic Media Classic을 Experience Manager과 통합하도록 구성하려면 다음 작업을 수행하십시오.**

1. [클라우드 구성 정의](#creating-a-cloud-configuration-for-scene) - Dynamic Media Classic 폴더와 에셋 폴더 간의 매핑을 정의합니다. 단방향(Experience Manager Assets에서 Dynamic Media Classic)만 동기화하려는 경우에도 이 단계를 완료하십시오.
1. [활성화 **Adobe CQ s7dam 리스너**](#enabling-the-adobe-cq-scene-dam-listener) - 다음 작업에서 완료 [!UICONTROL OSGi] 콘솔.
1. Experience Manager Assets을 Dynamic Media Classic에 자동으로 업로드하려면 해당 옵션을 켜고 Dynamic Media Classic을 [!UICONTROL DAM 자산 업데이트] 워크플로입니다. 자산을 수동으로 업로드할 수도 있습니다.
1. 사이드 킥에 Dynamic Media Classic 구성 요소 추가. 이 기능을 사용하여 사용자는 Experience Manager 페이지에서 Dynamic Media Classic 구성 요소를 사용할 수 있습니다.
1. [Experience Manager의 페이지에 구성 매핑](#enabling-scene-for-wcm) - 이 단계는 Dynamic Media Classic에서 만든 비디오 사전 설정을 보는 데 필요합니다. CQ 대상 폴더 외부에서 Dynamic Media Classic으로 자산을 게시해야 하는 경우에도 필요합니다.

이 섹션에서는 이러한 단계를 모두 수행하는 방법을 다룹니다. 중요한 제한 사항이 나와 있습니다.

### Dynamic Media Classic 및 Experience Manager Assets 간 동기화 작동 방식 {#how-synchronization-between-scene-and-aem-assets-works}

Experience Manager Assets 및 Dynamic Media Classic 동기화를 설정할 때 다음 사항을 이해하는 것이 중요합니다.

#### Experience Manager Assets에서 Dynamic Media Classic으로 업로드 {#uploading-to-scene-from-aem-assets}

* Dynamic Media Classic 업로드를 위한 Experience Manager에 지정된 동기화 폴더가 있습니다.
* 디지털 에셋이 지정된 동기화 폴더에 배치된 경우 Dynamic Media Classic에 대한 업로드를 자동화할 수 있습니다.
* Experience Manager의 폴더 및 하위 폴더 구조는 Dynamic Media Classic에서 복제됩니다.

>[!NOTE]
>
>Experience Manager은 Dynamic Media Classic에 업로드하기 전에 모든 메타데이터를 XMP으로 임베드하므로 메타데이터 노드의 모든 속성을 Dynamic Media Classic as XMP에서 사용할 수 있습니다.

#### 알려진 제한 사항 및 디자인에 따른 영향 {#known-limitations-and-design-implications}

Experience Manager Assets과 Dynamic Media Classic 간의 동기화와 함께 현재 다음과 같은 제한/디자인 문제가 있습니다.

<table>
 <tbody>
  <tr>
   <td><strong>제한/디자인 영향</strong></td>
   <td><strong>설명</strong></td>
  </tr>
  <tr>
   <td>지정된 동기화 (타겟) 폴더 1개</td>
   <td>Dynamic Media Classic 업로드를 위한 Experience Manager에서 회사당 하나의 지정된 폴더만 가질 수 있습니다. Dynamic Media Classic에서 둘 이상의 회사 계정에 액세스할 수 있어야 하는 경우 여러 구성을 만들 수 있습니다.</td>
  </tr>
  <tr>
   <td>폴더 구조</td>
   <td>에셋이 있는 동기화된 폴더를 삭제하면 모든 Dynamic Media Classic 원격 에셋이 삭제되지만 폴더는 유지됩니다.</td>
  </tr>
  <tr>
   <td>온디맨드 폴더</td>
   <td>WCM에서 Dynamic Media Classic에 수동으로 업로드되는 대상 폴더 외부에 있는 자산은 Dynamic Media Classic의 별도 온디맨드 폴더에 자동으로 배치됩니다. Experience Manager의 클라우드 구성에서 이 폴더를 구성합니다.</td>
  </tr>
  <tr>
   <td>혼합 미디어</td>
   <td>혼합 미디어 세트는 Experience Manager에서 지원되지 않지만 Experience Manager에 표시됩니다.</td>
  </tr>
  <tr>
   <td>PDF</td>
   <td>Dynamic Media Classic의 eCatalogs에서 생성된 PDF을 CQ 대상 폴더로 가져옵니다.</td>
  </tr>
  <tr>
   <td>UI 새로 고침</td>
   <td>User와 Dynamic Media Classic을 동기화할 때 Experience Manager 인터페이스를 새로 고쳐 변경 사항을 확인해야 합니다. </td>
  </tr>
  <tr>
   <td>비디오 썸네일</td>
   <td>Dynamic Media Classic을 통해 인코딩을 위해 Experience Manager Assets에 비디오를 업로드하는 경우 비디오 처리 시간에 따라 Experience Manager Assets에서 비디오 썸네일과 인코딩된 비디오를 사용할 수 있습니다.</td>
  </tr>
  <tr>
   <td>하위 폴더 Target</td>
   <td><p>대상 폴더 내의 하위 폴더를 사용하는 경우 위치에 관계없이 각 에셋에 고유한 이름을 사용해야 합니다. 또한 위치에 관계없이 에셋을 덮어쓰지 않도록 Dynamic Media Classic(설정 영역)를 구성해야 합니다.</p> <p>그렇지 않으면 Dynamic Media Classic 대상 하위 폴더에 업로드된 동일한 이름의 자산이 업로드되지만 대상 폴더의 동일한 이름의 자산은 삭제됩니다. </p> </td>
  </tr>
 </tbody>
</table>

### Dynamic Media Classic 서버 구성 {#configuring-scene-servers}

프록시 뒤에서 Experience Manager을 실행하거나 특수 방화벽 설정을 사용하는 경우 다른 지역의 호스트를 명시적으로 활성화해야 합니다. 서버는 의 콘텐츠에서 관리됩니다. `/etc/cloudservices/scene7/endpoints` 필요에 따라 사용자 정의할 수 있습니다. URL을 선택한 다음 편집하여 필요한 경우 URL을 변경합니다. 이전 버전의 Experience Manager에서 이 값은 하드 코딩되었습니다.

다음으로 이동하면 `/etc/cloudservices/scene7/endpoints.html`, 나열된 서버가 표시되며 URL을 탭하여 편집할 수 있습니다.

![chlimage_1-296](assets/chlimage_1-296.png)

### Dynamic Media Classic에 대한 클라우드 구성 만들기 {#creating-a-cloud-configuration-for-scene}

클라우드 구성은 Dynamic Media Classic 폴더와 Experience Manager Assets 폴더 간의 매핑을 정의합니다. Experience Manager Assets을 Dynamic Media Classic과 동기화하도록 구성해야 합니다. 자세한 내용은 동기화 작동 방식 을 참조하십시오.

>[!CAUTION]
>
>기존 Dynamic Media Classic 회사 계정에서 자산을 가져오는 경우 Experience Manager에 표시되는 데 시간이 오래 걸릴 수 있습니다. Dynamic Media Classic에서 에셋이 너무 많지 않은 폴더를 지정해야 합니다. 예를 들어 루트 폴더에 에셋이 너무 많은 경우가 있습니다.
>
>통합을 테스트하려면 루트 폴더가 전체 회사 대신 하위 폴더만 가리키도록 해야 합니다.

>[!NOTE]
>
>여러 구성이 있을 수 있습니다. 하나의 클라우드 구성은 Dynamic Media Classic 회사의 한 명의 사용자를 나타냅니다. 다른 Dynamic Media Classic 회사 또는 사용자에 액세스하려면 여러 구성을 만들어야 합니다.

**Dynamic Media Classic에 대한 클라우드 구성을 만들려면 다음을 수행하십시오.**

1. Experience Manager 아이콘을 선택하고 다음 위치로 이동합니다. **[!UICONTROL 배포]** > **[!UICONTROL Cloud Services]** Adobe Dynamic Media Classic에 액세스할 수 있습니다.

1. 선택 **[!UICONTROL 지금 구성]**.

   ![chlimage_1-297](assets/chlimage_1-297.png)

1. 다음에서 **[!UICONTROL 제목]** 필드 및 (선택 사항) **[!UICONTROL 이름]** 필드에 적절한 정보를 입력합니다. **[!UICONTROL 만들기]**&#x200B;를 선택합니다.

   >[!NOTE]
   >
   >구성을 추가로 만들 때 **[!UICONTROL 상위 구성]** 필드가 표시됩니다.
   >
   >실행 **아님** 상위 구성을 변경합니다. 상위 구성을 변경하면 통합이 중단될 수 있습니다.

1. Dynamic Media Classic 계정의 이메일 주소, 암호 및 지역을 입력하고 을(를) 선택합니다 **[!UICONTROL Dynamic Media Classic에 연결]**. Dynamic Media Classic 서버에 연결되어 있고 더 많은 옵션을 선택하면 대화 상자가 확장됩니다.

1. 다음을 입력합니다. **[!UICONTROL 회사]** 이름 및 **[!UICONTROL 루트 경로]**. 이 정보는 지정할 경로와 함께 게시된 서버 이름입니다. 게시된 서버 이름을 모를 경우 Dynamic Media Classic에서 **[!UICONTROL 설정 > 응용 프로그램 설정]**).

   >[!NOTE]
   >
   >Dynamic Media Classic 루트 경로는 Dynamic Media Classic 폴더 Experience Manager이 연결되는 경로입니다. 특정 폴더로 좁힐 수 있습니다.

   >[!CAUTION]
   >
   >Dynamic Media Classic 폴더의 크기에 따라 루트 폴더를 가져오는 데 시간이 오래 걸릴 수 있습니다. 또한 Dynamic Media Classic 데이터가 Experience Manager 스토리지를 초과할 수 있습니다. 올바른 폴더를 가져오고 있는지 확인하십시오. 너무 많은 데이터를 가져오면 시스템이 중지될 수 있습니다.

   ![chlimage_1-298](assets/chlimage_1-298.png)

1. 선택 **[!UICONTROL 확인]**. Experience Manager이 구성을 저장합니다.

>[!NOTE]
>
>다시 연결하는 경우:
>
>* 게시 시 Dynamic Media Classic에 다시 연결할 때 게시 시 암호를 재설정하거나 다시 연결할 때 작동하지 않습니다(작성자 인스턴스의 문제가 아님).
>* 지역, 회사 이름 등의 값을 수정하는 경우 Dynamic Media Classic에 다시 연결해야 합니다. 구성 옵션이 수정되었지만 저장되지 않은 경우 Experience Manager에서 구성이 유효하다고 잘못 표시됩니다. 다시 연결하십시오.
>


### Adobe CQ Dynamic Media Classic Dam 수신기 활성화 {#enabling-the-adobe-cq-scene-dam-listener}

기본적으로 비활성화되어 있는 Adobe CQ Dynamic Media Classic Dam 수신기를 활성화합니다.

**Adobe CQ Dynamic Media Classic Dam 리스너를 활성화하려면 다음을 수행하십시오.**

1. 다음 항목 선택 [!UICONTROL 도구] 아이콘을 클릭한 다음 로 이동합니다. **[!UICONTROL 작업]** > **[!UICONTROL 웹 콘솔]**.
1. 웹 콘솔에서 다음 위치로 이동합니다. **[!UICONTROL Adobe CQ Dynamic Media Classic Dam 수신기]** 및 선택 **[!UICONTROL 활성화됨]** 확인란.

   ![chlimage_1-299](assets/chlimage_1-299.png)

1. **[!UICONTROL 저장]**&#x200B;을 선택합니다.

### Dynamic Media Classic 업로드 워크플로우에 구성 가능한 시간 초과 추가 {#adding-configurable-timeout-to-scene-upload-workflow}

Experience Manager 인스턴스가 Dynamic Media Classic을 통해 비디오 인코딩을 처리하도록 구성된 경우 기본적으로 모든 업로드 작업에 35분 시간 제한이 있습니다. 실행 시간이 더 길어질 수 있는 비디오 인코딩 작업을 수용하기 위해 이 설정을 구성할 수 있습니다.

1. 다음으로 이동 **http://localhost:4502/system/console/configMgr/com.day.cq.dam.scene7.impl.Scene7UploadServiceImpl**.

   ![chlimage_1-300](assets/chlimage_1-300.png)

1. 에서 원하는 대로 숫자를 변경합니다. **[!UICONTROL 활성 작업 시간 초과]** 필드. 음수가 아닌 숫자는 UOM(초)으로 허용됩니다. 기본적으로 이 숫자는 2100으로 설정됩니다.

   >[!NOTE]
   >
   >모범 사례: 대부분의 에셋은 길어야 몇 분 내에 수집됩니다(예: 이미지). 그러나 예를 들어 더 큰 비디오와 같은 특정 경우에는 시간 초과 값을 7,200초(2시간)로 늘려 긴 처리 시간을 수용할 수 있습니다. 그렇지 않으면 이 Dynamic Media Classic 업로드 작업이 다음과 같이 표시됩니다. **[!UICONTROL 업로드 실패]** JCR(Java™ Content Repository) 메타데이터

1. **[!UICONTROL 저장]**&#x200B;을 선택합니다.

### Experience Manager Assets의 자동 업로드 {#autouploading-from-aem-assets}

자산이 CQ 대상 폴더에 있는 경우 Experience Manager 6.3.2부터 업로드된 모든 디지털 자산이 Dynamic Media Classic으로 업데이트되도록 Experience Manager Assets이 구성됩니다.

자산이 Experience Manager Assets에 추가되면 자동으로 업로드되고 Dynamic Media Classic에 게시됩니다.

>[!NOTE]
>
>Experience Manager Assets에서 Dynamic Media Classic으로 자동 업로드하는 최대 파일 크기는 500MB입니다.

**Experience Manager Assets에서 자동 업로드하려면:**

1. Experience Manager 아이콘을 선택하고 다음 위치로 이동합니다. **[!UICONTROL 배포]** > **[!UICONTROL Cloud Services]**.
1. Dynamic Media 제목 아래의 사용 가능한 구성에서 을 선택합니다. **[!UICONTROL dms7 (Dynamic Media]**).
1. 다음 항목 선택 **[!UICONTROL 고급]** 탭에서 **[!UICONTROL 자동 업로드 활성화]** 확인란을 선택한 다음 을 선택합니다 **[!UICONTROL 확인]**. 이제 Dynamic Media Classic에 업로드를 포함하도록 DAM 자산 워크플로우를 구성해야 합니다.

   >[!NOTE]
   >
   >다음을 참조하십시오 [Dynamic Media Classic에 푸시된 에셋의 상태(게시/게시 취소됨) 구성](#configuring-the-state-published-unpublished-of-assets-pushed-to-scene) 게시되지 않은 상태에서 Dynamic Media Classic으로 에셋을 푸시하는 방법에 대한 정보입니다.

   ![screen_shot_2018-03-15at52501pm](assets/screen_shot_2018-03-15at52501pm.jpg)

1. Experience Manager 시작 페이지로 돌아가서 를 선택합니다. **[!UICONTROL 워크플로]**. 를 두 번 클릭합니다. **DAM 자산 업데이트** 열려 있는 워크플로우입니다.
1. 사이드 킥에서 **[!UICONTROL 워크플로]** 구성 요소 및 선택 **[!UICONTROL Dynamic Media Classic]**. 드래그 **[!UICONTROL Dynamic Media Classic]** 워크플로우에 추가하고 을(를) 선택합니다. **[!UICONTROL 저장]**. 대상 폴더의 Experience Manager Assets에 추가된 에셋은 자동으로 Dynamic Media Classic에 업로드됩니다.

   ![chlimage_1-301](assets/chlimage_1-301.png)

   >[!NOTE]
   >
   >* 자동화 후 에셋을 추가할 때 CQ 대상 폴더에 배치되지 않으면 Dynamic Media Classic에 업로드되지 않습니다.
   >* Experience Manager은 Dynamic Media Classic에 업로드하기 전에 모든 메타데이터를 XMP으로 임베드하므로 메타데이터 노드의 모든 속성을 Dynamic Media Classic as XMP에서 사용할 수 있습니다.


### Dynamic Media Classic에 푸시된 에셋의 상태(게시됨/게시되지 않음)를 구성합니다. {#configuring-the-state-published-unpublished-of-assets-pushed-to-scene}

Experience Manager Assets에서 Dynamic Media Classic으로 자산을 푸시하는 경우 자동으로 게시(기본 비헤이비어)하거나 게시되지 않은 상태로 Dynamic Media Classic에 푸시할 수 있습니다.

시작하기 전에 스테이징 환경에서 테스트하려는 경우 Dynamic Media Classic에 자산을 즉시 게시하지 않을 수 있습니다. Dynamic Media Classic의 보안 테스트 환경에서 Experience Manager 을 사용하여 에셋의 에셋을 게시되지 않은 상태로 Dynamic Media Classic에 직접 푸시할 수 있습니다.

Dynamic Media Classic 자산은 보안 미리 보기를 통해 사용할 수 있습니다. 자산이 Experience Manager 내에 게시되는 경우에만 Dynamic Media Classic 자산이 프로덕션에서 라이브로 전환됩니다.

자산을 Dynamic Media Classic에 푸시할 때 즉시 게시하려면 옵션을 구성할 필요가 없습니다. 이 기능은 기본 동작입니다.

그러나 Dynamic Media Classic에 푸시된 자산을 자동으로 게시하지 않으려는 경우 이 섹션에서는 이 기능을 수행하도록 Experience Manager 및 Dynamic Media Classic을 구성하는 방법을 설명합니다.

#### 자산을 Dynamic Media Classic 게시 취소에 푸시하기 위한 사전 요구 사항 {#prerequisites-to-push-assets-to-scene-unpublished}

자산을 게시하지 않고 Dynamic Media Classic에 푸시하려면 먼저 다음을 설정해야 합니다.

1. [Admin Console을 사용하여 지원 사례 만들기](https://helpx.adobe.com/kr/enterprise/admin-guide.html/enterprise/using/support-for-experience-cloud.ug.html). 지원 사례에서 Dynamic Media Classic 계정에 대한 보안 미리 보기 활성화를 요청합니다.
1. [Dynamic Media Classic 계정에 대한 보안 미리 보기 설정](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/upload-publish/testing-assets-making-them-public.html?lang=en).

이러한 단계는 Dynamic Media Classic에서 보안 테스트 설정을 만들 때 따라야 하는 것과 동일한 단계입니다.

>[!NOTE]
>
>설치 환경이 UNIX® 64비트 운영 체제인 경우 [https://helpx.adobe.com/experience-manager/kb/enable-xmp-write-back-64-bit-redhat.html](https://helpx.adobe.com/experience-manager/kb/enable-xmp-write-back-64-bit-redhat.html) 기타 구성 옵션에 대해 설정해야 합니다.

#### 게시되지 않은 상태에서 에셋을 푸시하기 위한 알려진 제한 사항  {#known-limitations-for-pushing-assets-in-unpublished-state}

이 기능을 사용하는 경우 다음 제한 사항에 유의하십시오.

* 버전 제어를 지원하지 않습니다.
* 자산이 Experience Manager에 이미 게시되고 후속 버전이 만들어지면 해당 새 버전이 즉시 프로덕션에 라이브로 게시됩니다. 활성화 시 게시는 에셋의 초기 게시와만 작동합니다.

>[!NOTE]
>
>자산을 즉시 게시하려면 유지하는 것이 좋습니다 **[!UICONTROL 보안 미리 보기 활성화]** 을 로 설정 **[!UICONTROL 즉시]** 및 사용 **[!UICONTROL 자동 업로드 활성화]** 기능.

### Dynamic Media Classic에 푸시된 에셋의 상태를 게시 취소로 설정 {#setting-the-state-of-assets-pushed-to-scene-as-unpublished}

>[!NOTE]
>
>사용자가 Experience Manager에서 에셋을 게시하면 S7 에셋이 프로덕션/라이브 에셋으로 자동으로 트리거됩니다(에셋이 더 이상 보안 미리 보기/게시 취소에 있지 않음).

**Dynamic Media Classic에 푸시된 에셋의 상태를 게시 취소로 설정하려면 다음을 수행합니다.**

1. Experience Manager 아이콘을 선택하고 다음 위치로 이동합니다. **[!UICONTROL 배포]** > **[!UICONTROL Cloud Services]**.
1. 선택 **[!UICONTROL Dynamic Media Classic]**.
1. Dynamic Media Classic에서 구성을 선택합니다.
1. 다음 항목 선택 **[!UICONTROL 고급]** 탭.
1. 다음에서 **[!UICONTROL 보안 보기 활성화]** 드롭다운 메뉴에서 다음을 선택합니다. **[!UICONTROL AEM 게시 활성화 시]** 게시하지 않고 자산을 Dynamic Media Classic에 푸시할 수 있습니다. (기본적으로 이 값은 로 설정됩니다. **[!UICONTROL 즉시]**: 여기서 Dynamic Media Classic 자산은 즉시 게시됩니다.)

   다음을 참조하십시오 [Dynamic Media Classic 설명서](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/upload-publish/testing-assets-making-them-public.html) 공개하기 전에 에셋을 테스트하는 방법에 대한 자세한 정보입니다.

   ![chlimage_1-302](assets/chlimage_1-302.png)

1. 선택 **[!UICONTROL 확인]**.

보안 미리 보기를 활성화하면 자산이 게시 취소된 보안 미리 보기 서버로 푸시됩니다.

다음을 확인: **[!UICONTROL 보안 미리 보기]** 이 활성화되어 있으면 Experience Manager 페이지의 Dynamic Media Classic 구성 요소로 이동합니다. **[!UICONTROL 편집]**&#x200B;을 선택합니다. 자산에는 URL에 나열된 보안 미리보기 서버가 있습니다. Experience Manager에 게시하면 파일 참조의 서버 도메인이 미리보기 URL에서 프로덕션 URL로 업데이트됩니다.

### WCM용 Dynamic Media Classic 활성화 {#enabling-scene-for-wcm}

다음 두 가지 이유로 WCM용 Dynamic Media Classic 활성화가 필요합니다.

* 페이지 작성을 위한 범용 비디오 프로필의 드롭다운 목록을 활성화합니다. 이 목록이 없으면 **[!UICONTROL 범용 비디오 사전 설정]** 드롭다운이 비어 있으므로 설정할 수 없습니다.
* 디지털 에셋이 대상 폴더에 없는 경우 페이지 속성에서 해당 페이지에 대해 Dynamic Media Classic을 활성화하면 에셋을 Dynamic Media Classic에 업로드할 수 있습니다. 그런 다음 Dynamic Media Classic 구성 요소에 자산을 끌어다 놓습니다. 일반 상속 규칙이 적용됩니다(즉, 하위 페이지가 상위 페이지에서 구성을 상속함).

WCM용 Dynamic Media Classic을 활성화할 때 다른 구성과 마찬가지로 상속 규칙이 적용됩니다. 터치에 적합한 또는 클래식 사용자 인터페이스에서 WCM용 Dynamic Media Classic을 활성화할 수 있습니다.

#### 터치에 적합한 사용자 인터페이스에서 WCM용 Dynamic Media Classic 활성화 {#enabling-scene-for-wcm-in-the-touch-optimized-user-interface}

1. Experience Manager 아이콘을 선택하고 다음 위치로 이동합니다. **[!UICONTROL 사이트]**&#x200B;를 클릭한 다음 웹 사이트의 루트 페이지(언어별로 다름)를 선택합니다.

1. 도구 모음에서 [!UICONTROL 설정] 아이콘 및 선택 **[!UICONTROL 속성 열기]**.

1. 선택 **[!UICONTROL Cloud Services]** 및 선택 **[!UICONTROL 구성 추가]** 및 선택 **[!UICONTROL Dynamic Media Classic]**.
1. 다음에서 **[!UICONTROL Adobe Dynamic Media Classic]** 드롭다운 목록에서 원하는 구성을 선택하고 **[!UICONTROL 확인]**.

   ![chlimage_1-303](assets/chlimage_1-303.png)

   해당 Dynamic Media Classic 구성의 비디오 사전 설정은 해당 페이지 및 하위 페이지에서 Dynamic Media Classic 비디오 구성 요소와 함께 Experience Manager 시 사용할 수 있습니다.

#### 클래식 사용자 인터페이스에서 WCM용 Dynamic Media Classic 활성화 {#enabling-scene-for-wcm-in-the-classic-user-interface}

1. Experience Manager에서 **[!UICONTROL 웹 사이트]** 웹 사이트의 루트 페이지로 이동합니다(언어별 아님).

1. 사이드 킥에서 **[!UICONTROL 페이지]** 아이콘 및 선택 **[!UICONTROL 페이지 속성]**.

1. 선택 **[!UICONTROL Cloud Services]** > **[!UICONTROL 서비스 추가]** > **[!UICONTROL Dynamic Media Classic]**.
1. 다음에서 **[!UICONTROL Adobe Dynamic Media Classic]** 드롭다운 목록에서 원하는 구성을 선택하고 **[!UICONTROL 확인]**.

   해당 Dynamic Media Classic 구성의 비디오 사전 설정은 해당 페이지 및 하위 페이지에서 Dynamic Media Classic 비디오 구성 요소와 함께 Experience Manager 시 사용할 수 있습니다.

### 기본 구성 구성 {#configuring-a-default-configuration}

Dynamic Media Classic 구성이 여러 개 있는 경우 그 중 하나를 Dynamic Media Classic 콘텐츠 브라우저의 기본값으로 지정할 수 있습니다.

특정 시점에 하나의 Dynamic Media Classic 구성만 기본값으로 표시할 수 있습니다. 기본 구성은 Dynamic Media Classic 컨텐츠 브라우저에 기본적으로 표시되는 회사 자산입니다.

**기본 구성을 구성하려면 다음 작업을 수행하십시오.**

1. Experience Manager 아이콘을 선택하고 다음 위치로 이동합니다. **[!UICONTROL 배포]** > **[!UICONTROL Cloud Services]**.
1. 선택 **[!UICONTROL Dynamic Media Classic]**.
1. Dynamic Media Classic에서 구성을 선택합니다.
1. 구성을 열려면 다음을 선택합니다. **[!UICONTROL 편집]**.

1. 다음에서 **[!UICONTROL 일반]** 탭에서 **[!UICONTROL 기본 구성]** Dynamic Media Classic 컨텐츠 브라우저에 표시되는 기본 회사 및 루트 경로로 설정하려면 확인란을 선택합니다.

   ![chlimage_1-304](assets/chlimage_1-304.png)

   >[!NOTE]
   >
   >구성이 하나만 있는 경우 **[!UICONTROL 기본 구성]** 확인란은 영향을 주지 않습니다.

### 임시 폴더 구성 {#configuring-the-ad-hoc-folder}

자산이 CQ 대상 폴더에 없는 경우 Dynamic Media Classic에서 자산이 업로드되는 온디맨드 폴더를 구성할 수 있습니다. CQ 대상 폴더 외부에서 자산 게시 를 참조하십시오.

**임시 폴더를 구성하려면 다음 작업을 수행하십시오.**

1. Experience Manager 아이콘을 선택하고 다음 위치로 이동합니다. **[!UICONTROL 배포]** > **[!UICONTROL Cloud Services]**.
1. 선택 **[!UICONTROL Dynamic Media Classic]**.
1. Dynamic Media Classic에서 구성을 선택합니다.
1. 구성을 열려면 다음을 선택합니다. **[!UICONTROL 편집]**.

1. 다음 항목 선택 **[!UICONTROL 고급]** 탭. 다음에서 **[!UICONTROL 임시 폴더]** 필드, 다음을 수정할 수 있습니다. **애드혹** 폴더를 삭제합니다. 기본적으로 **name_of_the_company/CQ5_adhoc**.

   ![chlimage_1-305](assets/chlimage_1-305.png)

### 범용 비디오 사전 설정 구성 {#configuring-universal-presets}

비디오 구성 요소에 대한 범용 비디오 사전 설정을 구성하려면 을 참조하십시오. [비디오](/help/assets/s7-video.md).

## MIME 유형 기반 에셋/Dynamic Media Classic 업로드 작업 매개 변수 지원 활성화 {#enabling-mime-type-based-assets-scene-upload-job-parameter-support}

Digital Asset Manager/Dynamic Media Classic 에셋의 동기화에 의해 트리거되는 구성 가능한 Dynamic Media Classic 업로드 작업 매개 변수를 활성화할 수 있습니다.

특히 Experience Manager 웹 콘솔 구성 패널의 OSGi(Open Service Gateway 이니셔티브) 영역에서 MIME 유형별로 허용되는 파일 형식을 구성합니다. 그런 다음 JCR(Java™ Content Repository)의 각 MIME 유형에 사용되는 개별 업로드 작업 매개 변수를 사용자 정의할 수 있습니다.

**MIME 유형 기반 자산을 활성화하려면 다음을 수행하십시오.**

1. Experience Manager 아이콘을 선택하고 다음 위치로 이동합니다. **[!UICONTROL 도구]** > **[!UICONTROL 작업]** > **[!UICONTROL 웹 콘솔]**.
1. Adobe Experience Manager 웹 콘솔 구성 패널의 **[!UICONTROL OSGi]** 메뉴, 선택 **[!UICONTROL 구성]**.
1. 이름 열에서 을 찾아 선택합니다 **[!UICONTROL Adobe CQ Dynamic Media Classic 자산 MIME 유형 서비스]** 구성을 편집합니다.
1. MIME 유형 매핑 영역에서 더하기 기호(+)를 선택하여 MIME 유형을 추가합니다.

   다음을 참조하십시오 [지원되는 MIME 유형](/help/assets/assets-formats.md#supported-mime-types).

1. 텍스트 필드에 새 MIME 유형 이름을 입력합니다.

   예를 들어, `<file_extension>=<mime_type>` 에서와 같이 `EPS=application/postscript` 또는 `PSD=image/vnd.adobe.photoshop`.

1. 구성 창의 오른쪽 아래 모서리에서 을(를) 선택합니다 **[!UICONTROL 저장]**.
1. Experience Manager으로 돌아간 다음 왼쪽 레일에서 을 선택합니다. **[!UICONTROL CRXDE Lite]**.
1. CRXDE Lite 페이지의 왼쪽 레일에서 로 이동합니다. `/etc/cloudservices/scene7/<environment>` (대용 `<environment>` (실제 이름)입니다.
1. 확장 `<environment>` (대용 `<environment>` (실제 이름)을 사용하여 `mimeTypes` 노드.
1. 방금 추가한 mimeType을 선택합니다.

   예를 들어, `mimeTypes > application_postscript` 또는 `mimeTypes > image_vnd.adobe.photoshop`.

1. CRXDE Lite 페이지 오른쪽에서 **[!UICONTROL 속성]** 탭.
1. 에서 Dynamic Media Classic 업로드 작업 매개 변수를 지정합니다. **[!UICONTROL jobParam]** 값 필드.

   예, `psprocess="rasterize"&psresolution=120` .

   다음을 참조하십시오. [Adobe Dynamic Media Classic 이미지 프로덕션 시스템 API](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/c-overview.html) 추가 업로드 작업 매개 변수를 사용할 수 있습니다.

   >[!NOTE]
   >
   >PSD 파일을 업로드하고 레이어 추출이 있는 템플릿으로 처리하려면 **[!UICONTROL jobParam]** 값 필드:
   >
   >`process=MaintainLayers&layerNaming=AppendName&createTemplate=true`
   >
   >PSD 파일에 &quot;레이어&quot;가 있는지 확인하십시오. 엄밀히 말하면 하나의 이미지이거나 마스크가 있는 이미지라면, 처리할 레이어가 없기 때문에 이미지로 처리된다.

1. CRXDE Lite 페이지의 왼쪽 상단 모서리에서 을(를) 선택합니다. **[!UICONTROL 모두 저장]**.

## Dynamic Media Classic 및 Experience Manager 통합 문제 해결 {#troubleshooting-scene-and-aem-integration}

Experience Manager을 Dynamic Media Classic과 통합하는 데 문제가 있는 경우 솔루션에 대한 다음 시나리오를 참조하십시오.

**Dynamic Media Classic에 디지털 자산을 게시하지 못하는 경우:**

* 업로드하고 있는 에셋이 **[!UICONTROL CQ 대상]** 폴더(Dynamic Media Classic 클라우드 구성에서 이 폴더를 지정)
* 그렇지 않은 경우 에서 클라우드 구성을 구성해야 합니다. **[!UICONTROL 페이지 속성]** 해당 페이지의에 대한 업로드를 허용합니다. **[!UICONTROL CQ 애드혹]** 폴더를 삭제합니다.

* 로그에서 모든 정보를 확인하십시오.

**비디오 사전 설정이 표시되지 않는 경우:**

* 다음을 통해 해당 페이지의 클라우드 구성을 구성했는지 확인합니다. **[!UICONTROL 페이지 속성]**. 비디오 사전 설정은 Dynamic Media Classic 비디오 구성 요소에서 사용할 수 있습니다.

**비디오 자산이 Experience Manager에서 재생되지 않는 경우:**

* 올바른 비디오 구성 요소를 사용했는지 확인하십시오. Dynamic Media Classic 비디오 구성 요소는 기본 비디오 구성 요소와 다릅니다. 다음을 참조하십시오 [기본 비디오 구성 요소와 Dynamic Media Classic 비디오 구성 요소](/help/assets/s7-video.md).

**Experience Manager에서 새로 만들거나 수정한 자산이 Dynamic Media Classic에 자동으로 업로드되지 않는 경우:**

* 자산이 CQ 대상 폴더에 있는지 확인합니다. Experience Manager Assets에서 자산을 자동으로 업로드하도록 구성한 경우 CQ 대상 폴더에 있는 자산만 자동으로 업데이트됩니다.
* 자동 업로드를 활성화하도록 Cloud Services 구성을 구성했는지 그리고 Dynamic Media Classic 업로드를 포함하도록 DAM 에셋 워크플로를 업데이트하고 저장했는지 확인하십시오.
* Dynamic Media Classic 대상 폴더의 하위 폴더에 이미지를 업로드할 때 다음 중 하나를 수행해야 합니다.

   * 위치에 관계없이 모든 에셋의 이름이 고유한지 확인합니다. 그렇지 않으면 기본 대상 폴더의 자산이 삭제되고 하위 폴더의 자산만 유지됩니다.
   * Dynamic Media Classic 계정의 설정 영역에서 Dynamic Media Classic이 자산을 덮어쓰는 방법을 변경합니다. 하위 폴더에서 이름이 같은 자산을 사용하는 경우 위치에 관계없이 자산을 덮어쓰도록 Dynamic Media Classic을 설정하지 마십시오.

**삭제된 에셋 또는 폴더가 Dynamic Media Classic과 Experience Manager 간에 동기화되지 않는 경우:**

* Experience Manager Assets에서 삭제된 에셋 및 폴더는 여전히 Dynamic Media Classic의 동기화된 폴더에 표시됩니다. 수동으로 삭제하십시오.

**비디오 업로드에 실패한 경우:**

* 비디오 업로드에 실패하고 Experience Manager을 사용하여 Dynamic Media Classic 통합을 통해 비디오를 인코딩하는 경우 다음을 참조하십시오. [Dynamic Media Classic 업로드 워크플로우에 구성 가능한 시간 초과 추가](#adding-configurable-timeout-to-scene-upload-workflow).

>[!CAUTION]
>
>기존 Dynamic Media Classic 회사 계정에서 자산을 가져오는 경우 Experience Manager에 표시되는 데 시간이 오래 걸릴 수 있습니다. Dynamic Media Classic에서 에셋이 너무 많지 않은 폴더를 지정해야 합니다. 예를 들어 루트 폴더에 에셋이 너무 많은 경우가 있습니다.
>
>통합을 테스트하려면 루트 폴더가 전체 회사 대신 하위 폴더만 가리키도록 해야 합니다.
