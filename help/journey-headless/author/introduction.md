---
title: Adobe Experience Manager을 사용하여 Headless 작성
description: Adobe Experience Manager의 강력하고 유연한 Headless 기능에 대한 소개와 프로젝트 콘텐츠를 작성하는 방법을 알아봅니다.
exl-id: 39d2218a-4f11-459d-8514-cfd312246be5
solution: Experience Manager, Experience Manager Sites
feature: Headless,Content Fragments
role: Admin, Architect,Data Architect,Developer,User,Leader
source-git-commit: 9a3008553b8091b66c72e0b6c317573b235eee24
workflow-type: tm+mt
source-wordcount: '649'
ht-degree: 87%

---

# AEM을 통한 Headless 작성 - 소개 {#author-headless-introduction}

[AEM Headless 콘텐츠 작성 여정](overview.md)의 이 부분에서는 Adobe Experience Manager(AEM)를 사용한 Headless 콘텐츠 게재를 위한 콘텐츠 작성을 이해하는 데 필요한 (기본) 개념과 용어를 배울 수 있습니다.

## 목표 {#objective}

* **대상자**: 초급
* **목표**: Headless 작성과 관련된 개념 및 용어를 소개합니다.

## 콘텐츠 관리 시스템(CMS) {#content-management-system}

콘텐츠 관리 시스템이란 무엇입니까?

콘텐츠 관리 시스템(CMS)은 소위 콘텐츠를 관리하는 데 사용되는 컴퓨터 시스템입니다. 보다 정확히 말하면 웹 사이트에서 사용할 수 있는 콘텐츠를 관리하는 데 (일반적으로) 사용됩니다.

## Headless CMS {#headless-cms}

Headless는 웹에 해당 콘텐츠를 표시하는 방식에서 사실상 콘텐츠를 분리하는 시스템을 설명하는 데 사용되는 용어입니다.

일반적으로 CMS에서 콘텐츠를 관리하고, 동일한 CMS는 웹 페이지의 해당 콘텐츠 렌더링을 담당합니다.

이제 Headless는 콘텐츠 세트를 CMS에서 관리한 다음 하나 이상의 (독립적인) 애플리케이션에서 액세스할 수 있음을 의미합니다.

즉, 콘텐츠를 다양한 형식으로 모든 디바이스에 게재할 수 있습니다. 이를 통해 전체 프로세스를 보다 유연하게 구성할 수 있고 레이아웃 및 서식에 대해 걱정할 필요는 없습니다.

>[!NOTE]
>
>Headless CMS의 기술 세부 사항에 대해 자세히 알아보려면 CMS Headless 개발에 대해 알아보기에서 자세한 내용을 확인할 수 있습니다.

## Adobe Experience Manager {#aem-cms}

그렇다면 AEM이란 무엇입니까?

무엇보다도 AEM은 요구 사항에 맞게 사용자 정의할 수 있는 다양한 기능을 갖춘 콘텐츠 관리 시스템입니다.

즉, 다음 경우로 사용할 수 있습니다.

* Headless CMS
   * Headless의 경우 콘텐츠를 **콘텐츠 조각**&#x200B;으로 작성할 수 있습니다.
이는 **콘텐츠 조각 모델**&#x200B;을 기반으로 사전 정의된 구조가 있는 다양한 애플리케이션을 통해 직접 액세스할 수 있는 자체 포함된 콘텐츠 항목입니다.
즉, 콘텐츠에서 다양한 형식과 기능으로 다양한 디바이스를 사용할 수 있습니다.
(문제가 발생하면 AEM 웹 페이지를 구성할 때도 이 조각이 필요한 경우 사용할 수 있습니다.)

* “기존” CMS
   * 웹 사이트에서 콘텐츠를 렌더링하는 방법을 정의하는 다양한 구성 요소를 사용하여 웹 페이지용 콘텐츠를 작성합니다. 여기서도 프로젝트 팀이 사용자 지정된 구성 요소를 개발할 수 있으므로 AEM이 매우 유연합니다.

## 콘텐츠 모델링 {#content-modeling}

따라서 콘텐츠 모델링(데이터 모델링이라고도 함)은 또 다른 기술 용어입니다. 작성자가 관심을 가져야 하는 이유는 무엇입니까?

Headless 애플리케이션이 콘텐츠에 액세스하고 관련 작업을 수행하려면 콘텐츠는 사전 정의된 구조를 갖추고 있어야 합니다. 콘텐츠를 자유 형식으로 유지할 수 있지만 애플리케이션 구조는 *매우* 복잡해질 수 있습니다.

기본적으로 콘텐츠에서 준수해야 할 구조를 정의하는 프로세스에는 데이터 모델링이라는 모델 디자인이 포함됩니다.

AEM의 경우 콘텐츠 설계자 역할(종종 다른 개인)이 데이터 모델링을 수행하여 다양한 **콘텐츠 조각 모델**&#x200B;을 디자인한 다음 **콘텐츠 조각**&#x200B;을 통해 콘텐츠의 기준으로 사용할 수 있습니다.

>[!NOTE]
>
>데이터 모델링에 대해 자세히 알아보려면 AEM Headless 콘텐츠 설계자 여정에서 자세히 확인할 수 있습니다.

## 다음 단계 {#whats-next}

이제 개념과 용어를 배웠으므로 다음 단계는 [콘텐츠 조각 작성의 기본 사항에 대해 알아보기](basics.md)입니다. 콘텐츠 조각을 작성하는 방법과 함께 AEM 기본 처리 방법을 소개합니다.

## 추가 리소스 {#additional-resources}

* AEM Headless 개발자 여정
   * [CMS Headless 개발에 대해 알아보기](/help/journey-headless/developer/learn-about.md)

* [AEM Headless 콘텐츠 설계자 여정](/help/journey-headless/architect/overview.md)

* [AEM Headless 콘텐츠 번역 여정](/help/journey-headless/translation/overview.md)

* [AEM as a Headless CMS 소개](/help/sites-developing/headless/introduction.md)

* [AEM 개발자 포털](https://experienceleague.adobe.com/landing/experience-manager/headless/developer.html?lang=ko)

* [AEM의 Headless 튜토리얼](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/overview.html?lang=ko)
