---
title: Adobe Experience Manager과 Dynamic Media Classic 통합
description: Adobe Experience Manager을 Dynamic Media Classic과 통합하는 방법을 알아봅니다.
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
exl-id: f244cfb5-5550-4f20-92f0-bb296e2bf76e
source-git-commit: f4b7566abfa0a8dbb490baa0e849de6c355a3f06
workflow-type: tm+mt
source-wordcount: '5484'
ht-degree: 1%

---

# Adobe Experience Manager과 Dynamic Media Classic 통합 {#integrating-with-dynamic-media-classic-scene}

Adobe Dynamic Media Classic은 리치 미디어 자산을 관리, 개선, 게시 및 웹, 모바일, 이메일 및 인터넷에 연결된 디스플레이 및 프린트로 제공하기 위한 호스팅 솔루션입니다.

Dynamic Media Classic을 사용하려면 Dynamic Media Classic과 Adobe Experience Manager 자산이 서로 상호 작용할 수 있도록 클라우드 구성을 구성해야 합니다. 이 문서에서는 Experience Manager 및 Dynamic Media Classic을 구성하는 방법에 대해 설명합니다.

페이지에서 모든 Dynamic Media Classic 구성 요소를 사용하고 비디오를 사용하는 방법에 대한 자세한 내용은 [Dynamic Media Classic 사용](../assets/scene7.md)을 참조하십시오.

