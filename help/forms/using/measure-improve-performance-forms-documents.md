---
title: 양식의 효율성 및 전환 측정 및 개선
description: AEM Forms은 양식의 성능 및 전환율을 측정하고 개선할 수 있도록 하는 Adobe Target 및 Adobe Analytics 솔루션과 통합됩니다.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: integrations
docset: aem65
exl-id: 4f45ad22-611b-4b4f-8e89-cb64a122b70a
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '1274'
ht-degree: 0%

---

# 양식의 효율성 및 전환 측정 및 개선{#measure-and-improve-effectiveness-and-conversion-of-forms}

## 과제 {#the-challenge-br}

조직에서는 고객이 여러 채널에서 디지털 셀프서비스를 사용하여 트랜잭션을 수행할 수 있도록 권한을 부여하고 장려하고 있습니다. 그러나 일대일 피드백 메커니즘이 없는 경우 고객 경험을 향상시키고 전환을 늘리기 위해 디지털 양식으로 성공을 측정하고 실험하는 것은 어려워집니다.

ROI를 극대화하려면 조직은 고객이 서비스와 상호 작용하는 방법을 모니터링하고 디지털 아티팩트(양식)를 실험하여 고객 경험을 개선해야 합니다. 성공을 측정하고 개선 전략을 정의하려면 다음과 같은 질문에 대한 답변이 필요합니다.

* 얼마나 많은 고객이 내 양식에 액세스하거나 이를 사용하여 거래하려고 시도했습니까?
* 그들 중 몇 명이 성공적으로 거래를 완료했습니까?
* 얼마나 많은 사람들이 양식을 포기했을까요?
* 고객이 직면한 문제 영역은 무엇입니까?
* 어떤 변경 사항을 가져오고 무엇이 더 나은 전환을 초래하는지 어떻게 테스트합니까?

## 솔루션 {#the-solution}

