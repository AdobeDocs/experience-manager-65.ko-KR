---
title: AEM Headless 시작하기
description: 이 AEM Headless 개발자 여정의 부분에서는 AEM Headless 사전 요구 사항에 대해 알아봅니다.
exl-id: a94794a4-bf8b-4f3b-a761-3f02feedd5c0
source-git-commit: 10b370fd8f855f71c6d7d791c272137bb5e04d97
workflow-type: tm+mt
source-wordcount: '2998'
ht-degree: 96%

---

# AEM Headless 시작하기 {#getting-started}

이 [AEM Headless 개발자 여정](overview.md)의 부분에서는 AEM Headless로 자체 프로젝트 시작하기에 필요한 사항에 대해 알아봅니다.

## 지금까지의 스토리 {#story-so-far}

AEM Headless 번역 여정의 이전 문서인 [CMS Headless 개발에 대해 알아보기](learn-about.md)에서 Headless CMS의 기본 이론에 대해 알아보았습니다. 여기에서 알게 된 내용은 다음과 같습니다.

* Headless 콘텐츠 게재에 대한 기본적인 개념과 용어를 이해할 수 있습니다.
* Headless가 필요한 이유와 시점을 이해할 수 있습니다.
* 높은 수준에서 Headless 개념이 어떻게 사용되는지, 어떻게 상호 연관되는지를 파악할 수 있습니다.

이 문서는 해당 기본 사항을 기본으로 하며, 이를 통해 AEM을 사용하여 Headless 솔루션을 구현하는 방법을 이해할 수 있습니다.

## 목표 {#objective}

이 문서는 자체 프로젝트의 컨텍스트에서 AEM Headless를 이해하는 데 도움이 됩니다. 문서를 읽고 나면

* AEM의 Headless 기능에 대한 기본 사항을 이해합니다.
* AEM의 Headless 기능 사용에 대한 사전 요구 사항을 알아봅니다.
* AEM의 Headless 통합 수준을 파악합니다.
* 범위 측면에서 프로젝트를 정의할 수 있습니다.

## AEM 기본 사항 {#aem-basics}

AEM 내에서 Headless 프로젝트를 정의하기 전에 몇 가지 기본 AEM 개념을 이해해야 합니다.

### 작성자 인스턴스 {#author}

