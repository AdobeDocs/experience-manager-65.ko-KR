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
source-git-commit: d1da42d7274e9a4257b9e8effae2b754e0104aa4
workflow-type: tm+mt
source-wordcount: '2536'
ht-degree: 0%

---


# We.Gov 참조 사이트 연습 {#we-gov-reference-site-walkthrough}

## 전제 조건 {#pre-requisites}

We.Gov 참조 사이트 [설정 및 구성에 설명된 대로 참조 사이트를 설정합니다](../../forms/using/forms-install-configure-gov-reference-site.md).

## 사용자 스토리 {#user-story}

* AEM Forms

   * 자동 양식 변환
   * 작성
   * 양식 데이터 모델/데이터 소스

* AEM Forms

   * 데이터 캡처
   * (선택 사항) 데이터 통합(MS Dynamics)
   * (선택 사항) Adobe Sign

* 워크플로우
* 이메일 알림
* (선택 사항) 고객 커뮤니케이션

   * 인쇄 채널
   * 웹 채널

* Adobe Analytics
* 데이터 소스 통합

### Fictitious users and groups {#fictitious-users-and-groups}

We.Gov 데모 패키지는 다음과 같은 내장된 가상 사용자와 함께 제공됩니다.

* **가야 탄**:공공 기관의 서비스 자격 시민

![가상 사용자](/help/forms/using/assets/aya_tan_new.png)

* **조지 랑**:We.Gov 대행사 비즈니스 애널리스트

![가상 사용자](/help/forms/using/assets/george_lang.png)

* **카밀라 산토스**:We.Gov CX 리더

![가상 사용자](/help/forms/using/assets/camila_santos.png)

다음 그룹도 포함됩니다.

* **We.Gov Forms 사용자**

   * George Lang(회원)
   * Camila Santos(멤버)

* **We.Gov 사용자**

   * George Lang(회원)
   * Camila Santos(멤버)
   * Aya Tan(회원)

### 데모 개요 범례 {#demo-overview-terms-legend}

1. **가장**:AEM 데모에서 정의된 사용자 및 그룹
1. **단추**:탐색 시 색상이 지정된 사각형 또는 원 모양의 화살표
1. **다음을 클릭합니다**.사용자 스토리에서 작업을 실행하려면
1. **링크**:We.Gov 사이트의 주 메뉴 상단에 있습니다.
1. **사용자 지침**:사용자의 스토리를 탐색할 때 따라야 할 일련의 숫자 단계입니다.
1. **Forms 포털**: *https://&lt;aemserver>:&lt;port>/content/we-gov/formsportal.html*
1. **모바일 보기**: We.Gov 사용자는 크기가 다시 조정되는 브라우저로 모바일 보기를 복제할 수 있습니다.
1. **데스크탑 보기**:We.gov 사용자가 랩탑 또는 데스크탑에서 데모를 볼 수 있습니다.
1. **사전 화면 입력기 양식**:We.Gov 사이트의 홈 페이지에 있는 양식
1. **적응형 양식**:We.gov 데모를 위한 등록 신청 양식

   *https://&lt;aemserver>:&lt;port>/content/forms/af/adobe-gov-forms/enrollment-application-for-health-benefits.html*

1. **Adobe We.Gov 사이트**: *https://&lt;aemserver>:&lt;port>/content/we-gov/home.html*
1. **Adobe 받은 편지함**:AEM 백엔드의 상단 메뉴 [막대 Bell 아이콘](assets/bell.svg) 위치에 있습니다.

   *https://&lt;aemserver>:&lt;port>/aem/start.html*

1. **이메일 클라이언트**:이메일 보기 기본 설정(Gmail, Outlook)
1. **CTA**:클릭유도문안
1. **탐색**:브라우저 페이지에서 특정 참조점을 찾으려면
1. **AFC**:자동화된 Forms 변환

## 자동화된 Forms 전환(Camila) {#automated-forms-conversion}

**이 섹션**:CX Lead 의 Camila 에는 종이 기반 프로세스의 일부로 사용되었던 기존 PDF 기반 양식이 있습니다. 현대화된 작업의 일환으로 이 PDF 양식을 사용하여 최신 적응형 Forms을 자동으로 제작하고자 합니다.

