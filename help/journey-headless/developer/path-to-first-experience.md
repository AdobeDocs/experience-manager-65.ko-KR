---
title: AEM Headless를 사용한 첫 번째 경험으로의 경로
description: 이 AEM Headless 개발자 여정의 부분에서는 계획 고려 사항을 비롯해 AEM에서 첫 번째 Headless 경험을 구현하는 단계를 이해하고, 경로를 최대한 원활하게 만드는 모범 사례에 대해 알아보기도 합니다.
exl-id: 64a87b6b-67ff-4d88-9dfb-c3e5de65bbe6
source-git-commit: 7f35fdee9dbca9dfd3992b56579d6d06633f8dec
workflow-type: tm+mt
source-wordcount: '1990'
ht-degree: 90%

---

# AEM Headless를 사용한 첫 번째 경험으로의 경로 {#path-to-first-experience}

이 [AEM Headless 개발자 여정](overview.md)의 부분에서는 계획 고려 사항을 비롯해 AEM에서 첫 번째 Headless 경험을 구현하는 단계를 이해하고, 경로를 최대한 원활하게 만드는 모범 사례에 대해 알아보기도 합니다.

## 지금까지의 스토리 {#story-so-far}

AEM Headless 번역 여정의 이전 문서인 [AEM Headless 시작하기](getting-started.md)에서 Headless CMS의 기본 이론에 대해 알아보았습니다. 여기에서 알게 된 내용은 다음과 같습니다.

* AEM의 Headless 기능에 대한 기본 사항을 이해합니다.
* AEM의 Headless 기능 사용에 대한 사전 요구 사항을 알아봅니다.
* AEM의 Headless 통합 수준을 파악합니다.
* 범위 측면에서 프로젝트를 정의할 수 있습니다.

이 문서는 해당 기본 사항을 기본으로 하며, 이를 통해 자체 AEM Headless 프로젝트를 준비하는 방법을 이해할 수 있습니다.

## 목표 {#objective}

이 문서는 첫 번째 프로젝트를 구현하는 데 필요한 단계를 이해하는 데 도움이 됩니다. 문서를 읽고 나면

* 콘텐츠 디자인을 대한 중요한 계획 고려 사항을 이해할 수 있습니다.
* AEM에서 Headless를 구현하는 단계를 이해할 수 있습니다.
* 필요한 도구 및 AEM 구성을 파악할 수 있습니다.
* 모범 사례를 파악하여 원활하게 Headless 여정을 수행하고, 효율적으로 콘텐츠를 생성하고, 빠르게 콘텐츠를 게재할 수 있습니다.

## 요구 사항 {#requirements}

이 문서를 계속하기 전에 AEM Headless 개발자 여정의 이전 문서인 [AEM Headless 시작하기](getting-started.md)를 검토했는지 확인하고 다음을 진행합니다.

* 나열된 요구 사항을 수행합니다.
* 범위, 역할 및 성과를 비롯해 자체 프로젝트 정의를 고려했습니다.

## 성공을 위한 계획 수립 {#planning-for-success}

첫 번째 AEM Headless 프로젝트를 시작하려면 모든 채널에서 수행할 개인화와 업데이트를 지원하는 콘텐츠 모델이 있는지 확인해야 합니다.

AEM과 별도로, AEM에 대한 API 호출에 대해 클라이언트를 테스트할 수 있도록 클라이언트측 애플리케이션을 빌드하는 경우 적절한 개발 환경을 설정하도록 하려는 경우도 있습니다.

### 콘텐츠 조각 모델 및 API 정의 {#defining-models}

각 개별 채널을 확인하고 게재할 자체 콘텐츠 구조로 표시할 수 있도록 일관된 경험을 제공하고 다양한 채널에서 개인화된 캠페인을 관리하려고 합니다. 하지만 각 채널에 자체 콘텐츠 모델이 있으면 유지하는 것이 어려울 수 있습니다.