간단하게 말해, AEM은 서로 작동하여 콘텐츠를 만들고, 관리하고, 게시하는 작성자 인스턴스와 [게시 인스턴스](#publish)로 구성됩니다.

콘텐츠는 작성자 인스턴스에서 시작됩니다. 여기에서 콘텐츠 작성자는 콘텐츠를 만듭니다. 작성자 환경은 작성자가 콘텐츠를 만들고, 구성하고, 재사용할 수 있는 다양한 도구를 제공합니다.

### 게시 인스턴스 {#publish}

작성자 인스턴스에 생성된 콘텐츠는 다른 서비스에 게시되어야 사용할 수 있게 됩니다. 게시 인스턴스에는 게시된 모든 콘텐츠가 포함됩니다.

### 복제 {#replication}

복제는 콘텐츠를 작성자 인스턴스에서 게시 인스턴스로 이전하는 작업입니다. 이 작업은 작성자 또는 적절한 권한이 있는 다른 사용자가 콘텐츠를 게시하는 경우 AEM에 의해 자동으로 수행됩니다.

### AEM 기본 사항 요약 {#aem-basics-summary}

가장 간단하게 AEM에서 디지털 경험을 만들려면 다음 단계가 필요합니다.

1. 콘텐츠 작성자는 작성자 인스턴스에서 Headless 콘텐츠를 만듭니다.
1. 이 콘텐츠가 준비되면 게시 인스턴스에 복제됩니다.
1. 그런 다음 API를 호출하여 이 콘텐츠를 검색할 수 있습니다.

AEM Headless는 [다음 섹션에서 설명하는](#aem-headless-basics) Headless 콘텐츠를 관리하는 강력한 도구를 제공하여 이 기술적 토대를 기반으로 만들어집니다.

## AEM Headless 기본 사항 {#aem-headless-basics}

AEM의 Headless 기능은 몇 가지 주요 기능을 기반으로 합니다. 이 기능들은 여정 후반부에서 자세히 설명되어 있습니다. 이제 기능의 역할과 용어에 대한 기본 사항을 이해하는 것만으로도 중요합니다.

### 콘텐츠 조각 모델 {#content-fragment-models}

콘텐츠 조각 모델은 AEM에서 만들고 관리할 데이터 및 콘텐츠의 구조를 정의합니다. 콘텐츠를 위한 일종의 스캐폴딩 역할을 합니다. 콘텐츠를 만들려는 작성자는 정의된 콘텐츠 조각 모델 중에서 콘텐츠를 만드는 데 도움이 되는 모델을 선택합니다.

### 콘텐츠 조각 {#content-fragments}

콘텐츠 조각을 사용하여 페이지 독립적인 콘텐츠를 디자인하고 만들고 선별하고 게시할 수 있습니다. 이를 통해 여러 위치와 여러 채널에서 사용할 수 있는 콘텐츠를 준비할 수 있습니다.

콘텐츠 조각에는 구조화된 콘텐츠가 포함되어 있으며 JSON 형식으로 전달할 수 있습니다.

### GraphQL 및 REST API {#apis}

콘텐츠를 Headless 방식으로 수정하기 위해 AEM은 두 개의 강력한 API를 제공합니다.

* GraphQL API를 사용하여 콘텐츠 조각에 액세스하고 전달하기 위한 요청을 생성할 수 있습니다.
* Assets REST API를 사용하면 콘텐츠 조각(및 기타 자산)을 만들고 수정할 수 있습니다.

AEM Headless 여정 후반부에서 해당 API와 이를 사용하는 방법에 대해 알아봅니다. 또는 [추가 리소스](#additional-resources) 추가 설명서에 대해서는 아래 섹션 을 참조하십시오.

## Headless 통합 수준 {#integration-levels}

AEM은 CMS의 전체 Headless 및 기존 전체 스택 또는 Headful 모델을 모두 지원합니다. 단, AEM은 이 두 가지 독점적인 선택뿐만 아니라 두 가지 장점을 결합한 하이브리드 모델을 지원하는 기능을 제공하여 Headless 프로젝트를 유연하게 활용할 수 있습니다.

이 AEM Headless 개발자 여정은 Headless 개념에 대한 이해도를 높이기 위해 AEM에서 코딩 없이 최대한 빨리 작업을 실행할 수 있도록 순수 Headless 모델에 중점을 두고 있습니다.

단, AEM의 Headless 기능을 이해하고 나서 추가 하이브리드 가능성에 대해 알아야 합니다. 해당 사례는 인지도 제고를 위해 아래에 자세히 설명됩니다. 여정이 끝나고 나서 프로젝트에 이러한 유연성이 필요한 경우 해당 개념에 대해 자세히 소개합니다.

### 단일 페이지 애플리케이션(SPA) 등 Headless 콘텐츠는 이미 외부에서 사용되었습니다. {#already-have-a-spa}

AEM의 콘텐츠를 기존 외부 서비스로 제공하는 것이 최소 기본 요구 사항이라고 가정합니다.

#### 수준1: 콘텐츠 조각 통합 - 기존 Headless 모델 {#level-1}

이 수준의 통합은 기존 Headless 모델로서 이를 통해 콘텐츠 작성자는 AEM에서 콘텐츠를 만들어 GraphQL을 통해 Headless 방식으로 여러 외부 서비스에 제공하거나 Assets API를 통해 외부 서비스에서 편집할 수 있습니다. AEM에서는 코딩이 필요하지 않습니다.

이 모델에서 AEM은 AEM 콘텐츠 조각을 통해 콘텐츠를 만들고 제공하는 경우에만 사용됩니다. 콘텐츠를 렌더링하고 콘텐츠와 상호 작용하는 작업이 외부 사용 애플리케이션(종종 단일 페이지 애플리케이션(SPA))에 위임됩니다.

#### 수준 2: AEM에 SPA 임베드 - 하이브리드 모델 {#level-2}

이 수준의 통합은 첫 번째 수준을 기반으로 하므로 이를 통해 콘텐츠 작성자가 AEM 내 외부 애플리케이션의 컨텍스트에서 콘텐츠를 확인할 수 있도록 외부 애플리케이션(SPA)이 AEM에 임베드될 수도 있습니다. 애플리케이션은 AEM 내에서 제한된 외부 애플리케이션 편집을 지원할 수도 있습니다.

이 수준은 콘텐츠 작성자가 AEM의 콘텐츠를 Headful 방식으로 유연하게 작성할 수 있도록 해 주는 장점이 있으며, 임베드된 외부 SPA와 함께 콘텐츠를 컨텍스트 내에 표시하면서 콘텐츠를 Headless 방식으로 계속 제공합니다.

#### 수준 3: AEM의 SPA 임베드 및 전체 활성화 - 하이브리드 모델 {#level-3}

이 수준의 통합은 수준 2를 기본으로 하며, 이를 통해 AEM 내부에서 편집 가능한 외부 SAP에서 대부분의 콘텐츠를 활성화할 수 있습니다.

### 단일 페이지 애플리케이션(SPA) 등 Headless 콘텐츠는 아직 외부에서 사용되지 않았습니다. {#do-not-have-a-spa}

AEM에서 콘텐츠를 Headless 방식으로 사용하는 SPA를 만드는 것이 목표라면 콘텐츠 조각 기능을 사용하여 Headless 콘텐츠를 관리하고 AEM의 SPA 편집기 프레임워크로 SPA를 빌드할 수도 있습니다.

SPA 편집기를 통해 SPA는 AEM에서 콘텐츠를 사용할 뿐만 아니라 콘텐츠 작성자에 의해 AEM 내부에서 완전한 편집이 가능하므로 AEM 내에서 Headless를 유연하게 게재하고 상황에 맞게 편집할 수 있습니다.

## 요구 사항 및 사전 요구 사항 {#requirements-prerequisites}

AEM Headless 프로젝트를 시작하기 전에 알아 두어야 할 몇 가지 요구 사항이 있습니다.

### 지식 {#knowledge}

* GraphQL
* React 또는 Angular 프레임워크를 통해 SPA를 만드는 개발 경험
* 콘텐츠 조각을 만들고 편집기를 사용하는 기본 AEM 기술

### 도구 {#tools}

* 콘텐츠 배포 테스트를 위한 샌드박스 액세스
* 데이터 모델링 및 테스트에 대한 로컬 개발 인스턴스
* 기존 외부 SPA 또는 Headless AEM 콘텐츠의 다른 사용자

## 프로젝트 정의 {#defining-your-project}

성공적인 프로젝트를 위해 프로젝트 요구 사항뿐만 아니라 역할 및 책임을 명확히 정의해야 합니다.

### 범위 {#scope}

프로젝트의 범위를 명확히 정의해야 합니다. 범위는 허용 기준을 알려 주고 완료에 대한 정의를 설정할 수 있도록 합니다.

첫 번째 질문은 “AEM Headless를 통해 얻으려는 목표는 무엇입니까?”입니다. AEM이 아닌 자체 개발 도구로 빌드한 경험 애플리케이션을 보유하거나 앞으로 보유할 수 있다는 것이 이 질문에 대한 일반적인 답변입니다. 이 경험 애플리케이션은 모바일 앱, 웹 사이트 또는 기타 최종 사용자 고객용 경험 애플리케이션일 수 있습니다. AEM Headless 사용 목표는 AEM Headless 호출로 경험 애플리케이션에서 바로 콘텐츠나 CRUD 콘텐츠를 완전히 가져올 수 있는 최신 API를 사용하여 AEM에서 생성, 저장 및 관리되는 콘텐츠로 경험 애플리케이션을 피드하는 것입니다. 이 항목을 원하는 것이 아니면 [AEM 설명서](https://experienceleague.adobe.com/docs/experience-manager-65.html)로 돌아가 수행할 작업에 더 적합한 섹션을 찾습니다.

### 역할 및 책임 {#roles-responsibilities}

개별 프로젝트의 역할이 다양하지만 AEM Headless 개발 콘텐츠에서 고려해야 할 중요한 역할은 다음과 같습니다.

* [관리자](#administrator)
* [콘텐츠 작성자](#content-author)
* [콘텐츠 설계자](#content-architect)
* [개발자](#developer)

#### 관리자 {#administrator}

관리자는 시스템의 기본 설정 및 구성을 담당합니다. 예를 들어 관리자는 Identity Management System(IMS)이라는 Adobe 사용자 관리 시스템 내에서 조직을 설정합니다. 관리자는 조직이 IMS 내의 Adobe에 의해 생성되면 Adobe로부터 이메일 초대를 수신하는 조직의 첫 번째 사용자입니다. 관리자는 IMS에 로그인하여 다른 담당자의 사용자를 추가할 수 있습니다.

관리자가 사용자를 구성하면 모든 AEM 리소스에 액세스할 수 있는 권한이 부여되어 AEM Headless를 사용하여 경험 애플리케이션을 게재하는 기여자로 작업할 수 있습니다.

관리자는 AEM을 설정하고 런타임 환경을 준비하는 사용자로서, 이를 통해 [콘텐츠 작성자](#content-author)는 콘텐츠 및 [개발자](#developer)를 만들고 업데이트하여 경험 애플리케이션용 콘텐츠를 가져오거나 수정하는 API를 사용할 수 있습니다.

#### 콘텐츠 작성자 {#content-author}

콘텐츠 작성자는 AEM에서 Headless 방식으로 게재하는 콘텐츠를 만들고 관리합니다. 콘텐츠 작성자는 콘텐츠 조각과 자산 콘솔 등 AEM 기능을 사용하여 콘텐츠를 관리합니다.

콘텐츠 작성자는 다음 모범 사례를 고려해야 합니다.

#### 번역을 위한 계획 {#translation}

프로젝트의 시작 부분부터 번역을 위한 계획을 수립합니다. “번역 전문가”를 번역할 콘텐츠와 하지 않을 콘텐츠를 정의하고 지역 또는 로컬 콘텐츠 제작자가 수정할 수 있는 번역된 콘텐츠를 정의하는 역할을 담당할 별도의 담당자로서 간주합니다.

필요한 콘텐츠 번역에 대한 계획을 수립합니다.

* 다른 언어나 지역 특성에 적응할 수 있는 언어가 필요합니까?
* 로케일에 따라 달라지는 리치 미디어 콘텐츠(예: 이미지나 비디오 등)가 필요합니까?

콘텐츠 업데이트 워크플로를 명확히 알립니다. 시스템이 지원해야 하는 승인 프로세스는 무엇입니까? AEM 워크플로를 사용하여 이 프로세스를 자동화할 수 있습니까?

[콘텐츠 계층](#content-hierarchy)을 사용하여 번역을 보다 쉽게 할 수 있습니다.

AEM Headless 번역 여정 링크를 포함하여 AEM 워크플로 및 번역 도구에 대한 추가 설명서는 [추가 리소스](#additional-resources) 섹션을 참조하십시오.

##### 콘텐츠 계층 활용 {#content-hierarchy}

폴더 계층은 콘텐츠 관리와 관련된 두 가지 주요 문제를 해결할 수 있습니다.

* [번역](#translation) - AEM은 로케일별 폴더에서 콘텐츠 사본을 유지 관리하면서 콘텐츠 번역을 관리합니다.
* 조직 - 폴더를 사용하여 번역 요구 사항을 지원하고 콘텐츠 조각을 논리적으로 관리하는 데 필요한 콘텐츠 계층을 정의합니다.

AEM에서는 유연한 콘텐츠 구조를 사용하고 계층은 임의적으로 커질 수 있습니다. 단, 폴더 구조의 모든 변경 사항이 콘텐츠 경로를 [사용하는 기존 쿼리에 의도하지 않은 결과를 초래할 수 있음을 인식해야 합니다.](#developer)따라서 사전에 명확하게 설정 및 정의된 계층은 콘텐츠 작성자에게 도움이 될 수 있습니다.

특정 유형의 콘텐츠만 허용하도록 폴더를 제한할 수도 있습니다(콘텐츠 조각 모델 기반). 계층의 모든 폴더에 허용되는 모델을 항상 명시적으로 지정하는 것이 좋습니다. 지정된 폴더에 허용된 콘텐츠 지정:

* 콘텐츠 작성자는 폴더에 속하지 않는 콘텐츠를 작성할 수 없습니다.
* 유효한 콘텐츠 유형만 표시되도록 작성 중에 폴더에서 허용되는 콘텐츠 유형을 필터링하여 콘텐츠 생성 프로세스를 최적화합니다.

적절한 콘텐츠 구조를 만들면 채널 간에 Headless 콘텐츠 작성을 더 쉽게 조정하여 콘텐츠 재사용을 극대화할 수 있습니다. 여러 채널에서 콘텐츠를 활용하면 콘텐츠 프로덕션 효율성과 변경 관리를 크게 향상시킬 수 있습니다.

##### 좋은 명명 규칙 수립 {#naming-conventions}

콘텐츠 조각 이름은 콘텐츠 작성자를 설명해야 합니다. AEM은 저장소 수준에서 이름에 사용되는 ID의 이스케이프 및/또는 자르기를 투명하게 처리합니다. 따라서 콘텐츠 작성자가 제공하는 논리적 이름은 항상 읽을 수 있고 콘텐츠를 나타내야 합니다.

* 좋지 않은 이름: `cta_btn_1`
* 좋은 이름: `Call To Action Button`

AEM 페이지 이름 지정 규칙에 대한 추가 설명서는 [추가 리소스](#additional-resources) 섹션을 참조하십시오.

##### 콘텐츠 중첩을 지나치게 확장하지 마십시오. {#content-nesting}

[콘텐츠 조각](#content-fragments)은 AEM에서 Headless 콘텐츠를 만드는 데 사용됩니다. AEM은 콘텐츠 조각에 대해 최대 10개의 콘텐츠 중첩 수준을 지원합니다. 단, AEM은 상위 콘텐츠 조각에 정의된 각 참조를 반복적으로 해결한 다음 하위 참조가 동일한 수준의 참조에 모두 있는지 확인해야 하는 것이 중요합니다. 해당 작업은 빠르게 합산되어 성능 관련 문제가 될 수 있습니다.

일반적으로 콘텐츠 조각 참조는 다섯 개 수준 이상으로 중첩되어서는 안 됩니다.

#### 콘텐츠 설계자 {#content-architect}

콘텐츠 설계자는 Headless 방식으로 사이트에 게재할 데이터에 대한 요구 사항을 분석하고 해당 데이터의 구조를 정의합니다. 해당 구조를 AEM에서는 [콘텐츠 조각 모델](#content-fragment-models)이라고 합니다. 콘텐츠 조각 모델은 콘텐츠 작성자가 만든 콘텐츠 조각의 기초로 사용됩니다.

콘텐츠 조각 모델을 정의할 때 유용한 접근 방식은 콘텐츠를 사용하는 애플리케이션의 UX 구성 요소에 매핑하는 모델을 만드는 것입니다.

콘텐츠 작성자는 새 콘텐츠를 만들 때 지속적으로 모델과 상호 작용하므로 UX에 맞춰 모델을 조정하게 되면 최종 디지털 경험을 시각화하는 데 도움이 됩니다. 이 조정 단계를 추가하면서 아이콘을 UX 요소를 나타내는 콘텐츠 조각 모델에 지정할 수 있으므로 작성자는 시각적 큐에 따라 올바른 모델을 직관적으로 선택할 수 있습니다.

#### 개발자 {#developer}

개발자는 경우에 따라 단일 페이지 애플리케이션(SPA), 점진적 웹 앱(PWA), 웹 앱이나 AEM 외부 기타 서비스일 수 있는 해당 콘텐츠 사용자에게 AEM에서 Headless 방식으로 생성되는 콘텐츠를 연결하는 역할을 담당합니다.

GraphQL은 AEM과 Headless 콘텐츠 사용자 사이에서 “접착제” 역할을 합니다. GraphQL은 필요한 콘텐츠에 대한 AEM을 쿼리하는 언어입니다.

개발자는 쿼리에 대한 계획을 수립하는 경우 몇 가지 기본 권장 사항을 고려해야 합니다.

* 쿼리는 콘텐츠 조각 검색에 고정 경로(`ByPath`)를 사용해서는 안 됩니다.
   * [콘텐츠 작성자는 콘텐츠 조각 계층을 완전히 제어하고](#content-hierarchy) 해당 쿼리를 중단시키는 변경 내용을 적용할 수 있습니다.
   * 대신 쿼리는 동적 쿼리 매개변수가 있는 콘텐츠 조각 모델 참조를 선택하여 원하는 페이로드를 생성하도록 결과를 필터링해야 합니다.
* 최상의 쿼리를 수행하려면 항상 AEM에서 지속 쿼리를 사용합니다. 여정 후반부에서 자세히 설명합니다.
* GraphQL은 “필요한 것은 정확히 요청하고 제대로 얻습니다.”라는 모토에 따라 선언적입니다. 즉, GraphQL 쿼리를 만드는 도중 관계형 데이터베이스에서 만들 수 있는 `select *`유형 쿼리는 항상 피해야 합니다.

[AEM을 사용하여 일반적으로 Headless를 구현하는 경우 ](#level-1) 개발자는 AEM에 대한 코딩 지식이 필요하지 않습니다.

### 성능 요구 사항 {#performance-requirements}

프로젝트 성공을 위해 콘텐츠를 만들기 전에 성능을 고려해야 합니다.

사용자/방문자의 기대와 이에 대한 설계를 이해해야 합니다. 서비스 수준 목표(SLO)를 설정하고 이를 측정하여 사용자의 기대가 충족되었는지 파악합니다.

#### 트래픽 패턴 {#traffic-patterns}

트래픽과 트래픽 패턴을 이해하려면 과거 정보를 수집한 다음 앞으로 몇 년 동안 기대되는 성장을 추진합니다. 고려해야 할 가장 중요한 변수 중 일부는 다음과 같습니다.

* 시간/일/월 기준 예상되는 API 호출 개수는 얼마이고 개수가 증가하고 계절성이 발생할 가능성이 있습니까?
* 몇 명의 콘텐츠 작성자가 있습니까?
* 몇 명의 콘텐츠 작성자가 동시에 작업할 것으로 예상합니까?
* 콘텐츠 업데이트 주기란 무엇입니까?
* 몇 개의 콘텐츠 모델이 필요합니까?
* 몇 개의 모델 인스턴스가 필요합니까?

#### 업데이트 주기 {#update-frequency}

경험 섹션이 다르면 콘텐츠 업데이트 주기가 달라지는 경우가 있습니다. 이 정보를 이해하려면 CDN 및 캐시 구성을 미세 조정할 수 있어야 합니다. [콘텐츠 설계자](#content-architects)가 모델을 디자인하여 콘텐츠를 나타내는 경우 중요한 정보입니다. 고려해야 할 사항:

* 특정 기간이 경과하면 특정 유형의 콘텐츠는 만료되어야 합니까?
* 사용자별로 지정되어 캐시될 수 없는 요소가 있습니까?

## 다음 단계 {#what-is-next}

AEM Headless 개발자 여정의 한 부분을 완료했으므로,

* AEM의 Headless 기능에 대한 기본 사항을 이해합니다.
* AEM의 Headless 기능 사용에 대한 사전 요구 사항을 알아봅니다.
* AEM의 Headless 통합 수준을 파악합니다.
* 범위 측면에서 프로젝트를 정의할 수 있습니다.

다음 문서인 [AEM Headless를 사용한 첫 번째 경험으로의 경로](path-to-first-experience.md)를 검토하여 AEM Headless 여정을 계속하는 것이 좋습니다. 여기에서는 필요한 도구를 설정하는 방법과 AEM에서 데이터를 모델링하는 방법에 대해 어떻게 생각하고 있는지에 대해 알아보게 됩니다.

## 추가 리소스 {#additional-resources}

다음 문서인 [AEM Headless를 사용한 첫 번째 경험으로의 경로](path-to-first-experience.md)를 검토하여 Headless 개발 여정의 다음 부분으로 넘어가는 것이 좋습니다. 다음은 이 문서에 나열된 몇 가지 개념을 자세히 알아보는 추가적인 옵션 리소스이며, 이들 리소스를 Headless 여정에서 계속 사용할 필요는 없습니다.

* [AEM의 Headful 및 Headless](/help/sites-developing/headful-headless.md) - AEM에서 사용 가능한 Headless 통합 수준에 대한 전체 설명

* [AEM as a Headless CMS 소개](/help/sites-developing/headless/introduction.md)

* [AEM Headless 번역 여정](/help/journey-headless/translation/overview.md) - 이 설명서 여정을 통해 Headless 기술, AEM에서 Headless 콘텐츠를 제공하는 방법과 콘텐츠를 번역하는 방법을 폭넓게 이해할 수 있습니다.

* [AEM Headless 튜토리얼](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/overview.html) - 이 실습 튜토리얼을 사용하여 AEM을 통해 콘텐츠를 Headless 엔드포인트를 게재하는 옵션을 사용하는 방법을 살펴보고 자신에게 적합한 옵션을 선택합니다.
* [GraphQL API를 사용한 Headless 콘텐츠 관리](https://experienceleague.adobe.com/?Solution=Experience+Manager&amp;Solution=Experience+Manager+Sites&amp;Solution=Experience+Manager+Forms&amp;Solution=Experience+Manager+Screens&amp;launch=ExperienceManager-D-1-2020.1.headless#courses) - 이 과정에 따라 AEM에서 구현되는 GraphQL API의 개요를 확인합니다. AdobeID를 통한 인증이 필수입니다.
* [AEM Guides WKND - GraphQL](https://github.com/adobe/aem-guides-wknd-graphql) - 이 GitHub 프로젝트에는 AEM의 GraphQL API를 강조 표시하는 예제 애플리케이션이 포함됩니다.
* [작성 개념](/help/sites-authoring/author.md) - 작성-게시 설정의 세부 정보가 포함된 AEM의 작성 환경을 대한 기술 설명서
* [페이지 게시](/help/sites-authoring/publishing-pages.md) - AEM에서 콘텐츠 게시에 대한 기술 설명서
* [이름 지정 규칙](/help/sites-developing/naming-conventions.md) - AEM에서 페이지 이름 지정 제한 사항에 대한 기술 설명서
* [다중 사이트 관리자 및 번역](/help/sites-administering/msm-and-translation.md) - AEM의 강력한 번역 기능에 대한 기술 설명서
* [AEM 워크플로](/help/sites-authoring/workflows.md) - AEM에서 워크플로를 자동화하는 방법에 대한 기술 설명서
* [콘텐츠 조각](/help/assets/content-fragments/content-fragments.md) - 콘텐츠 조각에 대한 기술 설명서.
* [콘텐츠 조각 모델](/help/assets/content-fragments/content-fragments-models.md) - 콘텐츠 조각 모델에 대한 기술 설명서.
* [GraphQL 기술 설명서](https://graphql.org) - GraphQL 정의(외부 링크)
* [GraphQL API](/help/sites-developing/headless/graphql-api/graphql-api-content-fragments.md) - 콘텐츠 조각에 액세스하고 전달하기 위한 요청을 만드는 방법에 대한 기술 설명서
* [Assets REST API](/help/assets/assets-api-content-fragments.md) - 콘텐츠 조각(및 기타 자산)을 만들고 수정하는 방법에 대한 기술 설명서
* [지속 쿼리](/help/sites-developing/headless/graphql-api/persisted-queries.md) - AEM의 지속 쿼리에 대한 기술 설명서
* [AEM 개발자 포털](https://experienceleague.adobe.com/landing/experience-manager/headless/developer.html)