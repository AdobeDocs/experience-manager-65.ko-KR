---
title: We.Gov 참조 사이트 FOIA 연습
seo-title: We.Gov 참조 사이트 FOIA 연습
description: AEM Forms를 통해 정부가 정보 자유법에 따라 개인 사용자에 의해 요청되는 정보를 어떻게 수신하고 전송할 수 있는지 알아보려면 We.Gov 참조 사이트 연습을 참조하십시오.
seo-description: AEM Forms를 통해 정부가 정보 자유법에 따라 개인 사용자에 의해 요청되는 정보를 어떻게 수신하고 전송할 수 있는지 알아보려면 We.Gov 참조 사이트 연습을 참조하십시오.
uuid: 65d4233c-8dad-4e5e-8e39-22eb4f145adc
topic-tags: introduction
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: cef8f597-7935-4d98-aacf-9981470ab620
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# We.Gov 참조 사이트 FOIA 연습 {#we-gov-reference-site-foia-walkthrough}

## 필수 조건 {#pre-requisite}

AEM Forms 참조 사이트 설정 및 [구성에 설명된 대로 We.Gov 참조 사이트를](/help/forms/using/setup-reference-sites.md)설정합니다.

## Reference site Freedom of Information Act 시나리오 {#reference-site-freedom-of-information-act-scenario}

We.Gov는 입양 부모가 아이를 입양할 경우 아동 지원에 등록할 수 있도록 하는 주립 운영 조직입니다. We.Gov는 또한 부모가 정보의 자유법에 따라 다음 정부 부서에 정보를 요청할 수 있도록 허용합니다.

* Defense Logistics Agency
* 국방부 감찰관
* 법무부 - 정보 정책
* 해군
* 환경 보호국

