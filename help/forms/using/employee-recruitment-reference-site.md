---
title: 직원 채용 참조 사이트 연습
seo-title: 직원 채용
description: AEM Forms 참조 사이트는 조직에서 AEM Forms 기능을 사용하여 직원 채용 워크플로우를 구현하는 방법을 보여줍니다.
seo-description: AEM Forms 참조 사이트는 조직에서 AEM Forms 기능을 사용하여 직원 채용 워크플로우를 구현하는 방법을 보여줍니다.
uuid: 27e456ba-3c08-4c43-ad54-1ba0070995ad
topic-tags: introduction
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 5f04b13e-ea40-4c86-9168-e020c52435a2
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# 직원 채용 참조 사이트 연습 {#employee-recruitment-reference-site-walkthrough}

## 전제 조건 {#prerequisite}

AEM Forms 참조 사이트 설정 [및 구성에 설명된 대로 참조 사이트를](/help/forms/using/setup-reference-sites.md)설정합니다.

## 개요 {#overview}

We.Finance는 지원자들이 참조 사이트 포털을 통해 구직 신청을 할 수 있는 조직이다. 또한 이 조직은 포털에서 지원자의 면접 일정, 적목 및 내부 커뮤니케이션을 관리합니다. 사이트는 다음을 관리합니다.

* 구직 및 구직 지원자
* 후보자 심사 및 낙찰
* 인터뷰 프로세스
* 후보 세부 정보 수집
* 후보 배경 확인
* 선택한 후보자에게 오퍼 롤아웃

>[!NOTE]
>
>직원 채용 사용 사례는 We.Finance 및 We.Gov 참조 사이트 모두에서 사용할 수 있습니다. 연습에서 사용되는 예제, 이미지 및 설명은 We.Finance 참조 사이트를 사용합니다. 그러나 We.Gov를 사용하여 이러한 사용 사례를 실행하고 결함을 검토할 수 있습니다. 이렇게 하려면 **we-finance** 를 언급된 URL의 **we-gov** 로 바꿉니다.

### 워크플로우 모델 관련 {#workflow-models-involved}

직원 채용 사용 사례에는 두 가지 워크플로우가 포함됩니다.

* 인터뷰 전 - We Finance 직원 채용 워크플로우
* 인터뷰 후 - We Finance Employee Recruiting Post Interview 워크플로우

이러한 워크플로우는 AEM에서 만들어지며 다음 위치에서 찾을 수 있습니다.

`https://[authorHost]:[authorPort]/libs/cq/workflow/admin/console/content/models.html/etc/workflow/models/`

#### We Finance 직원 채용 워크플로우 {#we-finance-employee-recruiting-workflow}

다음은 본 문서에서 수행한 We Finance 직원 채용 워크플로우의 모델입니다.

![we-finance-employee-recruiting-workflow](assets/we-finance-employee-recruiting-workflow.png)

#### We Finance Employee Recruiting Post Interview 워크플로우 {#we-finance-employee-recruiting-post-interview-workflow}

다음은 이 문서에 이어 We Finance Employee Post Interruitment 워크플로우의 모델입니다.

![we-finance-employee-recruiting-post-interview-workflow](assets/we-finance-employee-recruiting-post-interview-workflow.png)

### 페르시아 {#personas}

The scenario includes the following personas:

* 그 조직에서 입사 지원자인 사라 로즈
* 채용 담당자 John Jacobs
* 채용 관리자인 Gloria Rios
* 인사 담당자인 John Doe

## 사라는 구직 신청을 한다 {#sarah-applies-for-a-job}

새라 로즈는 그 조직에서 일자리 기회를 찾고 있다. 웹 포털을 방문하여 취업 정보 페이지에 나와 있는 채용 사이트를 탐색합니다. 그녀는 일치하는 채용 목록을 찾아 신청한다.

![홈 페이지](assets/home-page.png)

We.Finance 홈 페이지

![경력 페이지](assets/career-page.png)

We.Finance 경력 페이지