대신, 브랜드 및 제품 계층, 상품이나 표면의 범주 또는 고객 여정의 단계 등 구성 원칙을 기반으로 다양한 표면의 콘텐츠가 연계되는 방식을 고려해야 합니다. 예를 들어 제조하는 자동차의 특정 브랜드를 지원하는 표면 세트가 있는 경우 전체 자동차에 적용되는 일반 정보에 대한 콘텐츠 모델을 시작한 다음 차량 시동 시점부터 서비스 문제 발생 시점까지 필요한 콘텐츠와 같은 특정 요소를 추가할 수 있습니다. 해당 모델은 일반 자동차 브랜드 콘텐츠의 상속을 적용하는 동시에 필요한 특정 컨텍스트에 따라 전환됩니다. 또한 전체 자동차 브랜드 마케터 또는 제품 관리자와 “차량 시동” 경험을 담당하는 작성자와 같은 역할에 따라 컨트롤을 적용할 수 있으므로 이 콘텐츠에 대한 향후 업데이트 관리에 도움이 됩니다.

콘텐츠를 표시할 다양한 클라이언트에 콘텐츠 모델과 뷰 지우기가 있는 경우 이 콘텐츠가 필요한 모든 클라이언트에 다양한 콘텐츠 모델 액세스와 연계된 GraphQL/API가 게시되었는지 확인해야 합니다. 특정 콘텐츠에 액세스하는 방법에는 다양한 옵션이 있습니다. 콘텐츠 캐싱과 고성능을 활성화하는 정적인 특정 콘텐츠를 요청할 수 있습니다. 추가 처리가 필요한 동적으로 생성된 콘텐츠를 요청할 수도 있습니다. 클라이언트가 비즈니스 요구 사항에 가장 효율적인 API를 사용하고 있는지 확인합니다.

## 환경 이해 {#understanding-environments}

AEM에는 개발, 스테이징, 프로덕션 등 세 가지 유형의 환경이 있습니다.

개발 환경(여러 환경이 있을 수 있음)은 아이디어를 실험하고 시도할 수 있는 안전한 장소입니다. 프로젝트 초기 단계에서 개발 환경을 사용하여 콘텐츠 모델의 변형을 시도하고 표면에 의도한 출력이 제공되었는지 확인하는 것이 좋습니다.

Headless 프로젝트의 스테이징 환경은 프로덕션으로 배포되기 전에 새 AEM 제품 릴리스를 확인하는 데 사용됩니다. 변경 내용을 적용하거나 AEM 릴리스가 변경되는 경우 여전히 동일한 출력을 제공하는 JSON 파일을 비교하여 렌더링할 수 있도록 프로덕션 콘텐츠 모델의 목록과 콘텐츠의 하위 집합을 최신 상태로 유지합니다.

프로덕션은 콘텐츠 작성자가 실제 콘텐츠를 만들고 관리하는 위치입니다. 프로덕션 모델 변경은 이전 버전과의 호환성을 고려하여 신중하게 수행해야 합니다.

개발 단계에서는 개발 및 스테이징 환경을 사용하여 작업하는 것이 좋습니다. 성능 테스트로 이동하면 프로덕션 환경으로 이동해야 합니다.

### 개발자와 콘텐츠 작성자의 협업 {#cooperation}

개발자는 채워진 콘텐츠 모델로 설정된 AEM 개발 환경이 필요합니다. 콘텐츠 작성자가 콘텐츠를 만들고 있으므로 개발자는 AEM Headless에서 콘텐츠를 사용할 클라이언트를 개발합니다. 그래서 API 정의가 실제로 중요합니다. 개발자는 AEM SDK를 사용하여 테스트 후크를 만들 수 있으므로 클라이언트가 콘텐츠를 제대로 렌더링할 수 있는지 확인하기 위해 클라이언트 및 단위 테스트를 만들 수 있습니다.

콘텐츠 작성자는 스테이징 환경에 정의된 콘텐츠 모델을 기반으로 콘텐츠를 만듭니다. 작성자는 콘텐츠 조각 작성 도구를 사용하여 콘텐츠 조각을 만들거나 기존 콘텐츠 조각을 편집합니다. 게시하기 전에 작성자는 개발자와 협력하여 콘텐츠 모델을 개발로 푸시하는 클라이언트에 콘텐츠가 표시되는 방식을 미리 보거나 개발자 환경을 설정하여 클라이언트에 콘텐츠가 표시되는 방식을 미리 볼 수 있습니다.

## 설정 {#setup}

