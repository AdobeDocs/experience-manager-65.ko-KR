---
title: 직원 채용 참조 사이트 연습
seo-title: 직원 채용
description: AEM Forms 참조 사이트에서는 조직이 AEM Forms 기능을 사용하여 직원 채용 워크플로우를 구현하는 방법을 소개하고 있습니다.
seo-description: AEM Forms 참조 사이트에서는 조직이 AEM Forms 기능을 사용하여 직원 채용 워크플로우를 구현하는 방법을 소개하고 있습니다.
uuid: 27e456ba-3c08-4c43-ad54-1ba0070995ad
topic-tags: introduction
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 5f04b13e-ea40-4c86-9168-e020c52435a2
translation-type: tm+mt
source-git-commit: af326f2d2b278fe36df05afc8c172f74c99a064c
workflow-type: tm+mt
source-wordcount: '1435'
ht-degree: 0%

---


# 직원 채용 참조 사이트 연습 {#employee-recruitment-reference-site-walkthrough}

## 개요 {#overview}

We.Finance는 지원자들이 참조 사이트 포털을 통해 취업신청을 할 수 있는 조직이다. 또한 이 조직은 포털에서 지원자의 인터뷰 일정, 단축 목록 및 내부 커뮤니케이션을 관리합니다. 사이트는 다음을 관리합니다.

* 구직 및 구직 지원자
* 후보자 심사 및 결격
* 면접 프로세스
* 후보 세부 정보 수집
* 후보 배경 확인
* 선택한 후보자에게 오퍼 롤아웃

>[!NOTE]
>
>직원 채용 사용 사례는 We.Finance 및 We.Gov 참조 사이트에서 모두 사용할 수 있습니다. 연습에서 사용되는 예제, 이미지 및 설명은 We.Finance 참조 사이트를 사용합니다. 그러나 이러한 사용 사례를 실행하고 We.Gov를 사용하여 결함을 검토할 수도 있습니다. 이렇게 하려면, 언급된 URL에서 **we-finance**&#x200B;을 **we-gov**&#x200B;로 바꾸십시오.

### 워크플로우 모델 관련 {#workflow-models-involved}

직원 채용 사용 사례에는 두 가지 워크플로우가 포함됩니다.

* 인터뷰 전 - We Finance 직원 채용 워크플로우
* 인터뷰 후 - We Finance Employee Recruiting Post Intermediation 워크플로우

이러한 워크플로우는 AEM에서 만들어지며 다음 위치에서 찾을 수 있습니다.

`https://[authorHost]:[authorPort]/libs/cq/workflow/admin/console/content/models.html/etc/workflow/models/`

#### We Finance 직원 채용 워크플로우 {#we-finance-employee-recruiting-workflow}

다음은 이 문서에 뒤따르는 We Finance 직원 채용 워크플로우의 모델입니다.

![we-finance-employee-recruiting-workflow](assets/we-finance-employee-recruiting-workflow.png)

#### We Finance Employee Recruitment Post Workflow {#we-finance-employee-recruiting-post-interview-workflow}

다음은 이 문서에 뒤따르는 We Finance 직원 사후 면접 워크플로우의 모델입니다.

![we-finance-employee-recruiting-post-intermediation-workflow](assets/we-finance-employee-recruiting-post-interview-workflow.png)

### 페르시아 {#personas}

The scenario contains the following personas:

* 그 조직에서 입사 지원자인 사라 로즈
* 채용 담당자 John Jacobs
* 채용 관리자 Gloria Rios
* John Doe, HR 담당자

## Sarah는 {#sarah-applies-for-a-job} 직업에 지원했다

새라 로즈는 이 조직에서 일자리 기회를 찾고 있다. 웹 포털을 방문하여 Career 페이지에 나열된 Job을 탐색합니다. 그녀는 적격한 취업 명단을 찾아 신청한다.

![홈 페이지](assets/home-page.png)

We.Finance 홈 페이지

![경력 페이지](assets/career-page.png)

We.Finance 경력 페이지

