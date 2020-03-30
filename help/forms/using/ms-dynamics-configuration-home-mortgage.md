---
title: We.Finance 참조 사이트의 홈 모기지 워크플로우에 대한 Microsoft Dynamics 365 구성
seo-title: We.Finance 참조 사이트의 홈 모기지 워크플로우에 대한 Microsoft Dynamics 365 구성
description: We.Finance 참조 사이트의 홈 모기지 워크플로우에 적응형 양식을 통해 Microsoft® Dynamics 365 서비스를 활용하는 방법을 살펴보십시오
seo-description: We.Finance 참조 사이트의 홈 모기지 워크플로우에 적응형 양식을 통해 Microsoft® Dynamics 365 서비스를 활용하는 방법을 살펴보십시오
uuid: a0656d90-84c7-46d1-9a16-dadcc19ff9ef
products: SG_EXPERIENCEMANAGER/6.3/FORMS
topic-tags: Configuration
discoiquuid: 6b31397a-fb06-4043-9368-59fb4fce8afa
translation-type: tm+mt
source-git-commit: f323b490c37effc3cbb36c793b62fa788eca9545

---


# We.Finance 참조 사이트의 홈 모기지 워크플로우에 대한 Microsoft Dynamics 365 구성 {#configure-microsoft-dynamics-for-the-home-mortgage-workflow-of-the-we-finance-reference-site}

We.Finance 참조 사이트의 홈 모기지 워크플로우에 적응형 양식을 통해 Microsoft® Dynamics 365 서비스를 활용하는 방법을 살펴보십시오

## 개요 {#overview}

Microsoft® Dynamics 365는 고객 계정, 연락처, 리드, 기회 및 사례를 만들고 관리하기 위한 엔터프라이즈 솔루션을 제공하는 CRM(Customer Relationship Management) 및 ERP(Enterprise Resource Planning) 소프트웨어입니다.

AEM Forms는 Dynamics 365를 양식 데이터 통합 [모듈과 통합하는 클라우드 서비스를](/help/forms/using/data-integration.md) 제공합니다. Microsoft® [Dynamics의 Home Mortgage 애플리케이션](/help/forms/using/finance-reference-site-walkthrough.md#home-mortgage-application-walkthrough-with-microsoft-dynamics) 연습 시나리오는 고객이 We.Finance 참조 사이트를 사용하여 사이트에서 Microsoft® Dynamics for Forms Data Integration을 사용할 때 대출을 신청하는 방법을 보여줍니다. Microsoft® Dynamics 시나리오에서 Home Mortgage 애플리케이션 연습을 사용하려면 Microsoft® Dynamics 365를 We.Finance 참조 사이트와 함께 사용하도록 구성해야 합니다.

## 전제 조건 {#prerequisites}

Dynamics 365를 설정하고 구성하기 전에 다음을 보유하십시오.

* [AEM Forms 참조 사이트를](/help/forms/using/setup-reference-sites.md)설정하고 구성합니다.

* AEM 6.3 양식 서비스 팩 1 이상
* Microsoft® Dynamics 365 계정
* Microsoft® Azure Active Directory와 함께 Dynamics 365 서비스에 등록된 응용 프로그램
* 등록된 응용 프로그램의 클라이언트 ID 및 클라이언트 암호

## 가정용 주택 담보 대출 계산기를 사이트 홈 페이지에 연결 {#link-the-home-mortgage-calculator-with-your-site-home-page}

1. 작성 인스턴스에서 다음 페이지로 이동합니다.

   `https://[server]:[port]/editor.html/content/we-finance/global/en/loan-landing-page.html`

1. Home Mortgage 계산기로 스크롤합니다.
1. 오른쪽 열(계산기) 패널을 강조 표시한 다음 을 눌러 팝업 메뉴를 표시합니다. 팝업 메뉴에서 구성을 누릅니다. AEM 양식 컨테이너 편집 대화 상자가 나타납니다.

   ![calculateconfigurepanel](assets/calculatorconfigurepanel.png)

1. AEM Forms 컨테이너 편집 대화 상자에서 자산 경로를 탐색하고 다음 경로에서 홈 모기지 계산기를 선택하고 확인을 **누릅니다**.

   formsanddocuments/We.Finance/MS Dynamics/

   ![selectassetpath](assets/selectassetpath.png)

1. **Done**&#x200B;을 누릅니다.
1. 편집된 페이지를 게시합니다.

   >[!NOTE]
   >
   >FDM과 계산기 필드의 바인딩은 We.Finance 참조 사이트 패키지를 통해 미리 구성됩니다. 바인딩을 보려면 작성 모드에서 양식을 열고 필드 바인딩 참조를 볼 수 있습니다.

1. 가정용 주택 담보 대출 응용 프로그램의 신청자 레코드를 저장할 사용자 지정 엔티티를 만들려면 AEMFormsFSIRefsite_1_0.zip 솔루션 패키지를 Microsoft® Dynamics 인스턴스로 가져옵니다.

   1. 다음 위치에서 패키지를 다운로드합니다.

      `https://'[server]:[port]'/content/aemforms-refsite-collaterals/we-finance/home-mortgage/ms-dynamics/AEMFormsFSIRefsite_1_0.zip`

   1. 솔루션 패키지를 Microsoft® Dynamics 인스턴스로 가져옵니다. Microsoft® Dynamics 인스턴스에서 설정 > **솔루션으로** 이동한 **다음** 가져오기를 **누릅니다**.

1. refsite에 사용된 사용자 연락처 세부 사항을 설정하려면 Sarah Rose Contact.CSV 패키지를 Microsoft® Dynamics 인스턴스로 가져옵니다.

   1. 다음 위치에서 패키지를 다운로드합니다.

      `https://'[server]:[port]'/content/aemforms-refsite-collaterals/we-finance/home-mortgage/ms-dynamics/Sarah%20Rose%20Contact.csv`

   1. 패키지를 Microsoft® Dynamics 인스턴스로 가져옵니다. Microsoft® Dynamics 인스턴스에서 판매 > **연락처로** 이동한 **다음** 데이터 **가져오기를**&#x200B;누릅니다.