AEM에서 Headless를 시작하기 전에 필요한 모든 기능이 활성화되어 있는지 확인해야 합니다. 이 섹션에서는 필요한 사항에 대해 간략히 소개합니다. 다음 단계를 수행하기 위한 실제 단계는 [AEM Headless 개발자 여정](#overview.md) 후반부에 자세히 설명되어 있습니다.

또한 다음을 선택적으로 볼 수 있습니다. [추가 리소스](#additional-resources) 개별 항목에 대한 자세한 내용은 을 참조하십시오.

### 구성 {#configuration}

1. 콘텐츠 조각 활성화
1. GraphQL 활성화
1. Headless SDK 설정

## 첫 번째 AEM Headless 앱 구현

콘텐츠를 게재할 AEM을 사용하여 첫 번째 Headless 앱을 구현하는 데 필요한 사항에 대한 개요입니다. 해당 단계를 수행하는 방법은 Headless 개발자 여정 후반부에 자세히 설명되어 있습니다.

1. 콘텐츠 조각 모델 만들기
1. 콘텐츠 조각 만들기
1. GraphQL로 콘텐츠 쿼리

## 모범 사례 {#best-practices}

Headless 프로젝트는 기술 구현뿐만 아니라 적합한 계획 수립 및 프로젝트 거버넌스로 인해 성공을 거두었습니다. 다음은 프로젝트를 계획할 때 콘텐츠 작성자와 개발자가 모두 염두에 두어야 할 몇 가지 모범 사례입니다.

### 콘텐츠 구성 {#organizing-content}

* 구조는 필요에 따라 복잡하게 만들지만 최대한 단순하게 유지합니다. 단순한 콘텐츠 구조는 콘텐츠 거버넌스를 간소화하고 시스템 성능을 개선하는 데 도움이 됩니다.
* 전략에서 콘텐츠 재사용의 우선 순위를 정합니다. 여러 상위 모델과 채널에서 재사용할 수 있는 하위 모델 및 콘텐츠 참조를 만듭니다.
* 콘텐츠 작성자가 학습하고 작성 작업에 신속하게 적응할 수 있도록 설명이 따로 필요하지 않은 콘텐츠 구조를 만듭니다.
* 액세스 제한이 있는 경우 콘텐츠 모델을 액세스 요구 사항에 일치시킵니다.
* 액세스 요구 사항이 있는 경우 콘텐츠 계층을 구축해야 합니다. 동일한 사용자 그룹이 편집한 콘텐츠를 함께 그룹화합니다.
* 유사한 콘텐츠를 폴더로 그룹화합니다.
   * 콘텐츠 작성자는 기존 콘텐츠를 복사하고 붙여넣어 새 콘텐츠를 만들 수 있습니다. 따라서 동일한 폴더에서 이 작업을 보다 효율적으로 수행할 수 있습니다.
   * AEM을 통해 허용되는 모델을 폴더당 설정할 수 있으므로 **새로 만들기** 버튼은 해당 위치에서 지원되는 모델만 표시합니다.
* 루트 폴더가 모델에 설정된 경우 새 콘텐츠 조각의 인라인 콘텐츠 조각 편집기 생성을 간소화할 수 있습니다. 그런 다음 실무자는 위치를 선택하지 않아도 됩니다. 이름만 입력하면 새 참조 편집을 시작할 수 있습니다.

### 콘텐츠 작성 {#authoring}

* 채널별 콘텐츠의 버전에는 콘텐츠 조각 변형을 사용하는 것이 좋습니다. 변형은 콘텐츠 마스터와 동기화되어 콘텐츠 변경 관리를 간소화합니다.
* 다른 콘텐츠 제작자를 초대하여 콘텐츠 검토를 실시하고 콘텐츠 조각 편집기와 콘텐츠 조각 Admin Console의 조각에서 전역적으로 사용할 수 있는 주석 및 댓글로 피드백을 제공할 수 있도록 합니다.
* 필수 요소를 최대한 적게 사용하여 흐름을 유지합니다. 필수 요소는 워크플로를 차단할 수 있습니다.

### 전역 콘텐츠 작성 {#localization}

* 콘텐츠 번역을 위한 규칙 및 거버넌스를 구축합니다. 시스템 로드를 줄이려면 번역을 장기간 실행할 수 있는 비동기 프로세스로 설정합니다. 현지화 품질 관리 및 버그 수정에 시간을 할당합니다.
* 번역 메모리 등 AEM과 통합할 수 있는 번역 기술 시스템에서 제공하는 모든 기능을 활용합니다.
* 이미지와 비디오 등 리치 미디어 콘텐츠에 현지화가 필요한지 확인합니다.

## 다음 단계 {#what-is-next}

AEM Headless 개발자 여정의 한 부분을 완료했으므로,

* 콘텐츠 디자인을 대한 중요한 계획 고려 사항을 이해할 수 있습니다.
* AEM에서 Headless를 구현하는 단계를 이해할 수 있습니다.
* 필요한 도구 및 AEM 구성을 파악할 수 있습니다.
* 모범 사례를 파악하여 원활하게 Headless 여정을 수행하고, 효율적으로 콘텐츠를 생성하고, 빠르게 콘텐츠를 게재할 수 있습니다.

이 기본 지식을 기반으로 AEM Headless의 기능과 유연성을 완전히 이해하려고 하므로 자체 프로젝트에 활용할 수 있습니다. 이 작업을 수행할 옵션이 있습니다.

### 나만의 어드벤처 선택 {#choose-your-path}

학습 스타일에 상관없이 Adobe는 성공적인 AEM Headless 프로젝트 시작을 기대합니다.

* **Headless 개념 및 AEM의 Headless 기술**&#x200B;에 대해 계속 알아보려면 다음 문서인 [콘텐츠를 AEM 콘텐츠 모델로 모델링하는 방법](model-your-content.md)을 검토하여 AEM Headless 여정을 계속하는 것이 좋습니다(AEM의 콘텐츠 구조를 모델링하는 방법에 대해 알아보는 경우).
* **직접 해보면서 배우는 것**&#x200B;을 선호하면 [AEM Headless 실습 튜토리얼 시작하기](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/multi-step/overview.html)로 이동할 수 있습니다(AEM Headless 콘텐츠를 노출하는 간단한 프로젝트를 구현하여 AEM Headless 개발로 직접 이동하는 경우).

## 추가 리소스 {#additional-resources}

다음 문서인 [콘텐츠를 AEM 콘텐츠 모델로 모델링하는 방법](model-your-content.md)을 검토하여 Headless 개발 여정의 다음 부분으로 넘어가는 것이 좋습니다. 다음은 이 문서에 나열된 몇 가지 개념을 자세히 알아보는 추가적인 옵션 리소스이며, 이들 리소스를 Headless 여정에서 계속 사용할 필요는 없습니다.

* [AEM Headless 번역 여정](/help/journey-headless/translation/overview.md) - 이 설명서 여정을 통해 Headless 기술, AEM에서 Headless 콘텐츠를 제공하는 방법과 콘텐츠를 번역하는 방법을 폭넓게 이해할 수 있습니다.
* [AEM Sites용 헤드리스 개발](/help/sites-developing/headless/introduction.md) - AEM Headless 개발자에게 필요한 기능을 간단히 소개합니다
* [AEM Headless 튜토리얼](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/overview.html) - 이 실습 튜토리얼을 사용하여 AEM을 통해 콘텐츠를 Headless 엔드포인트를 게재하는 옵션을 사용하는 방법을 살펴보고 자신에게 적합한 옵션을 선택합니다.
* [GraphQL API를 사용한 Headless 콘텐츠 관리](https://experienceleague.adobe.com/?Solution=Experience+Manager&amp;Solution=Experience+Manager+Sites&amp;Solution=Experience+Manager+Forms&amp;Solution=Experience+Manager+Screens&amp;launch=ExperienceManager-D-1-2020.1.headless#courses) - 이 과정에 따라 AEM에서 구현되는 GraphQL API의 개요를 확인합니다. AdobeID를 통한 인증이 필수입니다.
* [AEM Guides WKND - GraphQL](https://github.com/adobe/aem-guides-wknd-graphql) - 이 GitHub 프로젝트에는 AEM의 GraphQL API를 강조 표시하는 예제 애플리케이션이 포함됩니다.
* [Headless 시작 안내서](/help/sites-developing/headless/introduction.md#getting-started) - AEM에 대해 이미 알고 있는 사용자를 위한 AEM Headless 기능을 간략하게 소개합니다.
* [콘텐츠 조각 모델 만들기](/help/assets/content-fragments/content-fragments-models.md) - 콘텐츠 조각 모델에 대한 기술 설명서
* [콘텐츠 조각 만들기](/help/assets/content-fragments/content-fragments.md) - 콘텐츠 조각에 대한 기술 설명서
* [GraphQL로 콘텐츠 쿼리](/help/sites-developing/headless/graphql-api/graphql-api-content-fragments.md) - GraphQL API에 대한 기술 설명서
* [AEM 개발자 포털](https://experienceleague.adobe.com/landing/experience-manager/headless/developer.html)