AEM Forms은 와 통합됩니다. [Adobe Marketing Cloud](https://www.adobe.com/marketing-cloud.html) 솔루션 - [Adobe Analytics](https://www.adobe.com/marketing-cloud/web-analytics.html) 및 [Adobe Target](https://www.adobe.com/marketing-cloud/testing-targeting.html) - 양식 수행 방식을 모니터링하고 분석하는 데 도움이 되며 전환율을 높이는 경험을 실험하고 식별할 수 있습니다.

## 워크플로우 {#the-workflow}

성능을 측정하고 양식의 전환율을 개선하는 방법에 대한 자세한 내용을 살펴보겠습니다.

### 타겟 대상자 {#target-audience}

* 마케팅 전략 및 성공을 담당하는 비즈니스 사용자 및 분석가
* 인프라 및 솔루션 설치 및 유지 관리를 관리하는 IT 직원

### AEM Forms 구성 요소 및 관련 기능 {#aem-forms-components-and-features-involved}

* 적응형 양식
* Adobe Analytics과 통합하여 적응형 양식과의 고객 상호 작용 수집, 구성 및 보고
* Adobe Target과 통합하여 적응형 양식에 대한 A/B 테스트 실행

### 가정 {#assumptions}

* 이미 Adobe Marketing Cloud 계정이 있으며 Analytics 및 Target 솔루션에 등록되었습니다.
* 고객이 액세스할 수 있는 적응형 양식이 게시되었습니다.

### 워크플로우 단계 {#workflow-steps}

#### 1단계: AEM Forms에서 Analytics 및 Target 구성  {#step-configure-analytics-and-target-in-aem-forms-br}

**Analytics 구성**

양식과의 고객 상호 작용에 대한 심층적인 통찰력을 얻으려면 먼저 AEM Forms에서 Analytics를 구성해야 합니다. 다음 단계를 수행하십시오.

1. Adobe Analytics에서 보고서 세트 만들기
1. AEM에서 클라우드 서비스 구성 만들기
1. AEM에서 클라우드 서비스 프레임워크 만들기
1. AEM에서 AEM Forms Analytics 구성 서비스 구성
1. AEM의 양식에서 분석 활성화

자세한 단계는 를 참조하십시오. [적응형 양식에 대한 분석 및 보고서 구성](../../forms/using/configure-analytics-forms-documents.md).

**Target 구성**

적응형 양식에 대한 A/B 테스트를 만들고 실행하려면 의 설명에 따라 AEM Forms에서 Target을 구성합니다 [AEM Forms에서 Target 설정 및 통합](../../forms/using/ab-testing-adaptive-forms.md#p-set-up-and-integrate-target-in-aem-forms-p).

#### 2단계: 분석 보고서 보기 {#step-view-analytics-report-br}

고객이 Analytics를 활성화한 양식에 액세스하고 상호 작용할 때 상호 작용이 보안성이 높은 Analytics 데이터베이스에서 캡처됩니다. 데이터베이스는 클라이언트별로 분할되며 보안 연결을 통해 액세스할 수 있습니다.

AEM 내에서 분석 지원 양식에 대한 보고서를 보고 데이터를 분석할 수 있습니다. 보고서를 보려면 다음 작업을 수행하십시오.

1. AEM 서버에서 다음으로 이동합니다. **Forms > Forms 및 문서**.
1. 분석 보고서를 작성할 양식을 선택합니다.
1. Analytics 보고서 아이콘을 클릭합니다. 보고서가 표시됩니다.

이제 Analytics에서 양식을 수집하고 보고하는 데이터 포인트를 살펴보겠습니다.

**Forms analytics 보고서**

적응형 양식에 대한 분석 보고서는 양식 수준에서 다음 주요 성과 지표(KPI)를 캡처합니다.

* **평균 채우기 시간**: 양식 작성에 소요된 평균 시간
* **노출 횟수**: 검색 결과에 양식이 표시된 횟수

* **표현물**: 양식을 렌더링하거나 연 횟수
* **초안**: 양식이 초안으로 저장된 횟수

* **제출**: 양식 제출 횟수
* **중단**: 사용자가 양식을 완료하지 않고 떠난 횟수
* **방문 횟수/제출**: 제출당 방문 비율

또한 양식의 각 패널에 대한 다음 세부 정보를 확인할 수 있습니다.

* **시간**: 패널 및 해당 필드에서 보낸 평균 시간(초)

* **오류**: 1000개의 양식 표현물당 패널 및 해당 필드에서 발생한 오류 수

* **도움말**: 1000개의 양식 표현물당 패널 및 해당 필드에 대한 컨텍스트 내 도움말에 사용자가 액세스한 횟수

![적응형 양식에 대한 샘플 분석 보고서](assets/summary-report.png)

Forms Analytics 보고서에 대한 자세한 내용은 [AEM Forms 분석 보고서 보기 및 이해](../../forms/using/view-understand-aem-forms-analytics-reports.md).

>[!NOTE]
>
>Adobe Marketing Cloud의 Analytics 계정에서 세부 보고서를 보고 고객 및 양식과의 상호 작용에 대한 자세한 통찰력을 얻을 수 있습니다.

#### 3단계: 데이터 포인트 분석 {#step-analyze-data-points}

이 단계에서는 분석 보고서에서 데이터 포인트를 분석하고 양식이 수행되는 방식을 추론합니다. 성공 KPI에 부합하지 않으면 데이터를 기반으로 가설을 구성하고 문제를 해결할 수 있는 해결책을 찾습니다. 예:

* 양식의 평균 채우기 시간이 예상보다 길면 양식이 고객이 이해하기 복잡하거나 양식에서 표준 용어를 사용하지 않거나 양식이 너무 길 수 있습니다. 이 경우 양식 구조 및 필드를 단순화하거나, 양식 디자인을 재작업하거나, 양식 길이를 줄이거나, 비표준 양식 필드에 대한 도움말 설명 및 예를 추가할 수 있습니다.
* 대부분의 고객이 양식 패널에 대한 도움말에 액세스하고 있음을 데이터가 나타내는 경우 고객이 어떤 정보를 채워야 할지 혼란스러워하는 것이 분명합니다. 대체 용어를 사용하거나 해당 패널에 대한 예제 입력 및 도움말 설명을 추가할 수 있습니다.
* 양식의 중단이나 포기 비율이 예상보다 높은 경우 양식을 렌더링하는 데 시간이 오래 걸리거나 고객이 실수로 양식에 도달하거나 양식이 너무 복잡하기 때문일 수 있습니다. 이 경우 검색 결과에 표시되는 양식 설명을 최적화하고, 양식을 단순화하고, 양식을 최적화하여 더 빠르게 로드할 수 있습니다.

이러한 데이터 포인트를 분석하고 가설에 도달하면 양식에 필요한 변경 내용을 적용합니다.

#### 4단계: 분석 및 수정 사항 유효성 검사 {#step-validate-your-analysis-and-fixes}

이 단계에서는 양식에서 변경한 내용을 확인하고 전환율에 영향을 주는지 확인합니다.

**A/B 테스트 실행**

Target과 AEM Forms의 통합을 통해 적응형 양식에 대한 A/B 테스트를 만들 수 있습니다. A/B 테스트에서는 더 잘 작동하거나 더 많은 전환을 일으키는 경험을 알기 위해 실시간으로 고객에게 양식의 다양한 경험을 무작위로 제시합니다. 한 경험이 다른 경험보다 나은 전환을 제공함을 나타내는 중요한 데이터가 있으면 해당 경험을 우승자로 선언할 수 있으며, 앞으로 모든 고객에게 표시되는 기본 경험이 됩니다.

적응형 양식에 대한 A/B 테스트 만들기에 대한 자세한 내용은 [적응형 양식의 A/B 테스트](../../forms/using/ab-testing-adaptive-forms.md).

![적응형 양식에 대한 A/B 테스트의 샘플 요약 보고서](assets/ab-test-report-4.png)

## 모범 사례 {#best-practices}

실제 모범 사례는 이 워크플로우를 수행하는 동안 자신을 식별하는 것입니다. 환경 및 요구 사항에 따라 다릅니다. 워크플로우를 통해 학습을 캡처하고 모범 사례로 문서화합니다.

양식 디자인 및 A/B 테스트 실행에 대한 몇 가지 권장 사항은 다음과 같습니다.

**Forms 디자인**

* 양식을 간단하고 짧고 쉽게 탐색할 수 있도록 유지합니다. 탐색에 방향 신호를 사용합니다.
* 양식 필드에 표준 또는 일반 용어를 사용합니다.
* 사용자가 헷갈릴 수 있는 필드 및 필수 입력 내용을 예시 또는 도움말과 함께 설명합니다.
* 사용자 입력이 입력할 때 양식 제출 시 오류를 방지하기 위해 가능하면 사용자 입력을 확인합니다.
* 데스크탑 및 모바일 장치용 레이아웃을 최적화합니다.
* 알려진 사용자에 대한 정보를 자동으로 채웁니다.

**A/B 테스트**

* A/B 테스트를 실행하기 전에 가설을 구성하고 성공 지표를 식별합니다.
* 대체 경험에서 최소 변형(이상적으로 한 번에 하나씩)을 수행하여 무엇이 전환율에 영향을 미쳤는지 확인합니다.
* 자주 테스트하여 비효율성을 제거합니다.
