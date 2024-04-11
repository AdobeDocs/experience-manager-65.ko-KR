---
title: AEM Headless 개발자 여정
description: AEM Headless CMS 설명서. AEM의 강력하고 유연한 Headless 기능과 각각의 능력, 그리고 귀하의 첫 개발 프로젝트에서 이들 기능을 사용하는 방법에 대한 가이드 여정을 받으십시오.
exl-id: f24fb308-daa7-426f-ba45-37a236b5a500
solution: Experience Manager, Experience Manager Sites
feature: Headless,Content Fragments,GraphQL,Persisted Queries,Developing
role: Admin, Developer
source-git-commit: 9a3008553b8091b66c72e0b6c317573b235eee24
workflow-type: tm+mt
source-wordcount: '1204'
ht-degree: 74%

---

# AEM Headless 개발자 여정 {#aem-headless-developer-journey}

AEM의 강력하고 유연한 Headless 기능과 각각의 능력, 그리고 귀하의 첫 Headless 개발 프로젝트에서 이들 기능을 사용하는 방법에 대한 가이드 여정을 받으십시오. 이 여정은 첫 번째 Headless 애플리케이션을 개발하는 데 필요한 모든 AEM Headless 설명서를 제공합니다.

## 소개 {#introduction}

Headless 구현은 전체 스택 솔루션의 기존 방식과 마찬가지로 페이지 및 구성 요소 관리를 생략하고 채널 중립적이고 재사용 가능한 콘텐츠 조각 생성 및 크로스 채널 게재에 중점을 둡니다. 디지털 경험을 구현하기 위한 현대적이고 동적인 개발 패턴입니다.

이 안내서는 AEM에서 가장 headless 구현 주제를 안내하므로 완료 시 다음과 같은 작업을 수행할 수 있습니다.

* Headless 콘텐츠 게재와 이점을 완전하게 이해할 수 있습니다.
* AEM의 Headless 기능과 Headless 경험 게재를 위해 이 기능이 함께 작동하는 방식을 이해할 수 있습니다.
* 첫 번째 AEM Headless 프로젝트를 구현하는 첫 단계를 수행할 수 있습니다.

## AEM 설명서 여정 {#documentation-journeys}

[설명서 여정](/help/journey-documentation/home.md)은 AEM을 처음 접할 수 있는 독자가 최소한의 사전 주제 또는 AEM 지식을 전제로 비즈니스 문제를 처음부터 끝까지 이해하고 해결하는 데 도움이 되는 묘사를 제공하여 다양하고 복잡한 주제와 기능을 결합합니다.

설명서 여정은 Adobe의 최신 연구, Adobe 컨설턴트의 입증된 구현 경험 및 고객 프로젝트의 피드백을 통해 제공되는 모범 사례 원칙을 중심으로 설계되었습니다.

Adobe가 AEM을 통해 AEM 관련 Headless 비즈니스 사례를 해결하는 방법에 대해 알아보려면 [AEM Headless 여정](/help/journey-headless/overview.md)에서 시작해 보십시오.