Sarah가 Job 게시물에서 Apply를 클릭합니다. 작업 응용 프로그램 양식이 열립니다. 그녀는 신청서에 있는 모든 세부사항을 기입해서 제출한다.

![job-application-form](assets/job-application-form.png)

### 작동 방식 {#how-it-works}

We.Finance 홈 페이지와 경력 페이지는 AEM Sites 페이지입니다. 경력 페이지에는 서비스를 사용하여 일자리 오프닝에 가져오고 페이지에 나열하는 반복 가능한 패널을 사용하는 적응형 양식이 포함됩니다. 응용 양식을 `https://[authorHost]:[authorPort]/editor.html/content/forms/af/we-finance/employee/recruitment/jobs.html`에서 검토할 수 있습니다.

### 직접 보기 {#see-it-yourself}

`https://[publishHost]:[publishPort]/content/we-finance/global/en.html`으로 이동하고 **[!UICONTROL Career]**&#x200B;를 클릭합니다. **[!UICONTROL 검색]**&#x200B;을 클릭하여 작업 목록을 채운 다음 작업을 위해 **[!UICONTROL 적용]**&#x200B;을 클릭합니다. 양식에 세부 사항을 입력하고 애플리케이션을 제출합니다.

이 연습을 통한 커뮤니케이션이 지정된 이메일 ID로 전송되므로 응용 프로그램에서 올바른 이메일 ID를 지정해야 합니다.

## 존 제이콥스 씨는 고용 관리자의 심사 {#john-jacobs-shortlists-sarah-rose-s-profile-for-the-hiring-manager-s-screening} 심사를 위해 사라 로즈의 프로필을 최종 선발한다.

그 조직은 사라가 제출한 취업 신청서를 받는다. 신병인 존 제이콥스는 사라의 프로필을 검토할 임무를 맡았다. 그는 AEM 받은 편지함에서 작업을 검토하고, 작업 요구 사항과 일치하는 프로파일을 찾은 다음, 바로 가기 목록을 클릭합니다. 사라의 프로필은 고용 관리자인 글로리아 리오스에게 그녀의 승인을 위해 보내졌다.

![jjacobs-inbox-1](assets/jjacobs-inbox-1.png)

John의 AEM 받은 편지함

![후보자 유격수](assets/candidate-shortlist.png)

존 제이콥스, 고용 매니저 선발 과정에서 사라 로즈의 프로필을 열거하다

**작동 방식**

직무 지원 양식의 제출 작업은 John Jacob의 받은 편지함에서 애플리케이션을 심사하기 위한 작업을 생성하는 워크플로우를 트리거합니다. John이 애플리케이션을 검토하고 바로 분류하면 워크플로우는 채용 관리자인 Gloria의 받은 편지함에 작업을 생성합니다.

### 직접 보기 {#see-it-yourself-1}

`https://[publishHost]:[publishPort]/content/we-finance/global/en/login.html?resource=/aem/inbox.html`으로 이동하여 John Jacobs의 사용자 이름/암호로 jjacobs/password를 사용하여 로그인합니다. 후보 프로필 검토 작업을 열고 지원자를 바로 나열합니다.

## Gloria는 지원서를 검토하고 지원자 면접을 승인합니다 {#gloria-reviews-the-application-and-approves-the-applicant-for-an-interview}

채용 관리자인 Gloria는 그녀의 AEM 받은 편지함에서 바로 등록 된 프로필을 받았습니다. 그녀는 그것을 검토하고 인터뷰를 위해 사라 로즈를 승인하였다.

![미화원](assets/gloriainbox.png)

글로리아의 AEM 받은 편지함

![영광스런 일정 인터뷰](assets/gloriaschedulesinterview.png)

글로리아, 사라 로즈 씨의 인터뷰 승인

**작동 방식**

Gloria가 지원자 면접을 승인하면 워크플로우는 We.Finance의 채용 담당자 John Doe의 AEM 받은 편지함에 작업을 만듭니다.

### 직접 보기 {#see-it-yourself-2}

