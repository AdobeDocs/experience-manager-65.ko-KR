---
title: 개발 사례
seo-title: 개발 사례
description: AEM에서 개발하는 우수 사례
seo-description: AEM에서 개발하는 우수 사례
uuid: 27a75f7f-6e2c-4113-9e9f-c5013a4594c2
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: 8b0297a1-d922-410f-9aaf-3a6b87e11dc0
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 개발 사례{#development-practices}

## 완료 정의에 따라 작업 {#work-according-to-a-definition-of-done}

각 팀은 &quot;완료&quot;가 의미하는 것에 대해 다른 정의를 가지지만, 수락되기 전에 스토리가 정의된 기준을 충족하는지 확인하는 것이 중요합니다.

팀에서 일반적으로 지정하는 몇 가지 기준은 다음과 같습니다.

* 서식을 위해 검토한 코드
* 댓글/Javadoc 추가됨
* 필수 테스트 범위 수준 충족
* 단위 및 통합 테스트를 통과합니다.
* QA 환경에서 검증됨
* 현지화 구현

잘 정의된 DoD가 없다면, 많은 것들이 중간 정도 행해지고 아무것도 실제로 완성되지 않는 상황에서 끝나는 것은 쉽습니다.

### 코딩 및 서식 지정 규칙 정의 및 준수 {#define-and-adhere-to-coding-and-formatting-conventions}

들여쓰기 수준 및 공백과 같은 기능은 중요하지 않을 수 있지만 올바른 형식의 코드를 사용하면 가독성과 유지 관리가 훨씬 수월해집니다. 규칙은 팀으로서 논의되고 동의되어야 하며, 그 다음 코드에서 따라야 합니다.

### 높은 테스트 지원 목표 {#aim-for-high-test-coverage}

프로젝트 구현의 크기가 커지면 테스트에 필요한 시간이 증가합니다. 충분한 테스트 기간이 없다면 테스트 팀은 규모를 조정할 수 없으며 개발자는 결국 버그에 묻힐 것입니다.

개발자는 요구 사항을 충족할 프로덕션 코드 전에 실패한 유닛 테스트를 작성하여 TDD를 실습해야 합니다. QA는 시스템이 높은 수준에서 예상대로 작동하는지 확인하기 위해 자동화된 수락 테스트 세트를 생성해야 합니다.

Jackalope 및 Prospy와 같은 사용자 정의 프레임워크를 사용하여 JCR API를 좀 더 쉽게 조롱하여 단위 테스트를 작성하는 동안 개발자의 생산성을 보장할 수 있습니다.

### 데모 준비 {#stay-demo-ready}

각 반복이 끝날 때 시스템에 대한 데모를 사용할 수 있어야 합니다. 시스템을 데모 준비 상태로 유지하면 팀은 항상 프로덕션 준비 상태를 유지할 수 있고 기술 빚은 유지 관리 가능한 수준으로 유지할 수 있습니다.

### 지속적인 통합 환경 구현 및 사용 {#implement-a-continuous-integration-environment-and-use-it}

지속적인 통합 환경을 구현하면 단위 테스트와 통합 테스트를 쉽고 반복적으로 실행할 수 있습니다. 또한 개발 팀의 배포를 분리하여 팀의 다른 부분을 보다 효율적으로 활용하고 보다 안정적이고 예측 가능한 배포를 수행할 수 있습니다.

### 빌드 시간을 줄여 개발 주기를 신속하게 유지 {#keep-the-development-cycle-fast-by-keeping-build-times-low}

단위 테스트를 실행하는 데 시간이 오래 걸리면 개발자는 단위 테스트를 실행하지 않고 가치를 잃게 됩니다. 코드를 작성하고 배포하는 데 시간이 오래 걸리면 더 적은 시간을 할애할 수 있습니다. 짧은 빌드 시간을 우선 사항으로 설정하면 테스트 범위 및 CI 인프라에 투자한 시간이 팀의 생산성을 계속 높일 수 있습니다.

### Sonar 및 기타 정적 코드 분석 툴을 세밀하게 조정하고 보고서에 따라 대응 {#fine-tune-sonar-and-other-static-code-analysis-tools-and-act-on-their-reports}

코드 분석 도구는 유용할 수 있지만, 보고서가 개발 팀의 일부에 대한 작업을 수행하는 경우에만 사용할 수 있습니다. 이러한 툴이 제공하는 분석을 세부적으로 조정하지 않으면, 이러한 툴이 생성하는 권장 사항은 관련성이 없으며 가치를 잃게 됩니다.

### 보이 스카우트 규칙 따르기 {#follow-the-boy-scout-rule}

보이스카우트에겐 다음과 같은 규칙이 있다.&quot;당신이 찾은 것보다 더 잘 두세요.&quot; 개발 팀의 모든 구성원이 이 규칙을 따르고 혼란을 겪을 때 무언가를 정리하는 한, 코드는 지속적으로 개선됩니다.

### YAGNI 기능 구현 방지 {#avoid-implementing-yagni-features}

YAGNI(또는 You Are Not Need It) 기능은 현재 필요하지는 않지만 미래에 무언가를 필요로 할 때 구현되는 기능입니다. 이상적으로, 우리는 오늘날 작동될 가장 간단한 것을 구현하고 지속적인 리팩토링을 사용하여 시스템의 아키텍처가 시간의 경과에 따라 요구 사항과 함께 발전하도록 해야 합니다. 따라서 중요한 사항에 집중할 수 있을 뿐만 아니라 코드 블록 및 기립 현상을 방지할 수 있습니다.
