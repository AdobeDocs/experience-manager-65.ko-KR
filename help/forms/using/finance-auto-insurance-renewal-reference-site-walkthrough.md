---
title: We.Finance 자동 보험 갱신 참조 사이트 안내
seo-title: We.Finance 자동 보험 갱신 참조 사이트 안내
description: We.Finance 자동 보험 갱신 참조 사이트 안내
uuid: c749a6f7-71f1-4f47-b824-9c7b699072c7
contentOwner: dekalra
products: SG_EXPERIENCEMANAGER/6.5/FORMS
content-type: reference
discoiquuid: ad450124-49a5-4afb-aac3-ed3733d6504b
docset: aem65
exl-id: b6ded6ac-4fb1-49f9-b272-16774c3e89a3
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '748'
ht-degree: 0%

---

# We.Finance 자동 보험 갱신 참조 사이트 안내{#we-finance-auto-insurance-renewal-reference-site-walkthrough}

## We.Finance 참조 사이트 시나리오 {#we-finance-reference-site-scenario}

We.Finance 사이트는 AEM Forms의 대화형 통신 기능을 학습하기 위해 설계된 금융 서비스 사이트입니다.

AEM Forms와 Microsoft Dynamics와의 통합을 통해 금융 서비스 회사에서 고객 경험을 개인화하는 방법을 소개하는 We.Finance 자동 보험 사용 사례에 대한 자세한 연습을 참조하십시오. 상호 작용 연습은 금융 회사에서 복잡한 디지털 거래와 고객 커뮤니케이션을 쉽게 구현하도록 설계되었습니다.

**여정은 사용 사례부터 시작합니다.**

사라 로즈는 기존 We.Finance 고객이며, 자동차 보험 정책을 구매했습니다. 이제 그녀의 보험 보험 증권 갱신의 시기가 되었습니다. We.Finance 보험 대리인인 Gloria Rios가 Sarah에게 그녀의 정책 갱신에 대한 알림 메시지를 보냅니다. Sarah는 이메일에 제공된 지침을 따라 프로세스를 성공적으로 완료했습니다.

## 자동 보험 적용 연습 {#auto-insurance-application-walkthrough}

We.Finance 자동 보험 애플리케이션 시나리오는 사용자를 위한 시각적 내레이션이며, 두 가지 가상 사용자를 기반으로 합니다.

* We.Finance 고객 Sarah Rose
* Gloria Rios, 보험 대리인, We.Finance

### Gloria가 We.Finance에서 보험 정책 갱신 통신을 보냅니다. {#gloria-sends-an-insurance-policy-renewal-communication-from-we-finance}

Gloria가 AEM 인스턴스에 로그인하고 **자동 보험 갱신**&#x200B;을 클릭한 다음 **에이전트 UI 열기 를 클릭합니다.**&#x200B;클릭은 사라 로즈의 정책 세부 사항을 포함한 보험 문서를 미리 채웁니다. Gloria가&#x200B;**Submit**&#x200B;을 클릭하면 메시지가 &quot;Submission Initiated&quot; 화면에 표시되고 몇 초 후 &quot;Submitted Successfully&quot; 화면이 표시됩니다.

Sarah는 &quot;Your Auto Insurance Renewal&quot; 라는 제목이 있는 이메일을 받았다.

![에이전트 UI](assets/agent_ui_email_new.png)

#### 직접 {#see-it-yourself} 보기

**Adobe Experience Manager** > **Forms** > **Forms 및 문서** > **We.Finance** > **자동 보험**&#x200B;으로 이동합니다. 자동 보험 갱신 **대화형 통신**&#x200B;을 선택하고 **에이전트 UI 열기**&#x200B;를 클릭합니다. 대화형 커뮤니케이션이 에이전트 UI에서 열립니다. 첨부된 정책 문서가 포함된 전자 메일을 받을 올바른 전자 메일 주소를 입력하고 제출을 클릭합니다.

`https://[authorHost]: authorPort]/aem/formdetails.html/content/dam/formsanddocuments/we-finance/autoinsurance/auto-insurance-renewal.`에서 직접 자동 보험 갱신 대화형 커뮤니케이션에 액세스하여 검토할 수 있습니다