정보의 자유에 대한 자세한 내용은 www.foia.gov을 [참조하십시오](https://www.foia.gov).

The scenario includes the following personas:

* 정보를 요청하는 사람 사라 로즈
* 요청을 처리하는 사람 John Jacobs는 그 요청을 적절한 부서에 전달한다
* 요청에 따라 정보를 제공하는 정부 직원 Gloria Rios

## Sarah, FOIA를 통한 정보 요청 시작 {#sarah-initiates-request-for-information-under-foia}

정보 자유법에 따라, 사라는 2013년 회계년도 (FY) 2016년 동안 아동 및 가족 관련 사건 로그 사본을 요청합니다. 사라는 법무부에 이 요청을 제출하고 - 정보정책국에 제출하며, 그녀가 인쇄와 우편 비용으로 100달러를 지불할 의사가 있다는 것을 또한 나타낸다.

### 작동 방식 {#how-it-works}

### 직접 보기 {#see-it-yourself}

In your browser, open `https://<hostname>:<PublishPort>/wegov`. We.Gov 사이트에서 응용 프로그램 > 모든 응용 프로그램을 누릅니다. 모든 응용 프로그램 페이지에서 FOIA 요청에 대한 응용 프로그램 아래에 있는 적용을 누릅니다.

## 사라는 FOIA를 통해 정보 신청을 시작한다 {#sarah-starts-her-application-for-information-under-foia}

사라는 **적용을** 클릭하고 &quot;정보의 자유&quot; 요청 양식 페이지에서 다음을 포함한 정보를 입력합니다.

* **** 에이전시:사라는 법무부인 정보 정책국으로서 그 요청이 처리되었던 기관을 지정합니다.

* **최대**&#x200B;비용:사라는 인쇄와 우편 요금 지불을 위해 100달러까지 지불할 의사가 있다고 명시했다.
* **요청을 자세히**&#x200B;설명합니다.Sarah는 &quot;2013~2016 회계년도의 &quot;아동 및 가족 관련 행정 자료 사본 요청&quot;을 지정합니다.

![2013 - 2016 회계년도의 자녀 및 가족 관련 사례 로그 사본 요청](assets/sarahfiosform.png)

2013 - 2016 회계년도의 자녀 및 가족 관련 사례 로그 사본 요청

Sarah는 언제든지 저장을 눌러 양식 초안을 저장하고 나중에 다시 돌아와 양식을 채우고 제출할 수 있습니다. 사라는 양식을 제출한다.

>[!NOTE]
>
>이메일 재개 워크플로우는 로그인한 사용자에게만 작동합니다. 참조 사이트 시나리오에서 사용자 Sarah Rose가 추가되었는지 확인합니다. Sarah의 로그인 자격 증명이 `srose/password`있습니다.

## John Jacobs는 이 신청서를 받고 승인한다 {#john-jacobs-receives-and-approves-the-application}

John Jacobs는 요청을 받고 올바른 사람에게 전달한다. AEM Inbox를 사용하면 제출된 모든 애플리케이션을 한 곳에서 볼 수 있습니다.

### 작동 방식 {#how-it-works-1}

Sarah가 FOIA 신청서를 작성하고 제출하면, 신청서 기록이 John Jacobs의 받은 편지함으로 전송됩니다. John Jacobs는 제출된 신청서를 보고 이를 수락하거나 거부할 수 있습니다.

### 직접 보기 {#see-it-yourself-1}

https://&lt;***hostname***>:&lt;PublishPort>/content/we-finance/global/en/login.html?***resource=/aem/inbox.html에서 AEM***&#x200B;받은 편지함에 액세스할 수 있습니다. John Jacobs의 사용자 이름/암호를 사용하여 AEM 받은 편지함에 로그인하고 FOIA 응용 프로그램을 참조하십시오. 양식 중심의 워크플로우 작업에 AEM 받은 편지함을 사용하는 방법에 대한 자세한 내용은 AEM 받은 편지함에서 [양식 애플리케이션 및 작업 관리를 참조하십시오](/help/forms/using/manage-applications-inbox.md).

![조니](assets/johnjacobs.png)

John Jacobs는 애플리케이션 대시보드에서 애플리케이션을 보거나 승인하거나 거부할 수 있습니다. John Jacobs는 요청 세부 사항을 선택하여 열고 요청을 검토한 후 승인합니다.

![johnjacobstaskdetail-1](assets/johnjacobstaskdetail-1.png)

### <strong>Sarah가 확인 이메일을</strong> 받았다 {#strong-sarah-receives-an-acknowledgement-email-strong}

John Jacobs가 그 신청서를 승인한 후, Sarah는 We.Gov 사이트로부터 승인 이메일을 받았다. Sarah는 신청서 처리에 필요한 비용과 시간을 알려 준다. 이메일에는 사라가 애플리케이션에 대한 업데이트를 위해 연락할 수 있는 이메일과 전화 정보도 포함되어 있습니다.

![사라흐로스이메일](assets/sarahroseemail.png)

## Gloria는 FOIA 2차 승인 요청을 받습니다. {#gloria-receives-the-foia-request-for-second-level-approval}

John Jacobs가 필요한 정보를 작성하고 Sarah의 요청을 승인한 후, 마지막 승인을 위해 Gloria Rios에게 요청합니다. Gloria는 첨부한 기록 문서를 검토하고 그 요청을 승인한다.

![glorioosinbox](assets/gloriariosinbox.png)

### 작동 방식 {#how-it-works-2}

John Jacobs가 FOIA 요청을 승인하면 PDF 또는 애플리케이션 기록 문서가 작성되어 Gloria Rios의 받은 편지함으로 전송됩니다. Gloria는 제출된 요청을 보고 승인하거나 거부할 수 있습니다.

### 직접 보기 {#see-for-yourself}

https://&lt;***hostname***>:&lt;PublishPort>/content/we-finance/global/en/login.html?***resource=/aem/inbox.html에서 AEM***&#x200B;받은 편지함에 액세스할 수 있습니다. Gloria Rios의 사용자 이름/암호로 격자/암호를 사용하여 AEM 받은 편지함에 로그인하고 FOIS 요청을 참조하십시오.

Gloria가 요청을 열어 FOIA 요청의 세부 사항을 조사합니다. Gloria는 그 요청의 세부내용을 검토하고 필요한 문서 제공 가능성을 점검한 후 요청을 승인합니다.

![미미 승인](assets/gloriariosapproves.png)

## Sarah는 그녀의 요청이 승인되었다는 통보를 받는다 {#sarah-receives-notification-that-her-request-is-approved}

글로리아가 FOIA 요청을 승인한 후, 사라는 그녀의 요청이 승인되었다는 것을 알리는 이메일을 받았다. 또한, 이메일에는 문서 제공을 위한 임시 타임라인에 대한 정보와 후속 조치에 대한 연락처 정보가 포함되어 있습니다.

![sarahrosem 승인](assets/sarahroseemailapproval.png)

