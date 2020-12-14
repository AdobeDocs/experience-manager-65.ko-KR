---
title: Adobe Analytics 속성을 사용하여 구성 요소 데이터 매핑
seo-title: Adobe Analytics 속성을 사용하여 구성 요소 데이터 매핑
description: SiteCatalyst 속성을 사용하여 구성 요소 데이터를 매핑하는 방법을 알아봅니다.
seo-description: SiteCatalyst 속성을 사용하여 구성 요소 데이터를 매핑하는 방법을 알아봅니다.
uuid: b08ab37f-ad58-4c04-978f-8e21a3823ae8
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: 6c1f8869-62d9-4fac-aa0d-b99bb0e86d6b
docset: aem65
translation-type: tm+mt
source-git-commit: 6f49e01aa3e9841c7b2917870593452b778667d2
workflow-type: tm+mt
source-wordcount: '1470'
ht-degree: 0%

---


# Adobe Analytics 속성을 사용하여 구성 요소 데이터 매핑{#mapping-component-data-with-adobe-analytics-properties}

Adobe Analytics으로 전송할 데이터를 수집하는 프레임워크에 구성 요소를 추가합니다. 분석 데이터를 수집하도록 설계된 구성 요소는 데이터를 적절한 **CQ 변수**&#x200B;에 저장합니다. 이러한 구성 요소를 프레임워크에 추가하면 프레임워크에 CQ 변수 목록이 표시되므로 각각 적절한 **Analytics 변수**&#x200B;에 액세스할 수 있습니다.

![aa-11](assets/aa-11.png)

**AEM 보기**&#x200B;가 열리면 Analytics 변수가 Content Finder에 나타납니다.

![aa-12](assets/aa-12.png)

동일한 **CQ 변수**&#x200B;로 여러 Analytics 변수를 매핑할 수 있습니다.

![chlimage_1-68](assets/chlimage_1-68.png)

매핑된 데이터는 페이지가 로드되고 다음 조건이 충족되면 Adobe Analytics으로 전송됩니다.

* 페이지가 프레임워크와 연결됩니다.
* 페이지는 프레임워크에 추가되는 구성 요소를 사용합니다.

다음 절차를 사용하여 CQ 구성 요소 변수를 Adobe Analytics 보고서 속성과 매핑하십시오.

1. **AEM 보기**&#x200B;에서 사이드킥의 추적 구성 요소를 프레임워크로 드래그합니다. 예를 들어 **일반** 범주에서 **페이지** 구성 요소 구성 요소를 드래그합니다.

   ![aa-13](assets/aa-13.png)

   다음과 같은 몇 가지 기본 구성 요소 그룹이 있습니다.**일반**, **상거래**, **커뮤니티**, **Search &amp; Promote** 및 **기타**. AEM 인스턴스는 다른 그룹 및 구성 요소를 표시하도록 구성할 수 있습니다.

1. Adobe Analytics 변수를 구성 요소에 정의된 변수와 매핑하려면 컨텐츠 파인더의 **Analytics 변수**&#x200B;를 추적 구성 요소의 필드로 드래그합니다. 예를 들어 `Page Name (pageName)`을 `pagedata.title`로 드래그합니다.

   ![aa-14](assets/aa-14.png)

   >[!NOTE]
   >
   >프레임워크에 대해 선택된 보고서 세트 ID(RSID)는 컨텐츠 파인더에 표시되는 Adobe Analytics 변수를 결정합니다.

