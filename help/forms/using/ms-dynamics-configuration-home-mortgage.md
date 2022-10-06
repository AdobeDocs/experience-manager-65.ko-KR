---
title: We.Finance 참조 사이트의 홈 모기지 워크플로우에 대한 Microsoft Dynamics 365를 구성합니다
seo-title: Configure Microsoft Dynamics 365 for the home mortgage workflow of the We.Finance reference site
description: We.Finance 참조 사이트의 주택 융자 작업 과정을 위한 적응형 양식을 통해 Microsoft® Dynamics 365 서비스를 활용하는 방법을 알아봅니다
seo-description: Learn how to leverage the Microsoft® Dynamics 365 services through adaptive forms for the home mortgage workflow of the We.Finance Reference site
uuid: a0656d90-84c7-46d1-9a16-dadcc19ff9ef
products: SG_EXPERIENCEMANAGER/6.3/FORMS
topic-tags: develop, Configuration
discoiquuid: 6b31397a-fb06-4043-9368-59fb4fce8afa
exl-id: 2ac37dc5-d88d-4f98-8576-cd2ca6f0ea3a
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '398'
ht-degree: 1%

---

# We.Finance 참조 사이트의 홈 모기지 워크플로우에 대한 Microsoft Dynamics 365를 구성합니다 {#configure-microsoft-dynamics-for-the-home-mortgage-workflow-of-the-we-finance-reference-site}

We.Finance 참조 사이트의 주택 융자 작업 과정을 위한 적응형 양식을 통해 Microsoft® Dynamics 365 서비스를 활용하는 방법을 알아봅니다

## 개요 {#overview}

Microsoft® Dynamics 365는 고객 계정, 연락처, 리드, 기회 및 사례를 만들고 관리하는 엔터프라이즈 솔루션을 제공하는 CRM(고객 관계 관리) 및 ERP(Enterprise Resource Planning) 소프트웨어입니다.

AEM Forms은 Dynamics 365를 와 통합하는 클라우드 서비스를 제공합니다 [Forms 데이터 통합](/help/forms/using/data-integration.md) 모듈. Microsoft® Dynamics 시나리오와 함께 홈 모기지 애플리케이션 연습을 사용하려면 먼저 We.Finance 참조 사이트에서 사용할 Microsoft® Dynamics 365를 구성해야 합니다.

## 사전 요구 사항 {#prerequisites}

Dynamics 365를 설정하고 구성하기 전에 다음 내용이 있는지 확인하십시오.

* AEM 6.3 Forms 서비스 팩 1 이상
* Microsoft® Dynamics 365 계정
* Microsoft® Azure Active Directory를 사용하여 Dynamics 365 서비스에 등록된 응용 프로그램
* 등록된 응용 프로그램의 클라이언트 ID 및 클라이언트 암호

## 홈 모기지 계산기를 사이트 홈 페이지에 연결합니다 {#link-the-home-mortgage-calculator-with-your-site-home-page}

1. 작성자 인스턴스에서 다음 페이지로 이동합니다.

   `https://[server]:[port]/editor.html/content/we-finance/global/en/loan-landing-page.html`

1. 홈 모기지 계산기로 스크롤합니다.
1. 오른쪽 열의(계산기) 패널을 강조 표시하고 탭하여 팝업 메뉴를 표시합니다. 팝업 메뉴에서 구성 을 누릅니다. AEM Forms 컨테이너 편집 대화 상자가 나타납니다.

   ![calculateorconfigurepanel](assets/calculatorconfigurepanel.png)

1. AEM Forms 컨테이너 편집 대화 상자에서 자산 경로를 탐색하고 다음 경로에서 홈 모기지 계산기를 선택하고 를 탭합니다 **확인**:

   formsanddocuments/We.Finance/MS Dynamics/

   ![selectassetpath](assets/selectassetpath.png)

1. **Done**&#x200B;을 누릅니다.
1. 편집한 페이지를 게시합니다.

   >[!NOTE]
   >
   >We.Finance 참조 사이트 패키지를 통해 계산기 필드의 바인딩이 FDM과 미리 구성되어 있습니다. 바인딩을 보려면 작성 모드에서 양식을 열고 필드 바인딩 참조를 볼 수 있습니다.

1. 주택 담보 융자 응용 프로그램에 대한 지원자 레코드를 저장할 사용자 정의 엔티티를 생성하려면 AEMFormsFSIRefsite_1_0.zip 솔루션 패키지를 Microsoft® Dynamics 인스턴스로 가져옵니다.

   1. 다음 위치에서 패키지를 다운로드합니다.

      `https://'[server]:[port]'/content/aemforms-refsite-collaterals/we-finance/home-mortgage/ms-dynamics/AEMFormsFSIRefsite_1_0.zip`

   1. 솔루션 패키지를 Microsoft® Dynamics 인스턴스로 가져옵니다. Microsoft® Dynamics 인스턴스에서 다음 위치로 이동합니다. **설정** > **솔루션** 그런 다음 **가져오기**.

1. 레퍼사이트에서 사용되는 사용자 연락처 세부 사항을 설정하려면 Sarah Rose Contact.CSV 패키지를 Microsoft® Dynamics 인스턴스로 가져옵니다.

   1. 다음 위치에서 패키지를 다운로드합니다.

      `https://'[server]:[port]'/content/aemforms-refsite-collaterals/we-finance/home-mortgage/ms-dynamics/Sarah%20Rose%20Contact.csv`

   1. Microsoft® Dynamics 인스턴스로 패키지를 가져옵니다. Microsoft® Dynamics 인스턴스에서 다음 위치로 이동합니다. **영업** > **연락처** 그런 다음 **데이터 가져오기**.
