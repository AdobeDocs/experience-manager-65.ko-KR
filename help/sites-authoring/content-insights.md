---
title: 컨텐츠 인사이트
seo-title: 컨텐츠 인사이트
description: 컨텐츠 인사이트는 웹 분석 및 SEO 추천을 사용하여 페이지 성능에 대한 정보를 제공합니다.
seo-description: 컨텐츠 인사이트 웹 분석 및 SEO 추천을 사용하여 페이지 성능에 대한 정보를 제공합니다.
uuid: 32f5b37c-2a82-462a-9f0a-c19bed46e198
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
discoiquuid: 60f980fd-049e-43c1-8b5d-60a8279b357a
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '536'
ht-degree: 95%

---


# 컨텐츠 인사이트{#content-insight}

컨텐츠 인사이트는 웹 분석 및 SEO 추천을 사용하여 페이지 성능에 대한 정보를 제공합니다. 컨텐츠 인사이트를 사용하여 페이지를 수정하는 방법을 결정하거나 이전 변경 사항이 성능 변화에 어떻게 영향을 주었는지 알아보십시오. 사용자가 작성하는 모든 페이지의 경우, 컨텐츠 인사이트를 열어 페이지를 분석할 수 있습니다.

![chlimage_1-311](assets/chlimage_1-311.png)

컨텐츠 인사이트 페이지의 레이아웃은 사용 중인 장치의 화면 크기 및 방향에 맞게 변경됩니다.

## 보고서 데이터

컨텐츠 인사이트 페이지에는 Adobe SiteCatalyst, Adobe Target, Adobe Social 및 BrightEdge 데이터를 사용하는 보고서가 포함되어 있습니다.

* SiteCatalyst: 다음 지표에 대한 보고서를 사용할 수 있습니다.

   * 페이지 조회수
   * 페이지에서 보낸 평균 시간
   * 소스

* Target: 페이지에 오퍼가 포함된 캠페인 활동에 대해 보고합니다.
* BrightEdge: 검색 엔진에 대한 페이지 가시성을 개선하는 페이지 기능과 구현해야 하는 추천 기능에 대해 보고합니다.

[페이지에 대한 분석 및 권장 사항 열기](/help/sites-authoring/ci-analyze.md#opening-analytics-and-recommendations-for-a-page)를 참조하십시오.

## 보고 기간

보고서에는 사용자가 지정하는 기간 동안의 데이터가 표시됩니다. 보고 기간을 조정하면 보고서가 자동으로 해당 기간의 데이터로 새로 고쳐집니다. 시각적 단서는 각 버전의 성능을 비교할 수 있도록 페이지 버전이 변경된 시간을 나타냅니다.

또한 보고된 데이터의 세부기간(예: 일별, 매주, 매월 또는 연간 데이터)을 지정할 수 있습니다.

[보고 기간 변경](/help/sites-authoring/ci-analyze.md#changing-the-reporting-period)을 참조하십시오.

>[!NOTE]
>
>컨텐츠 인사이트 보고서를 사용하려면 관리자가 AEM을 SiteCatalyst, Target 및 BrightEdge와 통합해야 합니다. [SightCatalyst](/help/sites-administering/adobeanalytics.md)와 통합, [Adobe Target](/help/sites-administering/target.md)과 통합 및 [BrightEdge](/help/sites-administering/brightedge.md)와 통합을 참조하십시오.

## 보기 보고서 {#the-views-report}

보기 보고서에는 다음과 같은 페이지 트래픽 평가 기능이 포함되어 있습니다.

* 보고 기간 동안 한 페이지의 총 보기 횟수
* 보고 기간의 보기 횟수 그래프:

   * 총 보기 횟수
   * 고유 방문자 수

![chlimage_1-312](assets/chlimage_1-312.png)

## 페이지 평균 참여 보고서 {#the-page-average-engaged-report}

페이지 평균 참여 보고서에는 다음과 같은 페이지 효과 평가 기능이 포함되어 있습니다.

* 전체 보고 기간 동안 페이지가 열린 상태로 남아 있는 평균 시간
* 보고 기간의 페이지 보기에 대한 평균 길이 그래프

![chlimage_1-313](assets/chlimage_1-313.png)

## 소스 보고서 {#the-sources-report}

소스 보고서는 사용자가 페이지로 어떻게 이동했는지(예: 검색 엔진 결과나 알려진 URL 사용)를 나타냅니다.

![chlimage_1-314](assets/chlimage_1-314.png)

## 바운스 수 보고서 {#the-bounces-report}

바운스 수 보고서에는 선택한 보고 기간 동안 어떤 페이지에 대해 발생한 바운스 수를 보여주는 그래프가 포함되어 있습니다.

![chlimage_1-315](assets/chlimage_1-315.png)

## 캠페인 활동 보고서 {#the-campaign-activity-report}

페이지가 활성화된 각 캠페인의 경우 보고서는 *캠페인 이름* 활동으로 표시되며, 보고서에는 오퍼가 제공되는 각 세그먼트에 대한 페이지 노출 횟수 및 전환 횟수가 표시됩니다.

![chlimage_1-316](assets/chlimage_1-316.png)

## SEO 추천 보고서 {#the-seo-recommendations-report}

SEO 추천 보고서에는 페이지에 대한 BrightEdge 분석 결과가 포함되어 있습니다. 이 보고서는 검색 엔진을 사용하여 검색성을 최대화하기 위해 페이지가 포함하는 기능과 포함하지 않는 기능을 나타내는 페이지 기능 확인 목록입니다.

이 보고서를 사용하면 페이지 검색성을 개선하기 위한 개선이 수행되도록 작업을 생성할 수 있습니다. 추천은 추천을 구현하기 위해 작업이 생성되었음을 나타냅니다. [SEO 추천용 작업 지정](/help/sites-authoring/ci-analyze.md#assigning-tasks-for-seo-recommendations)을 참조하십시오.

![chlimage_1-317](assets/chlimage_1-317.png)

