---
title: 양식의 효율성 측정 및 전환 개선
seo-title: 양식의 효율성 측정 및 전환 개선
description: AEM Forms은 Adobe Target 및 Adobe Analytics 솔루션과 통합되어 있으므로 양식의 성능 및 전환율을 측정하고 향상시킬 수 있습니다.
seo-description: AEM Forms은 Adobe Target 및 Adobe Analytics 솔루션과 통합되어 있으므로 양식의 성능 및 전환율을 측정하고 향상시킬 수 있습니다.
uuid: fd2f087c-39f5-457d-8b44-c3ec4400b3fc
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: integrations
discoiquuid: a128877d-239c-4272-99c2-72d6486d5703
docset: aem65
exl-id: 4f45ad22-611b-4b4f-8e89-cb64a122b70a
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1311'
ht-degree: 0%

---

# 양식{#measure-and-improve-effectiveness-and-conversion-of-forms}의 효율성 및 변환 측정 및 개선

## 과제 {#the-challenge-br}

조직에서는 고객이 여러 채널에서 디지털 셀프 서비스를 사용하여 거래하도록 권한을 부여하고 권장하고 있습니다. 그러나 일대일 피드백 메커니즘이 없는 경우 성공을 측정하고 디지털 양식을 실험하여 고객 경험을 향상하고 전환을 늘리는 것은 쉽지 않습니다.

ROI를 극대화하려면 고객이 서비스와 상호 작용하는 방법을 모니터링하고 디지털 아티팩트(양식)를 실험하여 고객 경험을 향상해야 합니다. 성공을 측정하고 개선을 위한 전략을 정의하려면 조직에서 다음과 같은 질문에 대한 답변을 필요로 합니다.

* 얼마나 많은 고객이 내 양식에 액세스하거나 양식으로 전송하려고 합니까?
* 얼마나 많은 사람들이 거래를 성공적으로 완료했습니까?
* 얼마나 많은 사람들이 그 양식을 포기했는가?
* 고객이 직면하고 있는 문제 영역은 무엇입니까?
* 가져올 수 있는 변경 사항과 더 나은 전환을 일으키는 항목을 테스트하는 방법은 무엇입니까?

## 솔루션 {#the-solution}

