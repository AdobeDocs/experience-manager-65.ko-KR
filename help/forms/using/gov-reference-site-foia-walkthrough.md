---
title: We.Gov 참조 사이트 FOIA 연습
seo-title: We.Gov 참조 사이트 FOIA 연습
description: We.Gov 참조 사이트 연습에서 AEM Forms이 어떻게 정부가 개인의 정보 공개에 관한 법률(Freedom of Information Act)에 따라 요청한 정보를 받아 가져올 수 있는지 알아보십시오.
seo-description: We.Gov 참조 사이트 연습에서 AEM Forms이 어떻게 정부가 개인의 정보 공개에 관한 법률(Freedom of Information Act)에 따라 요청한 정보를 받아 가져올 수 있는지 알아보십시오.
uuid: 65d4233c-8dad-4e5e-8e39-22eb4f145adc
topic-tags: introduction
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: cef8f597-7935-4d98-aacf-9981470ab620
translation-type: tm+mt
source-git-commit: af326f2d2b278fe36df05afc8c172f74c99a064c
workflow-type: tm+mt
source-wordcount: '865'
ht-degree: 0%

---


# We.Gov 참조 사이트 FOIA 연습 {#we-gov-reference-site-foia-walkthrough}

## Reference site Freedom of Information Act scenario {#reference-site-freedom-of-information-act-scenario}

We.Gov는 입양 부모가 아이를 입양할 경우 양육비를 위해 등록할 수 있도록 하는 국영 운영 조직입니다. We.Gov는 또한 부모가 정보의 자유법에 따라 다음 정부 부서에 정보를 요청할 수 있도록 허용합니다.

* Defense Logistics Agency
* 국방부 감찰관
* 법무부 - 정보 정책국
* 해군
* 환경 보호국

