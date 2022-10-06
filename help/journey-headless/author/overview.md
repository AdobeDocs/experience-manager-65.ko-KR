---
title: AEM Headless Content Author 여정
description: AEM의 강력하고 유연한 헤드리스 기능 및 프로젝트용 컨텐츠를 작성하는 방법을 통해 안내식 여정을 살펴보려면 여기에서 시작하십시오.
exl-id: b8cdbd0f-c034-4c9f-976f-5e39b1bd33bf
source-git-commit: ed11891c27910154df1bfec6225aecd8a9245bff
workflow-type: tm+mt
source-wordcount: '849'
ht-degree: 29%

---

# AEM Headless Content Author 여정 {#aem-headless-author-journey}

AEM의 강력하고 유연한 헤드리스 기능과 헤드리스 프로젝트를 위한 컨텐츠를 작성하는 방법을 통해 안내식 여정을 살펴보려면 여기에서 시작하십시오.

## 소개 {#introduction}

헤드리스 구현은 어디에 있든 채널에 관계없이 고객에게 경험을 전달하는 데 점점 더 중요해지고 있습니다.

헤드리스 콘텐츠는 페이지 및 구성 요소의 기존 구조를 기반으로 하지 않습니다. 대신 채널 중립적이고 재사용 가능한 컨텐츠 조각 및 채널 간 게재 만들기를 기반으로 합니다.

AEM에서 컨텐츠 조각으로 구현됩니다. 개별 컨텐츠 조각에서 컨텐츠를 작성합니다. 이 조각은 애플리케이션에서 필요에 따라 선택하고 사용할 수 있습니다.

이러한 유연성은 헤드리스가 디지털 경험을 구현하기 위한 현대적이고 동적 개발 패턴임을 의미합니다.

이 안내서는 가장 중요한 주제를 안내합니다. 따라서 완료 시 다음과 같은 작업을 수행할 수 있습니다.

* 헤드리스 콘텐츠 전달의 정의와 그 이점에 대한 기본 이해를 얻으십시오.
* AEM 헤드리스 기능과 이 기능이 함께 작동하는 방식을 이해하여 헤드리스 경험을 제공합니다.
* AEM 헤드리스 프로젝트용 컨텐츠를 작성할 수 있습니다.

## AEM 설명서 여정 {#documentation-journeys}

[설명서 여정](/help/journey-documentation/home.md)은 AEM을 처음 접할 수 있는 독자가 최소한의 사전 주제 또는 AEM 지식을 전제로 비즈니스 문제를 처음부터 끝까지 이해하고 해결하는 데 도움이 되는 묘사를 제공하여 다양하고 복잡한 주제와 기능을 결합합니다.

설명서 여정은 Adobe의 최신 연구, Adobe 컨설턴트의 입증된 구현 경험 및 고객 프로젝트의 피드백을 통해 제공되는 모범 사례 원칙을 중심으로 설계되었습니다.

AEM에서 헤드리스 비즈니스 사례를 해결하는 방법을 Adobe이 권장하는 방법을 알아보려면, [AEM 헤드리스 여정](/help/journey-headless/home.md) 은 시작할 위치입니다.

## 대상자 {#audience}

이 여정은 컨텐츠 작성자 성향용으로 설계되었습니다. 컨텐츠 작성자는 컨텐츠 조각에서 실제 컨텐츠를 작성합니다.

이 여정은 AEM Headless 프로젝트용 컨텐츠를 작성하는 요구 사항, 단계 및 접근 방식을 설명합니다. 여정은 성공적인 프로젝트를 위해 작성자가 상호 작용해야 하는 추가 가상 사용자를 정의하지만 여정의 POI는 컨텐츠 작성자의 것입니다.

이 여정의 정보는 물론 다른 사용자에게 유용할 수 있지만, 일부 정보는 특정 역할에 유용할 것입니다. 추가 역할을 다루는 다가오는 여정은 추후에 업데이트될 예정입니다.

## 헤드리스 컨텐츠 작성자 여정 {#the-journey}

이 여정에서 다양한 주제들을 살펴보게 됩니다. 다음 문서는 AEM의 헤드리스에 대한 기본 지식을 제공하고 자세한 기술 설명서에 연결합니다.

여정의 특정 부분으로 바로 이동할 수 있지만, 많은 개념이 이전 문서의 개념을 기반으로 합니다. 따라서 AEM에서 헤드리스를 처음 사용하는 경우 시작 및 진행 순서로 시작하는 것이 좋습니다.