AEM Forms은 [Adobe Marketing Cloud](https://www.adobe.com/marketing-cloud.html) 솔루션 - [Adobe Analytics](https://www.adobe.com/marketing-cloud/web-analytics.html) 및 [Adobe Target](https://www.adobe.com/marketing-cloud/testing-targeting.html)과 통합됩니다. 이 기능을 통해 양식의 수행 방식을 모니터링하고 분석하여 전환율을 높이는 경험을 테스트하고 식별할 수 있습니다.

## 워크플로우 {#the-workflow}

성능을 측정하고 양식의 전환율을 향상시킬 수 있는 방법에 대한 세부 사항을 살펴보겠습니다.

### Target 대상 {#target-audience}

* 마케팅 전략 및 성공을 담당하는 비즈니스 사용자 및 분석가
* 인프라 및 솔루션 설치 및 유지 관리를 담당하는 IT 인력

### AEM Forms 구성 요소 및 관련 기능 {#aem-forms-components-and-features-involved}

* 적응형 양식
* 적응형 양식으로 고객 상호 작용을 수집, 구성 및 보고하기 위해 Adobe Analytics과 통합합니다
* 적응형 양식에 대한 A/B 테스트를 실행하도록 Adobe Target과 통합

### 가정 {#assumptions}

* 이미 Adobe Marketing Cloud 계정이 있고 Analytics 및 Target 솔루션에 등록되어 있습니다.
* 고객이 액세스할 수 있는 적응형 양식을 게시했습니다.

### 워크플로우 단계 {#workflow-steps}

#### 1단계:AEM Forms {#step-configure-analytics-and-target-in-aem-forms-br}에서 Analytics 및 Target 구성

**Analytics 구성**

양식을 사용한 고객 상호 작용에 대한 심도 있는 인사이트를 얻으려면 먼저 AEM Forms에서 Analytics를 구성해야 합니다. 다음 단계를 수행합니다.

1. Adobe Analytics에서 보고서 세트 만들기
1. AEM에서 클라우드 서비스 구성 만들기
1. AEM에서 클라우드 서비스 프레임워크 만들기
1. AEM에서 AEM Forms Analytics 구성 서비스 구성
1. AEM의 양식에서 분석 활성화

자세한 단계는 [적응형 양식에 대한 분석 및 보고서 구성](../../forms/using/configure-analytics-forms-documents.md)을 참조하십시오.

**Target 구성**

적응형 양식에 대한 A/B 테스트를 만들고 실행하려면 [AEM Forms에서 Target 설정 및 통합 설정에 설명된 대로 AEM Forms에서 Target을 구성하십시오](../../forms/using/ab-testing-adaptive-forms.md#p-set-up-and-integrate-target-in-aem-forms-p).

#### 2단계:Analytics 보고서 보기 {#step-view-analytics-report-br}

고객이 Analytics를 활성화한 양식에 액세스하고 상호 작용하면 고객의 상호 작용이 고도로 안전한 Analytics 데이터베이스에 캡처됩니다. 데이터베이스는 클라이언트에 의해 세그먼트화되고 보안 연결을 통해 액세스할 수 있습니다.

AEM 내에서 Analytics가 활성화된 양식을 보고 데이터를 분석할 수 있습니다. 보고서를 보려면 다음을 수행하십시오.

1. AEM 서버에서 **Forms > Forms 및 문서**&#x200B;로 이동합니다.
1. Analytics 보고서를 받을 양식을 선택합니다.
1. Analytics 보고서 아이콘을 클릭합니다. 보고서가 표시됩니다.

Analytics에서 양식에 대해 수집하고 보고하는 데이터 포인트를 살펴보겠습니다.

**Forms 분석 보고서**

적응형 양식에 대한 분석 보고서는 양식 수준에서 다음 주요 성과 지표(KPI)를 캡처합니다.

* **평균 채우기 시간**:양식 채우기에 걸린 평균 시간
* **노출 횟수**:검색 결과에 양식이 표시된 횟수입니다

* **표현물**:양식을 렌더링하거나 연 횟수입니다
* **초안**:양식을 초안으로 저장한 횟수입니다

* **제출**:양식을 제출한 횟수
* **중단**:사용자가 양식을 완료하지 않고 떠난 횟수입니다
* **방문/제출**:제출당 방문 비율

또한 양식의 각 패널에 대한 다음 세부 정보가 제공됩니다.

* **시간**:패널 및 해당 필드에서 보낸 평균 시간(초)

* **오류**:1000개의 양식 변환당 패널 및 해당 필드에서 발생한 오류 수

* **도움말**:사용자가 1000개의 양식 변환당 패널 및 해당 필드에 대한 컨텍스트 내 도움말에 액세스한 횟수입니다

![적응형 양식에 대한 샘플 분석 보고서](assets/summary-report.png)

Forms Analytics 보고서에 대한 자세한 내용은 [AEM Forms Analytics 보고서 보기 및 이해](../../forms/using/view-understand-aem-forms-analytics-reports.md)를 참조하십시오.

>[!NOTE]
>
>Adobe Marketing Cloud의 Analytics 계정에서 고객 및 양식과의 상호 작용에 대한 자세한 보고서를 보고 심층적인 통찰력을 얻을 수 있습니다.

#### 3단계:데이터 포인트 분석 {#step-analyze-data-points}

이 단계에서는 분석 보고서의 데이터 포인트를 분석하고 양식이 어떻게 작동하는지 유추하게 됩니다. 성공 KPI를 충족하지 않는 경우 데이터를 기반으로 가설을 만들고 가능한 해결 방법을 찾아 문제를 해결합니다. 예:

* 양식에 대한 평균 채우기 시간이 사용자의 예상보다 높은 경우 양식을 이해하는 것이 복잡하거나 양식이 표준 용어를 사용하지 않거나 양식이 너무 깁니다. 이 경우 양식 구조 및 필드를 단순화하고, 양식 디자인을 재작업하거나, 양식의 길이를 줄이거나, 비표준 양식 필드에 대한 도움말 설명 및 예를 추가할 수 있습니다.
* 데이터가 대부분의 고객이 양식 패널의 도움말에 액세스하고 있다고 표시하면 고객이 어떤 정보를 입력해야 하는지 의아해 하는 것이 분명합니다. 대체 용어를 사용하거나 해당 패널에 대한 예제 입력 및 도움말 설명을 추가할 수 있습니다.
* 양식의 중단 또는 포기 비율이 예상보다 높은 경우 양식을 렌더링하는 데 시간이 오래 걸리거나 고객이 실수로 양식에 도달했거나 너무 복잡할 수 있습니다. 이 경우 검색 결과에 표시되는 양식 설명을 최적화하고, 양식을 단순화하며, 양식을 빠르게 로드할 수 있도록 최적화하는 등의 작업을 수행할 수 있습니다.

이러한 데이터 포인트를 분석하고 가설에 도달하면 양식에서 필요한 변경 작업을 수행합니다.

#### 4단계:분석 유효성 검사 및 수정 사항 {#step-validate-your-analysis-and-fixes}

이 단계에서는 양식의 변경 사항에 대한 유효성을 확인하고 변경 내용이 전환율에 영향을 주는지 확인합니다.

**A/B 테스트 실행**

AEM Forms과 Target을 통합하면 적응형 양식에 대한 A/B 테스트를 만들 수 있습니다. A/B 테스트에서는 어떤 경험이 더 효과적인지 또는 더 많은 전환의 원인이 되는지 확인하기 위해 고객에게 양식의 다른 경험을 임의로 실시간 제공합니다. 한 경험이 다른 경험보다 나은 전환을 제공하는 경험을 나타내는 중요한 데이터가 있으면 해당 경험을 승자로 선언할 수 있으며, 앞으로는 모든 고객에게 표시되는 기본 경험이 됩니다.

적응형 양식에 대한 A/B 테스트를 만드는 방법에 대한 자세한 내용은 [적응형 양식](../../forms/using/ab-testing-adaptive-forms.md) A/B 테스트 를 참조하십시오.

![적응형 양식에 대한 A/B 테스트의 샘플 요약 보고서](assets/ab-test-report-4.png)

## 우수 사례 {#best-practices}

실제 우수 사례는 이 워크플로우를 수행할 때 자신을 식별하는 것입니다. 고객 환경과 요구 사항에 따라 다릅니다. 워크플로우를 통해 지식을 캡처하고 모범 사례로 문서화합니다.

양식 디자인 및 A/B 테스트 실행에 대한 몇 가지 권장 사항은 다음과 같습니다.

**Forms 디자인**

* 양식을 간단하고 짧고 쉽게 탐색할 수 있습니다. 탐색에 방향 큐를 사용합니다.
* 양식 필드에 표준 또는 공통 용어를 사용합니다.
* 사용자가 혼동될 수 있는 예제 또는 도움말을 사용하여 필드 및 필수 입력을 설명합니다.
* 입력할 때 사용자 입력의 유효성을 검사하여 양식 제출 시 오류를 방지합니다.
* 데스크탑 및 모바일 장치용 레이아웃을 최적화합니다.
* 알려진 사용자에 대한 정보를 자동으로 채웁니다.

**A/B 테스트**

* A/B 테스트를 실행하기 전에 가설을 작성하고 성공 지표를 확인합니다.
* 대체 경험에서 최소 변형(한 번에 하나씩)을 수행하여 전환율의 영향을 받은 사항을 파악합니다.
* 비효율성을 제거하기 위해 자주 테스트합니다.
