---
title: We.Gov 참조 사이트 연습
seo-title: We.Gov 참조 사이트 연습
description: 가상 사용자 및 그룹을 사용하여 We.Gov 데모 패키지를 사용하여 AEM Forms 작업을 수행합니다.
seo-description: 가상 사용자 및 그룹을 사용하여 We.Gov 데모 패키지를 사용하여 AEM Forms 작업을 수행합니다.
uuid: 797e301a-36ed-4bae-9ea8-ee77285c786d
contentOwner: anujkapo
discoiquuid: ddb3778b-be06-4cde-bc6e-0994efa42b18
docset: aem65
translation-type: tm+mt
source-git-commit: 2cf9dcf2e9cf71c54e19e2c6ee825c9a8f00a9b7

---


# We.Gov 참조 사이트 연습{#we-gov-reference-site-walkthrough}

## 전제 조건 {#pre-requisites}

We.Gov 참조 사이트 설정 [및 구성에 설명된 대로 참조 사이트를](../../forms/using/forms-install-configure-gov-reference-site.md)설정합니다.

## 사용자 스토리 {#user-story}

* AEM 양식

   * 데이터 캡처
   * 데이터 통합(MS Dynamics)
   * Adobe Sign

* 워크플로우
* 고객 커뮤니케이션

   * 인쇄 채널
   * 웹 채널

* Adobe Analytics

### Fictitious users and groups {#fictitious-users-and-groups}

We.Gov 데모 패키지는 다음과 같은 내장 가상 사용자와 함께 제공됩니다.

* **탄야**:정부 기관에서 서비스 이용 가능 시민

![가상 사용자](/help/forms/using/assets/aya_tan_new.png)

* **조지 랑**:We.Gov 에이전시 비즈니스 애널리스트

![가상 사용자](/help/forms/using/assets/george_lang.png)

* **카밀라 산토스**:We.Gov 에이전시 CX 리드

![가상 사용자](/help/forms/using/assets/camila_santos.png)

다음 그룹도 포함됩니다.

* **We.Gov Forms 사용자**

   * George Lang(회원)
   * Camila Santos(회원)

* **We.Gov 사용자**

   * George Lang(회원)
   * Camila Santos(회원)
   * Aya Tan(회원)

### 데모 개요 범례 {#demo-overview-terms-legend}

1. **가장**:AEM 데모에서 정의된 사용자 및 그룹.
1. **단추**:탐색 시 색상이 지정된 사각형 또는 원 모양의 화살표
1. **클릭**:사용자 스토리에서 작업을 실행하려면
1. **링크**:We.Gov 사이트의 주 메뉴 상단에 있습니다.
1. **사용자 지침**:사용자의 스토리를 탐색할 때 따라야 할 일련의 숫자 단계입니다.
1. **양식 포털**: *https://&lt;aemserver>:&lt;port>/content/we-gov/formsportal.html*
1. **모바일 보기**:We.Gov 사용자는 크기가 다시 조정되는 브라우저로 모바일 보기를 복제할 수 있습니다.
1. **데스크탑 보기**:We.gov 사용자는 랩탑 또는 데스크탑에서 데모를 볼 수 있습니다.
1. **사전 입력기 양식**:We.Gov 사이트의 홈 페이지에 있는 양식입니다.
1. **적응형 양식**:Adobe.gov 데모를 위한 등록 신청 양식

   *https://&lt;aemserver>:&lt;port>/content/forms/af/adobe-gov-forms/enrollment-application-for-health-benefits.html*

1. **Adobe We.Gov 사이트**: *https://&lt;aemserver>:&lt;port>/content/we-gov/home.html*
1. **Adobe 받은 편지함**:AEM 백엔드의 상단 메뉴 [막대 Bell 아이콘](assets/bell.svg) 위치에 있습니다.

   *https://&lt;aemserver>:&lt;port>/aem/start.html*

1. **이메일 클라이언트**:이메일 보기 기본 설정(Gmail, Outlook)
1. **CTA**:클릭유도문안
1. **탐색**:브라우저 페이지에서 특정 참조점을 찾으려면

## 모바일 보기 데모 {#mobile-view-demo}

**이 조항은 시연 전에 행해져야 한다.**

**사용자 지침:**

1. 탐색: *https://&lt;aemserver>:&lt;port>/content/we-gov/home.html*
1. 다음으로 로그인:

   1. **사용자**:aya.tan
   1. **암호**:암호

