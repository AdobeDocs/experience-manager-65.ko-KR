---
title: AEM Headless Content Author 여정
description: Adobe Experience Manager의 강력하고 유연한 헤드리스 기능 및 프로젝트용 컨텐츠를 작성하는 방법에 대한 소개입니다.
exl-id: 39d2218a-4f11-459d-8514-cfd312246be5
source-git-commit: ed11891c27910154df1bfec6225aecd8a9245bff
workflow-type: tm+mt
source-wordcount: '630'
ht-degree: 3%

---

# AEM을 통한 Headless 작성 - 소개 {#author-headless-introduction}

의 이 부분에서 [AEM Headless Content Author 여정](overview.md), AEM(Adobe Experience Manager)을 사용하여 헤드리스 컨텐츠 전달을 위한 컨텐츠 작성을 이해하는 데 필요한 (기본) 개념과 용어를 배울 수 있습니다.

## 목표 {#objective}

* **Audience**: 초보
* **목표**: 헤드리스 작성과 관련된 개념과 용어를 도입합니다.

## CMS(콘텐츠 관리 시스템) {#content-management-system}

컨텐츠 관리 시스템이란 무엇입니까?

CMS(Content Management System)는 컨텐츠 관리에 사용되는 컴퓨터 시스템이라는 뜻입니다. 이는 일반적으로 웹 사이트에서 사용할 수 있도록 하려는 컨텐츠를 관리하는 데 사용됩니다. 더 자세하게는 일반적으로 웹 사이트에서 사용할 수 있는 컨텐츠를 관리하는 데 사용됩니다.

## Headless CMS {#headless-cms}

헤드리스는 컨텐츠를 웹에 표시하는 방식에서 효과적으로 컨텐츠를 탐지하는 시스템을 설명하는 데 사용되는 용어입니다.

일반적으로 CMS에서 컨텐츠를 관리하며, 동일한 CMS가 웹 페이지에서 해당 컨텐츠를 렌더링할 책임이 있습니다.

이제, 헤드리스는 컨텐츠 세트를 CMS에서 관리하고 하나 이상의 (독립) 애플리케이션에서 액세스할 수 있음을 의미합니다.

즉, 컨텐츠를 다양한 형식으로 모든 장치에 전달할 수 있습니다. 이렇게 하면 전체 프로세스가 보다 유연해집니다. 즉, 레이아웃과 형식에 대해 걱정할 필요가 없습니다.

>[!NOTE]
>
>헤드리스 CMS의 기술적인 세부 사항에 대해 자세히 알아보려면 CMS 헤드리스 개발에 대한 학습 을 참조하십시오.

## Adobe Experience Manager {#aem-cms}

그러면 AEM은 무엇일까요?

우선, AEM은 요구 사항을 충족하도록 사용자 지정할 수 있는 다양한 기능을 갖춘 컨텐츠 관리 시스템입니다.

이는 모두 로 사용할 수 있음을 의미합니다.

* 헤드리스 CMS
   * 헤드리스의 경우 컨텐츠를 **컨텐츠 조각**.
이러한 항목은, **컨텐츠 조각 모델**.
즉, 컨텐츠는 광범위한 포맷과 다양한 기능을 통해 광범위한 장치에 도달할 수 있습니다.
(그리고 필요하면 이러한 조각을 AEM 웹 페이지를 구성할 때도 사용할 수 있습니다.)

* &quot;전통적인&quot; CMS
   * 컨텐츠는 웹 사이트에서 컨텐츠가 렌더링되는 방식을 정의하는 다양한 구성 요소를 사용하여 웹 페이지에 대해 작성됩니다. 여기에서도 AEM은 프로젝트 팀이 사용자 지정된 구성 요소를 개발할 수 있으므로 매우 유연합니다.

## 컨텐츠 모델링 {#content-modeling}

따라서 컨텐츠 모델링(데이터 모델링이라고도 함)은 또 다른 기술 용어입니다. 작성자로서 흥미를 느껴야 하는 이유는 무엇입니까?

헤드리스 애플리케이션에서 사용자 컨텐츠에 액세스하고 이를 사용하여 작업을 수행하려면 컨텐츠가 사전 정의된 구조를 가져야 합니다. 여러분의 컨텐츠가 자유형처럼 될 수 있지만, 그것은 생명을 만들 것입니다 *매우* 응용 프로그램에 대해 복잡합니다.

기본적으로 컨텐츠를 준수하기 위한 구조를 정의하는 과정에는 모델을 디자인하는 작업이 포함되며 이를 데이터 모델링이라고 합니다.

AEM의 경우 컨텐츠 설계자 역할(종종 다른 사람)은 데이터 모델링을 수행하여 다양한 **컨텐츠 조각 모델** - 을 사용하여 컨텐츠의 기반으로 사용할 수 있습니다. **컨텐츠 조각**.

>[!NOTE]
>
>데이터 모델링에 대해 자세히 알려면 AEM Headless Content Architect 여정 아래에서 자세히 읽어볼 수 있습니다.

## 다음 단계 {#whats-next}

개념과 용어를 학습했으므로 다음 단계는 다음과 같습니다 [컨텐츠 조각 작성에 대한 기본 사항을 알아봅니다](basics.md). 이렇게 하면 컨텐츠 조각을 작성하는 방법과 함께 AEM의 기본 처리가 도입됩니다.

## 추가 리소스 {#additional-resources}

* AEM Headless Developer 여정
   * [CMS 헤드리스 개발에 대해 알아보기](/help/journey-headless/developer/learn-about.md)

* [AEM 헤드리스 콘텐츠 설계 여정](/help/journey-headless/architect/overview.md)

* [AEM Headless 컨텐츠 번역 여정](/help/journey-headless/translation/overview.md)
