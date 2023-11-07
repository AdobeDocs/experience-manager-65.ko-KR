---
title: Adobe Analytics 속성을 사용하여 구성 요소 데이터 매핑
description: 구성 요소 데이터를 SiteCatalyst 속성과 매핑하는 방법을 알아봅니다.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
docset: aem65
exl-id: c7c0c705-ec16-40f5-ad08-193f82d01263
source-git-commit: fc2f26a69c208947c14e8c6036825bb217901481
workflow-type: tm+mt
source-wordcount: '1439'
ht-degree: 1%

---

# Adobe Analytics 속성을 사용하여 구성 요소 데이터 매핑{#mapping-component-data-with-adobe-analytics-properties}

Adobe Analytics으로 전송할 데이터를 수집하는 프레임워크에 구성 요소를 추가합니다. 분석 데이터를 수집하도록 설계된 구성 요소는 데이터를 적절한 위치에 저장합니다 **CQ 변수**. 이러한 구성 요소를 프레임워크에 추가하면 프레임워크에 CQ 변수 목록이 표시되므로 각 변수를 적절하게 추가할 수 있습니다 **Analytics 변수**.

![aa-](assets/aa-11.png)

다음의 경우 **AEM 보기** 가 열려 있습니다. Analytics 변수가 컨텐츠 파인더에 나타납니다.

![aa-](assets/aa-12.png)

여러 Analytics 변수를 동일한 로 매핑할 수 있습니다 **CQ 변수**.

![chlimage_1-68](assets/chlimage_1-68.png)

페이지가 로드되고 다음 조건이 충족되면 매핑된 데이터가 Adobe Analytics으로 전송됩니다.

* 페이지가 프레임워크와 연결됩니다.
* 이 페이지는 프레임워크에 추가된 구성 요소를 사용합니다.

다음 절차를 사용하여 CQ 구성 요소 변수를 Adobe Analytics 보고서 속성에 매핑합니다.

1. 다음에서 **AEM 보기**, 사이드 킥에서 추적 구성 요소를 프레임워크로 드래그합니다. 예를 들어 **페이지** 의 구성 요소 **일반** 범주.

   ![aa-](assets/aa-13.png)

   몇 가지 기본 구성 요소 그룹이 있습니다. **일반**, **상거래**, **커뮤니티**, 및 **기타**. AEM 인스턴스는 다른 그룹 및 구성 요소를 표시하도록 구성할 수 있습니다.

1. Adobe Analytics 변수를 구성 요소에 정의된 변수와 매핑하려면 **Analytics 변수** 콘텐츠 파인더에서 추적 구성 요소의 필드로 이동합니다. 예: 드래그 `Page Name (pageName)` 끝 `pagedata.title`.

   ![aa-](assets/aa-14.png)

   >[!NOTE]
   >
   >프레임워크에 대해 선택된 RSID(보고서 세트 ID)는 콘텐츠 파인더에 나타나는 Adobe Analytics 변수를 결정합니다.

1. 다른 구성 요소 및 변수에 대해 이전 두 단계를 반복합니다.

   >[!NOTE]
   >
   >여러 Analytics 변수를 매핑할 수 있습니다(예: `props`, `eVars`, `events`)를 동일한 CQ 변수에 추가합니다(예: `pagedata.title`)

   >[!CAUTION]
   >
   >다음을 수행하는 것이 좋습니다.
   >
   >* `eVars` 및 `props` 다음 중 하나로 시작하는 CQ 변수에 매핑됩니다. `pagedata.X` 또는 `eventdata.X`
   >* 반면에 이벤트는 다음으로 시작하는 변수에 매핑되어야 합니다. `eventdata.events.X`

1. 사이트의 게시 인스턴스에서 프레임워크를 사용할 수 있도록 하려면 **페이지** 사이드 킥 탭 및 클릭 **프레임워크를 활성화합니다.**

## 제품 관련 변수 매핑 {#mapping-product-related-variables}

AEM에서는 Adobe Analytics 제품 관련 속성에 매핑될 제품 관련 변수와 이벤트의 이름을 지정하는 규칙을 사용합니다.

| CQ 변수 | Analytics 변수 | 설명 |
|--- |--- |--- |
| `product.category` | `product.category` (전환 변수) | 제품 범주. |
| `product.sku` | `product.sku` (전환 변수) | 제품 sku. |
| `product.quantity` | `product.quantity` (전환 변수) | 구매 중인 제품 수입니다. |
| `product.price` | `product.price` (전환 변수) | 제품 가격. |
| `product.events.<eventName>` | 보고서에서 제품과 연결할 성공 이벤트입니다. | `product.events` 는 이라는 이벤트의 접두사입니다. *eventName.* |
| `product.evars.<eVarName>` | 전환 변수( `eVar`)을 클릭하여 제품과 연결합니다. | `product.evars` 는 eVar 변수의 접두사입니다. *eVarName.* |

