---
title: 분석 및 보고서 구성
seo-title: Configuring analytics and reports
description: 적응형 양식, 적응형 문서 및 HTML5 양식을 사용하는 동안 사용자가 직면한 상호 작용 패턴 및 문제를 발견하도록 Adobe Analytics을 구성하는 방법에 대해 알아봅니다.
seo-description: Learn how to configure Adobe Analytics to discover interaction patterns and problems users face while using adaptive forms, adaptive documents, and HTML5 forms.
uuid: ac5d1300-f303-40e8-a33e-4859a54ac10d
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: integrations
discoiquuid: 96a77980-4213-4779-a540-00905ea8f7e3
docset: aem65
exl-id: 72f0f8e3-e70b-4f78-aa0e-b31768b536f7
source-git-commit: 66631fd0813f623f3321072fc00fd90f7fa33d21
workflow-type: tm+mt
source-wordcount: '1531'
ht-degree: 3%

---

# Cloud Service 프레임워크를 사용한 Analytics {#analyticsusingcloudframework}

AEM Forms은 Analytics와 통합되어 게시된 양식 및 문서에 대한 성능 지표를 캡처하고 추적할 수 있습니다. 이러한 지표를 분석하는 목적은 양식이나 문서를 보다 유용하게 만드는 데 필요한 변경 사항에 대한 데이터를 기반으로 정보에 입각한 결정을 내리는 것입니다.