>[!NOTE]
>
>* Dynamic Media Classic의 DHTML 뷰어 플랫폼은 공식적으로 2014년 1월 31일에 종료되었습니다. 자세한 내용은 [DHTML 뷰어 지원 중단 FAQ](../sites-administering/dhtml-viewer-endoflifefaqs.md)를 참조하십시오.
>* Experience Manager에서 작동하도록 Dynamic Media Classic을 구성하기 전에 Dynamic Media Classic과 Experience Manager 통합을 위한 [우수 사례](#best-practices-for-integrating-scene-with-aem) 를 참조하십시오.
>* 사용자 지정 프록시 구성과 함께 Dynamic Media Classic을 사용하는 경우, Experience Manager의 일부 기능이 3.x API를 사용하고 다른 기능이 4.x API를 사용하기 때문에 HTTP 클라이언트 프록시 구성을 모두 구성해야 합니다. 3.x는 [http://localhost:4502/system/console/configMgr/com.day.commons.httpclient](http://localhost:4502/system/console/configMgr/com.day.commons.httpclient)로 구성되고 4.x는 [http://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator](http://localhost:4502/system/console/configMgr/org.apache.http.proxyconfigurator)로 구성됩니다.

>



## Experience Manager/Dynamic Media Classic과 Dynamic Media 통합 비교 {#aem-scene-integration-versus-dynamic-media}

Experience Manager 사용자는 Dynamic Media에서 작업할 두 솔루션 중에서 선택할 수 있습니다. 다음 중 하나를 사용할 수 있습니다.

* Experience Manager 인스턴스를 Dynamic Media Classic과 통합합니다.
* Experience Manager에 통합된 Dynamic Media을 사용합니다.

선택할 솔루션을 결정하려면 다음 기준을 사용하십시오.

* 게시 및 전달을 위해 Dynamic Media Classic에 자산을 있는 **기존** Dynamic Media Classic 고객이지만, 이러한 자산을 사이트(WCM) 작성 또는 Experience Manager 자산과 통합하시겠습니까, 아니면 두 가지 모두입니까? 이 경우 이 문서에 설명된 [Experience Manager/Dynamic Media Classic 지점 통합](#aem-scene-point-to-point-integration)을 사용하십시오.

* 리치 미디어 게재 요구 사항이 있는 **새** Experience Manager 고객인 경우 [Dynamic Media 옵션](#aem-dynamic-media)을 선택합니다. 이 옵션은 기존 S7 계정과 해당 시스템에 저장된 자산이 없는 경우에 가장 적합합니다.

* 경우에 따라 두 솔루션을 모두 사용합니다. [이중 사용 시나리오](/help/sites-administering/scene7.md#dual-use-scenario)에서는 해당 시나리오를 설명합니다.

### Experience Manager/Dynamic Media Classic 지점 통합 {#aem-scene-point-to-point-integration}

이 솔루션의 자산으로 작업하는 경우 다음 중 하나를 수행합니다.

* 자산을 Dynamic Media Classic에 바로 업로드한 다음 페이지 작성 또는 사용을 위해 **Dynamic Media Classic** 컨텐츠 브라우저를 통해 액세스합니다
* 자산을 업로드한 다음 Dynamic Media Classic에 자동 게시 기능을 활성화합니다. 페이지 작성을 위해 **자산** 컨텐츠 브라우저를 통해 액세스합니다

이 통합에 사용하는 구성 요소는 [디자인 모드](/help/sites-authoring/author-environment-tools.md#page-modes)의 **Dynamic Media Classic** 구성 요소 영역에 있습니다.

### Dynamic Media Experience Manager {#aem-dynamic-media}

Experience Manager Dynamic Media은 Experience Manager 플랫폼 내에서 직접 Dynamic Media Classic 기능을 통합하는 것입니다.

이 솔루션에서 자산으로 작업하는 경우 다음 워크플로우를 따릅니다.

1. 단일 이미지 및 비디오 자산을 Experience Manager에 바로 업로드합니다.
1. Experience Manager 내에서 바로 비디오를 인코딩하십시오.
1. Experience Manager 내에서 직접 이미지 기반 세트를 작성합니다.
1. 해당하는 경우 이미지나 비디오에 인터랙티브한 기능을 추가하십시오.

Dynamic Media에 사용하는 구성 요소는 [디자인 모드](/help/sites-authoring/author-environment-tools.md#page-modes)의 **[!UICONTROL Dynamic Media]** 구성 요소 영역에 있습니다. 여기에는 다음 항목이 포함됩니다.

* **[!UICONTROL Dynamic Media]**  -  **[!UICONTROL Dynamic]** Mediacomponent는 편리하게도 이미지를 추가하는지 아니면 비디오를 추가하는지에 따라 사용 가능한 선택 사항이 달라집니다. 이 구성 요소는 이미지 사전 설정, 이미지 세트와 같은 이미지 기반 뷰어, 스핀 세트, 혼합 미디어 세트 및 비디오를 지원합니다. 또한 뷰어는 응답형입니다. 화면 크기가 스크린의 크기에 따라 자동으로 변경됩니다. 모든 뷰어는 HTML5 뷰어입니다.

* **[!UICONTROL 대화형 미디어]**  -  **[!UICONTROL 대화형]** 미디어 구성 요소는 회전 배너, 대화형 이미지 및 대화형 비디오와 같은 자산을 위한 것입니다. 이러한 자산에는 핫스팟이나 이미지 맵과 같은 상호 작용이 있습니다. 이 구성 요소는 편리합니다. 즉, 이미지를 추가하는지 아니면 비디오를 추가하는지에 따라 다양한 선택 사항이 제공됩니다. 또한 뷰어는 응답형입니다. 화면 크기가 스크린의 크기에 따라 자동으로 변경됩니다. 모든 뷰어는 HTML5 뷰어입니다.

### 듀얼 사용 시나리오 {#dual-use-scenario}

기본적으로 Experience Manager의 Dynamic Media 및 Dynamic Media Classic 통합 기능을 동시에 사용할 수 있습니다. 다음 사용 사례 표에서는 특정 영역을 켜거나 끌 때 설명합니다.

Dynamic Media과 Dynamic Media Classic을 동시에 사용하려면 다음을 수행하십시오.

1. Cloud Services에서 [Dynamic Media Classic](#creating-a-cloud-configuration-for-scene)을 구성합니다.
1. 사용 사례와 관련된 특정 지침을 따르십시오.

   <table>
    <tbody>
    <tr>
    <td> </td>
    <td> </td>
    <td><strong>다이내믹 미디어</strong></td>
    <td> </td>
    <td><strong>Dynamic Media Classic 통합</strong></td>
    <td> </td>
    </tr>
    <tr>
    <td><strong>만약 ...</strong></td>
    <td><strong>사용 사례 워크플로우</strong></td>
    <td><strong>이미징/비디오</strong></td>
    <td><strong>Dynamic Media 구성 요소</strong></td>
    <td><strong>S7 컨텐츠 브라우저 및 구성 요소</strong></td>
    <td><strong>자산에서 S7로 자동 업로드</strong></td>
    </tr>
    <tr>
    <td>사이트 및 Dynamic Media의 새로운 기능</td>
    <td>자산을 Experience Manager에 업로드하고 Dynamic Media 구성 요소를 사용하여 사이트 페이지에서 자산을 작성합니다</td>
    <td><p>사용</p> <p>(3단계 참조)</p> </td>
    <td><a href="/help/assets/adding-dynamic-media-assets-to-pages.md">사용</a></td>
    <td>끔</td>
    <td>끔</td>
    </tr>
    <tr>
    <td>소매, 사이트 및 Dynamic Media의 새로운 기능</td>
    <td>관리 및 전달을 위해 비제품 자산을 Experience Manager에 업로드합니다. 제품 자산을 Dynamic Media Classic에 업로드하고, Experience Manager 및 구성 요소에서 Dynamic Media Classic 컨텐츠 브라우저를 사용하여 사이트에서 제품 세부 사항 페이지를 작성하십시오.</td>
    <td><p>사용</p> <p>(3단계 참조)</p> </td>
    <td><a href="/help/assets/adding-dynamic-media-assets-to-pages.md">사용</a></td>
    <td><a href="/help/assets/scene7.md#scene-content-browser">사용</a></td>
    <td>끔</td>
    </tr>
    <tr>
    <td>Assets 및 Dynamic Media의 새로운 기능</td>
    <td>자산을 Experience Manager에 업로드하고 Dynamic Media에서 게시된 URL/포함 코드를 사용합니다</td>
    <td><p>사용</p> <p>(3단계 참조)</p> </td>
    <td>끔</td>
    <td>끔</td>
    <td>끔</td>
    </tr>
    <tr>
    <td>Dynamic Media 및 템플릿의 새로운 기능</td>
    <td>이미징 및 비디오에 Dynamic Media을 사용합니다. Dynamic Media Classic에서 이미지 템플릿을 작성하고 Dynamic Media Classic 컨텐츠 파인더를 사용하여 사이트 페이지에 템플릿을 포함합니다.</td>
    <td><p>사용</p> <p>(3단계 참조)</p> </td>
    <td><a href="/help/assets/adding-dynamic-media-assets-to-pages.md">사용</a></td>
    <td><a href="/help/assets/scene7.md#scene-content-browser">사용</a></td>
    <td>끔</td>
    </tr>
    <tr>
    <td>기존 Dynamic Media Classic 고객 및 사이트를 처음 사용하는 고객</td>
    <td>자산을 Dynamic Media Classic에 업로드하고 Experience Manager Dynamic Media Classic 컨텐츠 브라우저를 사용하여 사이트 페이지에서 자산을 검색하고 작성합니다</td>
    <td>끔</td>
    <td>끔</td>
    <td><a href="/help/assets/scene7.md#scene-content-browser">사용</a></td>
    <td>끔</td>
    </tr>
    <tr>
    <td>사이트 및 자산을 처음 사용하는 기존 Dynamic Media Classic 고객</td>
    <td>자산을 DAM에 업로드하고 전달할 Dynamic Media Classic에 자동으로 게시합니다. Experience Manager Dynamic Media Classic 컨텐츠 브라우저를 사용하여 사이트 페이지에서 자산을 검색하고 작성합니다.</td>
    <td>끔</td>
    <td>끔</td>
    <td><a href="/help/assets/scene7.md#scene-content-browser">사용</a></td>
    <td><p><a href="#configuringautouploadingfromaemassets">사용</a></p> <p>(4단계 참조)</p> </td>
    </tr>
    <tr>
    <td>기존 Dynamic Media Classic 고객 및 Assets의 새로운 기능</td>
    <td><p>자산을 Experience Manager에 업로드하고 Dynamic Media을 사용하여 다운로드/공유를 위한 렌디션을 생성합니다. Experience Manager 자산을 Dynamic Media Classic에 자동으로 게시하여 배달합니다.</p> <p><strong>중요: </strong> 중복 처리를 발생시키고 Experience Manager에서 생성된 표현물은 Dynamic Media Classic에 동기화되지 않습니다</p> </td>
    <td><p>사용</p> <p>(3단계 참조)</p> </td>
    <td>끔</td>
    <td>끔</td>
    <td><p><a href="#configuringautouploadingfromaemassets">사용</a></p> <p>(4단계 참조)</p> </td>
    </tr>
    </tbody>
    </table>

1. (선택 사항) 사용 사례 표 참조) - [Dynamic Media 클라우드 구성](/help/assets/config-dynamic.md) 및 [Dynamic Media 서버](/help/assets/config-dynamic.md)를 사용하도록 설정합니다.
1. (선택 사항) 사용 사례 표 참조) - Dynamic Media Classic에 자산에서 자동 업로드를 활성화하도록 선택한 경우 다음을 추가해야 합니다.

   1. Dynamic Media Classic에 자동 업로드를 설정합니다.
   1. **Dynamic Media Classic 업로드** 단계를 모든 Dynamic Media 워크플로우 단계 ***Dam 자산 업데이트**워크플로우( `https://<server>:<host>/cf#/etc/workflow/models/dam/update_asset.html)`)의 뒤에 추가합니다*
   1. (선택 사항) Dynamic Media Classic 자산 업로드를 [https://&lt;server>:&lt;port>/system/console/configMgr/com.day.cq.dam.scene7.impl.Scene7AssetMimeTypeServiceImpl](http://localhost:4502/system/console/configMgr/com.day.cq.dam.scene7.impl.Scene7AssetMimeTypeServiceImpl)에서 MIME 유형으로 제한합니다. 이 목록에 없는 자산 MIME 유형은 Dynamic Media Classic 서버에 업로드되지 않습니다.
   1. (선택 사항) Dynamic Media Classic 구성에서 비디오를 설정합니다. Dynamic Media과 Dynamic Media Classic 중 하나 또는 둘 다에 대해 비디오 인코딩을 동시에 활성화할 수 있습니다. 동적 변환은 Experience Manager 인스턴스에서 미리 보기 및 재생에 사용되는 반면, Dynamic Media Classic 비디오 표현물은 Dynamic Media Classic 서버에 생성되고 저장됩니다. Dynamic Media과 Dynamic Media Classic 둘 다에 대해 비디오 인코딩 서비스를 설정할 때 [비디오 처리 프로필](/help/assets/video-profiles.md)을 Dynamic Media Classic 자산 폴더에 적용합니다.
   1. (선택 사항) [Dynamic Media Classic에서 보안 미리 보기 구성](/help/sites-administering/scene7.md#configuring-the-state-published-unpublished-of-assets-pushed-to-scene).

#### 제한 사항 {#limitations}

Dynamic Media Classic과 Dynamic Media을 모두 활성화한 경우 다음 제한 사항이 있습니다.

* 자산을 선택하고 Experience Manager 페이지의 Dynamic Media Classic 구성 요소로 드래그하여 Dynamic Media Classic에 수동으로 업로드하는 작업이 작동하지 않습니다.
* Experience Manager-Dynamic Media Classic 동기화된 자산은 Assets에서 자산을 편집할 때 Dynamic Media Classic으로 자동으로 업데이트되지만 롤백 작업은 새 업로드를 트리거하지 않습니다. 따라서 Dynamic Media Classic은 롤백 후 즉시 최신 버전을 가져오지 않습니다. 롤백이 완료된 후 다시 편집하는 것이 해결 방법입니다.
* Dynamic Media 자산이 Dynamic Media Classic 시스템과 상호 작용하지 않도록 한 사용 사례에는 Dynamic Media을 사용하고, 다른 사용 사례에는 Dynamic Media Classic 통합을 사용해야 합니까? 있는 경우 Dynamic Media Classic 구성을 Dynamic Media 폴더에 적용하지 마십시오. 또한 Dynamic Media 구성(처리 프로필)을 Dynamic Media Classic 폴더에 적용하지 마십시오.

## Dynamic Media Classic과 Experience Manager 통합을 위한 우수 사례 {#best-practices-for-integrating-scene-with-aem}

Dynamic Media Classic을 Experience Manager과 통합할 때 다음 영역에서 준수해야 하는 몇 가지 중요한 모범 사례가 있습니다.

* 통합 테스트
* 특정 시나리오에 대해서는 Dynamic Media Classic에서 바로 자산을 업로드하는 것이 좋습니다

[알려진 제한 사항](#known-limitations-and-design-implications)을 참조하십시오.

### 통합 테스트 {#test-driving-your-integration}

Adobe은 루트 폴더가 전체 회사가 아닌 하위 폴더만 가리키도록 하여 통합을 테스트하도록 권장합니다.

>[!CAUTION]
>
>기존 Dynamic Media Classic 회사 계정에서 자산을 가져오는 데 Experience Manager에 표시되는 데 시간이 오래 걸릴 수 있습니다. 자산이 너무 많지 않은 폴더를 Dynamic Media Classic에서 지정하도록 하십시오. 예를 들어 루트 폴더에 자산이 너무 많아 시스템이 충돌할 수 있습니다.

### Dynamic Media Classic과 Experience Manager Assets의 자산 업로드 {#uploading-assets-from-aem-assets-versus-from-scene}

자산 (디지털 자산 관리) 기능을 사용하거나 Dynamic Media Classic 컨텐츠 브라우저를 통해 Experience Manager에서 직접 Dynamic Media Classic에 액세스하여 자산을 업로드할 수 있습니다. 어떤 항목을 선택하느냐에 따라 다음과 같이 달라집니다.

* Experience Manager Assets에서 아직 지원하지 않는 Dynamic Media Classic 자산 유형은 Dynamic Media Classic 컨텐츠 브라우저를 통해 Dynamic Media Classic에서 직접 Experience Manager 웹 사이트에 추가해야 합니다. 예를 들어 이미지 템플릿입니다.
* Experience Manager Assets와 Dynamic Media Classic에서 모두 지원되는 자산 유형의 경우 업로드 방법을 결정하는 것은 다음 사항에 따라 달라집니다.

   * 현재 자산이 있는 곳 AND
   * 공통 저장소에서 관리하는 것이 얼마나 중요합니까?

자산이 이미 Dynamic Media Classic에 있고 공통 저장소에서 관리할 필요가 없다고 가정해 보겠습니다. 이 경우 자산을 Assets으로 내보내기만 하면 Dynamic Media Classic으로 다시 동기화하여 전달할 수 있으므로 불필요한 왕복 이동입니다. Adobe은 자산을 단일 저장소에 유지하고 전달만 위해 Dynamic Media Classic과 동기화하는 것이 좋습니다.

## Dynamic Media Classic 통합 구성 {#configuring-scene-integration}

Dynamic Media Classic에 자산을 업로드하도록 Experience Manager을 구성할 수 있습니다. CQ 대상 폴더의 자산은 Experience Manager에서 Dynamic Media Classic 회사 계정으로 업로드(자동 또는 수동으로)할 수 있습니다.

>[!NOTE]
>
>Adobe은 Dynamic Media Classic 자산을 가져올 때 지정된 대상 폴더만 사용할 것을 권장합니다. 대상 폴더 외부에 있는 디지털 자산은 Dynamic Media Classic 구성이 활성화된 페이지의 Dynamic Media Classic 구성 요소에서만 사용할 수 있습니다. 또한 Dynamic Media Classic의 온디맨드 폴더에 배치됩니다. 온디맨드 폴더는 Experience Manager과 동기화되지 않습니다(하지만 자산은 Dynamic Media Classic 컨텐츠 브라우저에서 검색 가능).

**와 통합하도록 Dynamic Media Classic을 구성하려면 다음을 수행하십시오.**

1. [클라우드 구성 정의](#creating-a-cloud-configuration-for-scene)  - Dynamic Media Classic 폴더와 자산 폴더 간의 매핑을 정의합니다. 단방향(Dynamic Media Classic에 Experience Manager) 동기화만 원하는 경우에도 이 단계를 완료하십시오.
1. [Adobe CQ  **s7dam Listener 활성화**](#enabling-the-adobe-cq-scene-dam-listener)  - OSGiconsole에서   수행됨.
1. Assets Experience Manager이 Dynamic Media Classic에 자동으로 업로드되도록 하려면 해당 옵션을 켜고 Dynamic Media Classic을 [!UICONTROL DAM 자산 업데이트] 워크플로우에 추가해야 합니다. 자산을 수동으로 업로드할 수도 있습니다.
1. 사이드 킥에 Dynamic Media Classic 구성 요소 추가 이 기능을 사용하면 Experience Manager 페이지에서 Dynamic Media Classic 구성 요소를 사용할 수 있습니다.
1. [구성을 Experience Manager의 페이지에 매핑](#enabling-scene-for-wcm)  - Dynamic Media Classic에서 만든 모든 비디오 사전 설정을 보려면 이 단계를 수행해야 합니다. CQ 대상 폴더의 외부에서 Dynamic Media Classic에 자산을 게시하기 위해 수행해야 하는 경우에도 필요합니다.

이 섹션에서는 이러한 모든 단계를 수행하는 방법에 대해 설명하고 중요한 제한 사항을 나열합니다.

### Dynamic Media Classic과 Experience Manager 자산 간의 동기화 작동 방식 {#how-synchronization-between-scene-and-aem-assets-works}

Experience Manager Assets 및 Dynamic Media Classic 동기화를 설정할 때 다음을 이해하는 것이 중요합니다.

#### Experience Manager 자산에서 Dynamic Media Classic으로 업로드 {#uploading-to-scene-from-aem-assets}

* Dynamic Media Classic 업로드를 위한 Experience Manager에 지정된 동기화 폴더가 있습니다.
* 디지털 자산이 지정된 동기화 폴더에 배치된 경우 Dynamic Media Classic에 대한 업로드를 자동화할 수 있습니다.
* Experience Manager의 폴더 및 하위 폴더 구조가 Dynamic Media Classic에 복제됩니다.

>[!NOTE]
>
>Experience Manager은 모든 메타데이터를 Dynamic Media Classic에 업로드하기 전에 XMP으로 포함하므로 메타데이터 노드의 모든 속성을 Dynamic Media Classic에서 XMP으로 사용할 수 있습니다.

#### 알려진 제한 사항 및 디자인 의미 {#known-limitations-and-design-implications}

Experience Manager Assets와 Dynamic Media Classic 간의 동기화를 통해 현재 다음과 같은 제한/디자인 관련 사항이 있습니다.

<table>
 <tbody>
  <tr>
   <td><strong>제한 사항/설계 관련</strong></td>
   <td><strong>설명</strong></td>
  </tr>
  <tr>
   <td>지정된 동기화(대상) 폴더 1개</td>
   <td>Dynamic Media Classic 업로드를 위한 Experience Manager에 회사당 하나의 지정된 폴더만 있을 수 있습니다. Dynamic Media Classic에서 두 개 이상의 회사 계정에 액세스할 수 있어야 하는 경우에는 여러 구성을 만들 수 있습니다.</td>
  </tr>
  <tr>
   <td>폴더 구조</td>
   <td>자산이 있는 동기화된 폴더를 삭제하면 모든 Dynamic Media Classic 원격 자산이 삭제되지만 폴더는 그대로 유지됩니다.</td>
  </tr>
  <tr>
   <td>온디맨드 폴더</td>
   <td>WCM에서 Dynamic Media Classic에 수동으로 업로드하는 대상 폴더 외부에 있는 자산은 Dynamic Media Classic의 별도의 온디맨드 폴더에 자동으로 배치됩니다. Experience Manager의 클라우드 구성에서 이 폴더를 구성합니다.</td>
  </tr>
  <tr>
   <td>혼합 미디어</td>
   <td>혼합 미디어 세트는 Experience Manager에서 지원되지 않지만 Experience Manager에 나타납니다.</td>
  </tr>
  <tr>
   <td>PDF</td>
   <td>Dynamic Media Classic의 eCatalogs에서 생성된 PDF를 CQ 대상 폴더로 가져옵니다.</td>
  </tr>
  <tr>
   <td>UI 새로 고침</td>
   <td>Experience Manager과 Dynamic Media Classic 간을 동기화할 때 사용자 인터페이스를 새로 고쳐 변경 사항을 확인합니다. </td>
  </tr>
  <tr>
   <td>비디오 축소판</td>
   <td>Dynamic Media Classic을 통해 인코딩을 위해 Experience Manager 자산에 비디오를 업로드하는 경우 비디오 처리 시간에 따라 Experience Manager 자산에서 비디오 축소판 및 인코딩된 비디오를 사용할 수 있는 시간이 좀 걸릴 수 있습니다.</td>
  </tr>
  <tr>
   <td>Target 하위 폴더</td>
   <td><p>대상 폴더 내에서 하위 폴더를 사용하는 경우 위치에 관계없이 각 자산에 대해 고유한 이름을 사용해야 합니다. 또한 위치에 관계없이 Dynamic Media Classic이 자산을 덮어쓰지 않도록 설정 영역에서 구성해야 합니다.</p> <p>그렇지 않으면 Dynamic Media Classic 대상 하위 폴더에 업로드된 이름이 같은 자산이 업로드되지만 대상 폴더에서 이름이 같은 자산이 삭제됩니다. </p> </td>
  </tr>
 </tbody>
</table>

### Dynamic Media Classic 서버 구성 {#configuring-scene-servers}

프록시 뒤에서 Experience Manager을 실행하거나 특수 방화벽 설정을 사용하는 경우에는 다른 지역의 호스트를 명시적으로 활성화해야 합니다. 서버는 `/etc/cloudservices/scene7/endpoints`의 컨텐츠에서 관리되며 필요에 따라 사용자 지정할 수 있습니다. 필요한 경우 URL을 선택한 다음 편집하여 URL을 변경합니다. 이전 버전의 Experience Manager에서는 이러한 값이 하드 코딩되었습니다.

`/etc/cloudservices/scene7/endpoints.html`으로 이동하면 나열된 서버가 표시됩니다(URL을 탭하여 편집할 수 있음).

![chlimage_1-296](assets/chlimage_1-296.png)

### Dynamic Media Classic용 클라우드 구성 만들기 {#creating-a-cloud-configuration-for-scene}

클라우드 구성은 Dynamic Media Classic 폴더와 Experience Manager 자산 폴더 간의 매핑을 정의합니다. Experience Manager 자산을 Dynamic Media Classic과 동기화하도록 구성해야 합니다. 자세한 내용은 동기화 작동 방식 을 참조하십시오.

>[!CAUTION]
>
>기존 Dynamic Media Classic 회사 계정에서 자산을 가져오는 데 Experience Manager에 표시되는 데 시간이 오래 걸릴 수 있습니다. Dynamic Media Classic에서 자산이 많지 않은 폴더를 지정하도록 하십시오. 예를 들어 루트 폴더에 자산이 너무 많은 경우가 있습니다.
>
>통합을 테스트하려면 전체 회사 대신 하위 폴더에 대한 루트 폴더 지점만 있어야 합니다.

>[!NOTE]
>
>다음과 같은 여러 구성을 사용할 수 있습니다. 하나의 클라우드 구성은 Dynamic Media Classic 회사에서 한 사용자를 나타냅니다. 다른 Dynamic Media Classic 회사나 사용자에게 액세스하려면 여러 구성을 만들어야 합니다.

**Dynamic Media Classic용 클라우드 구성을 만들려면:**

1. Experience Manager 아이콘을 선택하고 **[!UICONTROL 배포]** > **[!UICONTROL Cloud Services]**&#x200B;로 이동하여 Adobe Dynamic Media Classic에 액세스할 수 있습니다.

1. **[!UICONTROL 지금 구성]**&#x200B;을 선택합니다.

   ![chlimage_1-297](assets/chlimage_1-297.png)

1. **[!UICONTROL 제목]** 필드와 선택적으로 **[!UICONTROL 이름]** 필드에 적절한 정보를 입력합니다. **[!UICONTROL 만들기]**&#x200B;를 선택합니다.

   >[!NOTE]
   >
   >추가 구성을 만들 때 **[!UICONTROL 상위 구성]** 필드가 표시됩니다.
   >
   >**상위 구성을 변경하지 마십시오**. 상위 구성을 변경하면 통합이 중단될 수 있습니다.

1. Dynamic Media Classic 계정의 이메일 주소, 암호 및 영역을 입력하고 **[!UICONTROL Dynamic Media Classic에 연결]**&#x200B;을 선택합니다. Dynamic Media Classic 서버에 연결되고 더 많은 옵션을 사용하여 대화 상자가 확장됩니다.

1. **[!UICONTROL Company]** 이름과 **[!UICONTROL 루트 경로]**&#x200B;를 입력합니다. 이 정보는 지정할 경로와 함께 게시된 서버 이름입니다. 게시된 서버 이름을 모를 경우 Dynamic Media Classic에서 **[!UICONTROL 설정 > 애플리케이션 설정]**)으로 이동합니다.

   >[!NOTE]
   >
   >Dynamic Media Classic 루트 경로는 Dynamic Media Classic 폴더 Experience Manager이 연결되는 경로입니다. 특정 폴더로 축소할 수 있습니다.

   >[!CAUTION]
   >
   >Dynamic Media Classic 폴더의 크기에 따라 루트 폴더를 가져오는 데 시간이 오래 걸릴 수 있습니다. 또한 Dynamic Media Classic 데이터가 Experience Manager 저장소를 초과할 수 있습니다. 올바른 폴더를 가져오고 있는지 확인합니다. 너무 많은 데이터를 가져오면 시스템이 중지될 수 있습니다.

   ![chlimage_1-298](assets/chlimage_1-298.png)

1. **[!UICONTROL 확인]**&#x200B;을 선택합니다. Experience Manager이 구성을 저장합니다.

>[!NOTE]
>
>다시 연결하는 경우:
>
>* 게시 시 Dynamic Media Classic에 다시 연결할 때 게시 시 또는 다시 연결할 때 암호를 재설정해도 작동하지 않습니다(작성자 인스턴스의 문제가 아님).
>* 지역, 회사 이름과 같은 값을 수정하는 경우 Dynamic Media Classic에 다시 연결해야 합니다. 구성 옵션이 수정되었지만 저장되지 않은 경우, Experience Manager이 구성이 올바른지 잘못 나타냅니다. 반드시 다시 연결하십시오.

>



### Adobe CQ Dynamic Media Classic Dam 수신기 활성화 {#enabling-the-adobe-cq-scene-dam-listener}

기본적으로 비활성화된 Adobe CQ Dynamic Media Classic Dam 수신기를 활성화합니다.

**Adobe CQ Dynamic Media Classic Dam 수신기를 활성화하려면**

1. [!UICONTROL 도구] 아이콘을 선택한 다음 **[!UICONTROL 작업]** > **[!UICONTROL 웹 콘솔]**&#x200B;로 이동합니다.
1. 웹 콘솔에서 **[!UICONTROL Adobe CQ Dynamic Media Classic Dam 수신기]**&#x200B;로 이동하고 **[!UICONTROL 활성화됨]** 확인란을 선택합니다.

   ![chlimage_1-299](assets/chlimage_1-299.png)

1. **[!UICONTROL 저장]**&#x200B;을 선택합니다.

### Dynamic Media Classic 업로드 워크플로우에 구성 가능한 시간 제한 추가 {#adding-configurable-timeout-to-scene-upload-workflow}

Dynamic Media Classic을 통해 비디오 인코딩을 처리하도록 Experience Manager 인스턴스가 구성된 경우 기본적으로 업로드 작업에 35분 시간 제한이 있습니다. 실행 중인 비디오 인코딩 작업을 오래 수용하기 위해 이 설정을 구성할 수 있습니다.

1. **http://localhost:4502/system/console/configMgr/com.day.cq.dam.scene7.impl.Scene7UploadServiceImpl**&#x200B;로 이동합니다.

   ![chlimage_1-300](assets/chlimage_1-300.png)

1. **[!UICONTROL 활성 작업 시간 초과]** 필드에서 원하는 대로 숫자를 변경합니다. 음수가 아닌 숫자는 측정 단위로(초) 수락됩니다. 기본적으로 이 숫자는 2100로 설정됩니다.

   >[!NOTE]
   >
   >우수 사례: 대부분의 자산은 최대 몇 분 내에 수집됩니다(예: 이미지). 그러나 특정 경우(예: 큰 비디오) 긴 처리 시간을 수용하도록 시간 초과 값을 7200초(2시간)로 증가시킵니다. 그렇지 않으면 이 Dynamic Media Classic 업로드 작업은 JCR(Java™ Content Repository) 메타데이터에서 **[!UICONTROL UploadFailed]**&#x200B;로 표시됩니다.

1. **[!UICONTROL 저장]**&#x200B;을 선택합니다.

### Experience Manager 자산에서 자동 업로드 {#autouploading-from-aem-assets}

Experience Manager 6.3.2부터 자산이 CQ 대상 폴더에 있는 경우 업로드된 모든 디지털 자산이 Dynamic Media Classic으로 업데이트되도록 Experience Manager 자산이 구성됩니다.

자산이 Dynamic Media Assets에 추가되면 자산이 자동으로 업로드되고 Experience Manager Classic에 게시됩니다.

>[!NOTE]
>
>Experience Manager Assets에서 Dynamic Media Classic으로 자동 업로드하기 위한 최대 파일 크기는 500MB입니다.

**Experience Manager 자산에서 자동 업로드하려면**

1. Experience Manager 아이콘을 선택하고 **[!UICONTROL 배포]** > **[!UICONTROL Cloud Services]**&#x200B;로 이동합니다.
1. Dynamic Media 제목, 사용 가능한 구성 아래에서 **[!UICONTROL dms7(Dynamic Media]**)을 선택합니다.
1. **[!UICONTROL 고급]** 탭을 선택하고 **[!UICONTROL 자동 업로드 활성화]** 확인란을 선택한 다음 **[!UICONTROL 확인]**&#x200B;을 선택합니다. 이제 Dynamic Media Classic에 대한 업로드를 포함하도록 DAM 자산 워크플로우를 구성해야 합니다.

   >[!NOTE]
   >
   >게시 취소된 상태에서 Dynamic Media Classic으로 자산을 푸시하는 방법에 대한 자세한 내용은 Dynamic Media Classic에 푸시된 자산의 상태(게시/게시 취소됨) 구성 을 참조하십시오.[](#configuring-the-state-published-unpublished-of-assets-pushed-to-scene)

   ![screen_shot_2018-03-15at52501pm](assets/screen_shot_2018-03-15at52501pm.jpg)

1. Experience Manager 시작 페이지로 돌아가서 **[!UICONTROL 워크플로우]**&#x200B;를 선택합니다. **DAM 자산 업데이트** 워크플로우를 두 번 클릭하여 엽니다.
1. 사이드 킥에서 **[!UICONTROL 워크플로우]** 구성 요소로 이동하고 **[!UICONTROL Dynamic Media Classic]**&#x200B;을 선택합니다. **[!UICONTROL Dynamic Media Classic]**&#x200B;을(를) 워크플로우로 끌어서 **[!UICONTROL 저장]**&#x200B;을(를) 선택합니다. 대상 폴더의 Experience Manager 자산에 추가된 자산은 Dynamic Media Classic에 자동으로 업로드됩니다.

   ![chlimage_1-301](assets/chlimage_1-301.png)

   >[!NOTE]
   >
   >* 자동화 후 자산을 추가할 때 CQ 대상 폴더에 배치되지 않으면 Dynamic Media Classic에 업로드되지 않습니다.
   >* Experience Manager은 모든 메타데이터를 Dynamic Media Classic에 업로드하기 전에 XMP으로 포함하므로 메타데이터 노드의 모든 속성을 Dynamic Media Classic에서 XMP으로 사용할 수 있습니다.


### Dynamic Media Classic에 푸시된 자산의 상태(게시/게시 취소됨)를 구성합니다 {#configuring-the-state-published-unpublished-of-assets-pushed-to-scene}

자산을 Experience Manager Assets에서 Dynamic Media Classic으로 푸시할 경우, 자동으로(기본 동작)게시하거나, 게시 취소된 상태로 Dynamic Media Classic에 푸시할 수 있습니다.

라이브로 전환하기 전에 스테이징 환경에서 자산을 테스트하려는 경우 Dynamic Media Classic에 자산을 즉시 게시하지 않을 수 있습니다. Dynamic Media Classic의 보안 테스트 환경과 함께 Experience Manager을 사용하여 자산을 Dynamic Media Classic에서 게시되지 않은 상태로 직접 푸시할 수 있습니다.

Dynamic Media Classic 자산은 보안 미리 보기를 통해 계속 사용할 수 있습니다. 자산이 Experience Manager 내에 게시될 때만 Dynamic Media Classic 자산도 프로덕션에서 라이브로 전환됩니다.

Dynamic Media Classic으로 자산을 푸시할 때 자산을 즉시 게시하려면 옵션을 구성할 필요가 없습니다. 이 기능은 기본 동작입니다.

그러나 Dynamic Media Classic으로 푸시된 자산이 자동으로 게시되지 않게 하려면 이 섹션에서는 이 기능을 수행하도록 Experience Manager 및 Dynamic Media Classic을 구성하는 방법에 대해 설명합니다.

#### Dynamic Media Classic에 자산을 푸시하기 위한 사전 요구 사항 게시 취소됨 {#prerequisites-to-push-assets-to-scene-unpublished}

자산을 게시하지 않고 Dynamic Media Classic에 푸시하려면 먼저 다음을 설정해야 합니다.

1. [Admin Console을 사용하여 지원 사례를 만듭니다](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/support-for-experience-cloud.ug.html). 지원 사례에서 Dynamic Media Classic 계정에 대한 보안 미리 보기 활성화를 요청합니다.
1. [Dynamic Media Classic 계정에 대한 보안 미리 보기를 설정합니다](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/upload-publish/testing-assets-making-them-public.html?lang=en).

이러한 단계는 Dynamic Media Classic에서 보안 테스트 설정을 만들기 위해 수행하는 것과 동일합니다.

>[!NOTE]
>
>설치 환경이 UNIX® 64비트 운영 체제인 경우 설정해야 하는 다른 구성 옵션에 대해서는 [https://helpx.adobe.com/experience-manager/kb/enable-xmp-write-back-64-bit-redhat.html](https://helpx.adobe.com/experience-manager/kb/enable-xmp-write-back-64-bit-redhat.html)을 참조하십시오.

#### 게시 취소된 상태에서 자산을 푸시하기 위한 알려진 제한 사항  {#known-limitations-for-pushing-assets-in-unpublished-state}

이 기능을 사용하는 경우 다음 제한 사항을 참고하십시오.

* 버전 제어를 지원하지 않습니다.
* 자산이 이미 Experience Manager에 게시되어 있고 후속 버전이 만들어진 경우, 해당 새 버전이 즉시 프로덕션에 라이브로 게시됩니다. 활성화 시 게시 는 자산의 초기 게시에서만 작동합니다.

>[!NOTE]
>
>자산을 즉시 게시하려면 **[!UICONTROL 보안 미리 보기 활성화]**&#x200B;를 **[!UICONTROL 즉시]**&#x200B;로 설정하고 **[!UICONTROL 자동 업로드 활성화]** 기능을 사용하는 것이 좋습니다.

### Dynamic Media Classic에 푸시된 자산의 상태를 게시 취소됨으로 설정합니다 {#setting-the-state-of-assets-pushed-to-scene-as-unpublished}

>[!NOTE]
>
>사용자가 Experience Manager에서 자산을 게시하면 S7 자산이 프로덕션/라이브 자산으로 자동 트리거됩니다(자산이 더 이상 보안 미리 보기/게시 취소되지 않음).

**Dynamic Media Classic에 푸시된 자산의 상태를 게시 취소됨으로 설정하려면 다음을 수행하십시오.**

1. Experience Manager 아이콘을 선택하고 **[!UICONTROL 배포]** > **[!UICONTROL Cloud Services]**&#x200B;로 이동합니다.
1. **[!UICONTROL Dynamic Media Classic]**&#x200B;을 선택합니다.
1. Dynamic Media Classic에서 구성을 선택합니다.
1. **[!UICONTROL 고급]** 탭을 선택합니다.
1. **[!UICONTROL 보안 보기 활성화]** 드롭다운 메뉴에서 **[!UICONTROL AEM 게시 활성화 시]**&#x200B;를 선택하여 자산을 게시하지 않고 Dynamic Media Classic에 푸시합니다. 기본적으로 이 값은 **[!UICONTROL 즉시]**&#x200B;로 설정되며, 여기서 Dynamic Media Classic 자산이 즉시 게시됩니다.

   자산을 공개하기 전에 테스트하기 위한 자세한 내용은 [Dynamic Media Classic 설명서](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/upload-publish/testing-assets-making-them-public.html) 를 참조하십시오.

   ![chlimage_1-302](assets/chlimage_1-302.png)

1. **[!UICONTROL 확인]**&#x200B;을 선택합니다.

보안 미리 보기를 활성화하면 자산이 게시 취소된 보안 미리 보기 서버로 푸시됩니다.

**[!UICONTROL 보안 미리 보기]**&#x200B;가 활성화되어 있는지 확인하려면 Experience Manager의 페이지에서 Dynamic Media Classic 구성 요소로 이동합니다. **[!UICONTROL 편집]**&#x200B;을 선택하십시오. 자산에 URL에 나열된 보안 미리 보기 서버가 있습니다. Experience Manager에 게시하면 파일 참조의 서버 도메인이 미리 보기 URL에서 프로덕션 URL로 업데이트됩니다.

### WCM용 Dynamic Media Classic 활성화 {#enabling-scene-for-wcm}

WCM용 Dynamic Media Classic을 활성화해야 하는 이유는 두 가지가 있습니다.

* 페이지 작성을 위한 범용 비디오 프로필 드롭다운 목록을 사용할 수 있습니다. 이 목록이 없으면 **[!UICONTROL 범용 비디오 사전 설정]** 드롭다운이 비어 있으므로 설정할 수 없습니다.
* 디지털 자산이 대상 폴더에 없는 경우 페이지 속성에서 해당 페이지에 대해 Dynamic Media Classic을 활성화하면 자산을 Dynamic Media Classic에 업로드할 수 있습니다. 그런 다음 자산을 Dynamic Media Classic 구성 요소에 끌어다 놓습니다. 일반 상속 규칙이 적용됩니다(하위 페이지가 상위 페이지에서 구성을 상속함).

다른 구성과 마찬가지로 WCM에 대해 Dynamic Media Classic을 활성화하면 상속 규칙이 적용됩니다. 터치에 적합한 사용자 인터페이스나 클래식 사용자 인터페이스에서 WCM용 Dynamic Media Classic을 활성화할 수 있습니다.

#### 터치에 적합한 사용자 인터페이스에서 WCM용 Dynamic Media Classic 활성화 {#enabling-scene-for-wcm-in-the-touch-optimized-user-interface}

1. Experience Manager 아이콘을 선택하고 **[!UICONTROL 사이트]**&#x200B;로 이동한 다음, 웹 사이트의 루트 페이지(언어별 페이지 아님)로 이동합니다.

1. 도구 모음에서 [!UICONTROL 설정] 아이콘을 선택하고 **[!UICONTROL 속성 열기]**&#x200B;를 선택합니다.

1. **[!UICONTROL Cloud Services]**&#x200B;구성 추가&#x200B;]**를 선택하고**[!UICONTROL  Dynamic Media Classic ]**을 선택합니다.**[!UICONTROL 
1. **[!UICONTROL Dynamic Media Classic Adobe]** 드롭다운 목록에서 원하는 구성을 선택하고 **[!UICONTROL 확인]**&#x200B;을 선택합니다.

   ![chlimage_1-303](assets/chlimage_1-303.png)

   해당 Dynamic Media Classic 구성의 비디오 사전 설정은 해당 페이지 및 하위 페이지에서 Dynamic Media Classic 비디오 구성 요소와 함께 Experience Manager에서 사용할 수 있습니다.

#### 클래식 사용자 인터페이스에서 WCM용 Dynamic Media Classic 활성화 {#enabling-scene-for-wcm-in-the-classic-user-interface}

1. Experience Manager에서 **[!UICONTROL 웹 사이트]**&#x200B;를 선택하고 웹 사이트의 루트 페이지로 이동합니다(언어별 페이지 아님).

1. 사이드 킥에서 **[!UICONTROL 페이지]** 아이콘을 선택하고 **[!UICONTROL 페이지 속성]**&#x200B;을 선택합니다.

1. **[!UICONTROL Cloud Services]** > **[!UICONTROL 서비스 추가]** > **[!UICONTROL Dynamic Media Classic]**&#x200B;을 선택합니다.
1. **[!UICONTROL Dynamic Media Classic Adobe]** 드롭다운 목록에서 원하는 구성을 선택하고 **[!UICONTROL 확인]**&#x200B;을 선택합니다.

   해당 Dynamic Media Classic 구성의 비디오 사전 설정은 해당 페이지 및 하위 페이지에서 Dynamic Media Classic 비디오 구성 요소와 함께 Experience Manager에서 사용할 수 있습니다.

### 기본 구성 구성 {#configuring-a-default-configuration}

Dynamic Media Classic 구성이 여러 개 있는 경우 이 구성 중 하나를 Dynamic Media Classic 컨텐츠 브라우저의 기본값으로 지정할 수 있습니다.

특정 시점에 하나의 Dynamic Media Classic 구성만 기본값으로 표시할 수 있습니다. 기본 구성은 Dynamic Media Classic 컨텐츠 브라우저에 기본적으로 표시되는 회사 자산입니다.

**기본 구성을 구성하려면:**

1. Experience Manager 아이콘을 선택하고 **[!UICONTROL 배포]** > **[!UICONTROL Cloud Services]**&#x200B;로 이동합니다.
1. **[!UICONTROL Dynamic Media Classic]**&#x200B;을 선택합니다.
1. Dynamic Media Classic에서 구성을 선택합니다.
1. 구성을 열려면 **[!UICONTROL 편집]**&#x200B;을 선택합니다.

1. **[!UICONTROL 일반]** 탭에서 **[!UICONTROL 기본 구성]** 확인란을 선택하여 Dynamic Media Classic 콘텐츠 브라우저에 표시되는 기본 회사와 루트 경로로 만듭니다.

   ![chlimage_1-304](assets/chlimage_1-304.png)

   >[!NOTE]
   >
   >구성이 하나만 있는 경우 **[!UICONTROL 기본 구성]** 확인란을 선택하면 아무 영향이 없습니다.

### 임시 폴더 구성 {#configuring-the-ad-hoc-folder}

자산이 CQ 대상 폴더에 없을 때 Dynamic Media Classic에서 자산이 업로드되도록 온디맨드 폴더를 구성할 수 있습니다. CQ 대상 폴더 외부에서 자산 게시 를 참조하십시오.

**임시 폴더를 구성하려면 다음을 수행하십시오.**

1. Experience Manager 아이콘을 선택하고 **[!UICONTROL 배포]** > **[!UICONTROL Cloud Services]**&#x200B;로 이동합니다.
1. **[!UICONTROL Dynamic Media Classic]**&#x200B;을 선택합니다.
1. Dynamic Media Classic에서 구성을 선택합니다.
1. 구성을 열려면 **[!UICONTROL 편집]**&#x200B;을 선택합니다.

1. **[!UICONTROL 고급]** 탭을 선택합니다. **[!UICONTROL 애드혹 폴더]** 필드에서 **애드혹** 폴더를 수정할 수 있습니다. 기본적으로 **name_of_the_company/CQ5_adhoc**&#x200B;입니다.

   ![chlimage_1-305](assets/chlimage_1-305.png)

### 범용 비디오 사전 설정 구성 {#configuring-universal-presets}

비디오 구성 요소에 대한 범용 비디오 사전 설정을 구성하려면 [비디오](/help/assets/s7-video.md)를 참조하십시오.

## MIME 유형 기반 Assets/Dynamic Media Classic 업로드 작업 매개 변수 지원 활성화 {#enabling-mime-type-based-assets-scene-upload-job-parameter-support}

Digital Asset Manager/Dynamic Media Classic 자산의 동기화에 의해 트리거되는 구성 가능한 Dynamic Media Classic 업로드 작업 매개 변수를 활성화할 수 있습니다.

특히 [Experience Manager 웹 콘솔 구성] 패널의 OSGi(Open Service Gateway Initiative) 영역에서 MIME 유형별로 허용 파일 형식을 구성합니다. 그런 다음 JCR(Java™ Content Repository)에서 각 MIME 유형에 사용할 개별 업로드 작업 매개 변수를 사용자 지정할 수 있습니다.

**MIME 유형 기반 자산을 활성화하려면:**

1. Experience Manager 아이콘을 선택하고 **[!UICONTROL 도구]** > **[!UICONTROL 작업]** > **[!UICONTROL 웹 콘솔]**&#x200B;로 이동합니다.
1. Adobe Experience Manager 웹 콘솔 구성 패널의 **[!UICONTROL OSGi]** 메뉴에서 **[!UICONTROL 구성]**&#x200B;을 선택합니다.
1. 이름 열에서 **[!UICONTROL Adobe CQ Dynamic Media Classic Asset MIME 유형 서비스]**&#x200B;를 찾아 선택하여 구성을 편집합니다.
1. MIME 유형 매핑 영역에서 더하기 기호(+)를 선택하여 MIME 유형을 추가합니다.

   [지원되는 MIME 유형](/help/assets/assets-formats.md#supported-mime-types)을 참조하십시오.

1. 텍스트 필드에 새 MIME 유형 이름을 입력합니다.

   예를 들어 `EPS=application/postscript` 또는 `PSD=image/vnd.adobe.photoshop`에 `<file_extension>=<mime_type>`을 입력합니다.

1. 구성 창의 오른쪽 아래 모서리에서 **[!UICONTROL 저장]**&#x200B;을 선택합니다.
1. Experience Manager으로 돌아가서 왼쪽 레일에서 **[!UICONTROL CRXDE Lite]**&#x200B;을 선택합니다.
1. CRXDE Lite 페이지의 왼쪽 레일에서 `/etc/cloudservices/scene7/<environment>` (실제 이름의 경우 `<environment>` 대체)로 이동합니다.
1. `<environment>`(실제 이름의 `<environment>` 대체)를 확장하여 `mimeTypes` 노드를 표시합니다.
1. 방금 추가한 mimeType을 선택합니다.

   예: `mimeTypes > application_postscript` 또는 `mimeTypes > image_vnd.adobe.photoshop`

1. CRXDE Lite 페이지의 오른쪽에서 **[!UICONTROL 속성]** 탭을 선택합니다.
1. **[!UICONTROL jobParam]** 값 필드에서 Dynamic Media Classic 업로드 작업 매개 변수를 지정합니다.

   예, `psprocess="rasterize"&psresolution=120` .

   사용할 수 있는 업로드 작업 매개 변수에 대한 자세한 내용은 [Dynamic Media Classic 이미지 프로덕션 시스템 API](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-production-api/c-overview.html)를 참조하십시오.

   >[!NOTE]
   >
   >PSD 파일을 업로드하고 레이어 추출 시 템플릿으로 처리하려는 경우 **[!UICONTROL jobParam]** 값 필드에 다음을 입력합니다.
   >
   >`process=MaintainLayers&layerNaming=AppendName&createTemplate=true`
   >
   >PSD 파일에 &quot;레이어&quot;가 있는지 확인하십시오. 한 개의 이미지나 마스크가 있는 이미지라면 처리할 레이어가 없으므로 이미지로 처리됩니다.

1. CRXDE Lite 페이지의 왼쪽 위 모서리에서 **[!UICONTROL 모두 저장]**&#x200B;을 선택합니다.

## Dynamic Media Classic 및 Experience Manager 통합 문제 해결 {#troubleshooting-scene-and-aem-integration}

Dynamic Media Classic과 Experience Manager을 통합하는 데 문제가 있는 경우, 솔루션에 대한 다음 시나리오를 참조하십시오.

**Dynamic Media Classic에 디지털 자산 게시가 실패하는 경우:**

* 업로드하고 있는 자산이 **[!UICONTROL CQ target]** 폴더에 있는지 확인합니다(Dynamic Media Classic 클라우드 구성에서 이 폴더를 지정합니다).
* 그렇지 않은 경우 **[!UICONTROL CQ 애드혹]** 폴더에 업로드할 수 있도록 해당 페이지의 **[!UICONTROL 페이지 속성]**&#x200B;에서 클라우드 구성을 구성해야 합니다.

* 로그에서 정보를 확인합니다.

**비디오 사전 설정이 표시되지 않는 경우:**

* **[!UICONTROL 페이지 속성]**&#x200B;을 통해 해당 페이지의 클라우드 구성을 구성했는지 확인합니다. Dynamic Media Classic 비디오 구성 요소에서 비디오 사전 설정을 사용할 수 있습니다.

**비디오 자산이 Experience Manager에서 재생되지 않는 경우:**

* 올바른 비디오 구성 요소를 사용했는지 확인합니다. Dynamic Media Classic 비디오 구성 요소는 기본 비디오 구성 요소와 다릅니다. [기본 비디오 구성 요소와 Dynamic Media Classic 비디오 구성 요소](/help/assets/s7-video.md)를 참조하십시오.

**Experience Manager의 새 자산이나 수정된 자산이 Dynamic Media Classic에 자동으로 업로드되지 않는 경우:**

* 자산이 CQ 대상 폴더에 있는지 확인합니다. CQ 대상 폴더에 있는 자산만 자동으로 업데이트됩니다(자산을 자동으로 업로드하도록 Experience Manager 자산을 구성한 경우).
* 자동 업로드를 활성화하도록 Cloud Services 구성을 구성했으며 Dynamic Media Classic 업로드를 포함하도록 DAM 자산 워크플로우를 업데이트 및 저장했는지 확인합니다.
* Dynamic Media Classic 대상 폴더의 하위 폴더에 이미지를 업로드할 때 다음 중 하나를 수행해야 합니다.

   * 위치에 상관없이 모든 자산의 이름이 고유한지 확인합니다. 그렇지 않으면 기본 대상 폴더의 자산이 삭제되고 하위 폴더에 있는 자산만 유지됩니다.
   * Dynamic Media Classic이 Dynamic Media Classic 계정의 설정 영역에서 자산을 덮어쓰는 방식을 변경합니다. 하위 폴더에 동일한 이름의 자산을 사용하는 경우 위치에 관계없이 자산을 덮어쓰도록 Dynamic Media Classic을 설정하지 마십시오.

**삭제된 자산 또는 폴더가 Dynamic Media Classic과 Experience Manager 간에 동기화되지 않는 경우:**

* Experience Manager Assets에서 삭제된 자산 및 폴더는 Dynamic Media Classic의 동기화된 폴더에 계속 표시됩니다. 수동으로 삭제합니다.

**비디오 업로드에 실패하는 경우:**

* 비디오 업로드가 실패하고 Experience Manager을 사용하여 Dynamic Media Classic 통합을 통해 비디오를 인코딩하는 경우 [Dynamic Media Classic 업로드 워크플로우에 구성 가능한 시간 초과 추가](#adding-configurable-timeout-to-scene-upload-workflow)를 참조하십시오.

>[!CAUTION]
>
>기존 Dynamic Media Classic 회사 계정에서 자산을 가져오는 데 Experience Manager에 표시되는 데 시간이 오래 걸릴 수 있습니다. Dynamic Media Classic에서 자산이 많지 않은 폴더를 지정하도록 하십시오. 예를 들어 루트 폴더에 자산이 너무 많은 경우가 있습니다.
>
>통합을 테스트하려면 전체 회사 대신 하위 폴더에 대한 루트 폴더 지점만 있어야 합니다.
