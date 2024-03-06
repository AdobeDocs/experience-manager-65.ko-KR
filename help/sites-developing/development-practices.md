---
title: 개발 사례
description: Adobe Experience Manager에서 개발하기 위한 우수 사례입니다.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
exl-id: 65b2029e-03c9-4df4-8579-2b15dbee1035
source-git-commit: 9d497413d0ca72f22712581cf7eda1413eb8d643
workflow-type: tm+mt
source-wordcount: '617'
ht-degree: 0%

---

# 개발 사례{#development-practices}

## 완료(DoD)의 정의에 따른 작업 {#work-according-to-a-definition-of-done}

팀마다 &#39;완료&#39;가 의미하는 바에 대한 정의는 다르지만, 스토리가 받아들여지기 전에 이를 갖고 정의된 기준에 부합하는지 확인하는 것이 중요합니다.

팀에서 일반적으로 지정하는 몇 가지 기준은 다음과 같습니다.

* 형식을 위해 검토된 코드
* 댓글/Javadoc 추가됨
* 필요한 테스트 범위 수준 충족
* 단위 및 통합 테스트 통과
* QA 환경에서 확인됨
* 현지화 구현

잘 정의된 DoD가 없으면 많은 작업이 반쯤 진행되어 실제로 완성되는 것이 없는 상황에서 끝나기 쉽다.

### 코딩 및 포맷 규칙 정의 및 준수 {#define-and-adhere-to-coding-and-formatting-conventions}

들여쓰기 수준 및 공백과 같은 것은 중요하지 않은 것처럼 보일 수 있지만 적절한 형식의 코드를 사용하면 가독성과 유지 관리에 많은 도움이 됩니다. 규칙은 논의하고 팀으로 동의한 다음 코드에서 따라야 합니다.

### 높은 테스트 적용 범위를 목표로 합니다.  {#aim-for-high-test-coverage}

프로젝트 구현의 규모가 커짐에 따라 이를 테스트하는 데 필요한 시간도 늘어납니다. 좋은 테스트 범위 없이는 테스트 팀은 확장할 수 없으며 개발자는 결국 버그에 파묻힐 수 있습니다.

개발자는 요구 사항을 충족하는 프로덕션 코드 전에 실패한 단위 테스트를 작성하는 테스트 주도 개발(TDD)을 연습해야 합니다. QA는 시스템이 높은 수준에서 예상대로 작동할 수 있도록 자동화된 수락 테스트 세트를 만들어야 합니다.

Jackalope 및 Prosper와 같은 사용자 정의 프레임워크를 사용하여 JCR API를 조롱함으로써 개발자의 생산성을 보장하고 단위 테스트를 작성할 수 있습니다.

### 데모 준비 {#stay-demo-ready}

각 반복이 끝날 때 비즈니스에 데모를 통해 시스템을 사용할 수 있어야 합니다. 시스템을 데모 준비 상태로 유지하면 팀은 항상 프로덕션 준비의 반복에 놓이게 되며 기술적인 문제를 유지 관리 가능한 수준으로 유지할 수 있습니다.

### 지속적인 통합 환경 구현 및 사용 {#implement-a-continuous-integration-environment-and-use-it}

지속적인 통합 환경을 구현하면 단위 테스트와 통합 테스트를 쉽고 반복적으로 실행할 수 있습니다. 또한 개발 팀에서 배포를 분리하여 팀의 다른 부분이 보다 효율적으로 작업할 수 있도록 하고 보다 안정적이고 예측 가능한 배포를 만듭니다.

### 빌드 시간을 낮게 유지하여 개발 주기를 빠르게 유지 {#keep-the-development-cycle-fast-by-keeping-build-times-low}

단위 테스트를 실행하는 데 시간이 오래 걸리는 경우 개발자는 단위 테스트를 실행하지 않고 가치를 잃게 됩니다. 코드를 빌드하고 배포하는 데 시간이 오래 걸리는 경우 사람들이 이를 수행하는 빈도가 줄어듭니다. 짧은 빌드 시간을 우선 순위로 설정하여 테스트 범위 및 CI 인프라에 투자한 시간이 지속적으로 팀의 생산성을 높일 수 있도록 합니다.

### Sonar 및 기타 정적 코드 분석 도구를 미세 조정하고 보고서에 작동합니다. {#fine-tune-sonar-and-other-static-code-analysis-tools-and-act-on-their-reports}

코드 분석 도구는 유용할 수 있지만 이로 인해 보고서가 개발 팀에서 조치를 취하는 경우에만 유용합니다. 이러한 도구가 제공하는 분석을 미세 조정하지 않으면 이러한 도구가 생성하는 권장 사항은 관련이 없게 되고 가치를 잃게 됩니다.

### 소년 Scout 규칙 준수 {#follow-the-boy-scout-rule}

소년 Scout은 &quot;발견한 것보다 더 잘 내버려두라&quot;라는 규칙을 가지고 있습니다. 개발팀의 모든 구성원이 이 규칙을 준수하고 문제가 발생했을 때 무언가를 정리하는 한, 코드는 지속적으로 개선됩니다.

### YAGNI 기능 구현 방지 {#avoid-implementing-yagni-features}

YAGNI(You Are Gonna Not Gonna Need It) 기능은 현재 필요하지 않지만 향후 필요한 것이 있을 것으로 예상할 때 구현되는 기능입니다. 이상적으로, 우리는 오늘날 작동할 가장 간단한 것을 구현하고 시스템의 아키텍처가 시간이 지남에 따라 요구 사항을 충족하도록 지속적인 리팩터링을 사용해야 합니다. 이를 통해 중요한 사항에 집중하고 코드 오류 및 기능 크리프를 방지할 수 있습니다.