정보의 자유법에 대한 자세한 내용은 [www.foia.gov](https://www.foia.gov)를 참조하십시오.

The scenario contains the following personas:

* 정보를 요청하는 사람 사라 로즈
* 요청을 처리하는 John Jacobs는 그것을 적절한 부서에 전달한다
* 요청에따라 정보를 제공하는 정부 직원 글로리아 리오스

## Sarah는 FOIA {#sarah-initiates-request-for-information-under-foia}에 따라 정보 요청을 시작합니다.

&quot;정보의 자유법&quot;에 따라, Sarah는 2013년 회계년도 (FY) 2013년 - 2016년 동안 아동 및 가족 관련 케이스 로그 사본을 요청하고 있다. 사라는 법무부에 이 요청을 제출할 것이며, 그녀는 인쇄와 우편 비용을 100달러까지 지불할 의사가 있음을 의미한다.

### 작동 방식 {#how-it-works}

### 직접 보기 {#see-it-yourself}

브라우저에서 `https://<hostname>:<PublishPort>/wegov`을(를) 엽니다. We.Gov 사이트에서 응용 프로그램 > 모든 응용 프로그램을 누릅니다. 모든 응용 프로그램 페이지에서 FOIA 요청에 대한 응용 프로그램 아래의 적용을 누릅니다.

## 사라는 FOIA {#sarah-starts-her-application-for-information-under-foia} 아래에 정보 신청을 시작합니다.

Sarah는 **Apply**&#x200B;을 클릭하고 Freedom of Information Act Request Form 페이지에서 다음을 포함한 정보를 입력합니다.

* **에이전시:** 사라는 법무성 - 정보 정책부로 요청이 처리되었던 기관을 지정합니다.

* **최대 비용**:사라는 그녀가 인쇄와 우편 요금을 100달러까지 기꺼이 지불할 것을 명시하고 있다.
* **요청을 자세히 설명합니다**.Sarah는 &quot;2013년 회계년도에서 2016년 회계년도까지의 아동과 가족 관련 케이스 로그 사본 요청&quot;을 지정합니다.

![2013년부터 2016년까지 회계년도의 자녀 및 가족 사례 로그 관리 사본 요청](assets/sarahfiosform.png)

2013년부터 2016년까지 회계년도의 자녀 및 가족 사례 로그 관리 사본 요청

Sarah는 언제든지 저장을 눌러 양식 초안을 저장하고 나중에 다시 돌아와 양식을 채우고 제출할 수 있습니다. 사라는 양식을 제출한다.

>[!NOTE]
>
>이메일 다시 시작 워크플로우는 로그인한 사용자에게만 작동합니다. 참조 사이트 시나리오에서 사용자 Sarah Rose가 추가되었는지 확인합니다. Sarah의 로그인 자격 증명은 `srose/password`입니다.

## John Jacobs는 응용 프로그램 {#john-jacobs-receives-and-approves-the-application}을(를) 수신하고 승인합니다.

John Jacobs는 요청을 받고 그것을 올바른 사람에게 보낸다. AEM 받은 편지함은 한 곳에서 제출된 모든 애플리케이션을 볼 수 있도록 해줍니다.

### 작동 방식 {#how-it-works-1}

사라가 FOIA 신청서를 작성하고 제출하면, 그 신청서의 기록은 John Jacobs의 받은 편지함으로 전송됩니다. John Jacobs는 제출된 신청서를 보고 수락하거나 거부할 수 있습니다.

### 직접 보기 {#see-it-yourself-1}

https://&lt;***hostname***:&lt;***PublishPort***>/content/we-finance/global/en/login.html?resource=/aem/inbox.html에서 AEM 받은 편지함에 액세스할 수 있습니다. John Jacobs의 사용자 이름/암호를 사용하여 AEM 받은 편지함에 로그인하고 FOIA 응용 프로그램을 참조하십시오. 양식 중심의 워크플로우 작업에 AEM 받은 편지함을 사용하는 방법에 대한 자세한 내용은 AEM 받은 편지함의 Forms 응용 프로그램 및 작업 관리[를 참조하십시오.](/help/forms/using/manage-applications-inbox.md)

![조니](assets/johnjacobs.png)

John Jacobs는 애플리케이션 대시보드에서 애플리케이션을 보거나 승인하거나 거부할 수 있습니다. John Jacobs는 요청 세부 사항을 선택하고 열고 요청을 검토한 후 승인합니다.

![johnjacobstaskdetail-1](assets/johnjacobstaskdetail-1.png)

### <strong>Sarah가 확인 이메일을 받았다</strong> {#strong-sarah-receives-an-acknowledgement-email-strong}

John Jacobs가 그 신청을 승인한 후, Sarah는 We.Gov 사이트로부터 승인 이메일을 받았다. Sarah는 그녀의 신청을 처리하는 데 필요한 비용과 시간을 알려 준다. 또한 이메일에는 사라가 자신의 응용 프로그램에 대한 업데이트를 위해 연락할 수 있는 이메일과 전화 세부 정보도 포함되어 있습니다.

![사라로즈이메일](assets/sarahroseemail.png)

## Gloria는 FOIA의 2차 승인 요청 {#gloria-receives-the-foia-request-for-second-level-approval}을 받습니다.

John Jacobs가 필요한 정보를 입력하고 Sarah의 요청을 승인한 후, 요청은 Gloria Rios에게 가서 최종 승인을 얻습니다. Gloria는 첨부한 서류를 검토하고 그 요청을 승인한다.

![gladioosinbox](assets/gloriariosinbox.png)

### 작동 방식 {#how-it-works-2}

John Jacobs가 FOIA 요청을 승인하면 응용 프로그램의 PDF 또는 기록 문서가 만들어지고 Gloria Rios의 받은 편지함으로 전송됩니다. Gloria는 제출된 요청을 보고 승인하거나 거부할 수 있습니다.

### 직접 {#see-for-yourself} 보기

https://&lt;***hostname***:&lt;***PublishPort***>/content/we-finance/global/en/login.html?resource=/aem/inbox.html에서 AEM 받은 편지함에 액세스할 수 있습니다. Gloria Rios의 사용자 이름/암호로 격자/암호를 사용하여 AEM 받은 편지함에 로그인하고 FOIS 요청을 참조하십시오.

Gloria는 요청을 열어 FOIA 요청의 세부사항을 조사합니다. 글로리아는 요청서의 세부 내용을 검토하고 필요한 문서 제공 가능성을 점검한 후 요청을 승인한다.

![미분 승인](assets/gloriariosapproves.png)

## Sarah는 자신의 요청이 승인되었다는 알림을 받습니다. {#sarah-receives-notification-that-her-request-is-approved}

글로리아가 FOIA의 요청을 승인한 후, 사라는 그녀의 요청이 승인되었다는 이메일을 받았다. 또한, 이메일에는 문서 제공을 위한 임시 타임라인에 대한 정보와 후속 조치에 대한 연락처 정보도 포함되어 있습니다.

![sarahrosem approval](assets/sarahroseemailapproval.png)

