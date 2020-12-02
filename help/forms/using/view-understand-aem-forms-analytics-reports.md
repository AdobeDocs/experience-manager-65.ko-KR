---
title: AEM Forms 분석 보고서 보기 및 이해
seo-title: AEM Forms 분석 보고서 보기 및 이해
description: AEM Forms은 Adobe Analytics과 통합되어 게시된 적응형 양식에 대한 요약 및 세부 분석을 제공합니다.
seo-description: AEM Forms은 Adobe Analytics과 통합되어 게시된 적응형 양식에 대한 요약 및 세부 분석을 제공합니다.
uuid: b15ba5f3-aea7-40f5-893e-aaf3834cbc33
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: integrations
discoiquuid: 3690fa80-6332-4df8-afea-77b5490fe0d1
docset: aem65
translation-type: tm+mt
source-git-commit: 317fadfe48724270e59644d2ed9a90fbee95cf9f
workflow-type: tm+mt
source-wordcount: '1075'
ht-degree: 0%

---


# AEM Forms 분석 보고서 보기 및 이해{#view-and-understand-aem-forms-analytics-reports}

Adobe Experience Manager Forms은 Adobe Analytics과 통합되어 있으므로 게시된 양식과 문서에 대한 성능 지표를 캡처하고 추적할 수 있습니다. 이러한 지표를 분석하기 위한 목표는 양식이나 문서를 보다 유용하게 만드는 데 필요한 변경 사항에 대한 데이터를 기반으로 현명한 의사 결정을 내리는 것입니다.

## 분석 설정 {#setting-up-analytics}

AEM Forms의 분석 기능은 AEM Forms 추가 기능 패키지의 일부로 사용할 수 있습니다. Add-on 패키지 설치에 대한 자세한 내용은 [AEM Forms 설치 및 구성](../../forms/using/installing-configuring-aem-forms-osgi.md)을 참조하십시오.