1. 다른 구성 요소 및 변수에 대해 이전 2단계를 반복합니다.

   >[!NOTE]
   >
   >여러 Analytics 변수(예:같은 CQ 변수(예:`props`)`eVars``events``pagedata.title`

   >[!CAUTION]
   >
   >다음과 같은 것이 좋습니다.
   >    
   >    * `eVars` 를  `props`   `pagedata.X` 사용하거나 또는  `eventdata.X`
      >    
      >    
   * 반면에 이벤트는 `eventdata.events.X`로 시작하는 변수에 매핑되어야 합니다.


1. 사이트의 게시 인스턴스에서 프레임워크를 사용할 수 있게 하려면 사이드 킥의 **페이지** 탭을 열고 **프레임워크 활성화를 클릭합니다.**

## 제품 관련 변수 매핑 {#mapping-product-related-variables}

AEM에서는 Adobe Analytics 제품 관련 속성에 매핑되어야 하는 제품 관련 변수 및 이벤트의 이름 지정 규칙을 사용합니다.

| CQ 변수 | 분석 변수 | 설명 |
|---|---|---|
| `product.category` | `product.category` (전환 변수) | 제품 카테고리. |
| `product.sku` | `product.sku` (전환 변수) | 제품 sku. |
| `product.quantity` | `product.quantity` (전환 변수) | 구매하는 제품 수. |
| `product.price` | `product.price` (전환 변수) | 제품 가격입니다. |
| `product.events.<eventName>` | 보고서의 제품과 연결할 성공 이벤트입니다. | `product.events` 는 eventName이라는 이벤트의  *접두사다.* |
| `product.evars.<eVarName>` | 제품과 연결할 전환 변수( `eVar`). | `product.evars` 는 eVarName이라는 eVar 변수의  *접두어입니다.* |

여러 AEM Commerce 구성 요소는 이러한 변수 이름을 사용합니다.

>[!NOTE]
>
>Adobe Analytics 제품 속성을 CQ 변수에 매핑하지 마십시오. 표에 설명된 대로 제품 관련 매핑을 구성하는 것은 제품 변수 매핑과 사실상 같습니다.

### Adobe Analytics {#checking-reports-on-adobe-analytics}에서 보고서 확인 중

1. AEM에 제공된 동일한 자격 증명을 사용하여 Adobe Analytics 웹 사이트에 로그인합니다.
1. 선택한 RSID가 이전 단계에서 사용된 RSID인지 확인합니다.
1. **보고서**(페이지의 왼쪽)에서 **사용자 지정 전환**&#x200B;을 선택하고 **사용자 지정 전환 1-10**&#x200B;을 선택한 다음 `eVar7`에 해당하는 변수를 선택합니다

1. 사용 중인 Adobe Analytics 버전에 따라 보고서가 사용된 검색어로 업데이트될 때까지 평균 45분이 기다려야 합니다.예: 예제의 가지

## Adobe Analytics 프레임워크 {#using-the-content-finder-cf-with-adobe-analytics-frameworks}에서 컨텐츠 파인더(cf#) 사용

처음에 Adobe Analytics 프레임워크을 열 때 컨텐츠 파인더에는 다음과 같이 사전 정의된 Analytics 변수가 포함되어 있습니다.

* 트래픽
* 전환
* 이벤트

RSID를 선택하면 해당 RSID에 속하는 모든 변수가 목록에 추가됩니다.\
다른 추적 구성 요소에 있는 CQ 변수에 Analytics 변수를 매핑하려면 `cf#`이(가) 필요합니다. 기본 추적을 위한 프레임워크 설정을 참조하십시오.

프레임워크에 대해 선택한 보기에 따라, 컨텐츠 파인더는 Analytics 변수(AEM 보기) 또는 CQ 변수(Analytics 보기)로 채워집니다.

목록은 다음과 같은 방법으로 조작할 수 있습니다.

1. **AEM 보기**&#x200B;에서는 3개의 필터 단추를 사용하여 선택한 변수 유형에 따라 목록을 필터링할 수 있습니다.

   * *버튼*&#x200B;을 선택하지 않으면 목록에 전체 목록이 표시됩니다.
   * **트래픽** 단추를 선택하면 목록에는 트래픽 섹션에 속하는 변수만 표시됩니다.
   * **전환** 단추를 선택하면 목록에 전환 섹션에 속하는 변수만 표시됩니다.
   * **이벤트** 단추를 선택하면 목록에는 이벤트 섹션에 속하는 변수만 표시됩니다.

   >[!NOTE]
   >
   >한 번에 하나의 필터 단추만 활성화할 수 있습니다.

   >[!NOTE]
   >
   >Search &amp; Promote 변수는 전환 섹션에도 속합니다.

   1. 검색 필드에는 검색 필드에 입력한 텍스트에 따라 요소를 필터링하는 검색 기능도 있습니다.
   1. 목록에서 요소를 검색하는 동안 필터 옵션이 활성화되면 표시되는 결과도 활성 단추에 따라 필터링됩니다.
   1. 소용돌이 모양의 화살표 단추를 사용하여 언제든지 목록을 다시 로드할 수 있습니다.
   1. 프레임워크에서 여러 RSID를 선택한 경우 선택한 RSID 내에 사용된 모든 레이블을 사용하여 목록의 모든 변수가 표시됩니다.


1. Adobe Analytics 보기에서 Content Finder는 CQ 보기에서 드래그한 추적 구성 요소에 속하는 모든 CQ 변수를 표시합니다.

   * 예: **다운로드 구성 요소**&#x200B;가 CQ 보기에서 *드래그한*&#x200B;만(2개의 매핑 가능한 변수 *events data.downloadLink* 및 *events.startDownload*)인 경우, 컨텐츠 파인더는 Adobe Analytics으로 전환할 때 다음과 같이 표시됩니다. 보기:

   ![aa-22](assets/aa-22.png)

   * 3개의 변수 섹션(**트래픽**, **전환** 및 **이벤트**) 중 하나에 속하는 모든 Adobe Analytics 변수에 변수를 드래그 앤 드롭할 수 있습니다.

   * 새 추적 구성 요소를 CQ 보기의 프레임워크로 드래그하면 구성 요소에 속한 CQ 변수가 Adobe Analytics 보기의 Content Finder(cf#)에 자동으로 추가됩니다.
   >[!NOTE]
   >
   >한 번에 하나의 CQ 변수만 Adobe Analytics 변수에 매핑할 수 있습니다.

## AEM 보기 및 분석 보기 사용 {#using-aem-view-and-analytics-view}

지정된 시간에 사용자는 프레임워크 페이지에서 Adobe Analytics 매핑을 볼 때 2가지 방법 간에 전환할 수 있습니다. 2개의 보기에서는 2개의 서로 다른 관점에서 프레임워크 내의 매핑에 대한 더 나은 개요를 제공합니다.

### AEM 보기 {#aem-view}

![aa-23](assets/aa-23.png)

위의 이미지를 예로 들어 보면 **AEM 보기**&#x200B;에 다음 속성이 있습니다.

1. 프레임워크가 열릴 때의 기본 보기입니다.
1. 왼쪽:컨텐츠 파인더(cf#)는 선택한 RSID를 기준으로 Adobe Analytics 변수로 채워집니다.
1. 탭 머리글(**AEM 보기** 및 **분석 보기**):두 뷰 간을 전환하려면 이 옵션을 사용합니다.

1. **AEM 보기**:

   1. 프레임워크에 상위에서 상속되는 구성 요소가 있는 경우 구성 요소에 매핑된 변수와 함께 여기에 표시됩니다.

      1. 상속된 구성 요소가 잠겨 있습니다.
      1. 상속된 구성 요소의 잠금을 해제하려면 구성 요소 이름 옆에 있는 자물쇠를 두 번 클릭하면 됩니다
      1. 상속을 되돌리려면 잠금 해제된 구성 요소를 삭제해야 합니다.그 후 잠긴 상태가 다시 되돌아갑니다.
   1. **분석 프레임워크에 포함하려면 구성 요소를 여기로 드래그하십시오**.구성 요소를 사이드 킥에서 드래그하여 여기에 놓을 수 있습니다.
   1. 분석 프레임워크에 현재 포함된 모든 구성 요소를 찾을 수 있습니다.

      1. 구성 요소를 추가하려면 사이드 킥의 구성 요소 탭에서 구성 요소를 드래그합니다
      1. 구성 요소 및 모든 해당 매핑을 삭제하려면 구성 요소의 컨텍스트 메뉴에서 삭제를 선택한 다음 확인 대화 상자에서 삭제를 적용합니다.
      1. 구성 요소는 만들어진 프레임워크에서만 삭제할 수 있으며 일반적인 의미에서 하위 프레임워크에서는 삭제할 수 없습니다(덮어쓸 수만 있음).


### 분석 보기 {#analytics-view}

![aa-24](assets/aa-24.png)

1. 이 보기는 프레임워크의 **분석 보기** 탭으로 전환하여 액세스할 수 있습니다.
1. 왼쪽:CQ 보기의 프레임워크로 드래그한 구성 요소를 기준으로 CQ 변수에 의해 채워진 컨텐츠 파인더(cf#).
1. 탭 머리글(**AEM 보기** 및 **분석 보기**):두 뷰 간을 전환하려면 이 옵션을 사용합니다.

1. 3개의 표(트래픽, 전환, 이벤트)에는 사용 가능한 모든 Adobe Analytics 변수가 나열됩니다. 선택한 RSID에 속합니다. 여기에 표시된 매핑은 AEM 보기에서와 같아야 합니다.

   * **트래픽**:

      * CQ 변수( `eventdata.downloadLink`)에 매핑되는 트래픽 변수( `prop1`)

      * 구성 요소 옆에 자물쇠가 있으면 이는 구성 요소가 상위 프레임워크에서 상속되므로 편집할 수 없음을 의미합니다
   * **전환**:

      * CQ 변수( `pagedata.title`)에 매핑된 전환 변수( `eVar1`)

      * CQ 변수 필드를 두 번 클릭하고 코드를 수동으로 입력하여 인라인으로 추가된 javascript 표현식에 매핑되는 전환 변수( `eVar3`)
   * **이벤트**:

      * CQ 이벤트( `eventdata.events.pageView`)에 매핑된 이벤트 변수( `event1`)



>[!NOTE]
>
>모든 테이블의 CQ 변수 열은 필드를 두 번 클릭하고 텍스트를 추가하여 인라인으로도 채울 수 있습니다. 이러한 필드는 javascript를 입력으로 허용합니다.
>
>* 예: `prop3` 옆의
>* `'`* `Adobe:'+pagedata.title+':'+pagedata.sitesection`\
   >  *:*(콜론)을 사용하여 *siteselection*&#x200B;과 연결된 페이지의 *제목*&#x200B;을 전송하고 *Adobe*&#x200B;을 `prop3`으로 접두어로 보내려면

>



>[!CAUTION]
>
>지정된 시간에 하나의 CQ 변수만 Adobe Analytics 변수에 매핑할 수 있습니다.

