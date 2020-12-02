---
title: Adobe I/O을 사용한 Adobe Target 통합
seo-title: Adobe I/O을 사용한 Adobe Target 통합
description: Adobe I/O을 사용하여 AEM과 Adobe Target 통합에 대한 자세한 내용
seo-description: Adobe I/O을 사용하여 AEM과 Adobe Target 통합에 대한 자세한 내용
uuid: dd4ed638-e182-4d7e-9c98-282431812467
contentOwner: aheimoz
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: integration
discoiquuid: 3b9285db-8fba-4d12-8f52-41daa50a5403
docset: aem65
translation-type: tm+mt
source-git-commit: 26efba567985dcb89b2610935cab18943b7034b3
workflow-type: tm+mt
source-wordcount: '1335'
ht-degree: 1%

---


# Adobe I/O{#integration-with-adobe-target-using-adobe-i-o}을(를) 사용하여 Adobe Target과 통합

Target Standard API를 통해 AEM과 Adobe Target을 통합하려면 Adobe IMS(Identity Management 시스템) 및 Adobe I/O을 구성해야 합니다.

>[!NOTE]
>
>AEM 6.5에서는 Adobe Target 표준 API에 대한 지원이 새롭게 도입되었습니다. Target 표준 API는 IMS 인증을 사용합니다.
>
>AEM에서 Adobe Target Classic API를 사용해도 이전 버전과의 호환성이 지원됩니다. [Target 클래식 API는 사용자 자격 증명 인증](/help/sites-administering/target-configuring.md#manually-integrating-with-adobe-target)을 사용합니다.
>
>API 선택은 AEM/Target 통합에 사용되는 인증 방법에 의해 결정됩니다.

## 전제 조건 {#prerequisites}

이 절차를 시작하기 전:

* [Adobe ](https://helpx.adobe.com/kr/contact/enterprise-support.ec.html) 지원계정 제공:

   * Adobe 콘솔
   * Adobe I/O
   * Adobe Target
   * Adobe IMS(Identity Management 시스템)

* 조직의 시스템 관리자는 Admin Console을 사용하여 조직의 필수 개발자를 관련 제품 프로필에 추가해야 합니다.

   * 이를 통해 특정 개발자에게 Adobe I/O 내의 통합을 활성화할 수 있는 권한을 제공합니다.
   * 자세한 내용은 [개발자 관리](https://helpx.adobe.com/enterprise/admin-guide.html/enterprise/using/manage-developers.ug.html)를 참조하십시오.


## IMS 구성 구성 - 공개 키 생성 {#configuring-an-ims-configuration-generating-a-public-key}

구성의 첫 번째 단계는 AEM에서 IMS 구성을 만들고 공개 키를 생성하는 것입니다.

1. AEM에서 **도구** 메뉴를 엽니다.
1. **보안** 섹션에서 **Adobe IMS 구성**&#x200B;을 선택합니다.
1. **만들기**&#x200B;를 선택하여 **Adobe IMS를 엽니다. 기술 계정 구성**.
1. **클라우드 구성** 아래의 드롭다운을 사용하여 **Adobe Target**&#x200B;을 선택합니다.
1. **새 인증서**&#x200B;를 활성화하고 새 별칭을 입력합니다.
1. **인증서 만들기**&#x200B;로 확인합니다.

   ![](assets/integrate-target-io-01.png)

1. **다운로드**(또는 **공개 키 다운로드**)를 선택하여 파일을 로컬 드라이브에 다운로드합니다. 이렇게 하면 AEM](#configuring-adobe-i-o-for-adobe-target-integration-with-aem)와 Adobe Target 통합을 위해 Adobe I/O을 구성할 때 사용할 준비가 됩니다.[

   >[!CAUTION]
   >
   >이 구성을 열어 두십시오. 이 구성은 AEM](#completing-the-ims-configuration-in-aem)에서 IMS 구성을 완료할 때 다시 필요합니다.[

   ![](assets/integrate-target-io-02.png)

## AEM {#configuring-adobe-i-o-for-adobe-target-integration-with-aem}과의 Adobe Target 통합을 위해 Adobe I/O 구성

AEM에서 사용할 Adobe Target과 Adobe I/O 프로젝트(통합)를 만든 다음 필요한 권한을 할당해야 합니다.

### 프로젝트 {#creating-the-project} 만들기

Adobe I/O 콘솔을 열어 AEM에서 사용할 Adobe Target과 함께 I/O 프로젝트를 만듭니다.

>[!NOTE]
>
>[Adobe I/O 자습서](https://www.adobe.io/apis/experienceplatform/home/tutorials/alltutorials.html)도 참조하십시오.

1. 프로젝트를 위한 Adobe I/O 콘솔을 엽니다.

   [https://console.adobe.io/projects](https://console.adobe.io/projects)

1. 보유한 모든 프로젝트가 표시됩니다. **새 프로젝트 만들기**&#x200B;를 선택합니다. 위치 및 사용량은 다음에 따라 다릅니다.

   * 아직 프로젝트가 없는 경우 **새 프로젝트 만들기**가 가운데, 아래에 있게 됩니다.
      ![새 프로젝트 만들기 - 첫 번째 프로젝트](assets/integration-target-io-02.png)
   * 기존 프로젝트가 이미 있는 경우 목록이 표시되고 **새 프로젝트 만들기**가 오른쪽 상단에 표시됩니다.
      ![새 프로젝트 만들기 - 여러 프로젝트](assets/integration-target-io-03.png)


1. **프로젝트에 추가** 뒤에 **API**&#x200B;를 선택합니다.

   ![](assets/integration-target-io-10.png)

1. **Adobe Target**&#x200B;을 선택한 다음 **다음**&#x200B;을 선택합니다.

   >[!NOTE]
   >
   >Adobe Target에 가입했지만 목록에 표시되지 않는 경우 [Prerequirements](#prerequisites)을 확인해야 합니다.

   ![](assets/integration-target-io-12.png)

1. **공개 키를 업로드하고** 완료되면 다음을  **계속 진행합니다**.

   ![](assets/integration-target-io-13.png)

1. 자격 증명을 검토하고 **다음**&#x200B;으로 계속 진행합니다.

   ![](assets/integration-target-io-15.png)

1. 필요한 제품 프로필을 선택하고 **구성된 API 저장**&#x200B;으로 계속합니다.

   >[!NOTE]
   >
   >표시되는 제품 프로필은 다음 항목에 따라 다릅니다.
   >
   >* Adobe Target 표준 - **기본 작업 공간**&#x200B;만 사용 가능
   >* Adobe Target Premium - 사용 가능한 모든 작업 영역이 아래에 나와 있습니다.


   ![](assets/integration-target-io-16.png)

1. 그 창조는 확인될 것이다.

<!--
1. The creation will be confirmed, you can now **Continue to integration details**; these are needed for [Completing the IMS Configuration in AEM](#completing-the-ims-configuration-in-aem).

   ![](assets/integrate-target-io-07.png)
-->

### 통합 {#assigning-privileges-to-the-integration}에 권한 할당

이제 필요한 권한을 통합에 할당해야 합니다.

1. Adobe **Admin Console**&#x200B;을 엽니다.

   * [https://adminconsole.adobe.com](https://adminconsole.adobe.com/)

1. **제품**(위쪽 도구 모음)으로 이동한 다음 **Adobe Target - &lt;*your-tenant-id***(왼쪽 패널)을 선택합니다.
1. **제품 프로필**&#x200B;을 선택한 다음 목록의 필수 작업 공간을 선택합니다. 예: 기본 작업 공간.
1. **통합**&#x200B;을 선택한 다음 필요한 통합 구성을 선택합니다.
1. **편집기**&#x200B;를 **제품 역할**;대신 사용할 수 있습니다.****

## Adobe I/O 통합 프로젝트 {#details-stored-for-the-adobe-io-integration-project}에 대해 저장된 세부 정보

Adobe I/O 프로젝트 콘솔에서 모든 통합 프로젝트 목록을 볼 수 있습니다.

* [https://console.adobe.io/projects](https://console.adobe.io/projects)

구성에 대한 자세한 내용을 보려면 **특정 프로젝트 항목의 오른쪽에 있는 보기**&#x200B;를 선택합니다. 이러한 쿠키에는 다음이 포함됩니다.

* 프로젝트 개요
* 인사이트
* 자격 증명
   * 서비스 계정(JWT)
      * 자격 증명 세부 정보
      * JWT 생성
* APIS
   * 예를 들어, Adobe Target

이러한 기능 중 일부는 AEM의 Target에 대한 Adobe I/O 통합을 완료해야 합니다.

## AEM {#completing-the-ims-configuration-in-aem}에서 IMS 구성 완료

AEM으로 돌아가면 Target에 대한 Adobe I/O 통합에서 필요한 값을 추가하여 IMS 구성을 완료할 수 있습니다.

1. [IMS로 돌아갑니다. 구성이 AEM](#configuring-an-ims-configuration-generating-a-public-key)에서 열립니다.
1. **다음**&#x200B;을 선택합니다.

1. 여기에서 Adobe I/O](#details-stored-for-the-adobe-io-integration-project)의 [세부 정보를 사용할 수 있습니다.

   * **제목**:텍스트.
   * **인증 서버**:아래 Payloadsection의  `"aud"` 줄(예: 아래  **** 예제 `"https://ims-na1.adobelogin.com"` 에서)에서 이 파일을 복사하거나 붙여 넣습니다.
   * **API 키**:Target용 Adobe I/O  [](#details-stored-for-the-adobe-io-integration-project) 통합의 개요 섹션에서 복사
   * **클라이언트 암호**:Target에 대한 Adobe I/O  [](#details-stored-for-the-adobe-io-integration-project) 통합의 개요 섹션에서 이를 생성하고 복사합니다.
   * **페이로드**:Target용 Adobe I/O  [통합의 ](#details-stored-for-the-adobe-io-integration-project) JWT 생성 섹션에서 복사합니다.

   ![](assets/integrate-target-io-10.png)

1. **만들기**&#x200B;로 확인합니다.

1. Adobe Target 구성이 AEM 콘솔에 표시됩니다.

   ![](assets/integrate-target-io-11.png)

## IMS 구성 확인 {#confirming-the-ims-configuration}

구성이 예상대로 작동하는지 확인하려면:

1. 열기:

   * `https://localhost<port>/libs/cq/adobeims-configuration/content/configurations.html`

   예:

   * `https://localhost:4502/libs/cq/adobeims-configuration/content/configurations.html`


1. 구성을 선택합니다.
1. 도구 모음에서 **상태 확인**&#x200B;을 선택하고 **확인**&#x200B;을 선택합니다.

   ![](assets/integrate-target-io-12.png)

1. 성공하면 다음과 같은 메시지가 표시됩니다.

   ![](assets/integrate-target-io-13.png)

## Adobe Target Cloud Service {#configuring-the-adobe-target-cloud-service} 구성

이제 Cloud Service에서 Target Standard API를 사용하도록 구성을 참조할 수 있습니다.

1. **도구** 메뉴를 엽니다. 그런 다음 **Cloud Services** 섹션 내에서 **기존 Cloud Services**&#x200B;을 선택합니다.
1. **Adobe Target**&#x200B;으로 스크롤하고 **지금 구성**&#x200B;을 선택합니다.

   **구성 만들기** 대화 상자가 열립니다.

1. **제목**&#x200B;을 입력하고 필요한 경우 **이름**(비워 두면 제목에서 생성됩니다.)

   필요한 템플릿을 선택할 수도 있습니다(두 개 이상의 템플릿을 사용할 수 있는 경우).

1. **만들기**&#x200B;로 확인합니다.

   **구성 요소 편집** 대화 상자가 열립니다.

1. **Adobe Target 설정** 탭에 세부 정보를 입력합니다.

   * **인증**:IMS.
   * **테넌트 ID**:adobe IMS 테넌트 ID

      >[!NOTE]
      >
      >IMS의 경우 이 값을 Target 자체에서 가져와야 합니다. Target에 로그인하여 URL에서 테넌트 ID를 추출할 수 있습니다.
      >
      >예를 들어 URL이 다음과 같은 경우
      >
      >`https://experience.adobe.com/#/@yourtenantid/target/activities`
      >
      >그러면 `yourtenantid`을(를) 사용합니다.

   * **IMS 구성**:IMS 구성 이름을 선택합니다.
   * **API 유형**:REST
   * **A4T Analytics Cloud 구성**:타겟 활동 목표 및 지표에 사용되는 Analytics 클라우드 구성을 선택합니다. 컨텐츠를 타깃팅할 때 보고 소스로 Adobe Analytics을 사용하는 경우 이 기능이 필요합니다. 클라우드 구성이 표시되지 않으면 [A4T Analytics Cloud 구성](/help/sites-administering/target-configuring.md#configuring-a-t-analytics-cloud-configuration)의 참고 사항을 참조하십시오.
   * **정확한 타깃팅** 사용:기본적으로 이 확인란이 선택되어 있습니다. 이 옵션을 선택하면 클라우드 서비스 구성이 컨텍스트를 로드한 후 콘텐츠를 로드합니다. 참고 사항
   * **Adobe Target에서 세그먼트 동기화**:AEM에서 사용할 Target에 정의된 세그먼트를 다운로드하려면 이 옵션을 선택합니다. 인라인 세그먼트는 지원되지 않으며 항상 Target의 세그먼트를 사용해야 하기 때문에 API 유형 속성이 REST인 경우 이 옵션을 선택해야 합니다. &#39;segment&#39;의 AEM 용어는 &#39;audience&#39; Target과 같습니다.
   * **클라이언트 라이브러리**:AT.js 클라이언트 라이브러리를 원하는지, mbox.js(더 이상 사용되지 않음)를 원하는지 선택합니다.
   * **태그 관리 시스템을 사용하여 클라이언트 라이브러리를 제공합니다**.DTM(더 이상 사용되지 않음), Adobe 실행 또는 기타 태그 관리 시스템을 사용하십시오.
   * **사용자 지정 AT.js**:태그 관리 상자를 선택하거나 기본 AT.js를 사용하려면 비워 두십시오. 또는 사용자 지정 AT.js를 업로드합니다. AT.js를 선택한 경우에만 나타납니다.

   >[!NOTE]
   >
   >[Target Classic ](/help/sites-administering/target-configuring.md#manually-integrating-with-adobe-target) API를 사용하기 위한 Cloud Service 구성은 더 이상 사용되지 않습니다(Adobe Recommendations 설정 탭 사용).

   예:

   ![](assets/integrate-target-io-14.png)

1. **Target에 연결**&#x200B;을 클릭하여 Adobe Target과의 연결을 초기화합니다.

   연결이 성공하면 **연결 성공** 메시지가 표시됩니다.

1. 메시지에서 **OK**&#x200B;을 선택하고 대화 상자에서 **OK**&#x200B;을 선택하여 구성을 확인합니다.
1. 이제 [Target 프레임워크 추가](/help/sites-administering/target-configuring.md#adding-a-target-framework)로 진행하여 Target으로 보낼 ContextHub 또는 ClientContext 매개 변수를 구성할 수 있습니다. AEM 경험 조각을 Target으로 내보내는 경우 필요하지 않을 수 있습니다.

