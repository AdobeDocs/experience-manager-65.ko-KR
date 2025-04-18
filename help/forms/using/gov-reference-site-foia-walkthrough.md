---
title: We.Gov 참조 사이트 FOIA 연습
description: We.Gov 참조 사이트 안내 문서를 참조하여 AEM Forms이 정보 자유법에 따라 개인이 요청한 정보를 정부가 어떻게 받고 제공하는지 이해할 수 있습니다.
topic-tags: introduction
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 57b5ce89-6b01-4087-a485-6d9696f06378
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Foundation Components
role: Admin, User, Developer
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '842'
ht-degree: 0%

---

# We.Gov 참조 사이트 FOIA 연습 {#we-gov-reference-site-foia-walkthrough}

## 참조 사이트 정보의 자유 법률 시나리오 {#reference-site-freedom-of-information-act-scenario}

We.Gov는 입양한 부모가 아이를 입양한 경우, 아이 양육비를 등록할 수 있도록 하는 국영 기관입니다. We.Gov는 또한 부모들이 정보 자유법에 따라 다음 정부 부서에 정보를 요청할 수 있도록 하고 있습니다.

* 미국 국방병참국
* 미국 국방부 감찰관
* 법무부 - 정보 정책국
* 해군
* 환경 보호국

정보의 자유법에 대한 자세한 내용은 [https://www.foia.gov/](https://www.foia.gov)을(를) 참조하십시오.

이 시나리오에는 다음 가상 사용자가 포함됩니다.

* Sarah Rose, 아래에 정보를 요청하는 사람
* 요청을 처리하는 John Jacobs 는 해당 부서에 요청을 전달합니다
* Gloria Rios, 요청에 따라 정보를 제공하는 정부 직원

## Sarah가 FOIA에서 정보 요청을 시작함 {#sarah-initiates-request-for-information-under-foia}

정보 자유법에 따라 Sarah는 2013년부터 2016년까지 매년 어린이 및 가족 사건 기록부(FY)의 사본을 요청합니다. Sarah는 이 요청을 법무부 - 정보 정책국 (Office of Information Policy)에 제출하며 인쇄 및 우편 요금을 USD 100까지 지불할 수 있음을 의미합니다.

### 작동 방식 {#how-it-works}

### 직접 확인 {#see-it-yourself}

브라우저에서 `https://<hostname>:<PublishPort>/wegov`을(를) 엽니다. We.Gov 사이트에서 Applications > All Applications 를 선택합니다. 모든 응용 프로그램 페이지의 FOIA 요청에 대한 응용 프로그램 아래에서 적용을 선택합니다.

## Sarah는 FOIA에서 그녀의 정보 신청을 시작한다 {#sarah-starts-her-application-for-information-under-foia}

Sarah가 **적용**&#x200B;을 클릭하고 정보 자유 법안 요청 양식 페이지에서 Sarah가 다음을 포함한 정보를 입력합니다.

* **기관:** Sarah는 법무부 - 정보 정책 담당자로 요청을 처리한 기관을 지정합니다.

* **최대 지불 예정**: Sarah는 인쇄 및 우편 요금에 대해 최대 USD 100을 지불할 준비가 되어 있다고 지정합니다.
* **요청을 자세히 설명하십시오**: Sarah가 &quot;2013년부터 2016년까지 회계 연도의 하위 항목 및 가족 관리 사례 로그에 대한 복사본 요청&quot;을 지정합니다.

![2013~2016 회계 연도의 아동 및 가족 관리 사례 로그 복사본 요청](assets/sarahfiosform.png)

2013~2016 회계 연도의 아동 및 가족 관리 사례 로그 사본 요청

언제든지 Sarah가 **저장**&#x200B;을 선택하여 양식 초안을 저장하고 나중에 다시 돌아와 양식을 작성하고 제출할 수 있습니다. Sarah가 양식을 제출합니다.

>[!NOTE]
>
>이메일에서 다시 시작 워크플로우는 로그인한 사용자만 사용할 수 있습니다. 참조 사이트 시나리오에서 사용자 Sarah Rose가 추가되었는지 확인합니다. Sarah의 로그인 자격 증명은 `srose/password`입니다.

## John Jacobs는 신청서를 접수하고 승인한다 {#john-jacobs-receives-and-approves-the-application}

John Jacobs 는 요청을 받아 적합한 사람에게 보냅니다. AEM 받은 편지함을 사용하면 John이 제출된 모든 애플리케이션을 한 곳에서 볼 수 있습니다.

### 작동 방식 {#how-it-works-1}

Sarah가 FOIA 신청서를 작성하여 제출하면, 신청서에 대한 기록이 John Jacobs의 받은 편지함으로 보내진다. John Jacobs는 제출된 지원서를 보고 이를 수락 또는 거부할 수 있습니다.

### 직접 확인 {#see-it-yourself-1}

https://&lt;***호스트 이름***>:&lt;***PublishPort***>/content/we-finance/global/en/login.html?resource=/aem/inbox.html에서 AEM 받은 편지함에 액세스할 수 있습니다. John Jacobs의 사용자 이름/암호로 jjacobs/password를 사용하여 AEM Inbox에 로그인하고 FOIA 애플리케이션을 참조하십시오. 양식 중심의 워크플로 작업에 AEM 받은 편지함을 사용하는 방법에 대한 자세한 내용은 [AEM 받은 편지함에서 Forms 응용 프로그램 및 작업 관리](/help/forms/using/manage-applications-inbox.md)를 참조하십시오.

![johnjacobs](assets/johnjacobs.png)

John Jacobs는 애플리케이션 대시보드에서 애플리케이션을 보고 승인하거나 거부할 수 있습니다. John Jacobs는 요청 세부 사항을 선택하여 열고 요청을 검토한 후 승인합니다.

![johnjacobstaskdetail-1](assets/johnjacobstaskdetail-1.png)

### <strong>Sarah가 승인 이메일을 받습니다</strong> {#strong-sarah-receives-an-acknowledgement-email-strong}

존 제이콥스가 신청을 승인하면, 사라는 We.Gov 사이트로부터 승인 이메일을 받는다. Sarah는 자신의 신청서 처리에 필요한 비용과 시간에 대해 정보를 받는다. 이메일에는 Sarah가 애플리케이션의 업데이트를 위해 연락할 수 있는 이메일 및 전화 세부 정보도 포함됩니다.

![sarahroseemail](assets/sarahroseemail.png)

## 글로리아는 2단계 승인을 위한 FOIA 요청을 받습니다 {#gloria-receives-the-foia-request-for-second-level-approval}

존 제이콥스가 필요한 정보를 입력하고 사라의 요청을 승인하면 최종 승인을 위해 글로리아 리오스에게 넘어간다. 글로리아는 첨부된 기록 문서를 검토하고 요청을 승인합니다.

![글로리아리오시노박스](assets/gloriariosinbox.png)

### 작동 방식 {#how-it-works-2}

John Jacobs가 FOIA 요청을 승인하면 해당 응용 프로그램의 PDF 또는 기록 문서가 작성되어 Gloria Rios의 받은 편지함으로 전송됩니다. 글로리아는 제출된 요청을 보고 승인하거나 거부할 수 있습니다.

### 직접 보기 {#see-for-yourself}

https://&lt;***호스트 이름***>:&lt;***PublishPort***>/content/we-finance/global/en/login.html?resource=/aem/inbox.html에서 AEM 받은 편지함에 액세스할 수 있습니다. Gloria Rios의 사용자 이름/암호로 grios/password를 사용하여 AEM Inbox에 로그인하고 FOIS 요청을 확인합니다.

Gloria는 그 요청을 열고 FOIA 요청의 세부사항들을 조사합니다. Gloria는 요청의 세부사항을 검토하고 필요한 문서를 제공할 가능성을 확인한 후 요청을 승인합니다.

![gloriariosapprovals](assets/gloriariosapproves.png)

## Sarah가 요청이 승인되었다는 알림을 받습니다. {#sarah-receives-notification-that-her-request-is-approved}

글로리아가 FOIA 요청을 승인한 후, 사라는 자신의 요청이 승인되었음을 알리는 이메일을 수신합니다. 이메일에는 문서 제공을 위한 임시 타임라인에 대한 정보와 요청에 대한 후속 조치를 위한 연락처 세부 정보도 포함됩니다.

![sarahroseemailapproval](assets/sarahroseemailapproval.png)
