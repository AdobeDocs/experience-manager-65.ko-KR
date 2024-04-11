---
title: AEM 6.5 Sites를 위한 헤드리스 개발
description: 콘텐츠 모델, 콘텐츠 조각, GraphQL API와 같은 AEM 6.5의 강력한 Headless 기능을 함께 사용하여 경험을 중앙에서 관리하고 여러 채널에서 제공할 수 있는 방법에 대해 알아봅니다.
exl-id: b6598bcf-b2ce-403a-87cf-6895fec8a91b
solution: Experience Manager, Experience Manager Sites
feature: Headless,Content Fragments,GraphQL,Persisted Queries,Developing
role: Admin,Architect,Data Architect,Developer
source-git-commit: 9a3008553b8091b66c72e0b6c317573b235eee24
workflow-type: tm+mt
source-wordcount: '507'
ht-degree: 35%

---

# AEM 6.5 Sites를 위한 헤드리스 개발 {#headless-development}

콘텐츠 모델, 콘텐츠 조각, GraphQL API와 같은 AEM 6.5의 강력한 Headless 기능을 함께 사용하여 경험을 중앙에서 관리하고 여러 채널에서 제공할 수 있는 방법에 대해 알아봅니다.

## 개요 {#overview}

Headless 구현은 채널에 관계없이 어디에 있든지 대상자에게 경험을 제공하는 데 점점 더 중요해지고 있습니다.

Headless 구현은 전체 스택 및 하이브리드 솔루션의 기존 방식과 마찬가지로 페이지 및 구성 요소 관리를 생략하고 채널 중립적이고 재사용 가능한 콘텐츠 조각 생성 및 크로스 채널 게재에 중점을 둡니다. 웹 경험을 구현하기 위한 현대적이고 동적인 개발 패턴입니다.

![AEM 구현 모델](/help/sites-developing/headless/getting-started/assets/aem-implementation-models.png)

## Headful과 Headless 비교 {#headful-headless}

이 문서는 AEM의 전체 Headless 구현 모델에 중점을 둡니다. 그러나 Headful과 Headless가 AEM에서 양자택일이 될 필요는 없습니다. Headless 기능을 사용하여 콘텐츠를 관리하고 다양한 끝점에 전달할 수 있을 뿐만 아니라 콘텐츠 작성자가 단일 페이지 애플리케이션을 편집할 수도 있습니다. 모두 AEM에 있습니다.

>[!TIP]
>
>자세한 내용은 [AEM의 Headful과 Headless](/help/sites-developing/headful-headless.md)설명서를 참조하십시오.

## AEM 6.5 및 Headless {#aem-headless}

AEM 6.5는 세 가지 강력한 서비스를 제공하여 headless 구현 모델을 위한 유연한 도구입니다.

1. 콘텐츠 모델
   * 콘텐츠 모델은 콘텐츠를 구조적으로 표시한 것입니다.
   * 정보 설계자는 AEM 콘텐츠 조각 모델 편집기에서 이를 정의합니다.
   * 콘텐츠 모델은 콘텐츠 조각의 기초 역할을 합니다.
1. 콘텐츠 조각
   * 콘텐츠 조각은 콘텐츠 모델의 인스턴스입니다.
   * 이러한 구성 요소는 AEM 콘텐츠 조각 편집기를 사용하여 콘텐츠 작성자가 만듭니다.
   * AEM Assets에 저장되고 Assets 관리 UI에서 관리됩니다.
1. 전달을 위한 콘텐츠 API
   * AEM GraphQL API는 콘텐츠 조각 게재를 지원합니다.
   * AEM Assets REST API는 콘텐츠 조각 CRUD 작업을 지원합니다.
   * 를 사용하여 직접 콘텐츠 전달도 가능합니다. [콘텐츠 조각 핵심 구성 요소의 JSON 내보내기.](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/content-fragment-component.html?lang=ko-KR)

## AEM Headless의 첫 번째 단계 {#first-steps}

AEM Headless 기능을 시작하는 데 사용할 수 있는 몇 가지 리소스가 있습니다. 다양한 사용 사례를 위한 것이지만, 모두 AEM Headless 기능에 대한 탄탄한 개요를 제공합니다.

| 리소스 | 설명 | 유형 | 대상자 | 예상 시간 |
|---|---|---|---|---|
| [Headless 개발자 여정](/help/journey-headless/developer/overview.md) | **AEM 및 Headless를 처음 사용하는 사용자의 경우** 기술은 headless 이론에서 첫 번째 headless 프로젝트 실행에 이르기까지 AEM 및 headless 기능을 여기에서 포괄적으로 소개합니다. | 안내서 | **AEM 및 Headless를 처음 경험하는** 개발자 | 1시간 |
| [Headless 시작 안내서](/help/sites-developing/headless/getting-started/introduction.md) | 주요 AEM Headless 기능에 대한 간략한 요약이 필요한 **경험 있는 AEM 사용자의 경우** 이 빠른 시작 개요를 확인하십시오. | 빠른 시작 | **AEM 사용 경험이 있는** 개발자, 관리자 | 20분 |
| [AEM Headless 시작하기 실습형 튜토리얼](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/multi-step/overview.html) | **실습 접근 방식을 선호하고 AEM에 익숙한 경우**, 이 튜토리얼에서는 간단한 Headless 프로젝트 만들기로 바로 뛰어듭니다. | 튜토리얼 | 개발자 | 2시간 |
| [AEM 개발자 포털](https://experienceleague.adobe.com/landing/experience-manager/headless/developer.html) | 이 리소스 컬렉션은 두 리소스 모두에 대해 제공됩니다. **신규** 및 **경력자** 개발자. | 리소스 컬렉션 | 개발자 | |