### 자동화된 Forms 전환 - We.Gov(Camila) {#automated-forms-conversion-wegov}

1. https://&lt; *aemserver>:&lt;port>/aem/start.html으로 이동합니다.*

1. 다음으로 로그인:
   * **사용자**:카밀라.산토스
   * **암호**:암호
1. 메인 페이지에서 Forms > Forms 및 문서 > AEM Forms We.gov Forms > AFC를 선택합니다.
1. Camila는 PDF를 AEM Forms에 업로드합니다.

   ![양식 업로드](assets/aftia-upload-form.jpg)

1. 그런 다음 카밀라는 PDF 양식을 선택하고 자동 변환 **시작을** 클릭하여 전환 프로세스를 시작합니다. 양식을 변환한 경우 **변환** 덮어쓰기를 클릭해야 할 수 있습니다.

   >[!NOTE]
   >
   >AFC의 설정은 최종 사용자에 대해 미리 구성되므로 변경하지 말아야 합니다.

   * **선택 사항**:액세스 가능한 초마린 테마를 사용하려면 응용 양식 테마 지정을 클릭하고 옵션 목록에 나타나는 액세스 가능한 초마린 테마를 선택하면 됩니다.

   ![전환 시작](assets/aftia-start-conversion.jpg)

   ![초마린 테마](assets/aftia-upload-conversion-settings.jpg)

   전환 중에 완료 백분율이 표시됩니다. 상태가 [ **변환됨**] **으로** 표시되면 **출력** 폴더를 클릭하고 응용 양식을 선택한 다음 [편집]을 클릭하여 변환된 양식을 엽니다.

1. 카밀라는 그 양식에 대해 검토하고 모든 분야가 존재하는 것을 확실히 했다

   ![전환 검토](assets/aftia-review-conversion.jpg)

1. 카밀라 이후 양식 편집을 시작합니다. [루트 패널] > [편집](렌치) > [패널 레이아웃] 드롭다운 메뉴에서 [맨 위에 탭 선택] > [확인란 선택]을 선택합니다.

   ![속성 검토](assets/aftia-review-properties.jpg)

1. 이후 카밀라는 최종 결과물을 만들기 위해 필요한 모든 CSS와 필드 변경을 추가했다.

   ![CSS 추가](assets/aftia-add-css.jpg)

### 양식 데이터 모델 및 데이터 소스(Camila) {#data-sources}

**이 섹션**:문서를 변환하여 응용 양식을 생성했으면 Camila가 응용 양식을 데이터 소스에 연결해야 합니다.

