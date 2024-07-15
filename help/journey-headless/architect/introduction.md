---
title: Adobe Experience Manager Headless 콘텐츠 설계 여정
description: Adobe Experience Manager의 강력하고 유연한 Headless 기능을 접해 보고 프로젝트 콘텐츠를 모델링하는 방법을 알아봅니다.
exl-id: 49ba0d6d-dde4-42e2-92fd-c7655c0eebc0
solution: Experience Manager, Experience Manager Sites
feature: Headless,Content Fragments
role: Admin, Architect,Data Architect
source-git-commit: 9a3008553b8091b66c72e0b6c317573b235eee24
workflow-type: tm+mt
source-wordcount: '720'
ht-degree: 83%

---

# AEM을 통한 Headless용 콘텐츠 모델링 - 소개 {#architect-headless-introduction}

[AEM Headless 콘텐츠 설계 여정](overview.md)의 이 부분에서는 Adobe Experience Manager(AEM)를 사용한 Headless 콘텐츠 전달을 위한 콘텐츠 모델링을 이해하는 데 필요한 (기본) 개념과 용어를 배울 수 있습니다.

이 문서는 Headless 콘텐츠 게재, AEM이 Headless를 지원하는 방법 및 콘텐츠를 Headless용으로 모델링하는 방법을 이해하는 데 도움이 됩니다. 문서를 읽고 나면

* Headless 콘텐츠 게재에 대한 기본적인 개념을 이해할 수 있습니다.
* AEM이 Headless 및 콘텐츠 모델링을 지원하는 방법을 파악할 수 있습니다.

## 목표 {#objective}

* **대상자**: 초급
* **목표**: Headless 콘텐츠 모델링과 관련된 개념 및 용어를 소개합니다.

## 전체 콘텐츠 게재 {#full-stack}

사용하기 쉬운 대규모 콘텐츠 관리 시스템(CMS)이 부상하면서 조직은 이를 중앙 위치로 사용하여 메시지, 브랜딩 및 커뮤니케이션을 관리합니다. CMS를 경험 관리의 중심점으로 사용하면 효율성이 개선되어 서로 다른 시스템에서 작업을 복제할 필요가 없습니다.

![클래식 전체 스택 CMS](/help/journey-headless/developer/assets/full-stack.png)

전체 스택 CMS에서 콘텐츠를 조작하는 모든 기능은 CMS에 있습니다. 시스템 기능은 CMS 스택의 다양한 구성 요소를 구성합니다. 전체 스택 솔루션은 장점이 많습니다.

* 유지 관리할 한 개의 시스템이 있습니다.
* 콘텐츠는 중앙 집중식으로 관리됩니다.
* 시스템의 모든 서비스가 통합됩니다.
* 콘텐츠 작성이 원활하게 이뤄집니다.

따라서 새 채널을 추가해야 하거나 새로운 경험 유형에 대한 지원이 필요한 경우 한 개(또는 그 이상)의 새 구성 요소를 스택에 삽입할 수 있고 한 위치에서만 변경할 수 있습니다.

![스택에 새 채널 추가](/help/journey-headless/developer/assets/adding-channel.png)

하지만 스택의 다른 항목을 조정하여 변경 사항을 수용해야 하므로 스택 종속성의 복잡성이 빠르게 나타납니다.

## Headless의 헤드 {#the-head}

모든 시스템의 헤드는 일반적으로 해당 시스템의 출력 렌더러이며, 보통 GUI 또는 기타 그래픽 출력 형식입니다.

Headless CMS에 대해 말하자면 CMS는 콘텐츠를 관리하고 소비자에게 지속적으로 전달합니다. 그러나 **콘텐츠**&#x200B;를 표준화된 방식으로만 제공하면 Headless CMS는 최종 출력 렌더링을 생략하고 사용 서비스에 대한 콘텐츠 **프레젠테이션**&#x200B;를 종료합니다.

![Headless CMS](/help/journey-headless/developer/assets/headless-cms.png)

AR 경험, 웹 샵, 모바일 경험, 프로그레시브 웹 앱(PWA) 등 소비 서비스는 Headless CMS에서 콘텐츠를 가져와 자체 렌더링을 제공합니다. 콘텐츠에 대한 자체 헤드를 처리합니다.

헤드가 생략되면 복잡성이 제거되어 CMS를 간소화합니다. 이렇게 하면 실제로 콘텐츠가 필요하고 해당 렌더링에 가장 적합한 서비스로 콘텐츠를 렌더링하는 책임이 이전되기도 합니다.

## 콘텐츠 모델링 {#content-modeling}

콘텐츠 모델링(데이터 모델링이라고도 함)이 전문분야이므로 Headless의 모델링 시 고려해야 할 사항은 무엇입니까?

Headless 애플리케이션이 콘텐츠에 액세스하고 관련 작업을 수행하려면 콘텐츠는 사전 정의된 구조를 갖추고 있어야 합니다. 콘텐츠를 자유 형식으로 유지할 수 있지만 애플리케이션 구조는 *매우* 복잡해질 수 있습니다.

AEM의 경우 콘텐츠 설계자는 콘텐츠 모델링을 수행하여 다양한 **콘텐츠 조각 모델**&#x200B;을 디자인합니다. 이는 콘텐츠 작성자가 콘텐츠를 보유한 **콘텐츠 조각**&#x200B;을 생성할 때 사용되는 구조를 정의합니다.

### 콘텐츠에 액세스 {#access-content}

이는 개발 세부 정보에 가깝지만 스토리텔링을 완성하는 데 흥미를 줄 수도 있습니다.

콘텐츠 조각 모델을 만들고 작성자가 이를 사용하여 콘텐츠를 생성한 후에는 Headless 애플리케이션이 이 콘텐츠에 액세스해야 합니다.

AEM(Adobe Experience Manager)은 AEM GraphQL API를 사용하여 콘텐츠 조각에 선택적으로 액세스하여 필요한 콘텐츠만 반환할 수 있습니다. API를 사용하여 개발자는 특정 콘텐츠를 선택하는 쿼리를 만들 수 있습니다. 이 선택 프로세스는 *사용자의* 콘텐츠 조각 모델을 기반으로 합니다.

즉, 프로젝트는 애플리케이션에 사용할 구조화된 콘텐츠의 Headless 게재를 실현할 수 있습니다.

## 다음 단계 {#whats-next}

이제 개념과 용어를 배웠으므로 다음 단계는 [콘텐츠 조각 모델을 사용하여 모델링의 기본 사항에 대해 알아보기](basics.md)입니다.

## 추가 리소스 {#additional-resources}

* AEM Headless 개발자 여정
   * [CMS Headless 개발에 대해 알아보기](/help/journey-headless/developer/learn-about.md)
   * [콘텐츠를 모델링하는 방법에 대해 알아보기](/help/journey-headless/developer/model-your-content.md)
* [AEM as a Headless CMS 소개](/help/sites-developing/headless/introduction.md)
* [AEM 개발자 포털](https://experienceleague.adobe.com/landing/experience-manager/headless/developer.html)
* [AEM의 Headless 튜토리얼](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/overview.html)
