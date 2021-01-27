---
title: 분석 및 보고서 구성
seo-title: 분석 및 보고서 구성
description: 적응형 양식, 적응형 문서 및 HTML5 양식을 사용하는 동안 사용자가 직면한 인터랙션 패턴과 문제를 발견하도록 Adobe Analytics을 구성하는 방법을 살펴볼 수 있습니다.
seo-description: 적응형 양식, 적응형 문서 및 HTML5 양식을 사용하는 동안 사용자가 직면한 인터랙션 패턴과 문제를 발견하도록 Adobe Analytics을 구성하는 방법을 살펴볼 수 있습니다.
uuid: ac5d1300-f303-40e8-a33e-4859a54ac10d
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: integrations
discoiquuid: 96a77980-4213-4779-a540-00905ea8f7e3
docset: aem65
translation-type: tm+mt
source-git-commit: 5aa2fe48578633cbe5e4324f9e956e1dbbdab8af
workflow-type: tm+mt
source-wordcount: '1533'
ht-degree: 1%

---


# 분석 및 보고서 구성{#configuring-analytics-and-reports}

AEM Forms은 게시된 양식 및 문서에 대한 성능 지표를 캡처하고 추적할 수 있는 Adobe Analytics과 통합되어 있습니다. 이러한 지표를 분석하기 위한 목표는 양식이나 문서를 보다 유용하게 만드는 데 필요한 변경 사항에 대한 데이터를 기반으로 현명한 결정을 내리는 것입니다.