1. Camila는 자동화된 Forms 전환 - We. [Gov에서 변환된 양식에서 속성을 엽니다](#automated-forms-conversion-wegov).

1. 그런 다음 Camila에서 양식 모델 > 양식 데이터 모델을 선택합니다. 드롭다운 > 옵션 목록에서 We.gov 등록 FDM을 선택합니다.

1. 저장 및 닫기 단추를 클릭합니다.

   ![FDM 선택](assets/aftia-select-fdm.jpg)

1. Camila가 **출력** 폴더를 클릭하고 적응형 양식을 선택하고 **편집을** 클릭하여 완료된 We.Gov 양식을 엽니다.
1. Camila가 응용 양식 필드를 선택하고 구성 아이콘 ![을 클릭합니다](assets/configure-icon.svg). 바인딩 참조(Bind Reference) 필드를 사용하여 양식 데이터 모델 엔티티 **로 바인딩을** 생성합니다. 적응형 양식의 모든 필드에 대해 이 단계를 반복합니다.

### 양식 접근성 테스트(Camila) {#form-accessibility-testing}

또한 Camila는 작성된 컨텐츠가 기업 표준에 따라 올바로 작성되고 완벽하게 액세스할 수 있는지 확인합니다.

1. Camila가 **출력** 폴더를 클릭하고 적응형 양식을 선택하고 미리 보기 **를** 클릭하여 완료된 We.Gov 양식을 엽니다.

1. Chrome 개발자 도구 내에서 감사 탭을 엽니다.

1. 적응형 양식의 유효성을 검사하기 위해 액세서빌러티 검사를 수행합니다.

   ![접근성 검사](assets/aftia-accessibility.jpg)

## 적응형 양식 모바일 보기 데모(Aya) {#mobile-view-demo}

**이 부분은 시연 전에 해야 한다.**

**사용자 지침:**

1. 탐색: *https://&lt;aemserver>:&lt;port>/content/we-gov/home.html*
1. 다음으로 로그인:

   1. **사용자**:aya.tan
   1. **암호**:암호

1. 브라우저 창의 크기를 다시 조정하거나 브라우저의 에뮬레이터를 사용하여 모바일 장치 크기를 복제할 수 있습니다.

### We.Gov 웹 사이트(Aya) {#aya-user-story-we-gov-website}

![가상 사용자](/help/forms/using/assets/aya_tan_new-1.png)

**이 섹션**:아야는 시민입니다 지인으로부터 공공 기관에서 서비스를 받을 수 있다는 소식을 듣는다. 아야는 휴대폰에서 We.Gov 웹 사이트로 이동하여 그가 가질 수 있는 서비스에 대해 더 많이 알아본다.

### We.Gov Pre-Screener (Aya) {#aya-user-story-we-gov-pre-screener}

Aya는 휴대폰에서 간단한 적응형 양식을 작성해 자신의 자격 여부를 확인하기 위해 몇 가지 질문에 대답한다.

**사용자 지침:**

1. 각 드롭다운 필드에서 선택합니다.

   >[!NOTE]
   >
   >사용자가 20만 달러/1년 이상 버는 경우 해당 사용자는 자격 조건을 갖추지 못합니다.

1. &quot;**자격 조건?**” 단추.
1. 계속하려면 &quot;**지금**&#x200B;적용&quot; 버튼을 클릭합니다.

   ![지금 적용 링크](/help/forms/using/assets/apply_now_link.png)

### We.Gov 응용 양식(Aya) {#aya-user-story-we-gov-adaptive-form}

Aya는 자신의 모바일 장치에서 서비스를 요청하기 위해 응용 프로그램을 채우기 시작합니다.

Aya는 서비스 요청 애플리케이션을 완료하기 전에 집에서 일부 문서를 검토해야 합니다. 모바일 디바이스에서 애플리케이션을 저장하고 종료합니다.

**사용자 지침:**

1. 기본 정보 필드를 채우면 필수 필드와 드롭다운이 있습니다.

   1. 기본 정보

      1. 이름
      1. 성
      1. DOB
      1. 이메일

1. 다음 **동적 논리** 기능을 사용하여 가족 상태 **드롭다운을 사용하여 동적 기능을 시연할 수 있습니다** .

   1. **단일**:킨 패널 옆에 표시
   1. **결혼한 사람**:사용 가능한 종속 패널 표시
   1. **이혼**:킨 패널 옆에 표시
   1. **과부**:킨 패널 옆에 표시
   1. **아이들이 있나요?**:(예/아니요) 라디오 단추를 클릭하여 하위 종속 패널을 표시합니다.

      1. (추가/제거) 단추를 클릭하여 여러 하위 종속 패널을 추가/제거합니다.

1. 회색 메뉴 모음에서 오른쪽 화살표를 클릭합니다.
1. 하단에 있는 저장 버튼을 클릭합니다.

   ![적응형 양식 세부 정보](/help/forms/using/assets/adaptive_form.png)

## 데스크탑 데모 {#desktop-demo}

**이 섹션:** 다시 가정으로 아야는 필요한 정보를 찾고 데스크탑에서 애플리케이션을 재개했다. Aya는 응용 프로그램을 재개하기 위해 온라인 양식 포털로 이동합니다. 몇 가지 간단한 사용자 정의 기능을 사용하면 기관은 자동으로 링크를 생성하여 이메일로 전송하여 애플리케이션을 다시 시작할 수 있습니다.

### 지속적인 응용 양식(Aya) {#aya-user-story-continued-adaptive-form}

**사용자 지침:**

1. https://&lt; *aemserver>:&lt;port>/content/we-gov/home.html으로 이동합니다.*
1. 탐색 막대에서 &quot;**온라인 서비스&quot;를**&#x200B;클릭합니다.
1. &quot;초안 Forms&quot; 패널에서 기존 &quot;건강 혜택을 위한 등록 신청&quot;을 선택합니다.

   ![건강 보험 가입 신청](/help/forms/using/assets/enrollment_application.png)

   모양과 느낌은 동일하며 어떤 데이터도 다시 입력할 필요가 없습니다.

   **사용자 지침:**

1. 오른쪽 서클 CTA를 클릭하여 다음 섹션으로 이동합니다.

   ![RiRight 서클 CTA](/help/forms/using/assets/right_circle_cta_new.png)

   양식은 Aya의 마지막 항목 지점까지 채워집니다. Aya는 모든 정보를 입력했고 제출할 준비가 되었다.

   ![적응형 양식 제출](/help/forms/using/assets/submit_adaptive_form.png)

   >[!NOTE]
   >
   >Aya가 전화 번호 필드를 채우면 대시, 공백 또는 하이픈 없이 연속적인 11자리 숫자로 채워야 합니다.

   Aya 제출 후 감사 페이지가 수신됩니다. 원할 경우, 그녀는 자신이 열어서 Adobe Sign과 전자 방식으로 기록 문서에 서명할 수 있는 이메일을 받게 될 것이다.

### 선택 사항:Adobe Sign(Aya) {#adobe-sign}

**사용자 지침:**

1. 이메일 클라이언트로 이동하여 Adobe Sign 이메일을 찾습니다.
1. Adobe Sign 링크를 클릭합니다.

   ![Adobe 서명 링크](/help/forms/using/assets/adobe_sign_link.png)

**사용자 지침:**

1. &quot;**I agree**&quot; 상자를 선택합니다.
1. &quot;**수락&quot;을**&#x200B;클릭합니다.
1. 검토한 문서의 맨 아래로 스크롤합니다.
1. 강조 표시된 노란색 탭을 클릭하여 문서에 서명합니다.

   ![문서](/help/forms/using/assets/sign_document_new.png) 서명 ![테스트 문서 서명](/help/forms/using/assets/sign_test_document.png)

## 정부 기관(George) {#government-agent-george}

![정부 요원 조지](/help/forms/using/assets/george_lang-1.png)

**이 섹션:** 조지는 정부 기관인 아야 사의 비즈니스 분석가로 로부터 서비스를 요청하고 있다. George는 검토용으로 자신에게 지정된 모든 서비스 요청 응용 프로그램을 볼 수 있는 하나의 대시보드를 가지고 있습니다.

### AEM 받은 편지함(George) {#george-user-story-aem-inbox}

**사용자 지침:**

1. https://&lt; *aemserver>:&lt;port>/aem/start.html으로 이동합니다.*
1. 사용자 아이콘(오른쪽 상단)을 클릭하고 현재 관리 사용자와 로그인한 경우 &quot;**로그아웃**&quot;이나 &quot;가장 대상&#x200B;****&quot; 메뉴 옵션을 사용합니다.

   1. 다음으로 로그인:

      1. **사용자:** george.lang
      1. **암호:** 암호
   1. 또는 가장:

      1. &quot;가장 대상&#x200B;**&quot; 필드에 &quot;**&#x200B;조지&#x200B;**&quot;**&#x200B;를입력합니다.

      1. 가장하려면 확인을 클릭합니다.


1. 오른쪽 상단 모서리에서 알림(벨) 아이콘을 클릭합니다.
1. &quot;**모두**&#x200B;보기&quot;를 클릭하여 받은 편지함으로 이동합니다.
1. 받은 편지함에서 최신 &quot;**Health Benefits Application Review**&quot; 작업을 엽니다.

   ![Health Benefits Application Review](/help/forms/using/assets/health_benefits.png)

### 선택 사항:AEM 받은 편지함 및 MS Dynamics(George) {#george-user-story-aem-inbox-and-ms-dynamics}

데이터 통합 및 자동화된 워크플로우 덕분에 Aya의 애플리케이션이 데이터 전송 시 자동으로 생성된 CRM 레코드와 함께 나타납니다.

**사용자 지침:**

1. 읽기 전용 응용 양식을 열고 검사합니다.
1. &quot;MS Dynamics **열기**&quot; 버튼을 클릭하여 새 창에서 MS Dynamics 레코드를 엽니다.
1. CRM에서는 모든 정보를 업데이트할 수 있습니다

   1. Dynamics에서 바로 검토 노트를 추가할 수도 있습니다.

1. AEM 받은 편지함으로 닫습니다.

   ![MS Dynamics 레코드](/help/forms/using/assets/ms_dynamics.png)

### AEM 받은 편지함으로 돌아가기(George) {#george-user-story-back-to-aem-inbox}

George는 Aya의 응용 프로그램을 승인하고, 기존의 자동 작업 과정 덕분에 확인 이메일도 Aya로 전송됩니다.

**사용자 지침:**

1. 왼쪽 상단 모서리로 이동하고 &quot;**승인**&quot;을 클릭하여 애플리케이션을 승인합니다.
1. 모달에서 CX 리드에 대한 메시지를 남길 수 있습니다.
1. 완료를 클릭합니다.
1. (시민 역할) Aya로 보낸 이메일을 보려면 이메일 클라이언트를 엽니다.

   ![Aya로 보낸 이메일 보기](/help/forms/using/assets/email_client.png)

## CX 리드(Camila) {#cx-lead-camila}

![Camila(CX 리드)](/help/forms/using/assets/camila_santos-1.png)

**이 섹션:** CX Lead는 Aya와 환영 전화 통화를 설정하여 자신이 승인한 정부 서비스의 사용 방법을 설명합니다.

### (선택 사항) AEM 받은 편지함 및 MS Dynamics {#camila-user-story-aem-inbox-ms-dynamics}

**사용자 지침:**

1. https://&lt; *aemserver>:&lt;port>/aem/start.html으로 이동합니다.*
1. 사용자 아이콘(오른쪽 상단)을 클릭하고 현재 관리 사용자와 로그인한 경우 &quot;**로그아웃**&quot;이나 &quot;가장 대상&#x200B;****&quot; 메뉴 옵션을 사용합니다.

   1. 다음으로 로그인:

      1. **사용자**:카밀라.산토스
      1. **암호**:암호
   1. 또는 가장:

      1. &quot;가장&#x200B;**으로**&quot; 필드에 &quot;**Camila&quot;를**&#x200B;입력합니다.

      1. 가장하려면 확인을 클릭합니다.


1. 오른쪽 상단 모서리에서 알림(벨) 아이콘을 클릭합니다.
1. &quot;**모두**&#x200B;보기&quot;를 클릭하여 받은 편지함으로 이동합니다.
1. 받은 편지함에서 최신 &quot;**새 연락처 승인**&quot; 작업을 엽니다.

![새 연락처 승인](/help/forms/using/assets/new_contact_approval.png)

**(선택 사항) 사용자 지침:**

1. 읽기 전용 응용 양식을 열고 검사합니다.
1. &quot;MS Dynamics **열기**&quot; 버튼을 클릭하여 새 창에서 MS Dynamics 레코드를 엽니다.
1. CRM에서는 모든 정보를 업데이트할 수 있습니다

   1. 원할 경우, Dynamics에서 직접 새 호출 활동을 추가합니다.
   1. &quot;**활동**&quot; 섹션을 엽니다.
   1. &quot;**새 전화 통화**&quot; 옵션을 클릭합니다.
   1. 전화 통화 세부 사항을 추가합니다.
   1. 창을 저장하고 닫습니다.

1. AEM에서 왼쪽 위 모서리로 이동하고 &quot;**제출**&quot;을 클릭하여 애플리케이션을 제출합니다.
1. 모달에서 메시지를 남길 수 있습니다.
1. 완료를 클릭합니다.

   ![활동 탭](/help/forms/using/assets/activities_tab.png) 새 ![연락처 확인](/help/forms/using/assets/confirm_new_contact.png)

## (선택 사항) 환영 키트 시민(Aya) {#welcome-kit-citizen-aya}

**이 섹션:** Aya는 자신의 이점을 요약하고 채울 양식 필드도 포함하는 인터랙티브한 커뮤니케이션에 대한 링크가 포함된 이메일을 수신합니다. PDF 혜택 명세서 및 인터랙티브한 커뮤니케이션과 동일한 테마/브랜딩 방식으로 이메일에 연결된 링크가 포함되어 있습니다.

### 이메일 클라이언트 알림(Aya) {#aya-user-story-email-client}

**사용자 지침:**

1. 환영 키트 이메일을 찾아 엽니다.
1. 페이지 하단에 있는 PDF 첨부 파일로 스크롤합니다.
1. 을 클릭하여 PDF 첨부 파일을 엽니다.
1. 이메일 클라이언트에서 다시 스크롤하고 &quot;**View welcome kit online**&quot;을 클릭합니다.

   1. 그러면 동일한 문서의 웹 채널 버전이 열립니다.

1. PDF에 직접 신속하게 참조하려면

   *https://&lt;aemserver>:&lt;port>/aem/formdetails.html/content/dam/formsanddocuments/adobe-gov-forms/welcome-handbook/we-gov-welcome-handbook*

1. IC에 대한 빠른 참조:

   *https://&lt;aemserver>:&lt;port>/content/dam/formsanddocuments/adobe-gov-forms/welcome-handbook/we-gov-welcome-handbook/jcr:content?channel=web&amp;mode=preview&amp;wcmmode=disabled*

   ![환영 혜택 핸드북](/help/forms/using/assets/welcome_benefits_handbook.png) ![인터랙티브한 커뮤니케이션 링크](/help/forms/using/assets/interactive_communication.png)

## 갱신 알림 사용자(Aya) {#renewal-reminder-citizen-aya}

**이 섹션:** 카밀라는 또한 1년 후에 통신 미리 알림을 예약합니다. (자동화/실행 및 이메일 워크플로우 단계).

### 이메일 클라이언트 알림(Aya) {#aya-user-story-email-client-updated}

**사용자 지침:**

1. 이메일 클라이언트로 이동합니다.
1. 갱신 알림 이메일을 찾아 엽니다.
1. &quot;새 애플리케이션&#x200B;**제출**&quot; 버튼을 클릭하여 적응형 양식을 엽니다.

   1. 이 섹션은 2단계 데이터 사전 채우기를 지원하기 위해 의도적으로 비워 둡니다.

   ![갱신 알림 이메일](/help/forms/using/assets/renewal_reminder_email.png)

## (선택 사항) 양식 데이터 모델(카메라) {#form-data-model}

**이 섹션**:Camila는 AEM Forms 데이터 통합으로 이동하여 빠른 테스트를 실행하여 양식 데이터 모델 통합을 통해 외부 데이터 소스로 전송된 정보가 실제로 존재하는지 확인할 수 있습니다.

### 양식 데이터 모델(카메라) {#form-data-model-camila}

**이 섹션**:Camila가 Data Sources 페이지로 이동하여 서버가 Derby 데이터베이스 내에서 복제한 데이터의 유효성을 확인합니다.

1. 사용자 환경이 완료되고 사용자 제출이 완료되면 Camila는 AEM Forms(**Forms** > **데이터 통합)의 데이터 소스 탭으로 이동합니다**.

1. 그런 다음 Camila가 AEM Forms **We.gov FDM을** 선택한 다음 **We.gov 등록 FDM을 편집합니다**.

1. 그런 다음 Camila가 테스트할 **연락처** > **서비스** 읽기를선택합니다.

   ![연락처 읽기 서비스](assets/aftia-contact-read-service.jpg)

1. 그런 다음 Camila는 테스트 서비스에 연락처 ID를 제공한 다음 테스트 단추를 클릭합니다. 예를 들어 양식을 제출한 경우 1 또는 2입니다. 양식을 제출하지 않은 경우 데이터가 반환되지 않습니다.

   ![연락처 읽기 서비스](assets/aftia-test-service.jpg)

1. 그러면 Camilla에서 데이터가 데이터 원본에 성공적으로 삽입되었는지 확인할 수 있습니다.

   * Derby DS 내의 데이터는 다음 형식과 유사합니다.

   ```xml
      [
         {
         "ADDRESS_COUNTRY": "USA",
         "LAST_NAME": "Tan",
         "ADDRESS_CITY": "New York",
         "FIRST_NAME": "Aya",
         "ADDRESS_STATE": "AL",
         "ADDRESS_LINE1": "123 Street crescent",
         "GENDER_CODE": "2",
         "ADDRESS_LINE2": "123 Street crescent",
         "ADDRESS_POSTAL_CODE": "90210",
         "BIRTH_DATE": "1991-12-12",
         "CONTACT_ID": 1,
         "MIDDLE_NAME": "M",
         "HAS_CHILDREN_CODE": "0"
         }
   ]
   ```

## (선택 사항) 분석(카메라) {#analytics-cx-lead-camila}

**이 섹션:** Camila는 공공 기관 KPI에서 볼 수 있는 대시보드로 이동합니다. 예를 들어 서비스 요청 양식을 작성하고 폐기하는 시민의 %, 요청 제출부터 승인/거부 응답, 시민에게 발송한 혜택에 대한 참여 통계 등 평균 시간을 확인할 수 있습니다.

### Adobe Analytics 사이트 보고(Camila) {#camila-reviews-sites-reporting-we-gov-adobe-analytics}

1. https://&lt; *aemserver>:&lt;port>/sites.html/content로 이동합니다.*
1. 사이트 페이지를 보려면 &quot;**AEM Forms We.Gov 사이트**&quot;를 선택합니다.
1. 사이트 페이지(예: 홈) 중 하나를 선택하고 &quot;**분석 및 Recommendations**&quot;을 선택합니다.

   ![분석 및 권장 사항](/help/forms/using/assets/analytics_recommendation.jpg)

1. 이 페이지에서는 AEM Sites 페이지와 관련된 Adobe Analytics의 가져오는 정보를 볼 수 있습니다(참고:이 정보는 주기적으로 Adobe Analytics에서 새로 고쳐지며 실시간으로 표시되지 않습니다.)

   ![Adobe Analytics 주요 지표](/help/forms/using/assets/analytics_key_metrics.jpg)

1. 3단계에서 액세스한 페이지 보기 페이지로 돌아가면 디스플레이 설정을 변경하여 &quot;**목록 보기&quot;에서 항목을 볼 수도**&#x200B;있습니다.
1. &quot;**보기**&quot; 드롭다운 메뉴를 찾아 &quot;**목록 보기&quot;를**&#x200B;선택합니다.

   ![보기 드롭다운 메뉴의 목록 보기](/help/forms/using/assets/list_view_view_dropdown.jpg)

1. 동일한 메뉴에서 &quot;설정&#x200B;**보기**&quot;를 선택하고 &quot;**분석**&quot; 섹션에서 표시할 열을 선택합니다.

   ![열 표시 구성](/help/forms/using/assets/view_setting_analytics.jpg)

1. &quot;**업데이트**&quot;를 클릭하여 새 열을 사용할 수 있도록 합니다.

   ![새 열 사용 가능](/help/forms/using/assets/new_columns_available.jpg)

### Adobe Analytics Forms 보고(Camila) {#camila-reviews-forms-reporting-we-gov-adobe-analytics}

1. 다음으로 이동

   *https://&lt;aemserver>:&lt;port>/aem/forms.html/content/dam/formsanddocuments/adobe-gov-forms*

1. &quot;**건강 혜택을 위한 등록**&#x200B;애플리케이션&quot; 적응형 양식을 선택하고 &quot;**분석 보고서**&quot; 옵션을 선택합니다.

   ![건강 보험 가입 신청](/help/forms/using/assets/analytics_report_benefits.jpg)

1. 페이지가 로드될 때까지 기다렸다가 Analytics 보고서 데이터를 봅니다.

   ![분석 보고서 데이터](/help/forms/using/assets/analytics_report_data_updated.jpg)