`https://[publishHost]:[publishPort]/content/we-finance/global/en/login.html?resource=/aem/inbox.html`으로 이동하고 John Jacobs의 사용자 이름/암호로 jjacobs/password를 사용하여 로그인합니다. 후보 프로필 검토 작업을 열고 지원자를 바로 나열합니다.

`https://[publishHost]:[publishPort]/content/we-finance/global/en/login.html?resource=/aem/inbox.html`으로 가서 Gloria Rios의 사용자 이름/암호로 그리스/암호를 사용하여 로그인합니다. 후보 프로필 검토 작업을 열고 인터뷰 예약을 클릭합니다.

## John Doe가 {#john-doe-schedules-an-interview} 인터뷰를 예약합니다.

John Doe는 그의 받은 편지함에서 인터뷰를 예약하는 임무를 받습니다. John Doe는 작업을 선택하고 열고 면접 날짜와 시간, 위치, 그리고 인터뷰를 담당하는 HR 담당자를 존 제이콥으로 수정합니다. John Doe가 초대 이메일 전송을 클릭합니다. 사라에게 이메일이 보내지고, 사라를 인터뷰하기 위해 고용 매니저 글로리아에게 업무가 할당되었다.

![johnbosampinbox](assets/johnjacobsaeminbox.png)

John Doe의 AEM 받은 편지함

![johndoeschdule인터뷰](assets/johndoescheduleinterview.png)

John Doe는 인터뷰를 예약하고 자세한 내용을 사라 로즈에게 보냅니다

## Sarah Roz는 인터뷰 일정 {#sarah-rose-receives-the-email-with-interview-schedule}으로 이메일을 수신합니다.

Sarah Rose는 인터뷰 일정, 장소 및 기타 세부 정보가 있는 이메일을 받았다. 그녀는 면접 일정과 장소에서 괜찮다는 것을 보여주기 위해 수락을 클릭합니다. 세라는 정확한 정보에 따라 인터뷰를 한다.

![sarahroseinterviewemail](assets/sarahroseinterviewemail.png)

사라 로즈는 인터뷰 일정을 받았다

## 면접 후 고용 관리자는 사라 로즈를 지명한다. {#after-the-interviews-the-hiring-manager-shortlists-sarah-rose}

Sarah Rose가 인터뷰를 통해 면접을 다 보고 그것들을 삭제한 후, 고용 관리자인 Gloria Rios는 그녀의 받은 편지함에서 후보 선택 작업을 열고 선택을 클릭합니다. Gloria Rios의 결정은 HR 담당자 John Doe에게 추가 처리를 위해 전달됩니다.

![gladariosinboxoffer](assets/gloriariosinboxoffer.png)

글로리아의 AEM 받은 편지함

![영미자](assets/gloriariosselectcandidate.png)

Gloria Rios가 인터뷰 후에 Sarah Rose를 선택하다

## John Doe가 추가 정보 {#john-doe-requests-more-information} 요청

입사 지원자를 신청하기 전에, 그녀의 배경을 확인해야 한다. John Doe는 선택된 지원자의 세부 사항을 열고 검토하며 그녀의 고용 및 교육 세부 사항 중 일부가 아직 채워지지 않은 것을 발견했습니다. John Doe 클릭은 더 많은 정보가 필요합니다.

![](assets/johndoeinbox.png) ![johndoeinboxjohndoeneedmore](assets/johndoeneedmoreinformation.png)

John Doe는 Sarah Rose로부터 그녀의 교육과 근무 경험에 대한 더 많은 정보를 요청합니다

## Sarah Roz는 {#sarah-rose-receives-an-email-requesting-further-information} 추가 정보를 요청하는 이메일을 수신합니다.

사라 로즈는 그녀의 취업 신청서를 처리하는 데 더 많은 정보가 필요하다는 것을 알리는 이메일을 받았다. 이메일에는 필요한 정보를 입력할 수 있는 양식 링크가 포함되어 있습니다.

![사르라호시모알자세한 정보](assets/sarahroseemailmoredetails.png)

Sarah Rose는 그녀의 취업 신청서를 처리하는 데 더 많은 정보가 필요하다는 것을 알리는 이메일을 받았다

