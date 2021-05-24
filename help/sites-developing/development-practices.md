---
title: 개발 사례
seo-title: 개발 사례
description: AEM 개발 우수 사례
seo-description: AEM 개발 우수 사례
uuid: 27a75f7f-6e2c-4113-9e9f-c5013a4594c2
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: 8b0297a1-d922-410f-9aaf-3a6b87e11dc0
exl-id: 65b2029e-03c9-4df4-8579-2b15dbee1035
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '637'
ht-degree: 0%

---

# 개발 사례{#development-practices}

## 완료 {#work-according-to-a-definition-of-done} 정의에 따라 작업

각 팀에는 &quot;완료&quot;가 의미하는 바에 대한 다른 정의가 있지만, 받아들여지기 전에 스토리가 정의된 기준을 충족하는지 확인하는 것이 중요합니다.

팀에서 일반적으로 지정하는 몇 가지 기준은 다음과 같습니다.

* 형식을 위해 검토된 코드
* 댓글/Javadoc 추가됨
* 필요한 테스트 범위 수준 충족
* 단위 및 통합 테스트를 통과합니다.
* QA 환경에서 검증됨
* 구현된 로컬라이제이션

잘 정의된 DoD가 없으면, 많은 일들이 타협하고 아무것도 정말로 완성되지 않는 상황에서 끝나는 것은 쉽습니다.

### 코딩 및 서식 규칙 {#define-and-adhere-to-coding-and-formatting-conventions} 을 정의하고 준수합니다.

들여쓰기 수준 및 공백 같은 것은 중요하지 않을 수 있지만 올바른 형식의 코드를 사용하는 것은 가독성과 유지 관리를 가능하게 하는데 큰 도움이 됩니다. 규칙은 팀으로서 토론하고 동의한 다음 코드에서 따라야 합니다.

### 높은 테스트 적용 범위 {#aim-for-high-test-coverage} 목표

프로젝트 구현의 크기가 커질수록 테스트하는 데 필요한 시간이 증가합니다. 좋은 검사 범위가 없다면, 테스트 팀은 규모를 확장할 수 없을 것이고 개발자들은 결국 버그에 묻힐 것이다.

개발자는 요구 사항을 충족하는 프로덕션 코드 앞에 결함이 있는 단위 테스트를 작성하여 TDD를 연습해야 합니다. QA에서는 시스템이 높은 수준에서 예상대로 작동하는지 확인하기 위해 자동화된 수락 테스트 세트를 만들어야 합니다.

단위 테스트를 작성하는 동안 개발자의 생산성을 보장하기 위해 JCR API를 더 간단하게 조롱할 수 있도록 Jackalope 및 Prospy와 같은 사용자 지정 프레임워크가 있습니다.

### 데모 준비 중 {#stay-demo-ready}

각 반복 종료 시 시스템에서 비즈니스 데모를 사용할 수 있습니다. 시스템을 데모 준비 상태로 유지하면 팀은 항상 프로덕션 준비 상태를 반복하고 기술 부채를 유지 관리할 수 있는 수준으로 유지할 수 있습니다.

### 연속 통합 환경을 구현하고 {#implement-a-continuous-integration-environment-and-use-it} 사용

지속적인 통합 환경을 구현하면 단위 테스트 및 통합 테스트를 쉽고 반복적으로 실행할 수 있습니다. 또한 개발 팀에서 여러 배포를 분리하여 팀의 다른 부분이 보다 효율적으로 사용할 수 있도록 하고 보다 안정적이고 예측 가능한 배포를 만들 수 있습니다.

### 빌드 시간을 {#keep-the-development-cycle-fast-by-keeping-build-times-low} 미만으로 유지하여 개발 주기를 빠르게 유지합니다

단위 테스트를 실행하는 데 시간이 오래 걸리는 경우 개발자가 단위 테스트를 실행하지 않으므로 값이 손실됩니다. 코드를 빌드하고 배포하는 데 시간이 오래 걸리면 사람들이 더 적게 수행합니다. 짧은 빌드 시간을 우선 순위로 설정하면 테스트 범위 및 CI 인프라에 투자한 시간이 계속해서 팀의 생산성을 높일 수 있습니다.

### Sonar 및 기타 정적 코드 분석 도구를 미세 조정하고 해당 보고서에 작동합니다 {#fine-tune-sonar-and-other-static-code-analysis-tools-and-act-on-their-reports}

코드 분석 도구는 유용할 수 있지만 보고서가 개발 팀의 작업에 이어지는 경우에만 유용합니다. 이러한 도구에서 제공하는 분석을 세밀하게 조정하지 않으면 생성되는 권장 사항은 관련성이 없으며 해당 가치를 잃게 됩니다.

### 소년 Scout 규칙 {#follow-the-boy-scout-rule}을 따르십시오

소년 Scout은 다음과 같은 규칙이 있습니다.&quot;당신이 찾은 것보다 더 잘 두세요.&quot; 개발팀의 모든 구성원이 이 규칙을 준수하고 엉망으로 나타날 때 무언가를 정리하는 한, 코드는 지속적으로 개선될 것입니다.

### YAGNI 기능 {#avoid-implementing-yagni-features} 구현 방지

YAGNI(또는 You Are Not Need It) 기능은 미래에 우리가 무언가를 필요로 할 것이라고 예상할 때 지금 당장 필요한 것이 아니더라도 구현되는 것입니다. 이상적으로는 현재 작동 중인 가장 간단한 작업을 구현하고 지속적인 리팩터링을 사용하여 시스템의 아키텍처가 시간이 지남에 따라 요구 사항을 충족하도록 해야 합니다. 따라서 중요한 사항에 집중할 수 있고 코드 블록과 기능 크리프를 방지할 수 있습니다.