>[!NOTE]
>
>AEM Forms의 분석 기능은 AEM Forms 추가 기능 패키지의 일부로 사용할 수 있습니다. Add-on 패키지 설치에 대한 자세한 내용은 [AEM Forms 설치 및 구성](../../forms/using/installing-configuring-aem-forms-osgi.md)을 참조하십시오.
>
>추가 기능 패키지 외에도 AEM 인스턴스에 대한 Adobe Analytics 계정 및 관리자 권한이 필요합니다. 솔루션에 대한 자세한 내용은 [Adobe Analytics](https://www.adobe.com/solutions/digital-analytics.html)을 참조하십시오.

## 개요 {#overview}

Adobe Analytics을 사용하면 적응형 양식, HTML5 양식 및 인터랙티브한 커뮤니케이션을 사용하는 동안 사용자가 직면하는 인터랙션 패턴과 문제를 찾아낼 수 있습니다. 기본적으로 Adobe 분석은 다음 매개 변수에 대한 정보를 추적하고 저장합니다.

* **평균 칠 시간**:양식을 채우는 데 걸린 평균 시간입니다.
* **표현물**:양식을 연 횟수입니다.
* **초안**:초안 상태에서 양식을 저장한 횟수입니다.
* **제출**:양식을 제출한 횟수입니다.
* **중단**:사용자가 양식을 작성하지 않고 나가는 횟수입니다.

Adobe Analytics을 사용자 정의하여 추가 매개 변수를 추가/제거할 수 있습니다. 이 보고서에는 위의 정보와 함께 HTML5 및 적응형 양식의 모든 패널에 대한 다음 정보가 포함되어 있습니다.

* **시간**:패널 및 패널 필드에서 보낸 시간입니다.
* **오류**:패널 및 패널 필드에서 발생한 오류 수입니다.
* **도움말**:사용자가 패널 및 패널 필드의 도움말을 연 횟수입니다.

## 보고서 세트 {#creating-report-suite} 만들기

분석 데이터는 보고서 세트라는 고객별 저장소에 저장됩니다. 보고서 세트를 만들고 Adobe Analytics을 사용하려면 유효한 Adobe Marketing Cloud 계정이 있어야 합니다. 다음 단계를 수행하기 전에 유효한 Adobe Marketing Cloud 계정이 있는지 확인하십시오.

보고서 세트를 만들려면 다음 단계를 수행하십시오.

1. [https://sc.omniture.com/login/](https://sc.omniture.com/login/)에 로그인합니다.
1. Marketing Cloud에서 **관리** > **Admin Console** > **보고서 세트**&#x200B;를 선택합니다.
1. 보고서 세트 관리자에서 **새로 만들기** > **보고서 세트**&#x200B;를 선택합니다.

   ![새 보고서 세트 만들기](assets/newreportsuite_new.png)

   새 보고서 세트 만들기

1. 첫 번째 드롭다운 목록이 **Create from a Template**&#x200B;으로 설정된 다음 **Commerce**&#x200B;를 선택합니다.
1. **보고서 세트 ID** 필드를 찾고 새 보고서 세트 ID를 추가합니다. 예: JJEsquire. 보고서 세트 ID가 보고서 세트 ID 필드 아래에 나타납니다. 여기에는 회사 이름인 자동 접두사가 포함됩니다.
1. 새 **사이트 제목**&#x200B;을 추가합니다. 예: JJEsquire Getting Started Suite. 이 제목은 Analytics UI 내에서 사용됩니다. 코드에서 보고서 세트 ID를 사용합니다.
1. 드롭다운에서 **시간대**&#x200B;를 선택합니다. 이 보고서 세트에 들어오는 모든 데이터는 정의된 시간대를 기준으로 기록됩니다.
1. **기본 URL** 및 **기본 페이지** 필드를 비워 두십시오. 이 두 값은 Adobe Marketing Cloud 인터페이스에서 웹 사이트에 연결하는 데만 사용됩니다.
1. **Go Live 날짜**&#x200B;를 오늘로 설정합니다. Go Live 날짜는 보고서 세트가 활성화된 날짜를 결정합니다.
1. **일별 예상 페이지 보기 횟수** 필드에 100을 입력합니다. 이 필드를 사용하여 일별 웹 사이트에 대해 예상되는 페이지 보기 횟수를 예상하십시오. 이 예상치를 통해 Adobe은 수집할 데이터를 처리하는 적절한 양의 하드웨어를 배치할 수 있습니다.
1. 드롭다운에서 **기본 통화**&#x200B;를 선택합니다. 이 보고서 세트에 들어오는 모든 통화 데이터는 변환되어 이 통화 형식으로 저장됩니다.
1. **보고서** 세트 만들기를 클릭합니다. 보고서 세트가 성공적으로 만들어졌다는 메시지와 함께 페이지 새로 고침을 볼 수 있습니다.
1. 새로 만든 보고서 세트를 선택합니다. **설정 편집** > **일반** > **일반 계정 설정**&#x200B;으로 이동합니다.

   ![일반 계정 설정](assets/geographic_settings.png)

   일반 계정 설정

1. 일반 계정 설정 화면에서 **지리 보고**&#x200B;를 활성화하고 **저장을 클릭합니다.**
1. **설정 편집** > **트래픽** > **트래픽 변수**&#x200B;로 이동합니다.
1. 보고서 세트에서 다음 트래픽 변수를 구성하고 활성화합니다.

   * **formName**:적응형 양식의 식별자입니다.
   * **formInstance**:적응형 양식 인스턴스의 식별자입니다. 이 변수에 대한 경로 보고서를 활성화합니다.
   * **fieldName**:적응형 양식 필드의 식별자입니다. 이 변수에 대한 경로 보고서를 활성화합니다.
   * **panelName**:적응형 양식 패널의 식별자입니다. 이 변수에 대한 경로 보고서를 활성화합니다.
   * **formTitle**:양식의 제목입니다.
   * **fieldTitle**:양식 필드의 제목입니다.
   * **panelTitle**:양식 패널의 제목입니다.
   * **analyticsVersion**:양식 분석 버전.

1. **설정 편집** > **전환** > **성공 이벤트**&#x200B;로 이동합니다. 다음 성공 이벤트를 정의하고 활성화합니다.

   | 성공 이벤트 | 유형 |
   |---|---|
   | 포기 | 카운터 |
   | render | 카운터 |
   | panelVisit | 카운터 |
   | fieldVisit | 카운터 |
   | save | 카운터 |
   | 오류 | 카운터 |
   | 도움말 | 카운터 |
   | 제출 | 카운터 |
   | timeSpent | 숫자 |

   >[!NOTE]
   >
   >AEM Forms 분석을 구성하는 데 사용되는 이벤트 번호 및 prop 번호는 [AEM analytics](/help/sites-administering/adobeanalytics.md) 구성에 사용된 이벤트 번호 및 prop 번호와 달라야 합니다.

1. Adobe Marketing Cloud 계정에서 로그아웃합니다.

## Cloud Service 구성 {#creating-cloud-service-configuration} 만들기

Cloud Service 구성은 Adobe Analytics 계정에 대한 정보입니다. 이 구성을 통해 Adobe Experience Manager(AEM)은 Adobe Analytics에 연결할 수 있습니다. 사용하는 각 Analytics 계정에 대해 별도의 구성을 만듭니다.

1. AEM 작성자 인스턴스에 관리자로 로그인합니다.
1. 왼쪽 위 모서리에서 **Adobe Experience Manager** > **도구** ![](/help/forms/using/assets/tools.png) > **Cloud Services** > **기존 Cloud Services**&#x200B;을 클릭합니다.
1. **Adobe Analytics** 아이콘을 찾습니다. **구성 표시**&#x200B;를 클릭한 다음 **[+]**&#x200B;를 클릭하여 새 구성을 추가합니다.

   처음 사용하는 사용자의 경우 **지금 구성**&#x200B;을 클릭합니다.

1. 새 구성에 제목을 추가합니다(이름 필드 채우기는 선택 사항). 예: 내 분석 구성. **만들기**&#x200B;를 클릭합니다.

1. 구성 페이지에서 [편집] 패널이 열리면 필드를 채웁니다.

   * **회사**:Adobe Analytics에 포함된 회사 이름입니다.
   * **사용자 이름**:Adobe Analytics에 로그인하는 데 사용되는 이름입니다.
   * **암호**:위 계정에 대한 Adobe Analytics 암호입니다.
   * **데이터 센터**:Adobe Analytics 계정의 데이터 센터.

1. **Analytics에 연결**&#x200B;을 클릭합니다. 연결이 성공적으로 수행되었다는 메시지가 포함된 대화 상자가 나타납니다. **확인**&#x200B;을 클릭합니다.

## Cloud Service 프레임워크 {#creating-cloud-service-framework} 만들기

Adobe Analytics 프레임워크은 Adobe Analytics 변수와 AEM 변수 간의 매핑 세트입니다. 프레임워크를 사용하여 양식에서 Adobe Analytics 보고서에 데이터를 채우는 방법을 구성합니다. 프레임워크는 Adobe Analytics 구성과 연결되어 있습니다. 각 구성에 대해 여러 프레임워크를 만들 수 있습니다.

1. AEM 클라우드 서비스 콘솔에서 Adobe Analytics 아래의 **구성 표시**&#x200B;를 클릭합니다.
1. Analytics 구성 옆에 있는 **[+]** 링크를 클릭합니다.

   ![Adobe Analytics 구성](assets/adobe-analytics-cloud-services.png)

   Adobe Analytics 구성

1. 프레임워크에 대해 **제목** 및 **이름**&#x200B;을 입력하고 **Adobe Analytics** 프레임워크를 선택하고 **만들기**&#x200B;를 클릭합니다. 편집을 위해 프레임워크가 열립니다.
1. 사이드 창의 보고서 세트 섹션에서 **항목 추가**&#x200B;를 클릭한 다음 드롭다운을 사용하여 프레임워크와 상호 작용할 보고서 세트 ID(예: JJEsquire)를 선택합니다.
1. 보고서 세트 ID 옆에서 정보를 보고서 세트로 보내려는 서버 인스턴스를 선택합니다.

   ![information_to_send_to_report_suite](assets/information_to_send_to_report_suite.png)

1. SideKick의 **기타** 범주의 **양식 분석 구성 요소**&#x200B;를 프레임워크로 드래그합니다.
1. Analytics 변수를 구성 요소에 정의된 변수와 매핑하려면 AEM Content Finder에서 추적 구성 요소의 필드로 변수를 드래그합니다.

   ![Adobe Analytics 변수를 사용하여 AEM 변수 매핑](assets/analytics_new.png)

1. 사이드 킥의 **페이지 탭**&#x200B;을 사용하여 프레임워크를 활성화하고 **프레임워크 활성화**&#x200B;를 클릭합니다.

## AEM Forms Analytics 구성 서비스 {#configuring-aem-forms-analytics-configuration-service} 구성

1. 작성자 인스턴스에서 AEM 웹 콘솔 구성 관리자를 `https://<server>:<port>;/system/console/configMgr`에 엽니다.
1. AEM Forms Analytics 구성 찾기 및 열기

   ![AEM Forms Analytics 구성 서비스](assets/analytics_configuration.png)

   AEM Forms Analytics 구성 서비스

1. 다음 필드에 적절한 값을 지정하고 **저장**&#x200B;을 클릭합니다.

   * **SiteCatalyst 프레임워크**:추적 프레임워크 설정 섹션에서 정의한 프레임워크/구성을 선택합니다.
   * **필드 시간 추적 기준**:필드 방문을 추적해야 하는 기간(초)을 지정합니다. 기본값은 0입니다. 값이 0(영)보다 크면 별도의 추적 이벤트 2개가 Adobe Analytics 서버로 전송됩니다. 첫 번째 이벤트는 분석 서버가 종료한 필드 추적을 중지하도록 지시합니다. 두 번째 이벤트는 지정된 기간이 지난 후에 전송됩니다. 두 번째 이벤트는 analytics 서버에 방문 필드 추적을 시작하도록 지시합니다. 두 개의 별도 이벤트를 사용하면 한 필드에서 보낸 시간을 정확하게 측정할 수 있습니다. 값이 0(영)이면 단일 추적 이벤트가 Adobe Analytics 서버로 전송됩니다.

   * **분석 보고서 동기화 cron**:Adobe Analytics에서 보고서를 가져올 cron 식을 지정합니다. 기본값은 0 0 2 ?*.

   * **보고서 가져오기 시간 초과: 서버가 분석 보고서에 응답할 때까지 기다릴 시간(초)을** 지정합니다. 기본 시간은 120초입니다.
   >[!NOTE]
   >
   >보고서 가져오기 작업을 시간 초과 수행한 다음 지정된 시간(초)에 최대 10초가 더 걸릴 수 있습니다.

1. 게시 인스턴스에서 1-3단계를 반복하여 분석을 구성합니다.

이제 양식에 대한 분석을 활성화하고 분석 보고서를 생성할 수 있습니다.

## 양식 또는 문서 {#enabling-analytics-for-a-form-or-document} 분석 활성화

1. `https://[hostname]:'port'`에 AEM 포털에 로그인합니다.
1. **Forms > Forms &amp; Documents**&#x200B;를 클릭하고 양식이나 문서를 선택한 다음 **Analytics 사용**&#x200B;을 클릭합니다. 분석이 활성화됩니다.

   ![양식 또는 문서에 대한 분석 활성화](assets/enable-analytics-1.png)

   양식에 대한 분석 활성화

   **A.** 분석 활성화 단추  **B.** 선택한 양식

   양식 분석 보고서 보기에 대한 자세한 내용은 [AEM Forms 분석 보고서 보기 및 이해](../../forms/using/view-understand-aem-forms-analytics-reports.md)를 참조하십시오.