1. 브라우저 창의 크기를 다시 조정하거나 브라우저의 에뮬레이터를 사용하여 모바일 장치 크기를 복제할 수 있습니다.

### Aya 사용자 스토리(We.Gov 웹 사이트) {#aya-user-story-we-gov-website}

![가상 사용자](/help/forms/using/assets/aya_tan_new-1.png)

**이 섹션**:아야는 시민입니다 지인으로부터 청으로부터 서비스를 받을 수 있다는 소식을 들었다. Aya는 휴대 전화로 We.Gov 웹 사이트로 이동하여 자격 조건을 충족하는 서비스에 대해 자세히 알아봅니다.

### Aya 사용자 스토리(We.Gov pre-screener) {#aya-user-story-we-gov-pre-screener}

Aya는 자신의 휴대폰에 간단한 적응형 양식을 기재함으로써 그녀의 자격 여부를 확인하기 위해 몇 가지 질문에 대답합니다.

**사용자 지침:**

1. 각 드롭다운 필드에서 선택합니다.

   >[!NOTE]
   >
   >사용자가 200,000달러/년 이상 수익을 내는 경우 해당 사용자는 자격 조건을 갖추지 못합니다.

1. &quot;**자격 조건&quot;을 클릭합니다.**” 단추.
1. &quot;지금&#x200B;**적용**&quot; 버튼을 클릭하여 계속합니다.

   ![지금 적용 링크](/help/forms/using/assets/apply_now_link.png)

### Aya 사용자 스토리(We.Gov 응용 양식) {#aya-user-story-we-gov-adaptive-form}

Aya는 자신이 자격 조건을 갖추었다는 것을 알게 되었고 자신의 모바일 장치에서 서비스를 요청하기 위해 신청서를 작성하기 시작했습니다.

Aya는 서비스 요청 애플리케이션을 완료하기 전에 집에서 일부 문서를 검토해야 합니다. 그녀는 지원서를 저장하고 종료합니다.

**사용자 지침:**

1. 기본 정보 필드를 채우면 필수 필드와 드롭다운이 있습니다.

   1. 기본 정보

      1. 이름
      1. 가운데 이름
      1. 성
      1. 기본 이름
      1. DOB
      1. 성별
   1. 연락처 정보

      1. 상세 주소
      1. 도시
      1. 전화 번호
      1. 우편 번호
      1. 이메일
      1. 상태
   1. 무술 상태

      1. 가족 상태



1. 다음 **동적 로직을** 사용하여 가족 상태 드롭다운을 사용하여 동적 기능을 **시연합니다** .

   1. **단일**:킨 패널 옆에 표시
   1. **기혼**:사용 가능한 종속 패널 표시
   1. **이혼**:킨 패널 옆에 표시
   1. **과부**:킨 패널 옆에 표시
   1. **아이가 있나요?**:(예/아니요) 라디오 단추를 클릭하여 하위 종속 패널을 표시합니다.

      1. (추가/제거) 단추를 클릭하여 여러 하위 종속 패널을 추가/제거합니다.

1. 회색 메뉴 모음에서 오른쪽 화살표를 클릭합니다.
1. 하단의 저장 단추를 클릭합니다.

   ![적응형 양식 세부 사항](/help/forms/using/assets/adaptive_form.png)

## 데스크탑 데모 {#desktop-demo}

**이 섹션:** 집에 돌아온 Aya는 필요한 정보를 발견했고 그녀의 데스크톱에서 응용 프로그램을 다시 열었습니다. 아야는 온라인 양식 포털로 이동하여 응용 프로그램을 다시 시작합니다. 일부 간단한 사용자 정의 기능을 사용하면 기관은 자동으로 링크를 생성하여 이메일로 전송하여 애플리케이션을 다시 시작할 수 있습니다.

### Aya 사용자 스토리(지속적인 적응형 양식) {#aya-user-story-continued-adaptive-form}

**사용자 지침:**

1. https://&lt; *aemserver>:&lt;port>/content/we-gov/home.html으로 이동합니다.*
1. 탐색 막대에서 &quot;온라인 서비스&quot;를&#x200B;**클릭합니다**.
1. &quot;양식 초안&quot; 패널에서 기존 &quot;건강 혜택을 위한 등록 신청&quot;을 선택합니다.

   ![건강 혜택을 위한 등록 신청](/help/forms/using/assets/enrollment_application.png)

   모양과 느낌은 동일하며 데이터를 다시 입력할 필요가 없습니다.

   **사용자 지침:**