>[!NOTE]
>
>AEM Forms의 분석 기능은 AEM Forms 추가 기능 패키지의 일부로 사용할 수 있습니다. 추가 기능 패키지 설치에 대한 자세한 내용은 [AEM Forms 설치 및 구성](../../forms/using/installing-configuring-aem-forms-osgi.md).
>
>추가 기능 패키지 외에도 AEM 인스턴스에 대한 Adobe Analytics 계정 및 관리자 권한이 필요합니다. 솔루션에 대한 자세한 내용은 [Adobe Analytics](https://www.adobe.com/solutions/digital-analytics.html).

Adobe Launch를 사용하여 분석을 수행할 수도 있습니다. AEM Forms을 Adobe Launch와 통합하는 방법에 대한 자세한 내용은 [Adobe Launch를 사용한 Analytics](/help/forms/using/integrate-aem-forms-with-adobe-analytics.md).

## 개요 {#overview}

Adobe Analytics을 사용하여 적응형 양식, HTML 5 양식 및 대화형 커뮤니케이션을 사용하는 동안 사용자가 직면한 상호 작용 패턴 및 문제를 발견할 수 있습니다. 기본적으로 Adobe 분석은 다음 매개 변수에 대한 정보를 추적하고 저장합니다.

* **평균 채우기 시간**: 양식을 채우는 데 걸린 평균 시간입니다.
* **표현물**: 양식 열기 횟수
* **초안**: 양식이 초안 상태로 저장된 횟수입니다.
* **제출**: 양식 제출 횟수.
* **중단**: 양식을 완료하지 않고 사용자가 나가는 횟수입니다.

Adobe Analytics을 사용자 지정하여 매개 변수를 더 추가하거나 제거할 수 있습니다. 위의 정보와 함께 보고서에는 HTML 5의 모든 패널과 적응형 양식에 대한 다음 정보가 포함되어 있습니다.

* **시간**: 패널 및 패널의 필드에서 보낸 시간.
* **오류**: 패널 및 패널의 필드에서 발생한 오류 수.
* **도움말**: 사용자가 패널 및 패널의 필드에 대한 도움말을 연 횟수입니다.

## 보고서 세트 만들기 {#creating-report-suite}

Analytics 데이터는 보고서 세트라는 고객별 저장소에 저장됩니다. 보고서 세트를 만들고 Adobe Analytics을 사용하려면 유효한 Adobe Marketing Cloud 계정이 있어야 합니다. 다음 단계를 수행하기 전에 유효한 Adobe Marketing Cloud 계정이 있는지 확인하십시오.

보고서 세트를 만들려면 다음 단계를 수행하십시오.

1. 에 로그인합니다 [https://sc.omniture.com/login/](https://sc.omniture.com/login/)
1. Marketing Cloud에서 **관리자** > **Admin Console** > **보고서 세트**.
1. 선택 **새로 만들기** > **보고서 세트** 보고서 세트 관리자에서.

   ![새 보고서 세트 만들기](assets/newreportsuite_new.png)

   새 보고서 세트 만들기

1. 첫 번째 드롭다운 목록이 **템플릿에서 만들기** 다음을 선택합니다. **상거래**.
1. 를 찾습니다. **보고서 세트 ID** 필드를 지정하고 새 보고서 세트 ID를 추가합니다. 예를 들어 JJEsquire입니다. 보고서 세트 ID는 보고서 세트 ID 필드 아래에 나타납니다. 자동 접두사가 포함되며, 이 접두사는 종종 회사 이름입니다.
1. 새로 추가 **사이트 제목**. 예를 들어 JJEsquire Getting Started Suite입니다. 이 제목은 Analytics UI 내에서 사용됩니다. 코드에서 보고서 세트 ID를 사용합니다.
1. 선택 **시간대** 드롭다운에서 을 클릭합니다. 이 보고서 세트로 들어오는 모든 데이터는 정의된 시간대를 기준으로 기록됩니다.
1. 나가기 **기본 URL** 및 **기본 페이지** 필드가 비어 있습니다. 이 두 값은 웹 사이트에 링크하기 위해 Adobe Marketing Cloud 인터페이스에서만 사용됩니다.
1. 나가기 **Go-Live 날짜** 오늘로 설정합니다. Go-Live 날짜는 보고서 세트가 활성화되는 날짜를 결정합니다.
1. 다음에서 **일별 예상 페이지 보기 수** 필드에 100을 입력합니다. 이 필드를 사용하여 하루에 웹 사이트에 대해 예상되는 페이지 조회수를 예상할 수 있습니다. 이 예상 값을 통해 Adobe은 수집 중인 데이터를 처리할 적절한 양의 하드웨어를 배치할 수 있습니다.
1. 선택 **기본 통화** 드롭다운에서 을 클릭합니다. 이 보고서 세트로 들어오는 모든 통화 데이터는 이 통화 형식으로 변환되고 저장됩니다.
1. 클릭 **보고서 만들기** 스위트. 보고서 세트가 성공적으로 생성되었다는 메시지와 함께 페이지 새로 고침이 표시됩니다.
1. 새로 생성된 보고서 세트를 선택합니다. 다음으로 이동 **설정 편집** > **일반** > **일반 계정 설정**.

   ![일반 계정 설정](assets/geographic_settings.png)

   일반 계정 설정

1. 일반 계정 설정 화면에서 다음을 활성화합니다 **지역 보고**, 및 클릭 **저장.**
1. 다음으로 이동 **설정 편집** > **트래픽** > **트래픽 변수**.
1. 보고서 세트에서 다음 트래픽 변수를 구성하고 활성화합니다.

   * **formName**: 적응형 양식에 대한 식별자.
   * **formInstance**: 적응형 양식 인스턴스 식별자. 이 변수에 대한 경로 보고서를 활성화합니다.
   * **fieldName**: 적응형 양식 필드 식별자. 이 변수에 대한 경로 보고서를 활성화합니다.
   * **panelName**: 적응형 양식 패널의 식별자. 이 변수에 대한 경로 보고서를 활성화합니다.
   * **formTitle**: 양식 제목
   * **필드 제목**: 양식 필드의 제목
   * **panelTitle**: 양식 패널의 제목
   * **분석 버전**: 양식 분석 버전.

1. 다음으로 이동 **설정 편집** > **전환** > **성공 이벤트**. 다음 성공 이벤트를 정의하고 활성화합니다.

   | 성공 이벤트 | 유형 |
   |---|---|
   | 중단 | 카운터 |
   | 렌더링 | 카운터 |
   | panelVisit | 카운터 |
   | fieldVisit | 카운터 |
   | 저장 | 카운터 |
   | 오류 | 카운터 |
   | 도움말 | 카운터 |
   | 제출 | 카운터 |
   | 체류 시간 | 숫자 |

   >[!NOTE]
   >
   >AEM Forms Analytics를 구성하는 데 사용되는 이벤트 번호 및 prop 번호는 에서 사용되는 이벤트 번호 및 prop 번호와 달라야 합니다. [AEM 분석](/help/sites-administering/adobeanalytics.md) 구성.

1. Adobe Marketing Cloud 계정에서 로그아웃합니다.

## Cloud Service 구성 만들기 {#creating-cloud-service-configuration}

Cloud Service 구성은 Adobe Analytics 계정에 대한 정보입니다. 이 구성을 통해 Adobe Experience Manager(AEM)가 Adobe Analytics에 연결할 수 있습니다. 사용하는 각 Analytics 계정에 대해 별도의 구성을 만듭니다.

1. 관리자로 AEM 작성자 인스턴스에 로그인합니다.
1. 왼쪽 상단 모서리에서 을(를) 클릭합니다 **Adobe Experience Manager** > **도구** ![](/help/forms/using/assets/tools.png) > **Cloud Services** > **이전 Cloud Services**.
1. 찾기 **Adobe Analytics** 아이콘. 클릭 **구성 표시** 그런 다음 을(를) 클릭하여 **[+]** 새 구성을 추가합니다.

   처음 사용하는 경우 **지금 구성**.

1. 새 구성에 제목 을 추가합니다(이름 필드 채우기는 선택 사항). 예: 내 분석 구성. **만들기**&#x200B;를 클릭합니다.

1. 구성 페이지에서 편집 패널이 열리면 다음 필드를 채웁니다.

   * **회사**: Adobe Analytics에 포함된 회사 이름.
   * **사용자 이름**: Adobe Analytics에 로그인하는 데 사용되는 이름입니다.
   * **암호**: 위 계정의 Adobe Analytics 암호입니다.
   * **데이터 센터**: Adobe Analytics 계정의 데이터 센터입니다.

1. 클릭 **Analytics에 연결**. 연결이 성공했다는 메시지가 표시된 대화 상자가 나타납니다. **확인**&#x200B;을 클릭합니다.

## Cloud Service 프레임워크 만들기 {#creating-cloud-service-framework}

Adobe Analytics 프레임워크는 Adobe Analytics 변수와 AEM 변수 간의 매핑 세트입니다. 프레임워크를 사용하여 양식이 데이터를 Adobe Analytics 보고서에 채우는 방법을 구성합니다. 프레임워크는 Adobe Analytics 구성과 연결됩니다. 각 구성에 대해 여러 프레임워크를 만들 수 있습니다.

1. AEM 클라우드 서비스 콘솔에서 을 클릭합니다. **구성 표시**, Adobe Analytics 아래에 있습니다.
1. 다음을 클릭합니다. **[+]** analytics 구성 옆에 있는 링크입니다.

   ![Adobe Analytics 구성](assets/adobe-analytics-cloud-services.png)

   Adobe Analytics 구성

1. Type a **제목** 및 **이름** 프레임워크에 대해 다음을 선택합니다. **Adobe Analytics** 프레임워크 및 클릭 **만들기**. 편집할 프레임워크가 열립니다.
1. 측면 Pod의 보고서 세트 섹션에서 을(를) 클릭합니다. **항목 추가**&#x200B;을 클릭한 다음 드롭다운을 사용하여 프레임워크가 상호 작용할 보고서 세트 ID(예: JJEsquire)를 선택합니다.
1. 보고서 세트 ID 옆에 있는 보고서 세트에 정보를 전송할 서버 인스턴스를 선택합니다.

   ![information_to_send_to_report_suite](assets/information_to_send_to_report_suite.png)

1. 드래그 **양식 분석 구성 요소** 다음에서 **기타** 카테고리로 사이드 킥을 프레임워크에 추가합니다.
1. Analytics 변수를 구성 요소에 정의된 변수와 매핑하려면 AEM Content Finder에서 추적 구성 요소의 필드로 변수를 드래그합니다.

   ![AEM 변수와 Adobe Analytics 변수 매핑](assets/analytics_new.png)

1. 를 사용하여 프레임워크 활성화 **페이지 탭** 사이드 킥에서 **프레임워크 활성화**.

## AEM Forms Analytics 구성 서비스 구성 {#configuring-aem-forms-analytics-configuration-service}

1. 작성자 인스턴스에서 다음 위치에서 AEM 웹 콘솔 구성 관리자를 엽니다. `https://<server>:<port>;/system/console/configMgr`.
1. AEM Forms Analytics 구성 찾기 및 열기

   ![AEM Forms Analytics 구성 서비스](assets/analytics_configuration.png)

   AEM Forms Analytics 구성 서비스

1. 다음 필드에 적절한 값을 지정하고 **저장**.

   * **SiteCatalyst 프레임워크**: 추적을 위한 프레임워크 설정 섹션에서 정의한 프레임워크/구성을 선택합니다.
   * **필드 시간 추적 기준선**: 필드 방문을 추적해야 하는 기간(초)을 지정합니다. 기본값은 0입니다. 값이 0보다 크면 두 개의 개별 추적 이벤트가 Adobe Analytics 서버로 전송됩니다. 첫 번째 이벤트는 Analytics 서버에 종료한 필드 추적을 중지하도록 지시합니다. 두 번째 이벤트는 지정된 기간이 지난 후에 전송됩니다. 두 번째 이벤트는 Analytics 서버에 방문한 필드 추적을 시작하도록 지시합니다. 두 개의 개별 이벤트를 사용하면 필드에서 보낸 시간을 정확하게 측정할 수 있습니다. 값이 0(영)이면 단일 추적 이벤트가 Adobe Analytics 서버로 전송됩니다.

   * **Analytics 보고서 동기화 cron**: Adobe Analytics에서 보고서를 가져오기 위한 cron 표현식을 지정합니다. 기본값은 0 0 2 입니다. &#42; &#42;.

   * **보고서 가져오기 시간 제한:** 서버가 분석 보고서에 응답할 때까지 대기할 기간(초)을 지정합니다. 기본 시간은 120초입니다.
   >[!NOTE]
   >
   >보고서 가져오기 작업을 시간 초과한 후 지정된 시간(초)까지 최대 10초가 더 걸릴 수 있습니다.

1. 게시 인스턴스에서 1-3단계를 반복하여 analytics를 구성합니다.

이제 양식에 대해 분석을 활성화하고 분석 보고서를 생성할 수 있습니다.

## 양식 또는 문서에 대한 분석 활성화 {#enabling-analytics-for-a-form-or-document}

1. 에서 AEM 포털에 로그인합니다. `https://[hostname]:'port'`.
1. 클릭 **Forms > Forms 및 문서**&#x200B;을 클릭하고 양식 또는 문서를 선택한 다음 **Analytics 활성화**. 분석이 활성화됩니다.

   ![양식 또는 문서에 대한 분석 활성화](assets/enable-analytics-1.png)

   양식에 대한 분석 활성화

   **A.** Analytics 활성화 단추 **B.** 선택한 양식

   Forms Analytics 보고서 보기에 대한 자세한 내용은 [AEM Forms 분석 보고서 보기 및 이해](../../forms/using/view-understand-aem-forms-analytics-reports.md).