추가 기능 패키지 외에도 Adobe Analytics 계정이 필요합니다. 솔루션에 대한 자세한 내용은 [Adobe Analytics](https://www.adobe.com/solutions/digital-analytics.html)을 참조하십시오.

AEM Forms 추가 기능 패키지 및 Adobe Analytics 계정이 있으면 Adobe Analytics 계정을 AEM Forms과 통합하고 [분석 및 보고서 구성](../../forms/using/configure-analytics-forms-documents.md)에 설명된 대로 양식 또는 문서에 대한 추적을 활성화합니다.

### 사용자 상호 작용 정보가 기록된 방법 {#how-user-interaction-information-is-recorded}

사용자가 양식과 상호 작용하면 상호 작용이 기록되어 Analytics 서버로 전송됩니다. 다음 목록은 다양한 사용자 활동에 대한 서버 호출을 나타냅니다.

* 방문당 필드당 호출 2회
* 패널 방문
* 1개 비용 절감
* 2 제출
* 2 비용 절감
* 1 도움말
* 각 유효성 확인 오류에 대해 1
* 기본 패널 방문의 경우 양식 변환의 경우 1 + 기본 1의 필드 방문의 경우 1
* 2 양식 포기

>[!NOTE]
>
>이 목록은 완전하지 않다.

### 분석 보고서 보기 {#summary-report}

분석 보고서를 보려면 다음 단계를 수행합니다.

1. `https://[hostname]:'port'`에 AEM 포털에 로그인합니다.
1. **Forms > Forms 및 문서**&#x200B;를 클릭합니다.
1. 분석 보고서를 볼 양식을 선택합니다.
1. **자세히 > 분석 보고서**&#x200B;를 선택합니다.

![분석 보고서](assets/analyticsreport.png)

**A.** Analytics 보고서 명령

AEM Forms은 아래와 같이 양식과 각 패널에 대한 분석 보고서를 양식에 표시합니다.

![적응형 양식의 요약 보고서](assets/analyticsdashboard_callout.png)

**A.** B. **B.** 양식 수준 요약  **C.** C.Panel-Summary  **방문자 필터D.**   ****   **** D.Summary 브라우저방문자 필터E.E.방문자 필터F.필터 방문자 언어 -

기본적으로 지난 7일 동안의 분석 보고서가 표시됩니다. 지난 15일, 지난 1개월 등에 대한 보고서를 보거나 날짜 범위를 지정할 수 있습니다.

>[!NOTE]
>
>지난 7일 및 지난 15일과 같은 옵션에는 분석 보고서를 생성하는 날의 데이터가 포함되지 않습니다. 현재 날짜의 데이터를 포함하려면 현재 날짜를 포함한 날짜 범위를 지정한 다음 보고서를 실행해야 합니다.

![날짜 범위](assets/date-range.png)

### 응용 및 HTML5 양식에 대한 전환 그래프 {#conversions-graph-for-adaptive-and-html-forms}

양식 수준 전환 그래프는 다음과 같은 주요 성과 지표(KPI)에서 양식이 수행되는 방식에 대한 통찰력을 제공합니다.

* **표현물**:양식을 연 횟수
* **방문자**:양식의 방문자 수
* **제출**:양식을 제출한 횟수

![전환 그래프](assets/conversion-graph.png)

### 응용 및 HTML5 양식에 대한 분석 보고서 {#analytics-report-for-adaptive-and-html-forms}

양식 수준 요약 섹션에서는 다음과 같은 주요 성과 지표(KPI)에서 양식이 수행되는 방식에 대한 통찰력을 제공합니다.

* **평균 채우기 시간**:양식을 채우는 데 걸린 평균 시간입니다. 사용자가 양식에 시간을 할애하고 제출하지 않는 경우 이 계산에 해당 시간이 포함되지 않습니다.
* **표현물**:양식을 렌더링하거나 연 횟수
* **초안**:양식을 초안으로 저장한 횟수
* **제출**:양식을 제출한 횟수
* **중단**:사용자가 양식을 채우고 양식을 채우지 않고 떠난 횟수입니다
* **고유 방문자**:고유 방문자가 양식을 렌더링한 횟수입니다. 고유 방문자에 대한 자세한 내용은 [고유 방문자, 방문 및 고객 행동](https://helpx.adobe.com/analytics/kb/unique-visitors-visitor-behavior.html)을 참조하십시오.

![확장된 양식 수준 요약 분석 보고서](assets/analytics-report.png)

### 패널 보고서 {#bottom-summary-report}

패널 수준 요약 섹션은 양식의 각 패널에 대한 다음 정보를 제공합니다.

* **평균 채우기 시간**:양식이 전송되었는지 여부에 관계없이 패널에서 보낸 평균 시간
* **오류가 발생했습니다**.패널의 필드에 있는 사용자가 발생한 평균 오류 수입니다. 발견된 오류는 필드의 전체 오류를 양식의 표현물 수로 나누어 도달합니다.
* **액세스 도움말**:사용자가 패널의 필드에 대한 컨텍스트 내 도움말에 액세스한 평균 횟수입니다. 액세스한 도움말은 한 필드에 대한 도움말에 액세스한 총 횟수를 양식의 표현물 수로 나누어 도달합니다.

#### 세부 패널 보고서 {#detailed-panel-report}

패널 보고서에서 패널 이름을 클릭하여 각 패널의 세부 사항을 볼 수도 있습니다.

![자세한 패널 보고서](assets/panel-report-detailed.png)

세부 보고서에는 패널의 모든 필드에 대한 값이 표시됩니다.

패널 보고서에는 세 개의 탭이 있습니다.

* **시간 보고서**(기본값):패널의 각 필드를 채우는 데 걸린 시간(초)을 표시합니다.
* **오류 보고서**:필드를 채우는 동안 사용자가 발생한 오류 수를 표시합니다.
* **도움말 보고서**:특정 필드에 대한 도움말 액세스 횟수

여러 패널을 사용할 수 있는 경우 패널 간을 탐색할 수 있습니다.

### 필터:브라우저, OS 및 언어 {#filters-browser-os-and-language}

브라우저 배포, OS 배포 및 언어 배포 테이블에는 브라우저, OS 및 양식 사용자의 언어별로 변환, 방문자 및 제출이 표시됩니다. 이러한 표는 기본적으로 최대 5개의 항목을 표시합니다. 더 표시를 클릭하여 항목을 더 표시하고 덜 표시를 클릭하여 5개 이하의 정규 항목으로 돌아갈 수 있습니다.

분석 데이터를 추가로 필터링하려면 테이블의 항목을 클릭할 수 있습니다. 예를 들어 브라우저 배포 테이블에서 Google Chrome을 클릭하면 다음과 같이 Google Chrome 브라우저와 관련된 데이터로 보고서가 다시 렌더링됩니다.

![Analytics 보고서에 적용된 필터 - Google Chrome  ](assets/filter-1.png)

필터를 적용한 후 패널 보고서를 보는 경우 적용된 필터에 따라 패널 보고서 데이터도 표시됩니다.

필터가 적용되면:

* 한 번에 하나의 필터만 적용할 수 있으므로 배포 테이블이 읽기 전용이 됩니다.
* 적용된 필터 테이블이 사라집니다.
* 닫기 단추(아래에 강조 표시)를 클릭하여 적용된 필터를 제거할 수 있습니다.

![적용된 필터를 제거하려면 닫기 단추](assets/close-filter.png)

### A/B 테스트 {#a-b-testing}

A/B 테스트를 활성화하고 양식에 대해 설정한 경우 보고서 페이지에는 A/B 테스트 보고서를 표시하는 데 사용할 수 있는 드롭다운이 있습니다. A/B 테스트 보고서는 설정할 때 두 버전의 양식의 비교 성능을 표시합니다.

A/B 테스트에 대한 자세한 내용은 [적응형 양식에 대한 A/B 테스트 만들기 및 관리를 참조하십시오](../../forms/using/ab-testing-adaptive-forms.md).