>[!TIP]
>
>원하시면 **다음을 수행하여 학습** 및 은 기술적으로 설명되어 있으며 API 및 프레임워크로 구성되어 다음에서 사용할 수 있는 AEM Headless 튜토리얼을 참조하십시오. [추가 리소스 섹션](#additional-resources) 이 문서의 끝에 있습니다.

## 대상자 {#audience}

이 여정은 개발자를 위해 설계되어 개발자의 관점에서 AEM Headless 프로젝트에 대한 요구 사항, 단계 및 접근 방식을 제시합니다. 이 여정은 개발자가 프로젝트 성공을 위해 상호 작용해야 하는 추가 담당자를 정의하지만, 이 여정은 개발자의 관점에서 전개됩니다.

다음은 이 여정에서 상호 작용하는 담당자입니다.

| 담당자 | 설명 | 이 여정에서의 역할 |
|---|---|---|
| 개발자(타깃 대상자) | 다양한 소스의 콘텐츠를 사용하는 Headless 애플리케이션을 개발한 경험 | 이 여정의 타깃 대상자 |
| 콘텐츠 작성자 | Headless 방식으로 사이트에 게재되는 콘텐츠 생성 및 관리 | 콘텐츠 작성자는 개발자가 Headless 방식으로 게재하는 콘텐츠를 만듭니다. |
| 관리자 | AEM의 기본 설정 및 구성 관리 | 개발자는 관리자와 협력하여 개발에 필요한 구성을 변경할 수 있습니다. |
| 콘텐츠 설계자 | Headless 방식으로 사이트에 게재할 데이터에 대한 요구 사항 분석 및 해당 데이터의 구조 정의 | 개발자는 콘텐츠 설계자와 협력하여 데이터 구조와 데이터를 Headless 방식으로 게재하기 위한 요구 사항을 이해할 수 있습니다. |

이 여정에서 제공하는 정보는 모든 담당자에게 유용하지만 일부 정보는 특정 역할에 불필요할 수 있습니다. [추가 역할을 다루는 다가오는 여정](/help/journey-documentation/home.md#journeys)은 추후에 업데이트될 예정입니다.

## Headless 개발자 여정 {#the-journey}

이 여정에서 다양한 주제들을 살펴보게 됩니다. 다음 문서는 AEM에서의 Headless에 대한 기초 지식을 제공하며 상세 기술 설명서와 연결됩니다.

여정의 특정 부분으로 바로 이동할 수 있지만 많은 개념이 이전 문서의 개념을 기반으로 합니다. 따라서 AEM에서 Headless를 처음 수행하는 경우 처음부터 시작하여 순차적으로 진행하는 것이 좋습니다.

| # | 문서 | 설명 |
|---|---|---|
| 0 | AEM Headless 개발자 여정 | 이 문서 |
| 1 | [CMS Headless 개발에 대해 알아보기](learn-about.md) | Headless 기술과 사용 시기에 대해 알아봅니다. |
| 2 | [AEM Headless 시작하기](getting-started.md) | AEM Headless 사전 요구 사항에 대해 알아보기 |
| 3 | [AEM Headless를 사용한 첫 번째 경험으로의 경로](path-to-first-experience.md) | 개발 환경을 설정하고 간단한 앱을 AEM Headless와 통합하는 방법에 대해 알아보기 |
| 4 | [콘텐츠를 모델링하는 방법](model-your-content.md) | 콘텐츠 구조를 모델링하는 방법을 알아봅니다. 그런 다음 여러 채널에서 재사용할 수 있도록 콘텐츠 조각 모델 및 콘텐츠 조각을 사용하여 Adobe Experience Manager(AEM) 구조를 실현합니다. |
| 5 | [AEM 게재 API를 통해 콘텐츠에 액세스하는 방법](access-your-content.md) | GraphQL 쿼리를 사용하여 콘텐츠 조각의 콘텐츠에 액세스하는 방법에 대해 알아봅니다. |
| 6 | [AEM Assets API를 통해 콘텐츠를 업데이트하는 방법](update-your-content.md) | REST API를 사용하여 콘텐츠 조각의 콘텐츠에 액세스하고 업데이트하는 방법에 대해 알아봅니다. |
| 7 | [결합 방법 - AEM Headless의 앱과 콘텐츠](put-it-all-together.md) | AEM 프로젝트를 가져와 AEM Headless SDK 실행을 준비하는 방법에 대해 알아봅니다. |
| 8 | [Headless 애플리케이션 실행 방법](go-live.md) | 애플리케이션을 라이브로 배포하고 Git에서 로컬 코드를 가져와 CI/CD 파이프라인용 Cloud Manager Git으로 이동하는 방법에 대해 알아봅니다. |
| 9 | [옵션 - AEM을 통해 단일 페이지 애플리케이션(SPA)을 제작하는 방법](create-spa.md) | AEM Headless 기능을 이해했으면 Headful과 Headless 전달을 결합하는 방법을 살펴보고 AEM SPA Editor 프레임워크를 사용하여 편집 가능한 SPA을 만드는 방법을 알아봅니다. |

## 다음 단계 {#what-is-next}

이제 Adobe Headless 여정을 시작할 준비가 되었습니다. 여정의 다음 부분으로 계속 진행하여 이 문서를 읽어보시기 바랍니다. [CMS Headless 개발에 대해 알아봅니다.](learn-about.md)

### 나만의 어드벤처 선택 {#choose-your-path}

하지만 Adobe은 학습 스타일에 관계없이 AEM Headless 프로젝트를 시작할 때 성공하기를 원합니다. 따라서 이 두 가지 옵션을 고려하십시오.

* **Headless 개념 및 AEM의 Headless 기술**&#x200B;에 대해 계속 알아보려면 다음 문서인 [콘텐츠를 AEM 콘텐츠 모델로 모델링하는 방법](model-your-content.md)을 검토하여 권장하는 AEM Headless 여정을 계속하는 것이 좋습니다(AEM의 콘텐츠 구조를 모델링하는 방법에 대해 알아보는 경우).
* **직접 해보면서 배우는 것**&#x200B;을 선호하면 [AEM Headless 실습 튜토리얼 시작하기](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/multi-step/overview.html)로 이동할 수 있습니다(AEM Headless 콘텐츠를 노출하는 간단한 프로젝트를 구현하여 AEM Headless 개발로 직접 이동하는 경우).

## 추가 리소스 {#additional-resources}

설명서 여정에서는 복잡하고 상호 연관된 프로세스 및 기능을 안내하는 내러티브를 제공하여 AEM을 통해 비즈니스 문제를 해결하는 방법을 보여 줍니다. 여정은 한 가지 비즈니스 요구 사항을 충족시키기 위해 여러 기능이 함께 작동하는 방식을 보여 줍니다.

따라서 여정은 스스로 자립하도록 설계되었습니다. 그러나 몇 가지 유형이 서로 관련될 수 있습니다. AEM의 강력한 기능들이 함께 작동하는 방법에 대한 자세한 내용은 이들 추가 여정을 확인하십시오.

* [AEM Headless 튜토리얼](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/overview.html) - 직접 해보면서 배우는 것을 선호하고 기술 관련 소양을 갖추고 있다면 API 및 프레임워크로 구성된 실습형 튜토리얼을 사용하여 AEM Headless에 구축된 애플리케이션을 만들고 사용해 보십시오.
* [AEM Headless 번역 여정](/help/journey-headless/translation/overview.md) - 이 설명서 여정을 통해 Headless 기술, AEM에서 Headless 콘텐츠를 제공하는 방법과 콘텐츠를 번역하는 방법을 폭넓게 이해할 수 있습니다.
* [Headless 작성 여정](/help/journey-headless/author/overview.md) - AEM의 강력하고 유연한 Headless 기능과 각각의 능력, 그리고 귀하의 첫 Headless 프로젝트에서 콘텐츠를 모델링하는 방법에 대한 가이드 여정을 시작해 보십시오.
* [Headless 설계 여정](/help/journey-headless/architect/overview.md) - 여기에서 Adobe Experience Manager의 강력하고 유연한 Headless 기능을 접해 보고 프로젝트 콘텐츠를 모델링하는 방법을 알아보십시오.
* [AEM 기술 설명서](https://experienceleague.adobe.com/docs/experience-manager-65.html) - AEM 및 Headless 기술에 대해 확실히 이해하고 있다면 바로 심화 기술 문서를 참조할 수 있습니다.

   * [AEM as a Headless CMS 소개](/help/sites-developing/headless/introduction.md)

* [AEM 개발자 포털](https://experienceleague.adobe.com/landing/experience-manager/headless/developer.html?lang=ko-KR)