여러 AEM Commerce 구성 요소는 이러한 변수 이름을 사용합니다.

>[!NOTE]
>
>Adobe Analytics 제품 속성을 CQ 변수에 매핑하지 마십시오. 표에 설명된 대로 제품 관련 매핑을 구성하는 것은 제품 변수를 매핑하는 것과 사실상 동일합니다.

### Adobe Analytics 보고서 확인 {#checking-reports-on-adobe-analytics}

1. AEM에 제공된 것과 동일한 자격 증명을 사용하여 Adobe Analytics 웹 사이트에 로그인합니다.
1. 선택한 RSID가 이전 단계에서 사용한 RSID인지 확인합니다.
1. 위치 **보고서** (페이지 왼쪽) 을 선택합니다. **사용자 지정 전환**, 그런 다음 **사용자 지정 전환 1-10** 및 에 해당하는 변수 선택 `eVar7`

1. 사용 중인 Adobe Analytics 버전에 따라 사용된 검색어로 보고서가 업데이트될 때까지 평균 45분 정도 기다려야 합니다(예: 예에서 가지).

## Adobe Analytics 프레임워크에서 컨텐츠 파인더(cf#) 사용 {#using-the-content-finder-cf-with-adobe-analytics-frameworks}

처음에는 Adobe Analytics 프레임워크를 열 때 컨텐츠 파인더에 사전 정의된 Analytics 변수가 포함되어 있습니다.

* 트래픽
* 전환
* 이벤트

RSID를 선택하면 해당 RSID에 속하는 모든 변수가 목록에 추가됩니다.\
다음 `cf#` Analytics 변수를 다른 추적 구성 요소에 있는 CQ 변수에 매핑하는 데 필요합니다. 기본 추적을 위한 프레임워크 설정을 참조하십시오.

프레임워크에 대해 선택한 보기에 따라 컨텐츠 파인더는 Analytics 변수(AEM 보기의 경우) 또는 CQ 변수(Analytics 보기의 경우)로 채워집니다.

목록은 다음과 같은 방법으로 조작할 수 있습니다.

1. 다음 시기 **AEM 보기**&#x200B;세 개의 필터 버튼을 사용하여 선택한 변수 유형에 따라 목록을 필터링할 수 있습니다.

   * If *단추 없음* 이(가) 선택되면 목록에 전체 목록이 표시됩니다.
   * 다음과 같은 경우 **트래픽** 버튼을 선택하면 목록에 트래픽 섹션에 속하는 변수만 표시됩니다.
   * 다음과 같은 경우 **전환** 버튼을 선택하면 전환 섹션에 속하는 변수만 목록에 표시됩니다.
   * 다음과 같은 경우 **이벤트** 버튼을 선택하면 목록에 이벤트 섹션에 속하는 변수만 표시됩니다.

   >[!NOTE]
   >
   >한 번에 하나의 필터 버튼만 활성화할 수 있습니다.

   1. 목록에는 검색 필드에 입력한 텍스트에 따라 요소를 필터링하는 검색 기능도 있습니다.
   1. 목록에서 요소를 검색하는 동안 필터 옵션이 활성화되면 표시된 결과가 활성 단추에 따라 필터링됩니다.
   1. 언제든지 소용돌이 화살표 버튼을 사용하여 목록을 다시 로드할 수 있습니다.
   1. 프레임워크에서 여러 RSID를 선택한 경우 선택한 RSID 내에서 사용된 모든 레이블을 사용하여 목록의 모든 변수가 표시됩니다.

