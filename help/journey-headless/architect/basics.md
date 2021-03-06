---
title: 컨텐츠 모델링 기본 사항 학습
description: 컨텐츠 조각을 사용하여 헤드리스 CMS용 컨텐츠를 모델링하는 기본 사항을 알아봅니다.
source-git-commit: 38525b6cc14e9f6025564c060b8cfb4f9e0ea473
workflow-type: tm+mt
source-wordcount: '905'
ht-degree: 4%

---

# AEM을 사용하여 헤드리스에 대한 컨텐츠 모델링 기본 사항을 알아보십시오 {#content-modeling-headless-basics}

## 지금까지 이야기 {#story-so-far}

의 시작 [AEM Headless Content Architect 여정](overview.md) a [소개](introduction.md) 헤드리스를 위한 모델링 컨텐츠와 관련된 기본 개념 및 용어를 다룹니다.

이 문서는 AEM 헤드리스 프로젝트에 대한 컨텐츠를 모델링하는 방법을 이해할 수 있도록 이러한 단원을 기반으로 합니다.

## 목표 {#objective}

* **Audience**: 초보
* **목표**: 헤드리스 CMS에 대한 컨텐츠 모델링 개념을 소개합니다.

## 컨텐츠 조각 모델을 사용한 컨텐츠 모델링 {#architect-content-fragment-models}

컨텐츠(데이터) 모델링은 설정된 기술의 집합으로, 관계 데이터베이스를 개발할 때 자주 사용되므로 AEM Headless에 대해 컨텐츠 모델링이 의미하는 것은 무엇입니까?

### 왜? {#why}

애플리케이션이 AEM에서 필요한 컨텐츠를 일관되고 효율적으로 요청하고 수신할 수 있도록 하려면 이 컨텐츠를 구조화해야 합니다.

즉, 애플리케이션이 응답의 형식을 미리 알고 있으므로 처리하는 방법을 알 수 있습니다. 이 작업은 자유 형식 컨텐츠를 수신하는 것보다 훨씬 쉽습니다. 이 컨텐츠를 구문 분석하여 내용을 포함해야 하므로 사용 방법을 결정할 수 있습니다.

### 방법 소개 {#how}

AEM은 컨텐츠 조각을 사용하여 컨텐츠를 애플리케이션에 헤드리스 전달에 필요한 구조를 제공합니다.

컨텐츠 모델의 구조는 다음과 같습니다.

* 컨텐츠 조각 모델의 정의에 의해 구현됩니다.
* 컨텐츠 생성에 사용되는 컨텐츠 조각의 기반으로 사용됩니다.

>[!NOTE]
>
>컨텐츠 조각 모델은 AEM GraphQL 스키마를 기반으로 사용되므로, 개발자 여정에서 컨텐츠를 검색하는 데 사용됩니다.

컨텐츠에 대한 요청은 표준 GraphQL API의 사용자 정의된 구현인 AEM GraphQL API를 사용하여 수행됩니다. AEM GraphQL API를 사용하면 애플리케이션에서 특정 모델 유형에 따라 각 쿼리를 사용하여 컨텐츠 조각에 대한 (복잡한) 쿼리를 수행할 수 있습니다.

그런 다음 반환된 컨텐츠를 애플리케이션에서 사용할 수 있습니다.

## 컨텐츠 조각 모델을 사용하여 구조 만들기 {#create-structure-content-fragment-models}

컨텐츠 조각 모델은 컨텐츠의 구조를 정의할 수 있는 다양한 메커니즘을 제공합니다.

컨텐츠 조각 모델은 엔티티를 설명합니다.

>[!NOTE]
>새 모델을 만들 수 있으려면 구성 브라우저에서 컨텐츠 조각 기능을 활성화해야 합니다.

>[!TIP]
>
>컨텐츠 작성자가 컨텐츠 조각을 만들 때 선택할 모델을 알 수 있도록 모델의 이름을 지정해야 합니다.

모델 내에서:

1. **데이터 유형** 개별 속성을 정의할 수 있습니다.
예를 들어 교사 이름이 있는 필드를 **텍스트** Dell은 **숫자**.
1. 데이터 유형 **컨텐츠 참조** 및 **조각 참조** AEM 내에서 다른 컨텐츠와의 관계를 만들 수 있도록 해줍니다.
1. 다음 **조각 참조** 데이터 유형을 사용하면 모델 유형에 따라 컨텐츠 조각을 중첩하여 여러 수준의 구조를 구현할 수 있습니다. 이는 컨텐츠 모델링에 필수적입니다.

예:

![컨텐츠 조각을 사용한 컨텐츠 모델링](assets/headless-modeling-01.png "컨텐츠 조각을 사용한 컨텐츠 모델링")

## 데이터 유형 {#data-types}

AEM에서는 컨텐츠를 모델링하는 데 사용할 다음 데이터 유형을 제공합니다.

* 한 줄 텍스트
* 여러 줄 텍스트
* 번호
* 부울
* 날짜 및 시간
* 열거
* 태그
* 컨텐츠 참조
* 조각 참조
* JSON 개체

>[!NOTE]
>
>자세한 내용은 컨텐츠 조각 모델 - 데이터 유형에서 확인할 수 있습니다.

## 참조 및 중첩 컨텐츠 {#references-nested-content}

두 데이터 유형은 특정 조각 외부의 컨텐츠에 대한 참조를 제공합니다.

* **컨텐츠 참조**
모든 유형의 다른 컨텐츠에 대한 간단한 참조를 제공합니다.
예를 들어 지정된 위치에서 이미지를 참조할 수 있습니다.

* **조각 참조**
이 섹션에서는 다른 컨텐츠 조각에 대한 참조를 제공합니다.
이 유형의 참조는 중첩된 콘텐츠를 만드는 데 사용되며 콘텐츠를 모델링하는 데 필요한 관계를 도입합니다.
조각 작성자가 다음을 수행할 수 있도록 데이터 유형을 구성할 수 있습니다.
   * 참조된 조각을 직접 편집합니다.
   * 적절한 모델을 기반으로 새 컨텐츠 조각을 만듭니다

>[!NOTE]
>
>텍스트 블록 내의 링크를 사용하여 임시 참조를 만들 수도 있습니다.

## 구조 수준(중첩된 조각) {#levels-of-structure-nested-fragments}

컨텐츠 모델링용 **조각 참조** 데이터 유형을 사용하면 여러 수준의 구조 및 관계를 만들 수 있습니다.

이 참조를 사용하면 다음 작업을 수행할 수 있습니다 *connect* 상호 관계를 나타내는 다양한 컨텐츠 조각 모델 . 따라서 헤드리스 애플리케이션에서 필요에 따라 연결을 따르고 콘텐츠에 액세스할 수 있습니다.

>[!NOTE]
>
>이 방법은 주의해서 사용해야 하며, 우수 사례는 다음과 같이 정의할 수 있습니다. *필요한 만큼 중첩하지만 가능한 한 적게 중첩하다*.

조각 참조는 다른 조각을 참조할 수 있도록 해줍니다.

예를 들어 다음 컨텐츠 조각 모델이 정의되어 있을 수 있습니다.

* 도시
* 회사
* 개인
* 수상

매우 간단해 보이지만, 회사에는 CEO와 직원들이 모두 있습니다..그리고 이들은 모두 사람들이며, 각각 사람으로 정의되었습니다.

또한 사람은 상을 받을 수 있습니다(또는 둘 중 하나).

* 내 회사 - 회사
   * CEO - 개인
   * 직원 - 개인
      * Personal Award - Award

그리고 그것은 단지 시작자들을 위한 것입니다. 복잡성에 따라 시상식은 회사별 또는 회사가 특정 도시에 본점을 둘 수 있습니다.

이러한 상호 관계를 나타내는 것은 조각 참조(설계자), 컨텐츠 작성자 및 헤드리스 애플리케이션에서 이해할 수 있으므로 조각 참조에서 수행할 수 있습니다.

## 다음은 무엇입니까? {#whats-next}

이제 기본 사항을 익혔으므로 다음 단계는 다음과 같습니다 [AEM에서 컨텐츠 조각 모델 생성에 대해 알아봅니다](model-structure.md). 여기에는 사용 가능한 다양한 참조 및 헤드리스를 위한 모델링의 주요 부분인 조각 참조를 사용하여 구조 수준을 만드는 방법이 소개되고 논의됩니다.

## 추가 리소스 {#additional-resources}

* [컨텐츠 조각 모델](/help/assets/content-fragments/content-fragments-models.md)

   * [컨텐츠 조각 모델 - 데이터 유형](/help/assets/content-fragments/content-fragments-models.md#data-types)

* [작성 개념](/help/sites-authoring/author.md)

* [기본 처리](/help/sites-authoring/basic-handling.md) - 이 페이지는 주로 **Sites** 콘솔은 하지만 대부분의 기능은 작성에도 관련이 있습니다 **컨텐츠 조각** 아래에 **자산** 콘솔.

* [컨텐츠 조각을 사용한 작업](/help/assets/content-fragments/content-fragments.md)
