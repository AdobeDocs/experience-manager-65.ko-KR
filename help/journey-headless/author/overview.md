---
title: AEM Headless 콘텐츠 작성자 여정
description: AEM의 강력하고 유연한 Headless 기능, 각 능력과 프로젝트의 콘텐츠를 작성하는 방법에 대한 가이드 여정을 받으십시오.
exl-id: b8cdbd0f-c034-4c9f-976f-5e39b1bd33bf
solution: Experience Manager, Experience Manager Sites
feature: Headless,Content Fragments
role: Admin, Developer, User, Leader
source-git-commit: 07289e891399a78568dcac957bc089cc08c7898c
workflow-type: tm+mt
source-wordcount: '847'
ht-degree: 81%

---

# AEM Headless 콘텐츠 작성자 여정 {#aem-headless-author-journey}

AEM의 강력하고 유연한 Headless 기능과 Headless 프로젝트의 콘텐츠를 작성하는 방법에 대한 가이드 여정을 받으십시오.

## 소개 {#introduction}

Headless 구현은 채널에 관계없이 어디서든 경험을 대상자에게 전달하는 데 점점 더 중요해지고 있습니다.

Headless 콘텐츠는 페이지 및 구성 요소의 기존 구조를 기반으로 하지 않습니다. 대신 채널 중립적이고 재사용 가능한 콘텐츠 조각 생성 및 크로스 채널 게재를 기반으로 합니다.

AEM에서 콘텐츠 조각을 통해 실현됩니다. 필요에 따라 선택하고 사용하는 애플리케이션에 사용 가능한 개별 콘텐츠 조각의 콘텐츠를 작성합니다.

이러한 유연성은 Headless가 디지털 경험을 구현하기 위한 현대적이고 동적인 개발 패턴이라는 것임을 의미합니다.

이 안내서는 가장 중요한 주제를 안내하므로 완료 시 다음과 같은 작업을 수행할 수 있습니다.

* Headless 콘텐츠 게재와 이점을 기본적으로 이해할 수 있습니다.
* AEM의 Headless 기능과 Headless 경험 게재를 위해 이 기능이 함께 작동하는 방식을 이해할 수 있습니다.
* AEM Headless 프로젝트의 콘텐츠를 작성할 수 있습니다.

## AEM 설명서 여정 {#documentation-journeys}

[설명서 여정](/help/journey-documentation/home.md)은 AEM을 처음 접할 수 있는 독자가 최소한의 사전 주제 또는 AEM 지식을 전제로 비즈니스 문제를 처음부터 끝까지 이해하고 해결하는 데 도움이 되는 묘사를 제공하여 다양하고 복잡한 주제와 기능을 결합합니다.

설명서 여정은 Adobe의 최신 연구, Adobe 컨설턴트의 입증된 구현 경험 및 고객 프로젝트의 피드백을 통해 제공되는 모범 사례 원칙을 중심으로 설계되었습니다.

Adobe가 AEM을 통해 AEM 관련 Headless 비즈니스 사례를 해결하는 방법에 대해 알아보려면 [AEM Headless 여정](/help/journey-headless/overview.md)에서 시작해 보십시오.

## 대상자 {#audience}

이 여정은 콘텐츠 작성자 페르소나를 위해 설계되었습니다. 콘텐츠 작성자는 콘텐츠 조각에서 실제 콘텐츠를 생성합니다.

이 여정은 AEM Headless 프로젝트에 대한 요구 사항, 단계 및 접근 방식을 제시합니다. 이 여정은 작성자가 프로젝트 성공을 위해 상호 작용해야 하는 추가 페르소나를 정의하지만, 여정은 콘텐츠 작성자의 관점에서 전개됩니다.

이 여정의 정보는 다른 담당자에게 유용할 수 있지만 일부 정보는 특정 역할에게 불필요할 수 있습니다. 추가 역할을 다루는 다가오는 여정은 추후에 업데이트될 예정입니다.

## Headless 콘텐츠 작성자 여정 {#the-journey}

이 여정에서 다양한 주제들을 살펴보게 됩니다. 다음 문서는 AEM에서의 Headless에 대한 기초 지식을 제공하며 상세 기술 설명서와 연결됩니다.

여정의 특정 부분으로 바로 이동할 수 있지만 많은 개념이 이전 문서의 개념을 기반으로 합니다. 따라서 AEM에서 Headless를 처음 수행하는 경우 처음부터 시작하여 순차적으로 진행하는 것이 좋습니다.

