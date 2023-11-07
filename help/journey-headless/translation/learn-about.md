---
title: Headless 콘텐츠 및 AEM에서의 번역 방법에 대해 알아보기
description: Headless 개념, AEM에 매핑하는 방법 및 AEM 번역 이론에 대해 알아봅니다.
exl-id: cb2e2d89-e2d2-462f-8fff-b201847d0641
source-git-commit: fc2f26a69c208947c14e8c6036825bb217901481
workflow-type: tm+mt
source-wordcount: '757'
ht-degree: 94%

---

# Headless 콘텐츠 및 AEM에서의 번역 방법에 대해 알아보기 {#learn-about}

Headless 개념, AEM에 매핑하는 방법 및 AEM 번역 이론에 대해 알아봅니다.

## 목표 {#objective}

이 문서는 Headless 콘텐츠 게재, AEM이 Headless를 지원하는 방법 및 해당 콘텐츠가 번역되는 방법을 이해하는 데 도움이 됩니다. 문서를 읽고 나면

* Headless 콘텐츠 게재에 대한 기본적인 개념을 이해할 수 있습니다.
* AEM이 Headless 및 번역을 지원하는 방법을 파악할 수 있습니다.

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

AR 경험, 웹 샵, 모바일 경험, 점진적 웹 앱(PWA) 등과 같은 다양한 소비 서비스는 Headless CMS에서 콘텐츠를 가져와 자체 렌더링을 제공합니다. 콘텐츠에 대한 자체 헤드를 처리합니다.

헤드가 생략되면 복잡성이 제거되어 CMS를 간소화합니다. 이렇게 하면 실제로 콘텐츠가 필요하고 해당 렌더링에 가장 적합한 서비스로 콘텐츠를 렌더링하는 책임이 이전되기도 합니다.

## AEM의 Headless 사이트 콘텐츠 번역 {#translating-in-aem}

AEM은 강력한 도구를 통해 전체 스택 방식으로 기존 웹 페이지를 생성, 관리 및 전달하는 기능 외에도 자체 포함된 콘텐츠 선택 항목을 작성하여 Headless 방식으로 전달하는 기능을 제공하기도 합니다.

AEM의 강력한 도구를 통해 Headless 방식, 전체 스택 방식 또는 두 가지 모델로 콘텐츠를 동시에 전달할 수 있습니다. 번역 전문가는 동일한 번역 도구 세트를 두 가지 유형의 콘텐츠에 적용하여 통합된 방식으로 콘텐츠를 번역할 수 있습니다.

이후 여정에서는 AEM이 단계별로 콘텐츠를 번역하는 방법에 대한 자세한 내용을 알아봅니다. 단, 높은 수준의 개념은 간단합니다.

1. 번역 통합 프레임워크를 구성하여 번역 서비스와의 연결을 정의합니다.
1. 번역 규칙을 사용하여 번역할 콘텐츠를 정의합니다.
1. 콘텐츠를 수집할 번역 프로젝트를 만들어 번역 서비스로 전송하고 결과를 수신합니다.
1. 번역된 콘텐츠 검토하고 게시합니다.

## 다음 단계 {#what-is-next}

AEM Headless 번역 여정을 시작해 주셔서 감사합니다! 이 문서를 읽고 나면

* Headless 콘텐츠 게재에 대한 기본적인 개념을 이해할 수 있습니다.
* AEM이 Headless 및 번역을 지원하는 방법을 파악할 수 있습니다.

이 지식을 기반으로 다음 문서인 [AEM Headless 번역 시작하기](getting-started.md)를 검토하여 AEM Headless 번역 여정을 계속하십시오. 여기에서는 AEM이 Headless 콘텐츠를 관리하는 방법에 대한 개요를 살펴보고 번역 도구에 대해 알아보게 됩니다.

## 추가 리소스 {#additional-resources}

다음 문서인 [AEM Headless 번역 시작하기](getting-started.md)를 검토하여 Headless 번역 여정의 다음 부분으로 넘어가는 것이 좋습니다. 다음은 이 문서에 나열된 몇 가지 개념을 자세히 알아보는 추가적인 옵션 리소스이며, 이들 리소스를 Headless 여정에서 계속 사용할 필요는 없습니다.

* [MSM 및 번역](/help/sites-administering/msm-and-translation.md) - AEM의 다중 사이트 관리자에 대한 세부 정보 및 번역 도구 사용 방법
* [AEM as a Headless CMS 소개](/help/sites-developing/headless/introduction.md)
* [AEM 개발자 포털](https://experienceleague.adobe.com/landing/experience-manager/headless/developer.html)
* [AEM의 Headless 튜토리얼](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/overview.html)
