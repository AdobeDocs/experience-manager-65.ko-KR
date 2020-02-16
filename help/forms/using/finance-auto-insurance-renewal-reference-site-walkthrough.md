---
title: We.Finance 자동 보험 갱신 참조 사이트 연습
seo-title: We.Finance 자동 보험 갱신 참조 사이트 연습
description: 'null'
seo-description: 'null'
uuid: c749a6f7-71f1-4f47-b824-9c7b699072c7
contentOwner: dekalra
products: SG_EXPERIENCEMANAGER/6.5/FORMS
content-type: reference
discoiquuid: ad450124-49a5-4afb-aac3-ed3733d6504b
docset: aem65
translation-type: tm+mt
source-git-commit: b2fd6e0412ee0dacf7b68f4a0b219804dd4a6150

---


# We.Finance 자동 보험 갱신 참조 사이트 연습{#we-finance-auto-insurance-renewal-reference-site-walkthrough}

## 전제 조건 {#pre-requisites}

설정에 설명된 대로 참조 사이트를 [설정하고 AEM Forms 참조 사이트를 구성합니다](../../forms/using/setup-reference-sites.md).

## We.Finance 참조 사이트 시나리오 {#we-finance-reference-site-scenario}

We.Finance 사이트는 AEM Forms의 인터랙티브한 커뮤니케이션 기능을 학습하는 데 도움이 되는 금융 서비스 사이트입니다.

AEM 양식과 Microsoft Dynamics와의 통합을 통해 금융 서비스 회사에서 고객 경험을 개인화하는 방법을 소개하는 We.Finance 자동 보험 사용 사례를 자세히 살펴보십시오. 대화형 연습은 금융 회사의 복잡한 디지털 거래와 고객 커뮤니케이션을 쉽게 구현하기 위해 마련되었습니다.

**고객 여정은 사용 사례부터 시작됩니다.**

Sarah Rose는 기존 We.Finance 고객이며 자동차 보험 증권을 구입했습니다. 지금이 바로 그녀의 보험 증권 갱신의 시기이다. We.Finance의 보험 대리인인 Gloria Rios가 Sarah에게 그녀의 정책 갱신에 대한 메모를 보냅니다. Sarah는 이메일에 제공된 지침을 따라 작업을 성공적으로 완료했습니다.

## 자동 보험 신청 연습 {#auto-insurance-application-walkthrough}

We.Finance 자동 보험 신청 시나리오는 사용자를 위한 시각적 내레이션이며 다음 두 가지 측면을 기반으로 합니다.

* We.Finance 고객인 Sarah Rose
* Gloria Rios, We.Finance 보험 담당자

### Gloria가 We.Finance로부터 보험 증권 갱신 통신을 전송하다 {#gloria-sends-an-insurance-policy-renewal-communication-from-we-finance}

Gloria는 AEM 인스턴스에 로그인하고 자동 **보험 갱신을 클릭한** 다음 에이전트 UI **열기를 클릭합니다.**&#x200B;그 클릭은 새라 로즈의 정책 세부 사항으로 보험 서류를 미리 만든다. Gloria가&#x200B;**Submit를 클릭하면** &quot;Submit Initiated&quot; 화면에 메시지가 표시된 후 몇 초 후 &quot;Submitted Successfully&quot; 화면이 나타납니다.

Sarah는 &quot;Your Auto Insurance Renewal&quot;이라는 제목으로 이메일을 받았다.

![에이전트 UI](assets/agent_ui_email_new.png)

#### 직접 보기 {#see-it-yourself}

Adobe Experience **Manager >** 양식 **>** 양식 **및 문서** > **We.Finance** > Adobe ****&#x200B;자동 보험으로 이동합니다. 자동 보험 갱신 **대화형 통신을** 선택하고 에이전트 UI **열기를 클릭합니다**. 대화형 통신이 에이전트 UI에서 열립니다. 첨부된 정책 문서가 포함된 이메일을 수신할 유효한 이메일 주소를 입력하고 제출을 클릭합니다.

귀하는 `https://[authorHost]: authorPort]/aem/formdetails.html/content/dam/formsanddocuments/we-finance/autoinsurance/auto-insurance-renewal.`

