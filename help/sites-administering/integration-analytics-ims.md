---
title: IMS를 사용하여 Adobe Analytics과 통합
description: IMS를 사용하여 AEM과 Adobe Analytics 통합에 대해 알아보기
exl-id: 2833a6df-ef32-48ab-8395-0f26816f8443
source-git-commit: 259f257964829b65bb71b5a46583997581a91a4e
workflow-type: tm+mt
source-wordcount: '1057'
ht-degree: 65%

---


# IMS를 사용하여 Adobe Analytics과 통합 {#integration-with-adobe-analytics-using-ims}

Analytics Standard API를 통해 Adobe Analytics과 AEM을 통합하려면 Adobe Developer 콘솔을 사용하여 Adobe IMS(Identity Management 시스템)를 구성해야 합니다.

>[!NOTE]
>
>Adobe Analytics Standard API 2.0 지원은 AEM 6.5.12.0의 새로운 기능입니다. 이 API 버전은 IMS 인증을 지원합니다.
>
>이전 버전과의 호환성을 위해 AEM에서 Adobe Analytics Classic API 1.4 사용이 여전히 지원됩니다. 다음 [Analytics Classic API는 사용자 자격 증명 인증을 사용합니다](/help/sites-administering/adobeanalytics-connect.md).
>
>API 선택은 AEM/Analytics 통합에 사용되는 인증 방법에 따라 결정됩니다.
>
>자세한 내용은 [2.0 API로 마이그레이션](https://developer.adobe.com/analytics-apis/docs/2.0/guides/migration/)에서도 찾을 수 있습니다.

## 사전 요구 사항 {#prerequisites}

이 절차를 시작하기 전에:

* [Adobe 지원 팀](https://helpx.adobe.com/contact/enterprise-support.ec.html)은 다음에 대한 계정을 프로비저닝해야 합니다.

   * Adobe Console
   * Adobe Developer Console
   * Adobe Analytics 및
   * Adobe IMS(ID 관리 시스템)

* 조직의 시스템 관리자는 Admin Console을 사용하여 필요한 조직 개발자를 관련 제품 프로필에 추가해야 합니다.

   * 이렇게 하면 특정 개발자에게 Adobe Developer 콘솔 내에서 통합을 활성화할 수 있는 권한이 제공됩니다.
   * 자세한 내용은 [개발자 관리](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/manage-developers.ug.html)를 참조하십시오.


## IMS 구성 - 공개 키 생성 {#configuring-an-ims-configuration-generating-a-public-key}

구성의 첫 단계는 AEM에서 IMS 구성을 만들고 공개 키를 생성하는 것입니다.

1. AEM에서 **도구** 메뉴를 엽니다.
1. **보안** 섹션에서 **Adobe IMS 구성**&#x200B;을 선택합니다.
1. **만들기**&#x200B;를 선택하여 **Adobe IMS 기술 계정 구성**&#x200B;을 엽니다.
1. **클라우드 구성** 아래의 드롭다운을 사용하여 **Adobe Analytics**&#x200B;를 선택합니다.
1. **새 인증서 만들기**&#x200B;를 활성화한 다음 새 별칭을 입력합니다.
1. **인증서 만들기**&#x200B;를 사용하여 확인합니다.

   ![Adobe IMS 기술 계정 구성 마법사](assets/integrate-analytics-io-01.png)

1. **다운로드**(또는 **공개 키 다운로드**)를 선택하여 [AEM과의 Adobe Analytics 통합에 대해 IMS를 구성](#configuring-ims-for-adobe-analytics-integration-with-aem)할 때 사용할 수 있도록 파일을 로컬 드라이브에 다운로드합니다.

   >[!CAUTION]
   >
   >[AEM에서 IMS 구성을 완료](#completing-the-ims-configuration-in-aem)할 때 다시 필요하므로 이 구성을 열어 두십시오.

   ![Adobe I/O 키를 추가하는 정보 대화 상자](assets/integrate-analytics-io-02.png)

## AEM과의 Adobe Analytics 통합에 대해 IMS 구성 {#configuring-ims-for-adobe-analytics-integration-with-aem}

Adobe Developer Console을 사용하여 AEM이 사용할 Adobe Analytics로 프로젝트(통합)을 만든 다음 필요한 권한을 할당해야 합니다.

### 프로젝트 만들기 {#creating-the-project}

Adobe Developer Console을 열고 AEM이 사용할 Adobe Analytics를 사용하여 프로젝트를 만듭니다.

1. 프로젝트용 Adobe Developer Console을 엽니다.

   [https://developer.adobe.com/console/projects](https://developer.adobe.com/console/projects)

1. 보유 중인 모든 프로젝트가 표시됩니다. **새 프로젝트 만들기**&#x200B;를 선택합니다. 위치 및 사용량은 다음에 따라 달라집니다.

   * 보유 중인 프로젝트가 없는 경우 **새 프로젝트 만들기**는 중앙 하단에 표시됩니다.
     ![새 프로젝트 만들기 - 첫 번째 프로젝트](assets/integration-analytics-io-02.png)
   * 기존 프로젝트가 있는 경우 이들 프로젝트가 나열되며 **새 프로젝트 만들기**는 오른쪽 상단에 표시됩니다.
     ![새 프로젝트 만들기 - 여러 프로젝트](assets/integration-analytics-io-03.png)


1. **프로젝트에 추가**&#x200B;를 선택한 다음 **API**&#x200B;를 선택합니다.

   ![새 프로젝트 시작하기](assets/integration-analytics-io-10.png)

1. **Adobe Analytics**&#x200B;를 선택하고 **다음**&#x200B;을 선택합니다.

   >[!NOTE]
   >
   >Adobe Analytics을 구독하지만 나열되지 않는 경우 [전제 조건](#prerequisites).

   ![API 추가](assets/integration-analytics-io-12.png)

1. 인증 유형으로 **서비스 계정(JWT)**&#x200B;을 선택하고 **다음**&#x200B;을 사용하여 계속합니다.

   ![인증 유형 선택](assets/integration-analytics-io-12a.png)

1. **공개 키를 업로드**&#x200B;한 다음 완료되면 **다음**&#x200B;을 사용하여 계속합니다.

   ![공개 키 업로드](assets/integration-analytics-io-13.png)

1. 자격 증명을 검토하고 **다음**&#x200B;을 사용하여 계속합니다.

   ![자격 증명 검토](assets/integration-analytics-io-15.png)

1. 필요한 제품 프로필을 선택한 다음 **구성된 API 저장**&#x200B;을 사용하여 계속합니다.

   ![필요한 제품 프로필 선택](assets/integration-analytics-io-16.png)

1. 구성이 확인됩니다.

### 통합에 권한 할당 {#assigning-privileges-to-the-integration}

이제 필요한 권한을 통합에 할당해야 합니다.

1. Adobe **Admin Console**&#x200B;을 엽니다.

   * [https://adminconsole.adobe.com](https://adminconsole.adobe.com/)

1. **제품**&#x200B;으로 이동한 다음(상단 도구 모음) 왼쪽 패널에서 **Adobe Analytics - &lt;*테넌트 ID*>**&#x200B;을(를) 선택합니다.
1. **제품 프로필**&#x200B;을 선택한 다음 표시되는 목록에서 필요한 작업 영역을 선택합니다. (예: 기본 작업 영역)
1. **API 자격 증명**&#x200B;을 선택한 다음 필요한 통합 구성을 선택합니다.
1. **제품 역할**&#x200B;을 **관찰자**&#x200B;가 아닌 **편집자**&#x200B;로 선택합니다.

## 저장된 Adobe Developer Console 통합 프로젝트 세부 정보 {#details-stored-for-the-ims-integration-project}

Adobe Developer 프로젝트 콘솔에서 모든 통합 프로젝트 목록을 볼 수 있습니다.

* [https://developer.adobe.com/console/projects](https://developer.adobe.com/console/projects)

구성에 대한 세부 정보를 표시하려면 특정 프로젝트 항목을 선택합니다. 여기에는 다음이 포함됩니다.

* 프로젝트 개요
* 인사이트
* 자격 증명
   * 서비스 계정(JWT)
      * 자격 증명 세부 정보
      * JWT 생성
* API
   * (예: Adobe Analytics)

이 중 일부는 AEM에서 Adobe Analytics에 대한 통합을 완료해야 합니다.

## AEM에서 IMS 구성 완료 {#completing-the-ims-configuration-in-aem}

AEM으로 돌아가 Analytics용 통합 프로젝트에서 필요한 값을 추가하여 IMS 구성을 완료할 수 있습니다.

1. [AEM에서 열려 있는 IMS 구성](#configuring-an-ims-configuration-generating-a-public-key)으로 돌아갑니다.
1. **다음**&#x200B;을 선택합니다.

1. 여기에서 [Adobe Developer 콘솔 통합 프로젝트에 대해 저장된 세부 정보](#details-stored-for-the-ims-integration-project):

   * **제목**: 텍스트를 입력하십시오.
   * **인증 서버**: 아래 `aud`페이로드&#x200B;**섹션의** 줄에서 이 인증 서버를 복사하여 붙여넣습니다(아래 예에서 `https://ims-na1.adobelogin.com`).
   * **API 키**: [프로젝트 개요](#details-stored-for-the-ims-integration-project)의 **자격 증명** 섹션에서 이 API 키를 복사합니다.
   * **클라이언트 보안**: [서비스 계정(JWT) 섹션의 클라이언트 보안 탭](#details-stored-for-the-ims-integration-project)에서 이 클라이언트 보안을 생성한 다음 복사합니다.
   * **페이로드**: [서비스 계정(JWT) 섹션의 JWT 생성 탭](#details-stored-for-the-ims-integration-project)에서 이 페이로드를 복사합니다.

   ![AEM IMS 구성 세부 정](assets/integrate-analytics-io-10.png)

1. **만들기**&#x200B;를 사용하여 확인합니다.

1. AEM 콘솔에 Adobe Analytics 구성이 표시됩니다.

   ![IMS 구성](assets/integrate-analytics-io-11.png)

## IMS 구성 확인 {#confirming-the-ims-configuration}

구성이 예상대로 작동하는지 확인하려면 다음 작업을 수행하십시오.

1. 열기:

   * `https://localhost<port>/libs/cq/adobeims-configuration/content/configurations.html`

   예:

   * `https://localhost:4502/libs/cq/adobeims-configuration/content/configurations.html`

1. 구성을 선택합니다.
1. 도구 모음에서 **상태 확인**&#x200B;을 선택한 다음 **확인**&#x200B;을 선택합니다.

   ![IMS 구성 - 상태 확인](assets/integrate-analytics-io-12.png)

1. 성공하면 확인 메시지가 표시됩니다.

## Adobe Analytics Cloud 서비스 구성 {#configuring-the-adobe-analytics-cloud-service}

이제 Cloud Service이 Analytics Standard API를 사용하도록 구성을 참조할 수 있습니다.

1. 를 엽니다. **도구** 메뉴 아래의 제품에서 사용할 수 있습니다. 그런 다음 **Cloud Services** 섹션, 선택 **이전 Cloud Services**.
1. 아래로 스크롤하여 **Adobe Analytics** 및 선택 **지금 구성**.

   다음 **구성 만들기** 대화 상자가 열립니다.

1. 입력 **제목** 그리고, 원한다면 **이름** (비워 두면 제목에서 생성됩니다.)

   필요한 템플릿을 선택할 수도 있습니다(둘 이상의 템플릿을 사용할 수 있는 경우).

1. **만들기**&#x200B;를 사용하여 확인합니다.

   다음 **구성 요소 편집** 대화 상자가 열립니다.

1. 다음에 세부 정보를 입력합니다. **Analytics 설정** 탭:

   * **인증**: IMS

   * **IMS 구성**: IMS 구성의 이름을 선택합니다

1. 클릭 **Analytics에 연결** Adobe Analytics에 대한 연결을 초기화합니다.

   정상적으로 연결되면 **연결 성공**&#x200B;이라는 메시지가 표시됩니다.

1. 선택 **확인** 메시지를 표시합니다.

1. 필요에 따라 다른 매개 변수를 완료하고 다음을 수행합니다. **확인** 대화 상자에서 구성을 확인합니다.

1. 이제 다음으로 진행할 수 있습니다. [Analytics 프레임워크 추가](/help/sites-administering/adobeanalytics-connect.md) Adobe Analytics으로 전송할 매개 변수를 구성합니다.