1. 오른쪽 서클 CTA를 클릭하여 다음 섹션으로 이동합니다.

   ![RiRight 서클 CTA](/help/forms/using/assets/right_circle_cta_new.png)

   양식은 Aya의 마지막 항목 지점까지 채워집니다. Aya는 모든 정보를 입력했고 제출할 준비가 되었습니다.

   ![적응형 양식 제출](/help/forms/using/assets/submit_adaptive_form.png)

   Aya를 제출하면 Aya가 열리고 Adobe Sign을 사용하여 전자 서명할 준비가 된 전자 메일을 받게 됩니다.

**사용자 지침:**

1. 제출 후 감사 인사 페이지가 표시됩니다.
1. 이메일 클라이언트로 이동하여 Adobe Sign 이메일을 찾습니다.
1. Adobe Sign 링크를 클릭합니다.

   ![Adobe sign 링크](/help/forms/using/assets/adobe_sign_link.png)

**사용자 지침:**

1. &quot;동의함&quot;**상자를**&#x200B;선택합니다.
1. &quot;동의&quot;**를**&#x200B;클릭합니다.
1. 검토된 문서의 아래쪽으로 스크롤합니다.
1. 강조 표시된 노란색 탭을 클릭하여 문서에 서명합니다.

   ![문서](/help/forms/using/assets/sign_document_new.png) 서명 ![테스트 문서 서명](/help/forms/using/assets/sign_test_document.png)

## 공공 기관(George) {#government-agent-george}

![정부 요원 조지](/help/forms/using/assets/george_lang-1.png)

**이 섹션:** 조지는 정부 기관 Aya의 사업 분석가로 서비스를 요청하고 있습니다. George는 검토용으로 자신에게 지정된 모든 서비스 요청 응용 프로그램을 볼 수 있는 단일 대시보드를 가지고 있습니다.

### George 사용자 스토리(AEM 받은 편지함) {#george-user-story-aem-inbox}

**사용자 지침:**

1. https://&lt; *aemserver>:&lt;port>/aem/start.html으로 이동합니다.*
1. 사용자 아이콘(오른쪽 상단)을 클릭하고 현재 관리&#x200B;**사용자와**&#x200B;로그인한 경우 &quot;로그아웃&quot;**이나 &quot;가장**&#x200B;대상&quot; 메뉴 옵션을 사용합니다.

   1. 다음으로 로그인:

      1. **사용자:** george.lang
      1. **암호:** 암호
   1. 또는 가장:

      1. &quot;가장&#x200B;**대상**&quot; 필드에 &quot;**조지**&quot;를입력합니다.

      1. [확인]을 클릭하여 가장합니다.


1. 오른쪽 상단 모서리에서 알림(벨) 아이콘을 클릭합니다.
1. &quot;모두&#x200B;**보기**&quot;를 클릭하여 받은 편지함으로 이동합니다.
1. 받은 편지함에서 최신 &quot;Health Benefits Application **Review&quot; 작업을**&#x200B;엽니다.

   ![Health Benefits Application Review](/help/forms/using/assets/health_benefits.png)

### George 사용자 스토리(AEM 받은 편지함 및 MS Dynamics) {#george-user-story-aem-inbox-and-ms-dynamics}

데이터 통합 및 자동화된 워크플로우 덕분에 Aya의 애플리케이션이 데이터 전송 시 자동으로 생성된 CRM 레코드와 함께 나타납니다.

**사용자 지침:**

1. 읽기 전용 응용 양식을 열고 검사합니다.
1. &quot;MS Dynamics **열기**&quot; 버튼을 클릭하여 새 창에서 MS Dynamics 레코드를 엽니다.
1. CRM에서는 모든 정보를 업데이트할 수 있습니다

   1. 선택적으로 Dynamics에서 직접 검토 노트를 추가할 수 있습니다.

1. AEM 받은 편지함으로 닫고 돌아갑니다.

   ![MS Dynamics 레코드](/help/forms/using/assets/ms_dynamics.png)

### George 사용자 스토리(AEM 받은 편지함으로 돌아가기) {#george-user-story-back-to-aem-inbox}

George는 Aya의 응용 프로그램을 승인하며, 기존의 자동 워크플로 덕분에 확인 이메일도 Aya로 전송됩니다.

**사용자 지침:**

1. 왼쪽 상단 모서리로 이동하고 &quot;승인&quot;**을**&#x200B;클릭하여 애플리케이션을 승인합니다.
1. 모달에서 CX 리드에 대한 메시지를 남길 수 있습니다.
1. 완료를 클릭합니다.
1. (시민 역할) Aya로 보낸 이메일을 보려면 이메일 클라이언트를 엽니다.

   ![Aya로 보낸 이메일 보기](/help/forms/using/assets/email_client.png)