### 새라는 We.Finance로부터 보험 증권 갱신 통신을 받고 갱신하기로 결정했다 {#sarah-receives-an-insurance-policy-renewal-communication-from-we-finance-and-decides-to-renew}

새라는 그녀의 자동차 보험 정책이 곧 만료될 것이라는 것을 알려주는 We.Finance로부터 첨부 파일로 이메일을 받았다. 첨부파일은 그녀의 자동차 보험 서신의 인쇄본이다.

Sarah **는 지금** 갱신을 클릭하고 자신의 자동차 보험 서신의 웹 버전으로 보내진다. 이 편지 위에, 사라는 자신의 정책이 만료될 때까지 남은 일수를 찾았다. 이 페이지에서는 Sarah에게 정책 번호, 만기일, 그리고 할인 혜택 및 충성도 보상과 같은 기타 정보와 같은 그녀의 보험 정책 세부 사항에 대한 기본적인 개요를 제공합니다. Sarah **는 정책** 하단의 Renew Now를 다시 클릭합니다.

![ref1](assets/ref1.png)

#### 작동 방식 {#how-it-works}

자동 보험 서신의 웹 및 인쇄 출력은 인터랙티브 커뮤니케이션의 다중 채널 기능을 사용하여 만들어집니다.

이메일의 지금 갱신 단추는 게시 인스턴스의 대화형 통신인 자동 보험 갱신 응용 프로그램에 연결됩니다.

#### 직접 보기 {#see-it-yourself-1}

PDF가 첨부된 이메일을 수신해야 합니다. PDF는 자동 보험 서신의 인쇄 버전입니다. 지금 **갱신을** 클릭하여 정책의 웹 버전에 연결합니다. 개인 정보 및 정책 세부 사항을 확인하고 지금 **갱신을** 클릭하면 다른 인터랙티브 커뮤니케이션으로 이동합니다.

이메일의 **지금** 갱신 단추는 Sarah에게 정책의 웹 버전으로 안내한다. 다음 URL을 방문할 수 있습니다.

`https://[authorServer]:[authorPort]/content/document.html?schema=fdm&documentId=/content/forms/af/we-finance/autoinsurance/auto-insurance-renewal/channels/web.html&customerId=1`

자동 보험 갱신에 대한 자세한 요약을 확인하고 페이지 **하단에서 지금** 갱신을 클릭합니다.

### 사라는 지불 페이지에 도달한다 {#sarah-reaches-the-payment-page}

We.Finance takes Sarah to the Payment page. 사라는 자신의 정책 번호와 유통기한 을 기록하여 다시 확인한다. 페이지 오른쪽에서는 총 금액에 대해 10% 할인이 적용되는 갱신의 지불 요약을 확인합니다.

#### 작동 방식 {#how-it-works-1}

지금 갱신 단추를 누르면 사라가 결제 페이지로 이동합니다. 결제 페이지는 적응형 양식입니다.

#### 직접 보기 {#see-it-yourself-2}

지금 **갱신을** 클릭하여 지불 페이지로 이동합니다. 신용 카드 정보를 입력하고 결제 **만들기를 클릭합니다**.

작성 인스턴스에서 결제 페이지에 도달할 수 있습니다.

`https://[authorServer]:[authorPort]/content/document.html?documentId=/content/forms/af/we-finance/credit-card/ccbillpayment.html&schema=fdm&customerId=1`

### 사라가 돈을 지불해서 절차를 완료하세요 {#sarah-makes-the-payment-and-completes-the-process}

Sarah는 신용카드 세부 사항을 작성하고 결제 **만들기를 클릭합니다**.

#### 작동 방식 {#how-it-works-2}

Sarah가 신용 카드 세부 사항을 채우고 [제출]을 클릭하면 신용 카드 결제가 처리되고 응용 양식에 구성된 감사 메시지가 화면에 나타납니다.

#### 직접 보기 {#see-it-yourself-3}

결제를 클릭한 후 확인 메시지를 볼 수 있습니다.

`https://[authorServer]:[authorPort]/content/forms/af/we-finance/credit-card/ccbillpayment/jcr:content/guideContainer.guideThankYouPage.html?owner=admin&status=Submitted`