### Sarah는 We.Finance로부터 보험 증권 갱신 커뮤니케이션을 받고 {#sarah-receives-an-insurance-policy-renewal-communication-from-we-finance-and-decides-to-renew}을 갱신하기로 결정했다

사라가 We.Finance로부터 그녀의 자동차 보험 정책이 곧 만료된다는 것을 알려주는 첨부 파일이 있는 이메일을 받는다. 첨부물은 그녀의 자동차 보험 서신의 인쇄 버전이다.

Sarah는 **지금 갱신**&#x200B;을 클릭하고, 자신의 자동 보험 서신의 웹 버전으로 이동됩니다. 이 편지 외에, 사라는 그녀의 정책이 만료될 때까지 남은 일수를 찾았다. 이 페이지에서는 Sarah에게 정책 번호, 만기 금액, 할인 오퍼와 충성도 보상과 같은 기타 정보와 같은 보험 정책 세부 사항에 대한 기본 개요를 제공합니다. 사라가 정책 하단에 있는 **지금 갱신**&#x200B;을 다시 클릭합니다.

![ref1](assets/ref1.png)

#### 작동 방법 {#how-it-works}

자동 보험 서신의 웹 및 인쇄 출력은 대화형 커뮤니케이션의 다중 채널 기능을 사용하여 작성됩니다.

이메일의 지금 갱신 단추는 게시 인스턴스의 대화형 커뮤니케이션인 자동 보험 갱신 애플리케이션에 연결됩니다.

#### 직접 {#see-it-yourself-1} 보기

PDF가 첨부된 이메일을 받았어야 합니다. PDF는 자동 보험 증서의 인쇄 버전입니다. **지금 갱신**&#x200B;을 클릭하여 정책의 웹 버전에 연결합니다. 개인 정보 및 정책 세부 사항을 확인하고 **지금 갱신**&#x200B;을 클릭하여 다른 대화형 커뮤니케이션으로 이동합니다.

이메일의 **지금 갱신** 단추를 사용하면 Sarah가 정책의 웹 버전으로 이동됩니다. 다음 URL을 방문할 수 있습니다.

`https://[authorServer]:[authorPort]/content/document.html?schema=fdm&documentId=/content/forms/af/we-finance/autoinsurance/auto-insurance-renewal/channels/web.html&customerId=1`

자동 보험 갱신의 상세 요약을 확인하고 페이지 하단에 있는 **지금 갱신**&#x200B;을 클릭할 수 있습니다.

### Sarah가 결제 페이지 {#sarah-reaches-the-payment-page}에 도달함

We.Finance에서 Sarah를 결제 페이지로 데려갑니다. Sarah는 자신의 정책 번호와 만료 날짜를 다시 자신의 기록과 확인합니다. 페이지 오른쪽에서는 총 금액에 대해 10% 할인해 준 갱신 지불 요지를 확인합니다.

#### 작동 방법 {#how-it-works-1}

지금 갱신 단추가 사라를 결제 페이지로 안내합니다. 결제 페이지는 적응형 양식입니다.

#### 직접 {#see-it-yourself-2} 보기

**지금 갱신**&#x200B;을 클릭하여 결제 페이지에 도달합니다. 신용 카드 정보를 입력하고 **결제**&#x200B;를 클릭합니다.

에서 작성 인스턴스의 결제 페이지에 연결할 수 있습니다

`https://[authorServer]:[authorPort]/content/document.html?documentId=/content/forms/af/we-finance/credit-card/ccbillpayment.html&schema=fdm&customerId=1`

### Sarah가 지급을 완료하고 {#sarah-makes-the-payment-and-completes-the-process} 프로세스를 완료합니다

Sarah는 신용 카드 세부 사항을 입력하고 **결제**&#x200B;를 클릭합니다.

#### 작동 방법 {#how-it-works-2}

사라가 신용 카드 세부 사항을 입력하고 제출을 클릭하면, 그녀의 신용 카드 결제가 처리되고 적응형 양식에 구성된 감사 메시지가 화면에 나타납니다.

#### 직접 {#see-it-yourself-3} 보기

에서 결제 만들기를 클릭한 후 확인 메시지를 볼 수 있습니다

`https://[authorServer]:[authorPort]/content/forms/af/we-finance/credit-card/ccbillpayment/jcr:content/guideContainer.guideThankYouPage.html?owner=admin&status=Submitted`