1. Adobe Analytics 보기에서는 컨텐츠 파인더가 CQ 보기에서 드래그한 추적 구성 요소에 속하는 모든 CQ 변수를 표시합니다.

   * 예를 들어, **구성 요소 다운로드** 은(는) *한 번만 드래그됨* CQ 보기(매핑 가능한 변수가 두 개 있음)에서 *eventdata.downloadLink* 및 *eventdata.events.startDownload*) Adobe Analytics 보기로 전환할 때 콘텐츠 파인더는 다음과 같이 표시됩니다.

   ![aa-22](assets/aa-22.png)

   * Adobe Analytics 변수를 세 변수 섹션(**트래픽**, **전환** 및 **이벤트**).

   * 새 추적 구성 요소를 CQ 보기의 프레임워크로 드래그하면 구성 요소에 속한 CQ 변수가 Adobe Analytics 보기의 콘텐츠 파인더(cf#)에 자동으로 추가됩니다.

   >[!NOTE]
   >
   >주어진 시간에 하나의 CQ 변수만 Adobe Analytics 변수에 매핑할 수 있습니다.

## AEM 보기 및 Analytics 보기 사용 {#using-aem-view-and-analytics-view}

지정된 시간에 프레임워크 페이지에서 Adobe Analytics 매핑을 보는 두 가지 방법 간을 전환할 수 있습니다. 두 가지 관점은 프레임워크 내의 매핑에 대한 보다 나은 개요를 제공합니다.

### AEM 보기 {#aem-view}

![aa-](assets/aa-23.png)

위의 이미지를 예로 들자면 **AEM 보기** 에는 다음 속성이 있습니다.

1. 프레임워크가 열릴 때의 기본 보기입니다.
1. 왼쪽: 콘텐츠 파인더(cf#)는 선택한 RSID를 기반으로 Adobe Analytics 변수로 채워집니다.
1. 탭 머리글(**AEM 보기** 및 **Analytics 보기**): 두 보기 사이를 전환하려면 이 두 보기를 사용합니다.

1. **AEM 보기**:

   1. 프레임워크에 상위 항목에서 상속된 구성 요소가 있는 경우 구성 요소에 매핑된 변수와 함께 여기에 나열됩니다.

      1. 상속된 구성 요소가 잠겨 있습니다.
      1. 상속된 구성 요소의 잠금을 해제하려면 구성 요소 이름 옆에 있는 자물쇠를 두 번 클릭합니다
      1. 상속을 되돌리려면 잠금 해제된 구성 요소를 삭제합니다. 그런 다음 잠김 상태를 회복합니다.

   1. **여기에 구성 요소를 끌어 놓아 분석 프레임워크에 포함하십시오.**: 구성 요소를 Sidekick에서 드래그하여 여기에 놓을 수 있습니다.
   1. 현재 분석 프레임워크에 포함된 모든 구성 요소를 찾을 수 있습니다.

      1. 구성 요소를 추가하려면 사이드 킥의 구성 요소 탭에서 하나를 드래그합니다.
      1. 구성 요소와 모든 매핑을 삭제하려면 구성 요소의 컨텍스트 메뉴에서 삭제 를 선택한 다음 확인 대화 상자에서 삭제를 승인합니다.
      1. 구성 요소는 생성된 프레임워크에서만 삭제할 수 있으며 기존 의미의 하위 프레임워크에서는 삭제할 수 없습니다(덮어쓰기만 가능).

### Analytics 보기 {#analytics-view}

![aa-](assets/aa-24.png)

1. 이 보기는 로 전환하여 액세스할 수 있습니다. **Analytics 보기** 프레임워크의 탭입니다.
1. 왼쪽: CQ 보기에서 프레임워크로 드래그한 구성 요소를 기반으로 CQ 변수로 채워진 콘텐츠 파인더(cf#).
1. 탭 머리글(**AEM 보기** 및 **Analytics 보기**): 두 보기 사이를 전환하려면 이 두 보기를 사용합니다.

1. 세 개의 테이블(트래픽, 전환, 이벤트)에는 사용 가능한 모든 Adobe Analytics 변수가 나열되어 있습니다. 을(를) 선택한 RSID에 속합니다. 여기에 표시된 매핑은 AEM 보기와 동일해야 합니다.

   * **트래픽**:

      * 트래픽 변수( `prop1`)이 CQ 변수에 매핑되었습니다( `eventdata.downloadLink`)

      * 구성 요소 옆에 자물쇠가 있으면 상위 프레임워크에서 상속되었으므로 구성 요소를 편집할 수 없습니다

   * **전환**:

      * 전환 변수( `eVar1`)이 CQ 변수에 매핑되었습니다( `pagedata.title`)

      * 전환 변수( `eVar3`)CQ 변수 필드를 두 번 클릭하고 코드를 수동으로 입력하여 인라인에 추가된 JavaScript 표현식에 매핑됩니다

   * **이벤트**:

      * 이벤트 변수( `event1`)이 CQ 이벤트에 매핑됨( `eventdata.events.pageView`)

>[!NOTE]
>
>필드를 두 번 클릭하고 텍스트를 추가하여 테이블의 CQ 변수 열도 인라인으로 채울 수 있습니다. 이러한 필드는 JavaScript를 입력으로 허용합니다.
>
>예를 들어 다음 `prop3` 다음을 추가할 수 있습니다.
>     `'`* `Adobe:'+pagedata.title+':'+pagedata.sitesection`\
을(를) 전송하려면 *제목* 와 연결된 페이지 *sitesection* 사용 *:* (콜론) 및 접두사가 있는 *Adobe* 다음으로: `prop3`
>

>[!CAUTION]
>
주어진 시간에 하나의 CQ 변수만 Adobe Analytics 변수에 매핑할 수 있습니다.