## CX 리드(Camila) {#cx-lead-camila}

![Camila(CX 리드)](/help/forms/using/assets/camila_santos-1.png)

**이 섹션:** CX Lead 는 Aya 와 환영 전화 통화를 설정하여 승인 받은 공공 서비스 사용 방법을 설명합니다.

### Camila 사용자 스토리(AEM 받은 편지함 및 MS Dynamics) {#camila-user-story-aem-inbox-ms-dynamics}

**사용자 지침:**

1. https://&lt; *aemserver>:&lt;port>/aem/start.html으로 이동합니다.*
1. 사용자 아이콘(오른쪽 상단)을 클릭하고 현재 관리&#x200B;**사용자와**&#x200B;로그인한 경우 &quot;로그아웃&quot;**이나 &quot;가장**&#x200B;대상&quot; 메뉴 옵션을 사용합니다.

   1. 다음으로 로그인:

      1. **사용자**:카밀라.산토스
      1. **암호**:암호
   1. 또는 가장:

      1. &quot;가장&#x200B;**대상**&quot; 필드에 &quot;Camila&quot;**를**&#x200B;입력합니다.

      1. [확인]을 클릭하여 가장합니다.


1. 오른쪽 상단 모서리에서 알림(벨) 아이콘을 클릭합니다.
1. &quot;모두&#x200B;**보기**&quot;를 클릭하여 받은 편지함으로 이동합니다.
1. 받은 편지함에서 최신 &quot;새 연락처 승인&quot;**작업을**&#x200B;엽니다.

   ![새 연락처 승인](/help/forms/using/assets/new_contact_approval.png)

   **사용자 지침:**

1. 읽기 전용 응용 양식을 열고 검사합니다.
1. &quot;MS Dynamics **열기**&quot; 버튼을 클릭하여 새 창에서 MS Dynamics 레코드를 엽니다.
1. CRM에서는 모든 정보를 업데이트할 수 있습니다

   1. 원할 경우, Dynamics에서 직접 새 호출 활동을 추가합니다.
   1. &quot;활동&quot;**섹션을**&#x200B;엽니다.
   1. &quot;새 전화&#x200B;**통화&quot; 옵션을**&#x200B;클릭합니다.
   1. 전화 통화 세부 사항을 추가합니다.
   1. 창을 저장하고 닫습니다.

1. AEM에서 왼쪽 상단 모서리로 이동하고 &quot;제출&quot;**을**&#x200B;클릭하여 애플리케이션을 제출합니다.
1. 모달에서 메시지를 남길 수 있습니다.
1. 완료를 클릭합니다.

   ![활동 탭](/help/forms/using/assets/activities_tab.png) 새 ![연락처 확인](/help/forms/using/assets/confirm_new_contact.png)

## 환영 키트 시민(Aya) {#welcome-kit-citizen-aya}

**이 섹션:** Aya는 자신의 이점에 대해 요약하고 채울 양식 필드를 포함하는 인터랙티브한 커뮤니케이션에 대한 링크가 포함된 이메일을 수신합니다. PDF 혜택 확인서를 첨부하고 인터랙티브한 커뮤니케이션과 동일한 테마/브랜딩을 사용하여 이메일에 연결할 수 있습니다.

### Aya 사용자 스토리(이메일 클라이언트) {#aya-user-story-email-client}

**사용자 지침:**

1. 환영 키트 이메일을 찾아 엽니다.
1. 페이지 아래쪽에 있는 PDF 첨부 파일로 스크롤합니다.
1. 을 클릭하여 PDF 첨부 파일을 엽니다.
1. 이메일 클라이언트에서 다시 스크롤하여 &quot;온라인&#x200B;**시작 키트 보기&quot;를**&#x200B;클릭합니다.

   1. 그러면 동일한 문서의 웹 채널 버전이 열립니다.

1. PDF에 직접 신속하게 참조하려면

   *https://&lt;aemserver>:&lt;port>/aem/formdetails.html/content/dam/formsanddocuments/adobe-gov-forms/welcome-handbook/we-gov-welcome-handbook*