Sarah가 채용 게시에서 [적용]을 클릭합니다. 작업 응용 프로그램 양식이 열립니다. 그녀는 신청서에 있는 모든 세부사항을 기입해서 제출한다.

![job-application-form](assets/job-application-form.png)

### 작동 방식 {#how-it-works}

We.Finance 홈 페이지와 경력 페이지는 AEM 사이트 페이지입니다. 경력 페이지에는 반복 가능한 패널을 사용하여 서비스를 사용하여 채용 공고를 가져와 페이지에 나열하는 적응형 양식이 포함됩니다. 에서 적응형 양식을 검토할 수 `https://[authorHost]:[authorPort]/editor.html/content/forms/af/we-finance/employee/recruitment/jobs.html`있습니다.

### 직접 보기 {#see-it-yourself}

이동 `https://[publishHost]:[publishPort]/content/we-finance/global/en.html` 후 [경력]을 **[!UICONTROL 클릭합니다]**. [ **[!UICONTROL 검색]** ]을 클릭하여 작업 목록을 채운 다음 **[!UICONTROL [작업 적용]** ]을 클릭합니다. 양식에 세부 정보를 입력하고 애플리케이션을 제출합니다.

이 연습을 통한 통신이 지정된 이메일 ID로 전송되므로 응용 프로그램에서 올바른 이메일 ID를 지정해야 합니다.

## 존 제이콥스 씨는 고용 관리자 선발에 대한 사라 로즈의 프로필을 요약한다 {#john-jacobs-shortlists-sarah-rose-s-profile-for-the-hiring-manager-s-screening}

그 조직은 사라가 제출한 취업 신청서를 받는다. 리쿠르트 직원인 존 제이콥스는 사라의 프로필을 검토할 임무를 맡았다. AEM 받은 편지함에서 작업을 검토하고, 작업 요구 사항과 일치하는 프로필을 찾은 다음, 바로 가기 목록을 클릭합니다. 사라의 프로필은 고용 관리자인 글로리아 리오스, 그녀의 승인을 위해 보내졌다.

![jakelobox-inbox-1](assets/jjacobs-inbox-1.png)

John의 AEM 받은 편지함

![후보 지명 대상자](assets/candidate-shortlist.png)

존 제이콥스 씨는 고용 관리자 선발에 대한 사라 로즈의 프로필을 요약한다

**작동 방식**

Job Application 양식의 제출 작업은 John Jacob의 받은 편지함에서 애플리케이션을 심사하기 위한 작업을 생성하는 워크플로우를 트리거합니다. John이 애플리케이션을 검토하고 제한하면 워크플로우가 채용 관리자인 Gloria의 받은 편지함에 작업을 만듭니다.

### 직접 보기 {#see-it-yourself-1}

John Jacobs의 사용자 이름/암호로 jjacobs/ `https://[publishHost]:[publishPort]/content/we-finance/global/en/login.html?resource=/aem/inbox.html`암호를 사용하여 로그인합니다. 후보 프로파일 검토 작업을 열고 지원자를 바로 나열합니다.

## Gloria는 지원서를 검토하고 지원자 면접을 승인한다 {#gloria-reviews-the-application-and-approves-the-applicant-for-an-interview}

채용 관리자인 Gloria는 AEM Inbox에서 바로 나열된 프로필을 작업으로 수신합니다. 그녀는 그것을 검토하고, 인터뷰를 위해 사라 로즈를 승인하였다.

![미화원](assets/gloriainbox.png)

Gloria의 AEM 받은 편지함

![예찬예일면접](assets/gloriaschedulesinterview.png)

글로리아는 사라 로즈를 인터뷰에 응하게 했다

**작동 방식**

Gloria가 인터뷰를 승인하면 워크플로우는 We.Finance 채용 담당자인 John Doe의 AEM 받은 편지함에 작업을 만듭니다.

### 직접 보기 {#see-it-yourself-2}

John Jacobs의 사용자 이름/암호로 jjacobs/password로 이동하여 `https://[publishHost]:[publishPort]/content/we-finance/global/en/login.html?resource=/aem/inbox.html` 로그인합니다. 후보 프로파일 검토 작업을 열고 지원자를 바로 나열합니다.