Sarah가 이메일에 있는 세부 정보 제공 링크를 클릭합니다. 양식이 나타납니다. Sarah는 John Doe가 요청한 필수 교육 및 고용 세부 사항을 채우고 [제출]을 클릭합니다.

![additionalinformation1](assets/additionalinformation1.png)

Sarah는 이메일의 링크를 클릭하여 추가 정보 양식을 엽니다

![additionalinformation2](assets/additionalinformation2.png)

Sarah는 John Doe가 요청한 추가 정보를 채우고 [제출]을 클릭합니다

## John Doe는 제공된 추가 정보에 대해 선택된 후보 프로필을 검토합니다. {#john-doe-reviews-the-selected-candidate-profile-for-the-additional-information-provided}

John Doe는 후보 검토 요청을 선택하고 엽니다. John Doe는 Sarah가 필요한 모든 정보를 채웠음을 발견하였다. 애플리케이션을 검토한 후 John Doe가 승인을 클릭합니다. 존 도 씨의 승인 하에, 사라 로즈에 대한 신원 조사를 수행하라는 요청은 존 제이콥스에게 전달됩니다.

![johndoadditionalinginbox](assets/johndoeadditionainformationinbox.png)

John Doe의 AEM 받은 편지함

![johndoadditioninforumereview-copy](assets/johndoeadditionalinformationreview-copy.png)

John Doe는 Sarah가 제공한 추가 정보를 검토하고 승인합니다

## John Jacobs는 백그라운드 확인 요청 {#john-jacobs-receives-a-background-check-request}을 수신합니다.

John Jacobs는 그의 받은 편지함에서 배경 확인 요청을 봅니다. John Jacobs는 일을 시작하고 Sarah Rose가 제공한 정보를 검토합니다. 배경 확인을 한 후 John Jacobs는 Go Ahead를 클릭하여 배경 확인이 성공했음을 나타냅니다.

![johjacobbackgrotcheckbox](assets/johnjacobsbackgroundcheckinbox.png)

존 제이콥스의 AEM 받은 편지함

![johjacobbackgrocheckgoahead](assets/johnjacobsbackgroundcheckgoahead.png)

백그라운드 검사를 수행한 후 John Jacobs는 Go Ahead를 클릭합니다

## John Doe는 Sarah Rose {#john-doe-sends-out-the-joining-letter-to-sarah-rose}에게 입단 편지를 보냅니다.

John Doe는 그의 AEM 받은 편지함에서 조인 편지를 보내는 요청을 받습니다. John은 요청을 열고 세부 사항을 봅니다. John Doe는 연결된 문자 PDF를 첨부한 다음 [첨부 및 편지 보내기]를 클릭합니다.

![joineingletterinbox](assets/johndoejoiningletterinbox.png)

John Doe의 AEM 받은 편지함

![johndoejoinletterattachandsend](assets/johndoejoiningletterattachandsend.png)

John Doe가 서명을 위해 조인 편지를 보냅니다.

## Sarah Rose는 합작 문자 {#sarah-rose-receives-and-signs-the-joining-letter}을 수신하고 서명합니다.

사라 로즈는 서명하기 위해 함께 하는 편지를 받았다. Sarah가 여기를 클릭해서 편지를 검토하고 서명합니다. 연결된 문자 PDF가 열리고 문서에 서명할 필드가 표시됩니다.

![사라로초스관이렛메일](assets/sarahrosejoiningletteremail.png)

새라 로즈는 서명하기 위해 함께 하는 편지를 받았다

새라는 입력, 직접 쓰기, 서명 이미지 삽입, 모바일 터치스크린을 사용하여 서명을 그릴 수 있습니다. Sarah는 이름을 입력하고 [서명하기 클릭]을 클릭한 다음, 서명된 서신의 사본을 다운로드합니다.

![사라로초인레터서명](assets/sarahrosejoininglettersign.png)

사라가 같이 쓴 편지에 서명하기 위해 이름을 입력한다

![sarahrosejoininglettersign2](assets/sarahrosejoininglettersign2.png)

Sarah가 [서명하려면 클릭]을 클릭하여 조인 서신 서명 완료