| # | 문서 | 설명 |
|---|---|---|
| 0 | AEM Headless 콘텐츠 작성자 여정 | 이 문서 |
| 1 | [AEM Headless 작성 - 소개](introduction.md) | Adobe Experience Manager의 Headless 기능에 대한 소개 및 프로젝트 콘텐츠를 작성하는 방법. |
| 2 | [AEM을 통한 Headless 작성 기본 사항 - 소개](basics.md) | 콘텐츠 조각을 사용하여 Headless CMS용 콘텐츠를 작성하는 개념 및 메커니즘에 대해 알아봅니다. |
| 3 | [콘텐츠 조각의 참조 사용에 대해 알아보기](references.md) | 콘텐츠 조각의 참조를 사용하는 방법에 대해 알아봅니다. 또한 중첩된 조각을 사용하여 Headless CMS에 대한 여러 수준의 구조를 만들고 관리할 수 있습니다. |
| 4 | [콘텐츠 조각에 대한 메타데이터 및 태그 지정에 대해 알아보기](metadata-tagging.md) | 콘텐츠 조각에 대한 메타데이터 및 태그 지정에 대해 알아보기. |

## 다음 단계 {#what-is-next}

이제 Adobe Headless 여정을 시작할 준비가 되었습니다. 여정의 다음 부분으로 계속 진행하여 [AEM Headless용 작성 - 소개 문서를 읽어보시기 바랍니다.](introduction.md)

<!--
### Choose Your Own Adventure {#choose-your-path}

However, Adobe wants you to succeed as you get started with your AEM Headless project, regardless of your learning style. So consider these two options.

* If you prefer to continue to **learn about headless concepts and AEM's headless technologies**, you should continue your AEM headless journey as recommended by next reviewing the document [How to Model Your Content as AEM Content Models](model-your-content.md) where you learn how to model your content structure in AEM.
* If you prefer to **learn by doing**, you can jump to the [Getting Started with AEM Headless hands-on tutorial](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/multi-step/overview.html?lang=ko) where you will jump directly into AEM Headless development by implementing a simple project to expose AEM headless content.
-->

## 추가 리소스 {#additional-resources}

설명서 여정에서는 복잡하고 상호 연관된 프로세스 및 기능을 안내하는 내러티브를 제공하여 AEM을 통해 비즈니스 문제를 해결하는 방법을 보여 줍니다. 여정은 한 가지 비즈니스 요구 사항을 충족시키기 위해 여러 기능이 함께 작동하는 방식을 보여 줍니다.

따라서 여정은 스스로 자립하도록 설계되었습니다. 그러나 몇 가지 유형이 서로 관련될 수 있습니다. AEM의 강력한 기능들이 함께 작동하는 방법에 대한 자세한 내용은 이들 추가 여정을 확인하십시오.

* [AEM Headless 번역 여정](/help/journey-headless/translation/overview.md) - 이 설명서 여정을 통해 Headless 기술, AEM에서 Headless 콘텐츠를 제공하는 방법과 콘텐츠를 번역하는 방법을 폭넓게 이해할 수 있습니다.
* [AEM Headless 개발자 여정](/help/journey-headless/developer/overview.md) - 여기에서 AEM의 강력하고 유연한 Headless 기능과 각각의 능력, 그리고 귀하의 첫 개발 프로젝트에서 이들 기능을 사용하는 방법에 대한 가이드 여정을 시작해 보십시오.
* [Headless 설계 여정](/help/journey-headless/architect/overview.md) - 여기에서 Adobe Experience Manager의 강력하고 유연한 Headless 기능을 접해 보고 프로젝트 콘텐츠를 모델링하는 방법을 알아보십시오.
* [AEM 기술 설명서](https://experienceleague.adobe.com/docs/experience-manager-65.html?lang=ko) - AEM 및 Headless 기술에 대해 확실히 이해하고 있다면 바로 심화 기술 문서를 참조할 수 있습니다.
   * [AEM as a Headless CMS 소개](/help/sites-developing/headless/introduction.md)
* [AEM Headless 튜토리얼](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/overview.html?lang=ko) - 직접 수행하며 배우는 것을 선호하고 기술 관련 소양을 갖추고 있다면 API 및 프레임워크로 구성된 실습형 튜토리얼을 사용하여 AEM Headless에 구축된 애플리케이션을 만들고 사용해 보십시오.
* [AEM 개발자 포털](https://experienceleague.adobe.com/landing/experience-manager/headless/developer.html?lang=ko)