Gloria Rios의 사용자 이름/암호로 그리스/암호를 사용하여 로그인하십시오. `https://[publishHost]:[publishPort]/content/we-finance/global/en/login.html?resource=/aem/inbox.html` 후보 프로필 검토 작업을 열고 면접 예약을 클릭합니다.

## John Doe가 인터뷰를 예약합니다. {#john-doe-schedules-an-interview}

John Doe는 받은 편지함에서 인터뷰를 예약하는 작업을 받습니다. John Doe는 작업을 선택하여 열고 면접 날짜와 시간, 위치, 그리고 면접을 담당하는 HR 담당자를 John Jacob로 수정합니다. John Doe가 [초대장 이메일 보내기]를 클릭합니다. 사라에게 이메일이 보내지고 고용 관리자인 글로리아가 사라를 인터뷰하기 위해 업무를 맡긴다.

![johnbosamebox](assets/johnjacobsaeminbox.png)

John Doe의 AEM 받은 편지함

![johndoeschedule인터뷰를](assets/johndoescheduleinterview.png)

John Doe는 인터뷰를 예약하고 자세한 내용을 Sarah Rose에게 보냅니다

## Sarah Rose는 인터뷰 일정이 있는 이메일을 받았다 {#sarah-rose-receives-the-email-with-interview-schedule}

Sarah Rose는 인터뷰 일정, 장소 및 기타 세부 사항이 포함된 이메일을 받았다. 그녀는 면접 일정과 장소에 대해 괜찮다는 것을 나타내기 위해 수락을 클릭합니다. 세라는 정확한 정보를 바탕으로 인터뷰를 한다.

![sarahroseinterviewemail](assets/sarahroseinterviewemail.png)

사라 로즈는 인터뷰 일정을 받았다

## 인터뷰 후, 고용 관리자는 사라 로즈를 유인해 주었다 {#after-the-interviews-the-hiring-manager-shortlists-sarah-rose}

Sarah Rose가 인터뷰를 통해 문서를 정리하면, 고용 관리자인 Gloria Rios는 그녀의 받은 편지함에서 후보 선택 작업을 열고 선택을 클릭합니다. Gloria Rios의 결정은 인사 담당자인 John Doe에게 추가 처리를 위해 전달되었습니다.

![gladariosinboxoffer](assets/gloriariosinboxoffer.png)

Gloria의 AEM 받은 편지함

![영광스러운 사람](assets/gloriariosselectcandidate.png)

Gloria Rios가 인터뷰 후에 Sarah Rose를 선발하다

## John Doe가 추가 정보 요청 {#john-doe-requests-more-information}

지원자에게 조직에 가입하도록 요청하기 전에, 그녀의 배경을 확인해야 한다. John Doe는 선택된 지원자의 세부 사항을 열어 검토하고, 일부 채용 및 교육 세부 사항이 아직 채워지지 않은 것으로 파악합니다. John Doe 클릭에 대한 자세한 정보가 필요합니다.

![johndoeinbox](assets/johndoeinbox.png) johndoenedmore ![information](assets/johndoeneedmoreinformation.png)

John Doe는 Sarah Rose로부터 그녀의 교육과 근무 경험에 관한 더 많은 정보를 요청한다

## Sarah Rose, 정보 요청 이메일 받아 {#sarah-rose-receives-an-email-requesting-further-information}

사라 로즈는 그녀의 취업 신청서를 처리하는 데 더 많은 정보가 필요함을 알리는 이메일을 받았다. 이메일에는 필요한 정보를 작성하기 위한 양식의 링크가 포함되어 있습니다.

![사라호에모자세히](assets/sarahroseemailmoredetails.png)

사라 로즈는 그녀의 취업 신청서를 처리하는 데 더 많은 정보가 필요함을 알리는 이메일을 받았다

Sarah는 이메일에서 세부 정보 제공 링크를 클릭합니다. 양식이 나타납니다. Sarah는 John Doe의 요청에 따라 필요한 교육 및 고용 세부 사항을 작성하고 [제출]을 클릭합니다.