1. IC에 대한 빠른 참조:

   *https://&lt;aemserver>:&lt;port>/content/dam/formsanddocuments/adobe-gov-forms/welcome-handbook/we-gov-welcome-handbook/jcr:content?channel=web&amp;mode=preview&amp;wcmmode=disabled*

   ![환영 혜택 핸드북](/help/forms/using/assets/welcome_benefits_handbook.png) 인터랙티브 ![커뮤니케이션 링크](/help/forms/using/assets/interactive_communication.png)

## 갱신 알림 사용자(Aya) {#renewal-reminder-citizen-aya}

**이 섹션:** Camila는 또한 1년 후에 통신 미리 알림을 예약합니다. (자동화/실행 및 이메일을 위한 워크플로우 단계).

### Aya 사용자 스토리(이메일 클라이언트) {#aya-user-story-email-client-1}

**사용자 지침:**

1. 이메일 클라이언트로 이동합니다.
1. 갱신 알림 이메일을 찾아 엽니다.
1. &quot;새 응용&#x200B;**프로그램**&#x200B;제출&quot; 단추를 클릭하여 응용 양식을 엽니다.

   1. 이 섹션은 2단계에서 데이터를 미리 채울 수 있도록 의도적으로 비워 둡니다.
   ![갱신 알림 이메일](/help/forms/using/assets/renewal_reminder_email.png)

## Analytics CX 리드(Camila) {#analytics-cx-lead-camila}

**이 섹션:** Camila는 대시보드로 이동하여 서비스 요청 양식을 작성하고 포기하는 국민 %, 요청 제출에서 승인/거부 응답, 시민에게 보낸 혜택에 대한 관여 통계 등 공공 기관의 KPI를 확인할 수 있습니다.

### 카메라 리뷰 사이트 보고(Adobe.Gov Adobe Analytics) {#camila-reviews-sites-reporting-we-gov-adobe-analytics}

1. https://&lt; *aemserver>:&lt;port>/sites.html/content로 이동합니다.*
1. 사이트 페이지를 보려면 &quot;**AEM Forms We.Gov**&#x200B;사이트&quot;를 선택합니다.
1. 사이트 페이지(예: 홈) 중 하나를 선택하고 &quot;분석 및 권장&#x200B;**사항&quot;을**&#x200B;선택합니다.

   ![분석 및 권장 사항](/help/forms/using/assets/analytics_recommendation.jpg)

1. 이 페이지에는 AEM 사이트 페이지에 속하는 Adobe Analytics에서 가져온 정보가 표시됩니다(참고:이 정보는 Adobe Analytics에서 정기적으로 새로 고쳐지고 실시간으로 표시되지 않습니다.)

   ![Adobe Analytics 주요 지표](/help/forms/using/assets/analytics_key_metrics.jpg)

1. 3단계에서 액세스한 페이지 보기 페이지로 돌아가면 디스플레이 설정을 변경하여 &quot;목록 보기&quot;에서 항목을 볼 수&#x200B;**있습니다**.
1. &quot;보기&quot;**드롭다운 메뉴를**&#x200B;찾아 &quot;목록&#x200B;**보기&quot;를**&#x200B;선택합니다.

   ![보기 드롭다운 메뉴의 목록 보기](/help/forms/using/assets/list_view_view_dropdown.jpg)

1. 동일한 메뉴에서 &quot;설정&#x200B;**보기**&quot;를 선택하고 &quot;Analytics&quot; 섹션에서 표시할 열을&#x200B;**선택합니다**.

   ![열 표시 구성](/help/forms/using/assets/view_setting_analytics.jpg)

1. &quot;업데이트&quot;**를**&#x200B;클릭하여 새 열을 사용할 수 있도록 합니다.

   ![새 열 사용 가능](/help/forms/using/assets/new_columns_available.jpg)

### 카메라 검토 양식 보고(Adobe.Gov Adobe Analytics) {#camila-reviews-forms-reporting-we-gov-adobe-analytics}

1. 다음으로 이동

   *https://&lt;aemserver>:&lt;port>/aem/forms.html/content/dam/formsanddocuments/adobe-gov-forms*

1. &quot;건강&#x200B;**혜택을 위한 등록**&#x200B;애플리케이션&quot; 적응형 양식을 선택하고 &quot;분석 보고서&quot;**옵션을**&#x200B;선택합니다.

   ![건강 혜택을 위한 등록 신청](/help/forms/using/assets/analytics_report_benefits.jpg)

1. 페이지가 로드될 때까지 기다렸다가 Analytics 보고서 데이터를 봅니다.

   ![분석 보고서 데이터](/help/forms/using/assets/analytics_report_data_updated.jpg)