| # | 문서 | 설명 |
|---|---|---|
| 0 | AEM Headless Content Author 여정 | 이 문서 |
| 1 | [AEM Headless용 작성 - 소개](introduction.md) | Adobe Experience Manager의 헤드리스 기능 및 프로젝트용 컨텐츠를 작성하는 방법에 대한 소개입니다. |
| 2 | [AEM을 통한 Headless 작성 기본 사항 - 소개](basics.md) | 컨텐츠 조각을 사용하여 헤드리스 CMS용 컨텐츠를 작성하는 개념과 역학에 대해 알아봅니다. |
| 3 | [콘텐츠 조각의 참조 사용에 대해 알아보기](references.md) | 컨텐츠 조각에서 참조를 사용하는 방법에 대해 알아봅니다. 또한 중첩 조각을 사용하여 헤드리스 CMS에 대한 여러 수준의 구조를 만들고 관리할 수 있습니다. |
| 4 | [콘텐츠 조각에 대한 메타데이터 및 태그 지정에 대해 알아보기](metadata-tagging.md) | 콘텐츠 조각에 대한 메타데이터 및 태그 지정에 대해 알아보기. |

## 다음 단계 {#what-is-next}

이제 Adobe 헤드리스 여정을 시작할 준비가 되었습니다. 여정의 다음 부분으로 계속 이동하여 문서를 읽어 보십시오 [AEM Headless용 작성 - 소개.](introduction.md)

<!--
### Choose Your Own Adventure {#choose-your-path}

However, Adobe wants you to succeed as you get started with your AEM Headless project, regardless of your learning style. So please consider these two options.

* If you prefer to continue to **learn about headless concepts and AEM's headless technologies**, you should continue your AEM headless journey as recommended by next reviewing the document [How to Model Your Content as AEM Content Models](model-your-content.md) where you learn how to model your content structure in AEM.
* If you prefer to **learn by doing**, you can jump to the [Getting Started with AEM Headless hands-on tutorial](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/multi-step/overview.html) where you will jump directly into AEM Headless development by implementing a simple project to expose AEM headless content.
-->

## 추가 리소스 {#additional-resources}

설명서 여정은 복잡하고 관련된 프로세스와 기능을 안내하는 설명을 제공하여 AEM에서 비즈니스 문제를 해결하는 방법을 보여줍니다. 여정은 단일 비즈니스 요구 사항을 충족하기 위해 여러 기능이 함께 작동하는 방식을 보여줍니다.

이러한 여정은 스스로 설 수 있도록 고안되었습니다. 하지만 그들 중 많은 수가 서로 관련될 수 있습니다. AEM의 강력한 기능이 함께 작동하는 방식에 대한 자세한 내용은 이러한 추가 여정을 참조하십시오.

* [AEM 헤드리스 번역 여정](/help/journey-headless/translation/overview.md) - 이 설명서 여정은 헤드리스 기술, AEM에서 헤드리스 콘텐츠를 제공하는 방법 및 이를 번역할 수 있는 방법에 대한 광범위한 이해를 제공합니다.
* [AEM 헤드리스 개발자 여정](/help/journey-headless/developer/overview.md) - 여기에서 AEM의 강력하고 유연한 Headless 기능과 각각의 능력, 그리고 귀하의 첫 개발 프로젝트에서 이들 기능을 활용하는 방법에 대한 가이드 여정을 시작해 보십시오.
* [헤드리스 아키텍트 여정](/help/journey-headless/architect/overview.md) - Adobe Experience Manager의 강력하고 유연한 헤드리스 기능과 프로젝트 컨텐츠를 모델링하는 방법을 소개합니다.
* [AEM 기술 설명서](https://experienceleague.adobe.com/docs/experience-manager-65.html?lang=ko-KR) - AEM 및 헤드리스 기술에 대해 확실히 이해하고 있다면 바로 심화 기술 문서를 참조할 수 있습니다.
* [AEM 헤드리스 튜토리얼](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/overview.html) - 직접 해보면서 배우는 것을 선호하고 기술 관련 소양을 갖추고 있다면 API 및 프레임워크로 구성된 실습형 튜토리얼을 사용하여 AEM 헤드리스에 구축된 애플리케이션을 만들고 사용해 보십시오.