![additionalinformation1](assets/additionalinformation1.png)

Sarah는 이메일의 링크를 클릭하여 추가 정보 양식을 엽니다

![additionalinformation2](assets/additionalinformation2.png)

Sarah는 John Doe의 요청에 따라 추가 정보를 작성하고 [제출]을 클릭합니다

## John Doe는 제공된 추가 정보를 위해 선택된 후보 프로필을 검토합니다. {#john-doe-reviews-the-selected-candidate-profile-for-the-additional-information-provided}

John Doe는 후보 검토 요청을 선택하고 엽니다. John Doe는 Sarah가 필요에 따라 모든 정보를 채웠음을 발견했다. 애플리케이션을 검토한 후 John Doe는 승인을 클릭합니다. 존 도어의 승인을 받고, 사라 로즈에 대한 신원 확인을 수행하기 위한 요청이 존 제이콥스에게 전달되었다.

![johndoadditionationinbox](assets/johndoeadditionainformationinbox.png)

John Doe의 AEM 받은 편지함

![johndoadditioninforumereview-copy](assets/johndoeadditionalinformationreview-copy.png)

John Doe는 Sarah가 제공한 추가 정보를 검토하고 승인합니다.

## John Jacobs가 신원 확인 요청을 받습니다. {#john-jacobs-receives-a-background-check-request}

John Jacobs는 그의 받은 편지함에서 배경 확인 요청을 봅니다. John Jacobs는 일을 시작하고 Sarah Rose가 제공한 정보를 검토합니다. 배경 확인을 수행한 후 John Jacobs는 [계속 이동]을 클릭하여 배경 검사가 성공적으로 수행되었음을 나타냅니다.

![johnjacobbackgrotcheckbox](assets/johnjacobsbackgroundcheckinbox.png)

John Jacobs의 AEM 받은 편지함

![hundjacobbackgroundcheckgoahead](assets/johnjacobsbackgroundcheckgoahead.png)

배경 확인을 수행한 후 John Jacobs는 [계속 이동]을 클릭합니다

## John Doe가 Sarah Rose에게 입단 편지를 보냅니다 {#john-doe-sends-out-the-joining-letter-to-sarah-rose}

John Doe는 AEM 받은 편지함에서 조인 편지를 보내는 요청을 받습니다. John은 요청을 열고 세부 사항을 봅니다. John Doe는 연결된 문자 PDF를 첨부한 다음 [편지 첨부 및 보내기]를 클릭합니다.

![johndoejoinletter 받은 편지함](assets/johndoejoiningletterinbox.png)

John Doe의 AEM 받은 편지함

![johndoejoinletterattachandsend](assets/johndoejoiningletterattachandsend.png)

John Doe가 서명을 위해 조인 편지를 보냅니다.

## Sarah Rose는 그 소식을 받아 적고, 함께 있는 편지에 서명한다 {#sarah-rose-receives-and-signs-the-joining-letter}

Sarah Rose는 서명하기 위해 합자서를 받았다. Sarah가 여기를 클릭해서 편지를 검토하고 서명합니다. 연결된 문자 PDF가 열리고 문서에 서명할 필드가 있습니다.

![사라로조끼인레트메일](assets/sarahrosejoiningletteremail.png)

Sarah Rose, 서명자 환영

Sarah는 입력, 그리기, 직접 쓰기, 서명 이미지 삽입, 모바일 터치스크린 중 하나를 선택하여 서명을 그릴 수 있습니다. Sarah는 이름을 입력하고 [클릭하여 서명]을 클릭한 다음 서명한 편지함의 서명된 사본을 다운로드합니다.

![사라로즈게인레터 기호](assets/sarahrosejoininglettersign.png)

사라가 같이 쓴 편지에 서명하기 위해 이름을 입력한다

![sarahrosejoininglettersign2](assets/sarahrosejoininglettersign2.png)

Sarah가 [클릭하여 서명]을 클릭하여 조인 서신에 서명합니다.

