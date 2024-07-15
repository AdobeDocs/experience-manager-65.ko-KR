---
title: 컨텐츠 인사이트
description: Content Insight는 웹 분석 및 SEO 권장 사항을 사용하여 페이지 성능에 대한 정보를 제공합니다
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
exl-id: 187f3cde-a0db-4c02-9e8b-08272987a67d
solution: Experience Manager, Experience Manager Sites
feature: Authoring
role: User,Admin,Architect,Developer
source-git-commit: 9a3008553b8091b66c72e0b6c317573b235eee24
workflow-type: tm+mt
source-wordcount: '537'
ht-degree: 3%

---

# 컨텐츠 인사이트{#content-insight}

Content Insight는 웹 분석 및 SEO 권장 사항을 사용하여 페이지 성능에 대한 정보를 제공합니다. 컨텐츠 인사이트를 사용하여 페이지 수정 방법을 결정하거나 이전 변경 사항으로 성능이 어떻게 변경되었는지 알아볼 수 있습니다. 작성하는 모든 페이지에 대해 컨텐츠 인사이트를 열어 페이지를 분석할 수 있습니다.

![chlimage_1-311](assets/chlimage_1-311.png)

Content Insight 페이지의 레이아웃은 사용 중인 디바이스의 화면 차원과 방향에 맞게 변경됩니다.

## 보고서 데이터

Content Insight 페이지에는 Adobe SiteCatalyst, Adobe Target, Adobe Social 및 BrightEdge 데이터를 사용하는 보고서가 포함됩니다.

* SiteCatalyst: 다음 지표에 대한 보고서를 사용할 수 있습니다.

   * 페이지 보기 수
   * 페이지에서 보낸 평균 시간
   * 소스

* 타겟: 페이지에 오퍼가 포함된 캠페인 활동에 대한 보고서입니다.
* BrightEdge: 검색 엔진에 대한 페이지의 가시성을 개선하는 페이지 기능에 대해 보고하며 구현해야 하는 기능을 권장합니다.

[Analytics 및 Recommendations 열기](/help/sites-authoring/ci-analyze.md#opening-analytics-and-recommendations-for-a-page)를 참조하십시오.

## 보고 기간

보고서는 사용자가 제어하는 기간 동안의 데이터를 보여 줍니다. 보고 기간을 조정하면 보고서가 해당 기간의 데이터로 자동으로 새로 고쳐집니다. 시각적 큐는 페이지 버전이 변경되는 시간을 나타내므로 각 버전의 성능을 비교할 수 있습니다.

>[!NOTE]
>
>Content Insight 대시보드의 타임라인이 `GMT`에 있습니다.

보고된 데이터의 세부 기간(예: 일별, 주별, 월별 또는 연간 데이터)을 지정할 수도 있습니다.

[보고 기간 변경](/help/sites-authoring/ci-analyze.md#changing-the-reporting-period)을 참조하세요.

>[!NOTE]
>
>컨텐츠 인사이트 보고서를 사용하려면 관리자가 AEM을 SiteCatalyst, Target 및 BrightEdge와 통합해야 합니다. [SightCatalyst와 통합](/help/sites-administering/adobeanalytics.md), [Adobe Target과 통합](/help/sites-administering/target.md) 및 [BrightEdge와 통합](/help/sites-administering/brightedge.md)을 참조하십시오.

## 보기 보고서 {#the-views-report}

보기 보고서에는 페이지 트래픽을 평가하기 위한 다음 기능이 포함됩니다.

* 보고 기간 동안 페이지에 대한 총 보기 수입니다.
* 보고 기간 동안의 보기 수 그래프:

   * 총 보기 수.
   * 고유 방문자 수

![chlimage_1-312](assets/chlimage_1-312.png)

## 페이지 평균 참여 보고서 {#the-page-average-engaged-report}

페이지 평균 참여 보고서에는 페이지 효과를 평가하기 위한 다음 기능이 포함됩니다.

* 전체 보고 기간 동안 페이지가 열려 있는 평균 시간입니다.
* 보고 기간 동안 페이지 보기의 평균 길이에 대한 그래프입니다.

![chlimage_1-313](assets/chlimage_1-313.png)

## 소스 보고서 {#the-sources-report}

소스 보고서는 사용자가 검색 엔진 결과나 알려진 URL을 사용하여 페이지로 이동한 방식을 나타냅니다.

![chlimage_1-314](assets/chlimage_1-314.png)

## 바운스 보고서 {#the-bounces-report}

바운스 수 보고서에는 선택한 보고 기간 동안 페이지에 대해 발생한 바운스 수를 보여 주는 그래프가 포함되어 있습니다.

![chlimage_1-315](assets/chlimage_1-315.png)

## 캠페인 활동 보고서 {#the-campaign-activity-report}

페이지가 활성화된 각 캠페인에 대해 이름이 *캠페인 이름* 활동인 보고서가 나타납니다. 이 보고서는 오퍼가 제공되는 각 세그먼트에 대한 페이지 노출 횟수 및 전환 횟수를 보여줍니다.

![chlimage_1-316](assets/chlimage_1-316.png)

## SEO Recommendations 보고서 {#the-seo-recommendations-report}

SEO Recommendations 보고서에는 해당 페이지에 대한 BrightEdge 분석 결과가 포함되어 있습니다. 이 보고서는 검색 엔진을 사용하여 찾기 능력을 극대화하기 위해 페이지가 어떤 기능을 수행하는지, 어떤 기능을 포함하지 않는지 나타내는 페이지 기능 체크리스트입니다.

보고서를 사용하면 작업을 만들어 페이지 검색 기능을 향상시킬 수 있습니다. Recommendations은 권장 사항 구현을 위한 작업이 생성되었음을 나타냅니다. [SEO Recommendations에 대한 작업 할당](/help/sites-authoring/ci-analyze.md#assigning-tasks-for-seo-recommendations)을 참조하세요.

![chlimage_1-317](assets/chlimage_1-317.png)
